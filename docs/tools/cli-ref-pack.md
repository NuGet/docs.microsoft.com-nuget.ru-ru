---
title: Команда интерфейса командной строки NuGet pack
description: Справочник по командам пакет nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b5bd8bd30ad134f36433b8e4721ce131425a1483
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453368"
---
# <a name="pack-command-nuget-cli"></a>Команда pack (NuGet CLI)

**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** 2.7 +

Создает пакет NuGet на основе указанного `.nuspec` или файла проекта. `dotnet pack` Команды (см. в разделе [команды dotnet](dotnet-Commands.md)) и `msbuild -t:pack` (см. в разделе [целевых объектов MSBuild](../reference/msbuild-targets.md)) может использоваться в качестве альтернативы.

> [!Important]
> В рамках проекта Mono Создание пакета из файла проекта не поддерживается. Необходимо также настроить пути не являющейся локальной в `.nuspec` файла в пути в формате Unix, а nuget.exe не преобразует пути Windows, сам.

## <a name="usage"></a>Использование

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

где `<nuspecPath>` и `<projectPath>` укажите `.nuspec` или файла проекта соответственно.

## <a name="options"></a>Параметры

| Параметр | Описание: |
| --- | --- |
| BasePath | Задает базовый путь к файлам, определенным в `.nuspec` файл. |
| Построить | Указывает, что проект должен быть создан перед созданием пакета. |
| Исключить | Указывает один или несколько шаблонов с подстановочными знаками для исключения при создании пакета. Чтобы указать несколько шаблонов, повторите флаг - исключения. См. пример ниже. |
| ExcludeEmptyDirectories | Предотвращает включение пустые каталоги, при сборке пакета. |
| ForceEnglishOutput | *(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры. |
| ConfigFile | Укажите файл конфигурации для команды pack. |
| Справка | Отображает справку для команды. |
| IncludeReferencedProjects | Указывает, что встроенный пакет должен включать упоминаемые проекты как зависимости или как часть пакета. Если у упоминаемого проекта есть соответствующий `.nuspec` файл, который имеет имя, совпадающее с именем проекта, а затем этот проект добавляется в качестве зависимости. В противном случае проект добавляется как часть пакета. |
| MinClientVersion | Задайте *minClientVersion* атрибут для созданного пакета. Это значение будет переопределять значение существующего *minClientVersion* атрибута (если таковые имеются) в `.nuspec` файл. |
| MSBuildPath | *(4.0 и более поздние)*  Указывает путь к MSBuild для использования с командой, имеют приоритет перед `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 и более поздние)*  Указывает версию MSBuild для использования с помощью следующей команды. Поддерживаемые значения: 4, 12, 14, 15. По умолчанию выбирается MSBuild в пути в противном случае по умолчанию установленных самую новую версию MSBuild. |
| NoDefaultExcludes | Предотвращает исключения по умолчанию NuGet упаковать файлы и файлы и папки, начиная с точки, такие как `.svn` и `.gitignore`. |
| NoPackageAnalysis | Указывает, что пакету не нужно запускать анализ пакета после его сборки. |
| OutputDirectory | Указывает папку, в которой будет храниться созданный пакет. Если папка не указана, используется текущая папка. |
| Свойства | Последний в командной строке через появятся другие параметры. Указывает список свойств, которые переопределяют значения в файле проекта; см. в разделе [общие свойства проектов MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) для имен свойств. Аргументе свойств приведен список маркер = пар "значение", разделенных точкой с запятой, где каждое вхождение `$token$` в `.nuspec` файл будет заменен на заданное значение. Значения могут быть строки в кавычках. Обратите внимание, что для свойства «Конфигурация», значение по умолчанию «Debug». Чтобы изменить конфигурацию выпуска, используйте `-Properties Configuration=Release`. |
| Суффикс | *(3.4.4+)*  Добавляет суффикс для созданного внутреннего номер_версии, обычно используется для добавления сборки или другие идентификаторы предварительной версии. Например, с помощью `-suffix nightly` создаст пакет с like номера версии `1.2.3-nightly`. Суффиксы должны начинаться с буквы, чтобы избежать предупреждения, ошибки и потенциальных несовместимости с различными версиями NuGet и диспетчер пакетов NuGet. |
| Символы | Указывает, что пакет содержит источники и символы. При использовании с `.nuspec` файл, это создает обычный файл пакета NuGet и соответствующий пакет символов. По умолчанию она создает [пакета устаревших символов](../create-packages/Symbol-Packages.md). Новый рекомендуемый формат для пакетов символов — .snupkg. См. раздел [Создание пакетов символов (.snupkg)](../create-packages/Symbol-Packages-snupkg.md). |
| Средство | Указывает, что следует поместить выходные файлы проекта в `tool` папку. |
| Уровень детализации | Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*. |
| Версия | Переопределяет номер версии из `.nuspec` файла. |

Также см. в разделе [переменные среды](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>За исключением зависимости разработки

Некоторые пакеты NuGet полезны в качестве зависимости разработки, которые помогут вам создать свою собственную библиотеку, но не обязательно нужны как зависимости самого пакета.

`pack` Команда будет игнорировать `package` записей в `packages.config` , имеющих `developmentDependency` атрибут `true`. Эти записи не будут включены в качестве зависимостей в созданный пакет.

Например, рассмотрим следующие `packages.config` файл в исходном проекте:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Для этого проекта, пакет создан `nuget pack` будет зависят от `jQuery` и `microsoft-web-helpers` , но не `netfx-Guard`.

## <a name="examples"></a>Примеры

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
