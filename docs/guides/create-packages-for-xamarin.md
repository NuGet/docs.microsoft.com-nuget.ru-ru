---
title: Создание пакетов NuGet для Xamarin (iOS, Android и Windows) с помощью Visual Studio 2017 или 2019
description: Комплексное пошаговое руководство по созданию пакетов NuGet для Xamarin, использующих собственные API в iOS, Android и Windows.
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: 0cb653bad9e853d908039b3f7a94e1dd7eefdde5
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230906"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a><span data-ttu-id="e78df-103">Создание пакетов для Xamarin с помощью Visual Studio 2017 или 2019</span><span class="sxs-lookup"><span data-stu-id="e78df-103">Create packages for Xamarin with Visual Studio 2017 or 2019</span></span>

<span data-ttu-id="e78df-104">Пакет Xamarin содержит код, использующий собственные API в iOS, Android и Windows в зависимости от операционной системы во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="e78df-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="e78df-105">Хотя это несложно сделать, предпочтительнее позволить разработчикам использовать пакет из библиотек .NET Standard или PCL через общую контактную зону API.</span><span class="sxs-lookup"><span data-stu-id="e78df-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="e78df-106">В этом пошаговом руководстве с помощью Visual Studio 2017 или 2019 вы создадите кроссплатформенный пакет NuGet, который можно использовать в проектах для мобильных устройств в Windows, iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="e78df-106">In this walkthrough you use Visual Studio 2017 or 2019 to create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="e78df-107">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="e78df-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="e78df-108">Создание структуры проекта и кода абстракции</span><span class="sxs-lookup"><span data-stu-id="e78df-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="e78df-109">Написание кода для конкретных платформ</span><span class="sxs-lookup"><span data-stu-id="e78df-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="e78df-110">Создание и изменение файла NUSPEC</span><span class="sxs-lookup"><span data-stu-id="e78df-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="e78df-111">Упаковка компонента</span><span class="sxs-lookup"><span data-stu-id="e78df-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="e78df-112">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="e78df-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="e78df-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e78df-113">Prerequisites</span></span>

