---
title: "Спецификация команду NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Справочник по спецификации команду nuget.exe"
keywords: "ссылка характеристик NuGet, команда характеристик"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc7e772e737a0f74929d13e2b126f7796b6d0dc7
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="670ad-104">Команда характеристик (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="670ad-104">spec command (NuGet CLI)</span></span>

<span data-ttu-id="670ad-105">**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="670ad-105">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="670ad-106">Приводит к возникновению ошибки `.nuspec` файла для нового пакета.</span><span class="sxs-lookup"><span data-stu-id="670ad-106">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="670ad-107">Если выполняются в той же папке, что и файл проекта (`.csproj`, `.vbproj`, `.fsproj`), `spec` создает токенами `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="670ad-107">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="670ad-108">Дополнительные сведения см. в разделе [Создание пакета](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="670ad-108">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="670ad-109">Использование</span><span class="sxs-lookup"><span data-stu-id="670ad-109">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="670ad-110">где `<packageID>` — это дополнительный пакет идентификатор, для сохранения в `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="670ad-110">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="670ad-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="670ad-111">Options</span></span>

| <span data-ttu-id="670ad-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="670ad-112">Option</span></span> | <span data-ttu-id="670ad-113">Описание:</span><span class="sxs-lookup"><span data-stu-id="670ad-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="670ad-114">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="670ad-114">AssemblyPath</span></span> | <span data-ttu-id="670ad-115">Указывает путь к сборке для использования метаданных.</span><span class="sxs-lookup"><span data-stu-id="670ad-115">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="670ad-116">Force</span><span class="sxs-lookup"><span data-stu-id="670ad-116">Force</span></span> | <span data-ttu-id="670ad-117">Перезаписывает все существующие `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="670ad-117">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="670ad-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="670ad-118">ForceEnglishOutput</span></span> | <span data-ttu-id="670ad-119">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="670ad-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="670ad-120">Справка</span><span class="sxs-lookup"><span data-stu-id="670ad-120">Help</span></span> | <span data-ttu-id="670ad-121">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="670ad-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="670ad-122">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="670ad-122">NonInteractive</span></span> | <span data-ttu-id="670ad-123">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="670ad-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="670ad-124">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="670ad-124">Verbosity</span></span> | <span data-ttu-id="670ad-125">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="670ad-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="670ad-126">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="670ad-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="670ad-127">Примеры</span><span class="sxs-lookup"><span data-stu-id="670ad-127">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
