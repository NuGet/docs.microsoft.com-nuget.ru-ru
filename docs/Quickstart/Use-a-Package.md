---
title: "Вводное руководство по использованию пакетов NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Пошаговое руководство по установке и использованию пакета NuGet в проекте."
keywords: "установка NuGet, использование пакета NuGet, установка пакетов NuGet, ссылки на пакеты NuGet, использование пакетов NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 897419d1e49f12d54fbb996a2462e06e32933e65
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/31/2018
---
# <a name="install-and-use-a-package"></a>Установка и использование пакета

Пакеты NuGet — это единицы многократно используемого кода, предлагаемые другими разработчиками для ваших проектов. Дополнительные сведения см. в разделе [Что такое NuGet?](../What-is-NuGet.md).

[!INCLUDE [install-methods](../includes/install-methods.md)]

После установки ссылаться на пакет в коде можно с помощью `using <namespace>`, где \<namespace\> соответствует используемому пакету. После указания ссылки можно обращаться к пакету посредством его интерфейса API.

В оставшейся части этого раздела поэтапно рассматривается процесс установки популярного пакета [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) в проекте универсальной платформы Windows (UWP) с помощью пользовательского интерфейса диспетчера пакетов. Далее приводится пример использования пакета. Для других пакетов NuGet используется аналогичный рабочий процесс.

- [Установка необходимых компонентов](#install-pre-requisites)
- [Создание проекта](#create-a-project)
- [Добавление пакета NuGet Newtonsoft.Json](#add-the-newtonsoftjson-nuget-package)
- [Использование интерфейса API Newtonsoft.Json в приложении](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> **Начните работу с nuget.org**: разработчики приложений .NET часто устанавливают пакеты с сайта nuget.org. Здесь можно найти компоненты для использования в собственных приложениях. Вы можете выполнить поиск непосредственно на сайте nuget.org или найти и установить пакеты в Visual Studio, как описано в этом разделе.

## <a name="install-pre-requisites"></a>Установка необходимых компонентов

Для прохождения этого учебника требуется Visual Studio 2015 с обновлением 3 и инструментами для универсальных приложений Windows или Visual Studio 2017 с рабочей нагрузкой "Разработка приложений для универсальной платформы Windows". Если среда Visual Studio уже установлена, вы можете снова запустить установщик, чтобы установить инструменты для универсальной платформы Windows.

Вы можете установить бесплатный выпуск Community с сайта [visualstudio.com](https://www.visualstudio.com/) либо использовать выпуск Professional или Enterprise. 

## <a name="create-a-project"></a>Создание проекта

Для установки пакета NuGet требуется какой-либо проект на основе .NET в Visual Studio. В этом пошаговом руководстве можно использовать простое приложение Windows Presentation Foundation (WPF) или приложение универсальной платформы Windows (UWP).

- Для создания приложения WPF (Windows 7 или более поздней версии) последовательно выберите **Файл > Создать > Проект**, разверните узел **Visual C#**, выберите шаблон **Классический рабочий стол Windows > Приложение WPF (.NET Framework)** и нажмите кнопку **ОК**.
- Для создания приложения UWP (Windows 10) используйте вместо этого шаблон **Универсальные приложения Windows > Пустое приложение (универсальное приложение Windows)**. При появлении запроса оставьте значения свойств "Конечная версия" и "Минимальная версия" по умолчанию.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Добавление пакета NuGet Newtonsoft.Json

1. В обозревателе решений щелкните правой кнопкой мыши узел **Ссылки** и выберите пункт **Управление пакетами NuGet**.

    ![Пункт "Управление пакетами NuGet" для узла "Ссылки" проекта](media/QS_Use-02-ManageNuGetPackages.png)

1. Выберите nuget.org в качестве **источника пакетов**, перейдите на вкладку **Обзор**, выполните поиск по запросу **Newtonsoft.Json**, выберите этот пакет в списке и нажмите кнопку **Установить**.

    ![Поиск пакета Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. Если появится запрос на выбор формата диспетчера пакетов, выберите PackageReference (рекомендуется) или `packages.config`.

    ![Выбор формата ссылок на пакеты](media/QS_Use-03b-SelectFormat.png)

1. В запросе на проверку изменений нажмите кнопку **ОК**.

1. В обозревателе решений щелкните решение правой кнопкой мыши и выберите пункт **Собрать решение**. При этом будут восстановлены все пакеты NuGet, перечисленные в узле **Ссылки**. Дополнительные сведения см. в разделе [Восстановление пакета](../consume-packages/package-restore.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Использование интерфейса API Newtonsoft.Json в приложении

Добавив пакет Newtonsoft.Json в проект, вы можете вызывать его метод `JsonConvert.SerializeObject` для преобразования объекта в удобную для восприятия строку.

1. Откройте файл `MainWindow.xaml` (WPF) или `MainPage.xaml` (UWP) и замените существующий элемент `Grid` следующим кодом:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. В обозревателе решений разверните узел `MainWindow.xaml` (WPF) или `MainPage.xaml` (UWP), откройте файл `.cs` и вставьте следующий код внутри класса `MainWindow` или `MainPage` после конструктора:

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

1. Несмотря на то, что вы добавили пакет Newtonsoft.Json в проект, `JsonConvert` подчеркивается красной волнистой линией, так как требуется оператор `using`. Наведите указатель мыши на подчеркнутое слово `JsonConvert`, и вы увидите кнопку со значком лампочки и ссылку **Показать возможные решения**.

    ![Кнопка со значком лампочки и ссылка "Показать возможные решения"](media/QS_Use-04-ShowPotentialFixes.png)


1. Щелкните ссылку **Показать возможные решения** (или нажмите кнопку со значком лампочки) и выберите первое предложенное исправление (`using Newtonsoft.Json;`). В начало файла добавится необходимая строка.

    ![В список исправлений с предложением добавить оператор using](media/QS_Use-05-AddUsing.png)

1. Выполните сборку и запустите приложение, нажав клавишу F5 или выбрав команду **Отладка > Начать отладку** (ниже показано приложение UWP; приложение WPF выглядит аналогично).

    ![Изначальные выходные данные приложения UWP](media/QS_Use-06-AppStart.png)

1. Нажмите кнопку. Надпись TextBlock заменится текстом в формате JSON:

    ![Выходные данные приложения UWP после нажатия кнопки](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a>См. также

- [Общие сведения и процесс использования пакетов](../consume-packages/overview-and-workflow.md)
- [Поиск и выбор пакетов](../consume-packages/finding-and-choosing-packages.md)
- [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md)
