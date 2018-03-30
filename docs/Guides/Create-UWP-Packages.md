---
title: Создание пакетов NuGet Packages для универсальной платформы Windows | Документы Майкрософт
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/21/2017
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: Полное пошаговое руководство по созданию пакетов NuGet с помощью компонента среды выполнения Windows для универсальной платформы Windows.
keywords: создание пакета, пакеты для UWP, компоненты среды выполнения Windows
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 6923cdc87b0a550abb51316e384c79137eeaf63a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="create-uwp-packages"></a><span data-ttu-id="2f0a8-104">Создание пакетов универсальной платформы Windows</span><span class="sxs-lookup"><span data-stu-id="2f0a8-104">Create UWP packages</span></span>

<span data-ttu-id="2f0a8-105">[Универсальная платформа Windows (UWP)](https://developer.microsoft.com/windows) предоставляет единую платформу приложений для всех устройств с операционной системой Windows 10.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-105">The [Universal Windows Platform (UWP)](https://developer.microsoft.com/windows) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="2f0a8-106">В этой модели приложения UWP могут вызывать как интерфейсы API WinRT, общие для всех устройств, так и интерфейсы API (включая Win32 и .NET), относящиеся только к семейству устройств, на которых работает приложение.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-106">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="2f0a8-107">В этом пошаговом руководстве вы создадите пакет NuGet с собственным компонентом UWP (включая элемент управления XAML), который можно использовать как в управляемых, так и в собственных проектах.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-107">In this walkthrough you create a NuGet package with a native UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f0a8-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2f0a8-108">Prerequisites</span></span>

1. <span data-ttu-id="2f0a8-109">Visual Studio 2017 или Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-109">Visual Studio 2017 or Visual Studio 2015.</span></span> <span data-ttu-id="2f0a8-110">Установите бесплатный выпуск Community 2017 с сайта [visualstudio.com](https://www.visualstudio.com/). Вы также можете использовать выпуски Professional и Enterprise.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-110">Install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="2f0a8-111">Интерфейс командной строки NuGet.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-111">NuGet CLI.</span></span> <span data-ttu-id="2f0a8-112">Скачайте последнюю версию `nuget.exe` на странице [nuget.org/downloads](https://nuget.org/downloads), сохранив ее в любом месте на ваш выбор (скачивается сразу файл `.exe`).</span><span class="sxs-lookup"><span data-stu-id="2f0a8-112">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="2f0a8-113">Затем добавьте это расположение в переменную среды PATH, если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-113">Then add that location to your PATH environment variable if it isn't already.</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="2f0a8-114">Создание компонента среды выполнения Windows для UWP</span><span class="sxs-lookup"><span data-stu-id="2f0a8-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="2f0a8-115">В Visual Studio последовательно выберите **Файл > Создать > Проект**, разверните узел **Visual C++ > Windows > Универсальные**, выберите шаблон **Компонент среды выполнения Windows (универсальные приложения для Windows)**, измените имя на ImageEnhancer и нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="2f0a8-115">In Visual Studio, choose **File > New > Project**, expand the **Visual C++ > Windows > Universal** node, select the **Windows Runtime Component (Universal Windows)** template, change the name to ImageEnhancer, and click OK.</span></span> <span data-ttu-id="2f0a8-116">При появлении запроса оставьте значения свойств "Конечная версия" и "Минимальная версия" по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Создание проекта "Компонент среды выполнения Windows" для UWP](media/UWP-NewProject.png)

1. <span data-ttu-id="2f0a8-118">В обозревателе решений щелкните проект правой кнопкой мыши, выберите пункты **Добавить > Новый элемент**, щелкните узел **Visual C++ > XAML**, выберите элемент **Элемент управления-шаблон**, измените имя на AwesomeImageControl.cpp и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-118">Right click the project in Solution Explorer, select **Add > New Item**, click the **Visual C++ > XAML** node, select **Templated Control**, change the name to AwesomeImageControl.cpp, and click **Add**:</span></span>

    ![Добавление нового элемента управления-шаблона XAML в проект](media/UWP-NewXAMLControl.png)

1. <span data-ttu-id="2f0a8-120">В обозревателе решений щелкните проект правой кнопкой мыши и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="2f0a8-121">На странице "Свойства" разверните узел **Свойства конфигурации > C/C++** и щелкните элемент **Выходные файлы**.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-121">In the Properties page, expand **Configuration Properties > C/C++** and click **Output Files**.</span></span> <span data-ttu-id="2f0a8-122">В области справа измените значение свойства **Создавать файлы XML-документации** на "Да".</span><span class="sxs-lookup"><span data-stu-id="2f0a8-122">In the pane on the right, change the value for **Generate XML Documentation Files** to Yes:</span></span>

    ![Установка свойства "Создавать файлы XML-документации" в значение "Да"](media/UWP-GenerateXMLDocFiles.png)

1. <span data-ttu-id="2f0a8-124">Теперь щелкните *решение* правой кнопкой мыши, выберите пункт **Пакетная сборка** и в открывшемся диалоговом окне установите три флажка в строках, соответствующих конфигурации отладки, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-124">Right click the *solution* now, select **Batch Build**, check the three Debug boxes in the dialog as shown below.</span></span> <span data-ttu-id="2f0a8-125">Благодаря этому при сборке создается полный набор артефактов для каждой из целевых систем, поддерживаемых Windows.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-125">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Пакетная сборка](media/UWP-BatchBuild.png)

