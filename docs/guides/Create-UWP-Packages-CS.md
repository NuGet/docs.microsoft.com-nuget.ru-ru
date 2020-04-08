---
title: Создание пакетов NuGet Packages для универсальной платформы Windows
description: Полное пошаговое руководство по созданию пакетов NuGet с помощью компонента среды выполнения Windows для универсальной платформы Windows C#.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231755"
---
# <a name="create-uwp-packages-c"></a><span data-ttu-id="4d8f7-103">Создание пакетов универсальной платформы Windows (C#)</span><span class="sxs-lookup"><span data-stu-id="4d8f7-103">Create UWP packages (C#)</span></span>

<span data-ttu-id="4d8f7-104">[Универсальная платформа Windows (UWP)](/windows/uwp) предоставляет единую платформу приложений для всех устройств с операционной системой Windows 10.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-104">The [Universal Windows Platform (UWP)](/windows/uwp) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="4d8f7-105">В этой модели приложения UWP могут вызывать как интерфейсы API WinRT, общие для всех устройств, так и интерфейсы API (включая Win32 и .NET), относящиеся только к семейству устройств, на которых работает приложение.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="4d8f7-106">В этом пошаговом руководстве вы создадите пакет NuGet с компонентом UWP на C# (включая элемент управления XAML), который можно использовать как в управляемых, так и в собственных проектах.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-106">In this walkthrough you create a NuGet package with a C# UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d8f7-107">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4d8f7-107">Prerequisites</span></span>

1. <span data-ttu-id="4d8f7-108">Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-108">Visual Studio 2019.</span></span> <span data-ttu-id="4d8f7-109">Установите бесплатный выпуск Community 2019 с сайта [visualstudio.com](https://www.visualstudio.com/). Вы также можете использовать выпуски Professional и Enterprise.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-109">Install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="4d8f7-110">Интерфейс командной строки NuGet.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-110">NuGet CLI.</span></span> <span data-ttu-id="4d8f7-111">Скачайте последнюю версию `nuget.exe` на странице [nuget.org/downloads](https://nuget.org/downloads), сохранив ее в любом месте на ваш выбор (скачивается сразу файл `.exe`).</span><span class="sxs-lookup"><span data-stu-id="4d8f7-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="4d8f7-112">Затем добавьте это расположение в переменную среды PATH, если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-112">Then add that location to your PATH environment variable if it isn't already.</span></span> <span data-ttu-id="4d8f7-113">[Дополнительные сведения](/nuget/reference/nuget-exe-cli-reference#windows).</span><span class="sxs-lookup"><span data-stu-id="4d8f7-113">[More details](/nuget/reference/nuget-exe-cli-reference#windows).</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="4d8f7-114">Создание компонента среды выполнения Windows для UWP</span><span class="sxs-lookup"><span data-stu-id="4d8f7-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="4d8f7-115">В Visual Studio последовательно выберите **Файл > Создать > Проект**, выполните поиск "uwp c#", выберите шаблон **Компонент среды выполнения Windows (универсальные приложения для Windows)** , нажмите кнопку "Далее", измените имя на ImageEnhancer и нажмите кнопку "Создать".</span><span class="sxs-lookup"><span data-stu-id="4d8f7-115">In Visual Studio, choose **File > New > Project**, search for "uwp c#", select the **Windows Runtime Component (Universal Windows)** template, click next, change the name to ImageEnhancer, and click Create.</span></span> <span data-ttu-id="4d8f7-116">При появлении запроса оставьте значения свойств "Конечная версия" и "Минимальная версия" по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Создание проекта "Компонент среды выполнения Windows" для UWP](media/UWP-NewProject-CS.png)

1. <span data-ttu-id="4d8f7-118">В обозревателе решений щелкните проект правой кнопкой мыши, выберите пункты **Добавить > Новый элемент**, выберите элемент **Элемент управления-шаблон**, измените имя на AwesomeImageControl.cs и нажмите кнопку **Добавить**:</span><span class="sxs-lookup"><span data-stu-id="4d8f7-118">Right click the project in Solution Explorer, select **Add > New Item**, select **Templated Control**, change the name to AwesomeImageControl.cs, and click **Add**:</span></span>

    ![Добавление нового элемента управления-шаблона XAML в проект](media/UWP-NewXAMLControl-CS.png)

