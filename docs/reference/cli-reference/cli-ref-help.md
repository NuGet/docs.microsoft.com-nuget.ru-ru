---
title: Команда справки интерфейса командной строки NuGet
description: Справочник по команде nuget.exe Help
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 12776b7c16aeef223a0b682ee2468edec8ea3295
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623114"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="d56ff-103">help или ?</span><span class="sxs-lookup"><span data-stu-id="d56ff-103">help or ?</span></span> <span data-ttu-id="d56ff-104">команда (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="d56ff-104">command (NuGet CLI)</span></span>

<span data-ttu-id="d56ff-105">**Применимо к:** все &bullet; **Поддерживаемые версии**: все</span><span class="sxs-lookup"><span data-stu-id="d56ff-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="d56ff-106">Отображает общие справочные сведения и справочные сведения о конкретных командах.</span><span class="sxs-lookup"><span data-stu-id="d56ff-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="d56ff-107">Использование</span><span class="sxs-lookup"><span data-stu-id="d56ff-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="d56ff-108">WHERE [команда] определяет конкретную команду, для которой отображается справка.</span><span class="sxs-lookup"><span data-stu-id="d56ff-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="d56ff-109">С помощью некоторых команд можно учитывать, чтобы сначала указать *справку* , как в `nuget help install` , так как в NuGet.org есть пакет с именем "Help". Если вы выдаете команду `nuget install help` , вы не получите справку по команде install, но вместо этого установите пакет с именем Help.</span><span class="sxs-lookup"><span data-stu-id="d56ff-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="d56ff-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="d56ff-110">Options</span></span>

- **`-All`**

  <span data-ttu-id="d56ff-111">Печать подробной справки по всем доступным командам; пропускается, если указана определенная команда.</span><span class="sxs-lookup"><span data-stu-id="d56ff-111">Print detailed help for all available commands; ignored if a specific command is given.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="d56ff-112">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="d56ff-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d56ff-113">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="d56ff-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="d56ff-114">*(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="d56ff-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="d56ff-115">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="d56ff-115">Displays help information for the command.</span></span>

- **`-Markdown`**

  <span data-ttu-id="d56ff-116">Печать подробной справки в формате Markdown при использовании с `-All` .</span><span class="sxs-lookup"><span data-stu-id="d56ff-116">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="d56ff-117">В противном случае значение игнорируется.</span><span class="sxs-lookup"><span data-stu-id="d56ff-117">Ignored otherwise.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="d56ff-118">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="d56ff-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="d56ff-119">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="d56ff-119">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="d56ff-120">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d56ff-120">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d56ff-121">Примеры</span><span class="sxs-lookup"><span data-stu-id="d56ff-121">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
