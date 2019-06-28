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
# <a name="dotnet-cli-commands"></a><span data-ttu-id="b494f-103">команды интерфейса командной строки DotNet</span><span class="sxs-lookup"><span data-stu-id="b494f-103">dotnet CLI commands</span></span>

<span data-ttu-id="b494f-104">`dotnet` Интерфейса командной строки (CLI), который выполняется в Windows, Mac OS X и Linux, предоставляет ряд основных команд, таких как установка, восстановление и публикация пакетов.</span><span class="sxs-lookup"><span data-stu-id="b494f-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="b494f-105">Если dotnet удовлетворяет вашим требованиям, нет необходимости использовать `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="b494f-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="b494f-106">Примеры использования этих команд для получения пакетов, см. в разделе [установки и управления пакетами с помощью dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b494f-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="b494f-107">Примеры использования этих команд для создания пакетов, см. в разделе [создание и публикация пакета с помощью dotnet CLI]... / quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b494f-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI]../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="b494f-108">Полный справочник по командам на `dotnet` CLI, см. в разделе [средства интерфейса командной строки (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="b494f-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="b494f-109">Использование пакета</span><span class="sxs-lookup"><span data-stu-id="b494f-109">Package consumption</span></span>

- <span data-ttu-id="b494f-110">[**Команда DotNet add пакета**](/dotnet/core/tools/dotnet-add-package): Добавляет ссылку на пакет в файл проекта, а затем выполняет `dotnet restore` для установки пакета.</span><span class="sxs-lookup"><span data-stu-id="b494f-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="b494f-111">[**пакет удаляется DotNet**](/dotnet/core/tools/dotnet-remove-package): Удаляет ссылку на пакет из файла проекта.</span><span class="sxs-lookup"><span data-stu-id="b494f-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="b494f-112">[**Команда DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Восстанавливает зависимости и средства проекта.</span><span class="sxs-lookup"><span data-stu-id="b494f-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="b494f-113">По состоянию на NuGet 4.0, это решение работает один и тот же код как `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="b494f-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="b494f-114">[**DotNet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Выводит список расположений, из *глобальных пакетов*, *http-cache*, и *temp* папки и очищает содержимое этих папок.</span><span class="sxs-lookup"><span data-stu-id="b494f-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="b494f-115">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="b494f-115">Package creation</span></span>

- <span data-ttu-id="b494f-116">[**DotNet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Упаковывает код в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="b494f-116">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="b494f-117">По состоянию на NuGet 4.0, это решение работает один и тот же код как `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="b494f-117">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="b494f-118">[**DotNet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Отправляет пакет на сервер и публикует его, применимые к nuget.org, Visual Studio Team Services и сторонние серверы NuGet.</span><span class="sxs-lookup"><span data-stu-id="b494f-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="b494f-119">[**удалить DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Удаляет или из списка пакетов из узла, применимые к nuget.org, Visual Studio Team Services и сторонние серверы NuGet.</span><span class="sxs-lookup"><span data-stu-id="b494f-119">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
