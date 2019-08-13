---
title: Создание пакета NuGet с помощью CLI dotnet
description: Подробное руководство по проектированию и созданию пакета NuGet, включая принятие решений по ключевым аспектам, таким как файлы и управление версиями.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 8222e1edfa13951d2fda9a2384d93bba38ef4979
ms.sourcegitcommit: ba8ad1bd13a4bba3df94374e34e20c425a05af2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2019
ms.locfileid: "68833299"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="81816-103">Создание пакета NuGet с помощью CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="81816-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="81816-104">Независимо от назначения вашего пакета или содержащегося в нем кода, с помощью одного из средств CLI (`nuget.exe` или `dotnet.exe`) вы можете создать компонент, которым можно поделиться с любым количеством разработчиков для совместного использования.</span><span class="sxs-lookup"><span data-stu-id="81816-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="81816-105">В этой статье описывается, как создать пакет с помощью CLI dotnet.</span><span class="sxs-lookup"><span data-stu-id="81816-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="81816-106">См. подробнее об установке средств CLI `dotnet` в руководстве по [установке клиентских средств NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="81816-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="81816-107">Начиная с Visual Studio 2017, CLI dotnet входит в состав рабочих нагрузок .NET Core.</span><span class="sxs-lookup"><span data-stu-id="81816-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="81816-108">Для проектов .NET Core и .NET Standard с [форматом в стиле пакета SDK](../resources/check-project-format.md) и других проектов в таком стиле NuGet использует сведения в файле проекта напрямую для создания пакета.</span><span class="sxs-lookup"><span data-stu-id="81816-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="81816-109">См. пошаговые руководства по созданию пакетов .NET Standard с использованием [CLI dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) и [Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="81816-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) or [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="81816-110">`msbuild -t:pack` — это функциональный эквивалент `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="81816-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="81816-111">Чтобы выполнить сборку с помощью MSBuild, см. раздел [Создание пакета NuGet с помощью MSBuild](creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="81816-111">To build with MSBuild, see [Create a NuGet package using MSBuild](creating-a-package-msbuild.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="81816-112">Этот раздел относится к проектам [на основе пакетов SDK](../resources/check-project-format.md), в частности, к проектам .NET Core и .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="81816-112">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="81816-113">Настройка свойств</span><span class="sxs-lookup"><span data-stu-id="81816-113">Set properties</span></span>

<span data-ttu-id="81816-114">Для создания пакета необходимы следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="81816-114">The following properties are required to create a package.</span></span>

- <span data-ttu-id="81816-115">`PackageId` — идентификатор пакета, который должен быть уникальным в пределах коллекции, содержащей пакет.</span><span class="sxs-lookup"><span data-stu-id="81816-115">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="81816-116">Если не задано, по умолчанию используется значение `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="81816-116">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="81816-117">`Version` —определенный номер версии в формате *основной_номер.дополнительный_номер.исправление[-суффикс]* , где *-суффикс* указывает на [предварительные версии](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="81816-117">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="81816-118">По умолчанию используется значение 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="81816-118">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="81816-119">название пакета, которое должно отображаться на сайте размещения (например, nuget.org);</span><span class="sxs-lookup"><span data-stu-id="81816-119">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="81816-120">`Authors` — сведения об авторе и владельце.</span><span class="sxs-lookup"><span data-stu-id="81816-120">`Authors`, author and owner information.</span></span> <span data-ttu-id="81816-121">Если не задано, по умолчанию используется значение `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="81816-121">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="81816-122">`Company` — название компании.</span><span class="sxs-lookup"><span data-stu-id="81816-122">`Company`, your company name.</span></span> <span data-ttu-id="81816-123">Если не задано, по умолчанию используется значение `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="81816-123">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="81816-124">В Visual Studio эти значения можно задать в свойствах проекта (щелкните правой кнопкой мыши проект в обозревателе решений, выберите **Свойства** и перейдите на вкладку **Пакет**).</span><span class="sxs-lookup"><span data-stu-id="81816-124">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="81816-125">Эти свойства также можно задать напрямую в файле проекта (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="81816-125">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="81816-126">Присвойте пакету идентификатор, который будет уникальным на сайте nuget.org или в другом используемом источнике пакета.</span><span class="sxs-lookup"><span data-stu-id="81816-126">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="81816-127">В следующем примере показан простой полный файл проекта, в котором содержатся эти свойства.</span><span class="sxs-lookup"><span data-stu-id="81816-127">The following example shows a simple, complete project file with these properties included.</span></span> <span data-ttu-id="81816-128">(Можно создать новый проект по умолчанию с помощью команды `dotnet new classlib`.)</span><span class="sxs-lookup"><span data-stu-id="81816-128">(You can create a new default project using the `dotnet new classlib` command.)</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="81816-129">Можно также задать дополнительные свойства, такие как `Title`, `PackageDescription` и `PackageTags` (см. подробнее об [использовании целевых объектов пакета MSBuild](../reference/msbuild-targets.md#pack-target), [управлении ресурсами зависимостей](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) и [использовании свойств метаданных NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties)).</span><span class="sxs-lookup"><span data-stu-id="81816-129">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="81816-130">Если пакет будет общедоступным, обратите особое внимание на свойство **PackageTags**, так как теги помогают найти ваш пакет и понять его назначение.</span><span class="sxs-lookup"><span data-stu-id="81816-130">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="81816-131">Подробные сведения об объявлении зависимостей и указании номеров версий см. в разделе [Ссылки на пакеты в файлах проекта](../consume-packages/package-references-in-project-files.md) и [Управление версиями пакетов](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="81816-131">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="81816-132">Доступ к ресурсам зависимостей в пакете можно также предоставлять напрямую с помощью атрибутов `<IncludeAssets>` и `<ExcludeAssets>`.</span><span class="sxs-lookup"><span data-stu-id="81816-132">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="81816-133">См. подробнее об [управлении ресурсами зависимостей](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="81816-133">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="81816-134">Выбор уникального идентификатора пакета и номера версии</span><span class="sxs-lookup"><span data-stu-id="81816-134">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a><span data-ttu-id="81816-135">Выполнение команды pack</span><span class="sxs-lookup"><span data-stu-id="81816-135">Run the pack command</span></span>

<span data-ttu-id="81816-136">Чтобы создать пакет NuGet (`.nupkg` файл) из проекта, запустите команду `dotnet pack`, которая также автоматически построит проект:</span><span class="sxs-lookup"><span data-stu-id="81816-136">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="81816-137">На выходе показан путь к файлу `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="81816-137">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="81816-138">Автоматическое создание пакета при сборке</span><span class="sxs-lookup"><span data-stu-id="81816-138">Automatically generate package on build</span></span>

<span data-ttu-id="81816-139">Чтобы автоматически выполнить команду `dotnet pack` вместе с командой `dotnet build`, в разделе `<PropertyGroup>` файла проекта добавьте следующую строку:</span><span class="sxs-lookup"><span data-stu-id="81816-139">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="81816-140">Выполнив `dotnet pack` в решении, вы упакуете все проекты в решении, которые можно упаковать (свойство [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) имеет значение `true`).</span><span class="sxs-lookup"><span data-stu-id="81816-140">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="81816-141">При автоматическом создании пакета время на упаковку увеличивает время сборки проекта.</span><span class="sxs-lookup"><span data-stu-id="81816-141">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="81816-142">Тестирование установки пакета</span><span class="sxs-lookup"><span data-stu-id="81816-142">Test package installation</span></span>

<span data-ttu-id="81816-143">Перед публикацией пакета, как правило, необходимо протестировать процесс его установки в проекте.</span><span class="sxs-lookup"><span data-stu-id="81816-143">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="81816-144">Это позволяет убедиться в том, что все необходимые файлы помещаются в нужные места.</span><span class="sxs-lookup"><span data-stu-id="81816-144">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="81816-145">Установку можно протестировать вручную в Visual Studio или в командной строке, выполнив стандартную [процедуру установки пакета](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="81816-145">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="81816-146">Пакеты не изменяются.</span><span class="sxs-lookup"><span data-stu-id="81816-146">Packages are immutable.</span></span> <span data-ttu-id="81816-147">Если вы устраните проблему, измените содержимое пакета и снова выполните упаковку, при повторном тестировании вы все равно будете использовать старую версию пакета до тех пор, [пока не будет очищена папка глобальных пакетов](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders).</span><span class="sxs-lookup"><span data-stu-id="81816-147">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="81816-148">Это особенно важно при тестировании пакетов, которые не используют уникальную метку предварительной версии при каждой сборке.</span><span class="sxs-lookup"><span data-stu-id="81816-148">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81816-149">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="81816-149">Next Steps</span></span>

<span data-ttu-id="81816-150">Создав пакет, то есть файл `.nupkg`, вы можете опубликовать его в любой коллекции на ваш выбор, как описано в разделе [Публикация пакета](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="81816-150">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="81816-151">Вы также можете расширить возможности пакета или обеспечить поддержку других сценариев, как описано в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="81816-151">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="81816-152">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="81816-152">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="81816-153">Поддержка нескольких целевых платформ</span><span class="sxs-lookup"><span data-stu-id="81816-153">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="81816-154">Преобразования исходных файлов и файлов конфигурации</span><span class="sxs-lookup"><span data-stu-id="81816-154">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="81816-155">Локализация</span><span class="sxs-lookup"><span data-stu-id="81816-155">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="81816-156">Предварительные версии</span><span class="sxs-lookup"><span data-stu-id="81816-156">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="81816-157">Определение типа пакета</span><span class="sxs-lookup"><span data-stu-id="81816-157">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="81816-158">Создание пакетов, содержащих сборки COM-взаимодействия</span><span class="sxs-lookup"><span data-stu-id="81816-158">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="81816-159">Наконец, существуют дополнительные типы пакетов, о которых нужно знать:</span><span class="sxs-lookup"><span data-stu-id="81816-159">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="81816-160">Собственные пакеты</span><span class="sxs-lookup"><span data-stu-id="81816-160">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="81816-161">Пакеты символов</span><span class="sxs-lookup"><span data-stu-id="81816-161">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
