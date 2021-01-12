---
title: Распространенные конфигурации NuGet
description: Файлы NuGet.Config определяют поведение NuGet как на глобальном уровне, так и на уровне отдельных проектов. Для их изменения используется команда nuget config.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: e81c380eab3f1a8635e50e62811c7ae463ec3653
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699776"
---
# <a name="common-nuget-configurations"></a>Распространенные конфигурации NuGet

Поведение NuGet определяется совокупностью параметров в одном или нескольких файлах `NuGet.Config` формата XML, которые могут существовать на уровне проекта, пользователя и компьютера. Кроме того, используется глобальный файл `NuGetDefaults.Config`, определяющий конфигурацию источников пакетов. Параметры применяются ко всем командам, выполняемым в интерфейсе командной строки, консоли диспетчера пакетов и пользовательском интерфейсе диспетчера пакетов.

## <a name="config-file-locations-and-uses"></a>Расположение и использование файла конфигурации

| Область | Расположение файла NuGet.Config | Описание |
| --- | --- | --- |
| Решение | Текущая папка (т. е. папка решения) или любая другая папка вплоть до уровня корня диска.| Параметры папки решения применяются ко всем проектам во вложенных папках. Обратите внимание, что если файл конфигурации помещен в папку проекта, он никоим образом не влияет на проект. |
| Пользовательская | **Windows:** `%appdata%\NuGet\NuGet.Config`<br/>**Mac/Linux:** `~/.config/NuGet/NuGet.Config` или `~/.nuget/NuGet/NuGet.Config` (зависит от дистрибутива ОС) <br/>Дополнительные конфигурации поддерживаются на всех платформах. Эти конфигурации нельзя изменить с помощью инструментов. </br> **Windows:** `%appdata%\NuGet\config\*.Config` <br/>**Mac/Linux:** `~/.config/NuGet/config/*.config` или `~/.nuget/config/*.config` | Параметры применяются ко всем операциям, но переопределяются любыми параметрами, задаваемыми на уровне проекта. |
| Компьютер | **Windows:** `%ProgramFiles(x86)%\NuGet\Config`<br/>**Mac/Linux:** `$XDG_DATA_HOME`. Если значение `$XDG_DATA_HOME` — null или пусто, будет использоваться `~/.local/share` или `/usr/local/share` (зависит от дистрибутива ОС)  | Параметры применяются ко всем операциям на компьютере, но переопределяются любыми параметрами, задаваемыми на уровне пользователя или проекта. |

Примечания для более ранних версий NuGet:
- В NuGet 3.3 и более ранних версий параметры уровня решения располагались в папке `.nuget`. В NuGet версии 3.4 и более поздних эта папка не используется.
- В версиях NuGet с 2.6 по 3.x файл конфигурации уровня компьютера для Windows располагался в папке %ProgramData%\NuGet\Config[\\{IDE}[\\{версия}[\\{SKU}]]]\NuGet.Config, где атрибут *{IDE}* мог иметь значение *VisualStudio*, атрибут *{версия}* указывал на версию Visual Studio, например *14.0*, а атрибут *{SKU}* определял выпуск *Community*, *Pro* или *Enterprise*. Чтобы перенести параметры в NuGet версии 4.0 или более поздней, просто скопируйте файл конфигурации в папку %ProgramFiles(x86)%\NuGet\Config. В Linux ранее использовалось расположение /etc/opt, а в Mac — /Library/Application Support.

## <a name="changing-config-settings"></a>Изменение параметров конфигурации

Файл `NuGet.Config` представляет собой простой текстовый файл в формате XML, который содержит пары ключей и значений, описываемые в разделе [Параметры конфигурации NuGet](../reference/nuget-config-file.md).

Управление параметрами осуществляется с помощью команды [config command](../reference/cli-reference/cli-ref-config.md) интерфейса командной строки NuGet:
- По умолчанию изменения вносятся в файл конфигурации уровня пользователя.
- Для изменения параметров в другом файле используйте параметр `-configFile`. В таком случае файлы могут иметь любые имена.
- Ключи всегда задаются с учетом регистра символов.
- Для изменения параметров в файле уровня компьютера требуется повышение прав.

> [!Warning]
> Файл конфигурации можно изменять в любом редакторе, однако если он будет содержать неправильно сформированный код XML (несоответствующие теги, неправильно используемые кавычки и т. д.), NuGet (версии 3.4.3 и более поздней) будет полностью игнорировать его без выдачи каких-либо уведомлений. Поэтому для управления параметрами рекомендуется использовать команду `nuget config`.

### <a name="setting-a-value"></a>Настройка значения

Windows:

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

Mac/Linux:

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> В NuGet 3.4 и более поздних версий можно использовать в любом значении переменные среды, такие как `repositoryPath=%PACKAGEHOME%` (Windows) и `repositoryPath=$PACKAGEHOME` (Mac/Linux).

### <a name="removing-a-value"></a>Удаление значения

Чтобы удалить значение, укажите ключ с пустым значением.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Создание нового файла конфигурации

