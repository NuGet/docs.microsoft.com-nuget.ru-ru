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
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>Краткое руководство. Установка и использование пакета Visual Studio для Mac

Пакеты NuGet содержат многократно используемый код, предлагаемый другими разработчиками для ваших проектов. Дополнительные сведения см. в разделе [Что такое NuGet?](../What-is-NuGet.md). Пакеты устанавливаются в проекте Visual Studio для Mac с помощью диспетчера пакетов NuGet. В этой статье описано, как использовать популярный пакет [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) и консольный проект .NET Core. Этот процесс применим к любому другому проекту Xamarin или .NET Core.

После установки ссылаться на пакет в коде можно с помощью `using <namespace>`, где \<namespace\> соответствует используемому пакету. После указания ссылки можно обращаться к пакету посредством его интерфейса API.

> [!Tip]
> **Начните работу с сайта nuget.org**: Разработчики .NET обычно находят компоненты, которые можно использовать в собственных приложениях, просматривая сайт *nuget.org*. Вы можете выполнить поиск непосредственно на сайте *nuget.org* или найти и установить пакеты в Visual Studio, как описано в этой статье. См. подробнее о [поиске и оценке пакетов NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Предварительные требования

- Visual Studio 2019 для Mac.

Вы можете установить бесплатный выпуск Community 2019 с сайта [visualstudio.com](https://www.visualstudio.com/) либо использовать выпуск Professional или Enterprise.

См. сведения об [установке и использовании пакета в Visual Studio в Windows](install-and-use-a-package-in-visual-studio.md).

## <a name="create-a-project"></a>Создание проекта

Пакеты NuGet можно установить в проект .NET, если эти пакеты поддерживают ту же требуемую версию .NET Framework, что и проект.

В этом пошаговом руководстве описано, как использовать консольное приложение .NET Core. Создайте проект в Visual Studio для Mac. Для этого выберите **Файл > Создать решение** и щелкните **.NET Core > Приложение > Консольное приложение**. Нажмите кнопку **Далее**. При появлении запроса примите для **целевой платформы** значения по умолчанию.

Visual Studio создаст проект и откроет его в обозревателе решений.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Добавление пакета NuGet Newtonsoft.Json

Чтобы установить пакет, используйте диспетчер пакетов NuGet. При установке пакета NuGet регистрирует зависимость в файле проекта или файле `packages.config` (в зависимости от формата проекта). Дополнительные сведения см. в разделе [Обзор использования пакетов и рабочий процесс](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Диспетчер пакетов NuGet

1. В обозревателе решений щелкните правой кнопкой мыши **Зависимости** и выберите **Добавить пакеты**.

    ![Пункт "Управление пакетами NuGet" для узла "Ссылки" проекта](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. Вверху слева выберите nuget.org в качестве **источника пакетов**, выполните поиск по запросу **Newtonsoft.Json**, выберите этот пакет в списке и щелкните **Пакеты**:

    ![Поиск пакета Newtonsoft.Json](media/QS_Use_Mac-03-NewtonsoftJson.png)

    См. сведения о диспетчере пакетов NuGet в руководстве по [установке пакетов и управлению ими с помощью Visual Studio для Mac](../consume-packages/install-use-packages-visual-studio.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Использование интерфейса API Newtonsoft.Json в приложении

Добавив пакет Newtonsoft.Json в проект, вы можете вызывать его метод `JsonConvert.SerializeObject` для преобразования объекта в удобную для восприятия строку.

1. Откройте файл `Program.cs` (на Панели решения) и замените его содержимое следующим кодом:

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

1. Выполните сборку и запустите приложение, щелкнув **Отладка > Начать отладку**:

1. После запуска приложения в консоли отобразятся сериализованные выходные данные JSON:

  ![Выходные данные консольного приложения](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>Следующие шаги
Поздравляем! Вы установили пакет NuGet и поработали с ним.

> [!div class="nextstepaction"]
> [Установка пакетов и управление ими с использованием Visual Studio для Mac](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

См. подробнее о возможностях NuGet по приведенным ниже ссылкам.

- [Общие сведения и процесс использования пакетов](../consume-packages/overview-and-workflow.md)
- [Ссылки на пакеты в файлах проекта](../consume-packages/package-references-in-project-files.md)
