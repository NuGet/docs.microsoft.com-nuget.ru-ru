---
title: "команды NuGet dotNet | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Краткая ссылка для команд, связанных с NuGet dotnet интерфейс командной строки."
keywords: "команды NuGet DotNet, пакет dotnet, dotnet восстановления, локальные nuget dotnet, dotnet nuget push, dotnet nuget delete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2851938cd43b35454d8e4ad595fbd93229d4dd72
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/20/2018
---
# <a name="dotnet-commands"></a>команды dotNet

`dotnet` Интерфейс командной строки, которая выполняется в Windows, Mac OS X и Linux, предоставляет ряд важных nuget.exe команд, приведенные ниже. Если dotnet удовлетворяет вашим требованиям, нет необходимости использовать `nuget.exe`.

Подробные сведения по `dotnet`, в разделе [средства командной строки (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Использование пакета

- [**DotNet добавить пакет**](/dotnet/core/tools/dotnet-add-package): Добавляет ссылку на пакет в файл проекта, а затем выполняет `dotnet restore` для установки пакета.
- [**Удаление DotNet пакета**](/dotnet/core/tools/dotnet-remove-package): Удаляет ссылку пакета из файла проекта.
- [**Восстановление DotNet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): восстанавливает зависимости и средств проекта. Начиная с версии NuGet 4.0 выполняет один и тот же код как `nuget restore`.
- [**локальные переменные nuget DotNet**](/dotnet/core/tools/dotnet-nuget-locals): очищает или список локальных ресурсов NuGet кэша HTTP-запроса, временном кэше и папке пакеты глобального уровня компьютера.

## <a name="package-creation"></a>Создание пакета

- [**пакет DotNet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): пакеты кода в пакет NuGet. Начиная с версии NuGet 4.0 выполняет один и тот же код как `nuget pack`.
- [**Принудительная nuget DotNet**](/dotnet/core/tools/dotnet-nuget-push): помещает пакет на сервере и публикует его, применимые к nuget.org, Visual Studio Team Services и серверы NuGet сторонних разработчиков.
- [**удалить DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): удаляет или unlists пакета из узла, применимые к nuget.org, Visual Studio Team Services и серверы NuGet сторонних разработчиков.
