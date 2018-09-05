---
title: Справочник по PowerShell NuGet Find-Package
description: Ссылка для команды PowerShell Find-Package в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: c6797e3778c7095a9abfc6cd87e2337313988c20
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550982"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="dfbc8-103">Find-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="dfbc8-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="dfbc8-104">*3.0 и более поздних версиях; в этом разделе описываются команды в [консоли диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows. Общая команда PowerShell Find-Package, см. в разделе [Справочник по PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="dfbc8-104">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="dfbc8-105">Получает набор удаленные пакеты с указанным Идентификатором или ключевые слова из источника пакета.</span><span class="sxs-lookup"><span data-stu-id="dfbc8-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="dfbc8-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="dfbc8-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="dfbc8-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="dfbc8-107">Parameters</span></span>

| <span data-ttu-id="dfbc8-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="dfbc8-108">Parameter</span></span> | <span data-ttu-id="dfbc8-109">Описание</span><span class="sxs-lookup"><span data-stu-id="dfbc8-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dfbc8-110">Идентификатор &lt;ключевые слова&gt;</span><span class="sxs-lookup"><span data-stu-id="dfbc8-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="dfbc8-111">(Обязательно) Ключевые слова для поиска источника пакета.</span><span class="sxs-lookup"><span data-stu-id="dfbc8-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="dfbc8-112">С помощью - ExactMatch возвращать только те пакеты, в которых идентификатор пакета соответствует ключевые слова.</span><span class="sxs-lookup"><span data-stu-id="dfbc8-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="dfbc8-113">Если ключевые слова не заданы, `Find-Package` возвращает список пакетов 20 наиболее популярных загрузок или номер, указанных по — сначала.</span><span class="sxs-lookup"><span data-stu-id="dfbc8-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="dfbc8-114">Обратите внимание, что - идентификатор не является обязательным и холостой.</span><span class="sxs-lookup"><span data-stu-id="dfbc8-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="dfbc8-115">Исходный код</span><span class="sxs-lookup"><span data-stu-id="dfbc8-115">Source</span></span> | <span data-ttu-id="dfbc8-116">Путь к URL-адрес или папке источника пакета для поиска.</span><span class="sxs-lookup"><span data-stu-id="dfbc8-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="dfbc8-117">Пути к локальной папке может быть абсолютным или относительным для текущей папки.</span><span class="sxs-lookup"><span data-stu-id="dfbc8-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="dfbc8-118">Если этот параметр опущен, `Find-Package` выполняет поиск в текущем выбранном источнике пакета.</span><span class="sxs-lookup"><span data-stu-id="dfbc8-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="dfbc8-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="dfbc8-119">AllVersions</span></span> | <span data-ttu-id="dfbc8-120">Отображает все доступные версии каждого пакета, а не только последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="dfbc8-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="dfbc8-121">First</span><span class="sxs-lookup"><span data-stu-id="dfbc8-121">First</span></span> | <span data-ttu-id="dfbc8-122">Количество возвращаемых пакетов из начала списка. значение по умолчанию — 20.</span><span class="sxs-lookup"><span data-stu-id="dfbc8-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="dfbc8-123">Skip</span><span class="sxs-lookup"><span data-stu-id="dfbc8-123">Skip</span></span> | <span data-ttu-id="dfbc8-124">Пропускает первый &lt;int&gt; пакеты из отображаемого списка.</span><span class="sxs-lookup"><span data-stu-id="dfbc8-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="dfbc8-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="dfbc8-125">IncludePrerelease</span></span> | <span data-ttu-id="dfbc8-126">Включает в себя предварительные выпуски пакетов в результатах.</span><span class="sxs-lookup"><span data-stu-id="dfbc8-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="dfbc8-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="dfbc8-127">ExactMatch</span></span> | <span data-ttu-id="dfbc8-128">Указанный для использования &lt;ключевые слова&gt; как идентификатор пакета, с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="dfbc8-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="dfbc8-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="dfbc8-129">StartWith</span></span> | <span data-ttu-id="dfbc8-130">Возвращает пакеты, пакета, идентификатор начинается с &lt;ключевые слова&gt;.</span><span class="sxs-lookup"><span data-stu-id="dfbc8-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="dfbc8-131">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="dfbc8-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="dfbc8-132">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="dfbc8-132">Common Parameters</span></span>

<span data-ttu-id="dfbc8-133">`Find-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладки, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="dfbc8-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="dfbc8-134">Примеры</span><span class="sxs-lookup"><span data-stu-id="dfbc8-134">Examples</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```