1. <span data-ttu-id="2f0a8-127">В диалоговом окне "Пакетная сборка" щелкните **Сборка**, чтобы проверить проект и создать выходные файлы, которые потребуются для пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-127">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="2f0a8-128">В этом пошаговом руководстве для пакета будут использоваться артефакты отладки.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-128">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="2f0a8-129">Если пакет не является отладочным, в диалоговом окне "Пакетная сборка" установите вместо этого флажки в строках, соответствующих конфигурации выпуска, и при выполнении последующих действий обращайтесь к полученным папкам выпуска.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-129">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="2f0a8-130">Создание и изменение файла NUSPEC</span><span class="sxs-lookup"><span data-stu-id="2f0a8-130">Create and update the .nuspec file</span></span>

<span data-ttu-id="2f0a8-131">Чтобы создать исходный файл `.nuspec`, выполните три указанных ниже действия.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-131">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="2f0a8-132">В следующих разделах приводятся указания по другим необходимым изменениям.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-132">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="2f0a8-133">Откройте командную строку и перейдите к папке, содержащей файл `ImageEnhancer.vcxproj` (это вложенная папка в папке с файлом решения).</span><span class="sxs-lookup"><span data-stu-id="2f0a8-133">Open a command prompt and navigate to the folder containing `ImageEnhancer.vcxproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="2f0a8-134">Выполните команду NuGet `spec`, чтобы создать файл `ImageEnhancer.nuspec` (его имя будет соответствовать имени файла `.vcxproj`):</span><span class="sxs-lookup"><span data-stu-id="2f0a8-134">Run the NuGet `spec` command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.vcxproj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="2f0a8-135">Откройте файл `ImageEnhancer.nuspec` в редакторе и измените его содержимое так, как показано ниже, заменив YOUR_NAME на соответствующее значение.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-135">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="2f0a8-136">Значение `<id>` должно быть уникальным в пределах nuget.org (см. соглашения об именовании, описанные в разделе [Создание пакета](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="2f0a8-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="2f0a8-137">Кроме того, обратите внимание на то, что необходимо изменить теги author и description, иначе на этапе упаковки произойдет ошибка.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="2f0a8-138">Если пакет будет общедоступным, обратите особое внимание на элемент `<tags>`, так как эти теги помогают найти ваш пакет и понять его назначение.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="2f0a8-139">Добавление метаданных Windows в пакет</span><span class="sxs-lookup"><span data-stu-id="2f0a8-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="2f0a8-140">Компоненту среды выполнения Windows требуются метаданные, которые описывают все его общедоступные типы, что делает возможным использование компонента другими приложениями и библиотеками.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="2f0a8-141">Эти метаданные содержатся в файле WINMD, который создается при компиляции проекта и должен быть включен в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="2f0a8-142">В это же время создается XML-файл с данными IntelliSense, который также необходимо включить в пакет.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="2f0a8-143">Добавьте следующий узел `<files>` в файл `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="2f0a8-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="2f0a8-144">Добавление содержимого XAML</span><span class="sxs-lookup"><span data-stu-id="2f0a8-144">Adding XAML content</span></span>

