---
title: Команда help NuGet CLI
description: Справочник по командам справки nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: dbfc803e24c824d30e128d6e86cfa3c43660668f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="95438-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="95438-103">help or ?</span></span> <span data-ttu-id="95438-104">Команда (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="95438-104">command (NuGet CLI)</span></span>

<span data-ttu-id="95438-105">**Применяется к:** все &bullet; **поддерживаемые версии**: все</span><span class="sxs-lookup"><span data-stu-id="95438-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="95438-106">Отображаются общие справочные сведения и справочные сведения о конкретных команд.</span><span class="sxs-lookup"><span data-stu-id="95438-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="95438-107">Использование</span><span class="sxs-lookup"><span data-stu-id="95438-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="95438-108">где [команда] определяет той или иной команды для отображения справки.</span><span class="sxs-lookup"><span data-stu-id="95438-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="95438-109">Для некоторых команд, следует учитывать для указания *справки* во-первых, как с `nuget help install`, так как пакет с именем «Справка» на nuget.org. Если вы предоставляете команде `nuget install help`, не сможете получить справку в команду установки, а установит пакет с именем справки.</span><span class="sxs-lookup"><span data-stu-id="95438-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="95438-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="95438-110">Options</span></span>

| <span data-ttu-id="95438-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="95438-111">Option</span></span> | <span data-ttu-id="95438-112">Описание</span><span class="sxs-lookup"><span data-stu-id="95438-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="95438-113">Все</span><span class="sxs-lookup"><span data-stu-id="95438-113">All</span></span> | <span data-ttu-id="95438-114">Печать подробная справка для всех доступных команд; игнорируется, если задан той или иной команды.</span><span class="sxs-lookup"><span data-stu-id="95438-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="95438-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="95438-115">ConfigFile</span></span> | <span data-ttu-id="95438-116">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="95438-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="95438-117">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="95438-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="95438-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="95438-118">ForceEnglishOutput</span></span> | <span data-ttu-id="95438-119">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="95438-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="95438-120">Справка</span><span class="sxs-lookup"><span data-stu-id="95438-120">Help</span></span> | <span data-ttu-id="95438-121">Отображает справку для саму команду справки.</span><span class="sxs-lookup"><span data-stu-id="95438-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="95438-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="95438-122">Markdown</span></span> | <span data-ttu-id="95438-123">Печать подробной справки в формате markdown при использовании с `-All`.</span><span class="sxs-lookup"><span data-stu-id="95438-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="95438-124">В противном случае значение не обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="95438-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="95438-125">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="95438-125">NonInteractive</span></span> | <span data-ttu-id="95438-126">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="95438-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="95438-127">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="95438-127">Verbosity</span></span> | <span data-ttu-id="95438-128">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="95438-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="95438-129">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="95438-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="95438-130">Примеры</span><span class="sxs-lookup"><span data-stu-id="95438-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
