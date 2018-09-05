---
title: команды DotNet NuGet
description: Краткая ссылка для команд, связанных с NuGet, с помощью интерфейса командной строки dotnet.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: 88e058be674ecddc500665bfa3517f19acde0cd7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546320"
---
# <a name="dotnet-commands"></a>Команды dotnet

`dotnet` Интерфейса командной строки, который выполняется в Windows, Mac OS X и Linux, предоставляет ряд важных nuget.exe команды, перечисленные ниже. Если dotnet удовлетворяет вашим требованиям, нет необходимости использовать `nuget.exe`.

Дополнительные сведения о `dotnet`, см. в разделе [средства интерфейса командной строки (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Использование пакета

- [**Команда DotNet add пакета**](/dotnet/core/tools/dotnet-add-package): Добавляет ссылку на пакет в файл проекта, а затем выполняет `dotnet restore` для установки пакета.
- [**пакет удаляется DotNet**](/dotnet/core/tools/dotnet-remove-package): Удаляет ссылку на пакет из файла проекта.
- [**Команда DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): восстанавливает зависимости и средства проекта. По состоянию на NuGet 4.0, это решение работает один и тот же код как `nuget restore`.
- [**DotNet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): перечислены расположения *глобальных пакетов*, *http-cache*, и *temp* папки и очищает содержимое элемента Эти папки.

## <a name="package-creation"></a>Создание пакета

- [**DotNet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): упаковывает код в пакет NuGet. По состоянию на NuGet 4.0, это решение работает один и тот же код как `nuget pack`.
- [**DotNet nuget push**](/dotnet/core/tools/dotnet-nuget-push): отправляет пакет на сервер и публикует его, применимые к nuget.org, Visual Studio Team Services и сторонние серверы NuGet.
- [**удалить DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): удаляет или из списка пакетов из узла, применимые к nuget.org, Visual Studio Team Services и сторонние серверы NuGet.
