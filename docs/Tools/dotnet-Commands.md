---
title: команды NuGet DotNet
description: Краткая ссылка для команд, связанных с NuGet dotnet интерфейс командной строки.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: fe49274af339c987d5e090c99edd78f62f59ce47
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2018
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
