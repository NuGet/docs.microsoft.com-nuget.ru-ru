---
title: Команда init NuGet CLI
description: Справочник по команде init nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f5e819d014637d1ebb0403d9d838f9362efb20f0
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="b03a4-103">команда init (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b03a4-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="b03a4-104">**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="b03a4-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="b03a4-105">Копирует все пакеты из папки на жестком диске в папку назначения с помощью иерархическом виде, как описано для [добавьте команду](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="b03a4-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="b03a4-106">То есть с использованием `init` эквивалентно использованию `add` на каждый пакет в папке.</span><span class="sxs-lookup"><span data-stu-id="b03a4-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="b03a4-107">Как и в `add`, то следует локальную папку или UNC-путь; HTTP пакета репозиториев, таких как nuget.org или закрытый серверы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="b03a4-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="b03a4-108">Использование</span><span class="sxs-lookup"><span data-stu-id="b03a4-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="b03a4-109">где `<source>` — папка, содержащая пакеты и `<destination>` локальная папка или путь UNC, в который копируются пакеты.</span><span class="sxs-lookup"><span data-stu-id="b03a4-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="b03a4-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="b03a4-110">Options</span></span>

| <span data-ttu-id="b03a4-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="b03a4-111">Option</span></span> | <span data-ttu-id="b03a4-112">Описание</span><span class="sxs-lookup"><span data-stu-id="b03a4-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b03a4-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b03a4-113">ConfigFile</span></span> | <span data-ttu-id="b03a4-114">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="b03a4-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b03a4-115">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="b03a4-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b03a4-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b03a4-116">ForceEnglishOutput</span></span> | <span data-ttu-id="b03a4-117">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="b03a4-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b03a4-118">Expand</span><span class="sxs-lookup"><span data-stu-id="b03a4-118">Expand</span></span> | <span data-ttu-id="b03a4-119">Добавляет все файлы в каждом пакете, который добавляется к источнику пакета; то же, что `-Expand` с `add` команды.</span><span class="sxs-lookup"><span data-stu-id="b03a4-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="b03a4-120">Справка</span><span class="sxs-lookup"><span data-stu-id="b03a4-120">Help</span></span> | <span data-ttu-id="b03a4-121">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="b03a4-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="b03a4-122">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="b03a4-122">NonInteractive</span></span> | <span data-ttu-id="b03a4-123">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="b03a4-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b03a4-124">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="b03a4-124">Verbosity</span></span> | <span data-ttu-id="b03a4-125">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="b03a4-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b03a4-126">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b03a4-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b03a4-127">Примеры</span><span class="sxs-lookup"><span data-stu-id="b03a4-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
