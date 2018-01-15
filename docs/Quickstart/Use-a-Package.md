---
title: "Вводное руководство по использованию пакетов NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: f31f8259-20a8-4617-880e-5819299372d2
description: "Пошаговое руководство по установке и использованию пакета NuGet в проекте."
keywords: "установка NuGet, использование пакета NuGet, установка пакетов NuGet, ссылки на пакеты NuGet, использование пакетов NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 639f4883f5ce904a44d8aa23d76c93ed79ea4b9d
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/10/2018
---
# <a name="install-and-use-a-package"></a><span data-ttu-id="70ca5-104">Установка и использование пакета</span><span class="sxs-lookup"><span data-stu-id="70ca5-104">Install and use a package</span></span>

<span data-ttu-id="70ca5-105">Пакеты NuGet — это единицы многократно используемого кода, предлагаемые другими разработчиками для ваших проектов.</span><span class="sxs-lookup"><span data-stu-id="70ca5-105">NuGet packages are units of reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="70ca5-106">Дополнительные сведения см. в разделе [Что такое NuGet?](../What-is-NuGet.md).</span><span class="sxs-lookup"><span data-stu-id="70ca5-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span>

[!INCLUDE [install-methods](../includes/install-methods.md)]

<span data-ttu-id="70ca5-107">После установки ссылаться на пакет в коде можно с помощью `using <namespace>`, где \<namespace\> соответствует используемому пакету.</span><span class="sxs-lookup"><span data-stu-id="70ca5-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="70ca5-108">После указания ссылки можно обращаться к пакету посредством его интерфейса API.</span><span class="sxs-lookup"><span data-stu-id="70ca5-108">Once the reference is made, you can call the package through its API.</span></span>

<span data-ttu-id="70ca5-109">В оставшейся части этого раздела поэтапно рассматривается процесс установки популярного пакета [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) в проекте универсальной платформы Windows (UWP) с помощью пользовательского интерфейса диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="70ca5-109">The remainder of this topic walks through the process of using the Package Manager UI to install the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package in a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="70ca5-110">Далее приводится пример использования пакета.</span><span class="sxs-lookup"><span data-stu-id="70ca5-110">It then shows an example of using the package.</span></span> <span data-ttu-id="70ca5-111">Аналогичный процесс используется практически для любого пакета NuGet в проектах.</span><span class="sxs-lookup"><span data-stu-id="70ca5-111">You use a similar same workflow for virtually every NuGet package you use in a project.</span></span>

