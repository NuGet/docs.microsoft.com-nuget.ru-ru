---
title: Установка и использование пакетов с помощью CLI dotnet | Документация Майкрософт
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: quickstart
ms.prod: nuget
ms.technology: ''
description: Пошаговое руководство по установке и использованию пакета NuGet в проекте .NET Core.
keywords: установка NuGet, использование пакета NuGet, установка пакетов NuGet, ссылки на пакеты NuGet, использование пакетов NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 87a37a733ebbbbf9bc161247b657a69f30ed4fb3
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="9fba4-104">Установка и использование пакета с помощью CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="9fba4-104">Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="9fba4-105">Пакеты NuGet содержат многократно используемый код, предлагаемый другими разработчиками для ваших проектов.</span><span class="sxs-lookup"><span data-stu-id="9fba4-105">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="9fba4-106">Дополнительные сведения см. в разделе [Что такое NuGet?](../What-is-NuGet.md).</span><span class="sxs-lookup"><span data-stu-id="9fba4-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="9fba4-107">Пакеты устанавливаются в проект .NET Core с помощью команды `dotnet add package`, как описано в статье о популярном пакете [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).</span><span class="sxs-lookup"><span data-stu-id="9fba4-107">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="9fba4-108">После установки ссылаться на пакет в коде можно с помощью `using <namespace>`, где \<namespace\> соответствует используемому пакету.</span><span class="sxs-lookup"><span data-stu-id="9fba4-108">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="9fba4-109">Затем можно использовать API пакета.</span><span class="sxs-lookup"><span data-stu-id="9fba4-109">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="9fba4-110">**Начните с сайта nuget.org**: разработчики .NET обычно находят компоненты, которые можно использовать в собственных приложениях, просматривая сайт nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9fba4-110">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="9fba4-111">Вы можете выполнить поиск непосредственно на сайте nuget.org или найти и установить пакеты в Visual Studio, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="9fba4-111">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fba4-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9fba4-112">Prerequisites</span></span>

- <span data-ttu-id="9fba4-113">[Пакет SDK для .NET Core](https://www.microsoft.com/net/download/), который предоставляет программу командной строки `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="9fba4-113">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="9fba4-114">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="9fba4-114">Create a project</span></span>

<span data-ttu-id="9fba4-115">Пакеты NuGet могут быть установлены в любой проект .NET.</span><span class="sxs-lookup"><span data-stu-id="9fba4-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="9fba4-116">В рамках этого пошагового руководства создайте простой консольный проект .NET Core следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9fba4-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="9fba4-117">Создайте папку для проекта.</span><span class="sxs-lookup"><span data-stu-id="9fba4-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="9fba4-118">Создайте проект с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="9fba4-118">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="9fba4-119">Чтобы проверить, что приложение создано правильно, используйте команду `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="9fba4-119">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="9fba4-120">Добавление пакета NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="9fba4-120">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="9fba4-121">Чтобы установить пакет `Newtonsoft.json`, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9fba4-121">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

1. <span data-ttu-id="9fba4-122">Чтобы увидеть добавленную ссылку, после завершения команды откройте файл `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="9fba4-122">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
  </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="9fba4-123">Использование интерфейса API Newtonsoft.Json в приложении</span><span class="sxs-lookup"><span data-stu-id="9fba4-123">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="9fba4-124">Откройте файл `Program.cs` и добавьте вверху файла следующую строку:</span><span class="sxs-lookup"><span data-stu-id="9fba4-124">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="9fba4-125">Перед строкой `class Program` добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="9fba4-125">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="9fba4-126">Замените функцию `Main` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="9fba4-126">Replace the `Main` function with the following:</span></span>

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. <span data-ttu-id="9fba4-127">Выполните сборку и запуск приложения с помощью команды `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="9fba4-127">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="9fba4-128">В результате вы получите JSON-представление объекта `Account` в коде:</span><span class="sxs-lookup"><span data-stu-id="9fba4-128">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="9fba4-129">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="9fba4-129">Related articles</span></span>

- [<span data-ttu-id="9fba4-130">Общие сведения и процесс использования пакетов</span><span class="sxs-lookup"><span data-stu-id="9fba4-130">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="9fba4-131">Поиск и выбор пакетов</span><span class="sxs-lookup"><span data-stu-id="9fba4-131">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="9fba4-132">Способы установки пакета NuGet</span><span class="sxs-lookup"><span data-stu-id="9fba4-132">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="9fba4-133">Настройка поведения NuGet</span><span class="sxs-lookup"><span data-stu-id="9fba4-133">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
