---
title: Справочник по Get-Package PowerShell для NuGet
description: Справочник по Get-Package команде PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 1576e3f20eba1ecdd099b1e7c23aef6b1a1a0a4f
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237235"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="81b93-103">Get-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="81b93-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="81b93-104">*В этом разделе описывается команда в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows. Общие команды PowerShell Get-Package см. в [справочнике по PackageManagement для PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="81b93-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="81b93-105">Получение списка пакетов, установленных в локальном репозитории, список пакетов, доступных из источника пакета при использовании с параметром-ListAvailable, или список доступных обновлений при использовании с параметром-Update.</span><span class="sxs-lookup"><span data-stu-id="81b93-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="81b93-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="81b93-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="81b93-107">Без параметров `Get-Package` отображает список пакетов, установленных в проекте по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="81b93-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="81b93-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="81b93-108">Parameters</span></span>

| <span data-ttu-id="81b93-109">Параметр</span><span class="sxs-lookup"><span data-stu-id="81b93-109">Parameter</span></span> | <span data-ttu-id="81b93-110">Описание</span><span class="sxs-lookup"><span data-stu-id="81b93-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="81b93-111">Источник</span><span class="sxs-lookup"><span data-stu-id="81b93-111">Source</span></span> | <span data-ttu-id="81b93-112">URL-адрес или путь к папке для пакета.</span><span class="sxs-lookup"><span data-stu-id="81b93-112">The URL or folder path for the package .</span></span> <span data-ttu-id="81b93-113">Пути к локальным папкам могут быть абсолютными или относительно текущей папки.</span><span class="sxs-lookup"><span data-stu-id="81b93-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="81b93-114">Если этот параметр опущен, `Get-Package` Поиск выполняется в текущем выбранном источнике пакета.</span><span class="sxs-lookup"><span data-stu-id="81b93-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="81b93-115">При использовании с параметром-ListAvailable по умолчанию принимает значение nuget.org.</span><span class="sxs-lookup"><span data-stu-id="81b93-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="81b93-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="81b93-116">ListAvailable</span></span> | <span data-ttu-id="81b93-117">Выводит список пакетов, доступных из источника пакета, по умолчанию — nuget.org. Показывает значение по умолчанию для пакетов 50, если не указаны значения-PageSize и/или-First.</span><span class="sxs-lookup"><span data-stu-id="81b93-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="81b93-118">Обновления</span><span class="sxs-lookup"><span data-stu-id="81b93-118">Updates</span></span> | <span data-ttu-id="81b93-119">Перечисляет пакеты с обновлением, доступным в источнике пакета.</span><span class="sxs-lookup"><span data-stu-id="81b93-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="81b93-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="81b93-120">ProjectName</span></span> | <span data-ttu-id="81b93-121">Проект, из которого получаются установленные пакеты.</span><span class="sxs-lookup"><span data-stu-id="81b93-121">The project from which to get installed packages.</span></span> <span data-ttu-id="81b93-122">Если этот параметр опущен, то возвращает установленные проекты для всего решения.</span><span class="sxs-lookup"><span data-stu-id="81b93-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="81b93-123">Filter</span><span class="sxs-lookup"><span data-stu-id="81b93-123">Filter</span></span> | <span data-ttu-id="81b93-124">Строка фильтра, используемая для уменьшения списка пакетов путем его применения к ИДЕНТИФИКАТОРу, описанию и тегам пакета.</span><span class="sxs-lookup"><span data-stu-id="81b93-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="81b93-125">First</span><span class="sxs-lookup"><span data-stu-id="81b93-125">First</span></span> | <span data-ttu-id="81b93-126">Число пакетов, возвращаемых с начала списка.</span><span class="sxs-lookup"><span data-stu-id="81b93-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="81b93-127">Если не указано, по умолчанию используется значение 50.</span><span class="sxs-lookup"><span data-stu-id="81b93-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="81b93-128">Пропустить</span><span class="sxs-lookup"><span data-stu-id="81b93-128">Skip</span></span> | <span data-ttu-id="81b93-129">Опускает первые &lt; целочисленные &gt; пакеты из отображаемого списка.</span><span class="sxs-lookup"><span data-stu-id="81b93-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="81b93-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="81b93-130">AllVersions</span></span> | <span data-ttu-id="81b93-131">Отображает все доступные версии каждого пакета, а не только последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="81b93-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="81b93-132">инклудепререлеасе</span><span class="sxs-lookup"><span data-stu-id="81b93-132">IncludePrerelease</span></span> | <span data-ttu-id="81b93-133">Включает в результаты предварительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="81b93-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="81b93-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="81b93-134">PageSize</span></span> | <span data-ttu-id="81b93-135">*(3.0 +)* Если используется с параметром-ListAvailable (обязательно), число пакетов, которые необходимо вывести в список, прежде чем будет предложено продолжить.</span><span class="sxs-lookup"><span data-stu-id="81b93-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="81b93-136">Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="81b93-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="81b93-137">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="81b93-137">Common Parameters</span></span>

<span data-ttu-id="81b93-138">`Get-Package` поддерживает следующие [Общие параметры PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="81b93-138">`Get-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="81b93-139">Примеры</span><span class="sxs-lookup"><span data-stu-id="81b93-139">Examples</span></span>

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```