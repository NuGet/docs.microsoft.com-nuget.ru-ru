---
title: Установка и использование пакета NuGet с помощью CLI dotnet
description: Пошаговое руководство по установке и использованию пакета NuGet в проекте .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: ee456fd49675db37fee78dc14502a897d84a2b99
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342469"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="7d949-103">Краткое руководство. Установка и использование пакета с помощью CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="7d949-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="7d949-104">Пакеты NuGet содержат многократно используемый код, предлагаемый другими разработчиками для ваших проектов.</span><span class="sxs-lookup"><span data-stu-id="7d949-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="7d949-105">Дополнительные сведения см. в разделе [Что такое NuGet?](../What-is-NuGet.md).</span><span class="sxs-lookup"><span data-stu-id="7d949-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="7d949-106">Пакеты устанавливаются в проект .NET Core с помощью команды `dotnet add package`, как описано в статье о популярном пакете [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).</span><span class="sxs-lookup"><span data-stu-id="7d949-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="7d949-107">После установки ссылаться на пакет в коде можно с помощью `using <namespace>`, где \<namespace\> соответствует используемому пакету.</span><span class="sxs-lookup"><span data-stu-id="7d949-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="7d949-108">Затем можно использовать API пакета.</span><span class="sxs-lookup"><span data-stu-id="7d949-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="7d949-109">**Начните работу с сайта nuget.org**: разработчики .NET обычно находят компоненты, которые можно использовать в собственных приложениях, просматривая сайт nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7d949-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="7d949-110">Вы можете выполнить поиск непосредственно на сайте nuget.org или найти и установить пакеты в Visual Studio, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="7d949-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d949-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7d949-111">Prerequisites</span></span>

- <span data-ttu-id="7d949-112">[Пакет SDK для .NET Core](https://www.microsoft.com/net/download/), который предоставляет программу командной строки `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="7d949-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="7d949-113">Начиная с версии Visual Studio 2017, средство CLI dotnet автоматически устанавливается вместе с любыми рабочими нагрузками, связанными с .NET Core.</span><span class="sxs-lookup"><span data-stu-id="7d949-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="7d949-114">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="7d949-114">Create a project</span></span>

<span data-ttu-id="7d949-115">Пакеты NuGet могут быть установлены в любой проект .NET.</span><span class="sxs-lookup"><span data-stu-id="7d949-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="7d949-116">В рамках этого пошагового руководства создайте простой консольный проект .NET Core следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7d949-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="7d949-117">Создайте папку для проекта.</span><span class="sxs-lookup"><span data-stu-id="7d949-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="7d949-118">Создайте проект с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="7d949-118">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="7d949-119">Чтобы проверить, что приложение создано правильно, используйте команду `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="7d949-119">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="7d949-120">Добавление пакета NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="7d949-120">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="7d949-121">Чтобы установить пакет `Newtonsoft.json`, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7d949-121">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="7d949-122">Чтобы увидеть добавленную ссылку, после завершения команды откройте файл `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="7d949-122">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="7d949-123">Использование интерфейса API Newtonsoft.Json в приложении</span><span class="sxs-lookup"><span data-stu-id="7d949-123">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="7d949-124">Откройте файл `Program.cs` и добавьте вверху файла следующую строку:</span><span class="sxs-lookup"><span data-stu-id="7d949-124">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="7d949-125">Перед строкой `class Program` добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="7d949-125">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="7d949-126">Замените функцию `Main` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="7d949-126">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="7d949-127">Выполните сборку и запуск приложения с помощью команды `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="7d949-127">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="7d949-128">В результате вы получите JSON-представление объекта `Account` в коде:</span><span class="sxs-lookup"><span data-stu-id="7d949-128">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="7d949-129">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="7d949-129">Next steps</span></span>

<span data-ttu-id="7d949-130">Поздравляем! Вы установили пакет NuGet и поработали с ним.</span><span class="sxs-lookup"><span data-stu-id="7d949-130">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7d949-131">Установка и использование пакета с помощью CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="7d949-131">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)

<span data-ttu-id="7d949-132">См. подробнее о возможностях NuGet по приведенным ниже ссылкам.</span><span class="sxs-lookup"><span data-stu-id="7d949-132">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="7d949-133">Общие сведения и процесс использования пакетов</span><span class="sxs-lookup"><span data-stu-id="7d949-133">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="7d949-134">Поиск и выбор пакетов</span><span class="sxs-lookup"><span data-stu-id="7d949-134">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="7d949-135">Ссылки на пакеты в файлах проекта</span><span class="sxs-lookup"><span data-stu-id="7d949-135">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
