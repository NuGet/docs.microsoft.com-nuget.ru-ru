---
title: Команда поиска интерфейса командной строки NuGet
description: Справочник по команде поиска nuget.exe
author: advay26
ms.author: t-adtand
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 8d63efefb8f14c03fbe3986d8d7eebcc3eb5bcac
ms.sourcegitcommit: 6cda91f135e58cf57a2471b0c7c4a2f748f40024
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/02/2020
ms.locfileid: "89359686"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="3cfc4-103">Команда Search (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="3cfc4-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="3cfc4-104">Область **применения:** &bullet; **Поддерживаемые версии** для использования пакетов: 5.8 +</span><span class="sxs-lookup"><span data-stu-id="3cfc4-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="3cfc4-105">Выполняет поиск в заданном источнике с помощью предоставленной строки запроса.</span><span class="sxs-lookup"><span data-stu-id="3cfc4-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="3cfc4-106">Если источники не указаны, используются все источники, определенные в% AppData% \NuGet\NuGet.config.</span><span class="sxs-lookup"><span data-stu-id="3cfc4-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="3cfc4-107">Использование</span><span class="sxs-lookup"><span data-stu-id="3cfc4-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="3cfc4-108">где условия поиска применяются к именам пакетов, тегов и описаний пакетов так же, как и при их использовании в nuget.org.</span><span class="sxs-lookup"><span data-stu-id="3cfc4-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="3cfc4-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="3cfc4-109">Options</span></span>

| <span data-ttu-id="3cfc4-110">Имя</span><span class="sxs-lookup"><span data-stu-id="3cfc4-110">Name</span></span> | <span data-ttu-id="3cfc4-111">Описание</span><span class="sxs-lookup"><span data-stu-id="3cfc4-111">Description</span></span> | <span data-ttu-id="3cfc4-112">Использование</span><span class="sxs-lookup"><span data-stu-id="3cfc4-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="3cfc4-113">Предварительной</span><span class="sxs-lookup"><span data-stu-id="3cfc4-113">PreRelease</span></span> | <span data-ttu-id="3cfc4-114">Пакеты предварительной версии не включаются по умолчанию, но могут быть включены с помощью этого аргумента</span><span class="sxs-lookup"><span data-stu-id="3cfc4-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="3cfc4-115">— Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="3cfc4-115">-PreRelease</span></span> |
| <span data-ttu-id="3cfc4-116">Источник</span><span class="sxs-lookup"><span data-stu-id="3cfc4-116">Source</span></span> | <span data-ttu-id="3cfc4-117">Конкретные источники пакетов для поиска вместо запроса источников по умолчанию в __nuget.config__</span><span class="sxs-lookup"><span data-stu-id="3cfc4-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="3cfc4-118">-Источник `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="3cfc4-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="3cfc4-119">Take</span><span class="sxs-lookup"><span data-stu-id="3cfc4-119">Take</span></span> | <span data-ttu-id="3cfc4-120">Число возвращаемых результатов.</span><span class="sxs-lookup"><span data-stu-id="3cfc4-120">The number of results to return.</span></span> <span data-ttu-id="3cfc4-121">Значение по умолчанию — 20.</span><span class="sxs-lookup"><span data-stu-id="3cfc4-121">The default value is 20.</span></span> | <span data-ttu-id="3cfc4-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="3cfc4-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="3cfc4-123">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="3cfc4-123">Verbosity</span></span> | <span data-ttu-id="3cfc4-124">Уровень детализации, отображаемый в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="3cfc4-124">The level of detail to display in the output.</span></span> <span data-ttu-id="3cfc4-125">Значение по умолчанию — _Обычная_.</span><span class="sxs-lookup"><span data-stu-id="3cfc4-125">The default is _normal_.</span></span> <span data-ttu-id="3cfc4-126">(См. Примечание ниже)</span><span class="sxs-lookup"><span data-stu-id="3cfc4-126">(See the note below)</span></span>  | <span data-ttu-id="3cfc4-127">— Уровень детализации `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="3cfc4-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="3cfc4-128">Справка</span><span class="sxs-lookup"><span data-stu-id="3cfc4-128">Help</span></span> | <span data-ttu-id="3cfc4-129">Отображает справочные сведения для команды</span><span class="sxs-lookup"><span data-stu-id="3cfc4-129">Displays help information for the command</span></span> | <span data-ttu-id="3cfc4-130">-Справка</span><span class="sxs-lookup"><span data-stu-id="3cfc4-130">-Help</span></span> |

<span data-ttu-id="3cfc4-131">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3cfc4-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="3cfc4-132">Уровни детализации:</span><span class="sxs-lookup"><span data-stu-id="3cfc4-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="3cfc4-133">_quiet_ — идентификатор пакета, версия</span><span class="sxs-lookup"><span data-stu-id="3cfc4-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="3cfc4-134">_Обычная_ — идентификатор пакета, версия, загрузки, предварительный просмотр описания</span><span class="sxs-lookup"><span data-stu-id="3cfc4-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="3cfc4-135">_подробный_ идентификатор пакета, версия, загрузки, полное описание, другие сведения, например URL-адрес запроса</span><span class="sxs-lookup"><span data-stu-id="3cfc4-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="3cfc4-136">Примеры</span><span class="sxs-lookup"><span data-stu-id="3cfc4-136">Examples</span></span>

<span data-ttu-id="3cfc4-137">Поиск пакетов, связанных с *ведением журнала*, из источников по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="3cfc4-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="3cfc4-138">Поиск пакетов, связанных с *ведением журнала*, с подробным уровнем детализации:</span><span class="sxs-lookup"><span data-stu-id="3cfc4-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="3cfc4-139">Поиск пакетов, связанных с *ведением журнала*, и отображение только основных 5 результатов:</span><span class="sxs-lookup"><span data-stu-id="3cfc4-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="3cfc4-140">Поиск пакетов, связанных с *JSON*, включая предварительные версии, из указанного источника или веб-канала:</span><span class="sxs-lookup"><span data-stu-id="3cfc4-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="3cfc4-141">Поиск пакетов, связанных с *JSON*, из нескольких источников и веб-каналов:</span><span class="sxs-lookup"><span data-stu-id="3cfc4-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