1. <span data-ttu-id="e78df-114">Visual Studio 2017 или 2019 с универсальной платформой Windows (UWP) и Xamarin.</span><span class="sxs-lookup"><span data-stu-id="e78df-114">Visual Studio 2017 or 2019 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="e78df-115">Установите бесплатный выпуск Community с сайта [visualstudio.com](https://www.visualstudio.com/). Вы также можете использовать выпуски Professional и Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e78df-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="e78df-116">Чтобы включить средства UWP и Xamarin, выберите "Выборочная установка" и задайте соответствующие параметры.</span><span class="sxs-lookup"><span data-stu-id="e78df-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="e78df-117">Интерфейс командной строки NuGet.</span><span class="sxs-lookup"><span data-stu-id="e78df-117">NuGet CLI.</span></span> <span data-ttu-id="e78df-118">Скачайте последнюю версию nuget.exe на странице [nuget.org/downloads](https://nuget.org/downloads), сохранив ее в любом месте на ваш выбор.</span><span class="sxs-lookup"><span data-stu-id="e78df-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="e78df-119">Затем добавьте это расположение в переменную среды PATH, если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="e78df-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="e78df-120">nuget.exe является программой интерфейса командной строки, а не установщиком, поэтому сохраните скачиваемый из браузера файл, но не запускайте его.</span><span class="sxs-lookup"><span data-stu-id="e78df-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="e78df-121">Создание структуры проекта и кода абстракции</span><span class="sxs-lookup"><span data-stu-id="e78df-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="e78df-122">Скачайте и запустите [расширение шаблонов кроссплатформенного подключаемого модуля .NET Standard](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e78df-122">Download and run the [Cross-Platform .NET Standard Plugin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="e78df-123">Эти шаблоны упрощают создание структуры проекта для этого пошагового руководства.</span><span class="sxs-lookup"><span data-stu-id="e78df-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="e78df-124">В Visual Studio 2017 выберите **Файл > Создать > Проект**, выполните поиск по запросу `Plugin`, выберите шаблон **Cross-Platform .NET Standard Library Plugin** (Подключаемый модуль для кроссплатформенной библиотеки .NET Standard), измените имя на LoggingLibrary и нажмите кнопку OK.</span><span class="sxs-lookup"><span data-stu-id="e78df-124">In Visual Studio 2017, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Новый проект пустого приложения (переносимое Xamarin.Forms) в Visual Studio 2017](media/CrossPlatform-NewProject.png)

    <span data-ttu-id="e78df-126">В Visual Studio 2019 выберите **Файл > Создать > Проект**, выполните поиск по запросу `Plugin`, выберите шаблон **Cross-Platform .NET Standard Library Plugin** (Подключаемый модуль для кроссплатформенной библиотеки .NET Standard) и нажмите кнопку "Далее".</span><span class="sxs-lookup"><span data-stu-id="e78df-126">In Visual Studio 2019, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, and click Next.</span></span>

    ![Новый проект пустого приложения (переносимое Xamarin.Forms) в Visual Studio 2019](media/CrossPlatform-NewProject19-Part1.png)

    <span data-ttu-id="e78df-128">Измените имя на LoggingLibrary и щелкните "Создать".</span><span class="sxs-lookup"><span data-stu-id="e78df-128">Change the name to LoggingLibrary, and click Create.</span></span>

    ![Новая конфигурация пустого приложения (переносимое Xamarin.Forms) в Visual Studio 2019](media/CrossPlatform-NewProject19-Part2.png)

<span data-ttu-id="e78df-130">Полученное решение содержит два общих проекта, а также различные проекты для конкретных платформ:</span><span class="sxs-lookup"><span data-stu-id="e78df-130">The resulting solution contains two Shared projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="e78df-131">Проект `ILoggingLibrary`, который содержится в файле `ILoggingLibrary.shared.cs`, определяет общий интерфейс (контактную зону API) компонента.</span><span class="sxs-lookup"><span data-stu-id="e78df-131">The `ILoggingLibrary` project, which is contained in the `ILoggingLibrary.shared.cs` file, defines the public interface (the API surface area) of the component.</span></span> <span data-ttu-id="e78df-132">Именно здесь вы можете определить интерфейс для библиотеки.</span><span class="sxs-lookup"><span data-stu-id="e78df-132">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="e78df-133">Другой общий проект содержит код в `CrossLoggingLibrary.shared.cs`, который будет определять реализацию абстрактного интерфейса во время выполнения для конкретной платформы.</span><span class="sxs-lookup"><span data-stu-id="e78df-133">The other Shared project contains code in `CrossLoggingLibrary.shared.cs` that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="e78df-134">В общем случае изменять этот файл не требуется.</span><span class="sxs-lookup"><span data-stu-id="e78df-134">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="e78df-135">Каждый из проектов для конкретных платформ, таких как `LoggingLibrary.android.cs`, содержит собственную реализацию интерфейса в его соответствующих файлах `LoggingLibraryImplementation.cs` (VS 2017) или `LoggingLibrary.<PLATFORM>.cs` (VS 2019).</span><span class="sxs-lookup"><span data-stu-id="e78df-135">The platform-specific projects, such as `LoggingLibrary.android.cs`, each contain a native implementation of the interface in their respective `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) files.</span></span> <span data-ttu-id="e78df-136">Именно здесь вы можете создать код библиотеки.</span><span class="sxs-lookup"><span data-stu-id="e78df-136">This is where you build out your library's code.</span></span>

<span data-ttu-id="e78df-137">По умолчанию файл ILoggingLibrary.shared.cs проекта `ILoggingLibrary` содержит определение интерфейса, но не методы.</span><span class="sxs-lookup"><span data-stu-id="e78df-137">By default, the ILoggingLibrary.shared.cs file of the `ILoggingLibrary` project contains an interface definition, but no methods.</span></span> <span data-ttu-id="e78df-138">В рамках этого пошагового руководства добавьте метод `Log` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e78df-138">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace Plugin.LoggingLibrary
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="e78df-139">Написание кода для конкретных платформ</span><span class="sxs-lookup"><span data-stu-id="e78df-139">Write your platform-specific code</span></span>

<span data-ttu-id="e78df-140">Чтобы реализовать интерфейс `ILoggingLibrary` и его методы для конкретной платформы, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="e78df-140">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="e78df-141">Откройте файл `LoggingLibraryImplementation.cs` (VS 2017) или `LoggingLibrary.<PLATFORM>.cs` (VS 2019) для проекта каждой платформы и добавьте необходимый код.</span><span class="sxs-lookup"><span data-stu-id="e78df-141">Open the `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) file of each platform project and add the necessary code.</span></span> <span data-ttu-id="e78df-142">Например (при использовании проекта платформы `Android`):</span><span class="sxs-lookup"><span data-stu-id="e78df-142">For example (using the `Android` platform project):</span></span>

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Text;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. <span data-ttu-id="e78df-143">Повторите эту реализацию в проектах для каждой платформы, которую требуется поддерживать.</span><span class="sxs-lookup"><span data-stu-id="e78df-143">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="e78df-144">Щелкните правой кнопкой мыши решение и выберите **Собрать решение**, чтобы проверить свою работу и создать артефакты, которые вы затем упакуете.</span><span class="sxs-lookup"><span data-stu-id="e78df-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="e78df-145">Если возникают ошибки об отсутствующих ссылках, щелкните решение правой кнопкой мыши, выберите **Восстановить пакеты NuGet**, чтобы установить зависимости, и повторите сборку.</span><span class="sxs-lookup"><span data-stu-id="e78df-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="e78df-146">Если вы используете Visual Studio 2019, перед тем как выбрать параметр **Восстановить пакеты NuGet** и попытаться выполнить перестроение, необходимо изменить версию `MSBuild.Sdk.Extras` на `2.0.54` в `LoggingLibrary.csproj`.</span><span class="sxs-lookup"><span data-stu-id="e78df-146">If you are using Visual Studio 2019, before selecting **Restore NuGet Packages** and trying to rebuild, you need to change the version of `MSBuild.Sdk.Extras` to `2.0.54` in `LoggingLibrary.csproj`.</span></span> <span data-ttu-id="e78df-147">Доступ к этому файлу можно получить только щелкнув правой кнопкой мыши проект (под решением) и выбрав `Unload Project`, после чего нужно щелкнуть правой кнопкой мыши выгруженный проект и выбрать `Edit LoggingLibrary.csproj`.</span><span class="sxs-lookup"><span data-stu-id="e78df-147">This file can only be accessed by first right-clicking the project (below the solution) and selecting `Unload Project`, after which you right-click on the unloaded project and select `Edit LoggingLibrary.csproj`.</span></span>

