---
title: Команда спецификации интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe Spec
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327571"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="ff0b3-103">Команда spec (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="ff0b3-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="ff0b3-104">Область **применения:** &bullet; **Поддерживаемые версии** для создания пакетов: все</span><span class="sxs-lookup"><span data-stu-id="ff0b3-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ff0b3-105">`.nuspec` Создает файл для нового пакета.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="ff0b3-106">При запуске в той же папке, что и файл проекта`.csproj`( `.vbproj`, `.fsproj`,) `spec` , создает `.nuspec` файл с маркерами.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="ff0b3-107">Дополнительные сведения см. [в разделе Создание пакета](../../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="ff0b3-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="ff0b3-108">Использование</span><span class="sxs-lookup"><span data-stu-id="ff0b3-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="ff0b3-109">где `<packageID>` — это необязательный идентификатор пакета для сохранения `.nuspec` в файле.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="ff0b3-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="ff0b3-110">Options</span></span>

| <span data-ttu-id="ff0b3-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="ff0b3-111">Option</span></span> | <span data-ttu-id="ff0b3-112">Описание</span><span class="sxs-lookup"><span data-stu-id="ff0b3-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ff0b3-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="ff0b3-113">AssemblyPath</span></span> | <span data-ttu-id="ff0b3-114">Указывает путь к сборке, используемой для метаданных.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="ff0b3-115">Перевести</span><span class="sxs-lookup"><span data-stu-id="ff0b3-115">Force</span></span> | <span data-ttu-id="ff0b3-116">Перезаписывает существующий `.nuspec` файл.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="ff0b3-117">форцеенглишаутпут</span><span class="sxs-lookup"><span data-stu-id="ff0b3-117">ForceEnglishOutput</span></span> | <span data-ttu-id="ff0b3-118">*(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ff0b3-119">Help</span><span class="sxs-lookup"><span data-stu-id="ff0b3-119">Help</span></span> | <span data-ttu-id="ff0b3-120">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="ff0b3-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ff0b3-121">NonInteractive</span></span> | <span data-ttu-id="ff0b3-122">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ff0b3-123">Verbosity</span><span class="sxs-lookup"><span data-stu-id="ff0b3-123">Verbosity</span></span> | <span data-ttu-id="ff0b3-124">Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ff0b3-125">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ff0b3-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ff0b3-126">Примеры</span><span class="sxs-lookup"><span data-stu-id="ff0b3-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
