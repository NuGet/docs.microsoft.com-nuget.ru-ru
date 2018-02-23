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
# <a name="dotnet-commands"></a><span data-ttu-id="4b6fa-104">команды dotNet</span><span class="sxs-lookup"><span data-stu-id="4b6fa-104">dotNet commands</span></span>

<span data-ttu-id="4b6fa-105">`dotnet` Интерфейс командной строки, которая выполняется в Windows, Mac OS X и Linux, предоставляет ряд важных nuget.exe команд, приведенные ниже.</span><span class="sxs-lookup"><span data-stu-id="4b6fa-105">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="4b6fa-106">Если dotnet удовлетворяет вашим требованиям, нет необходимости использовать `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="4b6fa-106">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="4b6fa-107">Подробные сведения по `dotnet`, в разделе [средства командной строки (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="4b6fa-107">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="4b6fa-108">Использование пакета</span><span class="sxs-lookup"><span data-stu-id="4b6fa-108">Package consumption</span></span>

- <span data-ttu-id="4b6fa-109">[**DotNet добавить пакет**](/dotnet/core/tools/dotnet-add-package): Добавляет ссылку на пакет в файл проекта, а затем выполняет `dotnet restore` для установки пакета.</span><span class="sxs-lookup"><span data-stu-id="4b6fa-109">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="4b6fa-110">[**Удаление DotNet пакета**](/dotnet/core/tools/dotnet-remove-package): Удаляет ссылку пакета из файла проекта.</span><span class="sxs-lookup"><span data-stu-id="4b6fa-110">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="4b6fa-111">[**Восстановление DotNet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): восстанавливает зависимости и средств проекта.</span><span class="sxs-lookup"><span data-stu-id="4b6fa-111">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="4b6fa-112">Начиная с версии NuGet 4.0 выполняет один и тот же код как `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="4b6fa-112">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="4b6fa-113">[**локальные переменные nuget DotNet**](/dotnet/core/tools/dotnet-nuget-locals): очищает или список локальных ресурсов NuGet кэша HTTP-запроса, временном кэше и папке пакеты глобального уровня компьютера.</span><span class="sxs-lookup"><span data-stu-id="4b6fa-113">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as the http-request cache, the temporary cache, and the machine-wide global packages folder.</span></span>

## <a name="package-creation"></a><span data-ttu-id="4b6fa-114">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="4b6fa-114">Package creation</span></span>

- <span data-ttu-id="4b6fa-115">[**пакет DotNet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): пакеты кода в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="4b6fa-115">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="4b6fa-116">Начиная с версии NuGet 4.0 выполняет один и тот же код как `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="4b6fa-116">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="4b6fa-117">[**Принудительная nuget DotNet**](/dotnet/core/tools/dotnet-nuget-push): помещает пакет на сервере и публикует его, применимые к nuget.org, Visual Studio Team Services и серверы NuGet сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="4b6fa-117">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="4b6fa-118">[**удалить DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): удаляет или unlists пакета из узла, применимые к nuget.org, Visual Studio Team Services и серверы NuGet сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="4b6fa-118">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