> [!Note]
> <span data-ttu-id="e78df-148">Чтобы выполнить сборку для iOS, необходим сетевой Mac, подключенный к Visual Studio, как описано в разделе [Введение в Xamarin.iOS для Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span><span class="sxs-lookup"><span data-stu-id="e78df-148">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="e78df-149">Если у вас нет доступного Mac, очистите проект iOS в диспетчере конфигураций (шаг 3 выше).</span><span class="sxs-lookup"><span data-stu-id="e78df-149">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="e78df-150">Создание и изменение файла NUSPEC</span><span class="sxs-lookup"><span data-stu-id="e78df-150">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="e78df-151">Откройте командную строку, перейдите в папку `LoggingLibrary`, находящуюся на один уровень ниже места расположения файла `.sln`, и выполните команду NuGet `spec`, чтобы создать первичный файл `Package.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="e78df-151">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="e78df-152">Переименуйте этот файл на `LoggingLibrary.nuspec` и откройте его в редакторе.</span><span class="sxs-lookup"><span data-stu-id="e78df-152">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="e78df-153">Измените содержимое файла так, как показано ниже, заменив YOUR_NAME на соответствующее значение.</span><span class="sxs-lookup"><span data-stu-id="e78df-153">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="e78df-154">Значение `<id>` должно быть уникальным в пределах nuget.org (см. соглашения об именовании, описанные в разделе [Создание пакета](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="e78df-154">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="e78df-155">Кроме того, обратите внимание на то, что необходимо изменить теги author и description, иначе на этапе упаковки произойдет ошибка.</span><span class="sxs-lookup"><span data-stu-id="e78df-155">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="e78df-156">Вы можете добавить для версии пакета суффикс `-alpha`, `-beta` или `-rc`, чтобы пометить пакет как предварительную версию. Дополнительные сведения о предварительных версиях см. в разделе [Предварительные версии](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="e78df-156">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="e78df-157">Добавление базовых сборок</span><span class="sxs-lookup"><span data-stu-id="e78df-157">Add reference assemblies</span></span>

<span data-ttu-id="e78df-158">Чтобы включить базовые сборки для конкретной платформы, добавьте следующий код в элемент `<files>` файла `LoggingLibrary.nuspec` соответствующим образом для поддерживаемых платформ:</span><span class="sxs-lookup"><span data-stu-id="e78df-158">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> <span data-ttu-id="e78df-159">Чтобы сократить имена файлов DLL и XML, щелкните правой кнопкой мыши любой заданный проект, откройте вкладку **Библиотека** и измените имена сборок.</span><span class="sxs-lookup"><span data-stu-id="e78df-159">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="e78df-160">Добавление зависимостей</span><span class="sxs-lookup"><span data-stu-id="e78df-160">Add dependencies</span></span>

<span data-ttu-id="e78df-161">При наличии конкретных зависимостей для собственных реализаций укажите их с помощью элемента `<dependencies>` с элементами `<group>`, например:</span><span class="sxs-lookup"><span data-stu-id="e78df-161">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

<span data-ttu-id="e78df-162">Например, следующий код задает iTextSharp в качестве зависимости для целевого объекта UAP:</span><span class="sxs-lookup"><span data-stu-id="e78df-162">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="e78df-163">Итоговый файл NUSPEC</span><span class="sxs-lookup"><span data-stu-id="e78df-163">Final .nuspec</span></span>

<span data-ttu-id="e78df-164">Итоговый файл `.nuspec` должен выглядеть следующим образом (YOUR_NAME, и в этом случае необходимо заменить на соответствующее значение):</span><span class="sxs-lookup"><span data-stu-id="e78df-164">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2018</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="e78df-165">Упаковка компонента</span><span class="sxs-lookup"><span data-stu-id="e78df-165">Package the component</span></span>

<span data-ttu-id="e78df-166">Когда будет готов файл `.nuspec` со ссылками на все файлы, которые необходимо включить в пакет, можно выполнить команду `pack`:</span><span class="sxs-lookup"><span data-stu-id="e78df-166">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="e78df-167">Будет создан файл `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="e78df-167">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="e78df-168">Если открыть файл в таком средстве, как [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), и развернуть все узлы, отобразится следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="e78df-168">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Пакет LoggingLibrary в обозревателе пакетов NuGet](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="e78df-170">Файл `.nupkg` — это просто ZIP-файл с другим расширением.</span><span class="sxs-lookup"><span data-stu-id="e78df-170">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="e78df-171">Поэтому чтобы просмотреть содержимое пакета, можно просто изменить расширение `.nupkg` на `.zip`, но не забудьте восстановить расширение перед отправкой пакета на сайт nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e78df-171">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="e78df-172">Чтобы предоставить доступ к пакету другим разработчикам, следуйте инструкциям в разделе [Публикация пакета](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="e78df-172">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="e78df-173">См. также</span><span class="sxs-lookup"><span data-stu-id="e78df-173">Related topics</span></span>

- [<span data-ttu-id="e78df-174">Справочник по файлу NUSPEC</span><span class="sxs-lookup"><span data-stu-id="e78df-174">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="e78df-175">Пакеты символов</span><span class="sxs-lookup"><span data-stu-id="e78df-175">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="e78df-176">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="e78df-176">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="e78df-177">Поддержка нескольких версий платформы .NET Framework</span><span class="sxs-lookup"><span data-stu-id="e78df-177">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="e78df-178">Включение в пакет свойств и целей MSBuild</span><span class="sxs-lookup"><span data-stu-id="e78df-178">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="e78df-179">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="e78df-179">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
