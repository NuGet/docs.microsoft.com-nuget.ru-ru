---
title: Команда help интерфейса командной строки NuGet
description: Справочник по команде help nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546567"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="898ac-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="898ac-103">help or ?</span></span> <span data-ttu-id="898ac-104">Команда (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="898ac-104">command (NuGet CLI)</span></span>

<span data-ttu-id="898ac-105">**Применяется к:** все &bullet; **поддерживаемые версии**: все</span><span class="sxs-lookup"><span data-stu-id="898ac-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="898ac-106">Отображаются общие справочные сведения и справочные сведения о конкретных команд.</span><span class="sxs-lookup"><span data-stu-id="898ac-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="898ac-107">Использование</span><span class="sxs-lookup"><span data-stu-id="898ac-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="898ac-108">где [команда] определяет определенной команды для отображения справки.</span><span class="sxs-lookup"><span data-stu-id="898ac-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="898ac-109">При этом часть команд, следует учитывать указать *помочь* первыми, как с `nuget help install`, так как имеется пакет с именем «Справка» на сайте nuget.org. Если вы предоставите команда `nuget install help`, не получить справку по команде install, а установит пакет с именем справки.</span><span class="sxs-lookup"><span data-stu-id="898ac-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="898ac-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="898ac-110">Options</span></span>

| <span data-ttu-id="898ac-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="898ac-111">Option</span></span> | <span data-ttu-id="898ac-112">Описание</span><span class="sxs-lookup"><span data-stu-id="898ac-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="898ac-113">Все</span><span class="sxs-lookup"><span data-stu-id="898ac-113">All</span></span> | <span data-ttu-id="898ac-114">Печать подробная справка для всех доступных команд; игнорируется, если предоставляется определенную команду.</span><span class="sxs-lookup"><span data-stu-id="898ac-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="898ac-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="898ac-115">ConfigFile</span></span> | <span data-ttu-id="898ac-116">Чтобы применить файл конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="898ac-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="898ac-117">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="898ac-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="898ac-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="898ac-118">ForceEnglishOutput</span></span> | <span data-ttu-id="898ac-119">*(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры.</span><span class="sxs-lookup"><span data-stu-id="898ac-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="898ac-120">Справка</span><span class="sxs-lookup"><span data-stu-id="898ac-120">Help</span></span> | <span data-ttu-id="898ac-121">Отображает справку по команде help сам.</span><span class="sxs-lookup"><span data-stu-id="898ac-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="898ac-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="898ac-122">Markdown</span></span> | <span data-ttu-id="898ac-123">Печать подробная справка в формате markdown, при использовании с `-All`.</span><span class="sxs-lookup"><span data-stu-id="898ac-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="898ac-124">В противном случае учитывается.</span><span class="sxs-lookup"><span data-stu-id="898ac-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="898ac-125">Неинтерактивная</span><span class="sxs-lookup"><span data-stu-id="898ac-125">NonInteractive</span></span> | <span data-ttu-id="898ac-126">Подавление для пользователя данные или подтверждения.</span><span class="sxs-lookup"><span data-stu-id="898ac-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="898ac-127">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="898ac-127">Verbosity</span></span> | <span data-ttu-id="898ac-128">Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="898ac-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="898ac-129">Также см. в разделе [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="898ac-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="898ac-130">Примеры</span><span class="sxs-lookup"><span data-stu-id="898ac-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
