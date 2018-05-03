---
title: Спецификация команду NuGet CLI
description: Справочник по спецификации команду nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68d661030ce7bcff7d7a3a1c96c07e149ad4ffea
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="23f4e-103">Команда характеристик (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="23f4e-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="23f4e-104">**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="23f4e-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="23f4e-105">Приводит к возникновению ошибки `.nuspec` файла для нового пакета.</span><span class="sxs-lookup"><span data-stu-id="23f4e-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="23f4e-106">Если выполняются в той же папке, что и файл проекта (`.csproj`, `.vbproj`, `.fsproj`), `spec` создает токенами `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="23f4e-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="23f4e-107">Дополнительные сведения см. в разделе [Создание пакета](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="23f4e-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="23f4e-108">Использование</span><span class="sxs-lookup"><span data-stu-id="23f4e-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="23f4e-109">где `<packageID>` — это дополнительный пакет идентификатор, для сохранения в `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="23f4e-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="23f4e-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="23f4e-110">Options</span></span>

| <span data-ttu-id="23f4e-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="23f4e-111">Option</span></span> | <span data-ttu-id="23f4e-112">Описание</span><span class="sxs-lookup"><span data-stu-id="23f4e-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="23f4e-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="23f4e-113">AssemblyPath</span></span> | <span data-ttu-id="23f4e-114">Указывает путь к сборке для использования метаданных.</span><span class="sxs-lookup"><span data-stu-id="23f4e-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="23f4e-115">Force</span><span class="sxs-lookup"><span data-stu-id="23f4e-115">Force</span></span> | <span data-ttu-id="23f4e-116">Перезаписывает все существующие `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="23f4e-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="23f4e-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="23f4e-117">ForceEnglishOutput</span></span> | <span data-ttu-id="23f4e-118">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="23f4e-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="23f4e-119">Справка</span><span class="sxs-lookup"><span data-stu-id="23f4e-119">Help</span></span> | <span data-ttu-id="23f4e-120">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="23f4e-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="23f4e-121">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="23f4e-121">NonInteractive</span></span> | <span data-ttu-id="23f4e-122">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="23f4e-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="23f4e-123">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="23f4e-123">Verbosity</span></span> | <span data-ttu-id="23f4e-124">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="23f4e-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="23f4e-125">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="23f4e-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="23f4e-126">Примеры</span><span class="sxs-lookup"><span data-stu-id="23f4e-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
