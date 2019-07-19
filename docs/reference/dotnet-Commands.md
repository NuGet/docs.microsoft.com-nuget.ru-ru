---
title: команды NuGet CLI DotNet
description: Краткий справочник по связанным с NuGet командам с помощью интерфейса командной строки DotNet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327491"
---
# <a name="dotnet-cli-commands"></a><span data-ttu-id="bb0a4-103">команды CLI DotNet</span><span class="sxs-lookup"><span data-stu-id="bb0a4-103">dotnet CLI commands</span></span>

<span data-ttu-id="bb0a4-104">Интерфейс `dotnet` командной строки (CLI), работающий в Windows, Mac OS X и Linux, предоставляет ряд ключевых команд, таких как установка, восстановление и публикация пакетов.</span><span class="sxs-lookup"><span data-stu-id="bb0a4-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="bb0a4-105">Если DotNet удовлетворяет вашим потребностям, нет необходимости использовать `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="bb0a4-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="bb0a4-106">Примеры использования этих команд для использования пакетов см. в разделе [Установка пакетов и управление ими с помощью DotNet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bb0a4-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="bb0a4-107">Примеры использования этих команд для создания пакетов см. в разделе [Создание и Публикация пакета с помощью интерфейса командной строки DotNet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bb0a4-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="bb0a4-108">Полный справочник по `dotnet` командам CLI см. в разделе [средства интерфейса командной строки (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="bb0a4-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="bb0a4-109">Использование пакета</span><span class="sxs-lookup"><span data-stu-id="bb0a4-109">Package consumption</span></span>

- <span data-ttu-id="bb0a4-110">[**Добавление пакета DotNet**](/dotnet/core/tools/dotnet-add-package): Добавляет ссылку на пакет в файл проекта, а затем запускает `dotnet restore` для установки пакета.</span><span class="sxs-lookup"><span data-stu-id="bb0a4-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="bb0a4-111">[**Удаление пакета DotNet**](/dotnet/core/tools/dotnet-remove-package): Удаляет ссылку на пакет из файла проекта.</span><span class="sxs-lookup"><span data-stu-id="bb0a4-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="bb0a4-112">[**DotNet Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Восстанавливает зависимости и средства проекта.</span><span class="sxs-lookup"><span data-stu-id="bb0a4-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="bb0a4-113">В версии NuGet 4.0 при этом выполняется тот же код, что и для команды `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="bb0a4-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="bb0a4-114">[**Локальные объекты NuGet DotNet**](/dotnet/core/tools/dotnet-nuget-locals): Перечисляет расположения папок *Global-Packages*, *HTTP-Cache*и *TEMP* и очищает содержимое этих папок.</span><span class="sxs-lookup"><span data-stu-id="bb0a4-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>
- <span data-ttu-id="bb0a4-115">[**DotNet New нужетконфиг**](/dotnet/core/tools/dotnet-new): [`nuget.config`](../reference/nuget-config-file.md) Создает файл для настройки поведения NuGet.</span><span class="sxs-lookup"><span data-stu-id="bb0a4-115">[**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new): Creates a [`nuget.config`](../reference/nuget-config-file.md) file to configure NuGet's behavior.</span></span>

## <a name="package-creation"></a><span data-ttu-id="bb0a4-116">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="bb0a4-116">Package creation</span></span>

- <span data-ttu-id="bb0a4-117">[**пакет DotNet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Упаковывает код в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="bb0a4-117">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span>
- <span data-ttu-id="bb0a4-118">Команда [**DotNet NuGet Push**](/dotnet/core/tools/dotnet-nuget-push): Публикует пакет на сервере NuGet.</span><span class="sxs-lookup"><span data-stu-id="bb0a4-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Publishes a package to a NuGet server.</span></span> <span data-ttu-id="bb0a4-119">Применимо к nuget.org, Azure Artifacts и [сторонним серверам NuGet](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="bb0a4-119">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
- <span data-ttu-id="bb0a4-120">[**Удаление DotNet NuGet**](/dotnet/core/tools/dotnet-nuget-delete): Удаляет пакет с сервера NuGet или выводит из него список.</span><span class="sxs-lookup"><span data-stu-id="bb0a4-120">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a NuGet server.</span></span> <span data-ttu-id="bb0a4-121">Применимо к nuget.org, Azure Artifacts и [сторонним серверам NuGet](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="bb0a4-121">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
