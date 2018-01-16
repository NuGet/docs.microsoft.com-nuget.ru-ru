---
title: "Создание кроссплатформенных пакетов NuGet (для iOS, Android и Windows) | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: ae24824b-a138-4d12-a810-1f653ddffd32
description: "Комплексное пошаговое руководство по созданию пакетов NuGet для Xamarin, использующих собственные API в iOS, Android и Windows."
keywords: "создание пакета, пакеты для Xamarin, кроссплатформенные пакеты"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f372856232f151efcf972881cffbe7d4bb7ed6ee
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="create-cross-platform-packages"></a><span data-ttu-id="695de-104">Создание кроссплатформенных пакетов</span><span class="sxs-lookup"><span data-stu-id="695de-104">Create cross-platform packages</span></span>

<span data-ttu-id="695de-105">Кроссплатформенный пакет содержит код, использующий собственные API в iOS, Android и Windows в зависимости от операционной системы во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="695de-105">A cross-platform package contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="695de-106">Хотя это несложно сделать, предпочтительнее позволить разработчикам использовать пакет из библиотек .NET Standard или PCL через общую контактную зону API.</span><span class="sxs-lookup"><span data-stu-id="695de-106">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="695de-107">В этом пошаговом руководстве вы создадите кроссплатформенный пакет NuGet, который можно использовать в проектах для мобильных устройств в Windows, iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="695de-107">In this walkthrough you'll create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="695de-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="695de-108">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="695de-109">Создание структуры проекта и кода абстракции</span><span class="sxs-lookup"><span data-stu-id="695de-109">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="695de-110">Написание кода для конкретных платформ</span><span class="sxs-lookup"><span data-stu-id="695de-110">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="695de-111">Создание и изменение файла NUSPEC</span><span class="sxs-lookup"><span data-stu-id="695de-111">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="695de-112">Упаковка компонента</span><span class="sxs-lookup"><span data-stu-id="695de-112">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="695de-113">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="695de-113">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="695de-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="695de-114">Pre-requisites</span></span>

