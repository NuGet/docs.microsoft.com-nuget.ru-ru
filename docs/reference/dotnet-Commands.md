---
title: команды NuGet CLI DotNet
description: Краткий справочник по связанным с NuGet командам с помощью интерфейса командной строки DotNet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327491"
---
# <a name="dotnet-cli-commands"></a>команды CLI DotNet

Интерфейс `dotnet` командной строки (CLI), работающий в Windows, Mac OS X и Linux, предоставляет ряд ключевых команд, таких как установка, восстановление и публикация пакетов. Если DotNet удовлетворяет вашим потребностям, нет необходимости использовать `nuget.exe`.

Примеры использования этих команд для использования пакетов см. в разделе [Установка пакетов и управление ими с помощью DotNet CLI](../consume-packages/install-use-packages-dotnet-cli.md). Примеры использования этих команд для создания пакетов см. в разделе [Создание и Публикация пакета с помощью интерфейса командной строки DotNet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Полный справочник по `dotnet` командам CLI см. в разделе [средства интерфейса командной строки (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Использование пакета

- [**Добавление пакета DotNet**](/dotnet/core/tools/dotnet-add-package): Добавляет ссылку на пакет в файл проекта, а затем запускает `dotnet restore` для установки пакета.
- [**Удаление пакета DotNet**](/dotnet/core/tools/dotnet-remove-package): Удаляет ссылку на пакет из файла проекта.
- [**DotNet Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Восстанавливает зависимости и средства проекта. В версии NuGet 4.0 при этом выполняется тот же код, что и для команды `nuget restore`.
- [**Локальные объекты NuGet DotNet**](/dotnet/core/tools/dotnet-nuget-locals): Перечисляет расположения папок *Global-Packages*, *HTTP-Cache*и *TEMP* и очищает содержимое этих папок.
- [**DotNet New нужетконфиг**](/dotnet/core/tools/dotnet-new): [`nuget.config`](../reference/nuget-config-file.md) Создает файл для настройки поведения NuGet.

## <a name="package-creation"></a>Создание пакета

- [**пакет DotNet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Упаковывает код в пакет NuGet.
- Команда [**DotNet NuGet Push**](/dotnet/core/tools/dotnet-nuget-push): Публикует пакет на сервере NuGet. Применимо к nuget.org, Azure Artifacts и [сторонним серверам NuGet](../hosting-packages/overview.md).
- [**Удаление DotNet NuGet**](/dotnet/core/tools/dotnet-nuget-delete): Удаляет пакет с сервера NuGet или выводит из него список. Применимо к nuget.org, Azure Artifacts и [сторонним серверам NuGet](../hosting-packages/overview.md).
