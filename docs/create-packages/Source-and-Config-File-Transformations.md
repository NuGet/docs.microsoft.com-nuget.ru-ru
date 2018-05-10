---
title: Преобразования исходного кода и файла конфигурации для пакетов NuGet
description: Сведения о возможности преобразования исходного кода и файлов конфигурации в формате XML для пакетов NuGet при установке.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 863bf22780313a34690617dd6a1604531272808b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="transforming-source-code-and-configuration-files"></a>Преобразования исходного кода и файлов конфигурации

Для проектов, использующих `packages.config`, NuGet поддерживает возможность выполнять преобразования исходного кода и файлов конфигурации при установке или удалении пакета. При установке пакета в проект с использованием [PackageReference](../consume-packages/package-references-in-project-files.md) применяются только преобразования исходного кода.

**Преобразование исходного кода** применяет одностороннюю замену токена к файлам в папке `content` или `contentFiles` пакета при установке пакета (`content` для клиентов, использующих `packages.config` и `contentFiles` для `PackageReference`) в тех случаях, когда токены ссылаются на [свойства проекта](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) Visual Studio. Это позволяет вставить файл в пространство имен проекта или настроить код, который обычно обращается к `global.asax` в проекте ASP.NET.

**Преобразование файла конфигурации** позволяет изменять файлы, уже существующие в целевом проекте, такие как `web.config` и `app.config`. Например, для пакета может потребоваться добавить элемент в раздел `modules` файла конфигурации. Это преобразование осуществляется путем включения в пакет особых файлов, которые описывают разделы, добавляемые в файлы конфигурации. При удалении пакета внесенные изменения отменяются, благодаря чему это преобразование является двусторонним.

## <a name="specifying-source-code-transformations"></a>Определение преобразований исходного кода

1. Файлы, которые требуется вставить в проект из пакета, должны располагаться в папках `content` и `contentFiles` пакета. Например, если требуется установить файл `ContosoData.cs` в папку `Models` целевого проекта, этот файл должен находиться в папках `content\Models` и `contentFiles\{lang}\{tfm}\Models` пакета.

1. Чтобы задать в NuGet инструкцию для применения замены маркера во время установки, добавьте к имени файла исходного кода расширение `.pp`. После установки расширение `.pp` у файла будет удалено.

    Например, чтобы выполнить преобразования в `ContosoData.cs`, присвойте файлу в пакете имя `ContosoData.cs.pp`. После установки он будет иметь имя `ContosoData.cs`.

1. В файле исходного кода используйте маркеры без учета регистра символов вида `$token$`, чтобы указать значения, которые NuGet будет заменять свойствами проекта:

    ```cs
    namespace $rootnamespace$.Models
    {
        public struct CategoryInfo
        {
            public string categoryid;
            public string description;
            public string htmlUrl;
            public string rssUrl;
            public string title;
        }
    }
    ```

    При установке NuGet заменяет `$rootnamespace$` на `Fabrikam`, используя свойства целевого проекта, корневым пространством имен которого является `Fabrikam`.

Маркер `$rootnamespace$` является одним из самых часто используемых свойств проекта. Остальные маркеры перечислены в статье [ProjectProperties Interface](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) (Интерфейс ProjectProperties). Естественно, необходимо учитывать, что некоторые свойства могут зависеть от типа проекта.

## <a name="specifying-config-file-transformations"></a>Определение преобразований файла конфигурации

Как описывается в следующих разделах, преобразования файла конфигурации могут быть выполнены двумя способами:

