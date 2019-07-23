---
title: Установка пакетов NuGet и управление ими с использованием CLI dotnet
description: Инструкции по использованию CLI dotnet для работы с пакетами NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 64f3a1978cd336064a77c9f3872357e65c37fc10
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842358"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>Установка пакетов и управление ими с использованием CLI dotnet

С помощью средства CLI вы можете легко устанавливаться, удалять и обновлять пакеты NuGet в проектах и решениях. Оно работает в Windows, Mac OS X и Linux.

Средство CLI dotnet предназначено для использования в проектах .NET Core и .NET Standard (проекты в стиле пакета SDK), а также в любых других проектах в стиле пакета SDK (например, в тех, которые нацелены на платформу .NET Framework). Дополнительные сведения см. в статье [Атрибут SDK](/dotnet/core/tools/csproj#additions).

В этой статье описываются общие принципы использования некоторых распространенных команд CLI dotnet. Для большинства из этих команд средство CLI ищет файл проекта в текущем каталоге, кроме случаев, когда файл проекта задан в самой команде (с помощью необязательного параметра). Полный список доступных команд и аргументов см. в статье [Средства интерфейса командной строки (CLI) .NET Core](../tools/dotnet-commands.md).

## <a name="prerequisites"></a>Предварительные требования

- [Пакет SDK для .NET Core](https://www.microsoft.com/net/download/), который предоставляет программу командной строки `dotnet`. Начиная с версии Visual Studio 2017, средство CLI dotnet автоматически устанавливается вместе с любыми рабочими нагрузками, связанными с .NET Core.

## <a name="install-a-package"></a>Установка пакета

Команда [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) добавляет в файл проекта ссылку на пакет, после чего выполняет команду `dotnet restore` для установки пакета.

1. Откройте командную строку и перейдите в каталог, в котором находится файл проекта.

2. Выполните следующую команду для установки пакета Nuget:

    ```cli
    dotnet add package <PACKAGE_NAME>
    ```

    Например, чтобы установить пакет `Newtonsoft.Json`, выполните следующую команду

    ```cli
    dotnet add package Newtonsoft.Json
    ```

3. После выполнения команды проверьте файл проекта и убедитесь, что пакет был установлен.

   Для этого можно открыть файл `.csproj` и проверить добавленную в него ссылку:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>Установка определенной версии пакета

Если версия пакета не указана, NuGet установит его последнюю версию. Также вы можете выполнить команду [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x), чтобы установить определенную версию пакета Nuget:

```cli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

Например, чтобы добавить версию 12.0.1 пакета `Newtonsoft.Json`, воспользуйтесь следующей командой:

```cli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a>Вывод списка ссылок на пакеты

Чтобы просмотреть список ссылок на пакеты для проекта, воспользуйтесь командой [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x).

```cli
dotnet list package
```

## <a name="remove-a-package"></a>Удаление пакета

Чтобы удалить ссылку на пакет из файла проекта, воспользуйтесь командой [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x).

```cli
dotnet remove package <PACKAGE_NAME>
```

Например, чтобы удалить пакет `Newtonsoft.Json`, выполните следующую команду

```cli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Обновление пакета

При выполнении команды `dotnet add package` NuGet устанавливает последнюю версию пакета, кроме случаев, когда версия задается с помощью параметра `-v`.

## <a name="restore-packages"></a>Восстановление пакетов

С помощью команды [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) вы можете восстановить пакеты, включенные в файл проекта (см. [PackageReference](../consume-packages/package-references-in-project-files.md)). При использовании .NET Core версии 2.0 и более поздней автоматическое восстановление доступно с помощью команд `dotnet build` и `dotnet run`. В версии NuGet 4.0 при этом выполняется тот же код, что и для команды `nuget restore`.

Как и с другими командами CLI `dotnet`, откройте командную строку и перейдите к каталогу, в котором находится файл проекта.

Восстановление пакета с помощью `dotnet restore`.

```cli
dotnet restore 
```
