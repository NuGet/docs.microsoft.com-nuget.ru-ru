---
title: Создание и публикация пакета NuGet с помощью CLI dotnet
description: Пошаговое руководство по созданию и публикации пакета NuGet с помощью .NET Core CLI — dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: c0e6de2c3b9978538d504f4af6e744ece43b4a4d
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488936"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="8db15-103">Краткое руководство. Создание и публикация пакета (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="8db15-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="8db15-104">Создание пакета NuGet из библиотеки классов .NET и его публикация на сайте nuget.org выполняются очень просто с помощью интерфейса командной строки (CLI) `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="8db15-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8db15-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8db15-105">Prerequisites</span></span>

1. <span data-ttu-id="8db15-106">Установите [пакет SDK для .NET Core](https://www.microsoft.com/net/download/), содержащий CLI `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="8db15-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="8db15-107">Начиная с версии Visual Studio 2017, средство CLI dotnet автоматически устанавливается вместе с любыми рабочими нагрузками, связанными с .NET Core.</span><span class="sxs-lookup"><span data-stu-id="8db15-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="8db15-108">[Зарегистрируйтесь для получения бесплатной учетной записи на nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), если вы не сделали этого ранее.</span><span class="sxs-lookup"><span data-stu-id="8db15-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="8db15-109">При создании учетной записи вам направляется сообщение электронной почты с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="8db15-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="8db15-110">Перед отправкой пакета вам нужно подтвердить учетную запись.</span><span class="sxs-lookup"><span data-stu-id="8db15-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="8db15-111">Создание проекта библиотеки классов</span><span class="sxs-lookup"><span data-stu-id="8db15-111">Create a class library project</span></span>

<span data-ttu-id="8db15-112">Вы можете использовать имеющийся проект библиотеки классов .NET для кода, который нужно упаковать, или же создать простой проект, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="8db15-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="8db15-113">Создайте папку с именем `AppLogger`.</span><span class="sxs-lookup"><span data-stu-id="8db15-113">Create a folder called `AppLogger`.</span></span>

1. <span data-ttu-id="8db15-114">Откройте командную строку и перейдите в папку `AppLogger`.</span><span class="sxs-lookup"><span data-stu-id="8db15-114">Open a command prompt and switch to the `AppLogger` folder.</span></span>

1. <span data-ttu-id="8db15-115">Введите `dotnet new classlib`; команда использует имя текущей папки для проекта.</span><span class="sxs-lookup"><span data-stu-id="8db15-115">Type `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

   <span data-ttu-id="8db15-116">Будет создан новый проект.</span><span class="sxs-lookup"><span data-stu-id="8db15-116">This creates the new project.</span></span>

1. <span data-ttu-id="8db15-117">Чтобы проверить, что приложение создано правильно, используйте команду `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="8db15-117">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="8db15-118">Добавление метаданных пакета в файл проекта</span><span class="sxs-lookup"><span data-stu-id="8db15-118">Add package metadata to the project file</span></span>

<span data-ttu-id="8db15-119">Каждому пакету NuGet нужен манифест, описывающий его содержимое и зависимости.</span><span class="sxs-lookup"><span data-stu-id="8db15-119">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="8db15-120">В итоговом пакете манифестом является файл `.nuspec`, созданный из свойств метаданных NuGet, включенных в файл проекта.</span><span class="sxs-lookup"><span data-stu-id="8db15-120">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="8db15-121">Откройте файл проекта (`.csproj`) и добавьте внутри тега `<PropertyGroup>` следующие минимальные свойства. При этом измените значения соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="8db15-121">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="8db15-122">Присвойте пакету идентификатор, уникальный на сайте nuget.org или в другом используемом узле.</span><span class="sxs-lookup"><span data-stu-id="8db15-122">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="8db15-123">При работе с этим руководством мы рекомендуем добавить к имени слово "Sample" или "Test", так как позже, после публикации, пакет станет общедоступным (хотя маловероятно, что кто-то будет его использовать).</span><span class="sxs-lookup"><span data-stu-id="8db15-123">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="8db15-124">Укажите любые дополнительные свойства, описанные в разделе [Свойства метаданных NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="8db15-124">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="8db15-125">Если пакет будет общедоступным, обратите особое внимание на свойство **PackageTags**, так как теги помогают найти ваш пакет и понять его назначение.</span><span class="sxs-lookup"><span data-stu-id="8db15-125">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="8db15-126">Выполнение команды pack</span><span class="sxs-lookup"><span data-stu-id="8db15-126">Run the pack command</span></span>

<span data-ttu-id="8db15-127">Чтобы создать пакет NuGet (`.nupkg` файл) из проекта, запустите команду `dotnet pack`, которая также автоматически построит проект:</span><span class="sxs-lookup"><span data-stu-id="8db15-127">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="8db15-128">На выходе показан путь к `.nupkg` файлу:</span><span class="sxs-lookup"><span data-stu-id="8db15-128">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="8db15-129">Автоматическое создание пакета при сборке</span><span class="sxs-lookup"><span data-stu-id="8db15-129">Automatically generate package on build</span></span>

<span data-ttu-id="8db15-130">Чтобы автоматически выполнить команду `dotnet pack` вместе с командой `dotnet build`, в разделе `<PropertyGroup>` файла проекта добавьте следующую строку:</span><span class="sxs-lookup"><span data-stu-id="8db15-130">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="8db15-131">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="8db15-131">Publish the package</span></span>

<span data-ttu-id="8db15-132">Получив файл `.nupkg`, опубликуйте его на сайте nuget.org, используя команду `dotnet nuget push`, а также ключ API, полученный на этом сайте.</span><span class="sxs-lookup"><span data-stu-id="8db15-132">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="8db15-133">Получение ключа API</span><span class="sxs-lookup"><span data-stu-id="8db15-133">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="8db15-134">Публикация с помощью команды dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="8db15-134">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="8db15-135">Ошибки публикации</span><span class="sxs-lookup"><span data-stu-id="8db15-135">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="8db15-136">Управление опубликованным пакетом</span><span class="sxs-lookup"><span data-stu-id="8db15-136">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a><span data-ttu-id="8db15-137">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="8db15-137">Next steps</span></span>

<span data-ttu-id="8db15-138">Поздравляем! Вы создали пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="8db15-138">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8db15-139">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="8db15-139">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)

<span data-ttu-id="8db15-140">См. подробнее о возможностях NuGet по приведенным ниже ссылкам.</span><span class="sxs-lookup"><span data-stu-id="8db15-140">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="8db15-141">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="8db15-141">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="8db15-142">Пакеты предварительного выпуска</span><span class="sxs-lookup"><span data-stu-id="8db15-142">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="8db15-143">Поддержка нескольких целевых платформ</span><span class="sxs-lookup"><span data-stu-id="8db15-143">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="8db15-144">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="8db15-144">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="8db15-145">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="8db15-145">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="8db15-146">Создание пакетов символов</span><span class="sxs-lookup"><span data-stu-id="8db15-146">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="8db15-147">Подписывание пакетов</span><span class="sxs-lookup"><span data-stu-id="8db15-147">Signing packages</span></span>](../create-packages/Sign-a-package.md)
