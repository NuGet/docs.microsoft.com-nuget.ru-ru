---
title: Упаковка элементов управления универсальной платформы Windows с помощью NuGet
description: Описывается, как создавать пакеты NuGet, содержащие элементы управления универсальной платформы Windows, включая необходимые метаданные и вспомогательные файлы для конструкторов Visual Studio и Blend.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/14/2018
ms.topic: tutorial
ms.openlocfilehash: 963846e857c8757176e4fbe1cd60c92a7397ba01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a><span data-ttu-id="68d2d-103">Создание элементов управления универсальной платформы Windows в виде пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="68d2d-103">Creating UWP controls as NuGet packages</span></span>

<span data-ttu-id="68d2d-104">В Visual Studio 2017 вы можете использовать возможности добавления элементов управления универсальной платформы Windows (UWP) в пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="68d2d-104">With Visual Studio 2017, you can take advantage of added capabilities for UWP controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="68d2d-105">В данном руководстве рассматривается использование этих возможностей на примере [образца пакета ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="68d2d-105">This guide walks you through these capabilities using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="68d2d-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="68d2d-106">Prerequisites</span></span>

1. <span data-ttu-id="68d2d-107">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="68d2d-107">Visual Studio 2017</span></span>
1. <span data-ttu-id="68d2d-108">Умение [создавать пакеты UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="68d2d-108">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="68d2d-109">Добавление поддержки элементов управления XAML на панели элементов или в области ресурсов</span><span class="sxs-lookup"><span data-stu-id="68d2d-109">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="68d2d-110">Чтобы элемент управления XAML отображался на панели элементов конструктора XAML в Visual Studio и в области ресурсов Blend, создайте файл `VisualStudioToolsManifest.xml` в корне папки `tools` проекта пакета.</span><span class="sxs-lookup"><span data-stu-id="68d2d-110">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="68d2d-111">Этот файл не требуется, если не нужно, чтобы элемент управления отображался на панели элементов или в области ресурсов.</span><span class="sxs-lookup"><span data-stu-id="68d2d-111">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="68d2d-112">Файл имеет следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="68d2d-112">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="68d2d-113">Здесь:</span><span class="sxs-lookup"><span data-stu-id="68d2d-113">where:</span></span>

- <span data-ttu-id="68d2d-114">*your_package_file* — имя файла элемента управления, например `ManagedPackage.winmd` (ManagedPackage — это произвольное имя, которое взято для примера и не имеет особого значения).</span><span class="sxs-lookup"><span data-stu-id="68d2d-114">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="68d2d-115">*vs_category* — метка группы, в которой должен отображаться элемент управления на панели элементов в конструкторе Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="68d2d-115">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="68d2d-116">Элемент `VSCategory` необходим для отображения элемента управления на панели элементов.</span><span class="sxs-lookup"><span data-stu-id="68d2d-116">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="68d2d-117">*blend_category* — метка группы, в которой должен отображаться элемент управления в области ресурсов конструктора Blend.</span><span class="sxs-lookup"><span data-stu-id="68d2d-117">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="68d2d-118">Элемент `BlendCategory` необходим для отображения элемента управления в области ресурсов.</span><span class="sxs-lookup"><span data-stu-id="68d2d-118">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="68d2d-119">*type_full_name_n* — полное имя каждого элемента управления, включая пространство имен, например `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="68d2d-119">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="68d2d-120">Обратите внимание на то, что нотация с точкой используется как для управляемых, так и для собственных типов.</span><span class="sxs-lookup"><span data-stu-id="68d2d-120">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="68d2d-121">Если один пакет содержит несколько сборок элементов управления, можно включить несколько элементов `<File>` в элемент `<FileList>`.</span><span class="sxs-lookup"><span data-stu-id="68d2d-121">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="68d2d-122">Вы также можете добавить несколько узлов `<ToolboxItems>` в один элемент `<File>`, чтобы упорядочить элементы управления по отдельным категориям.</span><span class="sxs-lookup"><span data-stu-id="68d2d-122">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="68d2d-123">В приведенном ниже примере элемент управления, реализованный в файле `ManagedPackage.winmd`, будет отображаться в Visual Studio и Blend в группе "Managed Package" (Управляемый пакет) и иметь имя MyCustomControl.</span><span class="sxs-lookup"><span data-stu-id="68d2d-123">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="68d2d-124">Все эти имена являются произвольными.</span><span class="sxs-lookup"><span data-stu-id="68d2d-124">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Пример элемента управления в Visual Studio](media/UWP-control-vs-toolbox.png)

![Пример элемента управления в Blend](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="68d2d-127">Каждый элемент, который должен отображаться на панели элементов или в области ресурсов, необходимо указывать явным образом.</span><span class="sxs-lookup"><span data-stu-id="68d2d-127">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="68d2d-128">При этом следует использовать формат `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="68d2d-128">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="68d2d-129">Добавление пользовательских значков для элементов управления</span><span class="sxs-lookup"><span data-stu-id="68d2d-129">Add custom icons to your controls</span></span>

<span data-ttu-id="68d2d-130">Чтобы на панели элементов или в области ресурсов отображался пользовательский значок, добавьте изображение в свой проект или соответствующий проект `design.dll` с именем Namespace.ControlName.extension и выберите действие сборки "Внедренный ресурс".</span><span class="sxs-lookup"><span data-stu-id="68d2d-130">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="68d2d-131">Поддерживаемые форматы: `.png`, `.jpg`, `.jpeg`, `.gif` и `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="68d2d-131">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="68d2d-132">Рекомендуемый размер изображения — 64 на 64 пикселя.</span><span class="sxs-lookup"><span data-stu-id="68d2d-132">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="68d2d-133">В приведенном ниже примере проект содержит файл изображения с именем ManagedPackage.MyCustomControl.png.</span><span class="sxs-lookup"><span data-stu-id="68d2d-133">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Задание пользовательского значка в проекте](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="68d2d-135">Для собственных элементов управления значки следует добавлять в качестве ресурсов в проект `design.dll`.</span><span class="sxs-lookup"><span data-stu-id="68d2d-135">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="68d2d-136">Поддержка определенных версий платформы Windows</span><span class="sxs-lookup"><span data-stu-id="68d2d-136">Support specific Windows platform versions</span></span>

<span data-ttu-id="68d2d-137">Пакеты UWP имеют свойства TargetPlatformVersion (TPV) и TargetPlatformMinVersion (TPMinV), которые определяют самую позднюю и самую раннюю версии ОС, в которых может быть установлено приложение.</span><span class="sxs-lookup"><span data-stu-id="68d2d-137">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="68d2d-138">Кроме того, свойство TPV определяет версию пакета SDK, на основе которой создается приложение.</span><span class="sxs-lookup"><span data-stu-id="68d2d-138">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="68d2d-139">Учитывайте эти свойства при разработке пакета UWP: использование интерфейсов API, которые выходят за пределы определенных в приложении версий платформы, приведет либо к сбою сборки, либо к ошибке приложения во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="68d2d-139">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="68d2d-140">Например, предположим, что вы указали в качестве значения свойства TPMinV для пакета элементов управления юбилейное обновление Windows 10 (версия 10.0, сборка 14393), и вам необходимо сделать так, чтобы пакет использовался проектами UWP, предназначенными только для этой или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="68d2d-140">For example, let’s say you’ve set the TPMinV for you controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="68d2d-141">Чтобы пакет могли потреблять проекты UWP, необходимо упаковать элементы управления, используя следующие имена папок:</span><span class="sxs-lookup"><span data-stu-id="68d2d-141">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0\*
    \ref\uap10.0\*

<span data-ttu-id="68d2d-142">Для проведения проверки TPMinV создайте [файл целей MSBuild](/visualstudio/msbuild/msbuild-targets) и включите его в пакет в папке `build\uap10.0" folder as `<имя_вашей_сборки>.targets`, replacing `<имя_вашей_сборки> на имя собственной сборки.</span><span class="sxs-lookup"><span data-stu-id="68d2d-142">To enforce the appropriate TPMinV check, create an [MSBuild targets file](/visualstudio/msbuild/msbuild-targets) and package it under the `build\uap10.0" folder as `<your_assembly_name>.targets`, replacing `<your_assembly_name>\` with the name of your specific assembly.</span></span>

<span data-ttu-id="68d2d-143">Вот пример того, как должен выглядеть файл целей:</span><span class="sxs-lookup"><span data-stu-id="68d2d-143">Here is an example of what the targets file should look like:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="ResolveAssemblyReferences" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a><span data-ttu-id="68d2d-144">Добавление поддержки на этапе разработки</span><span class="sxs-lookup"><span data-stu-id="68d2d-144">Add design-time support</span></span>

<span data-ttu-id="68d2d-145">Чтобы указать, где должны отображаться свойства элемента управления в инспекторе свойств, добавьте пользовательские графические элементы и другие элементы, а затем поместите файл `design.dll` в папку `lib\uap10.0\Design` для соответствующей целевой платформы.</span><span class="sxs-lookup"><span data-stu-id="68d2d-145">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="68d2d-146">Кроме того, чтобы работала команда **[Изменить шаблон > Изменить копию](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)**, нужно включить файл `Generic.xaml` и все объединяемые словари ресурсов в папку `<your_assembly_name>\Themes` (опять с использованием фактического имени сборки).</span><span class="sxs-lookup"><span data-stu-id="68d2d-146">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="68d2d-147">(Этот файл не влияет на поведение элемента управления во время выполнения.) В результате структура папок будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="68d2d-147">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="68d2d-148">По умолчанию свойства элемента управления отображаются в инспекторе свойств в категории "Прочее".</span><span class="sxs-lookup"><span data-stu-id="68d2d-148">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="68d2d-149">Использование строк и ресурсов</span><span class="sxs-lookup"><span data-stu-id="68d2d-149">Use strings and resources</span></span>

<span data-ttu-id="68d2d-150">В пакет можно внедрить строковые ресурсы (`.resw`), которые могут использоваться элементом управления или проектом UWP. Выберите для свойства **Действие сборки** файла `.resw` значение **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="68d2d-150">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="68d2d-151">Пример можно найти в файле [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) в образце пакета ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="68d2d-151">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

## <a name="package-content-such-as-images"></a><span data-ttu-id="68d2d-152">Упаковка содержимого, такого как изображения</span><span class="sxs-lookup"><span data-stu-id="68d2d-152">Package content such as images</span></span>

<span data-ttu-id="68d2d-153">Чтобы упаковать содержимое, например изображения, которое может использоваться элементом управления или проектом UWP, поместите эти файлы в папку `lib\uap10.0`.</span><span class="sxs-lookup"><span data-stu-id="68d2d-153">To package content such as images that can be used by your control or the consuming UWP project, place those files within the `lib\uap10.0` folder.</span></span>

<span data-ttu-id="68d2d-154">Вы также можете создать [файл целей MSBuild](/visualstudio/msbuild/msbuild-targets), чтобы ресурс копировался в выходную папку проекта.</span><span class="sxs-lookup"><span data-stu-id="68d2d-154">You may also author an [MSBuild targets file](/visualstudio/msbuild/msbuild-targets) to ensure the asset is copied to the consuming project’s output folder:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a><span data-ttu-id="68d2d-155">См. также</span><span class="sxs-lookup"><span data-stu-id="68d2d-155">See also</span></span>

- [<span data-ttu-id="68d2d-156">Создание пакетов универсальной платформы Windows</span><span class="sxs-lookup"><span data-stu-id="68d2d-156">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="68d2d-157">Образец ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="68d2d-157">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
