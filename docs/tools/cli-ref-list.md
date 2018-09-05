---
title: Команда list интерфейса командной строки NuGet
description: Справочник по командам списка nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549805"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="69bdc-103">Команда List (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="69bdc-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="69bdc-104">**Применяется к:** использование пакета, публикация &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="69bdc-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="69bdc-105">Отображает список пакетов из заданного источника.</span><span class="sxs-lookup"><span data-stu-id="69bdc-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="69bdc-106">Если источники не указаны, все источники, определенные в файле Глобальная конфигурация `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config`, используются.</span><span class="sxs-lookup"><span data-stu-id="69bdc-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="69bdc-107">Если `NuGet.Config` указывает нет источников, затем `list` использует веб-канал по умолчанию (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="69bdc-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="69bdc-108">Использование</span><span class="sxs-lookup"><span data-stu-id="69bdc-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="69bdc-109">где необязательно слов будет отфильтровать отображаемый список.</span><span class="sxs-lookup"><span data-stu-id="69bdc-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="69bdc-110">Условия поиска применяются к именам пакетов, теги и описания пакета так же, как это происходит при использовании их на сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="69bdc-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="69bdc-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="69bdc-111">Options</span></span>

| <span data-ttu-id="69bdc-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="69bdc-112">Option</span></span> | <span data-ttu-id="69bdc-113">Описание</span><span class="sxs-lookup"><span data-stu-id="69bdc-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="69bdc-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="69bdc-114">AllVersions</span></span> | <span data-ttu-id="69bdc-115">Список всех версий пакета.</span><span class="sxs-lookup"><span data-stu-id="69bdc-115">List all versions of a package.</span></span> <span data-ttu-id="69bdc-116">По умолчанию отображается только последняя версия пакета.</span><span class="sxs-lookup"><span data-stu-id="69bdc-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="69bdc-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="69bdc-117">ConfigFile</span></span> | <span data-ttu-id="69bdc-118">Чтобы применить файл конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="69bdc-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="69bdc-119">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="69bdc-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="69bdc-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="69bdc-120">ForceEnglishOutput</span></span> | <span data-ttu-id="69bdc-121">*(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры.</span><span class="sxs-lookup"><span data-stu-id="69bdc-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="69bdc-122">Справка</span><span class="sxs-lookup"><span data-stu-id="69bdc-122">Help</span></span> | <span data-ttu-id="69bdc-123">Отображает справку для команды.</span><span class="sxs-lookup"><span data-stu-id="69bdc-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="69bdc-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="69bdc-124">IncludeDelisted</span></span> | <span data-ttu-id="69bdc-125">*(3.2 и более поздние)*  Отображения исключенные пакеты.</span><span class="sxs-lookup"><span data-stu-id="69bdc-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="69bdc-126">Неинтерактивная</span><span class="sxs-lookup"><span data-stu-id="69bdc-126">NonInteractive</span></span> | <span data-ttu-id="69bdc-127">Подавление для пользователя данные или подтверждения.</span><span class="sxs-lookup"><span data-stu-id="69bdc-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="69bdc-128">Предварительные выпуски</span><span class="sxs-lookup"><span data-stu-id="69bdc-128">PreRelease</span></span> | <span data-ttu-id="69bdc-129">Включает в себя предварительные выпуски пакетов в списке.</span><span class="sxs-lookup"><span data-stu-id="69bdc-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="69bdc-130">Исходный код</span><span class="sxs-lookup"><span data-stu-id="69bdc-130">Source</span></span> | <span data-ttu-id="69bdc-131">Указывает список источников пакетов для поиска.</span><span class="sxs-lookup"><span data-stu-id="69bdc-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="69bdc-132">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="69bdc-132">Verbosity</span></span> | <span data-ttu-id="69bdc-133">Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="69bdc-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="69bdc-134">Также см. в разделе [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="69bdc-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="69bdc-135">Примеры</span><span class="sxs-lookup"><span data-stu-id="69bdc-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
