---
title: Команда locals для NuGet CLI
description: Справочник по командам nuget.exe "Локальные"
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 38d8b9366fb2749b77c987c950da3aa9e7f029fc
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794139"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="fa0f7-103">Команда locals (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fa0f7-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="fa0f7-104">**Применяется к:** упаковать потребления &bullet; **поддерживаемые версии:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="fa0f7-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="fa0f7-105">Очищает или перечисляет локальные ресурсы NuGet, такие как *http-cache*, *глобальных пакетов* папки и временной папки.</span><span class="sxs-lookup"><span data-stu-id="fa0f7-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="fa0f7-106">`locals` Команда также может использоваться для отображения списка из этих расположений.</span><span class="sxs-lookup"><span data-stu-id="fa0f7-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="fa0f7-107">Дополнительные сведения см. в разделе [управление папкой установки глобальных пакетов и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="fa0f7-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="fa0f7-108">Использование</span><span class="sxs-lookup"><span data-stu-id="fa0f7-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="fa0f7-109">где `<folder>` является одним из `all`, `http-cache`, `packages-cache` *(3.5 и более ранних версий)*, `global-packages`, `temp` *(версии 3.4 и более)*, и `plugins-cache` *(4.8 +)*.</span><span class="sxs-lookup"><span data-stu-id="fa0f7-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="fa0f7-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="fa0f7-110">Options</span></span>

| <span data-ttu-id="fa0f7-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="fa0f7-111">Option</span></span> | <span data-ttu-id="fa0f7-112">Описание:</span><span class="sxs-lookup"><span data-stu-id="fa0f7-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fa0f7-113">Clear</span><span class="sxs-lookup"><span data-stu-id="fa0f7-113">Clear</span></span> | <span data-ttu-id="fa0f7-114">Удаляет указанную папку.</span><span class="sxs-lookup"><span data-stu-id="fa0f7-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="fa0f7-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fa0f7-115">ConfigFile</span></span> | <span data-ttu-id="fa0f7-116">Чтобы применить файл конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="fa0f7-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fa0f7-117">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="fa0f7-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="fa0f7-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fa0f7-118">ForceEnglishOutput</span></span> | <span data-ttu-id="fa0f7-119">*(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры.</span><span class="sxs-lookup"><span data-stu-id="fa0f7-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fa0f7-120">Справка</span><span class="sxs-lookup"><span data-stu-id="fa0f7-120">Help</span></span> | <span data-ttu-id="fa0f7-121">Отображает справку для команды.</span><span class="sxs-lookup"><span data-stu-id="fa0f7-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="fa0f7-122">Список</span><span class="sxs-lookup"><span data-stu-id="fa0f7-122">List</span></span> | <span data-ttu-id="fa0f7-123">Вносит в список расположение указанная папка или расположение всех папок, при использовании с *все*.</span><span class="sxs-lookup"><span data-stu-id="fa0f7-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="fa0f7-124">Неинтерактивная</span><span class="sxs-lookup"><span data-stu-id="fa0f7-124">NonInteractive</span></span> | <span data-ttu-id="fa0f7-125">Подавление для пользователя данные или подтверждения.</span><span class="sxs-lookup"><span data-stu-id="fa0f7-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fa0f7-126">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="fa0f7-126">Verbosity</span></span> | <span data-ttu-id="fa0f7-127">Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="fa0f7-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="fa0f7-128">Также см. в разделе [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fa0f7-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fa0f7-129">Примеры</span><span class="sxs-lookup"><span data-stu-id="fa0f7-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="fa0f7-130">Дополнительные примеры см. в разделе [управление папкой установки глобальных пакетов и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="fa0f7-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
