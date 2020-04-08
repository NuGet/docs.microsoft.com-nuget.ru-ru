---
title: Установка и использование пакета NuGet с помощью CLI dotnet
description: Пошаговое руководство по установке и использованию пакета NuGet в проекте .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 006fff8360ac62393e4b88c1a253514591d22f4c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231282"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="b68aa-103">Краткое руководство. Установка и использование пакета с помощью dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="b68aa-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="b68aa-104">Пакеты NuGet содержат многократно используемый код, предлагаемый другими разработчиками для ваших проектов.</span><span class="sxs-lookup"><span data-stu-id="b68aa-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="b68aa-105">Дополнительные сведения см. в разделе [Что такое NuGet?](../What-is-NuGet.md).</span><span class="sxs-lookup"><span data-stu-id="b68aa-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="b68aa-106">Пакеты устанавливаются в проект .NET Core с помощью команды `dotnet add package`, как описано в статье о популярном пакете [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).</span><span class="sxs-lookup"><span data-stu-id="b68aa-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="b68aa-107">После установки ссылаться на пакет в коде можно с помощью `using <namespace>`, где \<namespace\> соответствует используемому пакету.</span><span class="sxs-lookup"><span data-stu-id="b68aa-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="b68aa-108">Затем можно использовать API пакета.</span><span class="sxs-lookup"><span data-stu-id="b68aa-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="b68aa-109">**Начните с сайта nuget.org**: разработчики .NET обычно находят компоненты, которые можно использовать в собственных приложениях, просматривая сайт nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b68aa-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="b68aa-110">Вы можете выполнить поиск непосредственно на сайте nuget.org или найти и установить пакеты в Visual Studio, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="b68aa-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b68aa-111">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b68aa-111">Prerequisites</span></span>

- <span data-ttu-id="b68aa-112">[Пакет SDK для .NET Core](https://www.microsoft.com/net/download/), который предоставляет программу командной строки `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="b68aa-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="b68aa-113">Начиная с версии Visual Studio 2017, средство CLI dotnet автоматически устанавливается вместе с любыми рабочими нагрузками, связанными с .NET Core.</span><span class="sxs-lookup"><span data-stu-id="b68aa-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="b68aa-114">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="b68aa-114">Create a project</span></span>

<span data-ttu-id="b68aa-115">Пакеты NuGet могут быть установлены в любой проект .NET.</span><span class="sxs-lookup"><span data-stu-id="b68aa-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="b68aa-116">В рамках этого пошагового руководства создайте простой консольный проект .NET Core следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b68aa-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="b68aa-117">Создайте папку для проекта.</span><span class="sxs-lookup"><span data-stu-id="b68aa-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="b68aa-118">Откройте командную строку и перейдите в новую папку.</span><span class="sxs-lookup"><span data-stu-id="b68aa-118">Open a command prompt and switch to the new folder.</span></span>

1. <span data-ttu-id="b68aa-119">Создайте проект с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="b68aa-119">Create the project using the following command:</span></span>

    ```dotnetcli
    dotnet new console
    ```

1. <span data-ttu-id="b68aa-120">Чтобы проверить, что приложение создано правильно, используйте команду `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="b68aa-120">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="b68aa-121">Добавление пакета NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="b68aa-121">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="b68aa-122">Чтобы установить пакет `Newtonsoft.json`, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b68aa-122">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="b68aa-123">Чтобы увидеть добавленную ссылку, после завершения команды откройте файл `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="b68aa-123">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="b68aa-124">Использование интерфейса API Newtonsoft.Json в приложении</span><span class="sxs-lookup"><span data-stu-id="b68aa-124">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="b68aa-125">Откройте файл `Program.cs` и добавьте вверху файла следующую строку:</span><span class="sxs-lookup"><span data-stu-id="b68aa-125">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="b68aa-126">Перед строкой `class Program` добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="b68aa-126">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="b68aa-127">Замените функцию `Main` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="b68aa-127">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="b68aa-128">Выполните сборку и запуск приложения с помощью команды `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="b68aa-128">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="b68aa-129">В результате вы получите JSON-представление объекта `Account` в коде:</span><span class="sxs-lookup"><span data-stu-id="b68aa-129">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a><span data-ttu-id="b68aa-130">Связанные видео</span><span class="sxs-lookup"><span data-stu-id="b68aa-130">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

<span data-ttu-id="b68aa-131">Другие видео о NuGet см. на [Channel 9](https://channel9.msdn.com/Series/NuGet-101) и [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="b68aa-131">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b68aa-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b68aa-132">Next steps</span></span>

<span data-ttu-id="b68aa-133">Поздравляем! Вы установили пакет NuGet и поработали с ним.</span><span class="sxs-lookup"><span data-stu-id="b68aa-133">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b68aa-134">Установка и использование пакета с помощью CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="b68aa-134">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)

<span data-ttu-id="b68aa-135">См. подробнее о возможностях NuGet по приведенным ниже ссылкам.</span><span class="sxs-lookup"><span data-stu-id="b68aa-135">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="b68aa-136">Общие сведения и процесс использования пакетов</span><span class="sxs-lookup"><span data-stu-id="b68aa-136">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="b68aa-137">Поиск и выбор пакетов</span><span class="sxs-lookup"><span data-stu-id="b68aa-137">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="b68aa-138">Ссылки на пакеты в файлах проекта</span><span class="sxs-lookup"><span data-stu-id="b68aa-138">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
