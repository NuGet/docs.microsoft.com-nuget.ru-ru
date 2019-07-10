---
title: Вводное руководство по использованию пакетов NuGet в Visual Studio
description: Пошаговое руководство по установке и использованию пакета NuGet в проекте Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 014b316ea03b45584406c313d46b96ad36340124
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426234"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="222fd-103">Краткое руководство. Установка и использование пакета в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="222fd-103">Quickstart: Install and use a package in Visual Studio</span></span>

<span data-ttu-id="222fd-104">Пакеты NuGet содержат многократно используемый код, предлагаемый другими разработчиками для ваших проектов.</span><span class="sxs-lookup"><span data-stu-id="222fd-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="222fd-105">Дополнительные сведения см. в разделе [Что такое NuGet?](../What-is-NuGet.md).</span><span class="sxs-lookup"><span data-stu-id="222fd-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="222fd-106">Пакеты устанавливаются в проект Visual Studio с помощью пользовательского интерфейса или консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="222fd-106">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="222fd-107">В этой статье описан процесс с использованием популярного пакета [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) и проекта универсальной платформы Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="222fd-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="222fd-108">Тот же процесс применяется к любому другому проекту .NET или .NET Core.</span><span class="sxs-lookup"><span data-stu-id="222fd-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="222fd-109">После установки ссылаться на пакет в коде можно с помощью `using <namespace>`, где \<namespace\> соответствует используемому пакету.</span><span class="sxs-lookup"><span data-stu-id="222fd-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="222fd-110">После указания ссылки можно обращаться к пакету посредством его интерфейса API.</span><span class="sxs-lookup"><span data-stu-id="222fd-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="222fd-111">**Начните работу с сайта nuget.org**: разработчики .NET обычно находят компоненты, которые можно использовать в собственных приложениях, просматривая сайт nuget.org.</span><span class="sxs-lookup"><span data-stu-id="222fd-111">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="222fd-112">Вы можете выполнить поиск непосредственно на сайте nuget.org или найти и установить пакеты в Visual Studio, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="222fd-112">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="222fd-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="222fd-113">Prerequisites</span></span>

