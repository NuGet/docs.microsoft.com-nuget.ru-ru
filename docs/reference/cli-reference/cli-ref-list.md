---
title: Команда списка CLI NuGet
description: Справочник по команде NuGet. exe List
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813342"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="62bcb-103">Команда list (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="62bcb-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="62bcb-104">Область **применения:** использование пакетов, публикация &bullet; **Поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="62bcb-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="62bcb-105">Отображает список пакетов из заданного источника.</span><span class="sxs-lookup"><span data-stu-id="62bcb-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="62bcb-106">Если источники не указаны, используются все источники, определенные в глобальном файле конфигурации `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="62bcb-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="62bcb-107">Если `NuGet.Config` не указывает источники, `list` использует канал по умолчанию (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="62bcb-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="62bcb-108">Метрики</span><span class="sxs-lookup"><span data-stu-id="62bcb-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="62bcb-109">где необязательные условия поиска будут фильтровать отображаемый список.</span><span class="sxs-lookup"><span data-stu-id="62bcb-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="62bcb-110">Условия поиска применяются к именам пакетов, тегов и описаний пакетов так же, как и при их использовании в nuget.org.</span><span class="sxs-lookup"><span data-stu-id="62bcb-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="62bcb-111">Options</span><span class="sxs-lookup"><span data-stu-id="62bcb-111">Options</span></span>

| <span data-ttu-id="62bcb-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="62bcb-112">Option</span></span> | <span data-ttu-id="62bcb-113">Описание</span><span class="sxs-lookup"><span data-stu-id="62bcb-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="62bcb-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="62bcb-114">AllVersions</span></span> | <span data-ttu-id="62bcb-115">Вывод списка всех версий пакета.</span><span class="sxs-lookup"><span data-stu-id="62bcb-115">List all versions of a package.</span></span> <span data-ttu-id="62bcb-116">По умолчанию отображается только последняя версия пакета.</span><span class="sxs-lookup"><span data-stu-id="62bcb-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="62bcb-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="62bcb-117">ConfigFile</span></span> | <span data-ttu-id="62bcb-118">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="62bcb-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="62bcb-119">Если не указано, используется `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="62bcb-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="62bcb-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="62bcb-120">ForceEnglishOutput</span></span> | <span data-ttu-id="62bcb-121">*(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="62bcb-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="62bcb-122">Справка</span><span class="sxs-lookup"><span data-stu-id="62bcb-122">Help</span></span> | <span data-ttu-id="62bcb-123">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="62bcb-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="62bcb-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="62bcb-124">IncludeDelisted</span></span> | <span data-ttu-id="62bcb-125">*(3.2 +)* Отображение пакетов, которые не были перечислены.</span><span class="sxs-lookup"><span data-stu-id="62bcb-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="62bcb-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="62bcb-126">NonInteractive</span></span> | <span data-ttu-id="62bcb-127">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="62bcb-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="62bcb-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="62bcb-128">PreRelease</span></span> | <span data-ttu-id="62bcb-129">Включает в список предварительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="62bcb-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="62bcb-130">Source</span><span class="sxs-lookup"><span data-stu-id="62bcb-130">Source</span></span> | <span data-ttu-id="62bcb-131">Указывает список источников пакетов для поиска.</span><span class="sxs-lookup"><span data-stu-id="62bcb-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="62bcb-132">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="62bcb-132">Verbosity</span></span> | <span data-ttu-id="62bcb-133">Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*.</span><span class="sxs-lookup"><span data-stu-id="62bcb-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="62bcb-134">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="62bcb-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="62bcb-135">Примеры</span><span class="sxs-lookup"><span data-stu-id="62bcb-135">Examples</span></span>

<span data-ttu-id="62bcb-136">Список всех пакетов из настроенных веб-каналов:</span><span class="sxs-lookup"><span data-stu-id="62bcb-136">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="62bcb-137">Перечисление пакетов, связанных с Azure, с подробным уровнем детализации:</span><span class="sxs-lookup"><span data-stu-id="62bcb-137">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="62bcb-138">Вывод списка всех версий пакетов, связанных с Azure, из настроенных веб-каналов:</span><span class="sxs-lookup"><span data-stu-id="62bcb-138">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="62bcb-139">Вывод списка всех версий пакетов, связанных с JSON, из указанного источника или веб-канала:</span><span class="sxs-lookup"><span data-stu-id="62bcb-139">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="62bcb-140">Список пакетов, связанных с JSON, из нескольких источников и веб-каналов:</span><span class="sxs-lookup"><span data-stu-id="62bcb-140">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

