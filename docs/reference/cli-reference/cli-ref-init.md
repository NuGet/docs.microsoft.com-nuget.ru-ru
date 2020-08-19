---
title: Команда NuGet CLI init
description: Справочник по команде nuget.exe init
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3b830d678a473c917b70bd46900bdb0206d3652e
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623088"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="1de1e-103">команда init (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="1de1e-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="1de1e-104">Область **применения:** &bullet; **Поддерживаемые версии** для создания пакетов: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="1de1e-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="1de1e-105">Копирует все пакеты из неструктурированной папки в конечную папку с помощью иерархического макета, как описано в [команде Add](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="1de1e-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="1de1e-106">То есть использование `init` эквивалентно использованию `add` команды для каждого пакета в папке.</span><span class="sxs-lookup"><span data-stu-id="1de1e-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="1de1e-107">Как и в `add` случае, назначение должно быть локальной папкой или UNC-путем. Репозитории пакетов HTTP, такие как nuget.org или частные серверы, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="1de1e-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="1de1e-108">Использование</span><span class="sxs-lookup"><span data-stu-id="1de1e-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="1de1e-109">где `<source>` — это папка, содержащая пакеты, а `<destination>` — Локальная папка или путь в формате UNC, в который копируются пакеты.</span><span class="sxs-lookup"><span data-stu-id="1de1e-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="1de1e-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="1de1e-110">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="1de1e-111">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="1de1e-111">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1de1e-112">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="1de1e-112">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="1de1e-113">Добавляет все файлы в каждом пакете, который добавляется в источник пакета; то же, что и `-Expand` `add` команда.</span><span class="sxs-lookup"><span data-stu-id="1de1e-113">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="1de1e-114">*(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="1de1e-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="1de1e-115">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="1de1e-115">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="1de1e-116">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="1de1e-116">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="1de1e-117">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="1de1e-117">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="1de1e-118">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1de1e-118">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1de1e-119">Примеры</span><span class="sxs-lookup"><span data-stu-id="1de1e-119">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
