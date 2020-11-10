---
title: Создание и публикация пакета NuGet с помощью CLI dotnet
description: Пошаговое руководство по созданию и публикации пакета NuGet с помощью .NET Core CLI — dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: a67c8cd92304c6c4abcffbb79ddbe964664d08fb
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237488"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="7bb27-103">Краткое руководство. Создание и публикация пакета (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="7bb27-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="7bb27-104">Создание пакета NuGet из библиотеки классов .NET и его публикация на сайте nuget.org выполняются очень просто с помощью интерфейса командной строки (CLI) `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="7bb27-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bb27-105">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7bb27-105">Prerequisites</span></span>

1. <span data-ttu-id="7bb27-106">Установите [пакет SDK для .NET Core](https://www.microsoft.com/net/download/), содержащий CLI `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="7bb27-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="7bb27-107">Начиная с версии Visual Studio 2017, средство CLI dotnet автоматически устанавливается вместе с любыми рабочими нагрузками, связанными с .NET Core.</span><span class="sxs-lookup"><span data-stu-id="7bb27-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="7bb27-108">[Зарегистрируйтесь для получения бесплатной учетной записи на nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), если вы не сделали этого ранее.</span><span class="sxs-lookup"><span data-stu-id="7bb27-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="7bb27-109">При создании учетной записи вам направляется сообщение электронной почты с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="7bb27-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="7bb27-110">Перед отправкой пакета вам нужно подтвердить учетную запись.</span><span class="sxs-lookup"><span data-stu-id="7bb27-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="7bb27-111">Создание проекта библиотеки классов</span><span class="sxs-lookup"><span data-stu-id="7bb27-111">Create a class library project</span></span>

<span data-ttu-id="7bb27-112">Вы можете использовать имеющийся проект библиотеки классов .NET для кода, который нужно упаковать, или же создать простой проект, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="7bb27-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="7bb27-113">Создайте папку с именем `AppLogger`.</span><span class="sxs-lookup"><span data-stu-id="7bb27-113">Create a folder called `AppLogger`.</span></span>

1. <span data-ttu-id="7bb27-114">Откройте командную строку и перейдите в папку `AppLogger`.</span><span class="sxs-lookup"><span data-stu-id="7bb27-114">Open a command prompt and switch to the `AppLogger` folder.</span></span>

