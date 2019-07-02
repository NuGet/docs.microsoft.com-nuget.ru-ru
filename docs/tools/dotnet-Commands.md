---
title: команды CLI NuGet DotNet
description: Краткая ссылка для команд, связанных с NuGet, с помощью интерфейса командной строки dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496469"
---
# <a name="dotnet-cli-commands"></a>команды интерфейса командной строки DotNet

`dotnet` Интерфейса командной строки (CLI), который выполняется в Windows, Mac OS X и Linux, предоставляет ряд основных команд, таких как установка, восстановление и публикация пакетов. Если dotnet удовлетворяет вашим требованиям, нет необходимости использовать `nuget.exe`.

Примеры использования этих команд для получения пакетов, см. в разделе [установки и управления пакетами с помощью dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md). Примеры использования этих команд для создания пакетов, см. в разделе [Создание и публикация пакета с помощью dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Полный справочник по командам на `dotnet` CLI, см. в разделе [средства интерфейса командной строки (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Использование пакета

- [**Команда DotNet add пакета**](/dotnet/core/tools/dotnet-add-package): Добавляет ссылку на пакет в файл проекта, а затем выполняет `dotnet restore` для установки пакета.
- [**пакет удаляется DotNet**](/dotnet/core/tools/dotnet-remove-package): Удаляет ссылку на пакет из файла проекта.
- [**Команда DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Восстанавливает зависимости и средства проекта. По состоянию на NuGet 4.0, это решение работает один и тот же код как `nuget restore`.
- [**DotNet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Выводит список расположений, из *глобальных пакетов*, *http-cache*, и *temp* папки и очищает содержимое этих папок.
- [**новый nugetconfig DotNet**](/dotnet/core/tools/dotnet-new): Создает [ `nuget.config` ](../reference/nuget-config-file.md) файл, чтобы настроить поведение NuGet.

## <a name="package-creation"></a>Создание пакета

- [**DotNet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Упаковывает код в пакет NuGet.
- [**DotNet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Публикует пакет на сервере NuGet. Применимо к nuget.org, артефакты Azure, и [сторонних серверов NuGet](../hosting-packages/overview.md).
- [**удалить DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Удаляет или из списка пакетов на сервере NuGet. Применимо к nuget.org, артефакты Azure, и [сторонних серверов NuGet](../hosting-packages/overview.md).
