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
# <a name="common-nuget-configurations"></a><span data-ttu-id="99f21-103">Распространенные конфигурации NuGet</span><span class="sxs-lookup"><span data-stu-id="99f21-103">Common NuGet configurations</span></span>

<span data-ttu-id="99f21-104">Поведение NuGet определяется совокупностью параметров в одном или нескольких файлах `NuGet.Config` формата XML, которые могут существовать на уровне проекта, пользователя и компьютера.</span><span class="sxs-lookup"><span data-stu-id="99f21-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="99f21-105">Кроме того, используется глобальный файл `NuGetDefaults.Config`, определяющий конфигурацию источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="99f21-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="99f21-106">Параметры применяются ко всем командам, выполняемым в интерфейсе командной строки, консоли диспетчера пакетов и пользовательском интерфейсе диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="99f21-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="99f21-107">Расположение и использование файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="99f21-107">Config file locations and uses</span></span>

| <span data-ttu-id="99f21-108">Область</span><span class="sxs-lookup"><span data-stu-id="99f21-108">Scope</span></span> | <span data-ttu-id="99f21-109">Расположение файла NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="99f21-109">NuGet.Config file location</span></span> | <span data-ttu-id="99f21-110">Описание</span><span class="sxs-lookup"><span data-stu-id="99f21-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="99f21-111">Решение</span><span class="sxs-lookup"><span data-stu-id="99f21-111">Solution</span></span> | <span data-ttu-id="99f21-112">Текущая папка (т. е. папка решения) или любая другая папка вплоть до уровня корня диска.</span><span class="sxs-lookup"><span data-stu-id="99f21-112">Current folder (aka Solution folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="99f21-113">Параметры папки решения применяются ко всем проектам во вложенных папках.</span><span class="sxs-lookup"><span data-stu-id="99f21-113">In a solution folder, settings apply to all projects in subfolders.</span></span> <span data-ttu-id="99f21-114">Обратите внимание, что если файл конфигурации помещен в папку проекта, он никоим образом не влияет на проект.</span><span class="sxs-lookup"><span data-stu-id="99f21-114">Note that if a config file is placed in a project folder, it has no effect on that project.</span></span> |
| <span data-ttu-id="99f21-115">Пользовательская</span><span class="sxs-lookup"><span data-stu-id="99f21-115">User</span></span> | <span data-ttu-id="99f21-116">**Windows:** `%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="99f21-116">**Windows:** `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="99f21-117">**Mac/Linux:** `~/.config/NuGet/NuGet.Config` или `~/.nuget/NuGet/NuGet.Config` (зависит от дистрибутива ОС)</span><span class="sxs-lookup"><span data-stu-id="99f21-117">**Mac/Linux:** `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> <br/><span data-ttu-id="99f21-118">Дополнительные конфигурации поддерживаются на всех платформах.</span><span class="sxs-lookup"><span data-stu-id="99f21-118">Additional configs are supported on all platforms.</span></span> <span data-ttu-id="99f21-119">Эти конфигурации нельзя изменить с помощью инструментов.</span><span class="sxs-lookup"><span data-stu-id="99f21-119">These configs cannot be edited by the tooling.</span></span> </br> <span data-ttu-id="99f21-120">**Windows:** `%appdata%\NuGet\config\*.Config`</span><span class="sxs-lookup"><span data-stu-id="99f21-120">**Windows:** `%appdata%\NuGet\config\*.Config`</span></span> <br/><span data-ttu-id="99f21-121">**Mac/Linux:** `~/.config/NuGet/config/*.config` или `~/.nuget/config/*.config`</span><span class="sxs-lookup"><span data-stu-id="99f21-121">**Mac/Linux:** `~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span></span> | <span data-ttu-id="99f21-122">Параметры применяются ко всем операциям, но переопределяются любыми параметрами, задаваемыми на уровне проекта.</span><span class="sxs-lookup"><span data-stu-id="99f21-122">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="99f21-123">Компьютер</span><span class="sxs-lookup"><span data-stu-id="99f21-123">Computer</span></span> | <span data-ttu-id="99f21-124">**Windows:** `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="99f21-124">**Windows:** `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="99f21-125">**Mac/Linux:** `$XDG_DATA_HOME`.</span><span class="sxs-lookup"><span data-stu-id="99f21-125">**Mac/Linux:** `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="99f21-126">Если значение `$XDG_DATA_HOME` — null или пусто, будет использоваться `~/.local/share` или `/usr/local/share` (зависит от дистрибутива ОС)</span><span class="sxs-lookup"><span data-stu-id="99f21-126">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="99f21-127">Параметры применяются ко всем операциям на компьютере, но переопределяются любыми параметрами, задаваемыми на уровне пользователя или проекта.</span><span class="sxs-lookup"><span data-stu-id="99f21-127">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="99f21-128">Примечания для более ранних версий NuGet:</span><span class="sxs-lookup"><span data-stu-id="99f21-128">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="99f21-129">В NuGet 3.3 и более ранних версий параметры уровня решения располагались в папке `.nuget`.</span><span class="sxs-lookup"><span data-stu-id="99f21-129">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="99f21-130">В NuGet версии 3.4 и более поздних эта папка не используется.</span><span class="sxs-lookup"><span data-stu-id="99f21-130">This folder is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="99f21-131">В версиях NuGet с 2.6 по 3.x файл конфигурации уровня компьютера для Windows располагался в папке %ProgramData%\NuGet\Config[\\{IDE}[\\{версия}[\\{SKU}]]]\NuGet.Config, где атрибут *{IDE}* мог иметь значение *VisualStudio*, атрибут *{версия}* указывал на версию Visual Studio, например *14.0*, а атрибут *{SKU}* определял выпуск *Community*, *Pro* или *Enterprise*.</span><span class="sxs-lookup"><span data-stu-id="99f21-131">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="99f21-132">Чтобы перенести параметры в NuGet версии 4.0 или более поздней, просто скопируйте файл конфигурации в папку %ProgramFiles(x86)%\NuGet\Config. В Linux ранее использовалось расположение /etc/opt, а в Mac — /Library/Application Support.</span><span class="sxs-lookup"><span data-stu-id="99f21-132">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="99f21-133">Изменение параметров конфигурации</span><span class="sxs-lookup"><span data-stu-id="99f21-133">Changing config settings</span></span>

<span data-ttu-id="99f21-134">Файл `NuGet.Config` представляет собой простой текстовый файл в формате XML, который содержит пары ключей и значений, описываемые в разделе [Параметры конфигурации NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="99f21-134">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="99f21-135">Управление параметрами осуществляется с помощью команды [config command](../reference/cli-reference/cli-ref-config.md) интерфейса командной строки NuGet:</span><span class="sxs-lookup"><span data-stu-id="99f21-135">Settings are managed using the NuGet CLI [config command](../reference/cli-reference/cli-ref-config.md):</span></span>
- <span data-ttu-id="99f21-136">По умолчанию изменения вносятся в файл конфигурации уровня пользователя.</span><span class="sxs-lookup"><span data-stu-id="99f21-136">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="99f21-137">Для изменения параметров в другом файле используйте параметр `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="99f21-137">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="99f21-138">В таком случае файлы могут иметь любые имена.</span><span class="sxs-lookup"><span data-stu-id="99f21-138">In this case files can use any filename.</span></span>
- <span data-ttu-id="99f21-139">Ключи всегда задаются с учетом регистра символов.</span><span class="sxs-lookup"><span data-stu-id="99f21-139">Keys are always case sensitive.</span></span>
- <span data-ttu-id="99f21-140">Для изменения параметров в файле уровня компьютера требуется повышение прав.</span><span class="sxs-lookup"><span data-stu-id="99f21-140">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="99f21-141">Файл конфигурации можно изменять в любом редакторе, однако если он будет содержать неправильно сформированный код XML (несоответствующие теги, неправильно используемые кавычки и т. д.), NuGet (версии 3.4.3 и более поздней) будет полностью игнорировать его без выдачи каких-либо уведомлений.</span><span class="sxs-lookup"><span data-stu-id="99f21-141">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="99f21-142">Поэтому для управления параметрами рекомендуется использовать команду `nuget config`.</span><span class="sxs-lookup"><span data-stu-id="99f21-142">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="99f21-143">Настройка значения</span><span class="sxs-lookup"><span data-stu-id="99f21-143">Setting a value</span></span>

<span data-ttu-id="99f21-144">Windows:</span><span class="sxs-lookup"><span data-stu-id="99f21-144">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="99f21-145">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="99f21-145">Mac/Linux:</span></span>

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
> <span data-ttu-id="99f21-146">В NuGet 3.4 и более поздних версий можно использовать в любом значении переменные среды, такие как `repositoryPath=%PACKAGEHOME%` (Windows) и `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="99f21-146">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="99f21-147">Удаление значения</span><span class="sxs-lookup"><span data-stu-id="99f21-147">Removing a value</span></span>

<span data-ttu-id="99f21-148">Чтобы удалить значение, укажите ключ с пустым значением.</span><span class="sxs-lookup"><span data-stu-id="99f21-148">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="99f21-149">Создание нового файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="99f21-149">Creating a new config file</span></span>

<span data-ttu-id="99f21-150">Скопируйте представленный ниже шаблон в новый файл и затем присвойте значения с помощью `nuget config -configFile <filename>`:</span><span class="sxs-lookup"><span data-stu-id="99f21-150">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="99f21-151">Порядок применения параметров</span><span class="sxs-lookup"><span data-stu-id="99f21-151">How settings are applied</span></span>

<span data-ttu-id="99f21-152">Благодаря применению нескольких файлов `NuGet.Config` вы можете хранить параметры в различных местах так, чтобы они применялись к отдельному проекту, группе проектов или всем проектам.</span><span class="sxs-lookup"><span data-stu-id="99f21-152">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="99f21-153">Эти параметры совместно применяются к любым операциям NuGet, которые вызываются из командной строки или из среды Visual Studio. Приоритет при этом имеют параметры, которые находятся на уровне, ближайшем к проекту или текущей папке.</span><span class="sxs-lookup"><span data-stu-id="99f21-153">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="99f21-154">В частности, NuGet загружает параметры из различных файлов конфигурации в следующем порядке:</span><span class="sxs-lookup"><span data-stu-id="99f21-154">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="99f21-155">[Файл NuGetDefaults.Config](#nuget-defaults-file), который содержит параметры, относящиеся только к источникам пакетов.</span><span class="sxs-lookup"><span data-stu-id="99f21-155">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="99f21-156">Файл уровня компьютера.</span><span class="sxs-lookup"><span data-stu-id="99f21-156">The computer-level file.</span></span>
1. <span data-ttu-id="99f21-157">Файл уровня пользователя.</span><span class="sxs-lookup"><span data-stu-id="99f21-157">The user-level file.</span></span>
1. <span data-ttu-id="99f21-158">Файл, заданный параметром `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="99f21-158">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="99f21-159">Файлы, найденные в каждой папке по пути от корня диска к текущей папке (папка, из которой была вызвана команда nuget.exe, или папка, содержащая проект Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="99f21-159">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="99f21-160">Например, при вызове команды в папке "c:\A\B\C" NuGet ищет и загружает файлы конфигурации сначала по пути "c:\,", затем "c:\A", затем "c:\A\B" и, наконец, "c:\A\B\C".</span><span class="sxs-lookup"><span data-stu-id="99f21-160">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="99f21-161">Параметры, найденные в этих файлах, NuGet применяет следующим образом:</span><span class="sxs-lookup"><span data-stu-id="99f21-161">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="99f21-162">Для элементов, состоящих из одного компонента, NuGet заменяет любое ранее найденное значение с тем же ключом.</span><span class="sxs-lookup"><span data-stu-id="99f21-162">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="99f21-163">Это означает, что параметры, найденные на самом близком к текущей папке или проекту уровне, переопределяют любые ранее найденные параметры.</span><span class="sxs-lookup"><span data-stu-id="99f21-163">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="99f21-164">Например, параметр `defaultPushSource` в файле `NuGetDefaults.Config` будет переопределен аналогичным параметром, найденным в любом другом файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="99f21-164">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="99f21-165">Для элементов коллекции (таких как `<packageSources>`) NuGet объединяет значения из всех файлов конфигурации в одну коллекцию.</span><span class="sxs-lookup"><span data-stu-id="99f21-165">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="99f21-166">Если для заданного узла указан параметр `<clear />`, NuGet игнорирует ранее определенные значения конфигурации для этого узла.</span><span class="sxs-lookup"><span data-stu-id="99f21-166">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="99f21-167">Пошаговое руководство по параметрам</span><span class="sxs-lookup"><span data-stu-id="99f21-167">Settings walkthrough</span></span>

<span data-ttu-id="99f21-168">Допустим, у вас есть следующая структура папок на двух отдельных дисках:</span><span class="sxs-lookup"><span data-stu-id="99f21-168">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="99f21-169">В показанных ниже расположениях присутствует четыре файла `NuGet.Config` со следующим содержимым.</span><span class="sxs-lookup"><span data-stu-id="99f21-169">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="99f21-170">(В этот пример не включен файл уровня компьютера, поведение которого аналогично файлу уровня пользователя.)</span><span class="sxs-lookup"><span data-stu-id="99f21-170">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="99f21-171">Файл А. Файл на уровне пользователей (`%appdata%\NuGet\NuGet.Config` в Windows, `~/.config/NuGet/NuGet.Config` в Mac и Linux):</span><span class="sxs-lookup"><span data-stu-id="99f21-171">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="99f21-172">Файл Б. disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="99f21-172">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="99f21-173">Файл В. disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="99f21-173">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="99f21-174">Файл Г. disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="99f21-174">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="99f21-175">Затем NuGet загружает и применяет параметры следующим образом, в зависимости от места вызова:</span><span class="sxs-lookup"><span data-stu-id="99f21-175">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="99f21-176">**Вызов из disk_drive_1/users**. Используется только репозиторий по умолчанию, представленный в файле конфигурации уровня пользователя (А), поскольку это единственный файл, найденный по пути disk_drive_1.</span><span class="sxs-lookup"><span data-stu-id="99f21-176">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="99f21-177">**Вызов из disk_drive_2/ или disk_drive_/tmp**. Сначала загружается файл уровня пользователя (А), а затем NuGet переходит в корень disk_drive_2 и находит файл (Б).</span><span class="sxs-lookup"><span data-stu-id="99f21-177">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="99f21-178">Кроме того, NuGet также ищет файл конфигурации в папке /tmp, но не находит его.</span><span class="sxs-lookup"><span data-stu-id="99f21-178">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="99f21-179">В результате используется репозиторий по умолчанию на веб-сайте nuget.org, включается восстановление пакетов и пакеты развертываются в папке disk_drive_2/tmp.</span><span class="sxs-lookup"><span data-stu-id="99f21-179">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="99f21-180">**Вызов из disk_drive_2/Project1 или disk_drive_2/Project1/Source**. Сначала загружается файл уровня пользователя (А), затем NuGet загружает файл (Б) из корня disk_drive_2, после чего загружается файл (В).</span><span class="sxs-lookup"><span data-stu-id="99f21-180">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="99f21-181">Параметры в файле (В) переопределяют параметры в файлах (Б) и (А), поэтому путь `repositoryPath`, по которому устанавливаются пакеты, будет иметь вид disk_drive_2/Project1/External/Packages вместо *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="99f21-181">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="99f21-182">Кроме того, поскольку файл (В) очищает `<packageSources>`, веб-сайт nuget.org будет недоступен в качестве источника, и останется только `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="99f21-182">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="99f21-183">**Вызов из disk_drive_2/Project2 или disk_drive_2/Project2/Source**. Сначала загружается файл уровня пользователя (А), а затем файл (Б) и файл (Г).</span><span class="sxs-lookup"><span data-stu-id="99f21-183">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="99f21-184">Поскольку `packageSources` не очищается, в качестве источников будут доступны одновременно `nuget.org` и `https://MyPrivateRepo/DQ/nuget`.</span><span class="sxs-lookup"><span data-stu-id="99f21-184">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="99f21-185">Пакеты развертываются по пути disk_drive_2/tmp, заданному в файле (Б).</span><span class="sxs-lookup"><span data-stu-id="99f21-185">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="additional-user-wide-configuration"></a><span data-ttu-id="99f21-186">Дополнительная конфигурация на уровне пользователя</span><span class="sxs-lookup"><span data-stu-id="99f21-186">Additional user wide configuration</span></span>

<span data-ttu-id="99f21-187">Начиная с версии 5.7 в NuGet появилась поддержка дополнительных файлов конфигурации на уровне пользователя.</span><span class="sxs-lookup"><span data-stu-id="99f21-187">Starting with 5.7, NuGet has added support for additional user wide configuration files.</span></span> <span data-ttu-id="99f21-188">Это позволяет сторонним поставщикам добавлять дополнительные пользовательские файлы конфигурации без повышения прав.</span><span class="sxs-lookup"><span data-stu-id="99f21-188">This allows third-party vendors to add additional user configuration files without elevation.</span></span>
<span data-ttu-id="99f21-189">Эти файлы конфигурации находятся в стандартной пользовательской папке конфигурации в подпапке `config`.</span><span class="sxs-lookup"><span data-stu-id="99f21-189">These configuration files are found in the standard user wide configuration folder within a `config` subfolder.</span></span>
<span data-ttu-id="99f21-190">Будут учитываться все файлы, которые имеют расширение `.config` или `.Config`.</span><span class="sxs-lookup"><span data-stu-id="99f21-190">All files ending with `.config` or `.Config` will be considered.</span></span>
<span data-ttu-id="99f21-191">Эти файлы нельзя изменить стандартными инструментами.</span><span class="sxs-lookup"><span data-stu-id="99f21-191">These files cannot be edited by the standard tooling.</span></span>

| <span data-ttu-id="99f21-192">Платформа ОС</span><span class="sxs-lookup"><span data-stu-id="99f21-192">OS Platform</span></span>  | <span data-ttu-id="99f21-193">Дополнительные конфигурации</span><span class="sxs-lookup"><span data-stu-id="99f21-193">Additional Configurations</span></span> |
| --- | --- |
| <span data-ttu-id="99f21-194">Windows</span><span class="sxs-lookup"><span data-stu-id="99f21-194">Windows</span></span>      | `%appdata%\NuGet\config\*.Config` |
| <span data-ttu-id="99f21-195">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="99f21-195">Mac/Linux</span></span>    | <span data-ttu-id="99f21-196">`~/.config/NuGet/config/*.config` или `~/.nuget/config/*.config`</span><span class="sxs-lookup"><span data-stu-id="99f21-196">`~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span></span> |

## <a name="nuget-defaults-file"></a><span data-ttu-id="99f21-197">Файл параметров по умолчанию NuGet</span><span class="sxs-lookup"><span data-stu-id="99f21-197">NuGet defaults file</span></span>

<span data-ttu-id="99f21-198">Файл `NuGetDefaults.Config` задает источники пакетов, из которых устанавливаются и обновляются пакеты, а также определяет целевой объект по умолчанию для публикации пакетов с использованием команды `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="99f21-198">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="99f21-199">Так как администраторы могут без усилий согласованно развертывать файлы `NuGetDefaults.Config` на компьютерах разработки и построения (например, с использованием групповой политики), они могут гарантировать то, что все пользователи организации будут иметь правильные источники пакетов вместо веб-сайта nuget.org.</span><span class="sxs-lookup"><span data-stu-id="99f21-199">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="99f21-200">Файл `NuGetDefaults.Config` никогда не вызывает удаление источника пакетов из конфигурации NuGet разработчика.</span><span class="sxs-lookup"><span data-stu-id="99f21-200">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="99f21-201">Это означает, что если разработчик уже использовал NuGet и для него зарегистрирован источник пакетов nuget.org, он не будет использован после создания файла `NuGetDefaults.Config`.</span><span class="sxs-lookup"><span data-stu-id="99f21-201">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="99f21-202">Кроме того, ни файл `NuGetDefaults.Config`, ни любой другой механизм в NuGet не могут предотвратить доступ к таким источникам пакетов, как nuget.org. Если организации требуется заблокировать доступ, необходимо использовать другие способы, например брандмауэры.</span><span class="sxs-lookup"><span data-stu-id="99f21-202">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="99f21-203">Расположение файла NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="99f21-203">NuGetDefaults.Config location</span></span>

<span data-ttu-id="99f21-204">В следующей таблице указано, где следует хранить файл `NuGetDefaults.Config` в зависимости от целевой ОС.</span><span class="sxs-lookup"><span data-stu-id="99f21-204">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="99f21-205">Платформа ОС</span><span class="sxs-lookup"><span data-stu-id="99f21-205">OS Platform</span></span>  | <span data-ttu-id="99f21-206">Расположение файла NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="99f21-206">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="99f21-207">Windows</span><span class="sxs-lookup"><span data-stu-id="99f21-207">Windows</span></span>      | <span data-ttu-id="99f21-208">**Visual Studio 2017 или NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="99f21-208">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="99f21-209">**Visual Studio 2015 или более ранней версии либо NuGet 3.x или более ранней версии:** `%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="99f21-209">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="99f21-210">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="99f21-210">Mac/Linux</span></span>    | <span data-ttu-id="99f21-211">`$XDG_DATA_HOME` (обычно `~/.local/share` или `/usr/local/share`, в зависимости от дистрибутива ОС)</span><span class="sxs-lookup"><span data-stu-id="99f21-211">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="99f21-212">Параметры в файле NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="99f21-212">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="99f21-213">`packageSources`. Эта коллекция имеет то же значение, что и `packageSources` в обычных файлах конфигурации и задает источники по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="99f21-213">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="99f21-214">NuGet использует эти источники в указанном порядке при установке или обновлении пакетов в проектах с помощью формата управления `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="99f21-214">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="99f21-215">Для проектов, в которых используется формат PackageReference, NuGet сначала использует локальные источники, затем — источники в сетевых папках, а после этого — HTTP-источники, независимо от порядка, заданного в файлах конфигурации.</span><span class="sxs-lookup"><span data-stu-id="99f21-215">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="99f21-216">NuGet всегда игнорирует порядок источников при операциях восстановления.</span><span class="sxs-lookup"><span data-stu-id="99f21-216">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="99f21-217">`disabledPackageSources`. Эта коллекция также имеет то же значение, что и в файлах `NuGet.Config`, где каждый затрагиваемый источник перечислен по имени и значению true/false, указывающему, включен он или отключен.</span><span class="sxs-lookup"><span data-stu-id="99f21-217">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="99f21-218">Это позволяет сохранять имя и URL-адрес источника в `packageSources`, не включая его по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="99f21-218">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="99f21-219">Отдельные разработчики при необходимости могут повторно включить источник, присвоив параметру источника значение false в других файлах `NuGet.Config`, не выполняя повторный поиск правильного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="99f21-219">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="99f21-220">Также рекомендуется предоставить разработчикам полный список URL-адресов внутренних источников для организации, но включить по умолчанию только источник для отдельной группы.</span><span class="sxs-lookup"><span data-stu-id="99f21-220">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="99f21-221">`defaultPushSource`: задает целевой объект по умолчанию для операций `nuget push`, переопределяя встроенное значение по умолчанию nuget.org. Администраторы могут развертывать этот параметр, чтобы избежать случайной публикации внутренних пакетов на открытом веб-сайте nuget.org, поскольку разработчикам придется специально использовать команду `nuget push -Source` для публикации на веб-сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="99f21-221">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="99f21-222">Пример файла NuGetDefaults.Config и приложения</span><span class="sxs-lookup"><span data-stu-id="99f21-222">Example NuGetDefaults.Config and application</span></span>

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
