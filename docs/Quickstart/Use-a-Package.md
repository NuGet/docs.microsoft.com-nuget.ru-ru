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
ms.openlocfilehash: bcccc7139de31a8d07e9ed52abfd12fe9e6d687b
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="install-and-use-a-package"></a><span data-ttu-id="8172f-104">Установка и использование пакета</span><span class="sxs-lookup"><span data-stu-id="8172f-104">Install and use a package</span></span>

[!INCLUDE [install-methods](../includes/install-methods.md)]

<span data-ttu-id="8172f-105">После установки ссылаться на пакет в коде можно с помощью `using <namespace>`, где \<namespace\> соответствует используемому пакету.</span><span class="sxs-lookup"><span data-stu-id="8172f-105">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="8172f-106">После указания ссылки можно обращаться к пакету посредством его интерфейса API.</span><span class="sxs-lookup"><span data-stu-id="8172f-106">Once the reference is made, you can call the package through its API.</span></span>

<span data-ttu-id="8172f-107">В оставшейся части этого раздела поэтапно рассматривается процесс установки популярного пакета [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) в проекте универсальной платформы Windows (UWP) с помощью пользовательского интерфейса диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="8172f-107">The remainder of this topic walks through the process of using the Package Manager UI to install the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package in a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="8172f-108">Далее приводится пример использования пакета.</span><span class="sxs-lookup"><span data-stu-id="8172f-108">It then shows an example of using the package.</span></span> <span data-ttu-id="8172f-109">Аналогичный процесс используется практически для любого пакета NuGet в проектах.</span><span class="sxs-lookup"><span data-stu-id="8172f-109">You use a similar same workflow for virtually every NuGet package you use in a project.</span></span>

