---
title: "Создание пакетов NuGet для платформы .NET Standard с помощью Visual Studio 2015 | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: "Полное пошаговое руководство по созданию пакетов NuGet для платформы .NET Standard с использованием NuGet 3.x и Visual Studio 2015."
keywords: "создание пакета, пакеты .NET Standard, таблица сопоставления .NET Standard"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e02888bf552997afe25e967f13e021e78e40d48d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="b8076-104">Создание пакетов .NET Standard с помощью Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="b8076-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="b8076-105">*Применяется к NuGet 3.x. Сведения о работе с NuGet 4.x и более поздних версий см. в разделе [Создание пакетов для платформы .NET Standard с помощью Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md).*</span><span class="sxs-lookup"><span data-stu-id="b8076-105">*Applies to NuGet 3.x. See [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="b8076-106">[Библиотека .NET Standard](/dotnet/articles/standard/library) представляет собой формальную спецификацию интерфейсов API .NET, которые должны быть доступны во всех средах выполнения .NET, что позволяет повысить степень унификации экосистемы .NET.</span><span class="sxs-lookup"><span data-stu-id="b8076-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="b8076-107">Библиотека .NET Standard определяет унифицированный набор API-интерфейсов библиотеки базовых классов (BCL) для реализации всеми платформами .NET независимо от рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="b8076-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="b8076-108">Таким образом, разработчики могут создавать переносимые библиотеки классов, которые могут использоваться во всех средах выполнения .NET, что позволяет свести к минимуму число директив условной компиляции, предназначенных для конкретных платформ, в общем коде либо полностью исключить их.</span><span class="sxs-lookup"><span data-stu-id="b8076-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="b8076-109">В этом руководстве приводятся пошаговые инструкции по созданию пакета nuget для библиотеки .NET Standard 1.4.</span><span class="sxs-lookup"><span data-stu-id="b8076-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="b8076-110">Этот пакет будет работать на платформах .NET Framework 4.6.1, .NET Core, Mono/Xamarin и универсальной платформе Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b8076-110">This will work across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="b8076-111">Дополнительные сведения см. в разделе [Таблица сопоставления .NET Standard](#net-standard-mapping-table) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="b8076-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

1. [<span data-ttu-id="b8076-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b8076-112">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="b8076-113">Создание проекта для библиотеки классов</span><span class="sxs-lookup"><span data-stu-id="b8076-113">Create the class library project</span></span>](#create-the-class-library-project)
1. [<span data-ttu-id="b8076-114">Создание и изменение файла NUSPEC</span><span class="sxs-lookup"><span data-stu-id="b8076-114">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="b8076-115">Упаковка компонента</span><span class="sxs-lookup"><span data-stu-id="b8076-115">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="b8076-116">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="b8076-116">Additional options</span></span>](#additional-options)
1. [<span data-ttu-id="b8076-117">Таблица сопоставления .NET Standard</span><span class="sxs-lookup"><span data-stu-id="b8076-117">.NET Standard mapping table</span></span>](#net-standard-mapping-table)
1. [<span data-ttu-id="b8076-118">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="b8076-118">Related topics</span></span>](#related-topics)


## <a name="pre-requisites"></a><span data-ttu-id="b8076-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b8076-119">Pre-requisites</span></span>

1. <span data-ttu-id="b8076-120">Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="b8076-120">Visual Studio 2015.</span></span> <span data-ttu-id="b8076-121">Установите бесплатный выпуск Community с сайта [visualstudio.com](https://www.visualstudio.com/). Вы также можете использовать выпуски Professional и Enterprise.</span><span class="sxs-lookup"><span data-stu-id="b8076-121">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span>
1. <span data-ttu-id="b8076-122">.NET Core. Установите .NET Core вместе с шаблонами и другими средствами для Visual Studio 2015 с веб-страницы [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span><span class="sxs-lookup"><span data-stu-id="b8076-122">.NET Core: Install .NET Core along with templates and other tools for Visual Studio 2015 from [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span></span>
1. <span data-ttu-id="b8076-123">Интерфейс командной строки NuGet.</span><span class="sxs-lookup"><span data-stu-id="b8076-123">NuGet CLI.</span></span> <span data-ttu-id="b8076-124">Скачайте последнюю версию nuget.exe на странице [nuget.org/downloads](https://nuget.org/downloads), сохранив ее в любом месте на ваш выбор.</span><span class="sxs-lookup"><span data-stu-id="b8076-124">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="b8076-125">Затем добавьте это расположение в переменную среды PATH, если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="b8076-125">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="b8076-126">nuget.exe является программой интерфейса командной строки, а не установщиком, поэтому сохраните скачиваемый из браузера файл, но не запускайте его.</span><span class="sxs-lookup"><span data-stu-id="b8076-126">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>



## <a name="create-the-class-library-project"></a><span data-ttu-id="b8076-127">Создание проекта для библиотеки классов</span><span class="sxs-lookup"><span data-stu-id="b8076-127">Create the class library project</span></span>

1. <span data-ttu-id="b8076-128">В Visual Studio выберите **Файл > Создать > Проект**, разверните узел **Visual C# > Windows**, выберите **Библиотека классов (переносимая)**, измените имя на "AppLogger" и нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="b8076-128">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![Создание нового проекта для библиотеки классов](media/NetStandard-NewProject.png)

1. <span data-ttu-id="b8076-130">В диалоговом окне **Добавление переносимой библиотеки классов** выберите параметры `.NET Framework 4.6` и `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="b8076-130">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>
1. <span data-ttu-id="b8076-131">Щелкните правой кнопкой мыши `AppLogger (Portable)` в обозревателе решений, выберите **Свойства**, перейдите на вкладку **Библиотека** и щелкните **Нацелить на стандартную платформу .NET** в разделе **Нацеливание**.</span><span class="sxs-lookup"><span data-stu-id="b8076-131">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="b8076-132">Появится запрос на подтверждение, после которого вы можете выбрать `.NET Standard 1.4` в раскрывающемся списке:</span><span class="sxs-lookup"><span data-stu-id="b8076-132">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![Настройка нацеливания на платформу .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="b8076-134">Перейдите на вкладку **Построение**, в разделе **Конфигурация** выберите `Release`, после чего установите флажок **XML-файл документации**.</span><span class="sxs-lookup"><span data-stu-id="b8076-134">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>
1. <span data-ttu-id="b8076-135">Добавьте собственный код для компонента, например:</span><span class="sxs-lookup"><span data-stu-id="b8076-135">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. <span data-ttu-id="b8076-136">Выполните построение проекта с использованием конфигурации выпуска и убедитесь, что файлы DLL и XML создаются в папке bin\Release.</span><span class="sxs-lookup"><span data-stu-id="b8076-136">Build the project (with the Release configuration) and check that DLL and XML files are produced within the bin\Release folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="b8076-137">Создание и изменение файла NUSPEC</span><span class="sxs-lookup"><span data-stu-id="b8076-137">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="b8076-138">Откройте командную строку, перейдите в папку, содержащую папку `AppLogg.csproj` (на один уровень ниже места расположения файла `.sln`) и выполните команду NuGet `spec`, чтобы создать первичный файл `AppLogger.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="b8076-138">Open a command prompt, navigate to the folder containing `AppLogg.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

```
nuget spec
```

1. <span data-ttu-id="b8076-139">Откройте файл `AppLogger.nuspec` в редакторе и измените его содержимое так, как показано ниже, заменив YOUR_NAME на соответствующее значение.</span><span class="sxs-lookup"><span data-stu-id="b8076-139">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="b8076-140">Значение `<id>` должно быть уникальным в пределах nuget.org (см. соглашения об именовании, описанные в разделе [Создание пакета](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="b8076-140">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="b8076-141">Кроме того, обратите внимание на то, что необходимо изменить теги authors и description, иначе на этапе упаковки произойдет ошибка.</span><span class="sxs-lookup"><span data-stu-id="b8076-141">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>AppLogger.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>AppLogger</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. <span data-ttu-id="b8076-142">Добавьте файл базовой сборки `.nuspec`, а именно DLL-файл библиотеки и XML-файл IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="b8076-142">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="b8076-143">Щелкните решение правой кнопкой мыши и выберите **Построить решение**, чтобы создать все файлы пакета.</span><span class="sxs-lookup"><span data-stu-id="b8076-143">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="b8076-144">Упаковка компонента</span><span class="sxs-lookup"><span data-stu-id="b8076-144">Package the component</span></span>

<span data-ttu-id="b8076-145">Когда будет готов файл `.nuspec` со ссылками на все файлы, которые необходимо включить в пакет, можно выполнить команду `pack`:</span><span class="sxs-lookup"><span data-stu-id="b8076-145">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack AppLogger.nuspec
```

<span data-ttu-id="b8076-146">Будет создан файл `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="b8076-146">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="b8076-147">Если открыть файл в таком средстве, как [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), и развернуть все узлы, вы увидите следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="b8076-147">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![Пакет AppLogger в обозревателе пакетов NuGet](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="b8076-149">Файл `.nupkg` — это просто ZIP-файл с другим расширением.</span><span class="sxs-lookup"><span data-stu-id="b8076-149">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="b8076-150">Поэтому чтобы просмотреть содержимое пакета, можно просто изменить расширение `.nupkg` на `.zip`, но не забудьте восстановить расширение перед отправкой пакета на сайт nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b8076-150">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="b8076-151">Чтобы предоставить доступ к пакету другим разработчикам, следуйте инструкциям в разделе [Публикация пакета](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="b8076-151">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="b8076-152">Обратите внимание, что команда `pack` требует наличия Mono 4.4.2 в Mac OS X и не работает в системах Linux.</span><span class="sxs-lookup"><span data-stu-id="b8076-152">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="b8076-153">На компьютерах Mac также необходимо преобразовать пути в формате Windows, указанные в файле `.nuspec`, в формат Unix.</span><span class="sxs-lookup"><span data-stu-id="b8076-153">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="additional-options"></a><span data-ttu-id="b8076-154">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="b8076-154">Additional options</span></span>

<span data-ttu-id="b8076-155">В следующих разделах описываются дополнительные возможности, доступные при создании пакета NuGet:</span><span class="sxs-lookup"><span data-stu-id="b8076-155">The following sections go into additional options for NuGet package creation:</span></span>

- [<span data-ttu-id="b8076-156">Объявление зависимостей</span><span class="sxs-lookup"><span data-stu-id="b8076-156">Declaring dependencies</span></span>](#declaring-dependencies)
- [<span data-ttu-id="b8076-157">Поддержка нескольких целевых платформ</span><span class="sxs-lookup"><span data-stu-id="b8076-157">Supporting multiple target frameworks</span></span>](#supporting-multiple-target-frameworks)
- [<span data-ttu-id="b8076-158">Добавление целевых объектов и свойств MSBuild</span><span class="sxs-lookup"><span data-stu-id="b8076-158">Adding targets and props for MSBuild</span></span>](#adding-targets-and-props-for-msbuild)
- [<span data-ttu-id="b8076-159">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="b8076-159">Creating localized packages</span></span>](#creating-localized-packages)
- [<span data-ttu-id="b8076-160">Добавление файла сведений</span><span class="sxs-lookup"><span data-stu-id="b8076-160">Adding a readme</span></span>](#adding-a-readme)

### <a name="declaring-dependencies"></a><span data-ttu-id="b8076-161">Объявление зависимостей</span><span class="sxs-lookup"><span data-stu-id="b8076-161">Declaring dependencies</span></span>

<span data-ttu-id="b8076-162">Если вы используете зависимости от других пакетов NuGet, их следует перечислить в элементе `<dependencies>` с элементами `<group>`.</span><span class="sxs-lookup"><span data-stu-id="b8076-162">If you have any dependencies on other NuGet packages, list those in the `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="b8076-163">Например, чтобы объявить зависимость от NewtonSoft.Json 8.0.3 или более поздней версии, добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="b8076-163">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="b8076-164">Синтаксис атрибута *version* в этом случае указывает, что приемлемыми являются версия 8.0.3 или более поздние.</span><span class="sxs-lookup"><span data-stu-id="b8076-164">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="b8076-165">Инструкции по указанию других диапазонов версий см. в разделе [Управление версиями пакета](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b8076-165">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="supporting-multiple-target-frameworks"></a><span data-ttu-id="b8076-166">Поддержка нескольких целевых платформ</span><span class="sxs-lookup"><span data-stu-id="b8076-166">Supporting multiple target frameworks</span></span>

<span data-ttu-id="b8076-167">Предположим, вам необходимо использовать преимущество API платформы .NET Framework 4.6.2, которое недоступно на платформе .NET Standard 1.4.</span><span class="sxs-lookup"><span data-stu-id="b8076-167">Suppose you'd like to take advantage of an API in .NET Framework 4.6.2 that is not available in .NET Standard 1.4.</span></span> <span data-ttu-id="b8076-168">Для этого сначала необходимо обеспечить компиляцию библиотеки для .NET 4.6.2 с использованием условной компиляции или общих проектов.</span><span class="sxs-lookup"><span data-stu-id="b8076-168">To do this, you'll first need to make sure the library compiles for .NET 4.6.2 by using conditional compilation or shared projects.</span></span> <span data-ttu-id="b8076-169">(В Visual Studio вы можете создать проект NetCore, добавить нужную платформу в раздел управления несколькими платформами, после чего выполнить построение.) Затем следует создать пакет, используя простую методику с применением рабочего каталога на основе соглашения, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="b8076-169">(In Visual Studio, you can create a NetCore project, add the framework of choice to the multiple framework section, and then build.) Then you create the package using the simple convention-based working directory technique as follows:</span></span>

1. <span data-ttu-id="b8076-170">В корневой папке проекта, содержащей файл `.nuspec`, создайте папку с именем `lib`.</span><span class="sxs-lookup"><span data-stu-id="b8076-170">In the project's root folder containing your `.nuspec` file, create a folder named `lib`.</span></span>
1. <span data-ttu-id="b8076-171">В папке `lib` создайте папку для каждой платформы, поддержку которой требуется реализовать:</span><span class="sxs-lookup"><span data-stu-id="b8076-171">Inside `lib`, create folders for each platform you want to support:</span></span>

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. <span data-ttu-id="b8076-172">В файл `.nuspec` добавьте узел `files` под узлом `package` и задайте ссылки на файлы в папке `lib`, используя подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="b8076-172">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `lib` using wildcards.</span></span> <span data-ttu-id="b8076-173">**Примечание**. В методике с применением рабочего каталога на основе соглашения не поддерживаются замены маркеров, поэтому необходимо заменить их литеральными значениями:</span><span class="sxs-lookup"><span data-stu-id="b8076-173">**Note:** Token replacements are not supported with the convention-based working directory approach, so replace them with literal values:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="b8076-174">Создайте пакет снова, используя `nuget pack AppLogger.spec`.</span><span class="sxs-lookup"><span data-stu-id="b8076-174">Create the package again using `nuget pack AppLogger.spec`.</span></span>

<span data-ttu-id="b8076-175">Дополнительные сведения об использовании этого метода см. в разделе [Поддержка нескольких версий платформы .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)</span><span class="sxs-lookup"><span data-stu-id="b8076-175">For more details on using this technique, see [Supporting Multiple .NET Framework Versions](../create-packages/supporting-multiple-target-frameworks.md)</span></span>

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="b8076-176">Добавление целевых объектов и свойств MSBuild</span><span class="sxs-lookup"><span data-stu-id="b8076-176">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="b8076-177">В некоторых случаях в проекты, использующие пакет, необходимо добавить пользовательские целевые объекты сборки или свойства, например, если во время сборки должно запускаться пользовательское средство или процесс.</span><span class="sxs-lookup"><span data-stu-id="b8076-177">In some cases you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="b8076-178">Это можно сделать, добавив файлы в папку `\build`, как описывается ниже.</span><span class="sxs-lookup"><span data-stu-id="b8076-178">You do this by adding files in a `\build` folder as described in the steps below.</span></span> <span data-ttu-id="b8076-179">Когда диспетчер NuGet устанавливает пакет с файлами \build, он добавляет в файл проекта элемент MSBuild, указывающий на файлы с расширениями .targets и .props.</span><span class="sxs-lookup"><span data-stu-id="b8076-179">When NuGet installs a package with \build files, it adds an MSBuild element in the project file pointing to the .targets and .props files.</span></span>

> [!Note]
> <span data-ttu-id="b8076-180">При использовании `project.json` целевые платформы не добавляются в проект, а предоставляются через файл `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="b8076-180">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>


1. <span data-ttu-id="b8076-181">В папке проекта, содержащей файл `.nuspec`, создайте папку с именем `build`.</span><span class="sxs-lookup"><span data-stu-id="b8076-181">In the project folder containing the your `.nuspec` file, create a folder named `build`.</span></span>
1. <span data-ttu-id="b8076-182">В папке `build` создайте папки для каждой поддерживаемой платформы и поместите в них файлы `.targets` и `.props`:</span><span class="sxs-lookup"><span data-stu-id="b8076-182">Inside `build`, create folders for each supported, and within those place your `.targets` and `.props` files:</span></span>

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. <span data-ttu-id="b8076-183">В файл `.nuspec` добавьте узел `files` под узлом `package` и задайте ссылки на файлы в папке `build`, используя подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="b8076-183">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `build` using wildcards.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. <span data-ttu-id="b8076-184">Создайте пакет снова, используя `nuget pack AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="b8076-184">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>

<span data-ttu-id="b8076-185">Дополнительные сведения см. в разделе [Включение в пакет свойств и целей MSBuild](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="b8076-185">For additional details, refer to [Include MSBuild props and targets in a package](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span></span>


### <a name="creating-localized-packages"></a><span data-ttu-id="b8076-186">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="b8076-186">Creating localized packages</span></span>

<span data-ttu-id="b8076-187">Для создания локализованных версий библиотеки можно создать отдельные пакеты для каждого языкового стандарта или включить локализованные сборки ресурсов в один пакет.</span><span class="sxs-lookup"><span data-stu-id="b8076-187">To create localized versions of your library, you can either create separate packages for different locales, or include localized resource assemblies within a single package.</span></span> <span data-ttu-id="b8076-188">Далее показана реализация второго подхода для немецкого и итальянского языков:</span><span class="sxs-lookup"><span data-stu-id="b8076-188">Here's how to do the latter approach for German and Italian:</span></span>

1. <span data-ttu-id="b8076-189">В папке каждой целевой платформы в папке `lib` создайте папки для каждого поддерживаемого языка (кроме английского).</span><span class="sxs-lookup"><span data-stu-id="b8076-189">Within each target framework folder under `lib`, create folders for each supported language other than the English default.</span></span> <span data-ttu-id="b8076-190">В эти папки можно поместить сборки ресурсов и локализованные XML-файлы IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="b8076-190">In these folders you can place resource assemblies  and localized IntelliSense XML files.</span></span> <span data-ttu-id="b8076-191">Пример:</span><span class="sxs-lookup"><span data-stu-id="b8076-191">For example:</span></span>

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. <span data-ttu-id="b8076-192">В файл `.nuspec` добавьте ссылки на эти файлы в узел `<files>`:</span><span class="sxs-lookup"><span data-stu-id="b8076-192">In the `.nuspec` file, reference these files in the `<files>` node:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="b8076-193">Создайте пакет снова, используя `nuget pack AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="b8076-193">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>


### <a name="adding-a-readme"></a><span data-ttu-id="b8076-194">Добавление файла сведений</span><span class="sxs-lookup"><span data-stu-id="b8076-194">Adding a readme</span></span>

<span data-ttu-id="b8076-195">Если включить файл `readme.txt` в корень пакета, Visual Studio будет отображать его при непосредственной установке пакета.</span><span class="sxs-lookup"><span data-stu-id="b8076-195">When you include a `readme.txt` file in the root of the package, Visual Studio will display it when the package is installed directly.</span></span>

> [!Note]
> <span data-ttu-id="b8076-196">Файлы сведений не отображаются для пакетов, которые устанавливаются в качестве зависимостей, или для проектов .NET Core.</span><span class="sxs-lookup"><span data-stu-id="b8076-196">Readme files are not shown for packages that are installed as a dependency, or for .NET Core projects.</span></span>


<span data-ttu-id="b8076-197">Чтобы сделать это, создайте файл `readme.txt`, поместите его в корневую папку проекта и задайте ссылку на него в файле `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="b8076-197">To do this, create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```


## <a name="net-standard-mapping-table"></a><span data-ttu-id="b8076-198">Таблица сопоставления .NET Standard</span><span class="sxs-lookup"><span data-stu-id="b8076-198">.NET Standard mapping table</span></span>

|<span data-ttu-id="b8076-199">Имя платформы</span><span class="sxs-lookup"><span data-stu-id="b8076-199">Platform Name</span></span> |<span data-ttu-id="b8076-200">Alias</span><span class="sxs-lookup"><span data-stu-id="b8076-200">Alias</span></span>|
|--------------|-----|
|<span data-ttu-id="b8076-201">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="b8076-201">.NET Standard</span></span> | <span data-ttu-id="b8076-202">netstandard</span><span class="sxs-lookup"><span data-stu-id="b8076-202">netstandard</span></span>| <span data-ttu-id="b8076-203">1.0</span><span class="sxs-lookup"><span data-stu-id="b8076-203">1.0</span></span>| <span data-ttu-id="b8076-204">1.1</span><span class="sxs-lookup"><span data-stu-id="b8076-204">1.1</span></span>| <span data-ttu-id="b8076-205">1.2</span><span class="sxs-lookup"><span data-stu-id="b8076-205">1.2</span></span>| <span data-ttu-id="b8076-206">1.3</span><span class="sxs-lookup"><span data-stu-id="b8076-206">1.3</span></span>| <span data-ttu-id="b8076-207">1.4</span><span class="sxs-lookup"><span data-stu-id="b8076-207">1.4</span></span>| <span data-ttu-id="b8076-208">1.5</span><span class="sxs-lookup"><span data-stu-id="b8076-208">1.5</span></span>| <span data-ttu-id="b8076-209">1.6</span><span class="sxs-lookup"><span data-stu-id="b8076-209">1.6</span></span>|
|<span data-ttu-id="b8076-210">.NET Core</span><span class="sxs-lookup"><span data-stu-id="b8076-210">.NET Core</span></span> | <span data-ttu-id="b8076-211">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="b8076-211">netcoreapp</span></span>| <span data-ttu-id="b8076-212">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-212">&#x2192;</span></span>| <span data-ttu-id="b8076-213">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-213">&#x2192;</span></span>| <span data-ttu-id="b8076-214">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-214">&#x2192;</span></span>| <span data-ttu-id="b8076-215">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-215">&#x2192;</span></span>| <span data-ttu-id="b8076-216">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-216">&#x2192;</span></span>| <span data-ttu-id="b8076-217">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-217">&#x2192;</span></span>| <span data-ttu-id="b8076-218">1.0</span><span class="sxs-lookup"><span data-stu-id="b8076-218">1.0</span></span>|
|<span data-ttu-id="b8076-219">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="b8076-219">.NET Framework</span></span>| <span data-ttu-id="b8076-220">net</span><span class="sxs-lookup"><span data-stu-id="b8076-220">net</span></span>| <span data-ttu-id="b8076-221">4.5</span><span class="sxs-lookup"><span data-stu-id="b8076-221">4.5</span></span>| <span data-ttu-id="b8076-222">4.5.1</span><span class="sxs-lookup"><span data-stu-id="b8076-222">4.5.1</span></span>| <span data-ttu-id="b8076-223">4.6</span><span class="sxs-lookup"><span data-stu-id="b8076-223">4.6</span></span>| <span data-ttu-id="b8076-224">4.6.1</span><span class="sxs-lookup"><span data-stu-id="b8076-224">4.6.1</span></span>| <span data-ttu-id="b8076-225">4.6.2</span><span class="sxs-lookup"><span data-stu-id="b8076-225">4.6.2</span></span>| <span data-ttu-id="b8076-226">4.6.3</span><span class="sxs-lookup"><span data-stu-id="b8076-226">4.6.3</span></span>|
|<span data-ttu-id="b8076-227">Платформы Mono и Xamarin</span><span class="sxs-lookup"><span data-stu-id="b8076-227">Mono/Xamarin Platforms</span></span>| <span data-ttu-id="b8076-228">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-228">&#x2192;</span></span>| <span data-ttu-id="b8076-229">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-229">&#x2192;</span></span>| <span data-ttu-id="b8076-230">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-230">&#x2192;</span></span>| <span data-ttu-id="b8076-231">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-231">&#x2192;</span></span>| <span data-ttu-id="b8076-232">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-232">&#x2192;</span></span>| <span data-ttu-id="b8076-233">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-233">&#x2192;</span></span>|
|<span data-ttu-id="b8076-234">Универсальная платформа Windows </span><span class="sxs-lookup"><span data-stu-id="b8076-234">Universal Windows Platform</span></span>| <span data-ttu-id="b8076-235">uap</span><span class="sxs-lookup"><span data-stu-id="b8076-235">uap</span></span>| <span data-ttu-id="b8076-236">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-236">&#x2192;</span></span>| <span data-ttu-id="b8076-237">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-237">&#x2192;</span></span>| <span data-ttu-id="b8076-238">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-238">&#x2192;</span></span>| <span data-ttu-id="b8076-239">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-239">&#x2192;</span></span>|<span data-ttu-id="b8076-240">10.0</span><span class="sxs-lookup"><span data-stu-id="b8076-240">10.0</span></span>|
|<span data-ttu-id="b8076-241">Windows</span><span class="sxs-lookup"><span data-stu-id="b8076-241">Windows</span></span>| <span data-ttu-id="b8076-242">win</span><span class="sxs-lookup"><span data-stu-id="b8076-242">win</span></span>| <span data-ttu-id="b8076-243">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-243">&#x2192;</span></span>| <span data-ttu-id="b8076-244">8.0</span><span class="sxs-lookup"><span data-stu-id="b8076-244">8.0</span></span>| <span data-ttu-id="b8076-245">8.1</span><span class="sxs-lookup"><span data-stu-id="b8076-245">8.1</span></span>|
|<span data-ttu-id="b8076-246">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="b8076-246">Windows Phone</span></span>| <span data-ttu-id="b8076-247">wpa</span><span class="sxs-lookup"><span data-stu-id="b8076-247">wpa</span></span>| <span data-ttu-id="b8076-248">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-248">&#x2192;</span></span>| <span data-ttu-id="b8076-249">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="b8076-249">&#x2192;</span></span>|<span data-ttu-id="b8076-250">8.1</span><span class="sxs-lookup"><span data-stu-id="b8076-250">8.1</span></span>|
|<span data-ttu-id="b8076-251">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="b8076-251">Windows Phone Silverlight</span></span>| <span data-ttu-id="b8076-252">wp</span><span class="sxs-lookup"><span data-stu-id="b8076-252">wp</span></span>| <span data-ttu-id="b8076-253">8.0</span><span class="sxs-lookup"><span data-stu-id="b8076-253">8.0</span></span>|



## <a name="related-topics"></a><span data-ttu-id="b8076-254">См. также</span><span class="sxs-lookup"><span data-stu-id="b8076-254">Related topics</span></span>

- [<span data-ttu-id="b8076-255">Справочник по файлу NUSPEC</span><span class="sxs-lookup"><span data-stu-id="b8076-255">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="b8076-256">Пакеты символов</span><span class="sxs-lookup"><span data-stu-id="b8076-256">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="b8076-257">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="b8076-257">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="b8076-258">Поддержка нескольких версий платформы .NET Framework</span><span class="sxs-lookup"><span data-stu-id="b8076-258">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="b8076-259">Включение в пакет свойств и целей MSBuild</span><span class="sxs-lookup"><span data-stu-id="b8076-259">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="b8076-260">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="b8076-260">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="b8076-261">Документация по библиотеке .NET Standard</span><span class="sxs-lookup"><span data-stu-id="b8076-261">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="b8076-262">Перенос кода в .NET Core из .NET Framework</span><span class="sxs-lookup"><span data-stu-id="b8076-262">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
