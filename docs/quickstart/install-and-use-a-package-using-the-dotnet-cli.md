---
title: Вводное руководство по использованию пакетов с помощью dotnet CLI
description: Пошаговое руководство по установке и использованию пакета NuGet в проекте .NET Core.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 2fac013de5457f26bbbaeff37209316daedcdbb0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816947"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="5b6f2-103">Краткое руководство. Установка и использование пакета с помощью dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="5b6f2-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="5b6f2-104">Пакеты NuGet содержат многократно используемый код, предлагаемый другими разработчиками для ваших проектов.</span><span class="sxs-lookup"><span data-stu-id="5b6f2-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="5b6f2-105">Дополнительные сведения см. в разделе [Что такое NuGet?](../What-is-NuGet.md).</span><span class="sxs-lookup"><span data-stu-id="5b6f2-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="5b6f2-106">Пакеты устанавливаются в проект .NET Core с помощью команды `dotnet add package`, как описано в статье о популярном пакете [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).</span><span class="sxs-lookup"><span data-stu-id="5b6f2-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="5b6f2-107">После установки ссылаться на пакет в коде можно с помощью `using <namespace>`, где \<namespace\> соответствует используемому пакету.</span><span class="sxs-lookup"><span data-stu-id="5b6f2-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="5b6f2-108">Затем можно использовать API пакета.</span><span class="sxs-lookup"><span data-stu-id="5b6f2-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="5b6f2-109">**Начните с сайта nuget.org**: разработчики .NET обычно находят компоненты, которые можно использовать в собственных приложениях, просматривая сайт nuget.org.</span><span class="sxs-lookup"><span data-stu-id="5b6f2-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="5b6f2-110">Вы можете выполнить поиск непосредственно на сайте nuget.org или найти и установить пакеты в Visual Studio, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="5b6f2-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b6f2-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5b6f2-111">Prerequisites</span></span>

- <span data-ttu-id="5b6f2-112">[Пакет SDK для .NET Core](https://www.microsoft.com/net/download/), который предоставляет программу командной строки `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="5b6f2-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="5b6f2-113">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="5b6f2-113">Create a project</span></span>

<span data-ttu-id="5b6f2-114">Пакеты NuGet могут быть установлены в любой проект .NET.</span><span class="sxs-lookup"><span data-stu-id="5b6f2-114">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="5b6f2-115">В рамках этого пошагового руководства создайте простой консольный проект .NET Core следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5b6f2-115">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="5b6f2-116">Создайте папку для проекта.</span><span class="sxs-lookup"><span data-stu-id="5b6f2-116">Create a folder for the project.</span></span>

1. <span data-ttu-id="5b6f2-117">Создайте проект с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="5b6f2-117">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="5b6f2-118">Чтобы проверить, что приложение создано правильно, используйте команду `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="5b6f2-118">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="5b6f2-119">Добавление пакета NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="5b6f2-119">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="5b6f2-120">Чтобы установить пакет `Newtonsoft.json`, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5b6f2-120">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="5b6f2-121">Чтобы увидеть добавленную ссылку, после завершения команды откройте файл `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="5b6f2-121">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="5b6f2-122">Использование интерфейса API Newtonsoft.Json в приложении</span><span class="sxs-lookup"><span data-stu-id="5b6f2-122">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="5b6f2-123">Откройте файл `Program.cs` и добавьте вверху файла следующую строку:</span><span class="sxs-lookup"><span data-stu-id="5b6f2-123">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="5b6f2-124">Перед строкой `class Program` добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="5b6f2-124">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="5b6f2-125">Замените функцию `Main` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="5b6f2-125">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="5b6f2-126">Выполните сборку и запуск приложения с помощью команды `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="5b6f2-126">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="5b6f2-127">В результате вы получите JSON-представление объекта `Account` в коде:</span><span class="sxs-lookup"><span data-stu-id="5b6f2-127">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="5b6f2-128">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="5b6f2-128">Related articles</span></span>

- [<span data-ttu-id="5b6f2-129">Общие сведения и процесс использования пакетов</span><span class="sxs-lookup"><span data-stu-id="5b6f2-129">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="5b6f2-130">Поиск и выбор пакетов</span><span class="sxs-lookup"><span data-stu-id="5b6f2-130">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="5b6f2-131">Способы установки пакета NuGet</span><span class="sxs-lookup"><span data-stu-id="5b6f2-131">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="5b6f2-132">Настройка поведения NuGet</span><span class="sxs-lookup"><span data-stu-id="5b6f2-132">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
