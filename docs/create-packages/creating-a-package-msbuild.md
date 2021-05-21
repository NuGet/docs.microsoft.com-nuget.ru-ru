---
title: Создание пакета NuGet с помощью MSBuild
description: Подробное руководство по проектированию и созданию пакета NuGet с помощью MSBuild, включая принятие решений по ключевым аспектам, таким как файлы и управление версиями.
author: JonDouglas
ms.author: jodou
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 18e0da335f65fde99d035388b95f35160757ee84
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901464"
---
# <a name="create-a-nuget-package-using-msbuild"></a><span data-ttu-id="4aae1-103">Создание пакета NuGet с помощью MSBuild</span><span class="sxs-lookup"><span data-stu-id="4aae1-103">Create a NuGet package using MSBuild</span></span>

<span data-ttu-id="4aae1-104">При создании пакета NuGet из кода вы формируете компонент, которым можно поделиться с любым количеством разработчиков для совместного использования.</span><span class="sxs-lookup"><span data-stu-id="4aae1-104">When you create a NuGet package from your code, you package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="4aae1-105">В этой статье описывается, как создать пакет с помощью MSBuild.</span><span class="sxs-lookup"><span data-stu-id="4aae1-105">This article describes how to create a package using MSBuild.</span></span> <span data-ttu-id="4aae1-106">MSBuild предустанавливается с каждой рабочей нагрузкой Visual Studio, содержащей NuGet.</span><span class="sxs-lookup"><span data-stu-id="4aae1-106">MSBuild comes preinstalled with every Visual Studio workload that contains NuGet.</span></span> <span data-ttu-id="4aae1-107">Кроме того, можно использовать MSBuild через dotnet CLI с помощью команды [dotnet msbuild](/dotnet/core/tools/dotnet-msbuild).</span><span class="sxs-lookup"><span data-stu-id="4aae1-107">Additionally you can also use MSBuild through the dotnet CLI with [dotnet msbuild](/dotnet/core/tools/dotnet-msbuild).</span></span>

<span data-ttu-id="4aae1-108">Для проектов .NET Core и .NET Standard с [форматом в стиле пакета SDK](../resources/check-project-format.md) и других проектов в таком стиле NuGet использует сведения в файле проекта напрямую для создания пакета.</span><span class="sxs-lookup"><span data-stu-id="4aae1-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span>  <span data-ttu-id="4aae1-109">Для проекта в стиле, отличном от SDK, который использует `<PackageReference>`, NuGet также использует файл проекта для создания пакета.</span><span class="sxs-lookup"><span data-stu-id="4aae1-109">For a non-SDK-style project that uses `<PackageReference>`, NuGet also uses the project file to create a package.</span></span>

<span data-ttu-id="4aae1-110">Проекты в стиле SDK имеют функциональные возможности пакетирования по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4aae1-110">SDK-style projects have the pack functionality available by default.</span></span> <span data-ttu-id="4aae1-111">Для проектов PackageReference в стиле, отличном от SDK, необходимо добавить пакет NuGet.Build.Tasks.Pack в зависимости проекта.</span><span class="sxs-lookup"><span data-stu-id="4aae1-111">For non SDK-style PackageReference projects, you need to add the NuGet.Build.Tasks.Pack package to the project dependencies.</span></span> <span data-ttu-id="4aae1-112">Подробные сведения о целевых объектах пакета MSBuild см. в разделе [Пакет NuGet и восстановление в качестве целевых объектов MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="4aae1-112">For detailed information about MSBuild pack targets, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