- <span data-ttu-id="222fd-114">Visual Studio 2017 с рабочей нагрузкой универсальной платформы Windows или</span><span class="sxs-lookup"><span data-stu-id="222fd-114">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="222fd-115">Visual Studio 2015 с обновлением 3 и инструментами для разработки универсальных приложений для Windows.</span><span class="sxs-lookup"><span data-stu-id="222fd-115">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="222fd-116">Вы можете установить бесплатный выпуск Community 2017 с сайта [visualstudio.com](https://www.visualstudio.com/) либо использовать выпуск Professional или Enterprise.</span><span class="sxs-lookup"><span data-stu-id="222fd-116">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="222fd-117">Если вы используете Visual Studio для Mac, см. статью [Включение пакета NuGet в проект](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="222fd-117">If you're using Visual Studio for Mac, see [Include a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="222fd-118">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="222fd-118">Create a project</span></span>

<span data-ttu-id="222fd-119">Пакеты NuGet можно установить в проект .NET, если эти пакеты поддерживают ту же требуемую версию .NET Framework, что и проект.</span><span class="sxs-lookup"><span data-stu-id="222fd-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="222fd-120">В этом пошаговом руководстве используется простое приложение универсальной Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="222fd-120">For this walkthrough, use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="222fd-121">Создайте проект в Visual Studio, выбрав пункты **Файл > Новый проект...**, а затем — **Универсальные приложения Windows > Пустое приложение (универсальное приложение для Windows)**.</span><span class="sxs-lookup"><span data-stu-id="222fd-121">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="222fd-122">При появлении запроса оставьте значения свойств "Конечная версия" и "Минимальная версия" по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="222fd-122">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="222fd-123">Добавление пакета NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="222fd-123">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="222fd-124">Для установки пакета можно использовать пользовательский интерфейс или консоль диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="222fd-124">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="222fd-125">При установке пакета NuGet регистрирует зависимость в файле проекта или файле `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="222fd-125">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="222fd-126">Дополнительные сведения см. в разделе [Обзор использования пакетов и рабочий процесс](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="222fd-126">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="222fd-127">Пользовательский интерфейс диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="222fd-127">Package Manager UI</span></span>

1. <span data-ttu-id="222fd-128">В обозревателе решений щелкните правой кнопкой мыши узел **Ссылки** и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="222fd-128">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Пункт "Управление пакетами NuGet" для узла "Ссылки" проекта](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="222fd-130">Выберите nuget.org в качестве **источника пакетов**, перейдите на вкладку **Обзор**, выполните поиск по запросу **Newtonsoft.Json**, выберите этот пакет в списке и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="222fd-130">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Поиск пакета Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="222fd-132">Примите все запросы касательно лицензии.</span><span class="sxs-lookup"><span data-stu-id="222fd-132">Accept any license prompts.</span></span>

1. <span data-ttu-id="222fd-133">(Visual Studio 2017.) Если вам будет предложено выбрать формат управления пакетом, выберите **PackageReference в файле проекта**.</span><span class="sxs-lookup"><span data-stu-id="222fd-133">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Выбор формата управления пакетами](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="222fd-135">В запросе на проверку изменений нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="222fd-135">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="222fd-136">Консоль диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="222fd-136">Package Manager Console</span></span>

1. <span data-ttu-id="222fd-137">Выберите команды меню **Сервис > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="222fd-137">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="222fd-138">После открытия консоли убедитесь, что в раскрывающемся списке **Проект по умолчанию** показан проект, в который требуется установить пакет.</span><span class="sxs-lookup"><span data-stu-id="222fd-138">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="222fd-139">Если в решении всего лишь один проект, он автоматически выбран.</span><span class="sxs-lookup"><span data-stu-id="222fd-139">If you have a single project in the solution, it is already selected.</span></span>

    ![Поиск пакета Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="222fd-141">Введите команду `Install-Package Newtonsoft.Json` (см. сведения о ней в [этой статье](../tools/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="222fd-141">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../tools/ps-ref-install-package.md)).</span></span> <span data-ttu-id="222fd-142">В окне консоли отображаются выходные данные команды.</span><span class="sxs-lookup"><span data-stu-id="222fd-142">The console window shows output for the command.</span></span> <span data-ttu-id="222fd-143">Ошибки обычно означают, что пакет не совместим с целевой платформой проекта.</span><span class="sxs-lookup"><span data-stu-id="222fd-143">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="222fd-144">Использование интерфейса API Newtonsoft.Json в приложении</span><span class="sxs-lookup"><span data-stu-id="222fd-144">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="222fd-145">Добавив пакет Newtonsoft.Json в проект, вы можете вызывать его метод `JsonConvert.SerializeObject` для преобразования объекта в удобную для восприятия строку.</span><span class="sxs-lookup"><span data-stu-id="222fd-145">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="222fd-146">Откройте файл `MainPage.xaml` и замените существующий элемент `Grid` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="222fd-146">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="222fd-147">Откройте файл `MainPage.xaml.cs` (который находится в обозревателе решений в узле `MainPage.xaml`) и вставьте в конструктор `MainPage` следующий код:</span><span class="sxs-lookup"><span data-stu-id="222fd-147">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

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

1. <span data-ttu-id="222fd-148">Несмотря на то что вы добавили пакет Newtonsoft.Json в проект, `JsonConvert` подчеркивается красной волнистой линией, так как оператор `using` требуется в верхней части файла кода.</span><span class="sxs-lookup"><span data-stu-id="222fd-148">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="222fd-149">Выполните сборку и запустите приложение, нажав клавишу F5 или выбрав команду **Отладка > Начать отладку**.</span><span class="sxs-lookup"><span data-stu-id="222fd-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![Изначальные выходные данные приложения UWP](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="222fd-151">Нажмите кнопку. Надпись TextBlock заменится текстом в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="222fd-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Выходные данные приложения UWP после нажатия кнопки](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="222fd-153">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="222fd-153">Related articles</span></span>

- [<span data-ttu-id="222fd-154">Общие сведения и процесс использования пакетов</span><span class="sxs-lookup"><span data-stu-id="222fd-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="222fd-155">Установка пакетов и управление ими с использованием Visual Studio</span><span class="sxs-lookup"><span data-stu-id="222fd-155">Install and manage packages using Visual Studio</span></span>](../tools/package-manager-ui.md)
- [<span data-ttu-id="222fd-156">Поиск и выбор пакетов</span><span class="sxs-lookup"><span data-stu-id="222fd-156">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="222fd-157">Распространенные конфигурации NuGet</span><span class="sxs-lookup"><span data-stu-id="222fd-157">Common NuGet configurations</span></span>](../consume-packages/configuring-nuget-behavior.md)
