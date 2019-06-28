---
title: команды CLI NuGet DotNet
description: Краткая ссылка для команд, связанных с NuGet, с помощью интерфейса командной строки dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: cc99b327c0edb4aeb573dfa8c2f9b9dba7b8cc38
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426003"
---
# <a name="dotnet-cli-commands"></a>команды интерфейса командной строки DotNet

`dotnet` Интерфейса командной строки (CLI), который выполняется в Windows, Mac OS X и Linux, предоставляет ряд основных команд, таких как установка, восстановление и публикация пакетов. Если dotnet удовлетворяет вашим требованиям, нет необходимости использовать `nuget.exe`.

Примеры использования этих команд для получения пакетов, см. в разделе [установки и управления пакетами с помощью dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md). Примеры использования этих команд для создания пакетов, см. в разделе [создание и публикация пакета с помощью dotnet CLI]... / quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Полный справочник по командам на `dotnet` CLI, см. в разделе [средства интерфейса командной строки (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Использование пакета

- [**Команда DotNet add пакета**](/dotnet/core/tools/dotnet-add-package): Добавляет ссылку на пакет в файл проекта, а затем выполняет `dotnet restore` для установки пакета.
- [**пакет удаляется DotNet**](/dotnet/core/tools/dotnet-remove-package): Удаляет ссылку на пакет из файла проекта.
- [**Команда DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Восстанавливает зависимости и средства проекта. По состоянию на NuGet 4.0, это решение работает один и тот же код как `nuget restore`.
- [**DotNet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Выводит список расположений, из *глобальных пакетов*, *http-cache*, и *temp* папки и очищает содержимое этих папок.

## <a name="package-creation"></a>Создание пакета

- [**DotNet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Упаковывает код в пакет NuGet. По состоянию на NuGet 4.0, это решение работает один и тот же код как `nuget pack`.
- [**DotNet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Отправляет пакет на сервер и публикует его, применимые к nuget.org, Visual Studio Team Services и сторонние серверы NuGet.
- [**удалить DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Удаляет или из списка пакетов из узла, применимые к nuget.org, Visual Studio Team Services и сторонние серверы NuGet.
