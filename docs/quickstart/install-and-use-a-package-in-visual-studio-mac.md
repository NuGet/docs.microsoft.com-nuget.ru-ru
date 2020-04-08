---
title: Установка и использование пакета NuGet в Visual Studio для Mac
description: Узнайте, как установить и использовать пакет NuGet в проекте Visual Studio для Mac.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238480"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a><span data-ttu-id="35af0-103">Краткое руководство. Установка и использование пакета Visual Studio для Mac</span><span class="sxs-lookup"><span data-stu-id="35af0-103">Quickstart: Install and use a package in Visual Studio for Mac</span></span>

<span data-ttu-id="35af0-104">Пакеты NuGet содержат многократно используемый код, предлагаемый другими разработчиками для ваших проектов.</span><span class="sxs-lookup"><span data-stu-id="35af0-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="35af0-105">Дополнительные сведения см. в разделе [Что такое NuGet?](../What-is-NuGet.md).</span><span class="sxs-lookup"><span data-stu-id="35af0-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="35af0-106">Пакеты устанавливаются в проекте Visual Studio для Mac с помощью диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="35af0-106">Packages are installed into a Visual Studio for Mac project using the NuGet Package Manager.</span></span> <span data-ttu-id="35af0-107">В этой статье описано, как использовать популярный пакет [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) и консольный проект .NET Core.</span><span class="sxs-lookup"><span data-stu-id="35af0-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a .NET Core console project.</span></span> <span data-ttu-id="35af0-108">Этот процесс применим к любому другому проекту Xamarin или .NET Core.</span><span class="sxs-lookup"><span data-stu-id="35af0-108">The same process applies to any other Xamarin or .NET Core project.</span></span>

