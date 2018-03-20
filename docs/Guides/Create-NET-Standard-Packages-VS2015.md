---
title: "Создание пакетов NuGet для платформы .NET Standard с помощью Visual Studio 2015 | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Полное пошаговое руководство по созданию пакетов NuGet для платформы .NET Standard с использованием NuGet 3.x и Visual Studio 2015."
keywords: "создание пакета, пакеты .NET Standard, таблица сопоставления .NET Standard"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: abf6a56cbc84bdd066e31e77c7883825a8456144
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="7fa71-104">Создание пакетов .NET Standard с помощью Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="7fa71-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="7fa71-105">*Применяется к NuGet 3.x. Сведения о работе с NuGet 4.x и более поздних версий см. в разделе [Создание и публикация пакета с помощью Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md).*</span><span class="sxs-lookup"><span data-stu-id="7fa71-105">*Applies to NuGet 3.x. See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="7fa71-106">[Библиотека .NET Standard](/dotnet/articles/standard/library) представляет собой формальную спецификацию интерфейсов API .NET, которые должны быть доступны во всех средах выполнения .NET, что позволяет повысить степень унификации экосистемы .NET.</span><span class="sxs-lookup"><span data-stu-id="7fa71-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="7fa71-107">Библиотека .NET Standard определяет унифицированный набор API-интерфейсов библиотеки базовых классов (BCL) для реализации всеми платформами .NET независимо от рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="7fa71-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="7fa71-108">Это позволяет разработчикам создавать код, который можно использовать во всех средах выполнения .NET, а также позволяет свести к минимуму число директив условной компиляции, предназначенных для конкретных платформ, в общем коде либо полностью исключить их.</span><span class="sxs-lookup"><span data-stu-id="7fa71-108">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="7fa71-109">Это руководство содержит пошаговые инструкции по созданию пакета NuGet для библиотеки .NET Standard 1.4.</span><span class="sxs-lookup"><span data-stu-id="7fa71-109">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="7fa71-110">Эта библиотека работает на платформах .NET Framework 4.6.1, .NET Core, Mono/Xamarin и универсальной платформе Windows 10.</span><span class="sxs-lookup"><span data-stu-id="7fa71-110">Such a library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="7fa71-111">Дополнительные сведения см. в разделе [Таблица сопоставления .NET Standard](#net-standard-mapping-table) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="7fa71-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fa71-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7fa71-112">Prerequisites</span></span>

