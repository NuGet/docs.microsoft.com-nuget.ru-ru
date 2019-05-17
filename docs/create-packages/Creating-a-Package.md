---
title: Создание пакетов NuGet
description: Подробное руководство по проектированию и созданию пакета NuGet, включая принятие решений по ключевым аспектам, таким как файлы и управление версиями.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: f0d9667b752caf7831278ac3fd63cfd67f7d34a4
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610587"
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="0f255-103">Создание пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="0f255-103">Creating NuGet packages</span></span>

<span data-ttu-id="0f255-104">Независимо от назначения вашего пакета или содержащегося в нем кода, вы можете создать с помощью программы `nuget.exe` компонент, которым можно поделиться с любым количеством разработчиков для совместного использования.</span><span class="sxs-lookup"><span data-stu-id="0f255-104">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="0f255-105">Инструкции по установке `nuget.exe` см. в разделе [Установка интерфейса командной строки NuGet](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="0f255-105">To install `nuget.exe`, see [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span> <span data-ttu-id="0f255-106">Обратите внимание на то, что программа `nuget.exe` не входит в состав Visual Studio по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0f255-106">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="0f255-107">С технической точки зрения, пакет NuGet — это просто ZIP-файл, расширение которого изменено на `.nupkg` и содержимое которого соответствует определенным соглашениям.</span><span class="sxs-lookup"><span data-stu-id="0f255-107">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="0f255-108">В этом разделе подробно описывается создание пакета, в котором соблюдаются эти соглашения.</span><span class="sxs-lookup"><span data-stu-id="0f255-108">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="0f255-109">Краткое руководство приводится в статье по [созданию и публикации пакета](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="0f255-109">For a focused walkthrough, refer to [Quickstart: create and publish a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="0f255-110">Создание пакета начинается с подготовки скомпилированного кода (сборок), символов и других файлов, которые должны быть включены в пакет (см. раздел [Процесс создания пакета](overview-and-workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="0f255-110">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="0f255-111">Этот процесс не зависит от компиляции и других задач по созданию файлов для пакета, хотя вы можете использовать информацию из файла проекта для синхронизации скомпилированных сборок и пакетов.</span><span class="sxs-lookup"><span data-stu-id="0f255-111">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Note]
> <span data-ttu-id="0f255-112">Этот раздел относится к любым типам проектов, кроме проектов .NET Core с использованием Visual Studio 2017 и NuGet 4.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="0f255-112">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="0f255-113">В таких проектах .NET Core NuGet использует сведения в файле проекта напрямую.</span><span class="sxs-lookup"><span data-stu-id="0f255-113">In those .NET Core projects, NuGet uses information in the project file directly.</span></span> <span data-ttu-id="0f255-114">Подробные сведения см. в разделах [Создание пакетов .NET Standard с помощью Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) и [Пакет NuGet и восстановление целевых объектов MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="0f255-114">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="0f255-115">Выбор сборок для добавления в пакет</span><span class="sxs-lookup"><span data-stu-id="0f255-115">Deciding which assemblies to package</span></span>

<span data-ttu-id="0f255-116">Большинство пакетов общего назначения содержат одну или несколько сборок, которые другие разработчики могут использовать в собственных проектах.</span><span class="sxs-lookup"><span data-stu-id="0f255-116">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="0f255-117">Как правило, для каждой сборки лучше создавать собственный пакет NuGet, если эти сборки используются независимо.</span><span class="sxs-lookup"><span data-stu-id="0f255-117">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="0f255-118">Например, если есть сборка `Utilities.dll`, которая зависит от сборки `Parser.dll`, но сборка `Parser.dll` также полезна сама по себе, создайте для каждой из этих сборок отдельный пакет.</span><span class="sxs-lookup"><span data-stu-id="0f255-118">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="0f255-119">Это позволит разработчикам использовать `Parser.dll` независимо от `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="0f255-119">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="0f255-120">Если библиотека состоит из нескольких сборок, которые не используются сами по себе, то их предпочтительнее объединить в одном пакете.</span><span class="sxs-lookup"><span data-stu-id="0f255-120">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="0f255-121">В продолжение предыдущего примера, если сборка `Parser.dll` содержит код, который используется только сборкой `Utilities.dll`, то сборку `Parser.dll` лучше включить в тот же пакет.</span><span class="sxs-lookup"><span data-stu-id="0f255-121">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="0f255-122">Аналогичным образом, если сборка `Utilities.dll` зависит от сборки `Utilities.resources.dll`, которая не используется сама по себе, включите их в один пакет.</span><span class="sxs-lookup"><span data-stu-id="0f255-122">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="0f255-123">Ресурсы представляют собой особый случай.</span><span class="sxs-lookup"><span data-stu-id="0f255-123">Resources are, in fact, a special case.</span></span> <span data-ttu-id="0f255-124">Когда пакет устанавливается в проекте, NuGet автоматически добавляет ссылки на библиотеки DLL сборок в пакете, *кроме* тех из них, в именах которых есть `.resources.dll`, так как они считаются локализованными вспомогательными сборками (см. раздел [Создание локализованных пакетов](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="0f255-124">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="0f255-125">По этой причине следует избегать использования `.resources.dll` в именах файлов пакета, которые содержат важный код.</span><span class="sxs-lookup"><span data-stu-id="0f255-125">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="0f255-126">Если библиотека содержит сборки COM-взаимодействия, следуйте дополнительным указаниям в разделе [Разработка пакетов, содержащих сборки COM-взаимодействия](#authoring-packages-with-com-interop-assemblies).</span><span class="sxs-lookup"><span data-stu-id="0f255-126">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="0f255-127">Назначение и структура файла NUSPEC</span><span class="sxs-lookup"><span data-stu-id="0f255-127">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="0f255-128">После того как вы решите, какие файлы нужно включить в пакет, следует создать манифест пакета в XML-файле `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="0f255-128">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="0f255-129">Манифест служит следующим целям:</span><span class="sxs-lookup"><span data-stu-id="0f255-129">The manifest:</span></span>

1. <span data-ttu-id="0f255-130">Описывает содержимое пакета и сам включается в него.</span><span class="sxs-lookup"><span data-stu-id="0f255-130">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="0f255-131">Управляет созданием пакета и предоставляет диспетчеру NuGet указания по установке пакета в проекте.</span><span class="sxs-lookup"><span data-stu-id="0f255-131">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="0f255-132">Например, в манифесте определяются другие зависимости пакета, чтобы диспетчер NuGet мог также установить их при установке основного пакета.</span><span class="sxs-lookup"><span data-stu-id="0f255-132">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="0f255-133">Содержит обязательные и необязательные свойства, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="0f255-133">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="0f255-134">Полные сведения, включая описание свойств, которые не упомянуты в этом разделе, см. в [справочнике по файлам NUSPEC](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="0f255-134">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="0f255-135">Обязательные свойства:</span><span class="sxs-lookup"><span data-stu-id="0f255-135">Required properties:</span></span>

- <span data-ttu-id="0f255-136">идентификатор пакета, который должен быть уникальным в пределах коллекции, содержащей пакет;</span><span class="sxs-lookup"><span data-stu-id="0f255-136">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="0f255-137">определенный номер версии в формате *основной_номер.дополнительный_номер.исправление[-суффикс]*, где *-суффикс* указывает на [предварительные версии](prerelease-packages.md);</span><span class="sxs-lookup"><span data-stu-id="0f255-137">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="0f255-138">название пакета, которое должно отображаться на сайте размещения (например, nuget.org);</span><span class="sxs-lookup"><span data-stu-id="0f255-138">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="0f255-139">сведения об авторе и владельце;</span><span class="sxs-lookup"><span data-stu-id="0f255-139">Author and owner information.</span></span>
- <span data-ttu-id="0f255-140">подробное описание пакета.</span><span class="sxs-lookup"><span data-stu-id="0f255-140">A long description of the package.</span></span>

<span data-ttu-id="0f255-141">Часто используемые необязательные свойства:</span><span class="sxs-lookup"><span data-stu-id="0f255-141">Common optional properties:</span></span>

- <span data-ttu-id="0f255-142">заметки о выпуске;</span><span class="sxs-lookup"><span data-stu-id="0f255-142">Release notes</span></span>
- <span data-ttu-id="0f255-143">сведения об авторских правах;</span><span class="sxs-lookup"><span data-stu-id="0f255-143">Copyright information</span></span>
- <span data-ttu-id="0f255-144">краткое описание для [пользовательского интерфейса диспетчера пакетов в Visual Studio](../tools/package-manager-ui.md);</span><span class="sxs-lookup"><span data-stu-id="0f255-144">A short description for the [Package Manager UI in Visual Studio](../tools/package-manager-ui.md)</span></span>
- <span data-ttu-id="0f255-145">код языка;</span><span class="sxs-lookup"><span data-stu-id="0f255-145">A locale ID</span></span>
- <span data-ttu-id="0f255-146">URL проекта</span><span class="sxs-lookup"><span data-stu-id="0f255-146">Project URL</span></span>
- <span data-ttu-id="0f255-147">лицензия в виде выражения или файла (`licenseUrl` скоро станет нерекомендуемым, используйте [nuspec-элемент метаданных `license`](../reference/nuspec.md#license));</span><span class="sxs-lookup"><span data-stu-id="0f255-147">License as an expression or file (`licenseUrl` is being deprecated, use the [`license` nuspec metadata element](../reference/nuspec.md#license))</span></span>
- <span data-ttu-id="0f255-148">URL-адрес значка;</span><span class="sxs-lookup"><span data-stu-id="0f255-148">An icon URL</span></span>
- <span data-ttu-id="0f255-149">список зависимостей и ссылок;</span><span class="sxs-lookup"><span data-stu-id="0f255-149">Lists of dependencies and references</span></span>
- <span data-ttu-id="0f255-150">теги, упрощающие поиск в коллекции.</span><span class="sxs-lookup"><span data-stu-id="0f255-150">Tags that assist in gallery searches</span></span>

<span data-ttu-id="0f255-151">Ниже приведен типичный (но вымышленный) файл `.nuspec` с комментариями, описывающими свойства.</span><span class="sxs-lookup"><span data-stu-id="0f255-151">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
        <!-- The identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- The package version number that is used when resolving dependencies -->
        <version>1.8.3-beta</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

<span data-ttu-id="0f255-152">Подробные сведения об объявлении зависимостей и указании номеров версий см. в разделе [Управление версиями пакета](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="0f255-152">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="0f255-153">Доступ к ресурсам зависимостей в пакете можно также предоставлять напрямую с помощью атрибутов `include` и `exclude` элемента `dependency`.</span><span class="sxs-lookup"><span data-stu-id="0f255-153">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="0f255-154">См. подраздел "Зависимости" в разделе [Справочник по файлам NUSPEC](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="0f255-154">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="0f255-155">Так как манифест включается в пакет, создаваемый на его основе, вы можете получить дополнительные примеры, изучив существующие пакеты.</span><span class="sxs-lookup"><span data-stu-id="0f255-155">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="0f255-156">Хорошим их источником может служить папка *global-packages* на компьютере, расположение которой можно получить с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="0f255-156">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="0f255-157">Перейдите в любую папку *пакет\версия*, скопируйте файл `.nupkg` в файл `.zip`, затем откройте этот файл `.zip` и изучите содержимое файла `.nuspec` в нем.</span><span class="sxs-lookup"><span data-stu-id="0f255-157">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="0f255-158">При создании файла `.nuspec` из проекта Visual Studio манифест содержит токены, которые заменяются сведениями из проекта при сборке пакета.</span><span class="sxs-lookup"><span data-stu-id="0f255-158">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="0f255-159">См. раздел [Создание файла NUSPEC на основе проекта Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="0f255-159">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="0f255-160">Создание файла NUSPEC</span><span class="sxs-lookup"><span data-stu-id="0f255-160">Creating the .nuspec file</span></span>

<span data-ttu-id="0f255-161">Создание полного манифеста, как правило, начинается с базового файла `.nuspec`, который создается одним из следующих способов на основе:</span><span class="sxs-lookup"><span data-stu-id="0f255-161">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- <span data-ttu-id="0f255-162">[рабочего каталога, соответствующего соглашениям](#from-a-convention-based-working-directory);</span><span class="sxs-lookup"><span data-stu-id="0f255-162">[A convention-based working directory](#from-a-convention-based-working-directory)</span></span>
- <span data-ttu-id="0f255-163">[библиотеки DLL сборки](#from-an-assembly-dll);</span><span class="sxs-lookup"><span data-stu-id="0f255-163">[An assembly DLL](#from-an-assembly-dll)</span></span>
- <span data-ttu-id="0f255-164">[проекта Visual Studio](#from-a-visual-studio-project);</span><span class="sxs-lookup"><span data-stu-id="0f255-164">[A Visual Studio project](#from-a-visual-studio-project)</span></span>    
- <span data-ttu-id="0f255-165">[нового файла со значениями по умолчанию](#new-file-with-default-values).</span><span class="sxs-lookup"><span data-stu-id="0f255-165">[New file with default values](#new-file-with-default-values)</span></span>

<span data-ttu-id="0f255-166">Затем нужно отредактировать файл вручную так, чтобы он описывал содержимое итогового пакета.</span><span class="sxs-lookup"><span data-stu-id="0f255-166">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="0f255-167">Автоматически формируемые файлы `.nuspec` содержат заполнители, которые нужно изменить перед созданием пакета с помощью команды `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="0f255-167">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="0f255-168">Если файл `.nuspec` содержит заполнители, эта команда завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="0f255-168">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="0f255-169">На основе рабочего каталога, соответствующего соглашениям</span><span class="sxs-lookup"><span data-stu-id="0f255-169">From a convention-based working directory</span></span>

<span data-ttu-id="0f255-170">Так как пакет NuGet — это просто ZIP-файл, расширение которого изменено на `.nupkg`, зачастую проще всего создать нужную структуру папок в локальной файловой системе, а затем создать файл `.nuspec` на основе этой структуры.</span><span class="sxs-lookup"><span data-stu-id="0f255-170">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="0f255-171">Команда `nuget pack` автоматически добавляет все файлы, имеющиеся в этой структуре папок (кроме папок, начинающихся с `.`, что позволяет иметь закрытые файлы в этой же структуре).</span><span class="sxs-lookup"><span data-stu-id="0f255-171">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="0f255-172">Преимущество такого подхода в том, что вам не нужно указывать в манифесте файлы, которые требуется включить в пакет (как описано далее в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="0f255-172">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="0f255-173">В процессе сборки можно создать структуру папок, которая будет в точности перенесена в пакет, и легко включить в него другие файлы, которые в противном случае не были бы добавлены в проект:</span><span class="sxs-lookup"><span data-stu-id="0f255-173">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="0f255-174">содержимое и исходный код, которые следует внедрить в конечный проект;</span><span class="sxs-lookup"><span data-stu-id="0f255-174">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="0f255-175">Сценарии PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f255-175">PowerShell scripts</span></span>
- <span data-ttu-id="0f255-176">преобразования существующих файлов конфигурации и исходного кода в проекте.</span><span class="sxs-lookup"><span data-stu-id="0f255-176">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="0f255-177">Ниже представлены соглашения в отношении папок.</span><span class="sxs-lookup"><span data-stu-id="0f255-177">The folder conventions are as follows:</span></span>

| <span data-ttu-id="0f255-178">Папка</span><span class="sxs-lookup"><span data-stu-id="0f255-178">Folder</span></span> | <span data-ttu-id="0f255-179">Описание</span><span class="sxs-lookup"><span data-stu-id="0f255-179">Description</span></span> | <span data-ttu-id="0f255-180">Действие при установке пакета</span><span class="sxs-lookup"><span data-stu-id="0f255-180">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f255-181">(корневая)</span><span class="sxs-lookup"><span data-stu-id="0f255-181">(root)</span></span> | <span data-ttu-id="0f255-182">Расположение файла readme.txt</span><span class="sxs-lookup"><span data-stu-id="0f255-182">Location for readme.txt</span></span> | <span data-ttu-id="0f255-183">При установке пакета в Visual Studio отображается файл readme.txt в корневой папке проекта.</span><span class="sxs-lookup"><span data-stu-id="0f255-183">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="0f255-184">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="0f255-184">lib/{tfm}</span></span> | <span data-ttu-id="0f255-185">Файлы сборки (`.dll`), документации (`.xml`) и символов (`.pdb`) для данного моникера целевой платформы (TFM)</span><span class="sxs-lookup"><span data-stu-id="0f255-185">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="0f255-186">Сборки добавляются как ссылки для использования во время компиляции или выполнения. Файлы `.xml` и `.pdb` копируются в папки проекта.</span><span class="sxs-lookup"><span data-stu-id="0f255-186">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="0f255-187">Сведения о создании вложенных папок для определенных целевых платформ см. в разделе [Поддержка нескольких целевых платформ](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="0f255-187">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="0f255-188">ref/{tfm}</span><span class="sxs-lookup"><span data-stu-id="0f255-188">ref/{tfm}</span></span> | <span data-ttu-id="0f255-189">Файлы сборки (`.dll`) и символов (`.pdb`) для определенного моникера целевой платформы (TFM)</span><span class="sxs-lookup"><span data-stu-id="0f255-189">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="0f255-190">Сборки добавляются как ссылки для использования только во время компиляции. Поэтому в папку bin проекта ничего не копируется.</span><span class="sxs-lookup"><span data-stu-id="0f255-190">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="0f255-191">runtimes</span><span class="sxs-lookup"><span data-stu-id="0f255-191">runtimes</span></span> | <span data-ttu-id="0f255-192">Файлы сборки (`.dll`), символов (`.pdb`) и машинных ресурсов (`.pri`) для определенной архитектуры</span><span class="sxs-lookup"><span data-stu-id="0f255-192">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="0f255-193">Сборки добавляются как ссылки для использования только во время выполнения. Остальные файлы копируются в папки проекта.</span><span class="sxs-lookup"><span data-stu-id="0f255-193">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="0f255-194">В папке `/ref/{tfm}` всегда должна быть соответствующая сборка (TFM) для `AnyCPU`, чтобы предоставить соответствующие сборки, используемые во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="0f255-194">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="0f255-195">См. раздел [Поддержка нескольких целевых платформ](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="0f255-195">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="0f255-196">содержание</span><span class="sxs-lookup"><span data-stu-id="0f255-196">content</span></span> | <span data-ttu-id="0f255-197">Произвольные файлы</span><span class="sxs-lookup"><span data-stu-id="0f255-197">Arbitrary files</span></span> | <span data-ttu-id="0f255-198">Содержимое копируется в корневую папку проекта.</span><span class="sxs-lookup"><span data-stu-id="0f255-198">Contents are copied to the project root.</span></span> <span data-ttu-id="0f255-199">Папку **content** можно представить как корневую папку целевого приложения, которое будет использовать пакет.</span><span class="sxs-lookup"><span data-stu-id="0f255-199">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="0f255-200">Чтобы пакет добавил изображение в папку */images* приложения, поместите это изображение в папку *content/images* пакета.</span><span class="sxs-lookup"><span data-stu-id="0f255-200">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="0f255-201">выполнить сборку</span><span class="sxs-lookup"><span data-stu-id="0f255-201">build</span></span> | <span data-ttu-id="0f255-202">Файлы MSBuild `.targets` и `.props`</span><span class="sxs-lookup"><span data-stu-id="0f255-202">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="0f255-203">Автоматически вставляются в файл проекта или файл `project.lock.json` (NuGet 3.x или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="0f255-203">Automatically inserted into the project file or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="0f255-204">средства</span><span class="sxs-lookup"><span data-stu-id="0f255-204">tools</span></span> | <span data-ttu-id="0f255-205">Скрипты и программы PowerShell, доступные из консоли диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="0f255-205">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="0f255-206">Папка `tools` добавляется в переменную среды `PATH` только для консоли диспетчера пакетов (в частности, она *не* добавляется в переменную `PATH` для среды MSBuild при сборке проекта).</span><span class="sxs-lookup"><span data-stu-id="0f255-206">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="0f255-207">Так как в структуре папок может быть сколько угодно сборок для любого числа целевых платформ, этот метод обязателен при создании пакетов, поддерживающих несколько платформ.</span><span class="sxs-lookup"><span data-stu-id="0f255-207">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="0f255-208">После того как вы подготовите нужную структуру папок, выполните в ней следующую команду, чтобы создать файл `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="0f255-208">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="0f255-209">Созданный файл `.nuspec` не содержит явных ссылок на файлы в структуре папок.</span><span class="sxs-lookup"><span data-stu-id="0f255-209">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="0f255-210">NuGet автоматически включает все файлы при создании пакета.</span><span class="sxs-lookup"><span data-stu-id="0f255-210">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="0f255-211">Однако вам необходимо отредактировать значения-заполнители в других частях манифеста.</span><span class="sxs-lookup"><span data-stu-id="0f255-211">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="0f255-212">На основе библиотеки DLL сборки</span><span class="sxs-lookup"><span data-stu-id="0f255-212">From an assembly DLL</span></span>

<span data-ttu-id="0f255-213">В такой простой ситуации, как создание пакета на основе сборки, вы можете создать файл `.nuspec` из содержащихся в сборке метаданных с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="0f255-213">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="0f255-214">При использовании такого формата ряд заполнителей в манифесте заменяется конкретными значениями из сборки.</span><span class="sxs-lookup"><span data-stu-id="0f255-214">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="0f255-215">Например, свойству `<id>` присваивается имя сборки, а свойству `<version>` — ее версия.</span><span class="sxs-lookup"><span data-stu-id="0f255-215">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="0f255-216">Однако остальные свойства в манифесте не имеют соответствующих значений в сборке и поэтому по-прежнему содержат заполнители.</span><span class="sxs-lookup"><span data-stu-id="0f255-216">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="0f255-217">На основе проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0f255-217">From a Visual Studio project</span></span>

<span data-ttu-id="0f255-218">Создавать файл `.nuspec` на основе файла `.csproj` или `.vbproj` удобно, так как ссылки на другие пакеты, установленные в проекте, как и на зависимости, создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="0f255-218">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="0f255-219">Просто выполните следующую команду в папке, в которой находится файл проекта:</span><span class="sxs-lookup"><span data-stu-id="0f255-219">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="0f255-220">Получившийся файл `<project-name>.nuspec` содержит *токены*, которые заменяются во время создания пакета значениями их проекта, включая ссылки на другие пакеты, которые уже установлены.</span><span class="sxs-lookup"><span data-stu-id="0f255-220">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="0f255-221">Токен отделяется символами `$` с обеих сторон свойства проекта.</span><span class="sxs-lookup"><span data-stu-id="0f255-221">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="0f255-222">Например, значение `<id>` в созданном таким образом манифесте, как правило, имеет следующий вид:</span><span class="sxs-lookup"><span data-stu-id="0f255-222">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="0f255-223">Этот токен заменяется значением `AssemblyName` из файла проекта во время упаковки.</span><span class="sxs-lookup"><span data-stu-id="0f255-223">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="0f255-224">Точные сведения о том, как значения из проекта сопоставляются с токенами `.nuspec`, см. в [справочнике по токенам замены](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="0f255-224">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="0f255-225">Токены избавляют от необходимости изменять критически важные значения, такие как номер версии, в файле `.nuspec` при обновлении пакета.</span><span class="sxs-lookup"><span data-stu-id="0f255-225">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="0f255-226">(При необходимости токены всегда можно заменить на конкретные значения.)</span><span class="sxs-lookup"><span data-stu-id="0f255-226">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="0f255-227">Обратите внимание на то, что при работе с проектом Visual Studio доступно несколько дополнительных параметров создания пакета, которые описываются далее в подразделе [Выполнение команды nuget pack для создания файла NUPKG](#running-nuget-pack-to-generate-the-nupkg-file).</span><span class="sxs-lookup"><span data-stu-id="0f255-227">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="0f255-228">Пакеты на уровне решения</span><span class="sxs-lookup"><span data-stu-id="0f255-228">Solution-level packages</span></span>

<span data-ttu-id="0f255-229">*Только в NuGet 2.x. Недоступно в NuGet 3.0 и более поздних версиях.*</span><span class="sxs-lookup"><span data-stu-id="0f255-229">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="0f255-230">В NuGet 2.x поддерживалась концепция пакетов на уровне решения, которые устанавливают средства или дополнительные команды для консоли диспетчера команд (содержимое папки `tools`), но не добавляют ссылки, содержимое или настройки сборки в проекты решения.</span><span class="sxs-lookup"><span data-stu-id="0f255-230">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="0f255-231">Такие пакеты не содержат файлов непосредственно в папках `lib`, `content` или `build`, а их зависимости не содержат файлов в соответствующих папках `lib`, `content` или `build`.</span><span class="sxs-lookup"><span data-stu-id="0f255-231">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="0f255-232">NuGet отслеживает установленные пакеты уровня решения в файле `packages.config` в папке `.nuget`, а не в файле `packages.config` проекта.</span><span class="sxs-lookup"><span data-stu-id="0f255-232">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="0f255-233">Новый файл со значениями по умолчанию</span><span class="sxs-lookup"><span data-stu-id="0f255-233">New file with default values</span></span>

<span data-ttu-id="0f255-234">Следующая команда создает манифест по умолчанию с заполнителями, формируя надлежащую структуру файлов:</span><span class="sxs-lookup"><span data-stu-id="0f255-234">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="0f255-235">Если не указать параметр \<package-name\>, получившийся файл будет иметь имя `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="0f255-235">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="0f255-236">Если указать имя, например `Contoso.Utility.UsefulStuff`, файл будет иметь имя `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="0f255-236">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="0f255-237">Полученный файл `.nuspec` содержит заполнители для значений, например `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="0f255-237">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="0f255-238">Прежде чем использовать этот файл для создания итогового файла `.nupkg`, его необходимо отредактировать.</span><span class="sxs-lookup"><span data-stu-id="0f255-238">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="0f255-239">Выбор уникального идентификатора пакета и задание номера версии</span><span class="sxs-lookup"><span data-stu-id="0f255-239">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="0f255-240">Идентификатор пакета (элемент `<id>`) и номер версии (элемент `<version>`) — два самых важных значения в манифесте, так как они однозначно определяют код, содержащийся в пакете.</span><span class="sxs-lookup"><span data-stu-id="0f255-240">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="0f255-241">**Рекомендации в отношении идентификатора пакета**</span><span class="sxs-lookup"><span data-stu-id="0f255-241">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="0f255-242">**Уникальность**. Идентификатор должен быть уникальным в пределах nuget.org или другой коллекции, в которой размещается пакет.</span><span class="sxs-lookup"><span data-stu-id="0f255-242">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="0f255-243">Прежде чем задавать идентификатор, проверьте, не используется ли оно уже в соответствующей коллекции.</span><span class="sxs-lookup"><span data-stu-id="0f255-243">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="0f255-244">Во избежание конфликтов рекомендуется использовать в качестве первой части идентификатора название организации, например `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="0f255-244">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="0f255-245">**Имена в стиле пространств имен**. Используйте шаблон, по которому строятся имена пространств имен в .NET, используя нотацию с точками, а не с дефисами.</span><span class="sxs-lookup"><span data-stu-id="0f255-245">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="0f255-246">Например, используйте идентификатор `Contoso.Utility.UsefulStuff` вместо `Contoso-Utility-UsefulStuff` или `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="0f255-246">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="0f255-247">Пользователям также удобно, когда идентификатор пакета соответствует пространствам имен, используемым в коде.</span><span class="sxs-lookup"><span data-stu-id="0f255-247">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="0f255-248">**Примеры пакетов**. Если вы создаете пакет с примером кода, демонстрирующим использование другого пакета, добавьте к идентификатору суффикс `.Sample`, например `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="0f255-248">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="0f255-249">(Образец пакета, конечно, должен иметь зависимость от другого пакета.) При создании образца пакета используйте описанный выше метод на основе рабочего каталога, соответствующего соглашениям.</span><span class="sxs-lookup"><span data-stu-id="0f255-249">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="0f255-250">В папке `content` разместите код образца в папке с именем `\Samples\<identifier>`, например `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="0f255-250">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="0f255-251">**Рекомендации в отношении версии пакета**</span><span class="sxs-lookup"><span data-stu-id="0f255-251">**Best practices for the package version:**</span></span>

- <span data-ttu-id="0f255-252">Как правило, версия пакета должна соответствовать версии библиотеки, хотя это не строгое требование.</span><span class="sxs-lookup"><span data-stu-id="0f255-252">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="0f255-253">Это легко реализовать, если пакет ограничен единственной сборкой, как было описано выше в подразделе [Выбор сборок для добавления в пакет](#deciding-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="0f255-253">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="0f255-254">В целом помните, что при разрешении зависимостей диспетчер NuGet ориентируется на версии пакетов, а не на версии сборок.</span><span class="sxs-lookup"><span data-stu-id="0f255-254">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="0f255-255">При применении нестандартной схемы версий обязательно учитывайте правила управления версиями в NuGet, которые изложены в разделе [Управление версиями пакета](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="0f255-255">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="0f255-256">Разобраться в принципах управления версиями также может помочь следующая серия коротких записей блога:</span><span class="sxs-lookup"><span data-stu-id="0f255-256">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="0f255-257">Часть 1. Решение проблем с DLL</span><span class="sxs-lookup"><span data-stu-id="0f255-257">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="0f255-258">Часть 2. Базовый алгоритм</span><span class="sxs-lookup"><span data-stu-id="0f255-258">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="0f255-259">Часть 3. Унификация путем переадресации привязок</span><span class="sxs-lookup"><span data-stu-id="0f255-259">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a><span data-ttu-id="0f255-260">Указание типа пакета</span><span class="sxs-lookup"><span data-stu-id="0f255-260">Setting a package type</span></span>

<span data-ttu-id="0f255-261">В NuGet 3.5 и более поздних версиях пакету можно присвоить определенный *тип пакета*, указывающий на его предполагаемое назначение.</span><span class="sxs-lookup"><span data-stu-id="0f255-261">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="0f255-262">Пакеты, которым не назначен тип, включая все пакеты, созданные в более ранних версиях NuGet, по умолчанию имеют тип `Dependency`.</span><span class="sxs-lookup"><span data-stu-id="0f255-262">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="0f255-263">Пакеты типа `Dependency` добавляют ресурсы времени сборки или времени выполнения в библиотеки и приложения, и их можно устанавливать в проектах любого типа (при условии, что они совместимы).</span><span class="sxs-lookup"><span data-stu-id="0f255-263">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="0f255-264">Пакеты типа `DotnetCliTool` являются расширениями [интерфейса командной строки .NET](/dotnet/articles/core/tools/index) и вызываются из командной строки.</span><span class="sxs-lookup"><span data-stu-id="0f255-264">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="0f255-265">Такие пакеты можно устанавливать только в проектах .NET Core, и они не влияют на операции восстановления.</span><span class="sxs-lookup"><span data-stu-id="0f255-265">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="0f255-266">Дополнительные сведения об этих расширениях проекта можно найти в документации по [расширяемости .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).</span><span class="sxs-lookup"><span data-stu-id="0f255-266">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="0f255-267">Для пакетов пользовательского типа применяются произвольные идентификаторы, в которых соблюдаются те же правила формата, что и в идентификаторах пакетов.</span><span class="sxs-lookup"><span data-stu-id="0f255-267">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="0f255-268">Типы, отличные от `Dependency` и `DotnetCliTool`, однако, не распознаются диспетчером пакетов NuGet в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f255-268">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="0f255-269">Типы пакетов задаются в файле `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="0f255-269">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="0f255-270">В целях обратной совместимости лучше *не* задавать тип `Dependency` явным образом, позволив диспетчеру NuGet определить его автоматически, что происходит, если тип не указан.</span><span class="sxs-lookup"><span data-stu-id="0f255-270">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="0f255-271">`.nuspec`: укажите тип пакета в узле `packageTypes\packageType` элемента `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="0f255-271">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="0f255-272">Добавление файла сведений и других файлов</span><span class="sxs-lookup"><span data-stu-id="0f255-272">Adding a readme and other files</span></span>

<span data-ttu-id="0f255-273">Чтобы явным образом указать файлы, которые следует включить в пакет, используйте узел `<files>` в файле `.nuspec`, который находится *после* тега `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="0f255-273">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> <span data-ttu-id="0f255-274">При использовании подхода на основе рабочего каталога, соответствующего соглашениям, файл readme.txt можно поместить в корневую папку пакета, а другое содержимое — в папку `content`.</span><span class="sxs-lookup"><span data-stu-id="0f255-274">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="0f255-275">Элементы `<file>` в манифесте не требуются.</span><span class="sxs-lookup"><span data-stu-id="0f255-275">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="0f255-276">Если в корневую папку пакета добавлен файл с именем `readme.txt`, Visual Studio отображает содержимое этого файла в виде обычного текста сразу после установки пакета напрямую.</span><span class="sxs-lookup"><span data-stu-id="0f255-276">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="0f255-277">(Файлы сведений не отображаются для пакетов, устанавливаемых как зависимости.)</span><span class="sxs-lookup"><span data-stu-id="0f255-277">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="0f255-278">Например, вот как выглядит файл сведений для пакета HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="0f255-278">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Отображение файла сведений для пакета NuGet при установке](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="0f255-280">Если узел `<files>` в файле `.nuspec` пуст, NuGet включает в пакет только содержимое из папки `lib`.</span><span class="sxs-lookup"><span data-stu-id="0f255-280">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="0f255-281">Включение в пакет свойств и целевых объектов MSBuild</span><span class="sxs-lookup"><span data-stu-id="0f255-281">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="0f255-282">В некоторых случаях в проекты, использующие пакет, необходимо добавить пользовательские целевые объекты сборки или свойства, например, если во время сборки должно запускаться пользовательское средство или процесс.</span><span class="sxs-lookup"><span data-stu-id="0f255-282">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="0f255-283">Для этого нужно поместить файлы в формате `<package_id>.targets` или `<package_id>.props` (например, `Contoso.Utility.UsefulStuff.targets`) в папку `\build` проекта.</span><span class="sxs-lookup"><span data-stu-id="0f255-283">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="0f255-284">Файлы в корневой папке `\build` считаются пригодными для всех целевых платформ.</span><span class="sxs-lookup"><span data-stu-id="0f255-284">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="0f255-285">Чтобы предоставить файлы для определенных платформ, сначала поместите их в соответствующие вложенные папки, например следующие:</span><span class="sxs-lookup"><span data-stu-id="0f255-285">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="0f255-286">Затем в файле `.nuspec` укажите ссылки на эти файлы в узле `<files>`:</span><span class="sxs-lookup"><span data-stu-id="0f255-286">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

<span data-ttu-id="0f255-287">Включение свойств и целевых объектов MSBuild в пакет [появилось в NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), поэтому рекомендуется добавить атрибут `minClientVersion="2.5"` в элемент `metadata`, чтобы указать минимальную версию клиента NuGet, необходимую для использования пакета.</span><span class="sxs-lookup"><span data-stu-id="0f255-287">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="0f255-288">Когда NuGet устанавливает пакет с `\build` файлом, он добавляет элементы MSBuild `<Import>` в файл проекта, указывая на `.targets` и `.props` файла.</span><span class="sxs-lookup"><span data-stu-id="0f255-288">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="0f255-289">(Файлы `.props` добавляются в начале файла проекта, а файлы `.targets` — в конце.) Отдельный условный элемент MSBuild `<Import>` добавляется в каждую требуемую версию .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="0f255-289">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="0f255-290">Файлы MSBuild `.props` и `.targets` для трансграничного таргетинга можно поместить в папку `\buildMultiTargeting`.</span><span class="sxs-lookup"><span data-stu-id="0f255-290">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildMultiTargeting` folder.</span></span> <span data-ttu-id="0f255-291">Во время установки пакета NuGet добавляет соответствующие элементы `<Import>` в файл проекта с условием, что требуемую версию .NET Framework не задано (свойство MSBuild `$(TargetFramework)` должно быть пустым).</span><span class="sxs-lookup"><span data-stu-id="0f255-291">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="0f255-292">В NuGet 3.x целевые платформы не добавляются в проект, а предоставляются через файл `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="0f255-292">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="0f255-293">Разработка пакетов, содержащих сборки COM-взаимодействия</span><span class="sxs-lookup"><span data-stu-id="0f255-293">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="0f255-294">Пакеты, содержащие сборки COM-взаимодействия, должны включать в себя соответствующий [файл целей](#including-msbuild-props-and-targets-in-a-package), чтобы в проекты были добавлены правильные метаданные `EmbedInteropTypes` в формате PackageReference.</span><span class="sxs-lookup"><span data-stu-id="0f255-294">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="0f255-295">По умолчанию метаданные `EmbedInteropTypes` всегда имеют значение false для всех сборок при использовании PackageReference, поэтому файл целей добавляет эти метаданные явным образом.</span><span class="sxs-lookup"><span data-stu-id="0f255-295">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="0f255-296">Во избежание конфликтов имя цели должно быть уникальным. В идеале следует использовать сочетание имен пакета и внедряемой сборки, заменив им элемент `{InteropAssemblyName}` в приведенном ниже примере.</span><span class="sxs-lookup"><span data-stu-id="0f255-296">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="0f255-297">(Пример см. также на странице [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop).)</span><span class="sxs-lookup"><span data-stu-id="0f255-297">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="0f255-298">Имейте в виду, что при использовании формата управления `packages.config` добавление ссылок на сборки из пакетов приводит к тому, что NuGet и Visual Studio проверяют наличие сборок COM-взаимодействия и присваивают свойству `EmbedInteropTypes` в файле проекта значение true.</span><span class="sxs-lookup"><span data-stu-id="0f255-298">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="0f255-299">В этом случае цели переопределяются.</span><span class="sxs-lookup"><span data-stu-id="0f255-299">In this case the targets are overriden.</span></span>

<span data-ttu-id="0f255-300">Кроме того, по умолчанию [ресурсы сборки не передаются транзитивно](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="0f255-300">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="0f255-301">Пакеты, созданные описанным здесь способом, работают иначе, если они извлекаются в качестве транзитивной зависимости из проекта в ссылку на проект.</span><span class="sxs-lookup"><span data-stu-id="0f255-301">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="0f255-302">Пользователь пакета может разрешить их передачу, изменив значение PrivateAssets по умолчанию так, чтобы сборка не включалась.</span><span class="sxs-lookup"><span data-stu-id="0f255-302">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="0f255-303">Выполнение команды nuget pack для создания файла NUPKG</span><span class="sxs-lookup"><span data-stu-id="0f255-303">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="0f255-304">Чтобы создать пакет на основе сборки или рабочего каталога, соответствующего соглашениям, выполните команду `nuget pack`, указав файл `.nuspec`, где `<project-name>` необходимо заменить на имя файла:</span><span class="sxs-lookup"><span data-stu-id="0f255-304">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="0f255-305">При использовании проекта Visual Studio выполните команду `nuget pack`, указав файл проекта. В результате автоматически загрузится файл `.nuspec` проекта, и все токены в нем будут заменены значениями из файла проекта.</span><span class="sxs-lookup"><span data-stu-id="0f255-305">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="0f255-306">Использование файла проекта напрямую является необходимым для замены токенов, так как проект является источником значений токенов.</span><span class="sxs-lookup"><span data-stu-id="0f255-306">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="0f255-307">Замена токенов не производится при использовании команды `nuget pack` с файлом `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="0f255-307">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="0f255-308">В любом случае команда `nuget pack` исключает папки, начинающиеся с точки, например `.git` или `.hg`.</span><span class="sxs-lookup"><span data-stu-id="0f255-308">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="0f255-309">NuGet указывает, есть ли в файле `.nuspec` ошибки, требующие исправления, например, если вы забыли изменить значения-заполнители в манифесте.</span><span class="sxs-lookup"><span data-stu-id="0f255-309">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="0f255-310">После успешного выполнения команды `nuget pack` вы получаете файл `.nupkg`, который можно опубликовать в подходящей коллекции, как описано в разделе [Публикация пакета](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="0f255-310">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="0f255-311">После создания пакета его полезно просмотреть, открыв в средстве [Обозреватель пакетов](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer).</span><span class="sxs-lookup"><span data-stu-id="0f255-311">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="0f255-312">В нем в графической форме представлено содержимое пакета и его манифест.</span><span class="sxs-lookup"><span data-stu-id="0f255-312">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="0f255-313">Вы также можете переименовать полученный файл `.nupkg` в файл `.zip` и просмотреть его содержимое напрямую.</span><span class="sxs-lookup"><span data-stu-id="0f255-313">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="0f255-314">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="0f255-314">Additional options</span></span>

<span data-ttu-id="0f255-315">С командой `nuget pack` можно использовать различные параметры командной строки для исключения файлов, переопределения номера версии в манифесте, изменения папки выходных данных и совершения других действий.</span><span class="sxs-lookup"><span data-stu-id="0f255-315">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="0f255-316">Полный список параметров см. в [справочнике по команде pack](../tools/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="0f255-316">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="0f255-317">Ниже приводятся некоторые часто используемые с проектами Visual Studio параметры.</span><span class="sxs-lookup"><span data-stu-id="0f255-317">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="0f255-318">**Проекты, на которые указывают ссылки**. Если проект ссылается на другие проекты, вы можете включить их в пакет или добавить в качестве зависимостей с помощью параметра `-IncludeReferencedProjects`.</span><span class="sxs-lookup"><span data-stu-id="0f255-318">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="0f255-319">Включение является рекурсивным, поэтому если `MyProject.csproj` ссылается на проекты B и C, а они ссылаются на проекты D, E и F, в пакет включаются файлы из проектов B, C, D, E и F.</span><span class="sxs-lookup"><span data-stu-id="0f255-319">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="0f255-320">Если в проекте, на который указывает ссылка, есть собственный файл `.nuspec`, NuGet вместо этого добавляет проект как зависимость.</span><span class="sxs-lookup"><span data-stu-id="0f255-320">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="0f255-321">Такой проект необходимо упаковать и опубликовать отдельно.</span><span class="sxs-lookup"><span data-stu-id="0f255-321">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="0f255-322">**Конфигурация сборки**. По умолчанию NuGet использует стандартную конфигурацию сборки, указанную в файле проекта. Обычно это конфигурация *Debug*.</span><span class="sxs-lookup"><span data-stu-id="0f255-322">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="0f255-323">Чтобы упаковать файлы из другой конфигурации сборки, например *Release*, используйте параметр `-properties`, указав конфигурацию:</span><span class="sxs-lookup"><span data-stu-id="0f255-323">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="0f255-324">**Символы**. Чтобы включить символы, позволяющие пользователям осуществлять пошаговое выполнение кода в пакете, используйте параметр `-Symbols`:</span><span class="sxs-lookup"><span data-stu-id="0f255-324">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="0f255-325">Тестирование установки пакета</span><span class="sxs-lookup"><span data-stu-id="0f255-325">Testing package installation</span></span>

<span data-ttu-id="0f255-326">Перед публикацией пакета, как правило, необходимо протестировать процесс его установки в проекте.</span><span class="sxs-lookup"><span data-stu-id="0f255-326">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="0f255-327">Это позволяет убедиться в том, что все необходимые файлы помещаются в нужные места.</span><span class="sxs-lookup"><span data-stu-id="0f255-327">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="0f255-328">Установку можно протестировать вручную в Visual Studio или в командной строке, выполнив стандартную [процедуру установки пакета](../consume-packages/ways-to-install-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="0f255-328">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/ways-to-install-a-package.md).</span></span>

<span data-ttu-id="0f255-329">Для автоматического тестирования выполните указанные ниже основные действия.</span><span class="sxs-lookup"><span data-stu-id="0f255-329">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="0f255-330">Скопируйте файл `.nupkg` в локальную папку.</span><span class="sxs-lookup"><span data-stu-id="0f255-330">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="0f255-331">Добавьте эту папку в источники пакета с помощью команды `nuget sources add -name <name> -source <path>` (см. описание [команды nuget sources](../tools/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="0f255-331">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="0f255-332">Обратите внимание на то, что на каждом компьютере этот локальный источник необходимо задать только один раз.</span><span class="sxs-lookup"><span data-stu-id="0f255-332">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="0f255-333">Установите пакет из источника с помощью команды `nuget install <packageID> -source <name>`, где `<name>` соответствует имени источника, предоставленному команде `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="0f255-333">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="0f255-334">Указание источника позволяет гарантировать, что пакет будет устанавливаться только из него.</span><span class="sxs-lookup"><span data-stu-id="0f255-334">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="0f255-335">В файловой системе проверьте, правильно ли установились файлы.</span><span class="sxs-lookup"><span data-stu-id="0f255-335">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f255-336">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="0f255-336">Next Steps</span></span>

<span data-ttu-id="0f255-337">Создав пакет, то есть файл `.nupkg`, вы можете опубликовать его в любой коллекции на ваш выбор, как описано в разделе [Публикация пакета](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="0f255-337">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="0f255-338">Вы также можете расширить возможности пакета или обеспечить поддержку других сценариев, как описано в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="0f255-338">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="0f255-339">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="0f255-339">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="0f255-340">Поддержка нескольких целевых платформ</span><span class="sxs-lookup"><span data-stu-id="0f255-340">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="0f255-341">Преобразования исходных файлов и файлов конфигурации</span><span class="sxs-lookup"><span data-stu-id="0f255-341">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="0f255-342">Локализация</span><span class="sxs-lookup"><span data-stu-id="0f255-342">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="0f255-343">Предварительные версии</span><span class="sxs-lookup"><span data-stu-id="0f255-343">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="0f255-344">Наконец, существуют дополнительные типы пакетов, о которых нужно знать:</span><span class="sxs-lookup"><span data-stu-id="0f255-344">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="0f255-345">Собственные пакеты</span><span class="sxs-lookup"><span data-stu-id="0f255-345">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="0f255-346">Пакеты символов</span><span class="sxs-lookup"><span data-stu-id="0f255-346">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
