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
# <a name="dotnet-commands"></a><span data-ttu-id="4e3af-103">Команды dotnet</span><span class="sxs-lookup"><span data-stu-id="4e3af-103">dotnet commands</span></span>

<span data-ttu-id="4e3af-104">`dotnet` Интерфейса командной строки, который выполняется в Windows, Mac OS X и Linux, предоставляет ряд важных nuget.exe команды, перечисленные ниже.</span><span class="sxs-lookup"><span data-stu-id="4e3af-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="4e3af-105">Если dotnet удовлетворяет вашим требованиям, нет необходимости использовать `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="4e3af-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="4e3af-106">Дополнительные сведения о `dotnet`, см. в разделе [средства интерфейса командной строки (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="4e3af-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="4e3af-107">Использование пакета</span><span class="sxs-lookup"><span data-stu-id="4e3af-107">Package consumption</span></span>

- <span data-ttu-id="4e3af-108">[**Команда DotNet add пакета**](/dotnet/core/tools/dotnet-add-package): Добавляет ссылку на пакет в файл проекта, а затем выполняет `dotnet restore` для установки пакета.</span><span class="sxs-lookup"><span data-stu-id="4e3af-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="4e3af-109">[**пакет удаляется DotNet**](/dotnet/core/tools/dotnet-remove-package): Удаляет ссылку на пакет из файла проекта.</span><span class="sxs-lookup"><span data-stu-id="4e3af-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="4e3af-110">[**Команда DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): восстанавливает зависимости и средства проекта.</span><span class="sxs-lookup"><span data-stu-id="4e3af-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="4e3af-111">По состоянию на NuGet 4.0, это решение работает один и тот же код как `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="4e3af-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="4e3af-112">[**DotNet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): перечислены расположения *глобальных пакетов*, *http-cache*, и *temp* папки и очищает содержимое элемента Эти папки.</span><span class="sxs-lookup"><span data-stu-id="4e3af-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="4e3af-113">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="4e3af-113">Package creation</span></span>

- <span data-ttu-id="4e3af-114">[**DotNet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): упаковывает код в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="4e3af-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="4e3af-115">По состоянию на NuGet 4.0, это решение работает один и тот же код как `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="4e3af-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="4e3af-116">[**DotNet nuget push**](/dotnet/core/tools/dotnet-nuget-push): отправляет пакет на сервер и публикует его, применимые к nuget.org, Visual Studio Team Services и сторонние серверы NuGet.</span><span class="sxs-lookup"><span data-stu-id="4e3af-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="4e3af-117">[**удалить DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): удаляет или из списка пакетов из узла, применимые к nuget.org, Visual Studio Team Services и сторонние серверы NuGet.</span><span class="sxs-lookup"><span data-stu-id="4e3af-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
