---
title: Многоплатформенное нацеливание пакетов NuGet
description: Описание различных способов нацеливания на несколько версий .NET Framework из одного пакета NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 09/27/2017
ms.topic: conceptual
ms.openlocfilehash: 429b9743ea678cd500b6f51630d03aac7812441e
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816960"
---
# <a name="supporting-multiple-net-framework-versions"></a><span data-ttu-id="f9d5f-103">Поддержка нескольких версий платформы .NET Framework</span><span class="sxs-lookup"><span data-stu-id="f9d5f-103">Supporting multiple .NET framework versions</span></span>

<span data-ttu-id="f9d5f-104">*Сведения о межплатформенном нацеливании для проектов .NET Core, использующих NuGet 4.0 или более поздней версии, см. в разделе [Создание и восстановление пакетов NuGet в качестве целей MSBuild](../reference/msbuild-targets.md).*</span><span class="sxs-lookup"><span data-stu-id="f9d5f-104">*For .NET Core projects using NuGet 4.0+, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) for details on cross-targeting.*</span></span>

<span data-ttu-id="f9d5f-105">Многие библиотеки предназначаются для определенной версии платформы .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-105">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="f9d5f-106">Например, у вас может быть одна версия библиотеки для универсальной платформы Windows и другая версия, использующая возможности .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-106">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span>