- [<span data-ttu-id="8172f-110">Установка необходимых компонентов</span><span class="sxs-lookup"><span data-stu-id="8172f-110">Install pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="8172f-111">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="8172f-111">Create a project</span></span>](#create-a-project)
- [<span data-ttu-id="8172f-112">Добавление пакета NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="8172f-112">Add the Newtonsoft.Json NuGet package</span></span>](#add-the-newtonsoftjson-nuget-package)
- [<span data-ttu-id="8172f-113">Использование интерфейса API Newtonsoft.Json в приложении</span><span class="sxs-lookup"><span data-stu-id="8172f-113">Use the Newtonsoft.Json API in the app</span></span>](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> <span data-ttu-id="8172f-114">**Начните работу с nuget.org**: разработчики приложений .NET часто устанавливают пакеты с сайта nuget.org. Здесь можно найти компоненты для использования в собственных приложениях.</span><span class="sxs-lookup"><span data-stu-id="8172f-114">**Start with nuget.org**: Installing packages from nuget.org is a common workflow that .NET developers use to find components they can reuse in their own applications.</span></span> <span data-ttu-id="8172f-115">Вы можете выполнить поиск непосредственно на сайте nuget.org или найти и установить пакеты в Visual Studio, как описано в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="8172f-115">You can always search nuget.org directly or find and install packages within Visual Studio as shown in this topic.</span></span>

## <a name="install-pre-requisites"></a><span data-ttu-id="8172f-116">Установка необходимых компонентов</span><span class="sxs-lookup"><span data-stu-id="8172f-116">Install pre-requisites</span></span>

<span data-ttu-id="8172f-117">Для прохождения этого учебника требуется Visual Studio 2015 с обновлением 3 и инструментами для универсальных приложений Windows или Visual Studio 2017 с рабочей нагрузкой "Разработка приложений для универсальной платформы Windows".</span><span class="sxs-lookup"><span data-stu-id="8172f-117">This tutorial requires Visual Studio 2015 Update 3 with Tools for Universal Windows Apps, or Visual Studio 2017 with the Universal Windows Platform development workload.</span></span> <span data-ttu-id="8172f-118">Если среда Visual Studio уже установлена, вы можете снова запустить установщик, чтобы установить инструменты для универсальной платформы Windows.</span><span class="sxs-lookup"><span data-stu-id="8172f-118">If you already have Visual Studio installed, you can run the installer again to add the UWP tools.</span></span>

<span data-ttu-id="8172f-119">Вы можете установить бесплатный выпуск Community с сайта [visualstudio.com](https://www.visualstudio.com/) либо использовать выпуск Professional или Enterprise.</span><span class="sxs-lookup"><span data-stu-id="8172f-119">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span> 

## <a name="create-a-project"></a><span data-ttu-id="8172f-120">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="8172f-120">Create a project</span></span>

<span data-ttu-id="8172f-121">Для установки пакета NuGet требуется какой-либо проект на основе .NET в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8172f-121">To install a NuGet package, you need some kind of .NET-based project in Visual Studio.</span></span> <span data-ttu-id="8172f-122">В этом пошаговом руководстве можно использовать простое приложение Windows Presentation Foundation (WPF) или приложение универсальной платформы Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="8172f-122">For this walkthrough, you can use use a simple Windows Presentation Foundation (WPF) or Universal Windows (UWP) app:</span></span>

- <span data-ttu-id="8172f-123">Для создания приложения WPF (Windows 7 или более поздней версии) последовательно выберите **Файл > Создать > Проект**, разверните узел **Visual C#**, выберите шаблон **Классический рабочий стол Windows > Приложение WPF (.NET Framework)** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8172f-123">For WPF (Windows 7+), choose **File > New > Project**, expand **Visual C#**, select **Windows Classic Desktop > WPF App (.NET Framework)**, and select **OK**.</span></span>
- <span data-ttu-id="8172f-124">Для создания приложения UWP (Windows 10) используйте вместо этого шаблон **Универсальные приложения Windows > Пустое приложение (универсальное приложение Windows)**.</span><span class="sxs-lookup"><span data-stu-id="8172f-124">For UWP (Windows 10), use the **Windows Universal > Blank App (Universal Windows)** instead.</span></span> <span data-ttu-id="8172f-125">При появлении запроса оставьте значения свойств "Конечная версия" и "Минимальная версия" по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8172f-125">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="8172f-126">Добавление пакета NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="8172f-126">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="8172f-127">В обозревателе решений щелкните правой кнопкой мыши узел **Ссылки** и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="8172f-127">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Пункт "Управление пакетами NuGet" для узла "Ссылки" проекта](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="8172f-129">Выберите nuget.org в качестве **источника пакетов**, перейдите на вкладку **Обзор**, выполните поиск по запросу **Newtonsoft.Json**, выберите этот пакет в списке и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="8172f-129">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Поиск пакета Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="8172f-131">Если появится запрос на выбор формата диспетчера пакетов, выберите PackageReference (рекомендуется) или `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="8172f-131">If prompted to select a package management format, choose between PackageReference (recommended) and `packages.config`:</span></span>

    ![Выбор формата ссылок на пакеты](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="8172f-133">В запросе на проверку изменений нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8172f-133">If prompted to review changes, select **OK**.</span></span>

1. <span data-ttu-id="8172f-134">В обозревателе решений щелкните решение правой кнопкой мыши и выберите пункт **Собрать решение**.</span><span class="sxs-lookup"><span data-stu-id="8172f-134">Right-click the solution in Solution Explorer and select **Build Solution**.</span></span> <span data-ttu-id="8172f-135">При этом будут восстановлены все пакеты NuGet, перечисленные в узле **Ссылки**.</span><span class="sxs-lookup"><span data-stu-id="8172f-135">This restores any NuGet packages listed under **References**.</span></span> <span data-ttu-id="8172f-136">Дополнительные сведения см. в разделе [Восстановление пакета](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="8172f-136">For more details, see [Package Restore](../consume-packages/package-restore.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="8172f-137">Использование интерфейса API Newtonsoft.Json в приложении</span><span class="sxs-lookup"><span data-stu-id="8172f-137">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="8172f-138">Добавив пакет Newtonsoft.Json в проект, вы можете вызывать его метод `JsonConvert.SerializeObject` для преобразования объекта в удобную для восприятия строку.</span><span class="sxs-lookup"><span data-stu-id="8172f-138">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="8172f-139">Откройте файл `MainWindow.xaml` (WPF) или `MainPage.xaml` (UWP) и замените существующий элемент `Grid` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="8172f-139">Open `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="8172f-140">В обозревателе решений разверните узел `MainWindow.xaml` (WPF) или `MainPage.xaml` (UWP), откройте файл `.cs` и вставьте следующий код внутри класса `MainWindow` или `MainPage` после конструктора:</span><span class="sxs-lookup"><span data-stu-id="8172f-140">Expand the `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) node in Solution Explorer, open the `.cs` file, and insert the following code inside the `MainWindow` or `MainPage` class, after the constructor:</span></span>

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

1. <span data-ttu-id="8172f-141">Несмотря на то, что вы добавили пакет Newtonsoft.Json в проект, `JsonConvert` подчеркивается красной волнистой линией, так как требуется оператор `using`.</span><span class="sxs-lookup"><span data-stu-id="8172f-141">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement.</span></span> <span data-ttu-id="8172f-142">Наведите указатель мыши на подчеркнутое слово `JsonConvert`, и вы увидите кнопку со значком лампочки и ссылку **Показать возможные решения**.</span><span class="sxs-lookup"><span data-stu-id="8172f-142">Hover over the underlined `JsonConvert` and you'll see the Lightbulb and the option to **Show potential fixes**:</span></span>

    ![Кнопка со значком лампочки и ссылка "Показать возможные решения"](media/QS_Use-04-ShowPotentialFixes.png)


1. <span data-ttu-id="8172f-144">Щелкните ссылку **Показать возможные решения** (или нажмите кнопку со значком лампочки) и выберите первое предложенное исправление (`using Newtonsoft.Json;`).</span><span class="sxs-lookup"><span data-stu-id="8172f-144">Click on **Show potential fixes** (or the Lightbulb) and select the first suggested fix, `using Newtonsoft.Json;`.</span></span> <span data-ttu-id="8172f-145">В начало файла добавится необходимая строка.</span><span class="sxs-lookup"><span data-stu-id="8172f-145">This adds the necessary line to the top of the file.</span></span>

    ![В список исправлений с предложением добавить оператор using](media/QS_Use-05-AddUsing.png)

1. <span data-ttu-id="8172f-147">Выполните сборку и запустите приложение, нажав клавишу F5 или выбрав команду **Отладка > Начать отладку** (ниже показано приложение UWP; приложение WPF выглядит аналогично).</span><span class="sxs-lookup"><span data-stu-id="8172f-147">Build and run the app by pressing F5 or selecting **Debug > Start Debugging** (UWP shown here; WPF is similar):</span></span>

    ![Изначальные выходные данные приложения UWP](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="8172f-149">Нажмите кнопку. Надпись TextBlock заменится текстом в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="8172f-149">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Выходные данные приложения UWP после нажатия кнопки](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a><span data-ttu-id="8172f-151">См. также</span><span class="sxs-lookup"><span data-stu-id="8172f-151">Related topics</span></span>

- [<span data-ttu-id="8172f-152">Общие сведения и процесс использования пакетов</span><span class="sxs-lookup"><span data-stu-id="8172f-152">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="8172f-153">Поиск и выбор пакетов</span><span class="sxs-lookup"><span data-stu-id="8172f-153">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="8172f-154">Настройка поведения NuGet</span><span class="sxs-lookup"><span data-stu-id="8172f-154">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
