---
title: Команда NuGet CLI Locals
description: Справочник по команде nuget.exe Locals
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: cdc2b760021ffc4a9e02edacb45beac01cc99bf1
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623062"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="81191-103">Команда Locals (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="81191-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="81191-104">Область **применения:** &bullet; **Поддерживаемые версии** потребления пакетов: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="81191-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="81191-105">Очищает или перечисляет локальные ресурсы NuGet, такие как *HTTP-Cache*, папка *Global-Packages* и временная папка.</span><span class="sxs-lookup"><span data-stu-id="81191-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="81191-106">`locals`Команду также можно использовать для вывода списка этих расположений.</span><span class="sxs-lookup"><span data-stu-id="81191-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="81191-107">Дополнительные сведения см. [в разделе Управление глобальными пакетами и папками кэша](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="81191-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="81191-108">Использование</span><span class="sxs-lookup"><span data-stu-id="81191-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="81191-109">где `<folder>` — один из `all` , `http-cache` , `packages-cache` *(3,5 и более ранних версий)*, `global-packages` , `temp` *(3.4 +)* и `plugins-cache` *(4.8 +)*.</span><span class="sxs-lookup"><span data-stu-id="81191-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="81191-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="81191-110">Options</span></span>

- **`-Clear`**

  <span data-ttu-id="81191-111">Очищает указанную папку.</span><span class="sxs-lookup"><span data-stu-id="81191-111">Clears the specified folder.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="81191-112">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="81191-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="81191-113">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="81191-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="81191-114">*(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="81191-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="81191-115">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="81191-115">Displays help information for the command.</span></span>

- **`-List`**

  <span data-ttu-id="81191-116">Отображает расположение указанной папки или расположения всех папок при использовании со *всеми*.</span><span class="sxs-lookup"><span data-stu-id="81191-116">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="81191-117">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="81191-117">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="81191-118">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="81191-118">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="81191-119">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="81191-119">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="81191-120">Примеры</span><span class="sxs-lookup"><span data-stu-id="81191-120">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="81191-121">Дополнительные примеры см. [в разделе Управление глобальными пакетами и папками кэша](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="81191-121">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
