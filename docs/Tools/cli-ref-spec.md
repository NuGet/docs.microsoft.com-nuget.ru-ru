---
title: "Спецификация команду NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: "Справочник по спецификации команду nuget.exe"
keywords: "ссылка характеристик NuGet, команда характеристик"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="ccc7e-104">Команда характеристик (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ccc7e-104">spec command (NuGet CLI)</span></span>

<span data-ttu-id="ccc7e-105">**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="ccc7e-105">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ccc7e-106">Приводит к возникновению ошибки `.nuspec` файла для нового пакета.</span><span class="sxs-lookup"><span data-stu-id="ccc7e-106">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="ccc7e-107">Если выполняются в той же папке, что и файл проекта (`.csproj`, `.vbproj`, `.fsproj`), `spec` создает токенами `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="ccc7e-107">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="ccc7e-108">Дополнительные сведения см. в разделе [Создание пакета](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="ccc7e-108">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="ccc7e-109">Использование</span><span class="sxs-lookup"><span data-stu-id="ccc7e-109">Usage</span></span>

```
nuget spec [<packageID>] [options]
```

<span data-ttu-id="ccc7e-110">где `<packageID>` — это дополнительный пакет идентификатор, для сохранения в `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="ccc7e-110">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="ccc7e-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="ccc7e-111">Options</span></span>

| <span data-ttu-id="ccc7e-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="ccc7e-112">Option</span></span> | <span data-ttu-id="ccc7e-113">Описание</span><span class="sxs-lookup"><span data-stu-id="ccc7e-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ccc7e-114">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="ccc7e-114">AssemblyPath</span></span> | <span data-ttu-id="ccc7e-115">Указывает путь к сборке для использования метаданных.</span><span class="sxs-lookup"><span data-stu-id="ccc7e-115">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="ccc7e-116">Force</span><span class="sxs-lookup"><span data-stu-id="ccc7e-116">Force</span></span> | <span data-ttu-id="ccc7e-117">Перезаписывает все существующие `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="ccc7e-117">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="ccc7e-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ccc7e-118">ForceEnglishOutput</span></span> | <span data-ttu-id="ccc7e-119">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="ccc7e-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ccc7e-120">Справка</span><span class="sxs-lookup"><span data-stu-id="ccc7e-120">Help</span></span> | <span data-ttu-id="ccc7e-121">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="ccc7e-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="ccc7e-122">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="ccc7e-122">NonInteractive</span></span> | <span data-ttu-id="ccc7e-123">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="ccc7e-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ccc7e-124">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="ccc7e-124">Verbosity</span></span> | <span data-ttu-id="ccc7e-125">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="ccc7e-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="ccc7e-126">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ccc7e-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ccc7e-127">Примеры</span><span class="sxs-lookup"><span data-stu-id="ccc7e-127">Examples</span></span>

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
