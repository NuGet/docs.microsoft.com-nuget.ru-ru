---
title: "Создание пакетов NuGet для платформы .NET Standard 2.0 с помощью Visual Studio 2017 | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: "Полное пошаговое руководство по созданию пакетов NuGet для платформы .NET Standard 2.0 с использованием NuGet 4.x и Visual Studio 2017."
keywords: "создание пакета, пакеты .NET Standard, .NET Core"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82e413119b12503336becd6019e4fa3e4ac0b1f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a><span data-ttu-id="c60ac-104">Создание пакетов .NET Standard 2.0 с помощью Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c60ac-104">Create .NET Standard 2.0 packages with Visual Studio 2017</span></span>

<span data-ttu-id="c60ac-105">*Применяется к NuGet 4.x+ и MSBuild 15.3 + в соответствии с обновлением 3 для Visual Studio 2017. Для более ранних версий Visual Studio 2017 эти инструкции можно применить к .NET Standard версий с 1.4 до 1.6, изменив свойство \<TargetFramework\>. Сведения о работе с NuGet 3.x+ см. в разделе [Создание пакетов для платформы .NET Standard с помощью Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span><span class="sxs-lookup"><span data-stu-id="c60ac-105">*Applies to NuGet 4.x+ and MSBuild 15.3+ as provided with Visual Studio 2017 Update 3. For earlier versions of Visual Studio 2017, these instructions apply to .NET Standard 1.4 to 1.6 by changing the \<TargetFramework\> property. Also see [Create .NET Standard Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) for working with NuGet 3.x+.*</span></span>

<span data-ttu-id="c60ac-106">[Библиотека .NET Standard](https://docs.microsoft.com/dotnet/articles/standard/library) представляет собой формальную спецификацию интерфейсов API .NET, которые должны быть доступны во всех средах выполнения .NET, что позволяет повысить степень унификации экосистемы .NET.</span><span class="sxs-lookup"><span data-stu-id="c60ac-106">The [.NET Standard Library](https://docs.microsoft.com/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="c60ac-107">Библиотека .NET Standard определяет унифицированный набор API-интерфейсов библиотеки базовых классов (BCL) для реализации всеми платформами .NET независимо от рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="c60ac-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="c60ac-108">Таким образом, разработчики могут создавать переносимые библиотеки классов, которые могут использоваться во всех средах выполнения .NET, что позволяет свести к минимуму число директив условной компиляции, предназначенных для конкретных платформ, в общем коде либо полностью исключить их.</span><span class="sxs-lookup"><span data-stu-id="c60ac-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="c60ac-109">В этом руководстве приведены пошаговые инструкции по созданию пакета NuGet для библиотеки .NET Standard 2.0 с использованием обновления 3 для Visual Studio 2017 и NuGet 4.0.</span><span class="sxs-lookup"><span data-stu-id="c60ac-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 2.0 with Visual Studio 2017 Update 3 and NuGet 4.0.</span></span>

1. [<span data-ttu-id="c60ac-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c60ac-110">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="c60ac-111">Создание проекта для библиотеки классов</span><span class="sxs-lookup"><span data-stu-id="c60ac-111">Create the class library project</span></span>](#create-the-netstandard-class-library-project)
1. [<span data-ttu-id="c60ac-112">Изменение метаданных в CSPROJ-файле</span><span class="sxs-lookup"><span data-stu-id="c60ac-112">Edit metadata in the .csproj file</span></span>](#edit-metadata-in-the-csproj-file)
1. [<span data-ttu-id="c60ac-113">Упаковка компонента</span><span class="sxs-lookup"><span data-stu-id="c60ac-113">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="c60ac-114">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="c60ac-114">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="c60ac-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c60ac-115">Pre-requisites</span></span>

<span data-ttu-id="c60ac-116">Для прохождения этого руководства требуется обновление 3 для Visual Studio 2017 с рабочей нагрузкой **Кроссплатформенная разработка .NET Core**.</span><span class="sxs-lookup"><span data-stu-id="c60ac-116">This walkthrough requires Visual Studio 2017 Update 3 with the **.NET Core cross-platform development** workload.</span></span> <span data-ttu-id="c60ac-117">Вы можете установить бесплатный выпуск Community с сайта [visualstudio.com](https://www.visualstudio.com/) либо использовать выпуск Professional или Enterprise.</span><span class="sxs-lookup"><span data-stu-id="c60ac-117">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/), or use the Professional and Enterprise editions.</span></span>

<span data-ttu-id="c60ac-118">Нужная рабочая нагрузка выглядит в Visual Studio Installer следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c60ac-118">The require workload appears as follows in the Visual Studio installer:</span></span>

![Рабочая нагрузка "Кроссплатформенная разработка .NET Core" в Visual Studio Installer](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a><span data-ttu-id="c60ac-120">Создание проекта библиотеки классов .NET Standard</span><span class="sxs-lookup"><span data-stu-id="c60ac-120">Create the .NET Standard class library project</span></span>

1. <span data-ttu-id="c60ac-121">В Visual Studio выберите **Файл > Создать > Проект**, разверните узел **Visual C# > .NET Standard**, выберите **Библиотека классов (.NET Standard)**, измените имя на "AppLogger" и нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="c60ac-121">In Visual Studio, **File > New > Project**, expand the **Visual C# > .NET Standard** node, select **Class Library (Net Standard)**, change the name to AppLogger, and click OK.</span></span>

    ![Создание нового проекта для библиотеки классов](media/NuGet4-02-NewProject.png)

1. <span data-ttu-id="c60ac-123">Измените конфигурацию сборки на **Выпуск**.</span><span class="sxs-lookup"><span data-stu-id="c60ac-123">Change the build configuration to **Release**.</span></span>
1. <span data-ttu-id="c60ac-124">Щелкните правой кнопкой мыши проект `AppLogger` в обозревателе решений и выберите пункт **Свойства**, откройте вкладку **Сборка**, установите флажок **Файл XML-документации** и задайте в качестве имени файла только `AppLogger.xml`.</span><span class="sxs-lookup"><span data-stu-id="c60ac-124">Right-click the `AppLogger` project in Solution Explorer, select **Properties**, select the **Build** tab, check the box for **XML documentation file**, and set the filename to just `AppLogger.xml`.</span></span> <span data-ttu-id="c60ac-125">Сохраните проект.</span><span class="sxs-lookup"><span data-stu-id="c60ac-125">Then save the project.</span></span>

1. <span data-ttu-id="c60ac-126">Добавьте код в компонент, например, следующий (который лишь выводит сообщения на консоль):</span><span class="sxs-lookup"><span data-stu-id="c60ac-126">Add your code to the component, such as the following (which clearly just outputs messages to the console):</span></span>

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

1. <span data-ttu-id="c60ac-127">Выполните сборку проекта с использованием конфигурации выпуска и убедитесь, что файлы DLL и XML создаются в папке `bin\Release\netstandard2.0`.</span><span class="sxs-lookup"><span data-stu-id="c60ac-127">Build the project (with the Release configuration) and check that DLL and XML files are produced within the `bin\Release\netstandard2.0` folder.</span></span>

## <a name="edit-metadata-in-the-csproj-file"></a><span data-ttu-id="c60ac-128">Изменение метаданных в CSPROJ-файле</span><span class="sxs-lookup"><span data-stu-id="c60ac-128">Edit metadata in the .csproj file</span></span>

<span data-ttu-id="c60ac-129">Для проектов NuGet 4.0 и .NET Core метаданные пакета содержатся непосредственно в файле `.csproj`, а не во внешних файлах, таких как `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="c60ac-129">With NuGet 4.0 and .NET Core projects, package metadata is contained directly in the `.csproj` file instead of external files such as a `.nuspec`.</span></span> <span data-ttu-id="c60ac-130">Полное описание этих метаданных приведено в разделе [Объекты pack и restore NuGet в качестве целевых объектов MSBuild](../schema/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="c60ac-130">A full description of that metadata is found in [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

1. <span data-ttu-id="c60ac-131">Щелкните правой кнопкой мыши проект в обозревателе решений, выберите пункт **Изменить AppLogger.csproj** и измените первую группу свойств, чтобы включить сведения о пакете, например следующего вида:</span><span class="sxs-lookup"><span data-stu-id="c60ac-131">Right-click the project in Solution Explorer, select **Edit AppLogger.csproj**, and then edit the first property group to include package information such as the following:</span></span>

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. <span data-ttu-id="c60ac-132">Сохраните проект, щелкните решение правой кнопкой мыши и выберите пункт **Собрать решение**, чтобы снова создать все файлы пакета, на этот раз с правильными метаданными.</span><span class="sxs-lookup"><span data-stu-id="c60ac-132">Save the project, then right-click the solution and select **Build Solution** to again generate all the files for the package, this time with the correct metadata.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="c60ac-133">Упаковка компонента</span><span class="sxs-lookup"><span data-stu-id="c60ac-133">Package the component</span></span>

<span data-ttu-id="c60ac-134">NuGet 4.0 поддерживает целевой объект pack с помощью MSBuild версии 15.1+ (включая MSBuild 15.3, входящий в состав обновления 3 для Visual Studio 2017), если проект содержит необходимые метаданные пакета, добавленные в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="c60ac-134">NuGet 4.0 supports a pack target using MSBuild version 15.1+ (including MSBuild 15.3 as part of Visual Studio 2017 Update 3) when the project contains the necessary package metadata, as was added in the previous section.</span></span> <span data-ttu-id="c60ac-135">Чтобы вызывать MSBuild таким образом, просто укажите целевой объект pack в командной строке в той же папке, где находится файл `.csproj`:</span><span class="sxs-lookup"><span data-stu-id="c60ac-135">To invoke MSBuild in this way, simply specify the pack target on the command line in the same folder as the `.csproj` file:</span></span>

    msbuild /t:pack /p:Configuration=Release

<span data-ttu-id="c60ac-136">Сведения о дополнительных возможностях использования `msbuild /t:pack`, таких как включение файлов содержимого, символов и исходного кода, см. в разделе [Объекты pack и restore NuGet в качестве целевых объектов MSBuild](../schema/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="c60ac-136">For additional options with `msbuild /t:pack`, such as including content files, symbols, and source code, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

<span data-ttu-id="c60ac-137">В любом случае приведенная выше команда создает `AppLogger.YOUR_NAME.1.0.0.nupkg` в папке `bin\Release` по умолчанию при сборе этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c60ac-137">In any case, the command above generates `AppLogger.YOUR_NAME.1.0.0.nupkg` in the `bin\Release` folder by default, as it builds that configuration.</span></span> <span data-ttu-id="c60ac-138">Если опустить параметр `/p`, конфигурацией по умолчанию будет `Debug`.</span><span class="sxs-lookup"><span data-stu-id="c60ac-138">If you omit the `/p` switch, the default configuration will be `Debug`.</span></span> 

<span data-ttu-id="c60ac-139">Если открыть файл в таком средстве, как [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), и развернуть все узлы, вы увидите следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="c60ac-139">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![Пакет AppLogger в обозревателе пакетов NuGet](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="c60ac-141">Файл `.nupkg` — это просто ZIP-файл с другим расширением.</span><span class="sxs-lookup"><span data-stu-id="c60ac-141">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="c60ac-142">Поэтому чтобы просмотреть содержимое пакета, можно просто изменить расширение `.nupkg` на `.zip`, но не забудьте восстановить расширение перед отправкой пакета на сайт nuget.org.</span><span class="sxs-lookup"><span data-stu-id="c60ac-142">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="c60ac-143">Чтобы предоставить доступ к пакету другим разработчикам, следуйте инструкциям в разделе [Публикация пакета](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="c60ac-143">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="c60ac-144">См. также</span><span class="sxs-lookup"><span data-stu-id="c60ac-144">Related topics</span></span>

- <span data-ttu-id="c60ac-145">Раздел [Ссылки на пакеты в файлах проекта](../consume-packages/package-references-in-project-files.md) подробно рассказывает, как описать пакет непосредственно в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="c60ac-145">[Package References in Project Files](../consume-packages/package-references-in-project-files.md) describes all the details of describing your package directly in the project file.</span></span>
- <span data-ttu-id="c60ac-146">Раздел [Объекты pack и restore NuGet в качестве целевых объектов MSBuild](../schema/msbuild-targets.md) описывает все возможности использования `msbuild /t:pack` для создания пакета.</span><span class="sxs-lookup"><span data-stu-id="c60ac-146">[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md) describes all the options for using `msbuild /t:pack` to create the package.</span></span>
- [<span data-ttu-id="c60ac-147">Документация по библиотеке .NET Standard</span><span class="sxs-lookup"><span data-stu-id="c60ac-147">.NET Standard Library documentation</span></span>](https://docs.microsoft.com/dotnet/articles/standard/library)
- [<span data-ttu-id="c60ac-148">Перенос кода в .NET Core из .NET Framework</span><span class="sxs-lookup"><span data-stu-id="c60ac-148">Porting to .NET Core from .NET Framework</span></span>](https://docs.microsoft.com/dotnet/articles/core/porting/index)
