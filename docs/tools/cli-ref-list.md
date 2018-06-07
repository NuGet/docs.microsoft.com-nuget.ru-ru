---
title: Команда list NuGet CLI
description: Справочник по команду nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b0f144d8abbba7388fe39cd113e4eeddccbca2c6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818442"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="41de5-103">Команда List (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="41de5-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="41de5-104">**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="41de5-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="41de5-105">Отображает список пакетов из данного источника.</span><span class="sxs-lookup"><span data-stu-id="41de5-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="41de5-106">Если не указан ни один из источников, все источники, определенные в файле Глобальная конфигурация `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config`, используются.</span><span class="sxs-lookup"><span data-stu-id="41de5-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="41de5-107">Если `NuGet.Config` указывает нет источников, затем `list` использует стандартный канал (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="41de5-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="41de5-108">Использование</span><span class="sxs-lookup"><span data-stu-id="41de5-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="41de5-109">где отображается список будет отфильтрован условия поиска необязательно.</span><span class="sxs-lookup"><span data-stu-id="41de5-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="41de5-110">Условия поиска, применяются к имена пакетов, теги и описание пакета, так же как при использовании их в nuget.org.</span><span class="sxs-lookup"><span data-stu-id="41de5-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="41de5-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="41de5-111">Options</span></span>

| <span data-ttu-id="41de5-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="41de5-112">Option</span></span> | <span data-ttu-id="41de5-113">Описание:</span><span class="sxs-lookup"><span data-stu-id="41de5-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="41de5-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="41de5-114">AllVersions</span></span> | <span data-ttu-id="41de5-115">Вывести все версии пакета.</span><span class="sxs-lookup"><span data-stu-id="41de5-115">List all versions of a package.</span></span> <span data-ttu-id="41de5-116">По умолчанию отображается только последняя версия пакета.</span><span class="sxs-lookup"><span data-stu-id="41de5-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="41de5-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="41de5-117">ConfigFile</span></span> | <span data-ttu-id="41de5-118">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="41de5-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="41de5-119">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="41de5-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="41de5-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="41de5-120">ForceEnglishOutput</span></span> | <span data-ttu-id="41de5-121">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="41de5-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="41de5-122">Справка</span><span class="sxs-lookup"><span data-stu-id="41de5-122">Help</span></span> | <span data-ttu-id="41de5-123">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="41de5-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="41de5-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="41de5-124">IncludeDelisted</span></span> | <span data-ttu-id="41de5-125">*(3.2 +)*  Отображение отсутствующие в списке пакетов.</span><span class="sxs-lookup"><span data-stu-id="41de5-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="41de5-126">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="41de5-126">NonInteractive</span></span> | <span data-ttu-id="41de5-127">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="41de5-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="41de5-128">Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="41de5-128">PreRelease</span></span> | <span data-ttu-id="41de5-129">Содержит предварительные версии пакетов в списке.</span><span class="sxs-lookup"><span data-stu-id="41de5-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="41de5-130">Исходный код</span><span class="sxs-lookup"><span data-stu-id="41de5-130">Source</span></span> | <span data-ttu-id="41de5-131">Указывает список источников пакетов для поиска.</span><span class="sxs-lookup"><span data-stu-id="41de5-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="41de5-132">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="41de5-132">Verbosity</span></span> | <span data-ttu-id="41de5-133">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="41de5-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="41de5-134">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="41de5-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="41de5-135">Примеры</span><span class="sxs-lookup"><span data-stu-id="41de5-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
