---
title: "Настройка поведения NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c1e34826-d07d-4609-a0fd-123459ae89c5
description: "Файлы NuGet.Config определяют поведение NuGet как на глобальном уровне, так и на уровне отдельных проектов. Для их изменения используется команда nuget config."
keywords: "файлы конфигурации NuGet, конфигурация NuGet, параметры поведения NuGet, параметры NuGet, Nuget.Config, NuGetDefaults.Config, параметры по умолчанию"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f9e56b68f70387435cdaa1537db503abb912fd2a
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="configuring-nuget-behavior"></a><span data-ttu-id="1f166-104">Настройка поведения NuGet</span><span class="sxs-lookup"><span data-stu-id="1f166-104">Configuring NuGet behavior</span></span>

<span data-ttu-id="1f166-105">Поведение NuGet определяется совокупностью параметров в одном или нескольких файлах `NuGet.Config` формата XML, которые могут существовать на уровне проекта, пользователя и компьютера.</span><span class="sxs-lookup"><span data-stu-id="1f166-105">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="1f166-106">Кроме того, в версии 2.7 и более поздних используется глобальный файл `NuGetDefaults.Config`, определяющий конфигурацию источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="1f166-106">A global `NuGetDefaults.Config` file (2.7+) also specifically configures package sources.</span></span> <span data-ttu-id="1f166-107">Параметры применяются ко всем командам, выполняемым в интерфейсе командной строки, консоли диспетчера пакетов и пользовательском интерфейсе диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="1f166-107">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

<span data-ttu-id="1f166-108">Содержание раздела</span><span class="sxs-lookup"><span data-stu-id="1f166-108">In this topic:</span></span>

