---
title: "Вводное руководство по созданию и публикации пакета NuGet с помощью интерфейса командной строки dotnet | Документация Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/24/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Пошаговое руководство по созданию и публикации пакета NuGet с помощью .NET Core CLI — dotnet."
keywords: "создание пакетов NuGet, публикация пакетов NuGet, руководство NuGet, публикация пакетов NuGet с помощью dotnet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c9f46cafafcdc238e43979d6f05521e19bf3d7f6
ms.sourcegitcommit: eabd401616a98dda2ae6293612acb3b81b584967
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/09/2018
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="c3789-104">Создание и публикация пакета</span><span class="sxs-lookup"><span data-stu-id="c3789-104">Create and publish a package</span></span>

<span data-ttu-id="c3789-105">Создание пакета NuGet из библиотеки классов .NET и его публикация на сайте nuget.org выполняются очень просто с помощью интерфейса командной строки (CLI) `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="c3789-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="c3789-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c3789-106">Pre-requisites</span></span>

1. <span data-ttu-id="c3789-107">Установите [пакет SDK для .NET Core](https://www.microsoft.com/net/download/), содержащий CLI `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="c3789-107">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span>

1. <span data-ttu-id="c3789-108">[Зарегистрируйтесь для получения бесплатной учетной записи на nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), если вы не сделали этого ранее.</span><span class="sxs-lookup"><span data-stu-id="c3789-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="c3789-109">При создании учетной записи вам направляется сообщение электронной почты с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="c3789-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="c3789-110">Перед отправкой пакета вам нужно подтвердить учетную запись.</span><span class="sxs-lookup"><span data-stu-id="c3789-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="c3789-111">Создание проекта библиотеки классов</span><span class="sxs-lookup"><span data-stu-id="c3789-111">Create a class library project</span></span>

<span data-ttu-id="c3789-112">Вы можете использовать имеющийся проект библиотеки классов .NET для кода, который нужно упаковать, или же создать простой проект, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="c3789-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="c3789-113">Создайте папку с именем `AppLogger` и перейдите в нее.</span><span class="sxs-lookup"><span data-stu-id="c3789-113">Create a folder called `AppLogger` and change into it.</span></span>

1. <span data-ttu-id="c3789-114">Создайте проект с помощью команды `dotnet new classlib`, которая использует имя текущей папки для проекта.</span><span class="sxs-lookup"><span data-stu-id="c3789-114">Create the project using `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="c3789-115">Добавление метаданных пакета в файл проекта</span><span class="sxs-lookup"><span data-stu-id="c3789-115">Add package metadata to the project file</span></span>

<span data-ttu-id="c3789-116">Каждому пакету NuGet нужен манифест, описывающий его содержимое и зависимости.</span><span class="sxs-lookup"><span data-stu-id="c3789-116">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="c3789-117">В итоговом пакете манифестом является файл `.nuspec`, созданный из свойств метаданных NuGet, включенных в файл проекта.</span><span class="sxs-lookup"><span data-stu-id="c3789-117">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="c3789-118">Откройте файл проекта (`.csproj`) и добавьте в него следующие минимальные свойства внутри имеющегося тега `<PropertyGroup>`, изменив значения соответствующим образом:</span><span class="sxs-lookup"><span data-stu-id="c3789-118">Open your project file (`.csproj`) and add the following minimal properties inside the exiting `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="c3789-119">Присвойте пакету идентификатор, уникальный на сайте nuget.org или в другом используемом узле.</span><span class="sxs-lookup"><span data-stu-id="c3789-119">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="c3789-120">При работе с этим руководством мы рекомендуем добавить к имени слово "Sample" или "Test", так как позже, после публикации, пакет станет общедоступным (хотя маловероятно, что кто-то будет его использовать).</span><span class="sxs-lookup"><span data-stu-id="c3789-120">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="c3789-121">Укажите любые дополнительные свойства, описанные в разделе [Свойства метаданных NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="c3789-121">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="c3789-122">Если пакет будет общедоступным, обратите особое внимание на свойство **PackageTags**, так как теги помогают найти ваш пакет и понять его назначение.</span><span class="sxs-lookup"><span data-stu-id="c3789-122">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="c3789-123">Выполнение команды pack</span><span class="sxs-lookup"><span data-stu-id="c3789-123">Run the pack command</span></span>

<span data-ttu-id="c3789-124">Чтобы создать пакет NuGet (файл `.nupkg`) из проекта, запустите команду `dotnet pack`:</span><span class="sxs-lookup"><span data-stu-id="c3789-124">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="c3789-125">В выходных данных будет показан путь к файлу `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="c3789-125">The output will show the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

## <a name="publish-the-package"></a><span data-ttu-id="c3789-126">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="c3789-126">Publish the package</span></span>

<span data-ttu-id="c3789-127">Получив файл `.nupkg`, опубликуйте его на сайте nuget.org, используя команду `dotnet nuget push`, а также ключ API, полученный на этом сайте.</span><span class="sxs-lookup"><span data-stu-id="c3789-127">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="c3789-128">Получение ключа API</span><span class="sxs-lookup"><span data-stu-id="c3789-128">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="c3789-129">Публикация с помощью команды dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="c3789-129">Publish with dotnet nuget push</span></span>

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="c3789-130">Ошибки публикации</span><span class="sxs-lookup"><span data-stu-id="c3789-130">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]


### <a name="manage-the-published-package"></a><span data-ttu-id="c3789-131">Управление опубликованным пакетом</span><span class="sxs-lookup"><span data-stu-id="c3789-131">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="c3789-132">См. также</span><span class="sxs-lookup"><span data-stu-id="c3789-132">Related topics</span></span>

- [<span data-ttu-id="c3789-133">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="c3789-133">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="c3789-134">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="c3789-134">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="c3789-135">Поддержка нескольких целевых платформ</span><span class="sxs-lookup"><span data-stu-id="c3789-135">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="c3789-136">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="c3789-136">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="c3789-137">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="c3789-137">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)