1. <span data-ttu-id="7bb27-115">Введите `dotnet new classlib`; команда использует имя текущей папки для проекта.</span><span class="sxs-lookup"><span data-stu-id="7bb27-115">Type `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

   <span data-ttu-id="7bb27-116">Будет создан новый проект.</span><span class="sxs-lookup"><span data-stu-id="7bb27-116">This creates the new project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="7bb27-117">Добавление метаданных пакета в файл проекта</span><span class="sxs-lookup"><span data-stu-id="7bb27-117">Add package metadata to the project file</span></span>

<span data-ttu-id="7bb27-118">Каждому пакету NuGet нужен манифест, описывающий его содержимое и зависимости.</span><span class="sxs-lookup"><span data-stu-id="7bb27-118">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="7bb27-119">В итоговом пакете манифестом является файл `.nuspec`, созданный из свойств метаданных NuGet, включенных в файл проекта.</span><span class="sxs-lookup"><span data-stu-id="7bb27-119">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="7bb27-120">Откройте файл проекта (`.csproj`) и добавьте внутри тега `<PropertyGroup>` следующие минимальные свойства. При этом измените значения соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="7bb27-120">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="7bb27-121">Присвойте пакету идентификатор, уникальный на сайте nuget.org или в другом используемом узле.</span><span class="sxs-lookup"><span data-stu-id="7bb27-121">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="7bb27-122">При работе с этим руководством мы рекомендуем добавить к имени слово "Sample" или "Test", так как позже, после публикации, пакет станет общедоступным (хотя маловероятно, что кто-то будет его использовать).</span><span class="sxs-lookup"><span data-stu-id="7bb27-122">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="7bb27-123">Укажите любые дополнительные свойства, описанные в разделе [Свойства метаданных NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="7bb27-123">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="7bb27-124">Если пакет будет общедоступным, обратите особое внимание на свойство **PackageTags** , так как теги помогают найти ваш пакет и понять его назначение.</span><span class="sxs-lookup"><span data-stu-id="7bb27-124">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="7bb27-125">Выполнение команды pack</span><span class="sxs-lookup"><span data-stu-id="7bb27-125">Run the pack command</span></span>

<span data-ttu-id="7bb27-126">Чтобы создать пакет NuGet (`.nupkg` файл) из проекта, запустите команду `dotnet pack`, которая также автоматически построит проект:</span><span class="sxs-lookup"><span data-stu-id="7bb27-126">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="7bb27-127">На выходе показан путь к `.nupkg` файлу:</span><span class="sxs-lookup"><span data-stu-id="7bb27-127">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="7bb27-128">Автоматическое создание пакета при сборке</span><span class="sxs-lookup"><span data-stu-id="7bb27-128">Automatically generate package on build</span></span>

<span data-ttu-id="7bb27-129">Чтобы автоматически выполнить команду `dotnet pack` вместе с командой `dotnet build`, в разделе `<PropertyGroup>` файла проекта добавьте следующую строку:</span><span class="sxs-lookup"><span data-stu-id="7bb27-129">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="7bb27-130">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="7bb27-130">Publish the package</span></span>

<span data-ttu-id="7bb27-131">Получив файл `.nupkg`, опубликуйте его на сайте nuget.org, используя команду `dotnet nuget push`, а также ключ API, полученный на этом сайте.</span><span class="sxs-lookup"><span data-stu-id="7bb27-131">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="7bb27-132">Получение ключа API</span><span class="sxs-lookup"><span data-stu-id="7bb27-132">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="7bb27-133">Публикация с помощью команды dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="7bb27-133">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="7bb27-134">Ошибки публикации</span><span class="sxs-lookup"><span data-stu-id="7bb27-134">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="7bb27-135">Управление опубликованным пакетом</span><span class="sxs-lookup"><span data-stu-id="7bb27-135">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-video"></a><span data-ttu-id="7bb27-136">Связанные видео</span><span class="sxs-lookup"><span data-stu-id="7bb27-136">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-the-NET-CLI-5-of-5/player]

<span data-ttu-id="7bb27-137">Другие видео о NuGet см. на [Channel 9](https://channel9.msdn.com/Series/NuGet-101) и [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="7bb27-137">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bb27-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7bb27-138">Next steps</span></span>

<span data-ttu-id="7bb27-139">Поздравляем! Вы создали пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="7bb27-139">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7bb27-140">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="7bb27-140">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)

<span data-ttu-id="7bb27-141">См. подробнее о возможностях NuGet по приведенным ниже ссылкам.</span><span class="sxs-lookup"><span data-stu-id="7bb27-141">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="7bb27-142">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="7bb27-142">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="7bb27-143">Пакеты предварительного выпуска</span><span class="sxs-lookup"><span data-stu-id="7bb27-143">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="7bb27-144">Поддержка нескольких целевых платформ</span><span class="sxs-lookup"><span data-stu-id="7bb27-144">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="7bb27-145">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="7bb27-145">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="7bb27-146">Добавление выражения лицензии или файла лицензии</span><span class="sxs-lookup"><span data-stu-id="7bb27-146">Adding a license expression or file</span></span>](../reference/msbuild-targets#packing-a-license-expression-or-a-license-file)
- [<span data-ttu-id="7bb27-147">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="7bb27-147">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="7bb27-148">Создание пакетов символов</span><span class="sxs-lookup"><span data-stu-id="7bb27-148">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="7bb27-149">Подписывание пакетов</span><span class="sxs-lookup"><span data-stu-id="7bb27-149">Signing packages</span></span>](../create-packages/Sign-a-package.md)