- Включите файлы `app.config.transform` и `web.config.transform` в папку `content` пакета. Расширение `.transform` указывает NuGet на то, что эти файлы содержат XML-код, который следует добавить в файлы конфигурации при установке пакета. При удалении пакета такой XML-код также удаляется.
- Включите файлы `app.config.install.xdt` и `web.config.install.xdt` в папку `content` пакета, используя [синтаксис XDT](https://msdn.microsoft.com/library/dd465326.aspx) для описания необходимых изменений. В этом случае также можно включить файл `.uninstall.xdt`, который необходим для отмены изменений при удалении пакета из проекта.

> [!Note]
> Преобразования не применяются к файлам `.config`, на которые задаются ссылки в Visual Studio.

Преимуществом использования XDT является то, что вместо простого объединения двух файлов предоставляется синтаксис для операций со структурой модели DOM XML с использованием элемента и атрибута, соответствующих применению полной поддержки XPath. XDT позволяет добавлять, обновлять и удалять элементы, помещать новые элементы в конкретное место, а также заменять или удалять элементы (включая дочерние узлы). Это позволяет легко создавать преобразования при удалении, которые обеспечивают отмену всех преобразований, выполненных во время установки пакета.

### <a name="xml-transforms"></a>Преобразования XML

Файлы `app.config.transform` и `web.config.transform` в папке `content` пакета содержат только те элементы, которые будут добавлены в существующие файлы `app.config` и `web.config` проекта.

Допустим, файл `web.config` проекта изначально имеет следующее содержимое:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Чтобы добавить элемент `MyNuModule` в раздел `modules` во время установки пакета, создайте файл `web.config.transform` в папке `content` пакета, который будет иметь следующий вид:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

После того как NuGet установит пакет, файл `web.config` будет иметь следующий вид:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Обратите внимание, что NuGet не заменяет раздел `modules`, а добавляет в него новую запись с новыми элементами и атрибутами. NuGet не изменяет какие-либо существующие элементы или атрибуты.

При удалении пакета NuGet снова проверяет файлы `.transform` и удаляет содержащиеся в них элементы из соответствующих файлов `.config`. Обратите внимание, что этот процесс не затрагивает строки файла `.config`, которые были изменены после установки пакета.

В качестве расширенного примера можно привести пакет [модулей ведения журнала и обработки ошибок ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/), который добавляет множество записей в файл `web.config`. При удалении пакета эти записи будут удалены.

Чтобы изучить соответствующий файл `web.config.transform`, скачайте пакет ELMAH по приведенной выше ссылке, измените расширение пакета с `.nupkg` на `.zip`, после чего откройте файл `content\web.config.transform`, содержащийся в этом ZIP-файле.

Чтобы просмотреть последствия установки и удаления пакета, создайте в Visual Studio новый проект ASP.NET (шаблон в разделе **Visual C# > Интернет** диалогового окна "Новый проект") и выберите приложение ASP.NET. Откройте файл `web.config`, чтобы просмотреть его первоначальное состояние. Щелкните проект правой кнопкой мыши, выберите пункт **Управление пакетами NuGet**, перейдите к пакету ELMAH на веб-сайте nuget.org и установите его последнюю версию. Обратите внимание на все изменения в файле `web.config`. Удалите пакет. Вы увидите, что было восстановлено исходное состояние файла `web.config`.

### <a name="xdt-transforms"></a>Преобразования XDT

Вы можете изменять файлы конфигурации с помощью [синтаксиса XDT](https://msdn.microsoft.com/library/dd465326.aspx). Кроме того, NuGet может заменять маркеры [свойствами проекта](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7), включая имена свойств с разделителями `$` (без учета регистра символов).

Например, следующий файл `app.config.install.xdt` вставит элемент `appSettings` в файл `app.config`, содержащий значения `FullPath`, `FileName` и `ActiveConfigurationSettings` из проекта:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <appSettings xdt:Transform="Insert">
        <add key="FullPath" value="$FullPath$" />
        <add key="FileName" value="$filename$" />
        <add key="ActiveConfigurationSettings " value="$ActiveConfigurationSettings$" />
    </appSettings>
</configuration>
```

Предположим, файл `web.config` проекта изначально имеет следующее содержимое:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Чтобы добавить элемент `MyNuModule` в раздел `modules` при установке пакета, файл `web.config.install.xdt` пакета должен иметь следующее содержимое:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" xdt:Transform="Insert" />
        </modules>
    </system.webServer>
</configuration>
```

После установки пакета файл `web.config` будет иметь следующий вид:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Чтобы удалить только элемент `MyNuModule` во время удаления пакета, файл `web.config.uninstall.xdt` должен иметь следующее содержимое:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" xdt:Transform="Remove" xdt:Locator="Match(name)" />
        </modules>
    </system.webServer>
</configuration>
```
