---
title: Команда справки интерфейса командной строки NuGet
description: Справочник по команде nuget.exe Help
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5d91638c4a6f167ea8a04e5dfa2905cb55084ddd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779352"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="a3997-103">help или ?</span><span class="sxs-lookup"><span data-stu-id="a3997-103">help or ?</span></span> <span data-ttu-id="a3997-104">команда (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="a3997-104">command (NuGet CLI)</span></span>

<span data-ttu-id="a3997-105">**Применимо к:** все &bullet; **Поддерживаемые версии**: все</span><span class="sxs-lookup"><span data-stu-id="a3997-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="a3997-106">Отображает общие справочные сведения и справочные сведения о конкретных командах.</span><span class="sxs-lookup"><span data-stu-id="a3997-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="a3997-107">Использование</span><span class="sxs-lookup"><span data-stu-id="a3997-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="a3997-108">WHERE [команда] определяет конкретную команду, для которой отображается справка.</span><span class="sxs-lookup"><span data-stu-id="a3997-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="a3997-109">С помощью некоторых команд можно учитывать, чтобы сначала указать *справку* , как в `nuget help install` , так как в NuGet.org есть пакет с именем "Help". Если вы выдаете команду `nuget install help` , вы не получите справку по команде install, но вместо этого установите пакет с именем Help.</span><span class="sxs-lookup"><span data-stu-id="a3997-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="a3997-110">Варианты</span><span class="sxs-lookup"><span data-stu-id="a3997-110">Options</span></span>

- **`-All`**

  <span data-ttu-id="a3997-111">Печать подробной справки по всем доступным командам; пропускается, если указана определенная команда.</span><span class="sxs-lookup"><span data-stu-id="a3997-111">Print detailed help for all available commands; ignored if a specific command is given.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="a3997-112">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="a3997-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a3997-113">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="a3997-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="a3997-114">*(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="a3997-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a3997-115">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="a3997-115">Displays help information for the command.</span></span>

- **`-Markdown`**

  <span data-ttu-id="a3997-116">Печать подробной справки в формате Markdown при использовании с `-All` .</span><span class="sxs-lookup"><span data-stu-id="a3997-116">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="a3997-117">В противном случае значение игнорируется.</span><span class="sxs-lookup"><span data-stu-id="a3997-117">Ignored otherwise.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a3997-118">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="a3997-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a3997-119">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="a3997-119">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="a3997-120">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a3997-120">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a3997-121">Примеры</span><span class="sxs-lookup"><span data-stu-id="a3997-121">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
