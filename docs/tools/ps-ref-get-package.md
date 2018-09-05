---
title: Справочник по PowerShell Get пакет NuGet
description: Ссылка для команды PowerShell Get-Package в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a28b29614dfe5abdeb24438b3451d96634a120db
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551446"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f3770-103">Get-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f3770-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f3770-104">*В этом разделе описываются команды в [консоли диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows. Общая команда PowerShell Get-Package, см. в разделе [Справочник по PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="f3770-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="f3770-105">Извлекает список пакетов, установленных в локальном репозитории, содержит список пакетов из источника пакета при использовании с параметром - ListAvailable или список доступных обновлений, при использовании с параметром - Update.</span><span class="sxs-lookup"><span data-stu-id="f3770-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="f3770-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="f3770-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="f3770-107">Без параметров `Get-Package` отображается список пакетов, установленных в проекте по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f3770-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="f3770-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="f3770-108">Parameters</span></span>

| <span data-ttu-id="f3770-109">Параметр</span><span class="sxs-lookup"><span data-stu-id="f3770-109">Parameter</span></span> | <span data-ttu-id="f3770-110">Описание</span><span class="sxs-lookup"><span data-stu-id="f3770-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f3770-111">Исходный код</span><span class="sxs-lookup"><span data-stu-id="f3770-111">Source</span></span> | <span data-ttu-id="f3770-112">Путь URL-адрес или папку для пакета.</span><span class="sxs-lookup"><span data-stu-id="f3770-112">The URL or folder path for the package .</span></span> <span data-ttu-id="f3770-113">Пути к локальной папке может быть абсолютным или относительным для текущей папки.</span><span class="sxs-lookup"><span data-stu-id="f3770-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="f3770-114">Если этот параметр опущен, `Get-Package` выполняет поиск в текущем выбранном источнике пакета.</span><span class="sxs-lookup"><span data-stu-id="f3770-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="f3770-115">При использовании с параметром - ListAvailable, по умолчанию на сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f3770-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="f3770-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="f3770-116">ListAvailable</span></span> | <span data-ttu-id="f3770-117">Список пакетов, доступных из источника пакета, установка значений по умолчанию на сайте nuget.org. Показывает 50 пакетов по умолчанию, если не указаны - PageSize и (или) - первый.</span><span class="sxs-lookup"><span data-stu-id="f3770-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="f3770-118">Обновления</span><span class="sxs-lookup"><span data-stu-id="f3770-118">Updates</span></span> | <span data-ttu-id="f3770-119">Список пакетов, для которых доступно обновление из источника пакета.</span><span class="sxs-lookup"><span data-stu-id="f3770-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="f3770-120">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="f3770-120">ProjectName</span></span> | <span data-ttu-id="f3770-121">Проект, из которого необходимо получить установленные пакеты.</span><span class="sxs-lookup"><span data-stu-id="f3770-121">The project from which to get installed packages.</span></span> <span data-ttu-id="f3770-122">Если не указано, возвращает сведения об установленных проекты для всего решения.</span><span class="sxs-lookup"><span data-stu-id="f3770-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="f3770-123">Фильтр</span><span class="sxs-lookup"><span data-stu-id="f3770-123">Filter</span></span> | <span data-ttu-id="f3770-124">Строка фильтра, используемая для сужения списка пакетов, применяя его к идентификатор пакета, описание и теги.</span><span class="sxs-lookup"><span data-stu-id="f3770-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="f3770-125">First</span><span class="sxs-lookup"><span data-stu-id="f3770-125">First</span></span> | <span data-ttu-id="f3770-126">Количество возвращаемых пакетов из начала списка.</span><span class="sxs-lookup"><span data-stu-id="f3770-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="f3770-127">Если не указан, значение по умолчанию — 50.</span><span class="sxs-lookup"><span data-stu-id="f3770-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="f3770-128">Skip</span><span class="sxs-lookup"><span data-stu-id="f3770-128">Skip</span></span> | <span data-ttu-id="f3770-129">Пропускает первый &lt;int&gt; пакеты из отображаемого списка.</span><span class="sxs-lookup"><span data-stu-id="f3770-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="f3770-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="f3770-130">AllVersions</span></span> | <span data-ttu-id="f3770-131">Отображает все доступные версии каждого пакета, а не только последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="f3770-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="f3770-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="f3770-132">IncludePrerelease</span></span> | <span data-ttu-id="f3770-133">Включает в себя предварительные выпуски пакетов в результатах.</span><span class="sxs-lookup"><span data-stu-id="f3770-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="f3770-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="f3770-134">PageSize</span></span> | <span data-ttu-id="f3770-135">*(3.0 и более поздние)*  При использовании - ListAvailable (обязательно), число пакетов в списке перед передачей указаниям, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="f3770-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="f3770-136">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="f3770-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f3770-137">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="f3770-137">Common Parameters</span></span>

<span data-ttu-id="f3770-138">`Get-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладки, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f3770-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f3770-139">Примеры</span><span class="sxs-lookup"><span data-stu-id="f3770-139">Examples</span></span>

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