- [<span data-ttu-id="1f166-109">Расположение и использование файла NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="1f166-109">NuGet.Config file locations and uses</span></span>](#config-file-locations-and-uses)
- [<span data-ttu-id="1f166-110">Изменение параметров</span><span class="sxs-lookup"><span data-stu-id="1f166-110">Changing settings</span></span>](#changing-config-settings)
- [<span data-ttu-id="1f166-111">Порядок применения параметров</span><span class="sxs-lookup"><span data-stu-id="1f166-111">How settings are applied</span></span>](#how-settings-are-applied)
- [<span data-ttu-id="1f166-112">Файл NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="1f166-112">NuGetDefaults.Config file</span></span>](#nuget-defaults-file)

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="1f166-113">Расположение и использование файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="1f166-113">Config file locations and uses</span></span>

| <span data-ttu-id="1f166-114">Область</span><span class="sxs-lookup"><span data-stu-id="1f166-114">Scope</span></span> | <span data-ttu-id="1f166-115">Расположение файла NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="1f166-115">NuGet.Config file location</span></span> | <span data-ttu-id="1f166-116">Описание</span><span class="sxs-lookup"><span data-stu-id="1f166-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1f166-117">Проект</span><span class="sxs-lookup"><span data-stu-id="1f166-117">Project</span></span> | <span data-ttu-id="1f166-118">Папка проекта или любая другая папка вплоть до уровня корня диска</span><span class="sxs-lookup"><span data-stu-id="1f166-118">Project folder or any folder up to the drive root</span></span> | <span data-ttu-id="1f166-119">Параметры, расположенные в папке проекта, применяются только к этому проекту.</span><span class="sxs-lookup"><span data-stu-id="1f166-119">In a project folder, settings apply only to that project.</span></span> <span data-ttu-id="1f166-120">Параметры, расположенные в родительских папках, которые содержат несколько вложенных папок проектов, применяются ко всем проектам в этих вложенных папках.</span><span class="sxs-lookup"><span data-stu-id="1f166-120">In parent folders that contain multiple projects subfolders, settings apply to all projects in those subfolders.</span></span> |
| <span data-ttu-id="1f166-121">Пользователь</span><span class="sxs-lookup"><span data-stu-id="1f166-121">User</span></span> | <span data-ttu-id="1f166-122">Windows: %APPDATA%\NuGet\NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="1f166-122">Windows: %APPDATA%\NuGet\NuGet.Config</span></span><br/><span data-ttu-id="1f166-123">Mac/Linux: ~/.nuget/NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="1f166-123">Mac/Linux: ~/.nuget/NuGet.Config</span></span> | <span data-ttu-id="1f166-124">Параметры применяются ко всем операциям, но переопределяются любыми параметрами, задаваемыми на уровне проекта.</span><span class="sxs-lookup"><span data-stu-id="1f166-124">Settings apply to all operations, but are overridden by any project-level settings.</span></span> <span data-ttu-id="1f166-125">При использовании команд интерфейса командной строки можно задать другой файл конфигурации с помощью параметра `-configFile`, чтобы игнорировать любые параметры в используемом по умолчанию файле уровня пользователя.</span><span class="sxs-lookup"><span data-stu-id="1f166-125">When using CLI commands, you can specify a different config file using the `-configFile` switch to ignore any settings in the default user-level file.</span></span> |
| <span data-ttu-id="1f166-126">Компьютер</span><span class="sxs-lookup"><span data-stu-id="1f166-126">Computer</span></span> | <span data-ttu-id="1f166-127">Windows: %ProgramFiles(x86)%\NuGet\Config</span><span class="sxs-lookup"><span data-stu-id="1f166-127">Windows: %ProgramFiles(x86)%\NuGet\Config</span></span><br/><span data-ttu-id="1f166-128">Mac/Linux: $XDG_DATA_HOME (как правило, ~/.local/share)</span><span class="sxs-lookup"><span data-stu-id="1f166-128">Mac/Linux: $XDG_DATA_HOME (typically ~/.local/share)</span></span> | <span data-ttu-id="1f166-129">Параметры применяются ко всем операциям на компьютере, но переопределяются любыми параметрами, задаваемыми на уровне пользователя или проекта.</span><span class="sxs-lookup"><span data-stu-id="1f166-129">Settings apply to all operations on the computer, but are overriden by any user- or project-level settings.</span></span> |

<span data-ttu-id="1f166-130">Примечания для более ранних версий NuGet:</span><span class="sxs-lookup"><span data-stu-id="1f166-130">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="1f166-131">В NuGet 3.3 и более ранних версий параметры уровня решения располагались в папке `.nuget`.</span><span class="sxs-lookup"><span data-stu-id="1f166-131">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="1f166-132">В NuGet версии 3.4 и более поздних этот файл не используется.</span><span class="sxs-lookup"><span data-stu-id="1f166-132">This file not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="1f166-133">В версиях NuGet с 2.6 по 3.x файл конфигурации уровня компьютера для Windows располагался в папке %ProgramData%\NuGet\Config[\\{IDE}[\\{версия}[\\{SKU}]]]\NuGet.Config, где атрибут *{IDE}* мог иметь значение *VisualStudio*, атрибут *{версия}* указывал на версию Visual Studio, например *14.0*, а атрибут *{SKU}* определял выпуск *Community*, *Pro* или *Enterprise*.</span><span class="sxs-lookup"><span data-stu-id="1f166-133">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="1f166-134">Чтобы перенести параметры в NuGet версии 4.0 или более поздней, просто скопируйте файл конфигурации в папку %ProgramFiles(x86)%\NuGet\Config. В Linus ранее использовалось расположение /etc/opt, а в Mac — /Library/Application Support.</span><span class="sxs-lookup"><span data-stu-id="1f166-134">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linus, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="1f166-135">Изменение параметров конфигурации</span><span class="sxs-lookup"><span data-stu-id="1f166-135">Changing config settings</span></span>

<span data-ttu-id="1f166-136">Файл `NuGet.Config` представляет собой простой текстовый файл в формате XML, который содержит пары ключей и значений, описываемые в разделе [Параметры конфигурации NuGet](../Schema/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="1f166-136">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../Schema/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="1f166-137">Управление параметрами осуществляется с помощью команды [config command](../tools/cli-ref-config.md) интерфейса командной строки NuGet:</span><span class="sxs-lookup"><span data-stu-id="1f166-137">Settings are managed using the NuGet CLI [config command](../tools/cli-ref-config.md):</span></span>
- <span data-ttu-id="1f166-138">По умолчанию изменения вносятся в файл конфигурации уровня пользователя.</span><span class="sxs-lookup"><span data-stu-id="1f166-138">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="1f166-139">Для изменения параметров в другом файле используйте параметр `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="1f166-139">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="1f166-140">В таком случае файлы могут иметь любые имена.</span><span class="sxs-lookup"><span data-stu-id="1f166-140">In this case files can use any filename.</span></span>
- <span data-ttu-id="1f166-141">Ключи всегда задаются с учетом регистра символов.</span><span class="sxs-lookup"><span data-stu-id="1f166-141">Keys are always case sensitive.</span></span>
- <span data-ttu-id="1f166-142">Для изменения параметров в файле уровня компьютера требуется повышение прав.</span><span class="sxs-lookup"><span data-stu-id="1f166-142">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="1f166-143">Файл конфигурации можно изменять в любом редакторе, однако если он будет содержать неправильно сформированный код XML (несоответствующие теги, неправильно используемые кавычки и т. д.), NuGet (версии 3.4.3 и более поздней) будет полностью игнорировать его без выдачи каких-либо уведомлений.</span><span class="sxs-lookup"><span data-stu-id="1f166-143">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="1f166-144">Поэтому для управления параметрами рекомендуется использовать команду `nuget config`.</span><span class="sxs-lookup"><span data-stu-id="1f166-144">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="1f166-145">Настройка значения</span><span class="sxs-lookup"><span data-stu-id="1f166-145">Setting a value</span></span>

<span data-ttu-id="1f166-146">Windows:</span><span class="sxs-lookup"><span data-stu-id="1f166-146">Windows:</span></span>

```
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\NuGet.Config
```

<span data-ttu-id="1f166-147">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="1f166-147">Mac/Linux:</span></span>

```
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> <span data-ttu-id="1f166-148">В NuGet 3.4 и более поздних версий можно использовать в любом значении переменные среды, такие как `repositoryPath=%PACKAGEHOME%` (Windows) и `repositoryPath=%PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="1f166-148">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=%PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="1f166-149">Удаление значения</span><span class="sxs-lookup"><span data-stu-id="1f166-149">Removing a value</span></span>

<span data-ttu-id="1f166-150">Чтобы удалить значение, укажите ключ с пустым значением.</span><span class="sxs-lookup"><span data-stu-id="1f166-150">To remove a value, specify a key with an empty value.</span></span>

```
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="1f166-151">Создание нового файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="1f166-151">Creating a new config file</span></span>

<span data-ttu-id="1f166-152">Скопируйте представленный ниже шаблон в новый файл и затем присвойте значения с помощью `nuget config --configFile <filename>`:</span><span class="sxs-lookup"><span data-stu-id="1f166-152">Copy the template below into the new file and then use `nuget config --configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

<br/>

## <a name="how-settings-are-applied"></a><span data-ttu-id="1f166-153">Порядок применения параметров</span><span class="sxs-lookup"><span data-stu-id="1f166-153">How settings are applied</span></span>

<span data-ttu-id="1f166-154">Благодаря применению нескольких файлов `NuGet.Config` вы можете хранить параметры в различных местах так, чтобы они применялись к отдельному проекту, группе проектов или всем проектам.</span><span class="sxs-lookup"><span data-stu-id="1f166-154">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="1f166-155">Эти параметры совместно применяются к любым операциям NuGet, которые вызываются из командной строки или из среды Visual Studio. Приоритет при этом имеют параметры, которые находятся на уровне, ближайшем к проекту или текущей папке.</span><span class="sxs-lookup"><span data-stu-id="1f166-155">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="1f166-156">В частности, NuGet загружает параметры из различных файлов конфигурации в следующем порядке:</span><span class="sxs-lookup"><span data-stu-id="1f166-156">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="1f166-157">[Файл NuGetDefaults.Config](#nuget-defaults-file), который содержит параметры, относящиеся только к источникам пакетов.</span><span class="sxs-lookup"><span data-stu-id="1f166-157">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="1f166-158">Файл уровня компьютера.</span><span class="sxs-lookup"><span data-stu-id="1f166-158">The computer-level file.</span></span>
1. <span data-ttu-id="1f166-159">Файл уровня пользователя.</span><span class="sxs-lookup"><span data-stu-id="1f166-159">The user-level file.</span></span>
1. <span data-ttu-id="1f166-160">Файл, заданный параметром `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="1f166-160">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="1f166-161">Файлы, найденные в каждой папке по пути от корня диска к текущей папке (папка, из которой была вызвана команда nuget.exe, или папка, содержащая проект Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="1f166-161">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="1f166-162">Например, при вызове команды в папке "c:\A\B\C" NuGet ищет и загружает файлы конфигурации сначала по пути "c:\,", затем "c:\A", затем "c:\A\B" и, наконец, "c:\A\B\C".</span><span class="sxs-lookup"><span data-stu-id="1f166-162">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="1f166-163">Параметры, найденные в этих файлах, NuGet применяет следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1f166-163">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="1f166-164">Для элементов, состоящих из одного компонента, NuGet заменяет любое ранее найденное значение с тем же ключом.</span><span class="sxs-lookup"><span data-stu-id="1f166-164">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="1f166-165">Это означает, что параметры, найденные на самом близком к текущей папке или проекту уровне, переопределяют любые ранее найденные параметры.</span><span class="sxs-lookup"><span data-stu-id="1f166-165">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="1f166-166">Например, параметр `defaultPushSource` в файле `NuGetDefaults.Config` будет переопределен аналогичным параметром, найденным в любом другом файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1f166-166">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="1f166-167">Для элементов коллекции (таких как `<packageSources>`) NuGet объединяет значения из всех файлов конфигурации в одну коллекцию.</span><span class="sxs-lookup"><span data-stu-id="1f166-167">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="1f166-168">Если для заданного узла указан параметр `<clear />`, NuGet игнорирует ранее определенные значения конфигурации для этого узла.</span><span class="sxs-lookup"><span data-stu-id="1f166-168">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="1f166-169">Пошаговое руководство по параметрам</span><span class="sxs-lookup"><span data-stu-id="1f166-169">Settings walkthrough</span></span>

<span data-ttu-id="1f166-170">Допустим, у вас есть следующая структура папок на двух отдельных дисках:</span><span class="sxs-lookup"><span data-stu-id="1f166-170">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="1f166-171">В показанных ниже расположениях присутствует четыре файла `NuGet.Config` со следующим содержимым.</span><span class="sxs-lookup"><span data-stu-id="1f166-171">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="1f166-172">(В этот пример не включен файл уровня компьютера, поведение которого аналогично файлу уровня пользователя.)</span><span class="sxs-lookup"><span data-stu-id="1f166-172">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="1f166-173">Файл А. Файл уровня пользователя (%APPDATA%\NuGet\NuGet.Config в Windows и ~/.nuget/NuGet.Config в Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="1f166-173">File A. User-level file, (%APPDATA%\NuGet\NuGet.Config on Windows, ~/.nuget/NuGet.Config on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="1f166-174">Файл Б. disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="1f166-174">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="1f166-175">Файл В. disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="1f166-175">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="1f166-176">Файл Г. disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="1f166-176">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="1f166-177">Затем NuGet загружает и применяет параметры следующим образом, в зависимости от места вызова:</span><span class="sxs-lookup"><span data-stu-id="1f166-177">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="1f166-178">**Вызов из disk_drive_1/users**. Используется только репозиторий по умолчанию, представленный в файле конфигурации уровня пользователя (А), поскольку это единственный файл, найденный по пути disk_drive_1.</span><span class="sxs-lookup"><span data-stu-id="1f166-178">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="1f166-179">**Вызов из disk_drive_2/ или disk_drive_/tmp**. Сначала загружается файл уровня пользователя (А), а затем NuGet переходит в корень disk_drive_2 и находит файл (Б).</span><span class="sxs-lookup"><span data-stu-id="1f166-179">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="1f166-180">Кроме того, NuGet также ищет файл конфигурации в папке /tmp, но не находит его.</span><span class="sxs-lookup"><span data-stu-id="1f166-180">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="1f166-181">В результате используется репозиторий по умолчанию на веб-сайте nuget.org, включается восстановление пакетов и пакеты развертываются в папке disk_drive_2/tmp.</span><span class="sxs-lookup"><span data-stu-id="1f166-181">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="1f166-182">**Вызов из disk_drive_2/Project1 или disk_drive_2/Project1/Source**. Сначала загружается файл уровня пользователя (А), затем NuGet загружает файл (Б) из корня disk_drive_2, после чего загружается файл (В).</span><span class="sxs-lookup"><span data-stu-id="1f166-182">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="1f166-183">Параметры в файле (В) переопределяют параметры в файлах (Б) и (А), поэтому путь `repositoryPath`, по которому устанавливаются пакеты, будет иметь вид disk_drive_2/Project1/External/Packages вместо *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="1f166-183">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="1f166-184">Кроме того, поскольку файл (В) очищает `<packageSources>`, веб-сайт nuget.org будет недоступен в качестве источника, и останется только `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="1f166-184">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="1f166-185">**Вызов из disk_drive_2/Project2 или disk_drive_2/Project2/Source**. Сначала загружается файл уровня пользователя (А), а затем файл (Б) и файл (Г).</span><span class="sxs-lookup"><span data-stu-id="1f166-185">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="1f166-186">Поскольку `packageSources` не очищается, в качестве источников будут доступны одновременно `nuget.org` и `https://MyPrivateRepo/DQ/nuget`.</span><span class="sxs-lookup"><span data-stu-id="1f166-186">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="1f166-187">Пакеты развертываются по пути disk_drive_2/tmp, заданному в файле (Б).</span><span class="sxs-lookup"><span data-stu-id="1f166-187">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="1f166-188">Файл параметров по умолчанию NuGet</span><span class="sxs-lookup"><span data-stu-id="1f166-188">NuGet defaults file</span></span>

<span data-ttu-id="1f166-189">Файл `NuGetDefaults.Config` задает источники пакетов, из которых устанавливаются и обновляются пакеты, а также определяет целевой объект по умолчанию для публикации пакетов с использованием команды `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="1f166-189">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="1f166-190">Поскольку администраторы могут с легкостью (например, с использованием групповой политики) и согласованно развертывать файлы `NuGetDefaults.Config` на компьютерах разработки и построения, они могут гарантировать то, что все пользователи организации будут иметь правильные источники пакетов вместо веб-сайта nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1f166-190">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensuring that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="1f166-191">Файл `NuGetDefaults.Config` никогда не вызывает удаление источника пакетов из конфигурации NuGet разработчика.</span><span class="sxs-lookup"><span data-stu-id="1f166-191">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="1f166-192">Это означает, что если разработчик уже использовал NuGet и для него зарегистрирован источник пакетов nuget.org, он не будет использован после создания файла `NuGetDefaults.Config`.</span><span class="sxs-lookup"><span data-stu-id="1f166-192">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="1f166-193">Кроме того, ни файл `NuGetDefaults.Config`, ни любой другой механизм в NuGet не могут предотвратить доступ к таким источникам пакетов, как nuget.org. Если организации требуется заблокировать доступ, необходимо использовать другие способы, например брандмауэры и т. д.</span><span class="sxs-lookup"><span data-stu-id="1f166-193">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it much use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="1f166-194">Расположение файла NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="1f166-194">NuGetDefaults.Config location</span></span>

<span data-ttu-id="1f166-195">Windows: %ProgramFiles(x86)%\NuGet\Config (в версиях NuGet с 2.7 до NuGet 3.x: %PROGRAMDATA%\NuGet\NuGetDefaults.Config) Mac/Linux: $XDG_DATA_HOME (как правило, ~/.local/share)</span><span class="sxs-lookup"><span data-stu-id="1f166-195">Windows: %ProgramFiles(x86)%\NuGet\Config (NuGet 2.7 to NuGet 3.x: %PROGRAMDATA%\NuGet\NuGetDefaults.Config) Mac/Linux: $XDG_DATA_HOME (typically ~/.local/share)</span></span> 

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="1f166-196">Параметры в файле NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="1f166-196">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="1f166-197">`packageSources`. Эта коллекция имеет то же значение, что и `packageSources` в обычных файлах конфигурации и задает источники по умолчанию в предпочитаемом порядке.</span><span class="sxs-lookup"><span data-stu-id="1f166-197">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources in their preferred order.</span></span> <span data-ttu-id="1f166-198">Если этот параметр существует в файле `NuGetDefaults.Config`, NuGet не использует веб-сайт nuget.org в качестве источника пакетов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1f166-198">If this setting exists in `NuGetDefaults.Config`, then NuGet doesn't use nuget.org as a default package source.</span></span> <span data-ttu-id="1f166-199">Таким образом, администратор может гарантировать, что все пользователи, работающие с этим файлом, используют одни и те же источники, и при необходимости исключить использование веб-сайта nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1f166-199">An administrator can thus make sure that everyone using this file is working with the same sources and avoids using nuget.org if desired.</span></span>

- <span data-ttu-id="1f166-200">`disabledPackageSources`. Эта коллекция также имеет то же значение, что и в файлах `NuGet.Config`, где каждый затрагиваемый источник перечислен по имени и значению true/false, указывающему, включен он или отключен.</span><span class="sxs-lookup"><span data-stu-id="1f166-200">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="1f166-201">Это позволяет сохранять имя и URL-адрес источника в `packageSources`, не включая его по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1f166-201">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="1f166-202">Отдельные разработчики при необходимости могут повторно включить источник, присвоив параметру источника значение false в других файлах `NuGet.Config`, не выполняя повторный поиск правильного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="1f166-202">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="1f166-203">Также рекомендуется предоставить разработчикам полный список URL-адресов внутренних источников для организации, но включить по умолчанию только источник для отдельной группы.</span><span class="sxs-lookup"><span data-stu-id="1f166-203">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="1f166-204">`defaultPushSource`: задает целевой объект по умолчанию для операций `nuget push`, переопределяя встроенное значение по умолчанию nuget.org. Администраторы могут развертывать этот параметр, чтобы избежать случайной публикации внутренних пакетов на открытом веб-сайте nuget.org, поскольку разработчикам придется специально использовать команду `nuget push -Source` для публикации на веб-сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1f166-204">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="1f166-205">Пример файла NuGetDefaults.Config и приложения</span><span class="sxs-lookup"><span data-stu-id="1f166-205">Example NuGetDefaults.Config and application</span></span>

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
