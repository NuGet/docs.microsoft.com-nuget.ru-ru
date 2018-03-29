---
title: Команда list NuGet CLI | Документы Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Справочник по команду nuget.exe
keywords: Справочник по список NuGet, команда список пакетов
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 61ad02eb99d6c56968c38841498df8aa9f74159d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="5b1ed-104">Команда List (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5b1ed-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="5b1ed-105">**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="5b1ed-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5b1ed-106">Отображает список пакетов из данного источника.</span><span class="sxs-lookup"><span data-stu-id="5b1ed-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="5b1ed-107">Если не указан ни один из источников, все источники, определенные в файле Глобальная конфигурация `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config`, используются.</span><span class="sxs-lookup"><span data-stu-id="5b1ed-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="5b1ed-108">Если `NuGet.Config` указывает нет источников, затем `list` использует стандартный канал (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="5b1ed-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="5b1ed-109">Использование</span><span class="sxs-lookup"><span data-stu-id="5b1ed-109">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="5b1ed-110">где отображается список будет отфильтрован условия поиска необязательно.</span><span class="sxs-lookup"><span data-stu-id="5b1ed-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="5b1ed-111">Условия поиска, применяются к имена пакетов, теги и описание пакета, так же как при использовании их в nuget.org.</span><span class="sxs-lookup"><span data-stu-id="5b1ed-111">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="5b1ed-112">Параметры</span><span class="sxs-lookup"><span data-stu-id="5b1ed-112">Options</span></span>

| <span data-ttu-id="5b1ed-113">Параметр</span><span class="sxs-lookup"><span data-stu-id="5b1ed-113">Option</span></span> | <span data-ttu-id="5b1ed-114">Описание</span><span class="sxs-lookup"><span data-stu-id="5b1ed-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5b1ed-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="5b1ed-115">AllVersions</span></span> | <span data-ttu-id="5b1ed-116">Вывести все версии пакета.</span><span class="sxs-lookup"><span data-stu-id="5b1ed-116">List all versions of a package.</span></span> <span data-ttu-id="5b1ed-117">По умолчанию отображается только последняя версия пакета.</span><span class="sxs-lookup"><span data-stu-id="5b1ed-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="5b1ed-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5b1ed-118">ConfigFile</span></span> | <span data-ttu-id="5b1ed-119">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="5b1ed-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5b1ed-120">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="5b1ed-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5b1ed-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5b1ed-121">ForceEnglishOutput</span></span> | <span data-ttu-id="5b1ed-122">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="5b1ed-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5b1ed-123">Справка</span><span class="sxs-lookup"><span data-stu-id="5b1ed-123">Help</span></span> | <span data-ttu-id="5b1ed-124">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="5b1ed-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="5b1ed-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="5b1ed-125">IncludeDelisted</span></span> | <span data-ttu-id="5b1ed-126">*(3.2 +)*  Отображение отсутствующие в списке пакетов.</span><span class="sxs-lookup"><span data-stu-id="5b1ed-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="5b1ed-127">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="5b1ed-127">NonInteractive</span></span> | <span data-ttu-id="5b1ed-128">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="5b1ed-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5b1ed-129">Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="5b1ed-129">PreRelease</span></span> | <span data-ttu-id="5b1ed-130">Содержит предварительные версии пакетов в списке.</span><span class="sxs-lookup"><span data-stu-id="5b1ed-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="5b1ed-131">Исходный код</span><span class="sxs-lookup"><span data-stu-id="5b1ed-131">Source</span></span> | <span data-ttu-id="5b1ed-132">Указывает список источников пакетов для поиска.</span><span class="sxs-lookup"><span data-stu-id="5b1ed-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="5b1ed-133">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="5b1ed-133">Verbosity</span></span> | <span data-ttu-id="5b1ed-134">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="5b1ed-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5b1ed-135">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5b1ed-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5b1ed-136">Примеры</span><span class="sxs-lookup"><span data-stu-id="5b1ed-136">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
