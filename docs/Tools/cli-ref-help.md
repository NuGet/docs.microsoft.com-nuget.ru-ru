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
ms.openlocfilehash: 97f72e1be0df6e97f8b06696b2b3861800e4ea08
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="59121-104">Справка или?</span><span class="sxs-lookup"><span data-stu-id="59121-104">help or ?</span></span> <span data-ttu-id="59121-105">команда (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="59121-105">command (NuGet CLI)</span></span>

<span data-ttu-id="59121-106">**Применяется к:** все &bullet; **поддерживаемые версии**: все</span><span class="sxs-lookup"><span data-stu-id="59121-106">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="59121-107">Отображаются общие справочные сведения и справочные сведения о конкретных команд.</span><span class="sxs-lookup"><span data-stu-id="59121-107">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="59121-108">Использование</span><span class="sxs-lookup"><span data-stu-id="59121-108">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="59121-109">где [команда] определяет той или иной команды для отображения справки.</span><span class="sxs-lookup"><span data-stu-id="59121-109">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="59121-110">Для некоторых команд, следует учитывать для указания *справки* во-первых, как с `nuget help install`, так как пакет с именем «Справка» на nuget.org. Если вы предоставляете команде `nuget install help`, вы не сможете получить справку в команду установки, но установит пакет с именем справки.</span><span class="sxs-lookup"><span data-stu-id="59121-110">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you'll not get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="59121-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="59121-111">Options</span></span>

| <span data-ttu-id="59121-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="59121-112">Option</span></span> | <span data-ttu-id="59121-113">Описание:</span><span class="sxs-lookup"><span data-stu-id="59121-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="59121-114">Все</span><span class="sxs-lookup"><span data-stu-id="59121-114">All</span></span> | <span data-ttu-id="59121-115">Печать подробная справка для всех доступных команд; игнорируется, если задан той или иной команды.</span><span class="sxs-lookup"><span data-stu-id="59121-115">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="59121-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="59121-116">ConfigFile</span></span> | <span data-ttu-id="59121-117">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="59121-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="59121-118">Если не указан, *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="59121-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="59121-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="59121-119">ForceEnglishOutput</span></span> | <span data-ttu-id="59121-120">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="59121-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="59121-121">Справка</span><span class="sxs-lookup"><span data-stu-id="59121-121">Help</span></span> | <span data-ttu-id="59121-122">Отображает справку для саму команду справки.</span><span class="sxs-lookup"><span data-stu-id="59121-122">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="59121-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="59121-123">Markdown</span></span> | <span data-ttu-id="59121-124">Печать подробной справки в формате markdown при использовании с `-All`.</span><span class="sxs-lookup"><span data-stu-id="59121-124">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="59121-125">В противном случае значение не обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="59121-125">Ignored otherwise.</span></span> |
| <span data-ttu-id="59121-126">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="59121-126">NonInteractive</span></span> | <span data-ttu-id="59121-127">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="59121-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="59121-128">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="59121-128">Verbosity</span></span> | <span data-ttu-id="59121-129">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="59121-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="59121-130">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="59121-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="59121-131">Примеры</span><span class="sxs-lookup"><span data-stu-id="59121-131">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