- [<span data-ttu-id="70ca5-112">Установка необходимых компонентов</span><span class="sxs-lookup"><span data-stu-id="70ca5-112">Install pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="70ca5-113">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="70ca5-113">Create a project</span></span>](#create-a-project)
- [<span data-ttu-id="70ca5-114">Добавление пакета NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="70ca5-114">Add the Newtonsoft.Json NuGet package</span></span>](#add-the-newtonsoftjson-nuget-package)
- [<span data-ttu-id="70ca5-115">Использование интерфейса API Newtonsoft.Json в приложении</span><span class="sxs-lookup"><span data-stu-id="70ca5-115">Use the Newtonsoft.Json API in the app</span></span>](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> <span data-ttu-id="70ca5-116">**Начните работу с nuget.org**: разработчики приложений .NET часто устанавливают пакеты с сайта nuget.org. Здесь можно найти компоненты для использования в собственных приложениях.</span><span class="sxs-lookup"><span data-stu-id="70ca5-116">**Start with nuget.org**: Installing packages from nuget.org is a common workflow that .NET developers use to find components they can reuse in their own applications.</span></span> <span data-ttu-id="70ca5-117">Вы можете выполнить поиск непосредственно на сайте nuget.org или найти и установить пакеты в Visual Studio, как описано в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="70ca5-117">You can always search nuget.org directly or find and install packages within Visual Studio as shown in this topic.</span></span>

## <a name="install-pre-requisites"></a><span data-ttu-id="70ca5-118">Установка необходимых компонентов</span><span class="sxs-lookup"><span data-stu-id="70ca5-118">Install pre-requisites</span></span>

<span data-ttu-id="70ca5-119">Для прохождения этого учебника требуется Visual Studio 2015 с обновлением 3 и инструментами для универсальных приложений Windows или Visual Studio 2017 с рабочей нагрузкой "Разработка приложений для универсальной платформы Windows".</span><span class="sxs-lookup"><span data-stu-id="70ca5-119">This tutorial requires Visual Studio 2015 Update 3 with Tools for Universal Windows Apps, or Visual Studio 2017 with the Universal Windows Platform development workload.</span></span> <span data-ttu-id="70ca5-120">Если среда Visual Studio уже установлена, вы можете снова запустить установщик, чтобы установить инструменты для универсальной платформы Windows.</span><span class="sxs-lookup"><span data-stu-id="70ca5-120">If you already have Visual Studio installed, you can run the installer again to add the UWP tools.</span></span>

<span data-ttu-id="70ca5-121">Вы можете установить бесплатный выпуск Community с сайта [visualstudio.com](https://www.visualstudio.com/) либо использовать выпуск Professional или Enterprise.</span><span class="sxs-lookup"><span data-stu-id="70ca5-121">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span> 

## <a name="create-a-project"></a><span data-ttu-id="70ca5-122">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="70ca5-122">Create a project</span></span>

<span data-ttu-id="70ca5-123">Для установки пакета NuGet требуется какой-либо проект на основе .NET в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="70ca5-123">To install a NuGet package, you need some kind of .NET-based project in Visual Studio.</span></span> <span data-ttu-id="70ca5-124">В этом пошаговом руководстве можно использовать простое приложение Windows Presentation Foundation (WPF) или приложение универсальной платформы Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="70ca5-124">For this walkthrough, you can use use a simple Windows Presentation Foundation (WPF) or Universal Windows (UWP) app:</span></span>

- <span data-ttu-id="70ca5-125">Для создания приложения WPF (Windows 7 или более поздней версии) последовательно выберите **Файл > Создать > Проект**, разверните узел **Visual C#**, выберите шаблон **Классический рабочий стол Windows > Приложение WPF (.NET Framework)** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="70ca5-125">For WPF (Windows 7+), choose **File > New > Project**, expand **Visual C#**, select **Windows Classic Desktop > WPF App (.NET Framework)**, and select **OK**.</span></span>
- <span data-ttu-id="70ca5-126">Для создания приложения UWP (Windows 10) используйте вместо этого шаблон **Универсальные приложения Windows > Пустое приложение (универсальное приложение Windows)**.</span><span class="sxs-lookup"><span data-stu-id="70ca5-126">For UWP (Windows 10), use the **Windows Universal > Blank App (Universal Windows)** instead.</span></span> <span data-ttu-id="70ca5-127">При появлении запроса оставьте значения свойств "Конечная версия" и "Минимальная версия" по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="70ca5-127">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="70ca5-128">Добавление пакета NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="70ca5-128">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="70ca5-129">В обозревателе решений щелкните правой кнопкой мыши узел **Ссылки** и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="70ca5-129">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Пункт "Управление пакетами NuGet" для узла "Ссылки" проекта](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="70ca5-131">Выберите nuget.org в качестве **источника пакетов**, перейдите на вкладку **Обзор**, выполните поиск по запросу **Newtonsoft.Json**, выберите этот пакет в списке и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="70ca5-131">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Поиск пакета Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="70ca5-133">Если появится запрос на выбор формата диспетчера пакетов, выберите PackageReference (рекомендуется) или `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="70ca5-133">If prompted to select a package management format, choose between PackageReference (recommended) and `packages.config`:</span></span>

    ![Выбор формата ссылок на пакеты](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="70ca5-135">В запросе на проверку изменений нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="70ca5-135">If prompted to review changes, select **OK**.</span></span>

1. <span data-ttu-id="70ca5-136">В обозревателе решений щелкните решение правой кнопкой мыши и выберите пункт **Собрать решение**.</span><span class="sxs-lookup"><span data-stu-id="70ca5-136">Right-click the solution in Solution Explorer and select **Build Solution**.</span></span> <span data-ttu-id="70ca5-137">При этом будут восстановлены все пакеты NuGet, перечисленные в узле **Ссылки**.</span><span class="sxs-lookup"><span data-stu-id="70ca5-137">This restores any NuGet packages listed under **References**.</span></span> <span data-ttu-id="70ca5-138">Дополнительные сведения см. в разделе [Восстановление пакета](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="70ca5-138">For more details, see [Package Restore](../consume-packages/package-restore.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="70ca5-139">Использование интерфейса API Newtonsoft.Json в приложении</span><span class="sxs-lookup"><span data-stu-id="70ca5-139">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="70ca5-140">Добавив пакет Newtonsoft.Json в проект, вы можете вызывать его метод `JsonConvert.SerializeObject` для преобразования объекта в удобную для восприятия строку.</span><span class="sxs-lookup"><span data-stu-id="70ca5-140">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="70ca5-141">Откройте файл `MainWindow.xaml` (WPF) или `MainPage.xaml` (UWP) и замените существующий элемент `Grid` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="70ca5-141">Open `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="70ca5-142">В обозревателе решений разверните узел `MainWindow.xaml` (WPF) или `MainPage.xaml` (UWP), откройте файл `.cs` и вставьте следующий код внутри класса `MainWindow` или `MainPage` после конструктора:</span><span class="sxs-lookup"><span data-stu-id="70ca5-142">Expand the `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) node in Solution Explorer, open the `.cs` file, and insert the following code inside the `MainWindow` or `MainPage` class, after the constructor:</span></span>

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

1. <span data-ttu-id="70ca5-143">Несмотря на то, что вы добавили пакет Newtonsoft.Json в проект, `JsonConvert` подчеркивается красной волнистой линией, так как требуется оператор `using`.</span><span class="sxs-lookup"><span data-stu-id="70ca5-143">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement.</span></span> <span data-ttu-id="70ca5-144">Наведите указатель мыши на подчеркнутое слово `JsonConvert`, и вы увидите кнопку со значком лампочки и ссылку **Показать возможные решения**.</span><span class="sxs-lookup"><span data-stu-id="70ca5-144">Hover over the underlined `JsonConvert` and you'll see the Lightbulb and the option to **Show potential fixes**:</span></span>

    ![Кнопка со значком лампочки и ссылка "Показать возможные решения"](media/QS_Use-04-ShowPotentialFixes.png)


1. <span data-ttu-id="70ca5-146">Щелкните ссылку **Показать возможные решения** (или нажмите кнопку со значком лампочки) и выберите первое предложенное исправление (`using Newtonsoft.Json;`).</span><span class="sxs-lookup"><span data-stu-id="70ca5-146">Click on **Show potential fixes** (or the Lightbulb) and select the first suggested fix, `using Newtonsoft.Json;`.</span></span> <span data-ttu-id="70ca5-147">В начало файла добавится необходимая строка.</span><span class="sxs-lookup"><span data-stu-id="70ca5-147">This adds the necessary line to the top of the file.</span></span>

    ![В список исправлений с предложением добавить оператор using](media/QS_Use-05-AddUsing.png)

1. <span data-ttu-id="70ca5-149">Выполните сборку и запустите приложение, нажав клавишу F5 или выбрав команду **Отладка > Начать отладку** (ниже показано приложение UWP; приложение WPF выглядит аналогично).</span><span class="sxs-lookup"><span data-stu-id="70ca5-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging** (UWP shown here; WPF is similar):</span></span>

    ![Изначальные выходные данные приложения UWP](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="70ca5-151">Нажмите кнопку. Надпись TextBlock заменится текстом в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="70ca5-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Выходные данные приложения UWP после нажатия кнопки](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a><span data-ttu-id="70ca5-153">См. также</span><span class="sxs-lookup"><span data-stu-id="70ca5-153">Related topics</span></span>

- [<span data-ttu-id="70ca5-154">Общие сведения и процесс использования пакетов</span><span class="sxs-lookup"><span data-stu-id="70ca5-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="70ca5-155">Поиск и выбор пакетов</span><span class="sxs-lookup"><span data-stu-id="70ca5-155">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="70ca5-156">Настройка поведения NuGet</span><span class="sxs-lookup"><span data-stu-id="70ca5-156">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
