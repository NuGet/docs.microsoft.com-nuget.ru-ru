---
title: Вводное руководство по использованию пакетов с помощью dotnet CLI
description: Пошаговое руководство по установке и использованию пакета NuGet в проекте .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 4b593cc215ad68629e5a93d1f17c90e53c0b4f4f
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324634"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Краткое руководство. Установка и использование пакета с помощью CLI dotnet

Пакеты NuGet содержат многократно используемый код, предлагаемый другими разработчиками для ваших проектов. Дополнительные сведения см. в разделе [Что такое NuGet?](../What-is-NuGet.md). Пакеты устанавливаются в проект .NET Core с помощью команды `dotnet add package`, как описано в статье о популярном пакете [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).

После установки ссылаться на пакет в коде можно с помощью `using <namespace>`, где \<namespace\> соответствует используемому пакету. Затем можно использовать API пакета.

> [!Tip]
> **Начните работу с сайта nuget.org**: разработчики .NET обычно находят компоненты, которые можно использовать в собственных приложениях, просматривая сайт nuget.org. Вы можете выполнить поиск непосредственно на сайте nuget.org или найти и установить пакеты в Visual Studio, как описано в этой статье.

## <a name="prerequisites"></a>Предварительные требования

- [Пакет SDK для .NET Core](https://www.microsoft.com/net/download/), который предоставляет программу командной строки `dotnet`.

## <a name="create-a-project"></a>Создание проекта

Пакеты NuGet могут быть установлены в любой проект .NET. В рамках этого пошагового руководства создайте простой консольный проект .NET Core следующим образом:

1. Создайте папку для проекта.

1. Создайте проект с помощью следующей команды:

    ```cli
    dotnet new console
    ```

1. Чтобы проверить, что приложение создано правильно, используйте команду `dotnet run`.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Добавление пакета NuGet Newtonsoft.Json

1. Чтобы установить пакет `Newtonsoft.json`, выполните следующую команду:

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. Чтобы увидеть добавленную ссылку, после завершения команды откройте файл `.csproj`.

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Использование интерфейса API Newtonsoft.Json в приложении

1. Откройте файл `Program.cs` и добавьте вверху файла следующую строку:

    ```cs
    using Newtonsoft.Json;
    ```

1. Перед строкой `class Program` добавьте следующий код:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. Замените функцию `Main` следующим кодом:

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

1. Выполните сборку и запуск приложения с помощью команды `dotnet run`. В результате вы получите JSON-представление объекта `Account` в коде:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a>Связанные статьи

- [Общие сведения и процесс использования пакетов](../consume-packages/overview-and-workflow.md)
- [Поиск и выбор пакетов](../consume-packages/finding-and-choosing-packages.md)
- [Способы установки пакета NuGet](../consume-packages/ways-to-install-a-package.md)
- [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md)
