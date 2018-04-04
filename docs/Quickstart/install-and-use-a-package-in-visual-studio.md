---
title: Вводное руководство по использованию пакетов NuGet в Visual Studio | Документация Майкрософт
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: quickstart
ms.prod: nuget
ms.technology: ''
description: Пошаговое руководство по установке и использованию пакета NuGet в проекте Visual Studio.
keywords: установка NuGet, использование пакета NuGet, установка пакетов NuGet, ссылки на пакеты NuGet, использование пакетов NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4205893cc02cffff8926513a555393d10c046f43
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="install-and-use-a-package-in-visual-studio"></a>Установка и использование пакета в Visual Studio

Пакеты NuGet содержат многократно используемый код, предлагаемый другими разработчиками для ваших проектов. Дополнительные сведения см. в разделе [Что такое NuGet?](../What-is-NuGet.md). Пакеты устанавливаются в проект Visual Studio с помощью пользовательского интерфейса или консоли диспетчера пакетов. В этой статье описан процесс с использованием популярного пакета [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) и проекта универсальной платформы Windows (UWP). Тот же процесс применяется к любому другому проекту .NET или .NET Core.

После установки ссылаться на пакет в коде можно с помощью `using <namespace>`, где \<namespace\> соответствует используемому пакету. После указания ссылки можно обращаться к пакету посредством его интерфейса API.

> [!Tip]
> **Начните с сайта nuget.org**: разработчики .NET обычно находят компоненты, которые можно использовать в собственных приложениях, просматривая сайт nuget.org. Вы можете выполнить поиск непосредственно на сайте nuget.org или найти и установить пакеты в Visual Studio, как описано в этой статье.

## <a name="prerequisites"></a>Предварительные требования

- Visual Studio 2017 с рабочей нагрузкой универсальной платформы Windows или
- Visual Studio 2015 с обновлением 3 и инструментами для разработки универсальных приложений для Windows.

Вы можете установить бесплатный выпуск Community 2017 с сайта [visualstudio.com](https://www.visualstudio.com/) либо использовать выпуск Professional или Enterprise.

## <a name="create-a-project"></a>Создание проекта

Пакеты NuGet можно установить в проект .NET, если эти пакеты поддерживают ту же требуемую версию .NET Framework, что и проект.

В этом пошаговом руководстве используется простое приложение универсальной Windows (UWP). Создайте проект в Visual Studio, выбрав пункты **Файл > Новый проект...**, а затем — **Универсальные приложения Windows > Пустое приложение (универсальное приложение для Windows)**. При появлении запроса оставьте значения свойств "Конечная версия" и "Минимальная версия" по умолчанию.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Добавление пакета NuGet Newtonsoft.Json

Для установки пакета можно использовать пользовательский интерфейс или консоль диспетчера пакетов. При установке пакета NuGet регистрирует зависимость в файле проекта или файле `packages.config`. Дополнительные сведения см. в разделе [Обзор использования пакетов и рабочий процесс](../consume-packages/Overview-and-Workflow.md).

### <a name="package-manager-ui"></a>Пользовательский интерфейс диспетчера пакетов

1. В обозревателе решений щелкните правой кнопкой мыши узел **Ссылки** и выберите пункт **Управление пакетами NuGet**.

    ![Пункт "Управление пакетами NuGet" для узла "Ссылки" проекта](media/QS_Use-02-ManageNuGetPackages.png)

1. Выберите nuget.org в качестве **источника пакетов**, перейдите на вкладку **Обзор**, выполните поиск по запросу **Newtonsoft.Json**, выберите этот пакет в списке и нажмите кнопку **Установить**.

    ![Поиск пакета Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. Примите все запросы касательно лицензии.

1. (Visual Studio 2017.) Если вам будет предложено выбрать формат управления пакетом, выберите **PackageReference в файле проекта**.

    ![Выбор формата управления пакетами](media/QS_Use-03b-SelectFormat.png)

1. В запросе на проверку изменений нажмите кнопку **ОК**.

### <a name="package-manager-console"></a>Консоль диспетчера пакетов

1. Выберите команды меню **Сервис > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**.

1. После открытия консоли убедитесь, что в раскрывающемся списке **Проект по умолчанию** показан проект, в который требуется установить пакет. Если в решении всего лишь один проект, он автоматически выбран.

    ![Поиск пакета Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. Введите команду `Install-Package Newtonsoft.json` (см. сведения о ней в [этой статье](../tools/ps-ref-install-package.md)). В окне консоли отображаются выходные данные команды. Ошибки обычно означают, что пакет не совместим с целевой платформой проекта.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Использование интерфейса API Newtonsoft.Json в приложении

Добавив пакет Newtonsoft.Json в проект, вы можете вызывать его метод `JsonConvert.SerializeObject` для преобразования объекта в удобную для восприятия строку.

1. Откройте файл `MainPage.xaml` и замените существующий элемент `Grid` следующим кодом:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Откройте файл `MainPage.xaml.cs` (который находится в обозревателе решений в узле `MainPage.xaml`) и вставьте в конструктор `MainPage` следующий код:

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

1. Несмотря на то что вы добавили пакет Newtonsoft.Json в проект, `JsonConvert` подчеркивается красной волнистой линией, так как оператор `using` требуется в верхней части файла кода.

    ```cs
    using Newtonsoft.json;
    ```

1. Выполните сборку и запустите приложение, нажав клавишу F5 или выбрав команду **Отладка > Начать отладку**.

    ![Изначальные выходные данные приложения UWP](media/QS_Use-06-AppStart.png)

1. Нажмите кнопку. Надпись TextBlock заменится текстом в формате JSON:

    ![Выходные данные приложения UWP после нажатия кнопки](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a>Связанные статьи

- [Общие сведения и процесс использования пакетов](../consume-packages/overview-and-workflow.md)
- [Поиск и выбор пакетов](../consume-packages/finding-and-choosing-packages.md)
- [Способы установки пакета NuGet](../consume-packages/ways-to-install-a-package.md)
- [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md)
