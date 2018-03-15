---
title: "Команда help NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Справочник по командам справки nuget.exe"
keywords: "Справка NuGet, команда «Справка»"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 281c6ccc7c58d153280441430be063d9ee89955d
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="4265c-104">Справка или?</span><span class="sxs-lookup"><span data-stu-id="4265c-104">help or ?</span></span> <span data-ttu-id="4265c-105">команда (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4265c-105">command (NuGet CLI)</span></span>

<span data-ttu-id="4265c-106">**Применяется к:** все &bullet; **поддерживаемые версии**: все</span><span class="sxs-lookup"><span data-stu-id="4265c-106">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="4265c-107">Отображаются общие справочные сведения и справочные сведения о конкретных команд.</span><span class="sxs-lookup"><span data-stu-id="4265c-107">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="4265c-108">Использование</span><span class="sxs-lookup"><span data-stu-id="4265c-108">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="4265c-109">где [команда] определяет той или иной команды для отображения справки.</span><span class="sxs-lookup"><span data-stu-id="4265c-109">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="4265c-110">Для некоторых команд, следует учитывать для указания *справки* во-первых, как с `nuget help install`, так как пакет с именем «Справка» на nuget.org. Если вы предоставляете команде `nuget install help`, не сможете получить справку в команду установки, а установит пакет с именем справки.</span><span class="sxs-lookup"><span data-stu-id="4265c-110">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="4265c-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="4265c-111">Options</span></span>

| <span data-ttu-id="4265c-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="4265c-112">Option</span></span> | <span data-ttu-id="4265c-113">Описание:</span><span class="sxs-lookup"><span data-stu-id="4265c-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4265c-114">Все</span><span class="sxs-lookup"><span data-stu-id="4265c-114">All</span></span> | <span data-ttu-id="4265c-115">Печать подробная справка для всех доступных команд; игнорируется, если задан той или иной команды.</span><span class="sxs-lookup"><span data-stu-id="4265c-115">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="4265c-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="4265c-116">ConfigFile</span></span> | <span data-ttu-id="4265c-117">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="4265c-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4265c-118">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="4265c-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="4265c-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4265c-119">ForceEnglishOutput</span></span> | <span data-ttu-id="4265c-120">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="4265c-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4265c-121">Справка</span><span class="sxs-lookup"><span data-stu-id="4265c-121">Help</span></span> | <span data-ttu-id="4265c-122">Отображает справку для саму команду справки.</span><span class="sxs-lookup"><span data-stu-id="4265c-122">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="4265c-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="4265c-123">Markdown</span></span> | <span data-ttu-id="4265c-124">Печать подробной справки в формате markdown при использовании с `-All`.</span><span class="sxs-lookup"><span data-stu-id="4265c-124">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="4265c-125">В противном случае значение не обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="4265c-125">Ignored otherwise.</span></span> |
| <span data-ttu-id="4265c-126">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="4265c-126">NonInteractive</span></span> | <span data-ttu-id="4265c-127">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="4265c-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4265c-128">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="4265c-128">Verbosity</span></span> | <span data-ttu-id="4265c-129">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="4265c-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="4265c-130">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4265c-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4265c-131">Примеры</span><span class="sxs-lookup"><span data-stu-id="4265c-131">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
