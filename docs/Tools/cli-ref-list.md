---
title: "Команда list NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: "Справочник по команду nuget.exe"
keywords: "Справочник по список NuGet, команда список пакетов"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="3b1ba-104">Команда List (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3b1ba-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="3b1ba-105">**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="3b1ba-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="3b1ba-106">Отображает список пакетов из данного источника.</span><span class="sxs-lookup"><span data-stu-id="3b1ba-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="3b1ba-107">Если не указан ни один из источников, все источники, определенные в файле Глобальная конфигурация `%AppData%\NuGet\NuGet.Config`, используются.</span><span class="sxs-lookup"><span data-stu-id="3b1ba-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="3b1ba-108">Если `NuGet.Config` указывает нет источников, затем `list` использует стандартный канал (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="3b1ba-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="3b1ba-109">Использование</span><span class="sxs-lookup"><span data-stu-id="3b1ba-109">Usage</span></span>

```
nuget list [search terms] [options]
```

<span data-ttu-id="3b1ba-110">где отображается список будет отфильтрован условия поиска необязательно.</span><span class="sxs-lookup"><span data-stu-id="3b1ba-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="3b1ba-111">Условия поиска применяются к имена пакетов, теги и описание пакета.</span><span class="sxs-lookup"><span data-stu-id="3b1ba-111">Search terms are applied to the names of packages, tags, and package descriptions.</span></span>

## <a name="options"></a><span data-ttu-id="3b1ba-112">Параметры</span><span class="sxs-lookup"><span data-stu-id="3b1ba-112">Options</span></span>
| <span data-ttu-id="3b1ba-113">Параметр</span><span class="sxs-lookup"><span data-stu-id="3b1ba-113">Option</span></span> | <span data-ttu-id="3b1ba-114">Описание</span><span class="sxs-lookup"><span data-stu-id="3b1ba-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3b1ba-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="3b1ba-115">AllVersions</span></span> | <span data-ttu-id="3b1ba-116">Вывести все версии пакета.</span><span class="sxs-lookup"><span data-stu-id="3b1ba-116">List all versions of a package.</span></span> <span data-ttu-id="3b1ba-117">По умолчанию отображается только последняя версия пакета.</span><span class="sxs-lookup"><span data-stu-id="3b1ba-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="3b1ba-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3b1ba-118">ConfigFile</span></span> | <span data-ttu-id="3b1ba-119">*(2.5 +)*  NuGet файла конфигурации для применения.</span><span class="sxs-lookup"><span data-stu-id="3b1ba-119">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="3b1ba-120">Если не указан, *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="3b1ba-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="3b1ba-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3b1ba-121">ForceEnglishOutput</span></span> | <span data-ttu-id="3b1ba-122">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="3b1ba-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3b1ba-123">Справка</span><span class="sxs-lookup"><span data-stu-id="3b1ba-123">Help</span></span> | <span data-ttu-id="3b1ba-124">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="3b1ba-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="3b1ba-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="3b1ba-125">IncludeDelisted</span></span> | <span data-ttu-id="3b1ba-126">*(3.2 +)*  Отображение отсутствующие в списке пакетов.</span><span class="sxs-lookup"><span data-stu-id="3b1ba-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="3b1ba-127">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="3b1ba-127">NonInteractive</span></span> | <span data-ttu-id="3b1ba-128">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="3b1ba-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3b1ba-129">Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="3b1ba-129">PreRelease</span></span> | <span data-ttu-id="3b1ba-130">Содержит предварительные версии пакетов в списке.</span><span class="sxs-lookup"><span data-stu-id="3b1ba-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="3b1ba-131">Исходный код</span><span class="sxs-lookup"><span data-stu-id="3b1ba-131">Source</span></span> | <span data-ttu-id="3b1ba-132">Указывает список источников пакетов для поиска.</span><span class="sxs-lookup"><span data-stu-id="3b1ba-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="3b1ba-133">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="3b1ba-133">Verbosity</span></span> | <span data-ttu-id="3b1ba-134">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="3b1ba-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="3b1ba-135">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3b1ba-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3b1ba-136">Примеры</span><span class="sxs-lookup"><span data-stu-id="3b1ba-136">Examples</span></span>

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
