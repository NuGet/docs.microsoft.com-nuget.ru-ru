---
title: Команда справки интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe Help
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327801"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="b09a5-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="b09a5-103">help or ?</span></span> <span data-ttu-id="b09a5-104">Команда (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b09a5-104">command (NuGet CLI)</span></span>

<span data-ttu-id="b09a5-105">**Применимо к:** &bullet; все **Поддерживаемые версии**: все</span><span class="sxs-lookup"><span data-stu-id="b09a5-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="b09a5-106">Отображает общие справочные сведения и справочные сведения о конкретных командах.</span><span class="sxs-lookup"><span data-stu-id="b09a5-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="b09a5-107">Использование</span><span class="sxs-lookup"><span data-stu-id="b09a5-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="b09a5-108">WHERE [команда] определяет конкретную команду, для которой отображается справка.</span><span class="sxs-lookup"><span data-stu-id="b09a5-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="b09a5-109">С помощью некоторых команд можно учитывать, чтобы сначала указать *справку* , как `nuget help install`в, так как в NuGet.org есть пакет с именем "Help". Если вы выдаете `nuget install help`команду, вы не получите справку по команде install, но вместо этого установите пакет с именем Help.</span><span class="sxs-lookup"><span data-stu-id="b09a5-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="b09a5-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="b09a5-110">Options</span></span>

| <span data-ttu-id="b09a5-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="b09a5-111">Option</span></span> | <span data-ttu-id="b09a5-112">Описание</span><span class="sxs-lookup"><span data-stu-id="b09a5-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b09a5-113">Все</span><span class="sxs-lookup"><span data-stu-id="b09a5-113">All</span></span> | <span data-ttu-id="b09a5-114">Печать подробной справки по всем доступным командам; пропускается, если указана определенная команда.</span><span class="sxs-lookup"><span data-stu-id="b09a5-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="b09a5-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b09a5-115">ConfigFile</span></span> | <span data-ttu-id="b09a5-116">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="b09a5-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b09a5-117">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="b09a5-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b09a5-118">форцеенглишаутпут</span><span class="sxs-lookup"><span data-stu-id="b09a5-118">ForceEnglishOutput</span></span> | <span data-ttu-id="b09a5-119">*(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="b09a5-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b09a5-120">Help</span><span class="sxs-lookup"><span data-stu-id="b09a5-120">Help</span></span> | <span data-ttu-id="b09a5-121">Отображает справочную информацию о самой команде справки.</span><span class="sxs-lookup"><span data-stu-id="b09a5-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="b09a5-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="b09a5-122">Markdown</span></span> | <span data-ttu-id="b09a5-123">Печать подробной справки в формате Markdown при использовании `-All`с.</span><span class="sxs-lookup"><span data-stu-id="b09a5-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="b09a5-124">В противном случае значение игнорируется.</span><span class="sxs-lookup"><span data-stu-id="b09a5-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="b09a5-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b09a5-125">NonInteractive</span></span> | <span data-ttu-id="b09a5-126">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="b09a5-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b09a5-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="b09a5-127">Verbosity</span></span> | <span data-ttu-id="b09a5-128">Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*.</span><span class="sxs-lookup"><span data-stu-id="b09a5-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b09a5-129">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b09a5-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b09a5-130">Примеры</span><span class="sxs-lookup"><span data-stu-id="b09a5-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
