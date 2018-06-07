---
title: Справочник по PowerShell Get пакет NuGet
description: Ссылка для команды Get-Package PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f4b71fc44e44dcbd5d123a0e2fed63adb79964b5
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818507"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="36f71-103">Get-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="36f71-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="36f71-104">*В этом разделе описываются команды в [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows. Общая команда PowerShell Get-Package. в разделе [PowerShell PackageManagement ссылка](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="36f71-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="36f71-105">Возвращает список пакетов, установленных в локальном хранилище, список пакетов из источника пакета при использовании с параметром - ListAvailable или список доступных обновлений, при использовании с параметром - Update.</span><span class="sxs-lookup"><span data-stu-id="36f71-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="36f71-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="36f71-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="36f71-107">Без параметров `Get-Package` отображается список пакетов, установленных в проекте по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="36f71-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="36f71-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="36f71-108">Parameters</span></span>

| <span data-ttu-id="36f71-109">Параметр</span><span class="sxs-lookup"><span data-stu-id="36f71-109">Parameter</span></span> | <span data-ttu-id="36f71-110">Описание:</span><span class="sxs-lookup"><span data-stu-id="36f71-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="36f71-111">Исходный код</span><span class="sxs-lookup"><span data-stu-id="36f71-111">Source</span></span> | <span data-ttu-id="36f71-112">Путь URL-адрес или папку для пакета.</span><span class="sxs-lookup"><span data-stu-id="36f71-112">The URL or folder path for the package .</span></span> <span data-ttu-id="36f71-113">Пути к локальной папке может быть абсолютным или относительным для текущей папки.</span><span class="sxs-lookup"><span data-stu-id="36f71-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="36f71-114">Если не указано, `Get-Package` выполняет поиск в текущем выбранном источнике пакетов.</span><span class="sxs-lookup"><span data-stu-id="36f71-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="36f71-115">При использовании с флагом-ListAvailable, по умолчанию nuget.org.</span><span class="sxs-lookup"><span data-stu-id="36f71-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="36f71-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="36f71-116">ListAvailable</span></span> | <span data-ttu-id="36f71-117">Список пакетов, доступных в источнике пакетов, по умолчанию принимается nuget.org. Показывает значение по умолчанию 50 пакетов, пока не будут указаны - PageSize или - первый.</span><span class="sxs-lookup"><span data-stu-id="36f71-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="36f71-118">Обновления</span><span class="sxs-lookup"><span data-stu-id="36f71-118">Updates</span></span> | <span data-ttu-id="36f71-119">Список пакетов, которые имеют в источнике пакета доступно обновление.</span><span class="sxs-lookup"><span data-stu-id="36f71-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="36f71-120">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="36f71-120">ProjectName</span></span> | <span data-ttu-id="36f71-121">Проект, из которого берутся установленные пакеты.</span><span class="sxs-lookup"><span data-stu-id="36f71-121">The project from which to get installed packages.</span></span> <span data-ttu-id="36f71-122">Если не указано, возвращает установленных проекты для всего решения.</span><span class="sxs-lookup"><span data-stu-id="36f71-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="36f71-123">Фильтр</span><span class="sxs-lookup"><span data-stu-id="36f71-123">Filter</span></span> | <span data-ttu-id="36f71-124">Строку фильтра, используемого для ограничения списка пакетов, применив его идентификатор пакета, описанию и тегам.</span><span class="sxs-lookup"><span data-stu-id="36f71-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="36f71-125">First</span><span class="sxs-lookup"><span data-stu-id="36f71-125">First</span></span> | <span data-ttu-id="36f71-126">Число пакетов, возвращаемых из начала списка.</span><span class="sxs-lookup"><span data-stu-id="36f71-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="36f71-127">Если не указано, по умолчанию — 50.</span><span class="sxs-lookup"><span data-stu-id="36f71-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="36f71-128">Skip</span><span class="sxs-lookup"><span data-stu-id="36f71-128">Skip</span></span> | <span data-ttu-id="36f71-129">Пропускает первый &lt;int&gt; пакеты из списка.</span><span class="sxs-lookup"><span data-stu-id="36f71-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="36f71-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="36f71-130">AllVersions</span></span> | <span data-ttu-id="36f71-131">Отображает все доступные версии каждого пакета, а не только последняя версия.</span><span class="sxs-lookup"><span data-stu-id="36f71-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="36f71-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="36f71-132">IncludePrerelease</span></span> | <span data-ttu-id="36f71-133">Предварительные выпуски пакетов включает в результаты.</span><span class="sxs-lookup"><span data-stu-id="36f71-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="36f71-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="36f71-134">PageSize</span></span> | <span data-ttu-id="36f71-135">*(3.0 +)*  При использовании с флагом-ListAvailable (обязательно), количество пакетов, чтобы вывести список перед выдачей запроса на продолжение.</span><span class="sxs-lookup"><span data-stu-id="36f71-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="36f71-136">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="36f71-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="36f71-137">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="36f71-137">Common Parameters</span></span>

<span data-ttu-id="36f71-138">`Get-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="36f71-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="36f71-139">Примеры</span><span class="sxs-lookup"><span data-stu-id="36f71-139">Examples</span></span>

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
