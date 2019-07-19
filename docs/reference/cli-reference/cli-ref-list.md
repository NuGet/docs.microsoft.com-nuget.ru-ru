---
title: Команда списка CLI NuGet
description: Справочник по команде NuGet. exe List
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327741"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="c8330-103">Команда list (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="c8330-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="c8330-104">Область **применения:** использование пакетов, публикация &bullet; **поддерживаемых версий:** все</span><span class="sxs-lookup"><span data-stu-id="c8330-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c8330-105">Отображает список пакетов из заданного источника.</span><span class="sxs-lookup"><span data-stu-id="c8330-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="c8330-106">Если источники не указаны, используются все источники, определенные в глобальном файле `%AppData%\NuGet\NuGet.Config` конфигурации (Windows) или. `~/.nuget/NuGet/NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="c8330-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="c8330-107">Если `NuGet.Config` не указывает источники `list` , использует канал по умолчанию (NuGet.org).</span><span class="sxs-lookup"><span data-stu-id="c8330-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="c8330-108">Использование</span><span class="sxs-lookup"><span data-stu-id="c8330-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="c8330-109">где необязательные условия поиска будут фильтровать отображаемый список.</span><span class="sxs-lookup"><span data-stu-id="c8330-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="c8330-110">Условия поиска применяются к именам пакетов, тегов и описаний пакетов так же, как и при их использовании в nuget.org.</span><span class="sxs-lookup"><span data-stu-id="c8330-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="c8330-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="c8330-111">Options</span></span>

| <span data-ttu-id="c8330-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="c8330-112">Option</span></span> | <span data-ttu-id="c8330-113">Описание</span><span class="sxs-lookup"><span data-stu-id="c8330-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c8330-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="c8330-114">AllVersions</span></span> | <span data-ttu-id="c8330-115">Вывод списка всех версий пакета.</span><span class="sxs-lookup"><span data-stu-id="c8330-115">List all versions of a package.</span></span> <span data-ttu-id="c8330-116">По умолчанию отображается только последняя версия пакета.</span><span class="sxs-lookup"><span data-stu-id="c8330-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="c8330-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c8330-117">ConfigFile</span></span> | <span data-ttu-id="c8330-118">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="c8330-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c8330-119">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="c8330-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c8330-120">форцеенглишаутпут</span><span class="sxs-lookup"><span data-stu-id="c8330-120">ForceEnglishOutput</span></span> | <span data-ttu-id="c8330-121">*(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="c8330-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c8330-122">Help</span><span class="sxs-lookup"><span data-stu-id="c8330-122">Help</span></span> | <span data-ttu-id="c8330-123">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="c8330-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="c8330-124">инклудеделистед</span><span class="sxs-lookup"><span data-stu-id="c8330-124">IncludeDelisted</span></span> | <span data-ttu-id="c8330-125">*(3.2 +)* Отображение пакетов, которые не были перечислены.</span><span class="sxs-lookup"><span data-stu-id="c8330-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="c8330-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c8330-126">NonInteractive</span></span> | <span data-ttu-id="c8330-127">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="c8330-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c8330-128">Предварительной</span><span class="sxs-lookup"><span data-stu-id="c8330-128">PreRelease</span></span> | <span data-ttu-id="c8330-129">Включает в список предварительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="c8330-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="c8330-130">Source</span><span class="sxs-lookup"><span data-stu-id="c8330-130">Source</span></span> | <span data-ttu-id="c8330-131">Указывает список источников пакетов для поиска.</span><span class="sxs-lookup"><span data-stu-id="c8330-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="c8330-132">Verbosity</span><span class="sxs-lookup"><span data-stu-id="c8330-132">Verbosity</span></span> | <span data-ttu-id="c8330-133">Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*.</span><span class="sxs-lookup"><span data-stu-id="c8330-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c8330-134">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c8330-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c8330-135">Примеры</span><span class="sxs-lookup"><span data-stu-id="c8330-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
