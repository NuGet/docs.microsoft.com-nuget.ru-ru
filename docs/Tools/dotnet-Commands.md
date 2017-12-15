---
title: "команды NuGet dotNet | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0c81dbc4-2c14-4ec8-b87a-b802a899c3ea
description: "Краткая ссылка для команд, связанных с NuGet dotnet интерфейс командной строки."
keywords: "команды NuGet DotNet, пакет dotnet, dotnet восстановления, локальные nuget dotnet, dotnet nuget push, dotnet nuget delete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ff4779f46db102f1384650d82118b34fedd4413
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="dotnet-commands"></a><span data-ttu-id="ac2ce-104">команды dotNet</span><span class="sxs-lookup"><span data-stu-id="ac2ce-104">dotNet commands</span></span>

<span data-ttu-id="ac2ce-105">DotNet интерфейс командной строки, который выполняется на Windows, Linux и Mac OS X, предоставляет ряд важных nuget.exe команды, приведенные ниже.</span><span class="sxs-lookup"><span data-stu-id="ac2ce-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="ac2ce-106">Где dotnet предоставляет нужные команды, не загружать nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="ac2ce-106">Where dotnet provides the desired commands, it is not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="ac2ce-107">[**пакет DotNet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): пакеты кода для пакета SDK NETCore проектов в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="ac2ce-107">[**dotnet pack**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs code for NETCore SDK projects into a NuGet package.</span></span> <span data-ttu-id="ac2ce-108">Следует использовать другие типы проектов[`nuget pack`](cli-ref-pack.md)</span><span class="sxs-lookup"><span data-stu-id="ac2ce-108">All other project types should use [`nuget pack`](cli-ref-pack.md)</span></span>
- <span data-ttu-id="ac2ce-109">[**Восстановление DotNet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): восстанавливает зависимости и средств проекта.</span><span class="sxs-lookup"><span data-stu-id="ac2ce-109">[**dotnet restore**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="ac2ce-110">Начиная с версии NuGet 4.0 выполняет один и тот же код как `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="ac2ce-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="ac2ce-111">[**локальные переменные nuget DotNet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): очищает или перечислены локальные ресурсы NuGet, такой как http - запрос кэша, временном кэше или в папке пакеты глобального уровня компьютера.</span><span class="sxs-lookup"><span data-stu-id="ac2ce-111">[**dotnet nuget locals**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="ac2ce-112">[**Принудительная nuget DotNet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): помещает пакет на сервере и публикует его, применимый к nuget.org, Visual Studio Team Services или сторонние серверы NuGet.</span><span class="sxs-lookup"><span data-stu-id="ac2ce-112">[**dotnet nuget push**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="ac2ce-113">[**удалить DotNet nuget**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): удаляет или unlists пакета с сервера, применимые к nuget.org, Visual Studio Team Services или сторонние серверы NuGet.</span><span class="sxs-lookup"><span data-stu-id="ac2ce-113">[**dotnet nuget delete**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
