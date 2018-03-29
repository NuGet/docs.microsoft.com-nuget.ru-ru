---
title: Локальные переменные команду NuGet CLI | Документы Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Ссылка для команды локальные nuget.exe
keywords: Справочник по NuGet локальные переменные, локальные команды
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0122c79e55b12838bd123cf91bfcbc5dbbd2a65c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="3ed27-104">Команда локальные переменные (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3ed27-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="3ed27-105">**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="3ed27-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="3ed27-106">Очищает или перечисляет локальные ресурсы NuGet, такие как *кэша http*, *глобального пакеты* папки и временные папки.</span><span class="sxs-lookup"><span data-stu-id="3ed27-106">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="3ed27-107">`locals` Команда также может использоваться для отображения списка из этих расположений.</span><span class="sxs-lookup"><span data-stu-id="3ed27-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="3ed27-108">Дополнительные сведения см. в разделе [управление глобального пакетами и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="3ed27-108">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="3ed27-109">Использование</span><span class="sxs-lookup"><span data-stu-id="3ed27-109">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="3ed27-110">где `<folder>` является одним из `all`, `http-cache`, `packages-cache` *(3.5 и более ранних)*, `global-packages`, и `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="3ed27-110">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="3ed27-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="3ed27-111">Options</span></span>

| <span data-ttu-id="3ed27-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="3ed27-112">Option</span></span> | <span data-ttu-id="3ed27-113">Описание</span><span class="sxs-lookup"><span data-stu-id="3ed27-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3ed27-114">Clear</span><span class="sxs-lookup"><span data-stu-id="3ed27-114">Clear</span></span> | <span data-ttu-id="3ed27-115">Удаляет указанную папку.</span><span class="sxs-lookup"><span data-stu-id="3ed27-115">Clears the specified folder.</span></span> |
| <span data-ttu-id="3ed27-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3ed27-116">ConfigFile</span></span> | <span data-ttu-id="3ed27-117">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="3ed27-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3ed27-118">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="3ed27-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3ed27-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3ed27-119">ForceEnglishOutput</span></span> | <span data-ttu-id="3ed27-120">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="3ed27-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3ed27-121">Справка</span><span class="sxs-lookup"><span data-stu-id="3ed27-121">Help</span></span> | <span data-ttu-id="3ed27-122">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="3ed27-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="3ed27-123">Список</span><span class="sxs-lookup"><span data-stu-id="3ed27-123">List</span></span> | <span data-ttu-id="3ed27-124">Выводит расположение указанная папка или расположение всех папок, при использовании с *все*.</span><span class="sxs-lookup"><span data-stu-id="3ed27-124">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="3ed27-125">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="3ed27-125">NonInteractive</span></span> | <span data-ttu-id="3ed27-126">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="3ed27-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3ed27-127">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="3ed27-127">Verbosity</span></span> | <span data-ttu-id="3ed27-128">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="3ed27-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3ed27-129">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3ed27-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3ed27-130">Примеры</span><span class="sxs-lookup"><span data-stu-id="3ed27-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="3ed27-131">Дополнительные примеры см. в разделе [управление глобального пакетами и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="3ed27-131">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
