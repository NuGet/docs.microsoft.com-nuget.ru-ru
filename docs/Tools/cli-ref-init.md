---
title: Команду NuGet CLI init | Документы Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Справочник по команде init nuget.exe
keywords: Справочник по init NuGet, команда init
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 01a3553622020b5868e33ece09cd7555cb712fd3
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="f23b5-104">команда init (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f23b5-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="f23b5-105">**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="f23b5-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="f23b5-106">Копирует все пакеты из папки на жестком диске в папку назначения с помощью иерархическом виде, как описано для [добавьте команду](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="f23b5-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="f23b5-107">То есть с использованием `init` эквивалентно использованию `add` на каждый пакет в папке.</span><span class="sxs-lookup"><span data-stu-id="f23b5-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="f23b5-108">Как и в `add`, то следует локальную папку или UNC-путь; HTTP пакета репозиториев, таких как nuget.org или закрытый серверы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="f23b5-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="f23b5-109">Использование</span><span class="sxs-lookup"><span data-stu-id="f23b5-109">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="f23b5-110">где `<source>` — папка, содержащая пакеты и `<destination>` локальная папка или путь UNC, в который копируются пакеты.</span><span class="sxs-lookup"><span data-stu-id="f23b5-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="f23b5-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="f23b5-111">Options</span></span>

| <span data-ttu-id="f23b5-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="f23b5-112">Option</span></span> | <span data-ttu-id="f23b5-113">Описание</span><span class="sxs-lookup"><span data-stu-id="f23b5-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f23b5-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f23b5-114">ConfigFile</span></span> | <span data-ttu-id="f23b5-115">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="f23b5-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f23b5-116">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="f23b5-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f23b5-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f23b5-117">ForceEnglishOutput</span></span> | <span data-ttu-id="f23b5-118">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="f23b5-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f23b5-119">Развернуть</span><span class="sxs-lookup"><span data-stu-id="f23b5-119">Expand</span></span> | <span data-ttu-id="f23b5-120">Добавляет все файлы в каждом пакете, который добавляется к источнику пакета; то же, что `-Expand` с `add` команды.</span><span class="sxs-lookup"><span data-stu-id="f23b5-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="f23b5-121">Справка</span><span class="sxs-lookup"><span data-stu-id="f23b5-121">Help</span></span> | <span data-ttu-id="f23b5-122">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="f23b5-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="f23b5-123">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="f23b5-123">NonInteractive</span></span> | <span data-ttu-id="f23b5-124">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="f23b5-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f23b5-125">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="f23b5-125">Verbosity</span></span> | <span data-ttu-id="f23b5-126">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="f23b5-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f23b5-127">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f23b5-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f23b5-128">Примеры</span><span class="sxs-lookup"><span data-stu-id="f23b5-128">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
