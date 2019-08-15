---
title: Управление пакетами NuGet с использованием CLI nuget.exe
description: Инструкции по использованию CLI nuget.exe для работы с пакетами NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 9ef990c16cca62a1fbad25ff1582bfa543135fab
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860584"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>Управление пакетами с использованием CLI nuget.exe

С помощью средства CLI вы можете легко восстанавливать пакеты NuGet в проектах и решениях. Это средство обеспечивает все функциональные возможности NuGet в Windows и большинство функций, выполняемых в рамках проекта Mono на компьютере Mac и Linux.

Средство CLI `nuget.exe` предназначено для работы с проектом .NET Framework и проектами не на основе пакетов SDK (например, для проектов, нацеленных на библиотеки .NET Standard). Если вы используете проект не на основе пакета SDK, который перенесен в `PackageReference`, используйте CLI `dotnet`. Чтобы указывать ссылки на пакеты, в CLI `nuget.exe` используется файл [packages.config](../reference/packages-config.md).

> [!NOTE]
> В большинстве сценариев рекомендуется [переносить проекты не на основе пакетов SDK](../reference/migrate-packages-config-to-package-reference.md), в которых используется файл `packages.config`, в PackageReference. В таких случаях можно использовать CLI `dotnet` вместо CLI `nuget.exe`. На данный момент не поддерживается миграция для проектов C++ и ASP.NET.

В этой статье описываются общие принципы использования некоторых распространенных команд CLI `nuget.exe`. Для большинства из этих команд средство CLI ищет файл проекта в текущем каталоге, кроме случаев, когда файл проекта задан в самой команде. Полный список доступных команд и аргументов см. в статье [Справочник по интерфейсу командной строки nuget.exe](../reference/nuget-exe-cli-reference.md).

## <a name="prerequisites"></a>Предварительные требования

- Установите интерфейс командной строки `nuget.exe`, скачав его на сайте [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), и сохраните этот файл `.exe` в подходящую папку. Добавьте эту папку в переменную среды PATH.

## <a name="install-a-package"></a>Установка пакета

Команда [install](../reference/cli-reference/cli-ref-install.md) позволяет скачать и установить пакет в проект с использованием заданных источников пакетов. По умолчанию для этого используется текущая папка. Установите новые пакеты в папку *packages* в корневом каталоге проекта.

> [!IMPORTANT]
> Команда `install` не вносит изменения в файл проекта или файл *packages.config*. В этом она похожа на команду `restore`, которая также только добавляет пакеты на диск, не изменяя при этом зависимые компоненты проекта. Чтобы добавить зависимый компонент, добавьте пакет с помощью пользовательского интерфейса диспетчера пакетов или консоли в Visual Studio, либо измените файл *packages.config* и затем выполните команду `install` или `restore`.

1. Откройте командную строку и перейдите в каталог, в котором находится файл проекта.

2. Выполните следующую команду для установки пакета NuGet в папку *packages*.

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    Например, чтобы установить пакет `Newtonsoft.json` в папку *packages*, выполните следующую команду:

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

Также вы можете использовать следующую команду, чтобы установить пакет NuGet с помощью существующего файла `packages.config` в папку *packages*. При этом пакет устанавливается локально и не добавляется в список зависимых компонентов проекта.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>Установка определенной версии пакета

Если при использовании команды [install](../reference/cli-reference/cli-ref-install.md) версия пакета не указана, NuGet установит его последнюю версию. Вы также можете установить определенную версию пакета Nuget.

```cli
nuget install <packageID | configFilePath> -Version <version>
```

Например, чтобы добавить версию 12.0.1 пакета `Newtonsoft.json`, воспользуйтесь следующей командой:

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

Дополнительные сведения об ограничениях и поведении команды `install` см. в статье [Установка пакета](#install-a-package).

## <a name="remove-a-package"></a>Удаление пакета

Если возникает необходимость, пакеты следует удалять из папки *packages*.

Чтобы переустановить пакеты, используйте команды `restore` или `install`.

## <a name="list-packages"></a>Вывод списка пакетов

Чтобы просмотреть список пакетов из заданного источника, выполните команду [list](../reference/cli-reference/cli-ref-list.md). Чтобы ограничить область поиска, используйте параметр `-Source`.

```cli
nuget list -Source <source>
```

Например, можно вывести список пакетов в папке *packages*.

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

Если вы указываете условие поиска, в результаты будут включены названия пакетов, теги и описания пакетов.

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>Обновление отдельного пакета

При выполнении команды `install` NuGet устанавливает последнюю версию пакета, кроме случаев, когда версия задается с помощью соответствующего параметра.

## <a name="update-all-packages"></a>Обновление всех пакетов

Чтобы обновить все пакеты, воспользуйтесь командой [update](../reference/cli-reference/cli-ref-update.md). При этом все пакеты в проекте, использующем файл `packages.config`, обновляются до последней доступной версии. Рекомендуется выполнить команду `restore` перед использованием команды `update`.

```cli
nuget update
```

## <a name="restore-packages"></a>Восстановление пакетов

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]