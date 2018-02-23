---
title: "Справочник по PowerShell NuGet Find-Package | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Ссылка для команды Find-Package PowerShell в консоли диспетчера пакетов NuGet в Visual Studio."
keywords: "Пакет NuGet консоли диспетчера, команд NuGet Powershell, справочник по NuGet Powershell, Find-Package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4303421c5f11177f3e5fc051a450934df47ab117
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/20/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="3768b-104">Find-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3768b-104">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3768b-105">*Версия 3.0 +; в этом разделе описываются команды в [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows. Общая команда PowerShell Find-Package. в разделе [PowerShell PackageManagement ссылка](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="3768b-105">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="3768b-106">Получает набор удаленных пакетов с указанным Идентификатором или ключевые слова из источника пакета.</span><span class="sxs-lookup"><span data-stu-id="3768b-106">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="3768b-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="3768b-107">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="3768b-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="3768b-108">Parameters</span></span>

| <span data-ttu-id="3768b-109">Параметр</span><span class="sxs-lookup"><span data-stu-id="3768b-109">Parameter</span></span> | <span data-ttu-id="3768b-110">Описание:</span><span class="sxs-lookup"><span data-stu-id="3768b-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3768b-111">Идентификатор &lt;ключевые слова&gt;</span><span class="sxs-lookup"><span data-stu-id="3768b-111">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="3768b-112">(Обязательно) Ключевые слова для поиска источника пакета.</span><span class="sxs-lookup"><span data-stu-id="3768b-112">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="3768b-113">С помощью - ExactMatch возвращать только те пакеты, ключевые слова совпадает с Идентификатором пакета.</span><span class="sxs-lookup"><span data-stu-id="3768b-113">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="3768b-114">Если ключевые слова не заданы, `Find-Package` возвращает список пакетов 20 основных по загрузок или номер заданные - сначала.</span><span class="sxs-lookup"><span data-stu-id="3768b-114">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="3768b-115">Обратите внимание, что - идентификатор является необязательным и холостой.</span><span class="sxs-lookup"><span data-stu-id="3768b-115">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="3768b-116">Исходный код</span><span class="sxs-lookup"><span data-stu-id="3768b-116">Source</span></span> | <span data-ttu-id="3768b-117">Путь URL-адрес или папку источника пакета для поиска.</span><span class="sxs-lookup"><span data-stu-id="3768b-117">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="3768b-118">Пути к локальной папке может быть абсолютным или относительным для текущей папки.</span><span class="sxs-lookup"><span data-stu-id="3768b-118">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="3768b-119">Если не указано, `Find-Package` выполняет поиск в текущем выбранном источнике пакетов.</span><span class="sxs-lookup"><span data-stu-id="3768b-119">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="3768b-120">AllVersions</span><span class="sxs-lookup"><span data-stu-id="3768b-120">AllVersions</span></span> | <span data-ttu-id="3768b-121">Отображает все доступные версии каждого пакета, а не только последняя версия.</span><span class="sxs-lookup"><span data-stu-id="3768b-121">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="3768b-122">First</span><span class="sxs-lookup"><span data-stu-id="3768b-122">First</span></span> | <span data-ttu-id="3768b-123">Число пакетов, возвращаемых из начала списка; значение по умолчанию — 20.</span><span class="sxs-lookup"><span data-stu-id="3768b-123">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="3768b-124">Skip</span><span class="sxs-lookup"><span data-stu-id="3768b-124">Skip</span></span> | <span data-ttu-id="3768b-125">Пропускает первый &lt;int&gt; пакеты из списка.</span><span class="sxs-lookup"><span data-stu-id="3768b-125">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="3768b-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="3768b-126">IncludePrerelease</span></span> | <span data-ttu-id="3768b-127">Предварительные выпуски пакетов включает в результаты.</span><span class="sxs-lookup"><span data-stu-id="3768b-127">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="3768b-128">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="3768b-128">ExactMatch</span></span> | <span data-ttu-id="3768b-129">Указанный для использования &lt;ключевые слова&gt; как идентификатор пакета с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="3768b-129">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="3768b-130">StartWith</span><span class="sxs-lookup"><span data-stu-id="3768b-130">StartWith</span></span> | <span data-ttu-id="3768b-131">Возвращает пакеты, пакет идентификатор начинается с &lt;ключевые слова&gt;.</span><span class="sxs-lookup"><span data-stu-id="3768b-131">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="3768b-132">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="3768b-132">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3768b-133">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="3768b-133">Common Parameters</span></span>

<span data-ttu-id="3768b-134">`Find-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3768b-134">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3768b-135">Примеры</span><span class="sxs-lookup"><span data-stu-id="3768b-135">Examples</span></span>

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
