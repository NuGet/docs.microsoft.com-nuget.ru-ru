---
title: "Упаковка элементов управления универсальной платформы Windows с помощью NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 3/21/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 1f9de20a-f394-4cf2-8e40-ba0f4239cd5e
description: "Описывается, как создавать пакеты NuGet, содержащие элементы управления универсальной платформы Windows, включая необходимые метаданные и вспомогательные файлы для конструкторов Visual Studio и Blend."
keywords: "элементы управления UWP NuGet, конструктор XAML в Visual Studio, конструктор Blend, пользовательские элементы управления"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8756ce472c11a05370914841245295361b3f179b
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a><span data-ttu-id="54926-104">Создание элементов управления универсальной платформы Windows в виде пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="54926-104">Creating UWP controls as NuGet packages</span></span>

<span data-ttu-id="54926-105">В Visual Studio 2017 вы можете использовать возможности добавления элементов управления универсальной платформы Windows (UWP) в пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="54926-105">With Visual Studio 2017, you can take advantage of added capabilities for UWP controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="54926-106">В данном руководстве рассматривается использование этих возможностей на примере [образца пакета ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="54926-106">This guide walks you through these capabilities using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> 

## <a name="pre-requisites"></a><span data-ttu-id="54926-107">Предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="54926-107">Pre-requisites:</span></span>

1.  <span data-ttu-id="54926-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="54926-108">Visual Studio 2017</span></span>
1.  <span data-ttu-id="54926-109">Умение [создавать пакеты UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="54926-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="54926-110">Добавление поддержки элементов управления XAML на панели элементов или в области ресурсов</span><span class="sxs-lookup"><span data-stu-id="54926-110">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="54926-111">Чтобы элемент управления XAML отображался на панели элементов конструктора XAML в Visual Studio и в области ресурсов Blend, создайте файл `VisualStudioToolsManifest.xml` в корне папки `tools` проекта пакета.</span><span class="sxs-lookup"><span data-stu-id="54926-111">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="54926-112">Этот файл не требуется, если не нужно, чтобы элемент управления отображался на панели элементов или в области ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54926-112">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

```
\build
\lib
\tools
    \VisualStudioToolsManifest.xml
```    

<span data-ttu-id="54926-113">Файл имеет следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="54926-113">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="54926-114">Здесь:</span><span class="sxs-lookup"><span data-stu-id="54926-114">where:</span></span>

- <span data-ttu-id="54926-115">*your_package_file* — имя файла элемента управления, например `ManagedPackage.winmd` (ManagedPackage — это произвольное имя, которое взято для примера и не имеет особого значения).</span><span class="sxs-lookup"><span data-stu-id="54926-115">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="54926-116">*vs_category* — метка группы, в которой должен отображаться элемент управления на панели элементов в конструкторе Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54926-116">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="54926-117">Элемент `VSCategory` необходим для отображения элемента управления на панели элементов.</span><span class="sxs-lookup"><span data-stu-id="54926-117">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="54926-118">*blend_category* — метка группы, в которой должен отображаться элемент управления в области ресурсов конструктора Blend.</span><span class="sxs-lookup"><span data-stu-id="54926-118">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="54926-119">Элемент `BlendCategory` необходим для отображения элемента управления в области ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54926-119">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="54926-120">*type_full_name_n* — полное имя каждого элемента управления, включая пространство имен, например `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="54926-120">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="54926-121">Обратите внимание на то, что нотация с точкой используется как для управляемых, так и для собственных типов.</span><span class="sxs-lookup"><span data-stu-id="54926-121">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="54926-122">Если один пакет содержит несколько сборок элементов управления, можно включить несколько элементов `<File>` в элемент `<FileList>`.</span><span class="sxs-lookup"><span data-stu-id="54926-122">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="54926-123">Вы также можете добавить несколько узлов `<ToolboxItems>` в один элемент `<File>`, чтобы упорядочить элементы управления по отдельным категориям.</span><span class="sxs-lookup"><span data-stu-id="54926-123">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="54926-124">В приведенном ниже примере элемент управления, реализованный в файле `ManagedPackage.winmd`, будет отображаться в Visual Studio и Blend в группе "Managed Package" (Управляемый пакет) и иметь имя MyCustomControl.</span><span class="sxs-lookup"><span data-stu-id="54926-124">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="54926-125">Все эти имена являются произвольными.</span><span class="sxs-lookup"><span data-stu-id="54926-125">All these names are arbitrary.</span></span>

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
> <span data-ttu-id="54926-128">Каждый элемент, который должен отображаться на панели элементов или в области ресурсов, необходимо указывать явным образом.</span><span class="sxs-lookup"><span data-stu-id="54926-128">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="54926-129">При этом следует использовать формат `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="54926-129">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="54926-130">Добавление пользовательских значков для элементов управления</span><span class="sxs-lookup"><span data-stu-id="54926-130">Add custom icons to your controls</span></span>

<span data-ttu-id="54926-131">Чтобы на панели элементов или в области ресурсов отображался пользовательский значок, добавьте изображение в свой проект или соответствующий проект `design.dll` с именем Namespace.ControlName.extension и выберите действие сборки "Внедренный ресурс".</span><span class="sxs-lookup"><span data-stu-id="54926-131">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="54926-132">Поддерживаемые форматы: `.png`, `.jpg`, `.jpeg`, `.gif` и `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="54926-132">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="54926-133">Рекомендуемый размер изображения — 64 на 64 пикселя.</span><span class="sxs-lookup"><span data-stu-id="54926-133">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="54926-134">В приведенном ниже примере проект содержит файл изображения с именем ManagedPackage.MyCustomControl.png.</span><span class="sxs-lookup"><span data-stu-id="54926-134">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Задание пользовательского значка в проекте](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="54926-136">Для собственных элементов управления значки следует добавлять в качестве ресурсов в проект `design.dll`.</span><span class="sxs-lookup"><span data-stu-id="54926-136">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="54926-137">Поддержка определенных версий платформы Windows</span><span class="sxs-lookup"><span data-stu-id="54926-137">Support specific Windows platform versions</span></span>

<span data-ttu-id="54926-138">Пакеты UWP имеют свойства TargetPlatformVersion (TPV) и TargetPlatformMinVersion (TPMinV), которые определяют самую позднюю и самую раннюю версии ОС, в которых может быть установлено приложение.</span><span class="sxs-lookup"><span data-stu-id="54926-138">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="54926-139">Кроме того, свойство TPV определяет версию пакета SDK, на основе которой создается приложение.</span><span class="sxs-lookup"><span data-stu-id="54926-139">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="54926-140">Учитывайте эти свойства при разработке пакета UWP: использование интерфейсов API, которые выходят за пределы определенных в приложении версий платформы, приведет либо к сбою сборки, либо к ошибке приложения во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="54926-140">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="54926-141">Например, предположим, что вы указали в качестве значения свойства TPMinV для пакета элементов управления юбилейное обновление Windows 10 (версия 10.0, сборка 14393), и вам необходимо сделать так, чтобы пакет использовался проектами UWP, предназначенными только для этой или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="54926-141">For example, let’s say you’ve set the TPMinV for you controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="54926-142">Чтобы пакет мог использоваться проектами UWP на основе `project.json`, необходимо упаковать элементы управления, используя следующие имена папок:</span><span class="sxs-lookup"><span data-stu-id="54926-142">To allow your package to be consumed by `project.json` based UWP projects, you must package your controls with the following folder names:</span></span>

```
\lib\uap10.0\*
\ref\uap10.0\*
```

<span data-ttu-id="54926-143">Для проведения проверки TPMinV создайте [файл целей MSBuild](/visualstudio/msbuild/msbuild-targets) и включите его в пакет в папке build (замените "your_assembly_name" на имя собственной сборки):</span><span class="sxs-lookup"><span data-stu-id="54926-143">To enforce the appropriate TPMinV check, create an [MSBuild targets file](/visualstudio/msbuild/msbuild-targets) and package it under the build folder (replacing "your_assembly_name" with the name of your specific assembly):</span></span>

```
\build
    \uap10.0
        your_assembly_name.targets
\lib
\tools
```

<span data-ttu-id="54926-144">Вот пример того, как должен выглядеть файл целей:</span><span class="sxs-lookup"><span data-stu-id="54926-144">Here is an example of what the targets file should look like:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="Build;ReBuild" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a><span data-ttu-id="54926-145">Добавление поддержки на этапе разработки</span><span class="sxs-lookup"><span data-stu-id="54926-145">Add design-time support</span></span>

<span data-ttu-id="54926-146">Чтобы указать, где должны отображаться свойства элемента управления в инспекторе свойств, добавьте пользовательские графические элементы и другие элементы, а затем поместите файл `design.dll` в папку `lib\<platform>\Design` для соответствующей целевой платформы.</span><span class="sxs-lookup"><span data-stu-id="54926-146">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\<platform>\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="54926-147">Кроме того, чтобы работала команда **[Изменить шаблон > Изменить копию](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)**, необходимо включить файл `Generic.xaml` и все объединяемые словари ресурсов в файл `<AssemblyName>\Themes`.</span><span class="sxs-lookup"><span data-stu-id="54926-147">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<AssemblyName>\Themes` folder.</span></span> <span data-ttu-id="54926-148">(Этот файл не влияет на поведение элемента управления во время выполнения.)</span><span class="sxs-lookup"><span data-stu-id="54926-148">(This file has no impact on the runtime behavior of a control.)</span></span>


```
\build
\lib
    \uap10.0.14393.0
        \Design
            \MyControl.design.dll
        \your_assembly_name
            \Themes     
                Generic.xaml
\tools
```

> [!Note]
> <span data-ttu-id="54926-149">По умолчанию свойства элемента управления отображаются в инспекторе свойств в категории "Прочее".</span><span class="sxs-lookup"><span data-stu-id="54926-149">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>


## <a name="use-strings-and-resources"></a><span data-ttu-id="54926-150">Использование строк и ресурсов</span><span class="sxs-lookup"><span data-stu-id="54926-150">Use strings and resources</span></span>

<span data-ttu-id="54926-151">В пакет можно внедрить строковые ресурсы (`.resw`), которые могут использоваться элементом управления или проектом UWP. Выберите для свойства **Действие сборки** файла `.resw` значение **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="54926-151">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="54926-152">Пример можно найти в файле [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) в образце пакета ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="54926-152">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

## <a name="package-content-such-as-images"></a><span data-ttu-id="54926-153">Упаковка содержимого, такого как изображения</span><span class="sxs-lookup"><span data-stu-id="54926-153">Package content such as images</span></span>

<span data-ttu-id="54926-154">Чтобы упаковать содержимое, например изображения, которое может использоваться элементом управления или проектом UWP,</span><span class="sxs-lookup"><span data-stu-id="54926-154">To package content such as images that can be used by your control or the consuming UWP project.</span></span> <span data-ttu-id="54926-155">добавьте папку `lib\uap10.0.14393.0` с этими файлами следующим образом (значение your_assembly_name и в этом случае должно соответствовать вашему элементу управления):</span><span class="sxs-lookup"><span data-stu-id="54926-155">add those files `lib\uap10.0.14393.0` folder as follows ("your_assembly_name" should again match your particular control):</span></span>

```
\build
\lib
    \uap10.0.14393.0
        \Design
        \your_assembly_name
\contosoSampleImage.jpg
\tools
```

<span data-ttu-id="54926-156">Вы также можете создать [файл целей MSBuild](/visualstudio/msbuild/msbuild-targets), чтобы ресурс копировался в выходную папку проекта:</span><span class="sxs-lookup"><span data-stu-id="54926-156">You may also author an[MSBuild targets file](/visualstudio/msbuild/msbuild-targets) to ensure the asset is copied to the consuming project’s output folder:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0.14393.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a><span data-ttu-id="54926-157">См. также</span><span class="sxs-lookup"><span data-stu-id="54926-157">See also</span></span>

- [<span data-ttu-id="54926-158">Создание пакетов универсальной платформы Windows</span><span class="sxs-lookup"><span data-stu-id="54926-158">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="54926-159">Образец ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="54926-159">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
