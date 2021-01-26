---
title: команды NuGet CLI DotNet
description: Краткий справочник по связанным с NuGet командам с помощью интерфейса командной строки DotNet.
author: JonDouglas
ms.author: jodou
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 5438354729ccc851bbbae6c0e7b9394d4226da52
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779991"
---
# <a name="dotnet-cli-commands"></a>Команды интерфейса командной строки DotNet

`dotnet`Интерфейс командной строки (CLI), работающий в Windows, Mac OS X и Linux, предоставляет ряд ключевых команд, таких как установка, восстановление и публикация пакетов. Если DotNet удовлетворяет вашим потребностям, нет необходимости использовать `nuget.exe` .

Примеры использования этих команд для использования пакетов см. в разделе [Установка пакетов и управление ими с помощью DotNet CLI](../consume-packages/install-use-packages-dotnet-cli.md). Примеры использования этих команд для создания пакетов см. в разделе [Создание и Публикация пакета с помощью интерфейса командной строки DotNet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Полный справочник по командам `dotnet` CLI см. в разделе [средства интерфейса командной строки (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Использование пакета

- [**DotNet Add Package**](/dotnet/core/tools/dotnet-add-package): добавляет ссылку на пакет в файл проекта, а затем запускает `dotnet restore` для установки пакета.
- Команда [**DotNet Remove Package**](/dotnet/core/tools/dotnet-remove-package): Удаляет ссылку на пакет из файла проекта.
- [**DotNet Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): восстанавливает зависимости и средства проекта. В версии NuGet 4.0 при этом выполняется тот же код, что и для команды `nuget restore`.
- [**DotNet NuGet Locals**](/dotnet/core/tools/dotnet-nuget-locals): перечисляет расположения папок *Global-Packages*, *HTTP-Cache* и *TEMP* и очищает содержимое этих папок.
- [**DotNet New нужетконфиг**](/dotnet/core/tools/dotnet-new): создает [`nuget.config`](../reference/nuget-config-file.md) файл для настройки поведения NuGet.

## <a name="package-creation"></a>Создание пакета

- [**DotNet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): упаковывает код в пакет NuGet.
- Команда [**DotNet NuGet Push**](/dotnet/core/tools/dotnet-nuget-push): публикует пакет на сервере NuGet. Применимо к nuget.org, Azure Artifacts и [сторонним серверам NuGet](../hosting-packages/overview.md).
- Команда [**DotNet NuGet Delete**](/dotnet/core/tools/dotnet-nuget-delete): удаляет пакет с сервера NuGet или выводит из него список. Применимо к nuget.org, Azure Artifacts и [сторонним серверам NuGet](../hosting-packages/overview.md).
- [**Проверка NuGet в DotNet**](/dotnet/core/tools/dotnet-nuget-verify): проверяет подписанный пакет NuGet.
