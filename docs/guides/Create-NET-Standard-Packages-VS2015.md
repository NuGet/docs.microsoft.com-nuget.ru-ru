---
title: Создание пакетов NuGet .NET Standard или .NET Framework с помощью Visual Studio 2015
description: Полное пошаговое руководство по созданию пакетов NuGet для платформы .NET Standard и .NET Framework с помощью NuGet 3.x и Visual Studio 2015.
author: JonDouglas
ms.author: jodou
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: d55228bbbd238d8930404ea52c5a80383bc9e0a3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774387"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="212dc-103">Создание пакетов .NET Standard или .NET Framework с помощью Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="212dc-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="212dc-104">**Примечание.** Рекомендуем разрабатывать библиотеки .NET Standard с помощью Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="212dc-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="212dc-105">Вы можете использовать и Visual Studio 2015, но средства .NET Core доступны только в предварительной пробной версии.</span><span class="sxs-lookup"><span data-stu-id="212dc-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="212dc-106">Сведения о работе с NuGet 4.x или более поздних версий и Visual Studio 2017 см. в статье [Создание и публикация пакета с помощью Visual Studio (.NET Standard)](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="212dc-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="212dc-107">[Библиотека .NET Standard](/dotnet/articles/standard/library) представляет собой формальную спецификацию интерфейсов API .NET, которые должны быть доступны во всех средах выполнения .NET, что позволяет повысить степень унификации экосистемы .NET.</span><span class="sxs-lookup"><span data-stu-id="212dc-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="212dc-108">Библиотека .NET Standard определяет унифицированный набор API-интерфейсов библиотеки базовых классов (BCL) для реализации всеми платформами .NET независимо от рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="212dc-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="212dc-109">Это позволяет разработчикам создавать код, который можно использовать во всех средах выполнения .NET, а также позволяет свести к минимуму число директив условной компиляции, предназначенных для конкретных платформ, в общем коде либо полностью исключить их.</span><span class="sxs-lookup"><span data-stu-id="212dc-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="212dc-110">В этом руководстве приведены пошаговые инструкции по созданию пакета NuGet для библиотеки .NET Standard 1.4 или .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="212dc-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="212dc-111">Библиотека .NET Standard 1.4 работает на платформах .NET Framework 4.6.1, .NET Core, Mono/Xamarin и универсальной платформе Windows 10.</span><span class="sxs-lookup"><span data-stu-id="212dc-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="212dc-112">Дополнительные сведения см. в разделе [Поддержка реализации .NET](/dotnet/standard/net-standard#net-implementation-support) (документация .NET).</span><span class="sxs-lookup"><span data-stu-id="212dc-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="212dc-113">При необходимости вы можете выбрать другую версию библиотеки .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="212dc-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="212dc-114">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="212dc-114">Prerequisites</span></span>

1. <span data-ttu-id="212dc-115">Visual Studio 2015 с обновлением 3</span><span class="sxs-lookup"><span data-stu-id="212dc-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="212dc-116">[Пакет SDK для .NET Core](https://www.microsoft.com/net/download/) (только .NET Standard)</span><span class="sxs-lookup"><span data-stu-id="212dc-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="212dc-117">Интерфейс командной строки NuGet.</span><span class="sxs-lookup"><span data-stu-id="212dc-117">NuGet CLI.</span></span> <span data-ttu-id="212dc-118">Скачайте последнюю версию nuget.exe на странице [nuget.org/downloads](https://nuget.org/downloads), сохранив ее в любом месте на ваш выбор.</span><span class="sxs-lookup"><span data-stu-id="212dc-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="212dc-119">Затем добавьте это расположение в переменную среды PATH, если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="212dc-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="212dc-120">nuget.exe является программой интерфейса командной строки, а не установщиком, поэтому сохраните скачиваемый из браузера файл, но не запускайте его.</span><span class="sxs-lookup"><span data-stu-id="212dc-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="212dc-121">Создание проекта для библиотеки классов</span><span class="sxs-lookup"><span data-stu-id="212dc-121">Create the class library project</span></span>

1. <span data-ttu-id="212dc-122">В Visual Studio выберите **Файл > Создать > Проект**, разверните узел **Visual C# > Windows**, выберите **Библиотека классов (переносимая)** , измените имя на AppLogger и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="212dc-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Создание нового проекта для библиотеки классов](media/NetStandard-NewProject.png)

1. <span data-ttu-id="212dc-124">В диалоговом окне **Добавление переносимой библиотеки классов** выберите параметры `.NET Framework 4.6` и `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="212dc-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="212dc-125">(Для платформы .NET Framework выберите любой подходящий параметр.)</span><span class="sxs-lookup"><span data-stu-id="212dc-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="212dc-126">Если библиотека создается для .NET Standard, щелкните правой кнопкой мыши `AppLogger (Portable)` в обозревателе решений, выберите **Свойства**, перейдите на вкладку **Библиотека** и щелкните **Нацелить на стандартную платформу .NET** в разделе **Нацеливание**.</span><span class="sxs-lookup"><span data-stu-id="212dc-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="212dc-127">Затем появится подтверждение, после чего вы можете выбрать из раскрывающегося списка версию `.NET Standard 1.4` (или любую другую доступную):</span><span class="sxs-lookup"><span data-stu-id="212dc-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Настройка нацеливания на платформу .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="212dc-129">Перейдите на вкладку **Построение**, в разделе **Конфигурация** выберите `Release`, после чего установите флажок **XML-файл документации**.</span><span class="sxs-lookup"><span data-stu-id="212dc-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="212dc-130">Добавьте собственный код для компонента, например:</span><span class="sxs-lookup"><span data-stu-id="212dc-130">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="212dc-131">Установите конфигурацию "Выпуск", выполните сборку проекта и убедитесь, что файлы DLL и XML создаются в папке `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="212dc-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="212dc-132">Создание и изменение файла NUSPEC</span><span class="sxs-lookup"><span data-stu-id="212dc-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="212dc-133">Откройте командную строку, перейдите в папку, содержащую папку `AppLogger.csproj` (на один уровень ниже места расположения файла `.sln`) и выполните команду NuGet `spec`, чтобы создать первичный файл `AppLogger.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="212dc-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="212dc-134">Откройте файл `AppLogger.nuspec` в редакторе и измените его содержимое так, как показано ниже, заменив YOUR_NAME на соответствующее значение.</span><span class="sxs-lookup"><span data-stu-id="212dc-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="212dc-135">Значение `<id>` должно быть уникальным в пределах nuget.org (см. соглашения об именовании, описанные в разделе [Создание пакета](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="212dc-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="212dc-136">Кроме того, обратите внимание на то, что необходимо изменить теги author и description, иначе на этапе упаковки произойдет ошибка.</span><span class="sxs-lookup"><span data-stu-id="212dc-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="212dc-137">Добавьте файл базовой сборки `.nuspec`, а именно DLL-файл библиотеки и XML-файл IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="212dc-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="212dc-138">Для платформы .NET Standard появятся примерно такие записи:</span><span class="sxs-lookup"><span data-stu-id="212dc-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="212dc-139">Для платформы .NET Framework появятся примерно такие записи:</span><span class="sxs-lookup"><span data-stu-id="212dc-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="212dc-140">Щелкните решение правой кнопкой мыши и выберите **Построить решение**, чтобы создать все файлы пакета.</span><span class="sxs-lookup"><span data-stu-id="212dc-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="212dc-141">Объявление зависимостей</span><span class="sxs-lookup"><span data-stu-id="212dc-141">Declaring dependencies</span></span>

<span data-ttu-id="212dc-142">Если вы используете зависимости от других пакетов NuGet, перечислите их в элементе `<dependencies>` манифеста с элементами `<group>`.</span><span class="sxs-lookup"><span data-stu-id="212dc-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="212dc-143">Например, чтобы объявить зависимость от NewtonSoft.Json 8.0.3 или более поздней версии, добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="212dc-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="212dc-144">Синтаксис атрибута *version* в этом случае указывает, что приемлемыми являются версия 8.0.3 или более поздние.</span><span class="sxs-lookup"><span data-stu-id="212dc-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="212dc-145">Инструкции по указанию других диапазонов версий см. в разделе [Управление версиями пакета](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="212dc-145">To specify different version ranges, refer to [Package versioning](../concepts/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="212dc-146">Добавление файла сведений</span><span class="sxs-lookup"><span data-stu-id="212dc-146">Adding a readme</span></span>

<span data-ttu-id="212dc-147">Создайте файл `readme.txt`, поместите его в корневую папку проекта и задайте ссылку на него в файле `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="212dc-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="212dc-148">При установке этого пакета в проекте Visual Studio отображает `readme.txt`.</span><span class="sxs-lookup"><span data-stu-id="212dc-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="212dc-149">Этот файл не отображается при установке в проектах .NET Core, а также для пакетов, устанавливаемых в качестве зависимости.</span><span class="sxs-lookup"><span data-stu-id="212dc-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="212dc-150">Упаковка компонента</span><span class="sxs-lookup"><span data-stu-id="212dc-150">Package the component</span></span>

<span data-ttu-id="212dc-151">Когда будет готов файл `.nuspec` со ссылками на все файлы, которые необходимо включить в пакет, можно выполнить команду `pack`:</span><span class="sxs-lookup"><span data-stu-id="212dc-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="212dc-152">Будет создан `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="212dc-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="212dc-153">Если открыть файл в таком средстве, как [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), и развернуть все узлы, отобразится следующее содержимое ( .NET Standard):</span><span class="sxs-lookup"><span data-stu-id="212dc-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![Пакет AppLogger в обозревателе пакетов NuGet](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="212dc-155">Файл `.nupkg` — это просто ZIP-файл с другим расширением.</span><span class="sxs-lookup"><span data-stu-id="212dc-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="212dc-156">Поэтому чтобы просмотреть содержимое пакета, можно просто изменить расширение `.nupkg` на `.zip`, но не забудьте восстановить расширение перед отправкой пакета на сайт nuget.org.</span><span class="sxs-lookup"><span data-stu-id="212dc-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="212dc-157">Чтобы предоставить доступ к пакету другим разработчикам, следуйте инструкциям в разделе [Публикация пакета](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="212dc-157">To make your package available to other developers, follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="212dc-158">Обратите внимание, что команда `pack` требует наличия Mono 4.4.2 в Mac OS X и не работает в системах Linux.</span><span class="sxs-lookup"><span data-stu-id="212dc-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="212dc-159">На компьютерах Mac также необходимо преобразовать пути в формате Windows, указанные в файле `.nuspec`, в формат Unix.</span><span class="sxs-lookup"><span data-stu-id="212dc-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="212dc-160">Связанные разделы</span><span class="sxs-lookup"><span data-stu-id="212dc-160">Related topics</span></span>

- [<span data-ttu-id="212dc-161">Справочник по файлу NUSPEC</span><span class="sxs-lookup"><span data-stu-id="212dc-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="212dc-162">Поддержка нескольких версий платформы .NET Framework</span><span class="sxs-lookup"><span data-stu-id="212dc-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="212dc-163">Включение в пакет свойств и целей MSBuild</span><span class="sxs-lookup"><span data-stu-id="212dc-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="212dc-164">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="212dc-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="212dc-165">Пакеты символов</span><span class="sxs-lookup"><span data-stu-id="212dc-165">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="212dc-166">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="212dc-166">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="212dc-167">Документация по библиотеке .NET Standard</span><span class="sxs-lookup"><span data-stu-id="212dc-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="212dc-168">Перенос кода в .NET Core из .NET Framework</span><span class="sxs-lookup"><span data-stu-id="212dc-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
