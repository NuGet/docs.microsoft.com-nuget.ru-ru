---
title: Создание пакета NuGet с помощью CLI nuget.exe
description: Подробное руководство по проектированию и созданию пакета NuGet, включая принятие решений по ключевым аспектам, таким как файлы и управление версиями.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: a9224ce4e515cf98893a7134077c90a47df1862a
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020075"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a><span data-ttu-id="f9053-103">Создание пакета с помощью CLI nuget.exe</span><span class="sxs-lookup"><span data-stu-id="f9053-103">Create a package using the nuget.exe CLI</span></span>

<span data-ttu-id="f9053-104">Независимо от назначения вашего пакета или содержащегося в нем кода, с помощью одного из средств CLI (`nuget.exe` или `dotnet.exe`) вы можете создать компонент, которым можно поделиться с любым количеством разработчиков для совместного использования.</span><span class="sxs-lookup"><span data-stu-id="f9053-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="f9053-105">Инструкции по установке средств CLI для NuGet см. в статье [Установка клиентских средств NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="f9053-105">To install NuGet CLI tools, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="f9053-106">Обратите внимание на то, что средство CLI не входит в состав Visual Studio по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f9053-106">Note that Visual Studio does not automatically include a CLI tool.</span></span>

- <span data-ttu-id="f9053-107">Чтобы создать пакет для проектов в другом стиле (например, для проектов .NET Framework) выполните шаги, описанные в этой статье.</span><span class="sxs-lookup"><span data-stu-id="f9053-107">For non-SDK-style projects, typically .NET Framework projects, follow the steps described in this article to create a package.</span></span> <span data-ttu-id="f9053-108">Пошаговые инструкции по использованию Visual Studio и CLI `nuget.exe` см. в руководстве по [созданию и публикации пакета .NET Framework](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="f9053-108">For step-by-step instructions using Visual Studio and the `nuget.exe` CLI, see [Create and publish a .NET Framework package](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span></span>

- <span data-ttu-id="f9053-109">См. подробнее о проектах .NET Core и .NET Standard [не на основе пакетов SDK](../resources/check-project-format.md) и других проектах на основе пакетов SDK в руководстве по [созданию пакета NuGet с помощью CLI dotnet](creating-a-package-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f9053-109">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, see [Create a NuGet package using the dotnet CLI](creating-a-package-dotnet-cli.md).</span></span>

- <span data-ttu-id="f9053-110">Для проектов, перенесенных из `packages.config` в [PackageReference](../consume-packages/package-references-in-project-files.md), используйте [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="f9053-110">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), use [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

<span data-ttu-id="f9053-111">С технической точки зрения, пакет NuGet — это просто ZIP-файл, расширение которого изменено на `.nupkg` и содержимое которого соответствует определенным соглашениям.</span><span class="sxs-lookup"><span data-stu-id="f9053-111">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="f9053-112">В этом разделе подробно описывается создание пакета, в котором соблюдаются эти соглашения.</span><span class="sxs-lookup"><span data-stu-id="f9053-112">This topic describes the detailed process of creating a package that meets those conventions.</span></span>

<span data-ttu-id="f9053-113">Создание пакета начинается с подготовки скомпилированного кода (сборок), символов и других файлов, которые должны быть включены в пакет (см. раздел [Процесс создания пакета](overview-and-workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="f9053-113">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="f9053-114">Этот процесс не зависит от компиляции и других задач по созданию файлов для пакета, хотя вы можете использовать информацию из файла проекта для синхронизации скомпилированных сборок и пакетов.</span><span class="sxs-lookup"><span data-stu-id="f9053-114">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Important]
> <span data-ttu-id="f9053-115">Эта статья применяется к проектам со стилем, отличным от пакетов SDK, то есть не таких как проекты .NET Core и .NET Standard, для которых используются Visual Studio 2017 и NuGet 4.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="f9053-115">This topic applies to non-SDK-style projects, typically projects other than .NET Core and .NET Standard projects using Visual Studio 2017 and higher versions and NuGet 4.0+.</span></span>

## <a name="decide-which-assemblies-to-package"></a><span data-ttu-id="f9053-116">Выбор сборок для добавления в пакет</span><span class="sxs-lookup"><span data-stu-id="f9053-116">Decide which assemblies to package</span></span>

<span data-ttu-id="f9053-117">Большинство пакетов общего назначения содержат одну или несколько сборок, которые другие разработчики могут использовать в собственных проектах.</span><span class="sxs-lookup"><span data-stu-id="f9053-117">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="f9053-118">Как правило, для каждой сборки лучше создавать собственный пакет NuGet, если эти сборки используются независимо.</span><span class="sxs-lookup"><span data-stu-id="f9053-118">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="f9053-119">Например, если есть сборка `Utilities.dll`, которая зависит от сборки `Parser.dll`, но сборка `Parser.dll` также полезна сама по себе, создайте для каждой из этих сборок отдельный пакет.</span><span class="sxs-lookup"><span data-stu-id="f9053-119">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="f9053-120">Это позволит разработчикам использовать `Parser.dll` независимо от `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="f9053-120">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="f9053-121">Если библиотека состоит из нескольких сборок, которые не используются сами по себе, то их предпочтительнее объединить в одном пакете.</span><span class="sxs-lookup"><span data-stu-id="f9053-121">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="f9053-122">В продолжение предыдущего примера, если сборка `Parser.dll` содержит код, который используется только сборкой `Utilities.dll`, то сборку `Parser.dll` лучше включить в тот же пакет.</span><span class="sxs-lookup"><span data-stu-id="f9053-122">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="f9053-123">Аналогичным образом, если сборка `Utilities.dll` зависит от сборки `Utilities.resources.dll`, которая не используется сама по себе, включите их в один пакет.</span><span class="sxs-lookup"><span data-stu-id="f9053-123">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="f9053-124">Ресурсы представляют собой особый случай.</span><span class="sxs-lookup"><span data-stu-id="f9053-124">Resources are, in fact, a special case.</span></span> <span data-ttu-id="f9053-125">Когда пакет устанавливается в проекте, NuGet автоматически добавляет ссылки на библиотеки DLL сборок в пакете, *кроме* тех из них, в именах которых есть `.resources.dll`, так как они считаются локализованными вспомогательными сборками (см. раздел [Создание локализованных пакетов](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="f9053-125">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="f9053-126">По этой причине следует избегать использования `.resources.dll` в именах файлов пакета, которые содержат важный код.</span><span class="sxs-lookup"><span data-stu-id="f9053-126">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="f9053-127">Если библиотека содержит сборки COM-взаимодействия, следуйте дополнительным указаниям в разделе [Создание пакетов, содержащих сборки COM-взаимодействия](author-packages-with-com-interop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="f9053-127">If your library contains COM interop assemblies, follow additional the guidelines in [Create packages with COM interop assemblies](author-packages-with-com-interop-assemblies.md).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="f9053-128">Назначение и структура файла NUSPEC</span><span class="sxs-lookup"><span data-stu-id="f9053-128">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="f9053-129">После того как вы решите, какие файлы нужно включить в пакет, следует создать манифест пакета в XML-файле `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="f9053-129">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="f9053-130">Манифест служит следующим целям:</span><span class="sxs-lookup"><span data-stu-id="f9053-130">The manifest:</span></span>

1. <span data-ttu-id="f9053-131">Описывает содержимое пакета и сам включается в него.</span><span class="sxs-lookup"><span data-stu-id="f9053-131">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="f9053-132">Управляет созданием пакета и предоставляет диспетчеру NuGet указания по установке пакета в проекте.</span><span class="sxs-lookup"><span data-stu-id="f9053-132">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="f9053-133">Например, в манифесте определяются другие зависимости пакета, чтобы диспетчер NuGet мог также установить их при установке основного пакета.</span><span class="sxs-lookup"><span data-stu-id="f9053-133">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="f9053-134">Содержит обязательные и необязательные свойства, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="f9053-134">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="f9053-135">Полные сведения, включая описание свойств, которые не упомянуты в этом разделе, см. в [справочнике по файлам NUSPEC](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="f9053-135">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="f9053-136">Обязательные свойства:</span><span class="sxs-lookup"><span data-stu-id="f9053-136">Required properties:</span></span>

- <span data-ttu-id="f9053-137">идентификатор пакета, который должен быть уникальным в пределах коллекции, содержащей пакет;</span><span class="sxs-lookup"><span data-stu-id="f9053-137">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="f9053-138">определенный номер версии в формате *основной_номер.дополнительный_номер.исправление[-суффикс]* , где *-суффикс* указывает на [предварительные версии](prerelease-packages.md);</span><span class="sxs-lookup"><span data-stu-id="f9053-138">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="f9053-139">название пакета, которое должно отображаться на сайте размещения (например, nuget.org);</span><span class="sxs-lookup"><span data-stu-id="f9053-139">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="f9053-140">сведения об авторе и владельце;</span><span class="sxs-lookup"><span data-stu-id="f9053-140">Author and owner information.</span></span>
- <span data-ttu-id="f9053-141">подробное описание пакета.</span><span class="sxs-lookup"><span data-stu-id="f9053-141">A long description of the package.</span></span>

<span data-ttu-id="f9053-142">Часто используемые необязательные свойства:</span><span class="sxs-lookup"><span data-stu-id="f9053-142">Common optional properties:</span></span>

- <span data-ttu-id="f9053-143">заметки о выпуске;</span><span class="sxs-lookup"><span data-stu-id="f9053-143">Release notes</span></span>
- <span data-ttu-id="f9053-144">сведения об авторских правах;</span><span class="sxs-lookup"><span data-stu-id="f9053-144">Copyright information</span></span>
- <span data-ttu-id="f9053-145">краткое описание для [пользовательского интерфейса диспетчера пакетов в Visual Studio](../consume-packages/install-use-packages-visual-studio.md);</span><span class="sxs-lookup"><span data-stu-id="f9053-145">A short description for the [Package Manager UI in Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span></span>
- <span data-ttu-id="f9053-146">код языка;</span><span class="sxs-lookup"><span data-stu-id="f9053-146">A locale ID</span></span>
- <span data-ttu-id="f9053-147">URL проекта</span><span class="sxs-lookup"><span data-stu-id="f9053-147">Project URL</span></span>
- <span data-ttu-id="f9053-148">лицензия в виде выражения или файла (`licenseUrl` скоро станет нерекомендуемым, используйте [nuspec-элемент метаданных `license`](../reference/nuspec.md#license));</span><span class="sxs-lookup"><span data-stu-id="f9053-148">License as an expression or file (`licenseUrl` is being deprecated, use the [`license` nuspec metadata element](../reference/nuspec.md#license))</span></span>
- <span data-ttu-id="f9053-149">URL-адрес значка;</span><span class="sxs-lookup"><span data-stu-id="f9053-149">An icon URL</span></span>
- <span data-ttu-id="f9053-150">список зависимостей и ссылок;</span><span class="sxs-lookup"><span data-stu-id="f9053-150">Lists of dependencies and references</span></span>
- <span data-ttu-id="f9053-151">теги, упрощающие поиск в коллекции.</span><span class="sxs-lookup"><span data-stu-id="f9053-151">Tags that assist in gallery searches</span></span>

<span data-ttu-id="f9053-152">Ниже приведен типичный (но вымышленный) файл `.nuspec` с комментариями, описывающими свойства.</span><span class="sxs-lookup"><span data-stu-id="f9053-152">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

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

<span data-ttu-id="f9053-153">Подробные сведения об объявлении зависимостей и указании номеров версий см. в разделе [packages.config](../reference/packages-config.md) и [Управление версиями пакета](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="f9053-153">For details on declaring dependencies and specifying version numbers, see [packages.config](../reference/packages-config.md) and [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="f9053-154">Доступ к ресурсам зависимостей в пакете можно также предоставлять напрямую с помощью атрибутов `include` и `exclude` элемента `dependency`.</span><span class="sxs-lookup"><span data-stu-id="f9053-154">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="f9053-155">См. подраздел "Зависимости" в разделе [Справочник по файлам NUSPEC](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="f9053-155">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="f9053-156">Так как манифест включается в пакет, создаваемый на его основе, вы можете получить дополнительные примеры, изучив существующие пакеты.</span><span class="sxs-lookup"><span data-stu-id="f9053-156">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="f9053-157">Хорошим их источником может служить папка *global-packages* на компьютере, расположение которой можно получить с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="f9053-157">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="f9053-158">Перейдите в любую папку *пакет\версия*, скопируйте файл `.nupkg` в файл `.zip`, затем откройте этот файл `.zip` и изучите содержимое файла `.nuspec` в нем.</span><span class="sxs-lookup"><span data-stu-id="f9053-158">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="f9053-159">При создании файла `.nuspec` из проекта Visual Studio манифест содержит токены, которые заменяются сведениями из проекта при сборке пакета.</span><span class="sxs-lookup"><span data-stu-id="f9053-159">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="f9053-160">См. раздел [Создание файла NUSPEC на основе проекта Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="f9053-160">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="create-the-nuspec-file"></a><span data-ttu-id="f9053-161">Создание NUSPEC-файла</span><span class="sxs-lookup"><span data-stu-id="f9053-161">Create the .nuspec file</span></span>

<span data-ttu-id="f9053-162">Создание полного манифеста, как правило, начинается с базового файла `.nuspec`, который создается одним из следующих способов на основе:</span><span class="sxs-lookup"><span data-stu-id="f9053-162">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- <span data-ttu-id="f9053-163">[рабочего каталога, соответствующего соглашениям](#from-a-convention-based-working-directory);</span><span class="sxs-lookup"><span data-stu-id="f9053-163">[A convention-based working directory](#from-a-convention-based-working-directory)</span></span>
- <span data-ttu-id="f9053-164">[библиотеки DLL сборки](#from-an-assembly-dll);</span><span class="sxs-lookup"><span data-stu-id="f9053-164">[An assembly DLL](#from-an-assembly-dll)</span></span>
- <span data-ttu-id="f9053-165">[проекта Visual Studio](#from-a-visual-studio-project);</span><span class="sxs-lookup"><span data-stu-id="f9053-165">[A Visual Studio project](#from-a-visual-studio-project)</span></span>    
- <span data-ttu-id="f9053-166">[нового файла со значениями по умолчанию](#new-file-with-default-values).</span><span class="sxs-lookup"><span data-stu-id="f9053-166">[New file with default values](#new-file-with-default-values)</span></span>

<span data-ttu-id="f9053-167">Затем нужно отредактировать файл вручную так, чтобы он описывал содержимое итогового пакета.</span><span class="sxs-lookup"><span data-stu-id="f9053-167">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="f9053-168">Автоматически формируемые файлы `.nuspec` содержат заполнители, которые нужно изменить перед созданием пакета с помощью команды `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="f9053-168">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="f9053-169">Если файл `.nuspec` содержит заполнители, эта команда завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="f9053-169">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="f9053-170">На основе рабочего каталога, соответствующего соглашениям</span><span class="sxs-lookup"><span data-stu-id="f9053-170">From a convention-based working directory</span></span>

<span data-ttu-id="f9053-171">Так как пакет NuGet — это просто ZIP-файл, расширение которого изменено на `.nupkg`, зачастую проще всего создать нужную структуру папок в локальной файловой системе, а затем создать файл `.nuspec` на основе этой структуры.</span><span class="sxs-lookup"><span data-stu-id="f9053-171">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="f9053-172">Команда `nuget pack` автоматически добавляет все файлы, имеющиеся в этой структуре папок (кроме папок, начинающихся с `.`, что позволяет иметь закрытые файлы в этой же структуре).</span><span class="sxs-lookup"><span data-stu-id="f9053-172">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="f9053-173">Преимущество такого подхода в том, что вам не нужно указывать в манифесте файлы, которые требуется включить в пакет (как описано далее в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="f9053-173">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="f9053-174">В процессе сборки можно создать структуру папок, которая будет в точности перенесена в пакет, и легко включить в него другие файлы, которые в противном случае не были бы добавлены в проект:</span><span class="sxs-lookup"><span data-stu-id="f9053-174">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="f9053-175">содержимое и исходный код, которые следует внедрить в конечный проект;</span><span class="sxs-lookup"><span data-stu-id="f9053-175">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="f9053-176">Сценарии PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9053-176">PowerShell scripts</span></span>
- <span data-ttu-id="f9053-177">преобразования существующих файлов конфигурации и исходного кода в проекте.</span><span class="sxs-lookup"><span data-stu-id="f9053-177">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="f9053-178">Ниже представлены соглашения в отношении папок.</span><span class="sxs-lookup"><span data-stu-id="f9053-178">The folder conventions are as follows:</span></span>

| <span data-ttu-id="f9053-179">Папка</span><span class="sxs-lookup"><span data-stu-id="f9053-179">Folder</span></span> | <span data-ttu-id="f9053-180">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="f9053-180">Description</span></span> | <span data-ttu-id="f9053-181">Действие при установке пакета</span><span class="sxs-lookup"><span data-stu-id="f9053-181">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f9053-182">(корневая)</span><span class="sxs-lookup"><span data-stu-id="f9053-182">(root)</span></span> | <span data-ttu-id="f9053-183">Расположение файла readme.txt</span><span class="sxs-lookup"><span data-stu-id="f9053-183">Location for readme.txt</span></span> | <span data-ttu-id="f9053-184">При установке пакета в Visual Studio отображается файл readme.txt в корневой папке проекта.</span><span class="sxs-lookup"><span data-stu-id="f9053-184">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="f9053-185">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="f9053-185">lib/{tfm}</span></span> | <span data-ttu-id="f9053-186">Файлы сборки (`.dll`), документации (`.xml`) и символов (`.pdb`) для данного моникера целевой платформы (TFM)</span><span class="sxs-lookup"><span data-stu-id="f9053-186">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="f9053-187">Сборки добавляются как ссылки для использования во время компиляции или выполнения. Файлы `.xml` и `.pdb` копируются в папки проекта.</span><span class="sxs-lookup"><span data-stu-id="f9053-187">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="f9053-188">Сведения о создании вложенных папок для определенных целевых платформ см. в разделе [Поддержка нескольких целевых платформ](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="f9053-188">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="f9053-189">ref/{tfm}</span><span class="sxs-lookup"><span data-stu-id="f9053-189">ref/{tfm}</span></span> | <span data-ttu-id="f9053-190">Файлы сборки (`.dll`) и символов (`.pdb`) для определенного моникера целевой платформы (TFM)</span><span class="sxs-lookup"><span data-stu-id="f9053-190">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="f9053-191">Сборки добавляются как ссылки для использования только во время компиляции. Поэтому в папку bin проекта ничего не копируется.</span><span class="sxs-lookup"><span data-stu-id="f9053-191">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="f9053-192">runtimes</span><span class="sxs-lookup"><span data-stu-id="f9053-192">runtimes</span></span> | <span data-ttu-id="f9053-193">Файлы сборки (`.dll`), символов (`.pdb`) и машинных ресурсов (`.pri`) для определенной архитектуры</span><span class="sxs-lookup"><span data-stu-id="f9053-193">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="f9053-194">Сборки добавляются как ссылки для использования только во время выполнения. Остальные файлы копируются в папки проекта.</span><span class="sxs-lookup"><span data-stu-id="f9053-194">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="f9053-195">В папке `/ref/{tfm}` всегда должна быть соответствующая сборка (TFM) для `AnyCPU`, чтобы предоставить соответствующие сборки, используемые во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="f9053-195">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="f9053-196">См. раздел [Поддержка нескольких целевых платформ](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="f9053-196">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="f9053-197">содержание</span><span class="sxs-lookup"><span data-stu-id="f9053-197">content</span></span> | <span data-ttu-id="f9053-198">Произвольные файлы</span><span class="sxs-lookup"><span data-stu-id="f9053-198">Arbitrary files</span></span> | <span data-ttu-id="f9053-199">Содержимое копируется в корневую папку проекта.</span><span class="sxs-lookup"><span data-stu-id="f9053-199">Contents are copied to the project root.</span></span> <span data-ttu-id="f9053-200">Папку **content** можно представить как корневую папку целевого приложения, которое будет использовать пакет.</span><span class="sxs-lookup"><span data-stu-id="f9053-200">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="f9053-201">Чтобы пакет добавил изображение в папку */images* приложения, поместите это изображение в папку *content/images* пакета.</span><span class="sxs-lookup"><span data-stu-id="f9053-201">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="f9053-202">выполнить сборку</span><span class="sxs-lookup"><span data-stu-id="f9053-202">build</span></span> | <span data-ttu-id="f9053-203">Файлы MSBuild `.targets` и `.props`</span><span class="sxs-lookup"><span data-stu-id="f9053-203">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="f9053-204">Автоматическое добавление в проект (NuGet 3.x+).</span><span class="sxs-lookup"><span data-stu-id="f9053-204">Automatically inserted into the project (NuGet 3.x+).</span></span> |
| <span data-ttu-id="f9053-205">buildMultiTargeting</span><span class="sxs-lookup"><span data-stu-id="f9053-205">buildMultiTargeting</span></span> | <span data-ttu-id="f9053-206">Файлы MSBuild `.targets` и `.props` для кроссплатформенного определения.</span><span class="sxs-lookup"><span data-stu-id="f9053-206">MSBuild `.targets` and `.props` files for cross-framework targeting</span></span> | <span data-ttu-id="f9053-207">Автоматическое добавление в проект.</span><span class="sxs-lookup"><span data-stu-id="f9053-207">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="f9053-208">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="f9053-208">buildTransitive</span></span> | <span data-ttu-id="f9053-209">Файлы MSBuild `.targets` и `.props` *(5.0+)* , которые можно транзитивно передавать в любой соответствующий проект.</span><span class="sxs-lookup"><span data-stu-id="f9053-209">*(5.0+)* MSBuild `.targets` and `.props` files that flow transitively to any consuming project.</span></span> <span data-ttu-id="f9053-210">См. об [этой функции](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior).</span><span class="sxs-lookup"><span data-stu-id="f9053-210">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> | <span data-ttu-id="f9053-211">Автоматическое добавление в проект.</span><span class="sxs-lookup"><span data-stu-id="f9053-211">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="f9053-212">средства</span><span class="sxs-lookup"><span data-stu-id="f9053-212">tools</span></span> | <span data-ttu-id="f9053-213">Скрипты и программы PowerShell, доступные из консоли диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="f9053-213">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="f9053-214">Папка `tools` добавляется в переменную среды `PATH` только для консоли диспетчера пакетов (в частности, она *не* добавляется в переменную `PATH` для среды MSBuild при сборке проекта).</span><span class="sxs-lookup"><span data-stu-id="f9053-214">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="f9053-215">Так как в структуре папок может быть сколько угодно сборок для любого числа целевых платформ, этот метод обязателен при создании пакетов, поддерживающих несколько платформ.</span><span class="sxs-lookup"><span data-stu-id="f9053-215">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="f9053-216">После того как вы подготовите нужную структуру папок, выполните в ней следующую команду, чтобы создать файл `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="f9053-216">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="f9053-217">Созданный файл `.nuspec` не содержит явных ссылок на файлы в структуре папок.</span><span class="sxs-lookup"><span data-stu-id="f9053-217">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="f9053-218">NuGet автоматически включает все файлы при создании пакета.</span><span class="sxs-lookup"><span data-stu-id="f9053-218">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="f9053-219">Однако вам необходимо отредактировать значения-заполнители в других частях манифеста.</span><span class="sxs-lookup"><span data-stu-id="f9053-219">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="f9053-220">На основе библиотеки DLL сборки</span><span class="sxs-lookup"><span data-stu-id="f9053-220">From an assembly DLL</span></span>

<span data-ttu-id="f9053-221">В такой простой ситуации, как создание пакета на основе сборки, вы можете создать файл `.nuspec` из содержащихся в сборке метаданных с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="f9053-221">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="f9053-222">При использовании такого формата ряд заполнителей в манифесте заменяется конкретными значениями из сборки.</span><span class="sxs-lookup"><span data-stu-id="f9053-222">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="f9053-223">Например, свойству `<id>` присваивается имя сборки, а свойству `<version>` — ее версия.</span><span class="sxs-lookup"><span data-stu-id="f9053-223">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="f9053-224">Однако остальные свойства в манифесте не имеют соответствующих значений в сборке и поэтому по-прежнему содержат заполнители.</span><span class="sxs-lookup"><span data-stu-id="f9053-224">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="f9053-225">На основе проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f9053-225">From a Visual Studio project</span></span>

<span data-ttu-id="f9053-226">Создавать файл `.nuspec` на основе файла `.csproj` или `.vbproj` удобно, так как ссылки на другие пакеты, установленные в проекте, как и на зависимости, создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="f9053-226">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="f9053-227">Просто выполните следующую команду в папке, в которой находится файл проекта:</span><span class="sxs-lookup"><span data-stu-id="f9053-227">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="f9053-228">Получившийся файл `<project-name>.nuspec` содержит *токены*, которые заменяются во время создания пакета значениями их проекта, включая ссылки на другие пакеты, которые уже установлены.</span><span class="sxs-lookup"><span data-stu-id="f9053-228">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="f9053-229">Если у вас есть зависимости пакетов для включения в файл *.nuspec*, используйте вместо этого `nuget pack` и получите файл *.nuspec* из созданного файла *.nupkg*.</span><span class="sxs-lookup"><span data-stu-id="f9053-229">If you have package dependencies to include in the *.nuspec*, instead use `nuget pack`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="f9053-230">Например, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f9053-230">For example, use the following command.</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```
```

A token is delimited by `$` symbols on both sides of the project property. For example, the `<id>` value in a manifest generated in this way typically appears as follows:

```xml
<id>$id$</id>
```

<span data-ttu-id="f9053-231">Этот токен заменяется значением `AssemblyName` из файла проекта во время упаковки.</span><span class="sxs-lookup"><span data-stu-id="f9053-231">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="f9053-232">Точные сведения о том, как значения из проекта сопоставляются с токенами `.nuspec`, см. в [справочнике по токенам замены](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="f9053-232">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="f9053-233">Токены избавляют от необходимости изменять критически важные значения, такие как номер версии, в файле `.nuspec` при обновлении пакета.</span><span class="sxs-lookup"><span data-stu-id="f9053-233">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="f9053-234">(При необходимости токены всегда можно заменить на конкретные значения.)</span><span class="sxs-lookup"><span data-stu-id="f9053-234">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="f9053-235">Обратите внимание на то, что при работе с проектом Visual Studio доступно несколько дополнительных параметров создания пакета, которые описываются далее в подразделе [Выполнение команды nuget pack для создания файла NUPKG](#run-nuget-pack-to-generate-the-nupkg-file).</span><span class="sxs-lookup"><span data-stu-id="f9053-235">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#run-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="f9053-236">Пакеты на уровне решения</span><span class="sxs-lookup"><span data-stu-id="f9053-236">Solution-level packages</span></span>

<span data-ttu-id="f9053-237">*Только в NuGet 2.x. Недоступно в NuGet 3.0 и более поздних версиях.*</span><span class="sxs-lookup"><span data-stu-id="f9053-237">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="f9053-238">В NuGet 2.x поддерживалась концепция пакетов на уровне решения, которые устанавливают средства или дополнительные команды для консоли диспетчера команд (содержимое папки `tools`), но не добавляют ссылки, содержимое или настройки сборки в проекты решения.</span><span class="sxs-lookup"><span data-stu-id="f9053-238">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="f9053-239">Такие пакеты не содержат файлов непосредственно в папках `lib`, `content` или `build`, а их зависимости не содержат файлов в соответствующих папках `lib`, `content` или `build`.</span><span class="sxs-lookup"><span data-stu-id="f9053-239">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="f9053-240">NuGet отслеживает установленные пакеты уровня решения в файле `packages.config` в папке `.nuget`, а не в файле `packages.config` проекта.</span><span class="sxs-lookup"><span data-stu-id="f9053-240">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="f9053-241">Новый файл со значениями по умолчанию</span><span class="sxs-lookup"><span data-stu-id="f9053-241">New file with default values</span></span>

<span data-ttu-id="f9053-242">Следующая команда создает манифест по умолчанию с заполнителями, формируя надлежащую структуру файлов:</span><span class="sxs-lookup"><span data-stu-id="f9053-242">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="f9053-243">Если не указать параметр \<package-name\>, получившийся файл будет иметь имя `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="f9053-243">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="f9053-244">Если указать имя, например `Contoso.Utility.UsefulStuff`, файл будет иметь имя `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="f9053-244">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="f9053-245">Полученный файл `.nuspec` содержит заполнители для значений, например `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="f9053-245">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="f9053-246">Прежде чем использовать этот файл для создания итогового файла `.nupkg`, его необходимо отредактировать.</span><span class="sxs-lookup"><span data-stu-id="f9053-246">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="f9053-247">Выбор уникального идентификатора пакета и задание номера версии</span><span class="sxs-lookup"><span data-stu-id="f9053-247">Choose a unique package identifier and setting the version number</span></span>

<span data-ttu-id="f9053-248">Идентификатор пакета (элемент `<id>`) и номер версии (элемент `<version>`) — два самых важных значения в манифесте, так как они однозначно определяют код, содержащийся в пакете.</span><span class="sxs-lookup"><span data-stu-id="f9053-248">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="f9053-249">**Рекомендации в отношении идентификатора пакета**</span><span class="sxs-lookup"><span data-stu-id="f9053-249">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="f9053-250">**Уникальность**. Идентификатор должен быть уникальным в пределах nuget.org или другой коллекции, в которой размещается пакет.</span><span class="sxs-lookup"><span data-stu-id="f9053-250">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="f9053-251">Прежде чем задавать идентификатор, проверьте, не используется ли оно уже в соответствующей коллекции.</span><span class="sxs-lookup"><span data-stu-id="f9053-251">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="f9053-252">Во избежание конфликтов рекомендуется использовать в качестве первой части идентификатора название организации, например `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="f9053-252">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="f9053-253">**Имена в стиле пространств имен**. Используйте шаблон, по которому строятся имена пространств имен в .NET, используя нотацию с точками, а не с дефисами.</span><span class="sxs-lookup"><span data-stu-id="f9053-253">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="f9053-254">Например, используйте идентификатор `Contoso.Utility.UsefulStuff` вместо `Contoso-Utility-UsefulStuff` или `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="f9053-254">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="f9053-255">Пользователям также удобно, когда идентификатор пакета соответствует пространствам имен, используемым в коде.</span><span class="sxs-lookup"><span data-stu-id="f9053-255">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="f9053-256">**Примеры пакетов**. Если вы создаете пакет с примером кода, демонстрирующим использование другого пакета, добавьте к идентификатору суффикс `.Sample`, например `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="f9053-256">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="f9053-257">(Образец пакета, конечно, должен иметь зависимость от другого пакета.) При создании образца пакета используйте описанный выше метод на основе рабочего каталога, соответствующего соглашениям.</span><span class="sxs-lookup"><span data-stu-id="f9053-257">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="f9053-258">В папке `content` разместите код образца в папке с именем `\Samples\<identifier>`, например `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="f9053-258">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="f9053-259">**Рекомендации в отношении версии пакета**</span><span class="sxs-lookup"><span data-stu-id="f9053-259">**Best practices for the package version:**</span></span>

- <span data-ttu-id="f9053-260">Как правило, версия пакета должна соответствовать версии библиотеки, хотя это не строгое требование.</span><span class="sxs-lookup"><span data-stu-id="f9053-260">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="f9053-261">Это легко реализовать, если пакет ограничен единственной сборкой, как было описано выше в подразделе [Выбор сборок для добавления в пакет](#decide-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="f9053-261">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#decide-which-assemblies-to-package).</span></span> <span data-ttu-id="f9053-262">В целом помните, что при разрешении зависимостей диспетчер NuGet ориентируется на версии пакетов, а не на версии сборок.</span><span class="sxs-lookup"><span data-stu-id="f9053-262">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="f9053-263">При применении нестандартной схемы версий обязательно учитывайте правила управления версиями в NuGet, которые изложены в разделе [Управление версиями пакета](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="f9053-263">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="f9053-264">Разобраться в принципах управления версиями также может помочь следующая серия коротких записей блога:</span><span class="sxs-lookup"><span data-stu-id="f9053-264">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="f9053-265">Часть 1. Решение проблем с DLL</span><span class="sxs-lookup"><span data-stu-id="f9053-265">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="f9053-266">Часть 2. Базовый алгоритм</span><span class="sxs-lookup"><span data-stu-id="f9053-266">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="f9053-267">Часть 3. Унификация путем переадресации привязок</span><span class="sxs-lookup"><span data-stu-id="f9053-267">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a><span data-ttu-id="f9053-268">Добавление файла сведений и других файлов</span><span class="sxs-lookup"><span data-stu-id="f9053-268">Add a readme and other files</span></span>

<span data-ttu-id="f9053-269">Чтобы явным образом указать файлы, которые следует включить в пакет, используйте узел `<files>` в файле `.nuspec`, который находится *после* тега `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="f9053-269">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

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
> <span data-ttu-id="f9053-270">При использовании подхода на основе рабочего каталога, соответствующего соглашениям, файл readme.txt можно поместить в корневую папку пакета, а другое содержимое — в папку `content`.</span><span class="sxs-lookup"><span data-stu-id="f9053-270">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="f9053-271">Элементы `<file>` в манифесте не требуются.</span><span class="sxs-lookup"><span data-stu-id="f9053-271">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="f9053-272">Если в корневую папку пакета добавлен файл с именем `readme.txt`, Visual Studio отображает содержимое этого файла в виде обычного текста сразу после установки пакета напрямую.</span><span class="sxs-lookup"><span data-stu-id="f9053-272">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="f9053-273">(Файлы сведений не отображаются для пакетов, устанавливаемых как зависимости.)</span><span class="sxs-lookup"><span data-stu-id="f9053-273">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="f9053-274">Например, вот как выглядит файл сведений для пакета HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="f9053-274">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Отображение файла сведений для пакета NuGet при установке](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="f9053-276">Если узел `<files>` в файле `.nuspec` пуст, NuGet включает в пакет только содержимое из папки `lib`.</span><span class="sxs-lookup"><span data-stu-id="f9053-276">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="include-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="f9053-277">Включение в пакет свойств и целей MSBuild</span><span class="sxs-lookup"><span data-stu-id="f9053-277">Include MSBuild props and targets in a package</span></span>

<span data-ttu-id="f9053-278">В некоторых случаях в проекты, использующие пакет, необходимо добавить пользовательские целевые объекты сборки или свойства, например, если во время сборки должно запускаться пользовательское средство или процесс.</span><span class="sxs-lookup"><span data-stu-id="f9053-278">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="f9053-279">Для этого нужно поместить файлы в формате `<package_id>.targets` или `<package_id>.props` (например, `Contoso.Utility.UsefulStuff.targets`) в папку `\build` проекта.</span><span class="sxs-lookup"><span data-stu-id="f9053-279">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="f9053-280">Файлы в корневой папке `\build` считаются пригодными для всех целевых платформ.</span><span class="sxs-lookup"><span data-stu-id="f9053-280">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="f9053-281">Чтобы предоставить файлы для определенных платформ, сначала поместите их в соответствующие вложенные папки, например следующие:</span><span class="sxs-lookup"><span data-stu-id="f9053-281">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="f9053-282">Затем в файле `.nuspec` укажите ссылки на эти файлы в узле `<files>`:</span><span class="sxs-lookup"><span data-stu-id="f9053-282">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

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

<span data-ttu-id="f9053-283">Включение свойств и целевых объектов MSBuild в пакет [появилось в NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), поэтому рекомендуется добавить атрибут `minClientVersion="2.5"` в элемент `metadata`, чтобы указать минимальную версию клиента NuGet, необходимую для использования пакета.</span><span class="sxs-lookup"><span data-stu-id="f9053-283">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="f9053-284">Когда NuGet устанавливает пакет с `\build` файлом, он добавляет элементы MSBuild `<Import>` в файл проекта, указывая на `.targets` и `.props` файла.</span><span class="sxs-lookup"><span data-stu-id="f9053-284">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="f9053-285">(Файлы `.props` добавляются в начале файла проекта, а файлы `.targets` — в конце.) Отдельный условный элемент MSBuild `<Import>` добавляется в каждую требуемую версию .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="f9053-285">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="f9053-286">Файлы MSBuild `.props` и `.targets` для трансграничного таргетинга можно поместить в папку `\buildMultiTargeting`.</span><span class="sxs-lookup"><span data-stu-id="f9053-286">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildMultiTargeting` folder.</span></span> <span data-ttu-id="f9053-287">Во время установки пакета NuGet добавляет соответствующие элементы `<Import>` в файл проекта с условием, что требуемую версию .NET Framework не задано (свойство MSBuild `$(TargetFramework)` должно быть пустым).</span><span class="sxs-lookup"><span data-stu-id="f9053-287">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="f9053-288">В NuGet 3.x целевые объекты не добавляются в проект, а предоставляются через `{projectName}.nuget.g.targets` и `{projectName}.nuget.g.props`.</span><span class="sxs-lookup"><span data-stu-id="f9053-288">With NuGet 3.x, targets are not added to the project but are instead made available through `{projectName}.nuget.g.targets` and `{projectName}.nuget.g.props`.</span></span>

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="f9053-289">Выполнение команды nuget pack для создания файла NUPKG</span><span class="sxs-lookup"><span data-stu-id="f9053-289">Run nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="f9053-290">Чтобы создать пакет на основе сборки или рабочего каталога, соответствующего соглашениям, выполните команду `nuget pack`, указав файл `.nuspec`, где `<project-name>` необходимо заменить на имя файла:</span><span class="sxs-lookup"><span data-stu-id="f9053-290">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="f9053-291">При использовании проекта Visual Studio выполните команду `nuget pack`, указав файл проекта. В результате автоматически загрузится файл `.nuspec` проекта, и все токены в нем будут заменены значениями из файла проекта.</span><span class="sxs-lookup"><span data-stu-id="f9053-291">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="f9053-292">Использование файла проекта напрямую является необходимым для замены токенов, так как проект является источником значений токенов.</span><span class="sxs-lookup"><span data-stu-id="f9053-292">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="f9053-293">Замена токенов не производится при использовании команды `nuget pack` с файлом `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="f9053-293">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="f9053-294">В любом случае команда `nuget pack` исключает папки, начинающиеся с точки, например `.git` или `.hg`.</span><span class="sxs-lookup"><span data-stu-id="f9053-294">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="f9053-295">NuGet указывает, есть ли в файле `.nuspec` ошибки, требующие исправления, например, если вы забыли изменить значения-заполнители в манифесте.</span><span class="sxs-lookup"><span data-stu-id="f9053-295">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="f9053-296">После успешного выполнения команды `nuget pack` вы получаете файл `.nupkg`, который можно опубликовать в подходящей коллекции, как описано в разделе [Публикация пакета](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="f9053-296">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="f9053-297">После создания пакета его полезно просмотреть, открыв в средстве [Обозреватель пакетов](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer).</span><span class="sxs-lookup"><span data-stu-id="f9053-297">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="f9053-298">В нем в графической форме представлено содержимое пакета и его манифест.</span><span class="sxs-lookup"><span data-stu-id="f9053-298">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="f9053-299">Вы также можете переименовать полученный файл `.nupkg` в файл `.zip` и просмотреть его содержимое напрямую.</span><span class="sxs-lookup"><span data-stu-id="f9053-299">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="f9053-300">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="f9053-300">Additional options</span></span>

<span data-ttu-id="f9053-301">С командой `nuget pack` можно использовать различные параметры командной строки для исключения файлов, переопределения номера версии в манифесте, изменения папки выходных данных и совершения других действий.</span><span class="sxs-lookup"><span data-stu-id="f9053-301">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="f9053-302">Полный список параметров см. в [справочнике по команде pack](../reference/cli-reference/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="f9053-302">For a complete list, refer to the [pack command reference](../reference/cli-reference/cli-ref-pack.md).</span></span>

<span data-ttu-id="f9053-303">Ниже приводятся некоторые часто используемые с проектами Visual Studio параметры.</span><span class="sxs-lookup"><span data-stu-id="f9053-303">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="f9053-304">**Проекты, на которые указывают ссылки**. Если проект ссылается на другие проекты, вы можете включить их в пакет или добавить в качестве зависимостей с помощью параметра `-IncludeReferencedProjects`.</span><span class="sxs-lookup"><span data-stu-id="f9053-304">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="f9053-305">Включение является рекурсивным, поэтому если `MyProject.csproj` ссылается на проекты B и C, а они ссылаются на проекты D, E и F, в пакет включаются файлы из проектов B, C, D, E и F.</span><span class="sxs-lookup"><span data-stu-id="f9053-305">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="f9053-306">Если в проекте, на который указывает ссылка, есть собственный файл `.nuspec`, NuGet вместо этого добавляет проект как зависимость.</span><span class="sxs-lookup"><span data-stu-id="f9053-306">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="f9053-307">Такой проект необходимо упаковать и опубликовать отдельно.</span><span class="sxs-lookup"><span data-stu-id="f9053-307">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="f9053-308">**Конфигурация сборки**. По умолчанию NuGet использует стандартную конфигурацию сборки, указанную в файле проекта. Обычно это конфигурация *Debug*.</span><span class="sxs-lookup"><span data-stu-id="f9053-308">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="f9053-309">Чтобы упаковать файлы из другой конфигурации сборки, например *Release*, используйте параметр `-properties`, указав конфигурацию:</span><span class="sxs-lookup"><span data-stu-id="f9053-309">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="f9053-310">**Символы**. Чтобы включить символы, позволяющие пользователям осуществлять пошаговое выполнение кода в пакете, используйте параметр `-Symbols`:</span><span class="sxs-lookup"><span data-stu-id="f9053-310">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a><span data-ttu-id="f9053-311">Тестирование установки пакета</span><span class="sxs-lookup"><span data-stu-id="f9053-311">Test package installation</span></span>

<span data-ttu-id="f9053-312">Перед публикацией пакета, как правило, необходимо протестировать процесс его установки в проекте.</span><span class="sxs-lookup"><span data-stu-id="f9053-312">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="f9053-313">Это позволяет убедиться в том, что все необходимые файлы помещаются в нужные места.</span><span class="sxs-lookup"><span data-stu-id="f9053-313">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="f9053-314">Установку можно протестировать вручную в Visual Studio или в командной строке, выполнив стандартную [процедуру установки пакета](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="f9053-314">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

<span data-ttu-id="f9053-315">Для автоматического тестирования выполните указанные ниже основные действия.</span><span class="sxs-lookup"><span data-stu-id="f9053-315">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="f9053-316">Скопируйте файл `.nupkg` в локальную папку.</span><span class="sxs-lookup"><span data-stu-id="f9053-316">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="f9053-317">Добавьте эту папку в источники пакета с помощью команды `nuget sources add -name <name> -source <path>` (см. описание [команды nuget sources](../reference/cli-reference/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="f9053-317">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../reference/cli-reference/cli-ref-sources.md)).</span></span> <span data-ttu-id="f9053-318">Обратите внимание на то, что на каждом компьютере этот локальный источник необходимо задать только один раз.</span><span class="sxs-lookup"><span data-stu-id="f9053-318">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="f9053-319">Установите пакет из источника с помощью команды `nuget install <packageID> -source <name>`, где `<name>` соответствует имени источника, предоставленному команде `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="f9053-319">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="f9053-320">Указание источника позволяет гарантировать, что пакет будет устанавливаться только из него.</span><span class="sxs-lookup"><span data-stu-id="f9053-320">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="f9053-321">В файловой системе проверьте, правильно ли установились файлы.</span><span class="sxs-lookup"><span data-stu-id="f9053-321">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9053-322">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="f9053-322">Next Steps</span></span>

<span data-ttu-id="f9053-323">Создав пакет, то есть файл `.nupkg`, вы можете опубликовать его в любой коллекции на ваш выбор, как описано в разделе [Публикация пакета](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="f9053-323">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="f9053-324">Вы также можете расширить возможности пакета или обеспечить поддержку других сценариев, как описано в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="f9053-324">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="f9053-325">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="f9053-325">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="f9053-326">Поддержка нескольких целевых платформ</span><span class="sxs-lookup"><span data-stu-id="f9053-326">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="f9053-327">Преобразования исходных файлов и файлов конфигурации</span><span class="sxs-lookup"><span data-stu-id="f9053-327">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="f9053-328">Локализация</span><span class="sxs-lookup"><span data-stu-id="f9053-328">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="f9053-329">Предварительные версии</span><span class="sxs-lookup"><span data-stu-id="f9053-329">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="f9053-330">Определение типа пакета</span><span class="sxs-lookup"><span data-stu-id="f9053-330">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="f9053-331">Создание пакетов, содержащих сборки COM-взаимодействия</span><span class="sxs-lookup"><span data-stu-id="f9053-331">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="f9053-332">Наконец, существуют дополнительные типы пакетов, о которых нужно знать:</span><span class="sxs-lookup"><span data-stu-id="f9053-332">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="f9053-333">Собственные пакеты</span><span class="sxs-lookup"><span data-stu-id="f9053-333">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="f9053-334">Пакеты символов</span><span class="sxs-lookup"><span data-stu-id="f9053-334">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
