---
title: команды NuGet DotNet
description: Краткая ссылка для команд, связанных с NuGet dotnet интерфейс командной строки.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: dd30c5d5e29ff7ef7c6622a9b93c32b908198d52
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817025"
---
# <a name="dotnet-commands"></a>Команды dotnet

`dotnet` Интерфейс командной строки, которая выполняется в Windows, Mac OS X и Linux, предоставляет ряд важных nuget.exe команд, приведенные ниже. Если dotnet удовлетворяет вашим требованиям, нет необходимости использовать `nuget.exe`.

Подробные сведения по `dotnet`, в разделе [средства командной строки (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Использование пакета

- [**DotNet добавить пакет**](/dotnet/core/tools/dotnet-add-package): Добавляет ссылку на пакет в файл проекта, а затем выполняет `dotnet restore` для установки пакета.
- [**Удаление DotNet пакета**](/dotnet/core/tools/dotnet-remove-package): Удаляет ссылку пакета из файла проекта.
- [**Восстановление DotNet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): восстанавливает зависимости и средств проекта. Начиная с версии NuGet 4.0 выполняет один и тот же код как `nuget restore`.
- [**локальные переменные nuget DotNet**](/dotnet/core/tools/dotnet-nuget-locals): содержит расположений *глобального пакеты*, *кэша http*, и *temp* папки и очищает содержимое Эти папки.

## <a name="package-creation"></a>Создание пакета

- [**пакет DotNet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): пакеты кода в пакет NuGet. Начиная с версии NuGet 4.0 выполняет один и тот же код как `nuget pack`.
- [**Принудительная nuget DotNet**](/dotnet/core/tools/dotnet-nuget-push): помещает пакет на сервере и публикует его, применимые к nuget.org, Visual Studio Team Services и серверы NuGet сторонних разработчиков.
- [**удалить DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): удаляет или unlists пакета из узла, применимые к nuget.org, Visual Studio Team Services и серверы NuGet сторонних разработчиков.
