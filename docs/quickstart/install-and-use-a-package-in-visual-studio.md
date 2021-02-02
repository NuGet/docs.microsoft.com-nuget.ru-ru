---
title: Установка и использование пакета NuGet в Visual Studio
description: Пошаговое руководство по установке и использованию пакета NuGet в проекте Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 55f6a64d90ce8ca628d1ac5c68f8133872a214e0
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775533"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a><span data-ttu-id="90992-103">Краткое руководство. Установка и использование пакета в Visual Studio (только в Windows)</span><span class="sxs-lookup"><span data-stu-id="90992-103">Quickstart: Install and use a package in Visual Studio (Windows only)</span></span>

<span data-ttu-id="90992-104">Пакеты NuGet содержат многократно используемый код, предлагаемый другими разработчиками для ваших проектов.</span><span class="sxs-lookup"><span data-stu-id="90992-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="90992-105">Дополнительные сведения см. в разделе [Что такое NuGet?](../What-is-NuGet.md).</span><span class="sxs-lookup"><span data-stu-id="90992-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="90992-106">Пакеты устанавливаются в проекте Visual Studio с помощью диспетчера пакетов NuGet, [консоли диспетчера пакетов](../consume-packages/install-use-packages-powershell.md) или [интерфейса командной строки .NET](install-and-use-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="90992-106">Packages are installed into a Visual Studio project using the NuGet Package Manager, the [Package Manager Console](../consume-packages/install-use-packages-powershell.md), or the [dotnet CLI](install-and-use-a-package-using-the-dotnet-cli.md).</span></span> <span data-ttu-id="90992-107">В этой статье описано, как использовать популярный пакет [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) и проект Windows Presentation Foundation (WPF).</span><span class="sxs-lookup"><span data-stu-id="90992-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Windows Presentation Foundation (WPF) project.</span></span> <span data-ttu-id="90992-108">Тот же процесс применяется к любому другому проекту .NET или .NET Core.</span><span class="sxs-lookup"><span data-stu-id="90992-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="90992-109">После установки ссылаться на пакет в коде можно с помощью `using <namespace>`, где \<namespace\> соответствует используемому пакету.</span><span class="sxs-lookup"><span data-stu-id="90992-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="90992-110">После указания ссылки можно обращаться к пакету посредством его интерфейса API.</span><span class="sxs-lookup"><span data-stu-id="90992-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="90992-111">**Начните работу с сайта nuget.org**: Разработчики .NET обычно находят компоненты, которые можно использовать в собственных приложениях, просматривая сайт *nuget.org*.</span><span class="sxs-lookup"><span data-stu-id="90992-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="90992-112">Вы можете выполнить поиск непосредственно на сайте *nuget.org* или найти и установить пакеты в Visual Studio, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="90992-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="90992-113">См. подробнее о [поиске и оценке пакетов NuGet](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="90992-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90992-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="90992-114">Prerequisites</span></span>

- <span data-ttu-id="90992-115">Использование Visual Studio 2019 с рабочей нагрузкой "Разработка классических приложений .NET".</span><span class="sxs-lookup"><span data-stu-id="90992-115">Visual Studio 2019 with the .NET Desktop Development workload.</span></span>

<span data-ttu-id="90992-116">Вы можете установить бесплатный выпуск Community 2019 с сайта [visualstudio.com](https://www.visualstudio.com/) либо использовать выпуск Professional или Enterprise.</span><span class="sxs-lookup"><span data-stu-id="90992-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="90992-117">См. сведения об [установке и использовании пакета в Visual Studio для Mac](install-and-use-a-package-in-visual-studio-mac.md).</span><span class="sxs-lookup"><span data-stu-id="90992-117">If you're using Visual Studio for Mac, see [Install and use a package in Visual Studio for Mac](install-and-use-a-package-in-visual-studio-mac.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="90992-118">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="90992-118">Create a project</span></span>

<span data-ttu-id="90992-119">Пакеты NuGet можно установить в проект .NET, если эти пакеты поддерживают ту же требуемую версию .NET Framework, что и проект.</span><span class="sxs-lookup"><span data-stu-id="90992-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="90992-120">В этом пошаговом руководстве описано, как использовать простое приложение WPF.</span><span class="sxs-lookup"><span data-stu-id="90992-120">For this walkthrough, use a simple WPF app.</span></span> <span data-ttu-id="90992-121">Создайте проект в Visual Studio, щелкнув **Файл** > **Создать проект** и введя **.NET** в поле поиска. Затем выберите **Приложение WPF (.NET Framework)** .</span><span class="sxs-lookup"><span data-stu-id="90992-121">Create a project in Visual Studio using **File** > **New Project**, typing **.NET** in the search box, and then selecting the **WPF App (.NET Framework)**.</span></span> <span data-ttu-id="90992-122">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="90992-122">Click **Next**.</span></span> <span data-ttu-id="90992-123">При появлении запроса примите значения по умолчанию для **платформы**.</span><span class="sxs-lookup"><span data-stu-id="90992-123">Accept the default values for **Framework** when prompted.</span></span>

<span data-ttu-id="90992-124">Visual Studio создаст проект и откроет его в обозревателе решений.</span><span class="sxs-lookup"><span data-stu-id="90992-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="90992-125">Добавление пакета NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="90992-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="90992-126">Для установки пакета можно использовать диспетчер пакетов NuGet или консоль диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="90992-126">To install the package, you can use either the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="90992-127">При установке пакета NuGet регистрирует зависимость в файле проекта или файле `packages.config` (в зависимости от формата проекта).</span><span class="sxs-lookup"><span data-stu-id="90992-127">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="90992-128">Дополнительные сведения см. в разделе [Обзор использования пакетов и рабочий процесс](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="90992-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="90992-129">Диспетчер пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="90992-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="90992-130">В обозревателе решений щелкните правой кнопкой мыши узел **Ссылки** и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="90992-130">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Пункт "Управление пакетами NuGet" для узла "Ссылки" проекта](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="90992-132">Выберите nuget.org в качестве **источника пакетов**, перейдите на вкладку **Обзор**, выполните поиск по запросу **Newtonsoft.Json**, выберите этот пакет в списке и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="90992-132">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Поиск пакета Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

    <span data-ttu-id="90992-134">См. подробнее о диспетчере пакетов NuGet в руководстве по [установке пакетов и управлении ими с помощью Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="90992-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span></span>

1. <span data-ttu-id="90992-135">Примите все запросы касательно лицензии.</span><span class="sxs-lookup"><span data-stu-id="90992-135">Accept any license prompts.</span></span>

1. <span data-ttu-id="90992-136">(Только в Visual Studio 2017.) Если вам будет предложено выбрать формат управления пакетом, выберите **PackageReference в файле проекта**.</span><span class="sxs-lookup"><span data-stu-id="90992-136">(Visual Studio 2017 only) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Выбор формата управления пакетами](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="90992-138">В запросе на проверку изменений нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="90992-138">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="90992-139">Консоль диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="90992-139">Package Manager Console</span></span>

1. <span data-ttu-id="90992-140">Последовательно выберите **Сервис** > **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="90992-140">Select the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="90992-141">После открытия консоли убедитесь, что в раскрывающемся списке **Проект по умолчанию** показан проект, в который требуется установить пакет.</span><span class="sxs-lookup"><span data-stu-id="90992-141">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="90992-142">Если в решении всего лишь один проект, он автоматически выбран.</span><span class="sxs-lookup"><span data-stu-id="90992-142">If you have a single project in the solution, it is already selected.</span></span>

    ![Выбор проекта для пакета](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="90992-144">Введите команду `Install-Package Newtonsoft.Json` (см. сведения о ней в [этой статье](../reference/ps-reference/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="90992-144">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="90992-145">В окне консоли отображаются выходные данные команды.</span><span class="sxs-lookup"><span data-stu-id="90992-145">The console window shows output for the command.</span></span> <span data-ttu-id="90992-146">Ошибки обычно означают, что пакет не совместим с целевой платформой проекта.</span><span class="sxs-lookup"><span data-stu-id="90992-146">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

   <span data-ttu-id="90992-147">См. подробнее о консоли диспетчера пакетов в руководстве по [установке пакетов и управлении ими с помощью консоли диспетчера пакетов](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="90992-147">If you want more information on the Package Manager Console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="90992-148">Использование интерфейса API Newtonsoft.Json в приложении</span><span class="sxs-lookup"><span data-stu-id="90992-148">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="90992-149">Добавив пакет Newtonsoft.Json в проект, вы можете вызывать его метод `JsonConvert.SerializeObject` для преобразования объекта в удобную для восприятия строку.</span><span class="sxs-lookup"><span data-stu-id="90992-149">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="90992-150">Откройте файл `MainWindow.xaml` и замените существующий элемент `Grid` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="90992-150">Open `MainWindow.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="90992-151">Откройте файл `MainWindow.xaml.cs` (который находится в обозревателе решений в узле `MainWindow.xaml`) и вставьте в класс `MainWindow` следующий код.</span><span class="sxs-lookup"><span data-stu-id="90992-151">Open the `MainWindow.xaml.cs` file (located in Solution Explorer under the `MainWindow.xaml` node), and insert the following code inside the `MainWindow` class:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. <span data-ttu-id="90992-152">Несмотря на то что вы добавили пакет Newtonsoft.Json в проект, `JsonConvert` подчеркивается красной волнистой линией, так как оператор `using` требуется в верхней части файла кода.</span><span class="sxs-lookup"><span data-stu-id="90992-152">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="90992-153">Выполните сборку и запустите приложение, нажав клавишу F5 или выбрав команду **Отладка** > **Начать отладку**.</span><span class="sxs-lookup"><span data-stu-id="90992-153">Build and run the app by pressing F5 or selecting **Debug** > **Start Debugging**:</span></span>

    ![Изначальные выходные данные приложения WPF](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="90992-155">Нажмите кнопку. Надпись TextBlock заменится текстом в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="90992-155">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Выходные данные приложения WPF после нажатия кнопки](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a><span data-ttu-id="90992-157">Связанные видео</span><span class="sxs-lookup"><span data-stu-id="90992-157">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

<span data-ttu-id="90992-158">Другие видео о NuGet см. на [Channel 9](https://channel9.msdn.com/Series/NuGet-101) и [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="90992-158">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="90992-159">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="90992-159">Next steps</span></span>

<span data-ttu-id="90992-160">Поздравляем! Вы установили пакет NuGet и поработали с ним.</span><span class="sxs-lookup"><span data-stu-id="90992-160">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="90992-161">Установка пакетов и управление ими с использованием Visual Studio</span><span class="sxs-lookup"><span data-stu-id="90992-161">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="90992-162">Установка пакетов и управление ими с использованием консоли диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="90992-162">Install and manage packages using Package Manager Console</span></span>](../consume-packages/install-use-packages-powershell.md)

<span data-ttu-id="90992-163">См. подробнее о возможностях NuGet по приведенным ниже ссылкам.</span><span class="sxs-lookup"><span data-stu-id="90992-163">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="90992-164">Общие сведения и процесс использования пакетов</span><span class="sxs-lookup"><span data-stu-id="90992-164">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="90992-165">Поиск и выбор пакетов</span><span class="sxs-lookup"><span data-stu-id="90992-165">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="90992-166">Ссылки на пакеты в файлах проекта</span><span class="sxs-lookup"><span data-stu-id="90992-166">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
