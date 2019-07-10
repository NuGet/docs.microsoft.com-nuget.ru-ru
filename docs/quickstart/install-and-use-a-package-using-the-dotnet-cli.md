---
title: Вводное руководство по использованию пакетов с помощью dotnet CLI
description: Пошаговое руководство по установке и использованию пакета NuGet в проекте .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 1060d98278fed89ac63ee17c1896ae8bdce72a9e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426168"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="cd3a3-103">Краткое руководство. Установка и использование пакета с помощью CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="cd3a3-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="cd3a3-104">Пакеты NuGet содержат многократно используемый код, предлагаемый другими разработчиками для ваших проектов.</span><span class="sxs-lookup"><span data-stu-id="cd3a3-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="cd3a3-105">Дополнительные сведения см. в разделе [Что такое NuGet?](../What-is-NuGet.md).</span><span class="sxs-lookup"><span data-stu-id="cd3a3-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="cd3a3-106">Пакеты устанавливаются в проект .NET Core с помощью команды `dotnet add package`, как описано в статье о популярном пакете [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).</span><span class="sxs-lookup"><span data-stu-id="cd3a3-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="cd3a3-107">После установки ссылаться на пакет в коде можно с помощью `using <namespace>`, где \<namespace\> соответствует используемому пакету.</span><span class="sxs-lookup"><span data-stu-id="cd3a3-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="cd3a3-108">Затем можно использовать API пакета.</span><span class="sxs-lookup"><span data-stu-id="cd3a3-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="cd3a3-109">**Начните работу с сайта nuget.org**: разработчики .NET обычно находят компоненты, которые можно использовать в собственных приложениях, просматривая сайт nuget.org.</span><span class="sxs-lookup"><span data-stu-id="cd3a3-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="cd3a3-110">Вы можете выполнить поиск непосредственно на сайте nuget.org или найти и установить пакеты в Visual Studio, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="cd3a3-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd3a3-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cd3a3-111">Prerequisites</span></span>

- <span data-ttu-id="cd3a3-112">[Пакет SDK для .NET Core](https://www.microsoft.com/net/download/), который предоставляет программу командной строки `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="cd3a3-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="cd3a3-113">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="cd3a3-113">Create a project</span></span>

<span data-ttu-id="cd3a3-114">Пакеты NuGet могут быть установлены в любой проект .NET.</span><span class="sxs-lookup"><span data-stu-id="cd3a3-114">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="cd3a3-115">В рамках этого пошагового руководства создайте простой консольный проект .NET Core следующим образом:</span><span class="sxs-lookup"><span data-stu-id="cd3a3-115">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="cd3a3-116">Создайте папку для проекта.</span><span class="sxs-lookup"><span data-stu-id="cd3a3-116">Create a folder for the project.</span></span>

1. <span data-ttu-id="cd3a3-117">Создайте проект с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="cd3a3-117">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="cd3a3-118">Чтобы проверить, что приложение создано правильно, используйте команду `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="cd3a3-118">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="cd3a3-119">Добавление пакета NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="cd3a3-119">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="cd3a3-120">Чтобы установить пакет `Newtonsoft.json`, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cd3a3-120">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="cd3a3-121">Чтобы увидеть добавленную ссылку, после завершения команды откройте файл `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="cd3a3-121">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="cd3a3-122">Использование интерфейса API Newtonsoft.Json в приложении</span><span class="sxs-lookup"><span data-stu-id="cd3a3-122">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="cd3a3-123">Откройте файл `Program.cs` и добавьте вверху файла следующую строку:</span><span class="sxs-lookup"><span data-stu-id="cd3a3-123">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="cd3a3-124">Перед строкой `class Program` добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="cd3a3-124">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="cd3a3-125">Замените функцию `Main` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="cd3a3-125">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="cd3a3-126">Выполните сборку и запуск приложения с помощью команды `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="cd3a3-126">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="cd3a3-127">В результате вы получите JSON-представление объекта `Account` в коде:</span><span class="sxs-lookup"><span data-stu-id="cd3a3-127">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="cd3a3-128">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="cd3a3-128">Related articles</span></span>

- [<span data-ttu-id="cd3a3-129">Установка и использование пакета с помощью CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="cd3a3-129">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)
- [<span data-ttu-id="cd3a3-130">Общие сведения и процесс использования пакетов</span><span class="sxs-lookup"><span data-stu-id="cd3a3-130">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="cd3a3-131">Поиск и выбор пакетов</span><span class="sxs-lookup"><span data-stu-id="cd3a3-131">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="cd3a3-132">Распространенные конфигурации NuGet</span><span class="sxs-lookup"><span data-stu-id="cd3a3-132">Common NuGet configurations</span></span>](../consume-packages/configuring-nuget-behavior.md)
