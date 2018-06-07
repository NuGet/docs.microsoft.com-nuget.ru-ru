---
title: Локальные переменные команду NuGet CLI
description: Ссылка для команды локальные nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 90e8c85e7a3e0e9520933e2ddd6dd84447475f2b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818205"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="b8d4a-103">Команда locals (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b8d4a-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="b8d4a-104">**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="b8d4a-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="b8d4a-105">Очищает или перечисляет локальные ресурсы NuGet, такие как *кэша http*, *глобального пакеты* папки и временные папки.</span><span class="sxs-lookup"><span data-stu-id="b8d4a-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="b8d4a-106">`locals` Команда также может использоваться для отображения списка из этих расположений.</span><span class="sxs-lookup"><span data-stu-id="b8d4a-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="b8d4a-107">Дополнительные сведения см. в разделе [управление глобального пакетами и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="b8d4a-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="b8d4a-108">Использование</span><span class="sxs-lookup"><span data-stu-id="b8d4a-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="b8d4a-109">где `<folder>` является одним из `all`, `http-cache`, `packages-cache` *(3.5 и более ранних)*, `global-packages`, и `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="b8d4a-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="b8d4a-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="b8d4a-110">Options</span></span>

| <span data-ttu-id="b8d4a-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="b8d4a-111">Option</span></span> | <span data-ttu-id="b8d4a-112">Описание:</span><span class="sxs-lookup"><span data-stu-id="b8d4a-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b8d4a-113">Clear</span><span class="sxs-lookup"><span data-stu-id="b8d4a-113">Clear</span></span> | <span data-ttu-id="b8d4a-114">Удаляет указанную папку.</span><span class="sxs-lookup"><span data-stu-id="b8d4a-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="b8d4a-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b8d4a-115">ConfigFile</span></span> | <span data-ttu-id="b8d4a-116">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="b8d4a-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b8d4a-117">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="b8d4a-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b8d4a-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b8d4a-118">ForceEnglishOutput</span></span> | <span data-ttu-id="b8d4a-119">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="b8d4a-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b8d4a-120">Справка</span><span class="sxs-lookup"><span data-stu-id="b8d4a-120">Help</span></span> | <span data-ttu-id="b8d4a-121">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="b8d4a-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="b8d4a-122">Список</span><span class="sxs-lookup"><span data-stu-id="b8d4a-122">List</span></span> | <span data-ttu-id="b8d4a-123">Выводит расположение указанная папка или расположение всех папок, при использовании с *все*.</span><span class="sxs-lookup"><span data-stu-id="b8d4a-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="b8d4a-124">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="b8d4a-124">NonInteractive</span></span> | <span data-ttu-id="b8d4a-125">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="b8d4a-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b8d4a-126">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="b8d4a-126">Verbosity</span></span> | <span data-ttu-id="b8d4a-127">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="b8d4a-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b8d4a-128">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b8d4a-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b8d4a-129">Примеры</span><span class="sxs-lookup"><span data-stu-id="b8d4a-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="b8d4a-130">Дополнительные примеры см. в разделе [управление глобального пакетами и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="b8d4a-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
