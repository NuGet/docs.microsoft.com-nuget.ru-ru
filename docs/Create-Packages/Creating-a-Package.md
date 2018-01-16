---
title: "Создание пакета NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 456797cb-e3e4-4b88-9b01-8b5153cee802
description: "Подробное руководство по проектированию и созданию пакета NuGet, включая принятие решений по ключевым аспектам, таким как файлы и управление версиями."
keywords: "создание пакета NuGet, создание пакета, манифест nuspec, соглашения о пакетах NuGet, версия пакета NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6675d21a2900a1b61e17c08518b328732f4472c5
ms.sourcegitcommit: 1cb047b24b3b69d80e808c23b2ace0d98d2dfdcc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2018
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="54881-104">Создание пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="54881-104">Creating NuGet packages</span></span>

<span data-ttu-id="54881-105">Независимо от назначения вашего пакета или содержащегося в нем кода, вы можете создать с помощью программы `nuget.exe` компонент, которым можно поделиться с любым количеством разработчиков для совместного использования.</span><span class="sxs-lookup"><span data-stu-id="54881-105">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="54881-106">Инструкции по установке `nuget.exe` см. в разделе [Установка интерфейса командной строки NuGet](../guides/Install-NuGet.md#nuget-cli).</span><span class="sxs-lookup"><span data-stu-id="54881-106">To install `nuget.exe`, see [Install NuGet CLI](../guides/Install-NuGet.md#nuget-cli).</span></span> <span data-ttu-id="54881-107">Обратите внимание на то, что программа `nuget.exe` не входит в состав Visual Studio по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="54881-107">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="54881-108">С технической точки зрения, пакет NuGet — это просто ZIP-файл, расширение которого изменено на `.nupkg` и содержимое которого соответствует определенным соглашениям.</span><span class="sxs-lookup"><span data-stu-id="54881-108">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="54881-109">В этом разделе подробно описывается создание пакета, в котором соблюдаются эти соглашения.</span><span class="sxs-lookup"><span data-stu-id="54881-109">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="54881-110">Краткое руководство приводится в разделе [Создание и публикация пакета](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="54881-110">For a focused walkthrough, refer to [Create and Publish a Package Quickstart](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="54881-111">Создание пакета начинается с подготовки скомпилированного кода (сборок), символов и других файлов, которые должны быть включены в пакет (см. раздел [Процесс создания пакета](Overview-and-Workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="54881-111">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](Overview-and-Workflow.md)).</span></span> <span data-ttu-id="54881-112">Этот процесс производится независимо от компиляции и других задач по созданию файлов для пакета, хотя вы можете использовать информацию из файла проекта для синхронизации скомпилированных сборок и пакетов.</span><span class="sxs-lookup"><span data-stu-id="54881-112">This process is independent from compiling or otherwise generating the files that go into the package, although you can use draw from information in a project file to keep the compiled assemblines and packages in sync.</span></span>

<span data-ttu-id="54881-113">В этом разделе.</span><span class="sxs-lookup"><span data-stu-id="54881-113">In this topic:</span></span>

- [<span data-ttu-id="54881-114">Выбор сборок для добавления в пакет</span><span class="sxs-lookup"><span data-stu-id="54881-114">Deciding which assemblies to package</span></span>](#deciding-which-assemblies-to-package)
- [<span data-ttu-id="54881-115">Назначение и структура файла `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="54881-115">The role and structure of the `.nuspec` file</span></span>](#the-role-and-structure-of-the-nuspec-file)
- <span data-ttu-id="54881-116">[Создание файла `.nuspec`](#creating-the-nuspec-file) на основе:</span><span class="sxs-lookup"><span data-stu-id="54881-116">[Creating the `.nuspec` file](#creating-the-nuspec-file) from:</span></span>
    - <span data-ttu-id="54881-117">[рабочего каталога, соответствующего соглашениям](#from-a-convention-based-working-directory);</span><span class="sxs-lookup"><span data-stu-id="54881-117">[A convention-based working directory](#from-a-convention-based-working-directory)</span></span>
    - <span data-ttu-id="54881-118">[библиотеки DLL сборки](#from-an-assembly-dll);</span><span class="sxs-lookup"><span data-stu-id="54881-118">[An assembly DLL](#from-an-assembly-dll)</span></span>
    - <span data-ttu-id="54881-119">[проекта Visual Studio](#from-a-visual-studio-project);</span><span class="sxs-lookup"><span data-stu-id="54881-119">[A Visual Studio project](#from-a-visual-studio-project)</span></span>
    - <span data-ttu-id="54881-120">[нового файла со значениями по умолчанию](#new-file-with-default-values).</span><span class="sxs-lookup"><span data-stu-id="54881-120">[New file with default values](#new-file-with-default-values)</span></span>    
- [<span data-ttu-id="54881-121">Выбор уникального идентификатора пакета и задание номера версии</span><span class="sxs-lookup"><span data-stu-id="54881-121">Choosing a unique package identifier and setting the version number</span></span>](#choosing-a-unique-package-identifier-and-setting-the-version-number)
- <span data-ttu-id="54881-122">[Выбор типа пакета](#setting-a-package-type) (NuGet 3.5 или более поздней версии)</span><span class="sxs-lookup"><span data-stu-id="54881-122">[Setting a package type](#setting-a-package-type) (NuGet 3.5 and later)</span></span>
- [<span data-ttu-id="54881-123">Добавление файла сведений и других файлов</span><span class="sxs-lookup"><span data-stu-id="54881-123">Adding a readme and other files</span></span>](#adding-a-readme-and-other-files)
- [<span data-ttu-id="54881-124">Включение в пакет свойств и целевых объектов MSBuild</span><span class="sxs-lookup"><span data-stu-id="54881-124">Including MSBuild props and targets in a package</span></span>](#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="54881-125">Разработка пакетов, содержащих сборки COM-взаимодействия</span><span class="sxs-lookup"><span data-stu-id="54881-125">Authoring packages that contain COM interop assemblies</span></span>](#authoring-packages-with-com-interop-assemblies)
- [<span data-ttu-id="54881-126">Выполнение команды nuget pack для создания файла NUPKG</span><span class="sxs-lookup"><span data-stu-id="54881-126">Running nuget pack to generate the .nupkg file</span></span>](#running-nuget-pack-to-generate-the-nupkg-file)

<span data-ttu-id="54881-127">После выполнения этих основных действий можно реализовать и другие возможности, описываемые в разделах этой документации.</span><span class="sxs-lookup"><span data-stu-id="54881-127">After these core steps, you can incorporate a variety of other features as described elsewhere in this documentation.</span></span> <span data-ttu-id="54881-128">См. подраздел [Дальнейшие действия](#next-steps) ниже.</span><span class="sxs-lookup"><span data-stu-id="54881-128">See [Next steps](#next-steps) below.</span></span>

> [!Note]
> <span data-ttu-id="54881-129">Этот раздел относится к любым типам проектов, кроме проектов .NET Core с использованием Visual Studio 2017 и NuGet 4.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="54881-129">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="54881-130">В таких проектах .NET Core NuGet использует сведения в файле `.csproj` напрямую.</span><span class="sxs-lookup"><span data-stu-id="54881-130">In those .NET Core projects, NuGet uses information in the `.csproj` file directly.</span></span> <span data-ttu-id="54881-131">Подробные сведения см. в разделах [Создание пакетов .NET Standard с помощью Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) и [Пакет NuGet и восстановление целевых объектов MSBuild](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="54881-131">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="54881-132">Выбор сборок для добавления в пакет</span><span class="sxs-lookup"><span data-stu-id="54881-132">Deciding which assemblies to package</span></span>

<span data-ttu-id="54881-133">Большинство пакетов общего назначения содержат одну или несколько сборок, которые другие разработчики могут использовать в собственных проектах.</span><span class="sxs-lookup"><span data-stu-id="54881-133">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="54881-134">Как правило, для каждой сборки лучше создавать собственный пакет NuGet, если эти сборки используются независимо.</span><span class="sxs-lookup"><span data-stu-id="54881-134">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="54881-135">Например, если есть сборка `Utilities.dll`, которая зависит от сборки `Parser.dll`, но сборка `Parser.dll` также полезна сама по себе, создайте для каждой из этих сборок отдельный пакет.</span><span class="sxs-lookup"><span data-stu-id="54881-135">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="54881-136">Это позволит разработчикам использовать `Parser.dll` независимо от `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="54881-136">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="54881-137">Если библиотека состоит из нескольких сборок, которые не используются сами по себе, то их предпочтительнее объединить в одном пакете.</span><span class="sxs-lookup"><span data-stu-id="54881-137">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="54881-138">В продолжение предыдущего примера, если сборка `Parser.dll` содержит код, который используется только сборкой `Utilities.dll`, то сборку `Parser.dll` лучше включить в тот же пакет.</span><span class="sxs-lookup"><span data-stu-id="54881-138">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>
    - <span data-ttu-id="54881-139">Аналогичным образом, если сборка `Utilities.dll` зависит от сборки `Utilities.resources.dll`, которая не используется сама по себе, включите их в один пакет.</span><span class="sxs-lookup"><span data-stu-id="54881-139">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="54881-140">Ресурсы представляют собой особый случай.</span><span class="sxs-lookup"><span data-stu-id="54881-140">Resources are, in fact, a special case.</span></span> <span data-ttu-id="54881-141">Когда пакет устанавливается в проекте, NuGet автоматически добавляет ссылки на библиотеки DLL сборок в пакете, *кроме* тех из них, в именах которых есть `.resources.dll`, так как они считаются локализованными вспомогательными сборками (см. раздел [Создание локализованных пакетов](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="54881-141">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="54881-142">По этой причине следует избегать использования `.resources.dll` в именах файлов пакета, которые содержат важный код.</span><span class="sxs-lookup"><span data-stu-id="54881-142">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="54881-143">Если библиотека содержит сборки COM-взаимодействия, следуйте дополнительным указаниям в разделе [Разработка пакетов, содержащих сборки COM-взаимодействия](#authoring-packages-with-com-interop-assemblies).</span><span class="sxs-lookup"><span data-stu-id="54881-143">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="54881-144">Назначение и структура файла NUSPEC</span><span class="sxs-lookup"><span data-stu-id="54881-144">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="54881-145">После того как вы решите, какие файлы нужно включить в пакет, следует создать манифест пакета в XML-файле `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="54881-145">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="54881-146">Манифест служит следующим целям:</span><span class="sxs-lookup"><span data-stu-id="54881-146">The manifest:</span></span>

1. <span data-ttu-id="54881-147">Описывает содержимое пакета и сам включается в него.</span><span class="sxs-lookup"><span data-stu-id="54881-147">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="54881-148">Управляет созданием пакета и предоставляет диспетчеру NuGet указания по установке пакета в проекте.</span><span class="sxs-lookup"><span data-stu-id="54881-148">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="54881-149">Например, в манифесте определяются другие зависимости пакета, чтобы диспетчер NuGet мог также установить их при установке основного пакета.</span><span class="sxs-lookup"><span data-stu-id="54881-149">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="54881-150">Содержит обязательные и необязательные свойства, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="54881-150">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="54881-151">Полные сведения, включая описание свойств, которые не упомянуты в этом разделе, см. в [справочнике по файлам NUSPEC](../schema/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="54881-151">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../schema/nuspec.md).</span></span>

<span data-ttu-id="54881-152">Обязательные свойства:</span><span class="sxs-lookup"><span data-stu-id="54881-152">Required properties:</span></span>

- <span data-ttu-id="54881-153">идентификатор пакета, который должен быть уникальным в пределах коллекции, содержащей пакет;</span><span class="sxs-lookup"><span data-stu-id="54881-153">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="54881-154">определенный номер версии в формате *основной_номер.дополнительный_номер.исправление[-суффикс]*, где *-суффикс* указывает на [предварительные версии](Prerelease-Packages.md);</span><span class="sxs-lookup"><span data-stu-id="54881-154">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](Prerelease-Packages.md)</span></span>
- <span data-ttu-id="54881-155">название пакета, которое должно отображаться на сайте размещения (например, nuget.org);</span><span class="sxs-lookup"><span data-stu-id="54881-155">The package title as it should appears on the host (like nuget.org)</span></span>
- <span data-ttu-id="54881-156">сведения об авторе и владельце;</span><span class="sxs-lookup"><span data-stu-id="54881-156">Author and owner information.</span></span>
- <span data-ttu-id="54881-157">подробное описание пакета.</span><span class="sxs-lookup"><span data-stu-id="54881-157">A long description of the package.</span></span>

<span data-ttu-id="54881-158">Часто используемые необязательные свойства:</span><span class="sxs-lookup"><span data-stu-id="54881-158">Common optional properties:</span></span>

- <span data-ttu-id="54881-159">заметки о выпуске;</span><span class="sxs-lookup"><span data-stu-id="54881-159">Release notes</span></span>
- <span data-ttu-id="54881-160">сведения об авторских правах;</span><span class="sxs-lookup"><span data-stu-id="54881-160">Copyright information</span></span>
- <span data-ttu-id="54881-161">краткое описание для [пользовательского интерфейса диспетчера пакетов в Visual Studio](../Tools/Package-Manager-UI.md);</span><span class="sxs-lookup"><span data-stu-id="54881-161">A short description for the [Package Manager UI in Visual Studio](../Tools/Package-Manager-UI.md)</span></span>
- <span data-ttu-id="54881-162">код языка;</span><span class="sxs-lookup"><span data-stu-id="54881-162">A locale ID</span></span>
- <span data-ttu-id="54881-163">URL-адреса домашней страницы и лицензии;</span><span class="sxs-lookup"><span data-stu-id="54881-163">Home page and license URLs</span></span>
- <span data-ttu-id="54881-164">URL-адрес значка;</span><span class="sxs-lookup"><span data-stu-id="54881-164">An icon URL</span></span>
- <span data-ttu-id="54881-165">список зависимостей и ссылок;</span><span class="sxs-lookup"><span data-stu-id="54881-165">Lists of dependencies and references</span></span>
- <span data-ttu-id="54881-166">теги, упрощающие поиск в коллекции.</span><span class="sxs-lookup"><span data-stu-id="54881-166">Tags that assist in gallery searches</span></span>

<span data-ttu-id="54881-167">Ниже приведен типичный (но вымышленный) файл `.nuspec` с комментариями, описывающими свойства.</span><span class="sxs-lookup"><span data-stu-id="54881-167">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

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

    <!-- Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  -->
    <owners>dejanatc, rjdey</owners>

    <!-- License and project URLs provide links for the gallery -->
    <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
    <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

    <!-- The icon is used in Visual Studio's package manager UI -->
    <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

    <!-- If true, this value prompts the user to accept the license when
            installing the package. -->
    <requireLicenseAcceptance>false</requireLicenseAcceptance>

    <!-- Any details about this particular release -->
    <releaseNotes>Bug fixes and performance improvements</releaseNotes>

    <!-- The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. -->
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

<span data-ttu-id="54881-168">Подробные сведения об объявлении зависимостей и указании номеров версий см. в разделе [Управление версиями пакета](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="54881-168">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="54881-169">Доступ к ресурсам зависимостей в пакете можно также предоставлять напрямую с помощью атрибутов `include` и `exclude` элемента `dependency`.</span><span class="sxs-lookup"><span data-stu-id="54881-169">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="54881-170">См. подраздел "Зависимости" в разделе [Справочник по файлам NUSPEC](../Schema/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="54881-170">See [.nuspec Reference - Dependencies](../Schema/nuspec.md#dependencies).</span></span>

<span data-ttu-id="54881-171">Так как манифест включается в пакет, создаваемый на его основе, вы можете получить дополнительные примеры, изучив существующие пакеты.</span><span class="sxs-lookup"><span data-stu-id="54881-171">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="54881-172">Хорошим их источником может служить глобальный кэш пакетов на вашем компьютере, расположение которого можно получить с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="54881-172">A good source is the global package cache on your machine, the location of which is returned by the following command:</span></span>

```
nuget locals -list global-packages
```

<span data-ttu-id="54881-173">Перейдите в любую папку *пакет\версия*, скопируйте файл `.nupkg` в файл `.zip`, затем откройте этот файл `.zip` и изучите содержимое файла `.nuspec` в нем.</span><span class="sxs-lookup"><span data-stu-id="54881-173">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="54881-174">При создании файла `.nuspec` из проекта Visual Studio манифест содержит токены, которые заменяются сведениями из проекта при сборке пакета.</span><span class="sxs-lookup"><span data-stu-id="54881-174">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="54881-175">См. раздел [Создание файла NUSPEC на основе проекта Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="54881-175">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="54881-176">Создание файла NUSPEC</span><span class="sxs-lookup"><span data-stu-id="54881-176">Creating the .nuspec file</span></span>

<span data-ttu-id="54881-177">Создание полного манифеста, как правило, начинается с базового файла `.nuspec`, который создается одним из следующих способов на основе:</span><span class="sxs-lookup"><span data-stu-id="54881-177">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- <span data-ttu-id="54881-178">[рабочего каталога, соответствующего соглашениям](#from-a-convention-based-working-directory);</span><span class="sxs-lookup"><span data-stu-id="54881-178">[A convention-based working directory](#from-a-convention-based-working-directory)</span></span>
- <span data-ttu-id="54881-179">[библиотеки DLL сборки](#from-an-assembly-dll);</span><span class="sxs-lookup"><span data-stu-id="54881-179">[An assembly DLL](#from-an-assembly-dll)</span></span>
- <span data-ttu-id="54881-180">[проекта Visual Studio](#from-a-visual-studio-project);</span><span class="sxs-lookup"><span data-stu-id="54881-180">[A Visual Studio project](#from-a-visual-studio-project)</span></span>    
- <span data-ttu-id="54881-181">[нового файла со значениями по умолчанию](#new-file-with-default-values).</span><span class="sxs-lookup"><span data-stu-id="54881-181">[New file with default values](#new-file-with-default-values)</span></span>

<span data-ttu-id="54881-182">Затем нужно отредактировать файл вручную так, чтобы он описывал содержимое итогового пакета.</span><span class="sxs-lookup"><span data-stu-id="54881-182">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="54881-183">Автоматически формируемые файлы `.nuspec` содержат заполнители, которые нужно изменить перед созданием пакета с помощью команды `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="54881-183">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="54881-184">Если файл `.nuspec` содержит заполнители, эта команда завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="54881-184">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="54881-185">На основе рабочего каталога, соответствующего соглашениям</span><span class="sxs-lookup"><span data-stu-id="54881-185">From a convention-based working directory</span></span>

<span data-ttu-id="54881-186">Так как пакет NuGet — это просто ZIP-файл, расширение которого изменено на `.nupkg`, зачастую проще всего создать нужную структуру папок в файловой системе, а затем создать файл `.nuspec` на основе этой структуры.</span><span class="sxs-lookup"><span data-stu-id="54881-186">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, its often easiest to create the folder structure you want on the file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="54881-187">Команда `nuget pack` автоматически добавляет все файлы, имеющиеся в этой структуре папок (кроме папок, начинающихся с `.`, что позволяет иметь закрытые файлы в этой же структуре).</span><span class="sxs-lookup"><span data-stu-id="54881-187">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you keep private files in the same structure).</span></span>

<span data-ttu-id="54881-188">Преимущество такого подхода в том, что вам не нужно указывать в манифесте файлы, которые требуется включить в пакет (как описано далее в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="54881-188">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="54881-189">В процессе сборки можно создать структуру папок, которая будет в точности перенесена в пакет, и легко включить в него другие файлы, которые в противном случае не были бы добавлены в проект:</span><span class="sxs-lookup"><span data-stu-id="54881-189">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="54881-190">содержимое и исходный код, которые следует внедрить в конечный проект;</span><span class="sxs-lookup"><span data-stu-id="54881-190">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="54881-191">скрипты PowerShell (пакеты в NuGet 2.x могут также включать в себя скрипты установки, которые не поддерживаются в NuGet 3.x и более поздних версиях);</span><span class="sxs-lookup"><span data-stu-id="54881-191">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="54881-192">преобразования существующих файлов конфигурации и исходного кода в проекте.</span><span class="sxs-lookup"><span data-stu-id="54881-192">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="54881-193">Ниже представлены соглашения в отношении папок.</span><span class="sxs-lookup"><span data-stu-id="54881-193">The folder conventions are as follows:</span></span>

| <span data-ttu-id="54881-194">Папка</span><span class="sxs-lookup"><span data-stu-id="54881-194">Folder</span></span> | <span data-ttu-id="54881-195">Описание:</span><span class="sxs-lookup"><span data-stu-id="54881-195">Description</span></span> | <span data-ttu-id="54881-196">Действие при установке пакета</span><span class="sxs-lookup"><span data-stu-id="54881-196">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54881-197">(корневая)</span><span class="sxs-lookup"><span data-stu-id="54881-197">(root)</span></span> | <span data-ttu-id="54881-198">Расположение файла readme.txt</span><span class="sxs-lookup"><span data-stu-id="54881-198">Location for readme.txt</span></span> | <span data-ttu-id="54881-199">При установке пакета в Visual Studio отображается файл readme.txt в корневой папке проекта.</span><span class="sxs-lookup"><span data-stu-id="54881-199">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="54881-200">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="54881-200">lib/{tfm}</span></span> | <span data-ttu-id="54881-201">Файлы сборки (`.dll`), документации (`.xml`) и символов (`.pdb`) для данного моникера целевой платформы (TFM)</span><span class="sxs-lookup"><span data-stu-id="54881-201">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="54881-202">Сборки добавляются как ссылки; файлы `.xml` и `.pdb` копируются в папки проекта.</span><span class="sxs-lookup"><span data-stu-id="54881-202">Assemblies are added as references; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="54881-203">Сведения о создании вложенных папок для определенных целевых платформ см. в разделе [Поддержка нескольких целевых платформ](Supporting-Multiple-Target-Frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="54881-203">See [Supporting multiple target frameworks](Supporting-Multiple-Target-Frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="54881-204">runtimes</span><span class="sxs-lookup"><span data-stu-id="54881-204">runtimes</span></span> | <span data-ttu-id="54881-205">Файлы сборки (`.dll`), символов (`.pdb`) и машинных ресурсов (`.pri`) для определенной архитектуры</span><span class="sxs-lookup"><span data-stu-id="54881-205">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="54881-206">Сборки добавляются как ссылки; остальные файлы копируются в папки проекта.</span><span class="sxs-lookup"><span data-stu-id="54881-206">Assemblies are added as references; other files are copied into project folders.</span></span> <span data-ttu-id="54881-207">См. раздел [Поддержка нескольких целевых платформ](Supporting-Multiple-Target-Frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="54881-207">See [Supporting multiple target frameworks](Supporting-Multiple-Target-Frameworks.md).</span></span> |
| <span data-ttu-id="54881-208">содержание</span><span class="sxs-lookup"><span data-stu-id="54881-208">content</span></span> | <span data-ttu-id="54881-209">Произвольные файлы</span><span class="sxs-lookup"><span data-stu-id="54881-209">Arbitrary files</span></span> | <span data-ttu-id="54881-210">Содержимое копируется в корневую папку проекта.</span><span class="sxs-lookup"><span data-stu-id="54881-210">Contents are copied to the project root.</span></span> <span data-ttu-id="54881-211">Папку **content** можно представить как корневую папку целевого приложения, которое будет использовать пакет.</span><span class="sxs-lookup"><span data-stu-id="54881-211">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="54881-212">Чтобы пакет добавил изображение в папку */images* приложения, поместите это изображение в папку *content/images* пакета.</span><span class="sxs-lookup"><span data-stu-id="54881-212">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="54881-213">выполнить сборку</span><span class="sxs-lookup"><span data-stu-id="54881-213">build</span></span> | <span data-ttu-id="54881-214">Файлы MSBuild `.targets` и `.props`</span><span class="sxs-lookup"><span data-stu-id="54881-214">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="54881-215">Автоматически вставляются в файл проекта (NuGet 2.x) или файл `project.lock.json` (NuGet 3.x или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="54881-215">Automatically inserted into the project file (NuGet 2.x) or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="54881-216">средства</span><span class="sxs-lookup"><span data-stu-id="54881-216">tools</span></span> | <span data-ttu-id="54881-217">Скрипты и программы PowerShell, доступные из консоли диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="54881-217">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="54881-218">Папка `tools` добавляется в переменную среды `PATH` только для консоли диспетчера пакетов (в частности, она *не* добавляется в переменную `PATH` для среды MSBuild при сборке проекта).</span><span class="sxs-lookup"><span data-stu-id="54881-218">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="54881-219">Так как в структуре папок может быть сколько угодно сборок для любого числа целевых платформ, этот метод обязателен при создании пакетов, поддерживающих несколько платформ.</span><span class="sxs-lookup"><span data-stu-id="54881-219">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks</span></span> 

<span data-ttu-id="54881-220">После того как вы подготовите нужную структуру папок, выполните в ней следующую команду, чтобы создать файл `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="54881-220">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```
nuget spec
```

<span data-ttu-id="54881-221">Созданный файл `.nuspec` не содержит явных ссылок на файлы в структуре папок.</span><span class="sxs-lookup"><span data-stu-id="54881-221">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="54881-222">NuGet автоматически включает все файлы при создании пакета.</span><span class="sxs-lookup"><span data-stu-id="54881-222">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="54881-223">Однако вам необходимо отредактировать значения-заполнители в других частях манифеста.</span><span class="sxs-lookup"><span data-stu-id="54881-223">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="54881-224">На основе библиотеки DLL сборки</span><span class="sxs-lookup"><span data-stu-id="54881-224">From an assembly DLL</span></span>

<span data-ttu-id="54881-225">В такой простой ситуации, как создание пакета на основе сборки, вы можете создать файл `.nuspec` из содержащихся в сборке метаданных с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="54881-225">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```
nuget spec <assembly-name>.dll
```

<span data-ttu-id="54881-226">При использовании такого формата ряд заполнителей в манифесте заменяется конкретными значениями из сборки.</span><span class="sxs-lookup"><span data-stu-id="54881-226">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="54881-227">Например, свойству `<id>` присваивается имя сборки, а свойству `<version>` — ее версия.</span><span class="sxs-lookup"><span data-stu-id="54881-227">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="54881-228">Однако остальные свойства в манифесте не имеют соответствующих значений в сборке и поэтому по-прежнему содержат заполнители.</span><span class="sxs-lookup"><span data-stu-id="54881-228">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="54881-229">На основе проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="54881-229">From a Visual Studio project</span></span>

<span data-ttu-id="54881-230">Создавать файл `.nuspec` на основе файла `.csproj` или `.vbproj` удобно, так как ссылки на другие пакеты, установленные в проекте, как и на зависимости, создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="54881-230">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="54881-231">Просто выполните следующую команду в папке, в которой находится файл проекта:</span><span class="sxs-lookup"><span data-stu-id="54881-231">Simply use the following command in the same folder as the project file:</span></span>

```
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="54881-232">Получившийся файл `<project-name>.nuspec` содержит *токены*, которые заменяются во время создания пакета значениями их проекта, включая ссылки на другие пакеты, которые уже установлены.</span><span class="sxs-lookup"><span data-stu-id="54881-232">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="54881-233">Токен отделяется символами `$` с обеих сторон свойства проекта.</span><span class="sxs-lookup"><span data-stu-id="54881-233">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="54881-234">Например, значение `<id>` в созданном таким образом манифесте, как правило, имеет следующий вид:</span><span class="sxs-lookup"><span data-stu-id="54881-234">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="54881-235">Этот токен заменяется значением `AssemblyName` из файла проекта во время упаковки.</span><span class="sxs-lookup"><span data-stu-id="54881-235">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="54881-236">Точные сведения о том, как значения из проекта сопоставляются с токенами `.nuspec`, см. в [справочнике по токенам замены](../schema/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="54881-236">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../schema/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="54881-237">Токены избавляют от необходимости изменять критически важные значения, такие как номер версии, в файле `.nuspec` при обновлении пакета.</span><span class="sxs-lookup"><span data-stu-id="54881-237">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="54881-238">(При необходимости токены всегда можно заменить на конкретные значения.)</span><span class="sxs-lookup"><span data-stu-id="54881-238">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="54881-239">Обратите внимание на то, что при работе с проектом Visual Studio доступно несколько дополнительных параметров создания пакета, которые описываются далее в подразделе [Выполнение команды nuget pack для создания файла NUPKG](#running-nuget-pack-to-generate-the-nupkg-file).</span><span class="sxs-lookup"><span data-stu-id="54881-239">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="54881-240">Пакеты на уровне решения</span><span class="sxs-lookup"><span data-stu-id="54881-240">Solution-level packages</span></span>

<span data-ttu-id="54881-241">*Только в NuGet 2.x. Недоступно в NuGet 3.0 и более поздних версиях.*</span><span class="sxs-lookup"><span data-stu-id="54881-241">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="54881-242">В NuGet 2.x поддерживалась концепция пакетов на уровне решения, которые устанавливают средства или дополнительные команды для консоли диспетчера команд (содержимое папки `tools`), но не добавляют ссылки, содержимое или настройки сборки в проекты решения.</span><span class="sxs-lookup"><span data-stu-id="54881-242">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="54881-243">Такие пакеты не содержат файлов непосредственно в папках `lib`, `content` или `build`, а их зависимости не содержат файлов в соответствующих папках `lib`, `content` или `build`.</span><span class="sxs-lookup"><span data-stu-id="54881-243">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span> 

<span data-ttu-id="54881-244">NuGet отслеживает установленные пакеты уровня решения в файле `packages.config` в папке `.nuget`, а не в файле `packages.config` проекта.</span><span class="sxs-lookup"><span data-stu-id="54881-244">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="54881-245">Новый файл со значениями по умолчанию</span><span class="sxs-lookup"><span data-stu-id="54881-245">New file with default values</span></span>

<span data-ttu-id="54881-246">Следующая команда создает манифест по умолчанию с заполнителями, формируя надлежащую структуру файлов:</span><span class="sxs-lookup"><span data-stu-id="54881-246">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```
nuget spec [<package-name>]
```

<span data-ttu-id="54881-247">Если не указать параметр \<package-name\>, получившийся файл будет иметь имя `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="54881-247">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="54881-248">Если указать имя, например `Contoso.Utility.UsefulStuff`, файл будет иметь имя `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="54881-248">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="54881-249">Полученный файл `.nuspec` содержит заполнители для значений, например `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="54881-249">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="54881-250">Прежде чем использовать этот файл для создания итогового файла `.nupkg`, его необходимо отредактировать.</span><span class="sxs-lookup"><span data-stu-id="54881-250">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="54881-251">Выбор уникального идентификатора пакета и задание номера версии</span><span class="sxs-lookup"><span data-stu-id="54881-251">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="54881-252">Идентификатор пакета (элемент `<id>`) и номер версии (элемент `<version>`) — два самых важных значения в манифесте, так как они однозначно определяют код, содержащийся в пакете.</span><span class="sxs-lookup"><span data-stu-id="54881-252">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="54881-253">**Рекомендации в отношении идентификатора пакета**</span><span class="sxs-lookup"><span data-stu-id="54881-253">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="54881-254">**Уникальность**. Идентификатор должен быть уникальным в пределах nuget.org или другой коллекции, в которой размещается пакет.</span><span class="sxs-lookup"><span data-stu-id="54881-254">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="54881-255">Прежде чем задавать идентификатор, проверьте, не используется ли оно уже в соответствующей коллекции.</span><span class="sxs-lookup"><span data-stu-id="54881-255">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="54881-256">Во избежание конфликтов рекомендуется использовать в качестве первой части идентификатора название организации, например `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="54881-256">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="54881-257">**Имена в стиле пространств имен**. Используйте шаблон, по которому строятся имена пространств имен в .NET, используя нотацию с точками, а не с дефисами.</span><span class="sxs-lookup"><span data-stu-id="54881-257">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="54881-258">Например, используйте идентификатор `Contoso.Utility.UsefulStuff` вместо `Contoso-Utility-UsefulStuff` или `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="54881-258">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="54881-259">Пользователям также удобно, когда идентификатор пакета соответствует пространствам имен, используемым в коде.</span><span class="sxs-lookup"><span data-stu-id="54881-259">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="54881-260">**Образцы пакетов**. Если вы создаете пакет с образцом кода, демонстрирующим использование другого пакета, добавьте к идентификатору суффикс `.Sample`, например `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="54881-260">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="54881-261">(Образец пакета, конечно, должен иметь зависимость от другого пакета.) При создании образца пакета используйте описанный выше метод на основе рабочего каталога, соответствующего соглашениям.</span><span class="sxs-lookup"><span data-stu-id="54881-261">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="54881-262">В папке `content` разместите код образца в папке с именем `\Samples\<identifier>`, например `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="54881-262">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="54881-263">**Рекомендации в отношении версии пакета**</span><span class="sxs-lookup"><span data-stu-id="54881-263">**Best practices for the package version:**</span></span>

- <span data-ttu-id="54881-264">Как правило, версия пакета должна соответствовать версии библиотеки, хотя это не строгое требование.</span><span class="sxs-lookup"><span data-stu-id="54881-264">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="54881-265">Это легко реализовать, если пакет ограничен единственной сборкой, как было описано выше в подразделе [Выбор сборок для добавления в пакет](#deciding-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="54881-265">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="54881-266">В целом помните, что при разрешении зависимостей диспетчер NuGet ориентируется на версии пакетов, а не на версии сборок.</span><span class="sxs-lookup"><span data-stu-id="54881-266">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="54881-267">При применении нестандартной схемы версий обязательно учитывайте правила управления версиями в NuGet, которые изложены в разделе [Управление версиями пакета](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="54881-267">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="54881-268">Разобраться в принципах управления версиями также может помочь следующая серия коротких записей блога:</span><span class="sxs-lookup"><span data-stu-id="54881-268">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="54881-269">Часть 1. Решение проблем с DLL</span><span class="sxs-lookup"><span data-stu-id="54881-269">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="54881-270">Часть 2. Базовый алгоритм</span><span class="sxs-lookup"><span data-stu-id="54881-270">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="54881-271">Часть 3. Унификация путем переадресации привязок</span><span class="sxs-lookup"><span data-stu-id="54881-271">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a><span data-ttu-id="54881-272">Указание типа пакета</span><span class="sxs-lookup"><span data-stu-id="54881-272">Setting a package type</span></span>

<span data-ttu-id="54881-273">В NuGet 3.5 и более поздних версиях пакету можно присвоить определенный *тип пакета*, указывающий на его предполагаемое назначение.</span><span class="sxs-lookup"><span data-stu-id="54881-273">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="54881-274">Пакеты, которым не назначен тип, включая все пакеты, созданные в более ранних версиях NuGet, по умолчанию имеют тип `Dependency`.</span><span class="sxs-lookup"><span data-stu-id="54881-274">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="54881-275">Пакеты типа `Dependency` добавляют ресурсы времени сборки или времени выполнения в библиотеки и приложения, и их можно устанавливать в проектах любого типа (при условии, что они совместимы).</span><span class="sxs-lookup"><span data-stu-id="54881-275">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="54881-276">Пакеты типа `DotnetCliTool` являются расширениями [интерфейса командной строки .NET](/dotnet/articles/core/tools/index) и вызываются из командной строки.</span><span class="sxs-lookup"><span data-stu-id="54881-276">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="54881-277">Такие пакеты можно устанавливать только в проектах .NET Core, и они не влияют на операции восстановления.</span><span class="sxs-lookup"><span data-stu-id="54881-277">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="54881-278">Дополнительные сведения об этих расширениях проекта можно найти в документации по [расширяемости .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).</span><span class="sxs-lookup"><span data-stu-id="54881-278">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

    <span data-ttu-id="54881-279">При установке пакета DotnetCliTool среда Visual Studio помещает его в узел `tools` файла `project.json`, а не в узел `dependencies`.</span><span class="sxs-lookup"><span data-stu-id="54881-279">When a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

- <span data-ttu-id="54881-280">Для пакетов пользовательского типа применяются произвольные идентификаторы, в которых соблюдаются те же правила формата, что и в идентификаторах пакетов.</span><span class="sxs-lookup"><span data-stu-id="54881-280">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="54881-281">Типы, отличные от `Dependency` и `DotnetCliTool`, однако, не распознаются диспетчером пакетов NuGet в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54881-281">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="54881-282">Типы пакетов задаются в файле `.nuspec` или в файле `project.json`.</span><span class="sxs-lookup"><span data-stu-id="54881-282">Package types are set either in the `.nuspec` file or in `project.json`.</span></span> <span data-ttu-id="54881-283">В обоих случаях в целях обратной совместимости лучше *не* задавать тип `Dependency` явным образом, позволив диспетчеру NuGet определить его автоматически, что происходит, если тип не указан.</span><span class="sxs-lookup"><span data-stu-id="54881-283">In both cases, it's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="54881-284">`.nuspec`: укажите тип пакета в узле `packageTypes\packageType` элемента `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="54881-284">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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

- <span data-ttu-id="54881-285">`project.json`: укажите тип пакета в свойстве `packOptions.packageType` файла JSON:</span><span class="sxs-lookup"><span data-stu-id="54881-285">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="54881-286">Добавление файла сведений и других файлов</span><span class="sxs-lookup"><span data-stu-id="54881-286">Adding a readme and other files</span></span>

<span data-ttu-id="54881-287">Чтобы явным образом указать файлы, которые следует включить в пакет, используйте узел `<files>` в файле `.nuspec`, который находится *после* тега `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="54881-287">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

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
> <span data-ttu-id="54881-288">При использовании подхода на основе рабочего каталога, соответствующего соглашениям, файл readme.txt можно поместить в корневую папку пакета, а другое содержимое — в папку `content`.</span><span class="sxs-lookup"><span data-stu-id="54881-288">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="54881-289">Элементы `<file>` в манифесте не требуются.</span><span class="sxs-lookup"><span data-stu-id="54881-289">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="54881-290">Если в корневую папку пакета добавлен файл с именем `readme.txt`, Visual Studio отображает содержимое этого файла в виде обычного текста сразу после установки пакета напрямую.</span><span class="sxs-lookup"><span data-stu-id="54881-290">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="54881-291">(Файлы сведений не отображаются для пакетов, устанавливаемых как зависимости.)</span><span class="sxs-lookup"><span data-stu-id="54881-291">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="54881-292">Например, вот как выглядит файл сведений для пакета HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="54881-292">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Отображение файла сведений для пакета NuGet при установке](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="54881-294">Если узел `<files>` в файле `.nuspec` пуст, NuGet включает в пакет только содержимое из папки `lib`.</span><span class="sxs-lookup"><span data-stu-id="54881-294">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="54881-295">Включение в пакет свойств и целевых объектов MSBuild</span><span class="sxs-lookup"><span data-stu-id="54881-295">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="54881-296">В некоторых случаях в проекты, использующие пакет, необходимо добавить пользовательские целевые объекты сборки или свойства, например, если во время сборки должно запускаться пользовательское средство или процесс.</span><span class="sxs-lookup"><span data-stu-id="54881-296">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="54881-297">Для этого нужно поместить файлы в формате `<package_id>.targets` или `<package_id>.props` (например, `Contoso.Utility.UsefulStuff.targets`) в папку `\build` проекта.</span><span class="sxs-lookup"><span data-stu-id="54881-297">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="54881-298">Файлы в корневой папке `\build` считаются пригодными для всех целевых платформ.</span><span class="sxs-lookup"><span data-stu-id="54881-298">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="54881-299">Чтобы предоставить файлы для определенных платформ, сначала поместите их в соответствующие вложенные папки, например следующие:</span><span class="sxs-lookup"><span data-stu-id="54881-299">To provide framework-specific files, first place those within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="54881-300">Затем в файле `.nuspec` укажите ссылки на эти файлы в узле `<files>`:</span><span class="sxs-lookup"><span data-stu-id="54881-300">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
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

<span data-ttu-id="54881-301">Когда диспетчер NuGet 2.x устанавливает пакет с файлами `\build`, он добавляет в файл проекта элементы MSBuild `<Import>`, указывающие на файлы `.targets` и `.props`.</span><span class="sxs-lookup"><span data-stu-id="54881-301">When NuGet 2.x installs a package with `\build` files, it adds an MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="54881-302">(Файлы `.props` добавляются в начале файла проекта, а файлы `.targets` — в конце.)</span><span class="sxs-lookup"><span data-stu-id="54881-302">(`.props` is added at the top of the project file; `.targets` is added at the bottom.)</span></span>

<span data-ttu-id="54881-303">В NuGet 3.x целевые платформы не добавляются в проект, а предоставляются через файл `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="54881-303">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="54881-304">Разработка пакетов, содержащих сборки COM-взаимодействия</span><span class="sxs-lookup"><span data-stu-id="54881-304">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="54881-305">Пакеты, содержащие сборки COM-взаимодействия, должны включать в себя соответствующий [файл целей](#including-msbuild-props-and-targets-in-a-package), чтобы в проекты были добавлены правильные метаданные `EmbedInteropTypes` в формате PackageReference.</span><span class="sxs-lookup"><span data-stu-id="54881-305">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="54881-306">По умолчанию метаданные `EmbedInteropTypes` всегда имеют значение false для всех сборок при использовании PackageReference, поэтому файл целей добавляет эти метаданные явным образом.</span><span class="sxs-lookup"><span data-stu-id="54881-306">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="54881-307">Во избежание конфликтов имя цели должно быть уникальным. В идеале следует использовать сочетание имен пакета и внедряемой сборки, заменив им элемент `{InteropAssemblyName}` в приведенном ниже примере.</span><span class="sxs-lookup"><span data-stu-id="54881-307">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="54881-308">(Пример см. также на странице [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop).)</span><span class="sxs-lookup"><span data-stu-id="54881-308">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml      
<Target Name="EmbeddingAssemblyNameFromPackageId" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <PropertyGroup>
    <_InteropAssemblyFileName>{InteropAssemblyName}</_InteropAssemblyFileName>
  </PropertyGroup>
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '$(_InteropAssemblyFileName)' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="54881-309">Имейте в виду, что при использовании формата ссылки `packages.config` добавление ссылок на сборки из пакетов приводит к тому, что NuGet и Visual Studio проверяют наличие сборок COM-взаимодействия и присваивают свойству `EmbedInteropTypes` в файле проекта значение true.</span><span class="sxs-lookup"><span data-stu-id="54881-309">Note that when using the `packages.config` reference format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="54881-310">В этом случае цели переопределяются.</span><span class="sxs-lookup"><span data-stu-id="54881-310">In this case the targets are overriden.</span></span>

<span data-ttu-id="54881-311">Кроме того, по умолчанию [ресурсы сборки не передаются транзитивно](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="54881-311">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="54881-312">Пакеты, созданные описанным здесь способом, работают иначе, если они извлекаются в качестве транзитивной зависимости из проекта в ссылку на проект.</span><span class="sxs-lookup"><span data-stu-id="54881-312">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="54881-313">Пользователь пакета может разрешить их передачу, изменив значение PrivateAssets по умолчанию так, чтобы сборка не включалась.</span><span class="sxs-lookup"><span data-stu-id="54881-313">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>  

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="54881-314">Выполнение команды nuget pack для создания файла NUPKG</span><span class="sxs-lookup"><span data-stu-id="54881-314">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="54881-315">Чтобы создать пакет на основе сборки или рабочего каталога, соответствующего соглашениям, выполните команду `nuget pack`, указав файл `.nuspec`, где `<manifest-name>` необходимо заменить на имя файла:</span><span class="sxs-lookup"><span data-stu-id="54881-315">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<manifest-name>` with your specific filename:</span></span>

```
nuget pack <project-name>.nuspec
```

<span data-ttu-id="54881-316">При использовании проекта Visual Studio выполните команду `nuget pack`, указав файл проекта. В результате автоматически загрузится файл `.nuspec` проекта, и все токены в нем будут заменены значениями из файла проекта.</span><span class="sxs-lookup"><span data-stu-id="54881-316">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="54881-317">Использование файла проекта напрямую является необходимым для замены токенов, так как проект является источником значений токенов.</span><span class="sxs-lookup"><span data-stu-id="54881-317">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="54881-318">Замена токенов не производится при использовании команды `nuget pack` с файлом `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="54881-318">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="54881-319">В любом случае команда `nuget pack` исключает папки, начинающиеся с точки, например `.git` или `.hg`.</span><span class="sxs-lookup"><span data-stu-id="54881-319">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="54881-320">NuGet указывает, есть ли в файле `.nuspec` ошибки, требующие исправления, например, если вы забыли изменить значения-заполнители в манифесте.</span><span class="sxs-lookup"><span data-stu-id="54881-320">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="54881-321">После успешного выполнения команды `nuget pack` вы получаете файл `.nupkg`, который можно опубликовать в подходящей коллекции, как описано в разделе [Публикация пакета](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="54881-321">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="54881-322">После создания пакета его полезно просмотреть, открыв в средстве [Обозреватель пакетов](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer).</span><span class="sxs-lookup"><span data-stu-id="54881-322">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="54881-323">В нем в графической форме представлено содержимое пакета и его манифест.</span><span class="sxs-lookup"><span data-stu-id="54881-323">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="54881-324">Вы также можете переименовать полученный файл `.nupkg` в файл `.zip` и просмотреть его содержимое напрямую.</span><span class="sxs-lookup"><span data-stu-id="54881-324">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="54881-325">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="54881-325">Additional options</span></span>

<span data-ttu-id="54881-326">С командой `nuget pack` можно использовать различные параметры командной строки для исключения файлов, переопределения номера версии в манифесте, изменения папки выходных данных и совершения других действий.</span><span class="sxs-lookup"><span data-stu-id="54881-326">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="54881-327">Полный список параметров см. в [справочнике по команде pack](../tools/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="54881-327">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="54881-328">Ниже приводятся некоторые часто используемые с проектами Visual Studio параметры.</span><span class="sxs-lookup"><span data-stu-id="54881-328">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="54881-329">**Проекты, на которые указывают ссылки**. Если проект ссылается на другие проекты, вы можете включить их в пакет или добавить в качестве зависимостей с помощью параметра `-IncludeReferencedProjects`:</span><span class="sxs-lookup"><span data-stu-id="54881-329">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="54881-330">Включение является рекурсивным, поэтому если `MyProject.csproj` ссылается на проекты B и C, а они ссылаются на проекты D, E и F, в пакет включаются файлы из проектов B, C, D, E и F.</span><span class="sxs-lookup"><span data-stu-id="54881-330">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="54881-331">Если в проекте, на который указывает ссылка, есть собственный файл `.nuspec`, NuGet вместо этого добавляет проект как зависимость.</span><span class="sxs-lookup"><span data-stu-id="54881-331">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="54881-332">Такой проект необходимо упаковать и опубликовать отдельно.</span><span class="sxs-lookup"><span data-stu-id="54881-332">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="54881-333">**Конфигурация сборки**. По умолчанию NuGet использует стандартную конфигурацию сборки, указанную в файле проекта. Обычно это конфигурация *Debug*.</span><span class="sxs-lookup"><span data-stu-id="54881-333">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="54881-334">Чтобы упаковать файлы из другой конфигурации сборки, например *Release*, используйте параметр `-properties`, указав конфигурацию:</span><span class="sxs-lookup"><span data-stu-id="54881-334">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="54881-335">**Символы**. Чтобы включить символы, позволяющие пользователям осуществлять пошаговое выполнение кода в пакете, используйте параметр `-Symbols`:</span><span class="sxs-lookup"><span data-stu-id="54881-335">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="54881-336">Тестирование установки пакета</span><span class="sxs-lookup"><span data-stu-id="54881-336">Testing package installation</span></span>

<span data-ttu-id="54881-337">Перед публикацией пакета, как правило, необходимо протестировать процесс его установки в проекте.</span><span class="sxs-lookup"><span data-stu-id="54881-337">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="54881-338">Это позволяет убедиться в том, что все необходимые файлы помещаются в нужные места.</span><span class="sxs-lookup"><span data-stu-id="54881-338">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="54881-339">Установку можно протестировать вручную в Visual Studio или в командной строке, выполнив стандартную [процедуру установки пакета](../Quickstart/Use-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="54881-339">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../Quickstart/Use-a-Package.md).</span></span>

<span data-ttu-id="54881-340">Для автоматического тестирования выполните указанные ниже основные действия.</span><span class="sxs-lookup"><span data-stu-id="54881-340">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="54881-341">Скопируйте файл `.nupkg` в локальную папку.</span><span class="sxs-lookup"><span data-stu-id="54881-341">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="54881-342">Добавьте эту папку в источники пакета с помощью команды `nuget sources -name <name> -source <path>` (см. описание [команды nuget sources](../tools/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="54881-342">Add the folder to your package sources using the `nuget sources -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="54881-343">Обратите внимание на то, что на каждом компьютере этот локальный источник необходимо задать только один раз.</span><span class="sxs-lookup"><span data-stu-id="54881-343">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="54881-344">Установите пакет из источника с помощью команды `nuget install <packageID> -source <name>`, где `<name>` соответствует имени источника, предоставленному команде `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="54881-344">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="54881-345">Указание источника позволяет гарантировать, что пакет будет устанавливаться только из него.</span><span class="sxs-lookup"><span data-stu-id="54881-345">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="54881-346">В файловой системе проверьте, правильно ли установились файлы.</span><span class="sxs-lookup"><span data-stu-id="54881-346">Examine the file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54881-347">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="54881-347">Next Steps</span></span>

<span data-ttu-id="54881-348">Создав пакет, то есть файл `.nupkg`, вы можете опубликовать его в любой коллекции на ваш выбор, как описано в разделе [Публикация пакета](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="54881-348">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="54881-349">Вы также можете расширить возможности пакета или обеспечить поддержку других сценариев, как описано в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="54881-349">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="54881-350">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="54881-350">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="54881-351">Поддержка нескольких целевых платформ</span><span class="sxs-lookup"><span data-stu-id="54881-351">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="54881-352">Преобразования исходных файлов и файлов конфигурации</span><span class="sxs-lookup"><span data-stu-id="54881-352">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="54881-353">Локализация</span><span class="sxs-lookup"><span data-stu-id="54881-353">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="54881-354">Предварительные версии</span><span class="sxs-lookup"><span data-stu-id="54881-354">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="54881-355">Наконец, существуют дополнительные типы пакетов, о которых нужно знать:</span><span class="sxs-lookup"><span data-stu-id="54881-355">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="54881-356">Собственные пакеты</span><span class="sxs-lookup"><span data-stu-id="54881-356">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="54881-357">Пакеты символов</span><span class="sxs-lookup"><span data-stu-id="54881-357">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
