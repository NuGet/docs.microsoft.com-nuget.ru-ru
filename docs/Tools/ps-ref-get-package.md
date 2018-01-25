---
title: "Справочник по PowerShell Get пакет NuGet | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Ссылка для команды Get-Package PowerShell в консоли диспетчера пакетов NuGet в Visual Studio."
keywords: "Пакет NuGet консоли диспетчера, команд NuGet Powershell, справочник по NuGet Powershell, Get-Package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c38e0da2e98d2e5bf5b4fc165462e9abcfdd73c0
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="0d352-104">Get-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="0d352-104">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="0d352-105">*В этом разделе описываются команды в [консоль диспетчера пакетов NuGet](Package-Manager-Console.md) в Visual Studio в Windows. Общая команда PowerShell Get-Package. в разделе [PowerShell PackageManagement ссылка](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="0d352-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="0d352-106">Возвращает список пакетов, установленных в локальном хранилище, список пакетов из источника пакета при использовании с параметром - ListAvailable или список доступных обновлений, при использовании с параметром - Update.</span><span class="sxs-lookup"><span data-stu-id="0d352-106">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="0d352-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="0d352-107">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="0d352-108">Без параметров `Get-Package` отображается список пакетов, установленных в проекте по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0d352-108">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="0d352-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="0d352-109">Parameters</span></span>

| <span data-ttu-id="0d352-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="0d352-110">Parameter</span></span> | <span data-ttu-id="0d352-111">Описание:</span><span class="sxs-lookup"><span data-stu-id="0d352-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0d352-112">Исходный код</span><span class="sxs-lookup"><span data-stu-id="0d352-112">Source</span></span> | <span data-ttu-id="0d352-113">Путь URL-адрес или папку для пакета.</span><span class="sxs-lookup"><span data-stu-id="0d352-113">The URL or folder path for the package .</span></span> <span data-ttu-id="0d352-114">Пути к локальной папке может быть абсолютным или относительным для текущей папки.</span><span class="sxs-lookup"><span data-stu-id="0d352-114">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="0d352-115">Если не указано, `Get-Package` выполняет поиск в текущем выбранном источнике пакетов.</span><span class="sxs-lookup"><span data-stu-id="0d352-115">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="0d352-116">При использовании с флагом-ListAvailable, по умолчанию nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0d352-116">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="0d352-117">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="0d352-117">ListAvailable</span></span> | <span data-ttu-id="0d352-118">Список пакетов, доступных в источнике пакетов, по умолчанию принимается nuget.org. Показывает значение по умолчанию 50 пакетов, пока не будут указаны - PageSize или - первый.</span><span class="sxs-lookup"><span data-stu-id="0d352-118">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="0d352-119">Обновления</span><span class="sxs-lookup"><span data-stu-id="0d352-119">Updates</span></span> | <span data-ttu-id="0d352-120">Список пакетов, которые имеют в источнике пакета доступно обновление.</span><span class="sxs-lookup"><span data-stu-id="0d352-120">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="0d352-121">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="0d352-121">ProjectName</span></span> | <span data-ttu-id="0d352-122">Проект, из которого берутся установленные пакеты.</span><span class="sxs-lookup"><span data-stu-id="0d352-122">The project from which to get installed packages.</span></span> <span data-ttu-id="0d352-123">Если не указано, возвращает установленных проекты для всего решения.</span><span class="sxs-lookup"><span data-stu-id="0d352-123">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="0d352-124">Фильтр</span><span class="sxs-lookup"><span data-stu-id="0d352-124">Filter</span></span> | <span data-ttu-id="0d352-125">Строку фильтра, используемого для ограничения списка пакетов, применив его идентификатор пакета, описанию и тегам.</span><span class="sxs-lookup"><span data-stu-id="0d352-125">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="0d352-126">First</span><span class="sxs-lookup"><span data-stu-id="0d352-126">First</span></span> | <span data-ttu-id="0d352-127">Число пакетов, возвращаемых из начала списка.</span><span class="sxs-lookup"><span data-stu-id="0d352-127">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="0d352-128">Если не указано, по умолчанию — 50.</span><span class="sxs-lookup"><span data-stu-id="0d352-128">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="0d352-129">Skip</span><span class="sxs-lookup"><span data-stu-id="0d352-129">Skip</span></span> | <span data-ttu-id="0d352-130">Пропускает первый &lt;int&gt; пакеты из списка.</span><span class="sxs-lookup"><span data-stu-id="0d352-130">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="0d352-131">AllVersions</span><span class="sxs-lookup"><span data-stu-id="0d352-131">AllVersions</span></span> | <span data-ttu-id="0d352-132">Отображает все доступные версии каждого пакета, а не только последняя версия.</span><span class="sxs-lookup"><span data-stu-id="0d352-132">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="0d352-133">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="0d352-133">IncludePrerelease</span></span> | <span data-ttu-id="0d352-134">Предварительные выпуски пакетов включает в результаты.</span><span class="sxs-lookup"><span data-stu-id="0d352-134">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="0d352-135">PageSize</span><span class="sxs-lookup"><span data-stu-id="0d352-135">PageSize</span></span> | <span data-ttu-id="0d352-136">*(3.0 +)*  При использовании с флагом-ListAvailable (обязательно), количество пакетов, чтобы вывести список перед выдачей запроса на продолжение.</span><span class="sxs-lookup"><span data-stu-id="0d352-136">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="0d352-137">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="0d352-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="0d352-138">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="0d352-138">Common Parameters</span></span>

<span data-ttu-id="0d352-139">`Get-Package`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="0d352-139">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="0d352-140">Примеры</span><span class="sxs-lookup"><span data-stu-id="0d352-140">Examples</span></span>

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