Скопируйте представленный ниже шаблон в новый файл и затем присвойте значения с помощью `nuget config -configFile <filename>`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Порядок применения параметров

Благодаря применению нескольких файлов `NuGet.Config` вы можете хранить параметры в различных местах так, чтобы они применялись к отдельному проекту, группе проектов или всем проектам. Эти параметры совместно применяются к любым операциям NuGet, которые вызываются из командной строки или из среды Visual Studio. Приоритет при этом имеют параметры, которые находятся на уровне, ближайшем к проекту или текущей папке.

В частности, NuGet загружает параметры из различных файлов конфигурации в следующем порядке:

1. [Файл NuGetDefaults.Config](#nuget-defaults-file), который содержит параметры, относящиеся только к источникам пакетов.
1. Файл уровня компьютера.
1. Файл уровня пользователя.
1. Файл, заданный параметром `-configFile`.
1. Файлы, найденные в каждой папке по пути от корня диска к текущей папке (папка, из которой была вызвана команда nuget.exe, или папка, содержащая проект Visual Studio). Например, при вызове команды в папке "c:\A\B\C" NuGet ищет и загружает файлы конфигурации сначала по пути "c:\,", затем "c:\A", затем "c:\A\B" и, наконец, "c:\A\B\C".

Параметры, найденные в этих файлах, NuGet применяет следующим образом:

1. Для элементов, состоящих из одного компонента, NuGet заменяет любое ранее найденное значение с тем же ключом. Это означает, что параметры, найденные на самом близком к текущей папке или проекту уровне, переопределяют любые ранее найденные параметры. Например, параметр `defaultPushSource` в файле `NuGetDefaults.Config` будет переопределен аналогичным параметром, найденным в любом другом файле конфигурации.

1. Для элементов коллекции (таких как `<packageSources>`) NuGet объединяет значения из всех файлов конфигурации в одну коллекцию.

1. Если для заданного узла указан параметр `<clear />`, NuGet игнорирует ранее определенные значения конфигурации для этого узла.

### <a name="settings-walkthrough"></a>Пошаговое руководство по параметрам

Допустим, у вас есть следующая структура папок на двух отдельных дисках:

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

В показанных ниже расположениях присутствует четыре файла `NuGet.Config` со следующим содержимым. (В этот пример не включен файл уровня компьютера, поведение которого аналогично файлу уровня пользователя.)

Файл А. Файл на уровне пользователей (`%appdata%\NuGet\NuGet.Config` в Windows, `~/.config/NuGet/NuGet.Config` в Mac и Linux):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

Файл Б. disk_drive_2/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="disk_drive_2/tmp" />
    </config>
    <packageRestore>
        <add key="enabled" value="True" />
    </packageRestore>
</configuration>
```

Файл В. disk_drive_2/Project1/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="External/Packages" />
        <add key="defaultPushSource" value="https://MyPrivateRepo/ES/api/v2/package" />
    </config>
    <packageSources>
        <clear /> <!-- ensure only the sources defined below are used -->
        <add key="MyPrivateRepo - ES" value="https://MyPrivateRepo/ES/nuget" />
    </packageSources>
</configuration>
```

Файл Г. disk_drive_2/Project2/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

Затем NuGet загружает и применяет параметры следующим образом, в зависимости от места вызова:

- **Вызов из disk_drive_1/users**. Используется только репозиторий по умолчанию, представленный в файле конфигурации уровня пользователя (А), поскольку это единственный файл, найденный по пути disk_drive_1.

- **Вызов из disk_drive_2/ или disk_drive_/tmp**. Сначала загружается файл уровня пользователя (А), а затем NuGet переходит в корень disk_drive_2 и находит файл (Б). Кроме того, NuGet также ищет файл конфигурации в папке /tmp, но не находит его. В результате используется репозиторий по умолчанию на веб-сайте nuget.org, включается восстановление пакетов и пакеты развертываются в папке disk_drive_2/tmp.

- **Вызов из disk_drive_2/Project1 или disk_drive_2/Project1/Source**. Сначала загружается файл уровня пользователя (А), затем NuGet загружает файл (Б) из корня disk_drive_2, после чего загружается файл (В). Параметры в файле (В) переопределяют параметры в файлах (Б) и (А), поэтому путь `repositoryPath`, по которому устанавливаются пакеты, будет иметь вид disk_drive_2/Project1/External/Packages вместо *disk_drive_2/tmp*. Кроме того, поскольку файл (В) очищает `<packageSources>`, веб-сайт nuget.org будет недоступен в качестве источника, и останется только `https://MyPrivateRepo/ES/nuget`.

- **Вызов из disk_drive_2/Project2 или disk_drive_2/Project2/Source**. Сначала загружается файл уровня пользователя (А), а затем файл (Б) и файл (Г). Поскольку `packageSources` не очищается, в качестве источников будут доступны одновременно `nuget.org` и `https://MyPrivateRepo/DQ/nuget`. Пакеты развертываются по пути disk_drive_2/tmp, заданному в файле (Б).

## <a name="additional-user-wide-configuration"></a>Дополнительная конфигурация на уровне пользователя

Начиная с версии 5.7 в NuGet появилась поддержка дополнительных файлов конфигурации на уровне пользователя. Это позволяет сторонним поставщикам добавлять дополнительные пользовательские файлы конфигурации без повышения прав.
Эти файлы конфигурации находятся в стандартной пользовательской папке конфигурации в подпапке `config`.
Будут учитываться все файлы, которые имеют расширение `.config` или `.Config`.
Эти файлы нельзя изменить стандартными инструментами.

| Платформа ОС  | Дополнительные конфигурации |
| --- | --- |
| Windows      | `%appdata%\NuGet\config\*.Config` |
| Mac/Linux    | `~/.config/NuGet/config/*.config` или `~/.nuget/config/*.config` |

## <a name="nuget-defaults-file"></a>Файл параметров по умолчанию NuGet

Файл `NuGetDefaults.Config` задает источники пакетов, из которых устанавливаются и обновляются пакеты, а также определяет целевой объект по умолчанию для публикации пакетов с использованием команды `nuget push`. Так как администраторы могут без усилий согласованно развертывать файлы `NuGetDefaults.Config` на компьютерах разработки и построения (например, с использованием групповой политики), они могут гарантировать то, что все пользователи организации будут иметь правильные источники пакетов вместо веб-сайта nuget.org.

> [!Important]
> Файл `NuGetDefaults.Config` никогда не вызывает удаление источника пакетов из конфигурации NuGet разработчика. Это означает, что если разработчик уже использовал NuGet и для него зарегистрирован источник пакетов nuget.org, он не будет использован после создания файла `NuGetDefaults.Config`.
>
> Кроме того, ни файл `NuGetDefaults.Config`, ни любой другой механизм в NuGet не могут предотвратить доступ к таким источникам пакетов, как nuget.org. Если организации требуется заблокировать доступ, необходимо использовать другие способы, например брандмауэры.

### <a name="nugetdefaultsconfig-location"></a>Расположение файла NuGetDefaults.Config

В следующей таблице указано, где следует хранить файл `NuGetDefaults.Config` в зависимости от целевой ОС.

| Платформа ОС  | Расположение файла NuGetDefaults.Config |
| --- | --- |
| Windows      | **Visual Studio 2017 или NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 или более ранней версии либо NuGet 3.x или более ранней версии:** `%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME` (обычно `~/.local/share` или `/usr/local/share`, в зависимости от дистрибутива ОС)|

### <a name="nugetdefaultsconfig-settings"></a>Параметры в файле NuGetDefaults.Config

- `packageSources`. Эта коллекция имеет то же значение, что и `packageSources` в обычных файлах конфигурации и задает источники по умолчанию. NuGet использует эти источники в указанном порядке при установке или обновлении пакетов в проектах с помощью формата управления `packages.config`. Для проектов, в которых используется формат PackageReference, NuGet сначала использует локальные источники, затем — источники в сетевых папках, а после этого — HTTP-источники, независимо от порядка, заданного в файлах конфигурации. NuGet всегда игнорирует порядок источников при операциях восстановления.

- `disabledPackageSources`. Эта коллекция также имеет то же значение, что и в файлах `NuGet.Config`, где каждый затрагиваемый источник перечислен по имени и значению true/false, указывающему, включен он или отключен. Это позволяет сохранять имя и URL-адрес источника в `packageSources`, не включая его по умолчанию. Отдельные разработчики при необходимости могут повторно включить источник, присвоив параметру источника значение false в других файлах `NuGet.Config`, не выполняя повторный поиск правильного URL-адреса. Также рекомендуется предоставить разработчикам полный список URL-адресов внутренних источников для организации, но включить по умолчанию только источник для отдельной группы.

- `defaultPushSource`: задает целевой объект по умолчанию для операций `nuget push`, переопределяя встроенное значение по умолчанию nuget.org. Администраторы могут развертывать этот параметр, чтобы избежать случайной публикации внутренних пакетов на открытом веб-сайте nuget.org, поскольку разработчикам придется специально использовать команду `nuget push -Source` для публикации на веб-сайте nuget.org.

### <a name="example-nugetdefaultsconfig-and-application"></a>Пример файла NuGetDefaults.Config и приложения

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!-- defaultPushSource key works like the 'defaultPushSource' key of NuGet.Config files. -->
    <!-- This can be used by administrators to prevent accidental publishing of packages to nuget.org. -->
    <config>
        <add key="defaultPushSource" value="https://contoso.com/packages/" />
    </config>

    <!-- Default Package Sources; works like the 'packageSources' section of NuGet.Config files. -->
    <!-- This collection cannot be deleted or modified but can be disabled/enabled by users. -->
    <packageSources>
        <add key="Contoso Package Source" value="https://contoso.com/packages/" />
        <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
    </packageSources>

    <!-- Default Package Sources that are disabled by default. -->
    <!-- Works like the 'disabledPackageSources' section of NuGet.Config files. -->
    <!-- Sources cannot be modified or deleted either but can be enabled/disabled by users. -->
    <disabledPackageSources>
        <add key="nuget.org" value="true" />
    </disabledPackageSources>
</configuration>
```
