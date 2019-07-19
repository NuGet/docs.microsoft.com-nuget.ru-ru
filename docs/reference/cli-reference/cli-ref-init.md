---
title: Команда NuGet CLI init
description: Справочник по команде NuGet. exe init
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327781"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="2aac2-103">команда init (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="2aac2-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="2aac2-104">Область **применения:** &bullet; **Поддерживаемые версии** для создания пакетов: 3.3+</span><span class="sxs-lookup"><span data-stu-id="2aac2-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="2aac2-105">Копирует все пакеты из неструктурированной папки в конечную папку с помощью иерархического макета, как описано в [команде Add](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="2aac2-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="2aac2-106">То есть использование `init` эквивалентно `add` использованию команды для каждого пакета в папке.</span><span class="sxs-lookup"><span data-stu-id="2aac2-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="2aac2-107">Как и в случае, назначение должно быть локальной папкой или UNC-путем. `add` Репозитории пакетов HTTP, такие как nuget.org или частные серверы, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="2aac2-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="2aac2-108">Использование</span><span class="sxs-lookup"><span data-stu-id="2aac2-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="2aac2-109">где `<source>` — это папка, содержащая пакеты `<destination>` , а — локальная папка или путь в формате UNC, в который копируются пакеты.</span><span class="sxs-lookup"><span data-stu-id="2aac2-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="2aac2-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="2aac2-110">Options</span></span>

| <span data-ttu-id="2aac2-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="2aac2-111">Option</span></span> | <span data-ttu-id="2aac2-112">Описание</span><span class="sxs-lookup"><span data-stu-id="2aac2-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2aac2-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2aac2-113">ConfigFile</span></span> | <span data-ttu-id="2aac2-114">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="2aac2-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2aac2-115">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="2aac2-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2aac2-116">форцеенглишаутпут</span><span class="sxs-lookup"><span data-stu-id="2aac2-116">ForceEnglishOutput</span></span> | <span data-ttu-id="2aac2-117">*(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="2aac2-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2aac2-118">Expand</span><span class="sxs-lookup"><span data-stu-id="2aac2-118">Expand</span></span> | <span data-ttu-id="2aac2-119">Добавляет все файлы в каждом пакете, который добавляется в источник пакета; то же `-Expand` , что `add` и команда.</span><span class="sxs-lookup"><span data-stu-id="2aac2-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="2aac2-120">Help</span><span class="sxs-lookup"><span data-stu-id="2aac2-120">Help</span></span> | <span data-ttu-id="2aac2-121">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="2aac2-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="2aac2-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2aac2-122">NonInteractive</span></span> | <span data-ttu-id="2aac2-123">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="2aac2-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2aac2-124">Verbosity</span><span class="sxs-lookup"><span data-stu-id="2aac2-124">Verbosity</span></span> | <span data-ttu-id="2aac2-125">Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*.</span><span class="sxs-lookup"><span data-stu-id="2aac2-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2aac2-126">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2aac2-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2aac2-127">Примеры</span><span class="sxs-lookup"><span data-stu-id="2aac2-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
