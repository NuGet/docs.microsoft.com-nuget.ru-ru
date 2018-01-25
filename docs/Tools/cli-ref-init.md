---
title: "Команду NuGet CLI init | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Справочник по команде init nuget.exe"
keywords: "Справочник по init NuGet, команда init"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6d7710cd024e2c2956fb73aa767c3be55b9fb0f9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="f5171-104">команда init (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f5171-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="f5171-105">**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="f5171-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="f5171-106">Копирует все пакеты из папки на жестком диске в папку назначения с помощью иерархическом виде, как описано для [добавьте команду](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="f5171-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="f5171-107">То есть с использованием `init` эквивалентно использованию `add` на каждый пакет в папке.</span><span class="sxs-lookup"><span data-stu-id="f5171-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="f5171-108">Как и в `add`, то следует локальную папку или UNC-путь; HTTP пакета репозиториев, таких как nuget.org или закрытый серверы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="f5171-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="f5171-109">Использование</span><span class="sxs-lookup"><span data-stu-id="f5171-109">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="f5171-110">где `<source>` — папка, содержащая пакеты и `<destination>` локальная папка или путь UNC, в который копируются пакеты.</span><span class="sxs-lookup"><span data-stu-id="f5171-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="f5171-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="f5171-111">Options</span></span>

| <span data-ttu-id="f5171-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="f5171-112">Option</span></span> | <span data-ttu-id="f5171-113">Описание:</span><span class="sxs-lookup"><span data-stu-id="f5171-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f5171-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f5171-114">ConfigFile</span></span> | <span data-ttu-id="f5171-115">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="f5171-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f5171-116">Если не указан, *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="f5171-116">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="f5171-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f5171-117">ForceEnglishOutput</span></span> | <span data-ttu-id="f5171-118">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="f5171-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f5171-119">Expand</span><span class="sxs-lookup"><span data-stu-id="f5171-119">Expand</span></span> | <span data-ttu-id="f5171-120">Добавляет все файлы в каждом пакете, который добавляется к источнику пакета; то же, что `-Expand` с `add` команды.</span><span class="sxs-lookup"><span data-stu-id="f5171-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="f5171-121">Справка</span><span class="sxs-lookup"><span data-stu-id="f5171-121">Help</span></span> | <span data-ttu-id="f5171-122">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="f5171-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="f5171-123">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="f5171-123">NonInteractive</span></span> | <span data-ttu-id="f5171-124">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="f5171-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f5171-125">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="f5171-125">Verbosity</span></span> | <span data-ttu-id="f5171-126">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="f5171-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f5171-127">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f5171-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f5171-128">Примеры</span><span class="sxs-lookup"><span data-stu-id="f5171-128">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
