---
title: Спецификации команду интерфейса командной строки NuGet
description: Справочник по командам спецификаций nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68b165751ab6794d2a01d7e466619b1ce4d7ed72
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546453"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="86c00-103">спецификации команда (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="86c00-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="86c00-104">**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="86c00-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="86c00-105">Создает `.nuspec` файла для нового пакета.</span><span class="sxs-lookup"><span data-stu-id="86c00-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="86c00-106">Если в той же папке, что файл проекта (`.csproj`, `.vbproj`, `.fsproj`), `spec` создает токенами `.nuspec` файл.</span><span class="sxs-lookup"><span data-stu-id="86c00-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="86c00-107">Дополнительные сведения см. в разделе [Создание пакета](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="86c00-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="86c00-108">Использование</span><span class="sxs-lookup"><span data-stu-id="86c00-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="86c00-109">где `<packageID>` — это дополнительный пакет идентификатор, чтобы сохранить в `.nuspec` файл.</span><span class="sxs-lookup"><span data-stu-id="86c00-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="86c00-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="86c00-110">Options</span></span>

| <span data-ttu-id="86c00-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="86c00-111">Option</span></span> | <span data-ttu-id="86c00-112">Описание</span><span class="sxs-lookup"><span data-stu-id="86c00-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="86c00-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="86c00-113">AssemblyPath</span></span> | <span data-ttu-id="86c00-114">Указывает путь к сборке, используемый для метаданных.</span><span class="sxs-lookup"><span data-stu-id="86c00-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="86c00-115">Force</span><span class="sxs-lookup"><span data-stu-id="86c00-115">Force</span></span> | <span data-ttu-id="86c00-116">Перезаписываются все существующие `.nuspec` файл.</span><span class="sxs-lookup"><span data-stu-id="86c00-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="86c00-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="86c00-117">ForceEnglishOutput</span></span> | <span data-ttu-id="86c00-118">*(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры.</span><span class="sxs-lookup"><span data-stu-id="86c00-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="86c00-119">Справка</span><span class="sxs-lookup"><span data-stu-id="86c00-119">Help</span></span> | <span data-ttu-id="86c00-120">Отображает справку для команды.</span><span class="sxs-lookup"><span data-stu-id="86c00-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="86c00-121">Неинтерактивная</span><span class="sxs-lookup"><span data-stu-id="86c00-121">NonInteractive</span></span> | <span data-ttu-id="86c00-122">Подавление для пользователя данные или подтверждения.</span><span class="sxs-lookup"><span data-stu-id="86c00-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="86c00-123">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="86c00-123">Verbosity</span></span> | <span data-ttu-id="86c00-124">Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="86c00-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="86c00-125">Также см. в разделе [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="86c00-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="86c00-126">Примеры</span><span class="sxs-lookup"><span data-stu-id="86c00-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