<span data-ttu-id="2f0a8-145">Чтобы добавить элемент управления XAML вместе с компонентом, необходимо включить XAML-файл с шаблоном по умолчанию для элемента управления (который создается шаблоном проекта).</span><span class="sxs-lookup"><span data-stu-id="2f0a8-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="2f0a8-146">Он также указывается в разделе `<files>`:</span><span class="sxs-lookup"><span data-stu-id="2f0a8-146">This also goes in the `<files>` section:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="2f0a8-147">Добавление библиотек, реализованных в машинном коде</span><span class="sxs-lookup"><span data-stu-id="2f0a8-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="2f0a8-148">В компоненте основная логика типа ImageEnhancer реализована в машинном коде, который содержится в различных сборках `ImageEnhancer.dll`, создаваемых для каждой целевой среды выполнения (ARM, x86 и x64).</span><span class="sxs-lookup"><span data-stu-id="2f0a8-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.dll` assemblies that are generated for each target runtime (ARM, x86, and x64).</span></span> <span data-ttu-id="2f0a8-149">Чтобы включить их в пакет, добавьте ссылки на них и на связанные с ними PRI-файлы ресурсов в раздел `<files>`:</span><span class="sxs-lookup"><span data-stu-id="2f0a8-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a><span data-ttu-id="2f0a8-150">Добавление файла TARGETS</span><span class="sxs-lookup"><span data-stu-id="2f0a8-150">Adding .targets</span></span>

<span data-ttu-id="2f0a8-151">В проектах C++ и JavaScript, которые могут использовать ваш пакет NuGet, требуется файл TARGETS, в котором определяются необходимые файлы сборок и файлы WINMD.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-151">Next, C++ and JavaScript projects that might consume your NuGet package need a .targets file to identify the necessary assembly and winmd files.</span></span> <span data-ttu-id="2f0a8-152">(В C# и Visual Basic это делается автоматически.) Чтобы создать этот файл, скопируйте приведенный ниже текст в файл `ImageEnhancer.targets` и сохраните его в той же папке, что и файл `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-152">(C# and Visual Basic projects do this automatically.) Create this file by copying the text below into `ImageEnhancer.targets` and save it in the same folder as the `.nuspec` file.</span></span> <span data-ttu-id="2f0a8-153">_Примечание_. Имя этого файла `.targets` должно совпадать с идентификатором пакета (например, элемент `<Id>` в файле `.nupspec`).</span><span class="sxs-lookup"><span data-stu-id="2f0a8-153">_Note_: This `.targets` file needs to be the same name as the package ID (e.g. the `<Id>` element in the `.nupspec` file):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

<span data-ttu-id="2f0a8-154">Затем добавьте ссылку на файл `ImageEnhancer.targets` в файле `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="2f0a8-154">Then refer to `ImageEnhancer.targets` in your `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="2f0a8-155">Итоговый файл NUSPEC</span><span class="sxs-lookup"><span data-stu-id="2f0a8-155">Final .nuspec</span></span>

<span data-ttu-id="2f0a8-156">Итоговый файл `.nuspec` должен выглядеть следующим образом (YOUR_NAME, и в этом случае необходимо заменить на соответствующее значение):</span><span class="sxs-lookup"><span data-stu-id="2f0a8-156">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="2f0a8-157">Упаковка компонента</span><span class="sxs-lookup"><span data-stu-id="2f0a8-157">Package the component</span></span>

<span data-ttu-id="2f0a8-158">Когда будет готов файл `.nuspec` со ссылками на все файлы, которые необходимо включить в пакет, можно выполнить команду `pack`:</span><span class="sxs-lookup"><span data-stu-id="2f0a8-158">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="2f0a8-159">Будет создан `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-159">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="2f0a8-160">Если открыть файл в таком средстве, как [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), и развернуть все узлы, отобразится следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="2f0a8-160">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Пакет ImageEnhancer в обозревателе пакетов NuGet](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="2f0a8-162">Файл `.nupkg` — это просто ZIP-файл с другим расширением.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-162">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="2f0a8-163">Поэтому чтобы просмотреть содержимое пакета, можно просто изменить расширение `.nupkg` на `.zip`, но не забудьте восстановить расширение перед отправкой пакета на сайт nuget.org.</span><span class="sxs-lookup"><span data-stu-id="2f0a8-163">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="2f0a8-164">Чтобы предоставить доступ к пакету другим разработчикам, следуйте инструкциям в разделе [Публикация пакета](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="2f0a8-164">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="2f0a8-165">См. также</span><span class="sxs-lookup"><span data-stu-id="2f0a8-165">Related topics</span></span>

- [<span data-ttu-id="2f0a8-166">Справочник по файлу NUSPEC</span><span class="sxs-lookup"><span data-stu-id="2f0a8-166">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="2f0a8-167">Пакеты символов</span><span class="sxs-lookup"><span data-stu-id="2f0a8-167">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="2f0a8-168">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="2f0a8-168">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="2f0a8-169">Поддержка нескольких версий платформы .NET Framework</span><span class="sxs-lookup"><span data-stu-id="2f0a8-169">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="2f0a8-170">Включение в пакет свойств и целей MSBuild</span><span class="sxs-lookup"><span data-stu-id="2f0a8-170">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="2f0a8-171">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="2f0a8-171">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