<span data-ttu-id="f9d5f-107">Для реализации такого сценария NuGet поддерживает объединение нескольких версий одной и той же библиотеки в одном пакете при использовании метода на основе рабочего каталога, соответствующего соглашениям, описанного в разделе [Создание пакета](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="f9d5f-107">To accommodate this, NuGet supports putting multiple versions of the same library in a single package when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="f9d5f-108">Структура папок, соответствующих версиям платформы</span><span class="sxs-lookup"><span data-stu-id="f9d5f-108">Framework version folder structure</span></span>

<span data-ttu-id="f9d5f-109">При создании пакета, который содержит только одну версию библиотеки или предназначается для нескольких платформ, вы всегда создаете в папке `lib` вложенные папки с именами платформ (с учетом регистра) согласно следующим соглашениям:</span><span class="sxs-lookup"><span data-stu-id="f9d5f-109">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="f9d5f-110">Полный список поддерживаемых имен см. в [справочнике по целевым платформам](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="f9d5f-110">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="f9d5f-111">Никогда не следует включать версию библиотеки, не относящуюся к конкретной платформе, помещая ее непосредственно в корневую папку `lib`.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-111">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="f9d5f-112">(Такая возможность поддерживалась только в `packages.config`.)</span><span class="sxs-lookup"><span data-stu-id="f9d5f-112">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="f9d5f-113">В таком случае библиотека будет совместима с любой целевой платформой и ее можно будет установить где угодно, что, скорее всего, приведет к непредвиденным ошибкам во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-113">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="f9d5f-114">Возможность добавления сборок в корневую папку (например, `lib\abc.dll`) или ее вложенные папки (например, `lib\abc\abc.dll`) является нерекомендуемой и игнорируется при использовании формата PackagesReference.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-114">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="f9d5f-115">Например, следующая структура папок поддерживает четыре версии сборки для конкретных платформ:</span><span class="sxs-lookup"><span data-stu-id="f9d5f-115">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="f9d5f-116">Чтобы легко включить все эти файлы при сборке пакета, используйте рекурсивный подстановочный знак `**` в разделе `<files>` файла `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="f9d5f-116">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="f9d5f-117">Папки для конкретных архитектур</span><span class="sxs-lookup"><span data-stu-id="f9d5f-117">Architecture-specific folders</span></span>

<span data-ttu-id="f9d5f-118">Если имеются сборки для конкретных архитектур, то есть отдельные сборки для архитектур ARM, x86 и x64, их необходимо поместить в папку с именем `runtimes` во вложенные папки `{platform}-{architecture}\lib\{framework}` или `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-118">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="f9d5f-119">Например, следующая структура папок содержит как библиотеки DLL в машинном коде, так и управляемые библиотеки DLL для Windows 10 и платформы `uap10.0`:</span><span class="sxs-lookup"><span data-stu-id="f9d5f-119">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

<span data-ttu-id="f9d5f-120">Пример указания ссылок на эти файлы в манифесте `.nuspec` см. в разделе [Создание пакетов универсальной платформы Windows](../guides/create-uwp-packages.md).</span><span class="sxs-lookup"><span data-stu-id="f9d5f-120">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="f9d5f-121">Сопоставление версий сборки и целевых платформ в проекте</span><span class="sxs-lookup"><span data-stu-id="f9d5f-121">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="f9d5f-122">Когда диспетчер NuGet устанавливает пакет с несколькими версиями сборки, он пытается сопоставить имя платформы, для которой предназначена сборка, с целевой платформой проекта.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-122">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="f9d5f-123">Если соответствия не найдено, NuGet копирует сборку с самой старшей версией, которая не старше версии целевой платформы проекта, при условии, что такая версия сборки доступна.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-123">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="f9d5f-124">Если совместимая сборка не найдена, NuGet возвращает соответствующее сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-124">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="f9d5f-125">Например, рассмотрим следующую структуру папок в пакете:</span><span class="sxs-lookup"><span data-stu-id="f9d5f-125">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="f9d5f-126">При установке этого пакета в проекте, предназначенном для .NET Framework 4.6, NuGet устанавливает сборку из папки `net45`, так как это самая старшая доступная версия не выше 4.6.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-126">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="f9d5f-127">Если же проект предназначен для .NET Framework 4.6.1, NuGet устанавливает сборку в папке `net461`.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-127">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="f9d5f-128">Если проект предназначен для .NET Framework 4.0 или более ранней версии, NuGet выдает сообщение об ошибке отсутствия совместимой сборки.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-128">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="f9d5f-129">Группирование сборок по версии платформы</span><span class="sxs-lookup"><span data-stu-id="f9d5f-129">Grouping assemblies by framework version</span></span>

<span data-ttu-id="f9d5f-130">NuGet копирует сборки только из одной папки библиотеки в проекте.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-130">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="f9d5f-131">Предположим, есть пакет со следующей структурой папок:</span><span class="sxs-lookup"><span data-stu-id="f9d5f-131">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="f9d5f-132">Когда этот пакет устанавливается в проекте, предназначенном для .NET Framework 4.5, устанавливается только сборка `MyAssembly.dll` (версия 2.0).</span><span class="sxs-lookup"><span data-stu-id="f9d5f-132">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="f9d5f-133">Сборка `MyAssembly.Core.dll` (версия 1.0) не устанавливается, так как ее нет в папке `net45`.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-133">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="f9d5f-134">Такое поведение NuGet обусловлено тем, что сборка `MyAssembly.Core.dll` могла быть объединена с версией 2.0 сборки `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-134">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="f9d5f-135">Чтобы установить сборку `MyAssembly.Core.dll` для .NET Framework 4.5, поместите ее копию в папку `net45`.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-135">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="f9d5f-136">Группирование сборок по профилю платформы</span><span class="sxs-lookup"><span data-stu-id="f9d5f-136">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="f9d5f-137">NuGet также поддерживает нацеливание на определенный профиль платформы путем добавления дефиса и имени платформы в конце имени папки.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-137">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="f9d5f-138">Поддерживаются следующие профили:</span><span class="sxs-lookup"><span data-stu-id="f9d5f-138">The supported profiles are as follows:</span></span>

- <span data-ttu-id="f9d5f-139">`client`: клиентский профиль;</span><span class="sxs-lookup"><span data-stu-id="f9d5f-139">`client`: Client Profile</span></span>
- <span data-ttu-id="f9d5f-140">`full`: полный профиль;</span><span class="sxs-lookup"><span data-stu-id="f9d5f-140">`full`: Full Profile</span></span>
- <span data-ttu-id="f9d5f-141">`wp`: Windows Phone;</span><span class="sxs-lookup"><span data-stu-id="f9d5f-141">`wp`: Windows Phone</span></span>
- <span data-ttu-id="f9d5f-142">`cf`: Compact Framework.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-142">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="f9d5f-143">Определение требуемой цели NuGet</span><span class="sxs-lookup"><span data-stu-id="f9d5f-143">Determining which NuGet target to use</span></span>

<span data-ttu-id="f9d5f-144">При упаковке библиотек, предназначенных для переносимой библиотеки классов, может быть нелегко определить цель NuGet, которую следует использовать в именах папок и файле `.nuspec`, особенно если нацеливание производится лишь на подмножество переносимой библиотеки классов.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-144">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="f9d5f-145">Следующие внешние ресурсы могут помочь в решении этой задачи:</span><span class="sxs-lookup"><span data-stu-id="f9d5f-145">The following external resources will help you with this:</span></span>

- <span data-ttu-id="f9d5f-146">[Профили платформы в .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="f9d5f-146">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span></span>
- <span data-ttu-id="f9d5f-147">[Профили переносимой библиотеки классов](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): таблица, в которой перечисляются профили переносимой библиотеки классов и эквивалентные цели NuGet</span><span class="sxs-lookup"><span data-stu-id="f9d5f-147">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="f9d5f-148">[Программа для работы с профилями переносимой библиотеки классов](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): программа командной строки, позволяющая определить профили переносимой библиотеки классов, доступные в системе</span><span class="sxs-lookup"><span data-stu-id="f9d5f-148">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="f9d5f-149">Файлы содержимого и скрипты PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9d5f-149">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="f9d5f-150">Изменяемые файлы содержимого и выполнение скриптов можно использовать только с форматом `packages.config`. Их не рекомендуется использовать с другими форматами и не следует применять для новых пакетов.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-150">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="f9d5f-151">При использовании `packages.config` файлы содержимого и скрипты PowerShell можно группировать по целевой платформе в папках `content` и `tools`, используя те же соглашения в отношении папок.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-151">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="f9d5f-152">Пример:</span><span class="sxs-lookup"><span data-stu-id="f9d5f-152">For example:</span></span>

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

<span data-ttu-id="f9d5f-153">Если папка платформы пуста, NuGet не добавляет ссылки на сборки или файлы содержимого и не выполняет скрипты PowerShell для этой платформы.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-153">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="f9d5f-154">Так как скрипт `init.ps1` выполняется на уровне решения независимо от проекта, его необходимо поместить непосредственно в папку `tools`.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-154">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="f9d5f-155">Если он находится в папке платформы, то он игнорируется.</span><span class="sxs-lookup"><span data-stu-id="f9d5f-155">It's ignored if placed under a framework folder.</span></span>