1. <span data-ttu-id="695de-115">Visual Studio 2015 с универсальной платформой Windows (UWP) и Xamarin.</span><span class="sxs-lookup"><span data-stu-id="695de-115">Visual Studio 2015 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="695de-116">Установите бесплатный выпуск Community с сайта [visualstudio.com](https://www.visualstudio.com/). Вы также можете использовать выпуски Professional и Enterprise.</span><span class="sxs-lookup"><span data-stu-id="695de-116">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="695de-117">Чтобы включить средства UWP и Xamarin, выберите "Выборочная установка" и задайте соответствующие параметры.</span><span class="sxs-lookup"><span data-stu-id="695de-117">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="695de-118">Интерфейс командной строки NuGet.</span><span class="sxs-lookup"><span data-stu-id="695de-118">NuGet CLI.</span></span> <span data-ttu-id="695de-119">Скачайте последнюю версию nuget.exe на странице [nuget.org/downloads](https://nuget.org/downloads), сохранив ее в любом месте на ваш выбор.</span><span class="sxs-lookup"><span data-stu-id="695de-119">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="695de-120">Затем добавьте это расположение в переменную среды PATH, если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="695de-120">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="695de-121">nuget.exe является программой интерфейса командной строки, а не установщиком, поэтому сохраните скачиваемый из браузера файл, но не запускайте его.</span><span class="sxs-lookup"><span data-stu-id="695de-121">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>


## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="695de-122">Создание структуры проекта и кода абстракции</span><span class="sxs-lookup"><span data-stu-id="695de-122">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="695de-123">Скачайте и запустите [расширение шаблонов подключаемого модуля для Xamarin](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="695de-123">Download and run the [Plugin for Xamarin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="695de-124">Эти шаблоны упрощают создание структуры проекта для этого пошагового руководства.</span><span class="sxs-lookup"><span data-stu-id="695de-124">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="695de-125">В Visual Studio выберите **Файл > Создать > Проект**, выполните поиск `Plugin`, выберите шаблон **Plugin for Xamarin** (Подключаемый модуль для Xamarin), измените имя на LoggingLibrary и нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="695de-125">In Visual Studio, **File > New > Project**, search for `Plugin`, select the **Plugin for Xamarin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Новый проект пустого приложения (переносимое Xamarin.Forms) в Visual Studio](media/CrossPlatform-NewProject.png)

<span data-ttu-id="695de-127">Полученное решение содержит два проекта PCL, а также различные проекты для конкретных платформ:</span><span class="sxs-lookup"><span data-stu-id="695de-127">The resulting solution contains two PCL projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="695de-128">PCL с именем `Plugin.LoggingLibrary.Abstractions (Portable)` определяет общий интерфейс (контактную зону API) компонента, в данном случае — интерфейс `ILoggingLibrary`, содержащийся в файле ILoggingLibrary.cs.</span><span class="sxs-lookup"><span data-stu-id="695de-128">The PCL named `Plugin.LoggingLibrary.Abstractions (Portable)`, defines the public interface (the API surface area) of the component, in this case the `ILoggingLibrary` interface contained in the ILoggingLibrary.cs file.</span></span> <span data-ttu-id="695de-129">Именно здесь вы определите интерфейс для библиотеки.</span><span class="sxs-lookup"><span data-stu-id="695de-129">This is where you'll define the interface to your library.</span></span>
- <span data-ttu-id="695de-130">Другой PCL `Plugin.LoggingLibrary (Portable)` содержит код в CrossLoggingLibrary.cs, который будет искать реализацию абстрактного интерфейса во время выполнения для конкретной платформы.</span><span class="sxs-lookup"><span data-stu-id="695de-130">The other PCL, `Plugin.LoggingLibrary (Portable)`, contains code in CrossLoggingLibrary.cs that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="695de-131">В общем случае изменять этот файл не требуется.</span><span class="sxs-lookup"><span data-stu-id="695de-131">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="695de-132">Каждый из проектов для конкретных платформ, таких как `Plugin.LoggingLibrary.Android`, содержит собственную реализацию интерфейса в его соответствующем файле LoggingLibraryImplementation.cs.</span><span class="sxs-lookup"><span data-stu-id="695de-132">The platform-specific projects, such as `Plugin.LoggingLibrary.Android`, each contain contain a native implementation of the interface in their respective LoggingLibraryImplementation.cs files.</span></span> <span data-ttu-id="695de-133">Именно здесь вы создадите код библиотеки.</span><span class="sxs-lookup"><span data-stu-id="695de-133">This is where you'll build out your library's code.</span></span>

<span data-ttu-id="695de-134">По умолчанию файл ILoggingLibrary.cs проекта Abstractions содержит определение интерфейса, но не методы.</span><span class="sxs-lookup"><span data-stu-id="695de-134">By default, the ILoggingLibrary.cs file of the Abstractions project contains an interface definition, but no methods.</span></span> <span data-ttu-id="695de-135">В рамках этого пошагового руководства добавьте метод `Log` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="695de-135">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="695de-136">Написание кода для конкретных платформ</span><span class="sxs-lookup"><span data-stu-id="695de-136">Write your platform-specific code</span></span>

<span data-ttu-id="695de-137">Чтобы реализовать интерфейс `ILoggingLibrary` и его методы для конкретной платформы, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="695de-137">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="695de-138">Откройте файл `LoggingLibraryImplementation.cs` для проекта каждой платформы и добавьте необходимый код.</span><span class="sxs-lookup"><span data-stu-id="695de-138">Open the `LoggingLibraryImplementation.cs` file of each platform project and add the necessary code.</span></span> <span data-ttu-id="695de-139">Например (при использовании проекта `Plugin.LoggingLibrary.Android`):</span><span class="sxs-lookup"><span data-stu-id="695de-139">For example (using the `Plugin.LoggingLibrary.Android` project):</span></span>

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

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

1. <span data-ttu-id="695de-140">Повторите эту реализацию в проектах для каждой платформы, которую требуется поддерживать.</span><span class="sxs-lookup"><span data-stu-id="695de-140">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="695de-141">Щелкните правой кнопкой мыши проект iOS, выберите пункт **Свойства**, откройте вкладку **Сборка** и удалите "\iPhone" из параметров **Выходной путь** и **Файл XML-документации**.</span><span class="sxs-lookup"><span data-stu-id="695de-141">Right-click the iOS project, select **Properties**, click the **Build** tab, and remove "\iPhone" from the **Output path** and **XML documentation file** settings.</span></span> <span data-ttu-id="695de-142">Это необходимо лишь для более удобного выполнения последующих действий в данном пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="695de-142">This is just for later convenience in this walkthrough.</span></span> <span data-ttu-id="695de-143">Когда все будет готово, сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="695de-143">Save the file when done.</span></span>
1. <span data-ttu-id="695de-144">Щелкните правой кнопкой мыши решение, выберите **Диспетчер конфигураций...** и установите флажки **Сборка** для PCL и каждой поддерживаемой платформы.</span><span class="sxs-lookup"><span data-stu-id="695de-144">Right-click the solution, select **Configuration Manager...**, and check the **Build** boxes for the PCLs and each platform you're supporting.</span></span>
1. <span data-ttu-id="695de-145">Щелкните правой кнопкой мыши решение и выберите **Собрать решение**, чтобы проверить свою работу и создать артефакты, которые вы затем упакуете.</span><span class="sxs-lookup"><span data-stu-id="695de-145">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you'll package next.</span></span> <span data-ttu-id="695de-146">Если возникают ошибки об отсутствующих ссылках, щелкните решение правой кнопкой мыши, выберите **Восстановить пакеты NuGet**, чтобы установить зависимости, и повторите сборку.</span><span class="sxs-lookup"><span data-stu-id="695de-146">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="695de-147">Чтобы выполнить сборку для iOS, необходим сетевой Mac, подключенный к Visual Studio, как описано в разделе [Введение в Xamarin.iOS для Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span><span class="sxs-lookup"><span data-stu-id="695de-147">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="695de-148">Если у вас нет доступного Mac, очистите проект iOS в диспетчере конфигураций (шаг 3 выше).</span><span class="sxs-lookup"><span data-stu-id="695de-148">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>


## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="695de-149">Создание и изменение файла NUSPEC</span><span class="sxs-lookup"><span data-stu-id="695de-149">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="695de-150">Откройте командную строку, перейдите в папку `LoggingLibrary`, находящуюся на один уровень ниже места расположения файла `.sln`, и выполните команду NuGet `spec`, чтобы создать первичный файл `Package.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="695de-150">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

```
nuget spec
```

1. <span data-ttu-id="695de-151">Переименуйте этот файл на `LoggingLibrary.nuspec` и откройте его в редакторе.</span><span class="sxs-lookup"><span data-stu-id="695de-151">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="695de-152">Измените содержимое файла так, как показано ниже, заменив YOUR_NAME на соответствующее значение.</span><span class="sxs-lookup"><span data-stu-id="695de-152">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="695de-153">Значение `<id>` должно быть уникальным в пределах nuget.org (см. соглашения об именовании, описанные в разделе [Создание пакета](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="695de-153">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="695de-154">Кроме того, обратите внимание на то, что необходимо изменить теги authors и description, иначе на этапе упаковки произойдет ошибка.</span><span class="sxs-lookup"><span data-stu-id="695de-154">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

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
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```
    
> [!Tip]
> <span data-ttu-id="695de-155">Вы можете добавить для версии пакета суффикс `-alpha`, `-beta` или `-rc`, чтобы пометить пакет как предварительную версию. Дополнительные сведения о предварительных версиях см. в разделе [Предварительные версии](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="695de-155">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="695de-156">Добавление базовых сборок</span><span class="sxs-lookup"><span data-stu-id="695de-156">Add reference assemblies</span></span>

<span data-ttu-id="695de-157">Чтобы включить базовые сборки для конкретной платформы, добавьте следующий код в элемент `<files>` файла `LoggingLibrary.nuspec` соответствующим образом для поддерживаемых платформ:</span><span class="sxs-lookup"><span data-stu-id="695de-157">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="695de-158">Чтобы сократить имена файлов DLL и XML, щелкните правой кнопкой мыши любой заданный проект, откройте вкладку **Библиотека** и измените имена сборок.</span><span class="sxs-lookup"><span data-stu-id="695de-158">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>


### <a name="add-dependencies"></a><span data-ttu-id="695de-159">Добавление зависимостей</span><span class="sxs-lookup"><span data-stu-id="695de-159">Add dependencies</span></span>

<span data-ttu-id="695de-160">При наличии конкретных зависимостей для собственных реализаций укажите их с помощью элемента `<dependencies>` с элементами `<group>`, например:</span><span class="sxs-lookup"><span data-stu-id="695de-160">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="695de-161">Например, следующий код задает iTextSharp в качестве зависимости для целевого объекта UAP:</span><span class="sxs-lookup"><span data-stu-id="695de-161">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="695de-162">Итоговый файл NUSPEC</span><span class="sxs-lookup"><span data-stu-id="695de-162">Final .nuspec</span></span>

<span data-ttu-id="695de-163">Итоговый файл `.nuspec` должен выглядеть следующим образом (YOUR_NAME, и в этом случае необходимо заменить на соответствующее значение):</span><span class="sxs-lookup"><span data-stu-id="695de-163">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2016</copyright>
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

## <a name="package-the-component"></a><span data-ttu-id="695de-164">Упаковка компонента</span><span class="sxs-lookup"><span data-stu-id="695de-164">Package the component</span></span>

<span data-ttu-id="695de-165">Когда будет готов файл `.nuspec` со ссылками на все файлы, которые необходимо включить в пакет, можно выполнить команду `pack`:</span><span class="sxs-lookup"><span data-stu-id="695de-165">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="695de-166">Будет создан файл `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="695de-166">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="695de-167">Если открыть файл в таком средстве, как [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), и развернуть все узлы, вы увидите следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="695de-167">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![Пакет LoggingLibrary в обозревателе пакетов NuGet](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="695de-169">Файл `.nupkg` — это просто ZIP-файл с другим расширением.</span><span class="sxs-lookup"><span data-stu-id="695de-169">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="695de-170">Поэтому чтобы просмотреть содержимое пакета, можно просто изменить расширение `.nupkg` на `.zip`, но не забудьте восстановить расширение перед отправкой пакета на сайт nuget.org.</span><span class="sxs-lookup"><span data-stu-id="695de-170">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>


<span data-ttu-id="695de-171">Чтобы предоставить доступ к пакету другим разработчикам, следуйте инструкциям в разделе [Публикация пакета](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="695de-171">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="695de-172">См. также</span><span class="sxs-lookup"><span data-stu-id="695de-172">Related topics</span></span>

- [<span data-ttu-id="695de-173">Справочник по файлу NUSPEC</span><span class="sxs-lookup"><span data-stu-id="695de-173">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="695de-174">Пакеты символов</span><span class="sxs-lookup"><span data-stu-id="695de-174">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="695de-175">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="695de-175">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="695de-176">Поддержка нескольких версий платформы .NET Framework</span><span class="sxs-lookup"><span data-stu-id="695de-176">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="695de-177">Включение в пакет свойств и целевых объектов MSBuild</span><span class="sxs-lookup"><span data-stu-id="695de-177">Including MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="695de-178">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="695de-178">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)