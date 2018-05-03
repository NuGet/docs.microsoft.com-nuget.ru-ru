---
title: Команда list NuGet CLI
description: Справочник по команду nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4a44c70937e7cb49e472c53e9857e9f44d269f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="7d412-103">Команда List (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7d412-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="7d412-104">**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="7d412-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="7d412-105">Отображает список пакетов из данного источника.</span><span class="sxs-lookup"><span data-stu-id="7d412-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="7d412-106">Если не указан ни один из источников, все источники, определенные в файле Глобальная конфигурация `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config`, используются.</span><span class="sxs-lookup"><span data-stu-id="7d412-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="7d412-107">Если `NuGet.Config` указывает нет источников, затем `list` использует стандартный канал (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="7d412-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="7d412-108">Использование</span><span class="sxs-lookup"><span data-stu-id="7d412-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="7d412-109">где отображается список будет отфильтрован условия поиска необязательно.</span><span class="sxs-lookup"><span data-stu-id="7d412-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="7d412-110">Условия поиска, применяются к имена пакетов, теги и описание пакета, так же как при использовании их в nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7d412-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="7d412-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="7d412-111">Options</span></span>

| <span data-ttu-id="7d412-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="7d412-112">Option</span></span> | <span data-ttu-id="7d412-113">Описание</span><span class="sxs-lookup"><span data-stu-id="7d412-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7d412-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="7d412-114">AllVersions</span></span> | <span data-ttu-id="7d412-115">Вывести все версии пакета.</span><span class="sxs-lookup"><span data-stu-id="7d412-115">List all versions of a package.</span></span> <span data-ttu-id="7d412-116">По умолчанию отображается только последняя версия пакета.</span><span class="sxs-lookup"><span data-stu-id="7d412-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="7d412-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7d412-117">ConfigFile</span></span> | <span data-ttu-id="7d412-118">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="7d412-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7d412-119">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="7d412-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7d412-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7d412-120">ForceEnglishOutput</span></span> | <span data-ttu-id="7d412-121">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="7d412-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7d412-122">Справка</span><span class="sxs-lookup"><span data-stu-id="7d412-122">Help</span></span> | <span data-ttu-id="7d412-123">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="7d412-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="7d412-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="7d412-124">IncludeDelisted</span></span> | <span data-ttu-id="7d412-125">*(3.2 +)*  Отображение отсутствующие в списке пакетов.</span><span class="sxs-lookup"><span data-stu-id="7d412-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="7d412-126">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="7d412-126">NonInteractive</span></span> | <span data-ttu-id="7d412-127">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="7d412-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7d412-128">Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="7d412-128">PreRelease</span></span> | <span data-ttu-id="7d412-129">Содержит предварительные версии пакетов в списке.</span><span class="sxs-lookup"><span data-stu-id="7d412-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="7d412-130">Исходный код</span><span class="sxs-lookup"><span data-stu-id="7d412-130">Source</span></span> | <span data-ttu-id="7d412-131">Указывает список источников пакетов для поиска.</span><span class="sxs-lookup"><span data-stu-id="7d412-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="7d412-132">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="7d412-132">Verbosity</span></span> | <span data-ttu-id="7d412-133">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="7d412-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7d412-134">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7d412-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7d412-135">Примеры</span><span class="sxs-lookup"><span data-stu-id="7d412-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