<span data-ttu-id="4aae1-113">Команда, создающая пакет, `msbuild -t:pack`, эквивалентна `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="4aae1-113">The command that creates a package, `msbuild -t:pack`, is functionality equivalent to `dotnet pack`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4aae1-114">Эта статья применяется к проектам [в стиле SDK](../resources/check-project-format.md) (обычно это проекты .NET Core и .NET Standard), а также к проектам в других стилях, использующим PackageReference.</span><span class="sxs-lookup"><span data-stu-id="4aae1-114">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects, and to non-SDK-style projects that use PackageReference.</span></span>

## <a name="set-properties"></a><span data-ttu-id="4aae1-115">Настройка свойств</span><span class="sxs-lookup"><span data-stu-id="4aae1-115">Set properties</span></span>

<span data-ttu-id="4aae1-116">Для создания пакета необходимы следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="4aae1-116">The following properties are required to create a package.</span></span>

- <span data-ttu-id="4aae1-117">`PackageId` — идентификатор пакета, который должен быть уникальным в пределах коллекции, содержащей пакет.</span><span class="sxs-lookup"><span data-stu-id="4aae1-117">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="4aae1-118">Если не задано, по умолчанию используется значение `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="4aae1-118">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="4aae1-119">`Version` —определенный номер версии в формате *основной_номер.дополнительный_номер.исправление[-суффикс]* , где *-суффикс* указывает на [предварительные версии](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="4aae1-119">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="4aae1-120">По умолчанию используется значение 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="4aae1-120">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="4aae1-121">название пакета, которое должно отображаться на сайте размещения (например, nuget.org);</span><span class="sxs-lookup"><span data-stu-id="4aae1-121">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="4aae1-122">`Authors` — сведения об авторе и владельце.</span><span class="sxs-lookup"><span data-stu-id="4aae1-122">`Authors`, author and owner information.</span></span> <span data-ttu-id="4aae1-123">Если не задано, по умолчанию используется значение `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="4aae1-123">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="4aae1-124">`Company` — название компании.</span><span class="sxs-lookup"><span data-stu-id="4aae1-124">`Company`, your company name.</span></span> <span data-ttu-id="4aae1-125">Если не задано, по умолчанию используется значение `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="4aae1-125">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="4aae1-126">Кроме того, при упаковке проектов, использующих PackageReference, в стиле, отличном от пакетов SDK, требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="4aae1-126">Additionally if you are packing non-SDK-style projects that use PackageReference, the following is required:</span></span>

- <span data-ttu-id="4aae1-127">`PackageOutputPath` — выходная папка для пакета, созданного при вызове пакета.</span><span class="sxs-lookup"><span data-stu-id="4aae1-127">`PackageOutputPath`, the output folder for the package generated when calling pack.</span></span>

<span data-ttu-id="4aae1-128">В Visual Studio эти значения можно задать в свойствах проекта (щелкните правой кнопкой мыши проект в обозревателе решений, выберите **Свойства** и перейдите на вкладку **Пакет**).</span><span class="sxs-lookup"><span data-stu-id="4aae1-128">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="4aae1-129">Эти свойства также можно задать напрямую в файле проекта (*.csproj*).</span><span class="sxs-lookup"><span data-stu-id="4aae1-129">You can also set these properties directly in the project files (*.csproj*).</span></span>

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="4aae1-130">Присвойте пакету идентификатор, который будет уникальным на сайте nuget.org или в другом используемом источнике пакета.</span><span class="sxs-lookup"><span data-stu-id="4aae1-130">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="4aae1-131">В следующем примере показан простой полный файл проекта, в котором содержатся эти свойства.</span><span class="sxs-lookup"><span data-stu-id="4aae1-131">The following example shows a simple, complete project file with these properties included.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="4aae1-132">Можно также задать дополнительные свойства, такие как `Title`, `PackageDescription` и `PackageTags` (см. подробнее об [использовании целевых объектов пакета MSBuild](../reference/msbuild-targets.md#pack-target), [управлении ресурсами зависимостей](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) и [использовании свойств метаданных NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties)).</span><span class="sxs-lookup"><span data-stu-id="4aae1-132">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="4aae1-133">Если пакет будет общедоступным, обратите особое внимание на свойство **PackageTags**, так как теги помогают найти ваш пакет и понять его назначение.</span><span class="sxs-lookup"><span data-stu-id="4aae1-133">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="4aae1-134">Подробные сведения об объявлении зависимостей и указании номеров версий см. в разделе [Ссылки на пакеты в файлах проекта](../consume-packages/package-references-in-project-files.md) и [Управление версиями пакетов](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4aae1-134">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="4aae1-135">Доступ к ресурсам зависимостей в пакете можно также предоставлять напрямую с помощью атрибутов `<IncludeAssets>` и `<ExcludeAssets>`.</span><span class="sxs-lookup"><span data-stu-id="4aae1-135">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="4aae1-136">См. подробнее об [управлении ресурсами зависимостей](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="4aae1-136">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="4aae1-137">Добавление необязательного поля описания</span><span class="sxs-lookup"><span data-stu-id="4aae1-137">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="4aae1-138">Выбор уникального идентификатора пакета и номера версии</span><span class="sxs-lookup"><span data-stu-id="4aae1-138">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a><span data-ttu-id="4aae1-139">Добавление пакета NuGet.Build.Tasks.Pack</span><span class="sxs-lookup"><span data-stu-id="4aae1-139">Add the NuGet.Build.Tasks.Pack package</span></span>

<span data-ttu-id="4aae1-140">Если вы используете MSBuild с проектом в стиле, отличном от SDK, и PackageReference, добавьте пакет NuGet.Build.Tasks.Pack в проект.</span><span class="sxs-lookup"><span data-stu-id="4aae1-140">If you are using MSBuild with a non-SDK-style project and PackageReference, add the NuGet.Build.Tasks.Pack package to your project.</span></span>

1. <span data-ttu-id="4aae1-141">Откройте файл проекта и добавьте следующее после элемента `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="4aae1-141">Open the project file and add the following after the `<PropertyGroup>` element:</span></span>

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="4aae1-142">Откройте Командную строку разработчика (в **поле поиска** введите **Командная строка разработчика**).</span><span class="sxs-lookup"><span data-stu-id="4aae1-142">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="4aae1-143">В общем случае следует запустить Командную строку разработчика для Visual Studio из меню **Пуск**, так как в этом случае настраиваются все необходимые пути для MSBuild.</span><span class="sxs-lookup"><span data-stu-id="4aae1-143">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

3. <span data-ttu-id="4aae1-144">Перейдите в папку, содержащую файл проекта, и введите следующую команду, чтобы установить пакет NuGet.Build.Tasks.Pack.</span><span class="sxs-lookup"><span data-stu-id="4aae1-144">Switch to the folder containing the project file and type the following command to install the NuGet.Build.Tasks.Pack package.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   <span data-ttu-id="4aae1-145">Убедитесь, что выходные данные MSBuild показывают, что сборка выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="4aae1-145">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="run-the-msbuild--tpack-command"></a><span data-ttu-id="4aae1-146">Выполните команду msbuild -t:pack</span><span class="sxs-lookup"><span data-stu-id="4aae1-146">Run the msbuild -t:pack command</span></span>

<span data-ttu-id="4aae1-147">Чтобы создать пакет NuGet (`.nupkg` файл) из проекта, запустите команду `msbuild -t:pack`, которая также автоматически построит проект:</span><span class="sxs-lookup"><span data-stu-id="4aae1-147">To build a NuGet package (a `.nupkg` file) from the project, run the `msbuild -t:pack` command, which also builds the project automatically:</span></span>

<span data-ttu-id="4aae1-148">В командной строке разработчика для Visual Studio введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4aae1-148">In the Developer command prompt for Visual Studio, type the following command:</span></span>

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

<span data-ttu-id="4aae1-149">На выходе показан путь к файлу `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="4aae1-149">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="4aae1-150">Автоматическое создание пакета при сборке</span><span class="sxs-lookup"><span data-stu-id="4aae1-150">Automatically generate package on build</span></span>

<span data-ttu-id="4aae1-151">Чтобы автоматически выполнить команду `msbuild -t:pack` при сборке или восстановлении проекта, в разделе `<PropertyGroup>` файла проекта добавьте следующую строку:</span><span class="sxs-lookup"><span data-stu-id="4aae1-151">To automatically run `msbuild -t:pack` when you build or restore the project, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="4aae1-152">Выполнив `msbuild -t:pack` в решении, вы упакуете все проекты в решении, которые можно упаковать (свойство [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) имеет значение `true`).</span><span class="sxs-lookup"><span data-stu-id="4aae1-152">When you run `msbuild -t:pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="4aae1-153">При автоматическом создании пакета время на упаковку увеличивает время сборки проекта.</span><span class="sxs-lookup"><span data-stu-id="4aae1-153">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="4aae1-154">Тестирование установки пакета</span><span class="sxs-lookup"><span data-stu-id="4aae1-154">Test package installation</span></span>

<span data-ttu-id="4aae1-155">Перед публикацией пакета, как правило, необходимо протестировать процесс его установки в проекте.</span><span class="sxs-lookup"><span data-stu-id="4aae1-155">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="4aae1-156">Это позволяет убедиться в том, что все необходимые файлы помещаются в нужные места.</span><span class="sxs-lookup"><span data-stu-id="4aae1-156">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="4aae1-157">Установку можно протестировать вручную в Visual Studio или в командной строке, выполнив стандартную [процедуру установки пакета](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="4aae1-157">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4aae1-158">Пакеты не изменяются.</span><span class="sxs-lookup"><span data-stu-id="4aae1-158">Packages are immutable.</span></span> <span data-ttu-id="4aae1-159">Если вы устраните проблему, измените содержимое пакета и снова выполните упаковку, при повторном тестировании вы все равно будете использовать старую версию пакета до тех пор, [пока не будет очищена папка глобальных пакетов](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders).</span><span class="sxs-lookup"><span data-stu-id="4aae1-159">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="4aae1-160">Это особенно важно при тестировании пакетов, которые не используют уникальную метку предварительной версии при каждой сборке.</span><span class="sxs-lookup"><span data-stu-id="4aae1-160">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4aae1-161">Next Steps</span><span class="sxs-lookup"><span data-stu-id="4aae1-161">Next Steps</span></span>

<span data-ttu-id="4aae1-162">Создав пакет, то есть файл `.nupkg`, вы можете опубликовать его в любой коллекции на ваш выбор, как описано в разделе [Публикация пакета](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="4aae1-162">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="4aae1-163">Вы также можете расширить возможности пакета или обеспечить поддержку других сценариев, как описано в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="4aae1-163">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="4aae1-164">Объекты pack и restore NuGet в качестве целевых объектов MSBuild</span><span class="sxs-lookup"><span data-stu-id="4aae1-164">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
- [<span data-ttu-id="4aae1-165">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="4aae1-165">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="4aae1-166">Поддержка нескольких целевых платформ</span><span class="sxs-lookup"><span data-stu-id="4aae1-166">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="4aae1-167">Преобразования исходных файлов и файлов конфигурации</span><span class="sxs-lookup"><span data-stu-id="4aae1-167">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="4aae1-168">Локализация</span><span class="sxs-lookup"><span data-stu-id="4aae1-168">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="4aae1-169">Предварительные версии</span><span class="sxs-lookup"><span data-stu-id="4aae1-169">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="4aae1-170">Определение типа пакета</span><span class="sxs-lookup"><span data-stu-id="4aae1-170">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="4aae1-171">Создание пакетов, содержащих сборки COM-взаимодействия</span><span class="sxs-lookup"><span data-stu-id="4aae1-171">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="4aae1-172">Наконец, существуют дополнительные типы пакетов, о которых нужно знать:</span><span class="sxs-lookup"><span data-stu-id="4aae1-172">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="4aae1-173">Собственные пакеты</span><span class="sxs-lookup"><span data-stu-id="4aae1-173">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="4aae1-174">Пакеты символов</span><span class="sxs-lookup"><span data-stu-id="4aae1-174">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)