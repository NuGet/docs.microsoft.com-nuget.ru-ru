---
title: Команда NuGet CLI init
description: Справочник по команде nuget.exe init
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f37572624cea744ce60a9a2e58ad3cbe2696cb9e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780074"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="7df42-103">команда init (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="7df42-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="7df42-104">Область **применения:** &bullet; **Поддерживаемые версии** для создания пакетов: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="7df42-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="7df42-105">Копирует все пакеты из неструктурированной папки в конечную папку с помощью иерархического макета, как описано в [команде Add](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="7df42-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="7df42-106">То есть использование `init` эквивалентно использованию `add` команды для каждого пакета в папке.</span><span class="sxs-lookup"><span data-stu-id="7df42-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="7df42-107">Как и в `add` случае, назначение должно быть локальной папкой или UNC-путем. Репозитории пакетов HTTP, такие как nuget.org или частные серверы, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="7df42-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="7df42-108">Использование</span><span class="sxs-lookup"><span data-stu-id="7df42-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="7df42-109">где `<source>` — это папка, содержащая пакеты, а `<destination>` — Локальная папка или путь в формате UNC, в который копируются пакеты.</span><span class="sxs-lookup"><span data-stu-id="7df42-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="7df42-110">Варианты</span><span class="sxs-lookup"><span data-stu-id="7df42-110">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="7df42-111">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="7df42-111">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7df42-112">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="7df42-112">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="7df42-113">Добавляет все файлы в каждом пакете, который добавляется в источник пакета; то же, что и `-Expand` `add` команда.</span><span class="sxs-lookup"><span data-stu-id="7df42-113">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="7df42-114">*(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="7df42-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="7df42-115">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="7df42-115">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="7df42-116">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="7df42-116">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="7df42-117">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="7df42-117">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="7df42-118">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7df42-118">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7df42-119">Примеры</span><span class="sxs-lookup"><span data-stu-id="7df42-119">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
