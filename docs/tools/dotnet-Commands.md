---
title: команды CLI NuGet DotNet
description: Краткая ссылка для команд, связанных с NuGet, с помощью интерфейса командной строки dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496469"
---
# <a name="dotnet-cli-commands"></a><span data-ttu-id="d70b5-103">команды интерфейса командной строки DotNet</span><span class="sxs-lookup"><span data-stu-id="d70b5-103">dotnet CLI commands</span></span>

<span data-ttu-id="d70b5-104">`dotnet` Интерфейса командной строки (CLI), который выполняется в Windows, Mac OS X и Linux, предоставляет ряд основных команд, таких как установка, восстановление и публикация пакетов.</span><span class="sxs-lookup"><span data-stu-id="d70b5-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="d70b5-105">Если dotnet удовлетворяет вашим требованиям, нет необходимости использовать `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="d70b5-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="d70b5-106">Примеры использования этих команд для получения пакетов, см. в разделе [установки и управления пакетами с помощью dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d70b5-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="d70b5-107">Примеры использования этих команд для создания пакетов, см. в разделе [Создание и публикация пакета с помощью dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d70b5-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="d70b5-108">Полный справочник по командам на `dotnet` CLI, см. в разделе [средства интерфейса командной строки (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="d70b5-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="d70b5-109">Использование пакета</span><span class="sxs-lookup"><span data-stu-id="d70b5-109">Package consumption</span></span>

- <span data-ttu-id="d70b5-110">[**Команда DotNet add пакета**](/dotnet/core/tools/dotnet-add-package): Добавляет ссылку на пакет в файл проекта, а затем выполняет `dotnet restore` для установки пакета.</span><span class="sxs-lookup"><span data-stu-id="d70b5-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="d70b5-111">[**пакет удаляется DotNet**](/dotnet/core/tools/dotnet-remove-package): Удаляет ссылку на пакет из файла проекта.</span><span class="sxs-lookup"><span data-stu-id="d70b5-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="d70b5-112">[**Команда DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Восстанавливает зависимости и средства проекта.</span><span class="sxs-lookup"><span data-stu-id="d70b5-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="d70b5-113">По состоянию на NuGet 4.0, это решение работает один и тот же код как `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="d70b5-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="d70b5-114">[**DotNet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Выводит список расположений, из *глобальных пакетов*, *http-cache*, и *temp* папки и очищает содержимое этих папок.</span><span class="sxs-lookup"><span data-stu-id="d70b5-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>
- <span data-ttu-id="d70b5-115">[**новый nugetconfig DotNet**](/dotnet/core/tools/dotnet-new): Создает [ `nuget.config` ](../reference/nuget-config-file.md) файл, чтобы настроить поведение NuGet.</span><span class="sxs-lookup"><span data-stu-id="d70b5-115">[**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new): Creates a [`nuget.config`](../reference/nuget-config-file.md) file to configure NuGet's behavior.</span></span>

## <a name="package-creation"></a><span data-ttu-id="d70b5-116">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="d70b5-116">Package creation</span></span>

- <span data-ttu-id="d70b5-117">[**DotNet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Упаковывает код в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="d70b5-117">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span>
- <span data-ttu-id="d70b5-118">[**DotNet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Публикует пакет на сервере NuGet.</span><span class="sxs-lookup"><span data-stu-id="d70b5-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Publishes a package to a NuGet server.</span></span> <span data-ttu-id="d70b5-119">Применимо к nuget.org, артефакты Azure, и [сторонних серверов NuGet](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="d70b5-119">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
- <span data-ttu-id="d70b5-120">[**удалить DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Удаляет или из списка пакетов на сервере NuGet.</span><span class="sxs-lookup"><span data-stu-id="d70b5-120">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a NuGet server.</span></span> <span data-ttu-id="d70b5-121">Применимо к nuget.org, артефакты Azure, и [сторонних серверов NuGet](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="d70b5-121">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