1. <span data-ttu-id="4d8f7-120">В обозревателе решений щелкните проект правой кнопкой мыши и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="4d8f7-121">На странице "Свойства" выберите вкладку **Сборка** и включите **файл документации XML**:</span><span class="sxs-lookup"><span data-stu-id="4d8f7-121">In the Properties page, choose **Build** tab and enable **XML Documentation File**:</span></span>

    ![Установка свойства "Создавать файлы XML-документации" в значение "Да"](media/UWP-GenerateXMLDocFiles-CS.png)

1. <span data-ttu-id="4d8f7-123">Теперь щелкните *решение* правой кнопкой мыши, выберите пункт **Пакетная сборка** и в открывшемся диалоговом окне установите пять флажков сборки в диалоговом окне, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-123">Right click the *solution* now, select **Batch Build**, check the five build boxes in the dialog as shown below.</span></span> <span data-ttu-id="4d8f7-124">Благодаря этому при сборке создается полный набор артефактов для каждой из целевых систем, поддерживаемых Windows.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Пакетная сборка](media/UWP-BatchBuild-CS.png)

1. <span data-ttu-id="4d8f7-126">В диалоговом окне "Пакетная сборка" щелкните **Сборка**, чтобы проверить проект и создать выходные файлы, которые потребуются для пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="4d8f7-127">В этом пошаговом руководстве для пакета будут использоваться артефакты отладки.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="4d8f7-128">Если пакет не является отладочным, в диалоговом окне "Пакетная сборка" установите вместо этого флажки в строках, соответствующих конфигурации выпуска, и при выполнении последующих действий обращайтесь к полученным папкам выпуска.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="4d8f7-129">Создание и изменение файла NUSPEC</span><span class="sxs-lookup"><span data-stu-id="4d8f7-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="4d8f7-130">Чтобы создать исходный файл `.nuspec`, выполните три указанных ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="4d8f7-131">В следующих разделах приводятся указания по другим необходимым изменениям.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="4d8f7-132">Откройте командную строку и перейдите к папке, содержащей файл `ImageEnhancer.csproj` (это вложенная папка в папке с файлом решения).</span><span class="sxs-lookup"><span data-stu-id="4d8f7-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.csproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="4d8f7-133">Выполните команду [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec), чтобы создать файл `ImageEnhancer.nuspec` (его имя будет соответствовать имени файла `.csroj`):</span><span class="sxs-lookup"><span data-stu-id="4d8f7-133">Run the [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.csroj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="4d8f7-134">Откройте файл `ImageEnhancer.nuspec` в редакторе и измените его содержимое так, как показано ниже, заменив YOUR_NAME на соответствующее значение.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="4d8f7-135">Не оставляйте никаких значений $propertyName$.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-135">Do not leave any of the $propertyName$ values.</span></span> <span data-ttu-id="4d8f7-136">Значение `<id>` должно быть уникальным в пределах nuget.org (см. соглашения об именовании, описанные в разделе [Создание пакета](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="4d8f7-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="4d8f7-137">Кроме того, обратите внимание на то, что необходимо изменить теги author и description, иначе на этапе упаковки произойдет ошибка.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2020</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="4d8f7-138">Если пакет будет общедоступным, обратите особое внимание на элемент `<tags>`, так как эти теги помогают найти ваш пакет и понять его назначение.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="4d8f7-139">Добавление метаданных Windows в пакет</span><span class="sxs-lookup"><span data-stu-id="4d8f7-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="4d8f7-140">Компоненту среды выполнения Windows требуются метаданные, которые описывают все его общедоступные типы, что делает возможным использование компонента другими приложениями и библиотеками.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="4d8f7-141">Эти метаданные содержатся в файле WINMD, который создается при компиляции проекта и должен быть включен в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="4d8f7-142">В это же время создается XML-файл с данными IntelliSense, который также необходимо включить в пакет.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="4d8f7-143">Добавьте следующий узел `<files>` в файл `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="4d8f7-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="4d8f7-144">Добавление содержимого XAML</span><span class="sxs-lookup"><span data-stu-id="4d8f7-144">Adding XAML content</span></span>

<span data-ttu-id="4d8f7-145">Чтобы добавить элемент управления XAML вместе с компонентом, необходимо включить XAML-файл с шаблоном по умолчанию для элемента управления (который создается шаблоном проекта).</span><span class="sxs-lookup"><span data-stu-id="4d8f7-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="4d8f7-146">Он также указывается в разделе `<files>`:</span><span class="sxs-lookup"><span data-stu-id="4d8f7-146">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="4d8f7-147">Добавление библиотек, реализованных в машинном коде</span><span class="sxs-lookup"><span data-stu-id="4d8f7-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="4d8f7-148">В компоненте основная логика типа ImageEnhancer реализована в машинном коде, который содержится в различных сборках `ImageEnhancer.winmd`, создаваемых для каждой целевой среды выполнения (ARM, ARM64, x86 и x64).</span><span class="sxs-lookup"><span data-stu-id="4d8f7-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.winmd` assemblies that are generated for each target runtime (ARM, ARM64, x86, and x64).</span></span> <span data-ttu-id="4d8f7-149">Чтобы включить их в пакет, добавьте ссылки на них и на связанные с ними PRI-файлы ресурсов в раздел `<files>`:</span><span class="sxs-lookup"><span data-stu-id="4d8f7-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="4d8f7-150">Итоговый файл NUSPEC</span><span class="sxs-lookup"><span data-stu-id="4d8f7-150">Final .nuspec</span></span>

<span data-ttu-id="4d8f7-151">Итоговый файл `.nuspec` должен выглядеть следующим образом (YOUR_NAME, и в этом случае необходимо заменить на соответствующее значение):</span><span class="sxs-lookup"><span data-stu-id="4d8f7-151">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="4d8f7-152">Упаковка компонента</span><span class="sxs-lookup"><span data-stu-id="4d8f7-152">Package the component</span></span>

<span data-ttu-id="4d8f7-153">Когда будет готов файл `.nuspec` со ссылками на все файлы, которые необходимо включить в пакет, можно выполнить команду [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack):</span><span class="sxs-lookup"><span data-stu-id="4d8f7-153">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="4d8f7-154">Будет создан `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-154">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="4d8f7-155">Если открыть файл в таком средстве, как [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), и развернуть все узлы, отобразится следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="4d8f7-155">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Пакет ImageEnhancer в обозревателе пакетов NuGet](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="4d8f7-157">Файл `.nupkg` — это просто ZIP-файл с другим расширением.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-157">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="4d8f7-158">Поэтому чтобы просмотреть содержимое пакета, можно просто изменить расширение `.nupkg` на `.zip`, но не забудьте восстановить расширение перед отправкой пакета на сайт nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4d8f7-158">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="4d8f7-159">Чтобы предоставить доступ к пакету другим разработчикам, следуйте инструкциям в разделе [Публикация пакета](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="4d8f7-159">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="4d8f7-160">Связанные разделы</span><span class="sxs-lookup"><span data-stu-id="4d8f7-160">Related topics</span></span>

- [<span data-ttu-id="4d8f7-161">Справочник по файлу NUSPEC</span><span class="sxs-lookup"><span data-stu-id="4d8f7-161">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="4d8f7-162">Пакеты символов</span><span class="sxs-lookup"><span data-stu-id="4d8f7-162">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="4d8f7-163">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="4d8f7-163">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="4d8f7-164">Поддержка нескольких версий платформы .NET Framework</span><span class="sxs-lookup"><span data-stu-id="4d8f7-164">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="4d8f7-165">Включение в пакет свойств и целей MSBuild</span><span class="sxs-lookup"><span data-stu-id="4d8f7-165">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="4d8f7-166">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="4d8f7-166">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
