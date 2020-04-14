---
title: Установка и использование пакета NuGet в Visual Studio
description: Пошаговое руководство по установке и использованию пакета NuGet в проекте Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 10bc34653d294cf70b5c91ce79a79cf6532fba1b
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "80147491"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a>Краткое руководство. Установка и использование пакета в Visual Studio (только в Windows)

Пакеты NuGet содержат многократно используемый код, предлагаемый другими разработчиками для ваших проектов. Дополнительные сведения см. в разделе [Что такое NuGet?](../What-is-NuGet.md). Пакеты устанавливаются в проекте Visual Studio с помощью диспетчера пакетов NuGet, [консоли диспетчера пакетов](../consume-packages/install-use-packages-powershell) или [интерфейса командной строки .NET](install-and-use-a-package-using-the-dotnet-cli.md). В этой статье описано, как использовать популярный пакет [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) и проект Windows Presentation Foundation (WPF). Тот же процесс применяется к любому другому проекту .NET или .NET Core.

После установки ссылаться на пакет в коде можно с помощью `using <namespace>`, где \<namespace\> соответствует используемому пакету. После указания ссылки можно обращаться к пакету посредством его интерфейса API.

> [!Tip]
> **Начните работу с сайта nuget.org**: Разработчики .NET обычно находят компоненты, которые можно использовать в собственных приложениях, просматривая сайт *nuget.org*. Вы можете выполнить поиск непосредственно на сайте *nuget.org* или найти и установить пакеты в Visual Studio, как описано в этой статье. См. подробнее о [поиске и оценке пакетов NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Предварительные требования

- Использование Visual Studio 2019 с рабочей нагрузкой "Разработка классических приложений .NET".

Вы можете установить бесплатный выпуск Community 2019 с сайта [visualstudio.com](https://www.visualstudio.com/) либо использовать выпуск Professional или Enterprise.

См. сведения об [установке и использовании пакета в Visual Studio для Mac](install-and-use-a-package-in-visual-studio-mac.md).

## <a name="create-a-project"></a>Создание проекта

Пакеты NuGet можно установить в проект .NET, если эти пакеты поддерживают ту же требуемую версию .NET Framework, что и проект.

В этом пошаговом руководстве описано, как использовать простое приложение WPF. Создайте проект в Visual Studio, щелкнув **Файл** > **Создать проект** и введя **.NET** в поле поиска. Затем выберите **Приложение WPF (.NET Framework)** . Нажмите кнопку **Далее**. При появлении запроса примите значения по умолчанию для **платформы**.

Visual Studio создаст проект и откроет его в обозревателе решений.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Добавление пакета NuGet Newtonsoft.Json

Для установки пакета можно использовать диспетчер пакетов NuGet или консоль диспетчера пакетов. При установке пакета NuGet регистрирует зависимость в файле проекта или файле `packages.config` (в зависимости от формата проекта). Дополнительные сведения см. в разделе [Обзор использования пакетов и рабочий процесс](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Диспетчер пакетов NuGet

1. В обозревателе решений щелкните правой кнопкой мыши узел **Ссылки** и выберите пункт **Управление пакетами NuGet**.

    ![Пункт "Управление пакетами NuGet" для узла "Ссылки" проекта](media/QS_Use-02-ManageNuGetPackages.png)

1. Выберите nuget.org в качестве **источника пакетов**, перейдите на вкладку **Обзор**, выполните поиск по запросу **Newtonsoft.Json**, выберите этот пакет в списке и нажмите кнопку **Установить**.

    ![Поиск пакета Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

    См. подробнее о диспетчере пакетов NuGet в руководстве по [установке пакетов и управлении ими с помощью Visual Studio](../consume-packages/install-use-packages-visual-studio.md).

1. Примите все запросы касательно лицензии.

1. (Только в Visual Studio 2017.) Если вам будет предложено выбрать формат управления пакетом, выберите **PackageReference в файле проекта**.

    ![Выбор формата управления пакетами](media/QS_Use-03b-SelectFormat.png)

1. В запросе на проверку изменений нажмите кнопку **ОК**.

### <a name="package-manager-console"></a>Консоль диспетчера пакетов

1. Последовательно выберите **Сервис** > **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**.

1. После открытия консоли убедитесь, что в раскрывающемся списке **Проект по умолчанию** показан проект, в который требуется установить пакет. Если в решении всего лишь один проект, он автоматически выбран.

    ![Поиск пакета Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. Введите команду `Install-Package Newtonsoft.Json` (см. сведения о ней в [этой статье](../reference/ps-reference/ps-ref-install-package.md)). В окне консоли отображаются выходные данные команды. Ошибки обычно означают, что пакет не совместим с целевой платформой проекта.

   См. подробнее о консоли диспетчера пакетов в руководстве по [установке пакетов и управлении ими с помощью консоли диспетчера пакетов](../consume-packages/install-use-packages-powershell.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Использование интерфейса API Newtonsoft.Json в приложении

Добавив пакет Newtonsoft.Json в проект, вы можете вызывать его метод `JsonConvert.SerializeObject` для преобразования объекта в удобную для восприятия строку.

1. Откройте файл `MainWindow.xaml` и замените существующий элемент `Grid` следующим кодом:

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Откройте файл `MainWindow.xaml.cs` (который находится в обозревателе решений в узле `MainWindow.xaml`) и вставьте в класс `MainWindow` следующий код.

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
    using Newtonsoft.Json;
    ```

1. Выполните сборку и запустите приложение, нажав клавишу F5 или выбрав команду **Отладка** > **Начать отладку**.

    ![Изначальные выходные данные приложения WPF](media/QS_Use-06-AppStart.png)

1. Нажмите кнопку. Надпись TextBlock заменится текстом в формате JSON:

    ![Выходные данные приложения WPF после нажатия кнопки](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a>Связанные видео

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

Другие видео о NuGet см. на [Channel 9](https://channel9.msdn.com/Series/NuGet-101) и [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="next-steps"></a>Следующие шаги

Поздравляем! Вы установили пакет NuGet и поработали с ним.

> [!div class="nextstepaction"]
> [Установка пакетов и управление ими с использованием Visual Studio](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [Установка пакетов и управление ими с использованием консоли диспетчера пакетов](../consume-packages/install-use-packages-powershell.md)

См. подробнее о возможностях NuGet по приведенным ниже ссылкам.

- [Общие сведения и процесс использования пакетов](../consume-packages/overview-and-workflow.md)
- [Поиск и выбор пакетов](../consume-packages/finding-and-choosing-packages.md)
- [Ссылки на пакеты в файлах проекта](../consume-packages/package-references-in-project-files.md)
