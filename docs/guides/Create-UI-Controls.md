---
title: Упаковка элементов управления пользовательским интерфейсом с помощью NuGet
description: Создание пакетов NuGet, которые содержат элементы управления UWP или WPF, включая необходимые метаданные и вспомогательные файлы для конструкторов Visual Studio и Blend.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: ab7499c415f63319fd314f33607f74d400b5f957
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818662"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="646c0-103">Создание элементов управления пользовательским интерфейсом в виде пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="646c0-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="646c0-104">В Visual Studio 2017 вы можете использовать возможности добавления элементов управления UWP и WPF в пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="646c0-104">With Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="646c0-105">В руководстве описано, как использовать эти возможности в контексте элементов управления UWP с использованием [примера ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="646c0-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="646c0-106">Это же применимо к элементам управления WPF, если не указано иное.</span><span class="sxs-lookup"><span data-stu-id="646c0-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="646c0-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="646c0-107">Prerequisites</span></span>

1. <span data-ttu-id="646c0-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="646c0-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="646c0-109">Умение [создавать пакеты UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="646c0-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="646c0-110">Создание структуры библиотеки</span><span class="sxs-lookup"><span data-stu-id="646c0-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="646c0-111">Это применимо только к элементам управления UWP.</span><span class="sxs-lookup"><span data-stu-id="646c0-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="646c0-112">Настраивая свойство `GenerateLibraryLayout`, вы обеспечите создание результатов сборки проекта в макете, который готов к упаковке без необходимости включать записи отдельных файлов в nuspec.</span><span class="sxs-lookup"><span data-stu-id="646c0-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="646c0-113">В окне свойств проекта перейдите на вкладку сборки и установите флажок "Создать структуру библиотеки".</span><span class="sxs-lookup"><span data-stu-id="646c0-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="646c0-114">Это изменит файл проекта и задаст для флага `GenerateLibraryLayout` значение true для текущее выбранной конфигурации сборки и платформы.</span><span class="sxs-lookup"><span data-stu-id="646c0-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="646c0-115">Можно также изменить файл проекта, чтобы добавить `<GenerateLibraryLayout>true</GenerateLibraryLayout>` в первую безусловную группу свойств.</span><span class="sxs-lookup"><span data-stu-id="646c0-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="646c0-116">Так свойство будет применено независимо от конфигурации сборки и платформы.</span><span class="sxs-lookup"><span data-stu-id="646c0-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="646c0-117">Добавление поддержки элементов управления XAML на панели элементов или в области ресурсов</span><span class="sxs-lookup"><span data-stu-id="646c0-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="646c0-118">Чтобы элемент управления XAML отображался на панели элементов конструктора XAML в Visual Studio и в области ресурсов Blend, создайте файл `VisualStudioToolsManifest.xml` в корне папки `tools` проекта пакета.</span><span class="sxs-lookup"><span data-stu-id="646c0-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="646c0-119">Этот файл не требуется, если не нужно, чтобы элемент управления отображался на панели элементов или в области ресурсов.</span><span class="sxs-lookup"><span data-stu-id="646c0-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="646c0-120">Файл имеет следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="646c0-120">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="646c0-121">Здесь:</span><span class="sxs-lookup"><span data-stu-id="646c0-121">where:</span></span>

- <span data-ttu-id="646c0-122">*your_package_file* — имя файла элемента управления, например `ManagedPackage.winmd` (ManagedPackage — это произвольное имя, которое взято для примера и не имеет особого значения).</span><span class="sxs-lookup"><span data-stu-id="646c0-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="646c0-123">*vs_category* — метка группы, в которой должен отображаться элемент управления на панели элементов в конструкторе Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="646c0-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="646c0-124">Элемент `VSCategory` необходим для отображения элемента управления на панели элементов.</span><span class="sxs-lookup"><span data-stu-id="646c0-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="646c0-125">*blend_category* — метка группы, в которой должен отображаться элемент управления в области ресурсов конструктора Blend.</span><span class="sxs-lookup"><span data-stu-id="646c0-125">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="646c0-126">Элемент `BlendCategory` необходим для отображения элемента управления в области ресурсов.</span><span class="sxs-lookup"><span data-stu-id="646c0-126">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="646c0-127">*type_full_name_n* — полное имя каждого элемента управления, включая пространство имен, например `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="646c0-127">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="646c0-128">Обратите внимание на то, что нотация с точкой используется как для управляемых, так и для собственных типов.</span><span class="sxs-lookup"><span data-stu-id="646c0-128">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="646c0-129">Если один пакет содержит несколько сборок элементов управления, можно включить несколько элементов `<File>` в элемент `<FileList>`.</span><span class="sxs-lookup"><span data-stu-id="646c0-129">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="646c0-130">Вы также можете добавить несколько узлов `<ToolboxItems>` в один элемент `<File>`, чтобы упорядочить элементы управления по отдельным категориям.</span><span class="sxs-lookup"><span data-stu-id="646c0-130">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="646c0-131">В приведенном ниже примере элемент управления, реализованный в файле `ManagedPackage.winmd`, будет отображаться в Visual Studio и Blend в группе "Managed Package" (Управляемый пакет) и иметь имя MyCustomControl.</span><span class="sxs-lookup"><span data-stu-id="646c0-131">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="646c0-132">Все эти имена являются произвольными.</span><span class="sxs-lookup"><span data-stu-id="646c0-132">All these names are arbitrary.</span></span>

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
> <span data-ttu-id="646c0-135">Каждый элемент, который должен отображаться на панели элементов или в области ресурсов, необходимо указывать явным образом.</span><span class="sxs-lookup"><span data-stu-id="646c0-135">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="646c0-136">При этом следует использовать формат `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="646c0-136">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="646c0-137">Добавление пользовательских значков для элементов управления</span><span class="sxs-lookup"><span data-stu-id="646c0-137">Add custom icons to your controls</span></span>

<span data-ttu-id="646c0-138">Чтобы на панели элементов или в области ресурсов отображался пользовательский значок, добавьте изображение в свой проект или соответствующий проект `design.dll` с именем Namespace.ControlName.extension и выберите действие сборки "Внедренный ресурс".</span><span class="sxs-lookup"><span data-stu-id="646c0-138">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="646c0-139">Поддерживаемые форматы: `.png`, `.jpg`, `.jpeg`, `.gif` и `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="646c0-139">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="646c0-140">Рекомендуемый размер изображения — 64 на 64 пикселя.</span><span class="sxs-lookup"><span data-stu-id="646c0-140">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="646c0-141">В приведенном ниже примере проект содержит файл изображения с именем ManagedPackage.MyCustomControl.png.</span><span class="sxs-lookup"><span data-stu-id="646c0-141">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Задание пользовательского значка в проекте](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="646c0-143">Для собственных элементов управления значки следует добавлять в качестве ресурсов в проект `design.dll`.</span><span class="sxs-lookup"><span data-stu-id="646c0-143">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="646c0-144">Поддержка определенных версий платформы Windows</span><span class="sxs-lookup"><span data-stu-id="646c0-144">Support specific Windows platform versions</span></span>

<span data-ttu-id="646c0-145">Пакеты UWP имеют свойства TargetPlatformVersion (TPV) и TargetPlatformMinVersion (TPMinV), которые определяют самую позднюю и самую раннюю версии ОС, в которых может быть установлено приложение.</span><span class="sxs-lookup"><span data-stu-id="646c0-145">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="646c0-146">Кроме того, свойство TPV определяет версию пакета SDK, на основе которой создается приложение.</span><span class="sxs-lookup"><span data-stu-id="646c0-146">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="646c0-147">Учитывайте эти свойства при разработке пакета UWP: использование интерфейсов API, которые выходят за пределы определенных в приложении версий платформы, приведет либо к сбою сборки, либо к ошибке приложения во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="646c0-147">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="646c0-148">Например, предположим, что вы указали в качестве значения свойства TPMinV для пакета элементов управления юбилейное обновление Windows 10 (версия 10.0, сборка 14393), и вам нужно, чтобы пакет использовался проектами UWP, предназначенными только для этой или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="646c0-148">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="646c0-149">Чтобы пакет могли потреблять проекты UWP, необходимо упаковать элементы управления, используя следующие имена папок:</span><span class="sxs-lookup"><span data-stu-id="646c0-149">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="646c0-150">NuGet автоматически проверит TPMinV для используемого проекта и отменит установку, если версия будет ниже Windows 10 Anniversary Edition (10.0; сборка 14393).</span><span class="sxs-lookup"><span data-stu-id="646c0-150">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="646c0-151">Для WPF вы можете настроить использование пакета элементов управления WPF в проектах, предназначенных для .NET Framework версии 4.6.1 и выше.</span><span class="sxs-lookup"><span data-stu-id="646c0-151">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="646c0-152">Для этого вам нужно упаковать элементы управления, используя следующие имена папок:</span><span class="sxs-lookup"><span data-stu-id="646c0-152">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="646c0-153">Добавление поддержки на этапе разработки</span><span class="sxs-lookup"><span data-stu-id="646c0-153">Add design-time support</span></span>

<span data-ttu-id="646c0-154">Чтобы указать, где должны отображаться свойства элемента управления в инспекторе свойств, добавьте пользовательские графические элементы и другие элементы, а затем поместите файл `design.dll` в папку `lib\uap10.0.14393\Design` для соответствующей целевой платформы.</span><span class="sxs-lookup"><span data-stu-id="646c0-154">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="646c0-155">Кроме того, чтобы работала команда **[Изменить шаблон > Изменить копию](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)**, нужно включить файл `Generic.xaml` и все объединяемые словари ресурсов в папку `<your_assembly_name>\Themes` (опять с использованием фактического имени сборки).</span><span class="sxs-lookup"><span data-stu-id="646c0-155">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="646c0-156">(Этот файл не влияет на поведение элемента управления во время выполнения.) В результате структура папок будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="646c0-156">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="646c0-157">Пример, в котором можно настроить использование пакета средств управления WPF в проектах, предназначенных для .NET Framework версии 4.6.1 и выше:</span><span class="sxs-lookup"><span data-stu-id="646c0-157">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="646c0-158">По умолчанию свойства элемента управления отображаются в инспекторе свойств в категории "Прочее".</span><span class="sxs-lookup"><span data-stu-id="646c0-158">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="646c0-159">Использование строк и ресурсов</span><span class="sxs-lookup"><span data-stu-id="646c0-159">Use strings and resources</span></span>

<span data-ttu-id="646c0-160">В пакет можно внедрить строковые ресурсы (`.resw`), которые могут использоваться элементом управления или проектом UWP. Выберите для свойства **Действие сборки** файла `.resw` значение **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="646c0-160">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="646c0-161">Пример можно найти в файле [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) в образце пакета ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="646c0-161">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="646c0-162">Это применимо только к элементам управления UWP.</span><span class="sxs-lookup"><span data-stu-id="646c0-162">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="646c0-163">См. также</span><span class="sxs-lookup"><span data-stu-id="646c0-163">See also</span></span>

- [<span data-ttu-id="646c0-164">Создание пакетов универсальной платформы Windows</span><span class="sxs-lookup"><span data-stu-id="646c0-164">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="646c0-165">Образец ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="646c0-165">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
