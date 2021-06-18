---
title: Команда поиска интерфейса командной строки NuGet
description: Справочник по команде поиска nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323665"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="c9870-103">Команда Search (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="c9870-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="c9870-104">Область **применения:** &bullet; **Поддерживаемые версии** для использования пакетов: 5.8 +</span><span class="sxs-lookup"><span data-stu-id="c9870-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="c9870-105">Выполняет поиск в заданном источнике с помощью предоставленной строки запроса.</span><span class="sxs-lookup"><span data-stu-id="c9870-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="c9870-106">Если источники не указаны, используются все источники, определенные в% AppData% \NuGet\NuGet.Config.</span><span class="sxs-lookup"><span data-stu-id="c9870-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.Config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="c9870-107">Использование</span><span class="sxs-lookup"><span data-stu-id="c9870-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="c9870-108">где условия поиска применяются к именам пакетов, тегов и описаний пакетов так же, как и при их использовании в nuget.org.</span><span class="sxs-lookup"><span data-stu-id="c9870-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="c9870-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="c9870-109">Options</span></span>

| <span data-ttu-id="c9870-110">name</span><span class="sxs-lookup"><span data-stu-id="c9870-110">Name</span></span> | <span data-ttu-id="c9870-111">Описание</span><span class="sxs-lookup"><span data-stu-id="c9870-111">Description</span></span> | <span data-ttu-id="c9870-112">Использование</span><span class="sxs-lookup"><span data-stu-id="c9870-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="c9870-113">Предварительной</span><span class="sxs-lookup"><span data-stu-id="c9870-113">PreRelease</span></span> | <span data-ttu-id="c9870-114">Пакеты предварительной версии не включаются по умолчанию, но могут быть включены с помощью этого аргумента</span><span class="sxs-lookup"><span data-stu-id="c9870-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="c9870-115">— Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="c9870-115">-PreRelease</span></span> |
| <span data-ttu-id="c9870-116">Источник</span><span class="sxs-lookup"><span data-stu-id="c9870-116">Source</span></span> | <span data-ttu-id="c9870-117">Конкретные источники пакетов для поиска вместо запроса источников по умолчанию в __nuget.config__</span><span class="sxs-lookup"><span data-stu-id="c9870-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="c9870-118">-Источник `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="c9870-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="c9870-119">Take</span><span class="sxs-lookup"><span data-stu-id="c9870-119">Take</span></span> | <span data-ttu-id="c9870-120">Число возвращаемых результатов.</span><span class="sxs-lookup"><span data-stu-id="c9870-120">The number of results to return.</span></span> <span data-ttu-id="c9870-121">Значение по умолчанию — 20.</span><span class="sxs-lookup"><span data-stu-id="c9870-121">The default value is 20.</span></span> | <span data-ttu-id="c9870-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="c9870-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="c9870-123">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="c9870-123">Verbosity</span></span> | <span data-ttu-id="c9870-124">Уровень детализации, отображаемый в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="c9870-124">The level of detail to display in the output.</span></span> <span data-ttu-id="c9870-125">Значение по умолчанию — _Обычная_.</span><span class="sxs-lookup"><span data-stu-id="c9870-125">The default is _normal_.</span></span> <span data-ttu-id="c9870-126">(См. Примечание ниже)</span><span class="sxs-lookup"><span data-stu-id="c9870-126">(See the note below)</span></span>  | <span data-ttu-id="c9870-127">— Уровень детализации `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="c9870-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="c9870-128">Справка</span><span class="sxs-lookup"><span data-stu-id="c9870-128">Help</span></span> | <span data-ttu-id="c9870-129">Отображает справочные сведения для команды</span><span class="sxs-lookup"><span data-stu-id="c9870-129">Displays help information for the command</span></span> | <span data-ttu-id="c9870-130">-Справка</span><span class="sxs-lookup"><span data-stu-id="c9870-130">-Help</span></span> |

<span data-ttu-id="c9870-131">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c9870-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="c9870-132">Уровни детализации:</span><span class="sxs-lookup"><span data-stu-id="c9870-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="c9870-133">_quiet_ — идентификатор пакета, версия</span><span class="sxs-lookup"><span data-stu-id="c9870-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="c9870-134">_Обычная_ — идентификатор пакета, версия, загрузки, предварительный просмотр описания</span><span class="sxs-lookup"><span data-stu-id="c9870-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="c9870-135">_подробный_ идентификатор пакета, версия, загрузки, полное описание, другие сведения, например URL-адрес запроса</span><span class="sxs-lookup"><span data-stu-id="c9870-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="c9870-136">Примеры</span><span class="sxs-lookup"><span data-stu-id="c9870-136">Examples</span></span>

<span data-ttu-id="c9870-137">Поиск пакетов, связанных с *ведением журнала*, из источников по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="c9870-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="c9870-138">Поиск пакетов, связанных с *ведением журнала*, с подробным уровнем детализации:</span><span class="sxs-lookup"><span data-stu-id="c9870-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="c9870-139">Поиск пакетов, связанных с *ведением журнала*, и отображение только основных 5 результатов:</span><span class="sxs-lookup"><span data-stu-id="c9870-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="c9870-140">Поиск пакетов, связанных с *JSON*, включая предварительные версии, из указанного источника или веб-канала:</span><span class="sxs-lookup"><span data-stu-id="c9870-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="c9870-141">Поиск пакетов, связанных с *JSON*, из нескольких источников и веб-каналов:</span><span class="sxs-lookup"><span data-stu-id="c9870-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