<span data-ttu-id="35af0-109">После установки ссылаться на пакет в коде можно с помощью `using <namespace>`, где \<namespace\> соответствует используемому пакету.</span><span class="sxs-lookup"><span data-stu-id="35af0-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="35af0-110">После указания ссылки можно обращаться к пакету посредством его интерфейса API.</span><span class="sxs-lookup"><span data-stu-id="35af0-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="35af0-111">**Начните работу с сайта nuget.org**: Разработчики .NET обычно находят компоненты, которые можно использовать в собственных приложениях, просматривая сайт *nuget.org*.</span><span class="sxs-lookup"><span data-stu-id="35af0-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="35af0-112">Вы можете выполнить поиск непосредственно на сайте *nuget.org* или найти и установить пакеты в Visual Studio, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="35af0-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="35af0-113">См. подробнее о [поиске и оценке пакетов NuGet](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="35af0-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35af0-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="35af0-114">Prerequisites</span></span>

- <span data-ttu-id="35af0-115">Visual Studio 2019 для Mac.</span><span class="sxs-lookup"><span data-stu-id="35af0-115">Visual Studio 2019 for Mac.</span></span>

<span data-ttu-id="35af0-116">Вы можете установить бесплатный выпуск Community 2019 с сайта [visualstudio.com](https://www.visualstudio.com/) либо использовать выпуск Professional или Enterprise.</span><span class="sxs-lookup"><span data-stu-id="35af0-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="35af0-117">См. сведения об [установке и использовании пакета в Visual Studio в Windows](install-and-use-a-package-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="35af0-117">If you're using Visual Studio on Windows, see [Install and use a package in Visual Studio (Windows Only)](install-and-use-a-package-in-visual-studio.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="35af0-118">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="35af0-118">Create a project</span></span>

<span data-ttu-id="35af0-119">Пакеты NuGet можно установить в проект .NET, если эти пакеты поддерживают ту же требуемую версию .NET Framework, что и проект.</span><span class="sxs-lookup"><span data-stu-id="35af0-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="35af0-120">В этом пошаговом руководстве описано, как использовать консольное приложение .NET Core.</span><span class="sxs-lookup"><span data-stu-id="35af0-120">For this walkthrough, use a simple .NET Core Console app.</span></span> <span data-ttu-id="35af0-121">Создайте проект в Visual Studio для Mac. Для этого выберите **Файл > Создать решение** и щелкните **.NET Core > Приложение > Консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="35af0-121">Create a project in Visual Studio for Mac using **File > New Solution...**, select the **.NET Core > App > Console Application** template.</span></span> <span data-ttu-id="35af0-122">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="35af0-122">Click **Next**.</span></span> <span data-ttu-id="35af0-123">При появлении запроса примите для **целевой платформы** значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="35af0-123">Accept the default values for **Target Framework** when prompted.</span></span>

<span data-ttu-id="35af0-124">Visual Studio создаст проект и откроет его в обозревателе решений.</span><span class="sxs-lookup"><span data-stu-id="35af0-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="35af0-125">Добавление пакета NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="35af0-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="35af0-126">Чтобы установить пакет, используйте диспетчер пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="35af0-126">To install the package, you use the NuGet Package Manager.</span></span> <span data-ttu-id="35af0-127">При установке пакета NuGet регистрирует зависимость в файле проекта или файле `packages.config` (в зависимости от формата проекта).</span><span class="sxs-lookup"><span data-stu-id="35af0-127">When you install a package, NuGet records the dependency in  either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="35af0-128">Дополнительные сведения см. в разделе [Обзор использования пакетов и рабочий процесс](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="35af0-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="35af0-129">Диспетчер пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="35af0-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="35af0-130">В обозревателе решений щелкните правой кнопкой мыши **Зависимости** и выберите **Добавить пакеты**.</span><span class="sxs-lookup"><span data-stu-id="35af0-130">In Solution Explorer, right-click **Dependencies** and choose **Add Packages...**.</span></span>

    ![Пункт "Управление пакетами NuGet" для узла "Ссылки" проекта](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. <span data-ttu-id="35af0-132">Вверху слева выберите nuget.org в качестве **источника пакетов**, выполните поиск по запросу **Newtonsoft.Json**, выберите этот пакет в списке и щелкните **Пакеты**:</span><span class="sxs-lookup"><span data-stu-id="35af0-132">Choose "nuget.org" as the **Package source** in the top left corner of the dialog, and search for **Newtonsoft.Json**, select that package in the list, and select **Add Packages...**:</span></span>

    ![Поиск пакета Newtonsoft.Json](media/QS_Use_Mac-03-NewtonsoftJson.png)

    <span data-ttu-id="35af0-134">См. сведения о диспетчере пакетов NuGet в руководстве по [установке пакетов и управлению ими с помощью Visual Studio для Mac](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="35af0-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="35af0-135">Использование интерфейса API Newtonsoft.Json в приложении</span><span class="sxs-lookup"><span data-stu-id="35af0-135">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="35af0-136">Добавив пакет Newtonsoft.Json в проект, вы можете вызывать его метод `JsonConvert.SerializeObject` для преобразования объекта в удобную для восприятия строку.</span><span class="sxs-lookup"><span data-stu-id="35af0-136">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="35af0-137">Откройте файл `Program.cs` (на Панели решения) и замените его содержимое следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="35af0-137">Open the `Program.cs` file (located in the Solution Pad) and replace the file contents with the following code:</span></span>

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. <span data-ttu-id="35af0-138">Выполните сборку и запустите приложение, щелкнув **Отладка > Начать отладку**:</span><span class="sxs-lookup"><span data-stu-id="35af0-138">Build and run the app by selecting **Run > Start Debugging**:</span></span>

1. <span data-ttu-id="35af0-139">После запуска приложения в консоли отобразятся сериализованные выходные данные JSON:</span><span class="sxs-lookup"><span data-stu-id="35af0-139">Once the app runs, you'll see the serialized JSON output appear in the console:</span></span>

  ![Выходные данные консольного приложения](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a><span data-ttu-id="35af0-141">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="35af0-141">Next steps</span></span>
<span data-ttu-id="35af0-142">Поздравляем! Вы установили пакет NuGet и поработали с ним.</span><span class="sxs-lookup"><span data-stu-id="35af0-142">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="35af0-143">Установка пакетов и управление ими с использованием Visual Studio для Mac</span><span class="sxs-lookup"><span data-stu-id="35af0-143">Install and manage packages using Visual Studio for Mac</span></span>](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

<span data-ttu-id="35af0-144">См. подробнее о возможностях NuGet по приведенным ниже ссылкам.</span><span class="sxs-lookup"><span data-stu-id="35af0-144">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="35af0-145">Общие сведения и процесс использования пакетов</span><span class="sxs-lookup"><span data-stu-id="35af0-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="35af0-146">Ссылки на пакеты в файлах проекта</span><span class="sxs-lookup"><span data-stu-id="35af0-146">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
