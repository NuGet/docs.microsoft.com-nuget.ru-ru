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
# <a name="dotnet-commands"></a><span data-ttu-id="0e5ca-103">Команды dotnet</span><span class="sxs-lookup"><span data-stu-id="0e5ca-103">dotnet commands</span></span>

<span data-ttu-id="0e5ca-104">`dotnet` Интерфейс командной строки, которая выполняется в Windows, Mac OS X и Linux, предоставляет ряд важных nuget.exe команд, приведенные ниже.</span><span class="sxs-lookup"><span data-stu-id="0e5ca-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="0e5ca-105">Если dotnet удовлетворяет вашим требованиям, нет необходимости использовать `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="0e5ca-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="0e5ca-106">Подробные сведения по `dotnet`, в разделе [средства командной строки (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="0e5ca-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="0e5ca-107">Использование пакета</span><span class="sxs-lookup"><span data-stu-id="0e5ca-107">Package consumption</span></span>

- <span data-ttu-id="0e5ca-108">[**DotNet добавить пакет**](/dotnet/core/tools/dotnet-add-package): Добавляет ссылку на пакет в файл проекта, а затем выполняет `dotnet restore` для установки пакета.</span><span class="sxs-lookup"><span data-stu-id="0e5ca-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="0e5ca-109">[**Удаление DotNet пакета**](/dotnet/core/tools/dotnet-remove-package): Удаляет ссылку пакета из файла проекта.</span><span class="sxs-lookup"><span data-stu-id="0e5ca-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="0e5ca-110">[**Восстановление DotNet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): восстанавливает зависимости и средств проекта.</span><span class="sxs-lookup"><span data-stu-id="0e5ca-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="0e5ca-111">Начиная с версии NuGet 4.0 выполняет один и тот же код как `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="0e5ca-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="0e5ca-112">[**локальные переменные nuget DotNet**](/dotnet/core/tools/dotnet-nuget-locals): содержит расположений *глобального пакеты*, *кэша http*, и *temp* папки и очищает содержимое Эти папки.</span><span class="sxs-lookup"><span data-stu-id="0e5ca-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="0e5ca-113">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="0e5ca-113">Package creation</span></span>

- <span data-ttu-id="0e5ca-114">[**пакет DotNet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): пакеты кода в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="0e5ca-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="0e5ca-115">Начиная с версии NuGet 4.0 выполняет один и тот же код как `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="0e5ca-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="0e5ca-116">[**Принудительная nuget DotNet**](/dotnet/core/tools/dotnet-nuget-push): помещает пакет на сервере и публикует его, применимые к nuget.org, Visual Studio Team Services и серверы NuGet сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="0e5ca-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="0e5ca-117">[**удалить DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): удаляет или unlists пакета из узла, применимые к nuget.org, Visual Studio Team Services и серверы NuGet сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="0e5ca-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
