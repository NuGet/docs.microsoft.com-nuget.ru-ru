---
title: Команда NuGet CLI Locals
description: Справочник по команде NuGet. exe Locals
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327811"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="2f6ed-103">Команда locals (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2f6ed-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="2f6ed-104">Область **применения:** &bullet; **Поддерживаемые версии** потребления пакетов: 3.3+</span><span class="sxs-lookup"><span data-stu-id="2f6ed-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="2f6ed-105">Очищает или перечисляет локальные ресурсы NuGet, такие как *HTTP-Cache*, папка *Global-Packages* и временная папка.</span><span class="sxs-lookup"><span data-stu-id="2f6ed-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="2f6ed-106">`locals` Команду также можно использовать для вывода списка этих расположений.</span><span class="sxs-lookup"><span data-stu-id="2f6ed-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="2f6ed-107">Дополнительные сведения см. [в разделе Управление глобальными пакетами и папками кэша](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="2f6ed-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="2f6ed-108">Использование</span><span class="sxs-lookup"><span data-stu-id="2f6ed-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="2f6ed-109">где `<folder>` — один из `all`, `http-cache` `global-packages` `temp` `plugins-cache` , `packages-cache` *(3,5 и более ранних версий)* ,, *(3.4 +)* и *(4.8 +)* .</span><span class="sxs-lookup"><span data-stu-id="2f6ed-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="2f6ed-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="2f6ed-110">Options</span></span>

| <span data-ttu-id="2f6ed-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="2f6ed-111">Option</span></span> | <span data-ttu-id="2f6ed-112">Описание</span><span class="sxs-lookup"><span data-stu-id="2f6ed-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2f6ed-113">Clear</span><span class="sxs-lookup"><span data-stu-id="2f6ed-113">Clear</span></span> | <span data-ttu-id="2f6ed-114">Очищает указанную папку.</span><span class="sxs-lookup"><span data-stu-id="2f6ed-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="2f6ed-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2f6ed-115">ConfigFile</span></span> | <span data-ttu-id="2f6ed-116">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="2f6ed-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2f6ed-117">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="2f6ed-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2f6ed-118">форцеенглишаутпут</span><span class="sxs-lookup"><span data-stu-id="2f6ed-118">ForceEnglishOutput</span></span> | <span data-ttu-id="2f6ed-119">*(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="2f6ed-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2f6ed-120">Help</span><span class="sxs-lookup"><span data-stu-id="2f6ed-120">Help</span></span> | <span data-ttu-id="2f6ed-121">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="2f6ed-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="2f6ed-122">Список</span><span class="sxs-lookup"><span data-stu-id="2f6ed-122">List</span></span> | <span data-ttu-id="2f6ed-123">Отображает расположение указанной папки или расположения всех папок при использовании со *всеми*.</span><span class="sxs-lookup"><span data-stu-id="2f6ed-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="2f6ed-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2f6ed-124">NonInteractive</span></span> | <span data-ttu-id="2f6ed-125">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="2f6ed-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2f6ed-126">Verbosity</span><span class="sxs-lookup"><span data-stu-id="2f6ed-126">Verbosity</span></span> | <span data-ttu-id="2f6ed-127">Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*.</span><span class="sxs-lookup"><span data-stu-id="2f6ed-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2f6ed-128">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2f6ed-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2f6ed-129">Примеры</span><span class="sxs-lookup"><span data-stu-id="2f6ed-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="2f6ed-130">Дополнительные примеры см. [в разделе Управление глобальными пакетами и папками кэша](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="2f6ed-130">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