1. <span data-ttu-id="7fa71-113">Visual Studio 2015 с обновлением 3</span><span class="sxs-lookup"><span data-stu-id="7fa71-113">Visual Studio 2015 Update 3</span></span>
1. [<span data-ttu-id="7fa71-114">Пакет SDK для .NET Core</span><span class="sxs-lookup"><span data-stu-id="7fa71-114">.NET Core SDK</span></span>](https://www.microsoft.com/net/download/)
1. <span data-ttu-id="7fa71-115">Интерфейс командной строки NuGet.</span><span class="sxs-lookup"><span data-stu-id="7fa71-115">NuGet CLI.</span></span> <span data-ttu-id="7fa71-116">Скачайте последнюю версию nuget.exe на странице [nuget.org/downloads](https://nuget.org/downloads), сохранив ее в любом месте на ваш выбор.</span><span class="sxs-lookup"><span data-stu-id="7fa71-116">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="7fa71-117">Затем добавьте это расположение в переменную среды PATH, если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="7fa71-117">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="7fa71-118">nuget.exe является программой интерфейса командной строки, а не установщиком, поэтому сохраните скачиваемый из браузера файл, но не запускайте его.</span><span class="sxs-lookup"><span data-stu-id="7fa71-118">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="7fa71-119">Создание проекта для библиотеки классов</span><span class="sxs-lookup"><span data-stu-id="7fa71-119">Create the class library project</span></span>

1. <span data-ttu-id="7fa71-120">В Visual Studio выберите **Файл > Создать > Проект**, разверните узел **Visual C# > Windows**, выберите **Библиотека классов (переносимая)**, измените имя на "AppLogger" и нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="7fa71-120">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![Создание нового проекта для библиотеки классов](media/NetStandard-NewProject.png)

1. <span data-ttu-id="7fa71-122">В диалоговом окне **Добавление переносимой библиотеки классов** выберите параметры `.NET Framework 4.6` и `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="7fa71-122">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>

1. <span data-ttu-id="7fa71-123">Щелкните правой кнопкой мыши `AppLogger (Portable)` в обозревателе решений, выберите **Свойства**, перейдите на вкладку **Библиотека** и щелкните **Нацелить на стандартную платформу .NET** в разделе **Нацеливание**.</span><span class="sxs-lookup"><span data-stu-id="7fa71-123">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="7fa71-124">Появится запрос на подтверждение, после которого вы можете выбрать `.NET Standard 1.4` в раскрывающемся списке:</span><span class="sxs-lookup"><span data-stu-id="7fa71-124">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![Настройка нацеливания на платформу .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="7fa71-126">Перейдите на вкладку **Построение**, в разделе **Конфигурация** выберите `Release`, после чего установите флажок **XML-файл документации**.</span><span class="sxs-lookup"><span data-stu-id="7fa71-126">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="7fa71-127">Добавьте собственный код для компонента, например:</span><span class="sxs-lookup"><span data-stu-id="7fa71-127">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. <span data-ttu-id="7fa71-128">Установите конфигурацию "Выпуск", выполните сборку проекта и убедитесь, что файлы DLL и XML создаются в папке `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="7fa71-128">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="7fa71-129">Создание и изменение файла NUSPEC</span><span class="sxs-lookup"><span data-stu-id="7fa71-129">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="7fa71-130">Откройте командную строку, перейдите в папку, содержащую папку `AppLogger.csproj` (на один уровень ниже места расположения файла `.sln`) и выполните команду NuGet `spec`, чтобы создать первичный файл `AppLogger.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="7fa71-130">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="7fa71-131">Откройте файл `AppLogger.nuspec` в редакторе и измените его содержимое так, как показано ниже, заменив YOUR_NAME на соответствующее значение.</span><span class="sxs-lookup"><span data-stu-id="7fa71-131">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="7fa71-132">Значение `<id>` должно быть уникальным в пределах nuget.org (см. соглашения об именовании, описанные в разделе [Создание пакета](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="7fa71-132">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="7fa71-133">Кроме того, обратите внимание на то, что необходимо изменить теги author и description, иначе на этапе упаковки произойдет ошибка.</span><span class="sxs-lookup"><span data-stu-id="7fa71-133">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="7fa71-134">Добавьте файл базовой сборки `.nuspec`, а именно DLL-файл библиотеки и XML-файл IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="7fa71-134">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="7fa71-135">Щелкните решение правой кнопкой мыши и выберите **Построить решение**, чтобы создать все файлы пакета.</span><span class="sxs-lookup"><span data-stu-id="7fa71-135">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="7fa71-136">Объявление зависимостей</span><span class="sxs-lookup"><span data-stu-id="7fa71-136">Declaring dependencies</span></span>

<span data-ttu-id="7fa71-137">Если вы используете зависимости от других пакетов NuGet, перечислите их в элементе `<dependencies>` манифеста с элементами `<group>`.</span><span class="sxs-lookup"><span data-stu-id="7fa71-137">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="7fa71-138">Например, чтобы объявить зависимость от NewtonSoft.Json 8.0.3 или более поздней версии, добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="7fa71-138">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="7fa71-139">Синтаксис атрибута *version* в этом случае указывает, что приемлемыми являются версия 8.0.3 или более поздние.</span><span class="sxs-lookup"><span data-stu-id="7fa71-139">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="7fa71-140">Инструкции по указанию других диапазонов версий см. в разделе [Управление версиями пакета](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="7fa71-140">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="7fa71-141">Добавление файла сведений</span><span class="sxs-lookup"><span data-stu-id="7fa71-141">Adding a readme</span></span>

<span data-ttu-id="7fa71-142">Создайте файл `readme.txt`, поместите его в корневую папку проекта и задайте ссылку на него в файле `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="7fa71-142">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="7fa71-143">При установке этого пакета в проекте Visual Studio отображает `readme.txt`.</span><span class="sxs-lookup"><span data-stu-id="7fa71-143">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="7fa71-144">Этот файл не отображается при установке в проектах .NET Core, а также для пакетов, устанавливаемых в качестве зависимости.</span><span class="sxs-lookup"><span data-stu-id="7fa71-144">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="7fa71-145">Упаковка компонента</span><span class="sxs-lookup"><span data-stu-id="7fa71-145">Package the component</span></span>

<span data-ttu-id="7fa71-146">Когда будет готов файл `.nuspec` со ссылками на все файлы, которые необходимо включить в пакет, можно выполнить команду `pack`:</span><span class="sxs-lookup"><span data-stu-id="7fa71-146">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="7fa71-147">Будет создан файл `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="7fa71-147">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="7fa71-148">Если открыть файл в таком средстве, как [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), и развернуть все узлы, отобразится следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="7fa71-148">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Пакет AppLogger в обозревателе пакетов NuGet](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="7fa71-150">Файл `.nupkg` — это просто ZIP-файл с другим расширением.</span><span class="sxs-lookup"><span data-stu-id="7fa71-150">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="7fa71-151">Поэтому чтобы просмотреть содержимое пакета, можно просто изменить расширение `.nupkg` на `.zip`, но не забудьте восстановить расширение перед отправкой пакета на сайт nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7fa71-151">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="7fa71-152">Чтобы предоставить доступ к пакету другим разработчикам, следуйте инструкциям в разделе [Публикация пакета](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="7fa71-152">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="7fa71-153">Обратите внимание, что команда `pack` требует наличия Mono 4.4.2 в Mac OS X и не работает в системах Linux.</span><span class="sxs-lookup"><span data-stu-id="7fa71-153">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="7fa71-154">На компьютерах Mac также необходимо преобразовать пути в формате Windows, указанные в файле `.nuspec`, в формат Unix.</span><span class="sxs-lookup"><span data-stu-id="7fa71-154">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="net-standard-mapping-table"></a><span data-ttu-id="7fa71-155">Таблица сопоставления .NET Standard</span><span class="sxs-lookup"><span data-stu-id="7fa71-155">.NET Standard mapping table</span></span>

| <span data-ttu-id="7fa71-156">Имя платформы</span><span class="sxs-lookup"><span data-stu-id="7fa71-156">Platform Name</span></span> | <span data-ttu-id="7fa71-157">Alias</span><span class="sxs-lookup"><span data-stu-id="7fa71-157">Alias</span></span> |
| --- | --- |
| <span data-ttu-id="7fa71-158">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="7fa71-158">.NET Standard</span></span> | <span data-ttu-id="7fa71-159">netstandard</span><span class="sxs-lookup"><span data-stu-id="7fa71-159">netstandard</span></span> | <span data-ttu-id="7fa71-160">1.0</span><span class="sxs-lookup"><span data-stu-id="7fa71-160">1.0</span></span> | <span data-ttu-id="7fa71-161">1.1</span><span class="sxs-lookup"><span data-stu-id="7fa71-161">1.1</span></span> | <span data-ttu-id="7fa71-162">1.2</span><span class="sxs-lookup"><span data-stu-id="7fa71-162">1.2</span></span> | <span data-ttu-id="7fa71-163">1.3</span><span class="sxs-lookup"><span data-stu-id="7fa71-163">1.3</span></span> | <span data-ttu-id="7fa71-164">1.4</span><span class="sxs-lookup"><span data-stu-id="7fa71-164">1.4</span></span> | <span data-ttu-id="7fa71-165">1.5</span><span class="sxs-lookup"><span data-stu-id="7fa71-165">1.5</span></span> | <span data-ttu-id="7fa71-166">1.6</span><span class="sxs-lookup"><span data-stu-id="7fa71-166">1.6</span></span> |
| <span data-ttu-id="7fa71-167">.NET Core</span><span class="sxs-lookup"><span data-stu-id="7fa71-167">.NET Core</span></span> | <span data-ttu-id="7fa71-168">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="7fa71-168">netcoreapp</span></span> | <span data-ttu-id="7fa71-169">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-169">&#x2192;</span></span> | <span data-ttu-id="7fa71-170">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-170">&#x2192;</span></span> | <span data-ttu-id="7fa71-171">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-171">&#x2192;</span></span> | <span data-ttu-id="7fa71-172">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-172">&#x2192;</span></span> | <span data-ttu-id="7fa71-173">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-173">&#x2192;</span></span> | <span data-ttu-id="7fa71-174">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-174">&#x2192;</span></span> | <span data-ttu-id="7fa71-175">1.0</span><span class="sxs-lookup"><span data-stu-id="7fa71-175">1.0</span></span> |
| <span data-ttu-id="7fa71-176">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="7fa71-176">.NET Framework</span></span> | <span data-ttu-id="7fa71-177">net</span><span class="sxs-lookup"><span data-stu-id="7fa71-177">net</span></span> | <span data-ttu-id="7fa71-178">4.5</span><span class="sxs-lookup"><span data-stu-id="7fa71-178">4.5</span></span> | <span data-ttu-id="7fa71-179">4.5.1</span><span class="sxs-lookup"><span data-stu-id="7fa71-179">4.5.1</span></span> | <span data-ttu-id="7fa71-180">4.6</span><span class="sxs-lookup"><span data-stu-id="7fa71-180">4.6</span></span> | <span data-ttu-id="7fa71-181">4.6.1</span><span class="sxs-lookup"><span data-stu-id="7fa71-181">4.6.1</span></span> | <span data-ttu-id="7fa71-182">4.6.2</span><span class="sxs-lookup"><span data-stu-id="7fa71-182">4.6.2</span></span> | <span data-ttu-id="7fa71-183">4.6.3</span><span class="sxs-lookup"><span data-stu-id="7fa71-183">4.6.3</span></span> |
| <span data-ttu-id="7fa71-184">Платформы Mono и Xamarin</span><span class="sxs-lookup"><span data-stu-id="7fa71-184">Mono/Xamarin Platforms</span></span> | <span data-ttu-id="7fa71-185">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-185">&#x2192;</span></span> | <span data-ttu-id="7fa71-186">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-186">&#x2192;</span></span> | <span data-ttu-id="7fa71-187">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-187">&#x2192;</span></span> | <span data-ttu-id="7fa71-188">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-188">&#x2192;</span></span> | <span data-ttu-id="7fa71-189">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-189">&#x2192;</span></span> | <span data-ttu-id="7fa71-190">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-190">&#x2192;</span></span> |
| <span data-ttu-id="7fa71-191">Универсальная платформа Windows </span><span class="sxs-lookup"><span data-stu-id="7fa71-191">Universal Windows Platform</span></span> | <span data-ttu-id="7fa71-192">uap</span><span class="sxs-lookup"><span data-stu-id="7fa71-192">uap</span></span> | <span data-ttu-id="7fa71-193">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-193">&#x2192;</span></span> | <span data-ttu-id="7fa71-194">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-194">&#x2192;</span></span> | <span data-ttu-id="7fa71-195">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-195">&#x2192;</span></span> | <span data-ttu-id="7fa71-196">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-196">&#x2192;</span></span> |<span data-ttu-id="7fa71-197">10.0</span><span class="sxs-lookup"><span data-stu-id="7fa71-197">10.0</span></span> |
| <span data-ttu-id="7fa71-198">Windows</span><span class="sxs-lookup"><span data-stu-id="7fa71-198">Windows</span></span> | <span data-ttu-id="7fa71-199">win</span><span class="sxs-lookup"><span data-stu-id="7fa71-199">win</span></span>| <span data-ttu-id="7fa71-200">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-200">&#x2192;</span></span> | <span data-ttu-id="7fa71-201">8.0</span><span class="sxs-lookup"><span data-stu-id="7fa71-201">8.0</span></span> | <span data-ttu-id="7fa71-202">8.1</span><span class="sxs-lookup"><span data-stu-id="7fa71-202">8.1</span></span> |
| <span data-ttu-id="7fa71-203">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="7fa71-203">Windows Phone</span></span> | <span data-ttu-id="7fa71-204">wpa</span><span class="sxs-lookup"><span data-stu-id="7fa71-204">wpa</span></span>| <span data-ttu-id="7fa71-205">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-205">&#x2192;</span></span>| <span data-ttu-id="7fa71-206">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7fa71-206">&#x2192;</span></span> | <span data-ttu-id="7fa71-207">8.1</span><span class="sxs-lookup"><span data-stu-id="7fa71-207">8.1</span></span> |
| <span data-ttu-id="7fa71-208">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="7fa71-208">Windows Phone Silverlight</span></span> | <span data-ttu-id="7fa71-209">wp</span><span class="sxs-lookup"><span data-stu-id="7fa71-209">wp</span></span> | <span data-ttu-id="7fa71-210">8.0</span><span class="sxs-lookup"><span data-stu-id="7fa71-210">8.0</span></span> |

## <a name="related-topics"></a><span data-ttu-id="7fa71-211">См. также</span><span class="sxs-lookup"><span data-stu-id="7fa71-211">Related topics</span></span>

- [<span data-ttu-id="7fa71-212">Справочник по файлу NUSPEC</span><span class="sxs-lookup"><span data-stu-id="7fa71-212">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="7fa71-213">Поддержка нескольких версий платформы .NET Framework</span><span class="sxs-lookup"><span data-stu-id="7fa71-213">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="7fa71-214">Включение в пакет свойств и целей MSBuild</span><span class="sxs-lookup"><span data-stu-id="7fa71-214">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="7fa71-215">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="7fa71-215">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="7fa71-216">Пакеты символов</span><span class="sxs-lookup"><span data-stu-id="7fa71-216">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="7fa71-217">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="7fa71-217">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="7fa71-218">Документация по библиотеке .NET Standard</span><span class="sxs-lookup"><span data-stu-id="7fa71-218">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="7fa71-219">Перенос кода в .NET Core из .NET Framework</span><span class="sxs-lookup"><span data-stu-id="7fa71-219">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
