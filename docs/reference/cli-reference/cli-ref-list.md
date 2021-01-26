---
title: Команда списка CLI NuGet
description: Справочник по команде nuget.exe List
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 55ccf0d86ad6df8001e7401d430ec29cd7a154c3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780051"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="80d28-103">Команда list (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="80d28-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="80d28-104">Область **применения:** использование пакетов, публикация &bullet; **поддерживаемых версий:** все</span><span class="sxs-lookup"><span data-stu-id="80d28-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="80d28-105">Отображает список пакетов из заданного источника.</span><span class="sxs-lookup"><span data-stu-id="80d28-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="80d28-106">Если источники не указаны, используются все источники, определенные в глобальном файле конфигурации `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` .</span><span class="sxs-lookup"><span data-stu-id="80d28-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="80d28-107">Если `NuGet.Config` не указывает источники, `list` использует канал по умолчанию (NuGet.org).</span><span class="sxs-lookup"><span data-stu-id="80d28-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="80d28-108">Использование</span><span class="sxs-lookup"><span data-stu-id="80d28-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="80d28-109">где необязательные условия поиска будут фильтровать отображаемый список.</span><span class="sxs-lookup"><span data-stu-id="80d28-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="80d28-110">[Условия поиска](../../consume-packages/finding-and-choosing-packages.md#search-syntax) применяются к именам пакетов, тегов и описаний пакетов так же, как и при их использовании в NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="80d28-110">[Search terms](../../consume-packages/finding-and-choosing-packages.md#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="80d28-111">Варианты</span><span class="sxs-lookup"><span data-stu-id="80d28-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="80d28-112">Вывод списка всех версий пакета.</span><span class="sxs-lookup"><span data-stu-id="80d28-112">List all versions of a package.</span></span> <span data-ttu-id="80d28-113">По умолчанию отображается только последняя версия пакета.</span><span class="sxs-lookup"><span data-stu-id="80d28-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="80d28-114">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="80d28-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="80d28-115">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="80d28-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="80d28-116">*(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="80d28-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="80d28-117">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="80d28-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="80d28-118">*(3.2 +)* Отображение пакетов, которые не были перечислены.</span><span class="sxs-lookup"><span data-stu-id="80d28-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="80d28-119">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="80d28-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="80d28-120">Включает в список предварительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="80d28-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="80d28-121">Источник пакета для поиска.</span><span class="sxs-lookup"><span data-stu-id="80d28-121">The package source to search.</span></span> <span data-ttu-id="80d28-122">Можно указать несколько источников с помощью `-Source` параметра несколько раз.</span><span class="sxs-lookup"><span data-stu-id="80d28-122">You can specify multiple sources by using the `-Source` option multiple times.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="80d28-123">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="80d28-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="80d28-124">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="80d28-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="80d28-125">Примеры</span><span class="sxs-lookup"><span data-stu-id="80d28-125">Examples</span></span>

<span data-ttu-id="80d28-126">Список всех пакетов из настроенных веб-каналов:</span><span class="sxs-lookup"><span data-stu-id="80d28-126">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="80d28-127">Перечисление пакетов, связанных с Azure, с подробным уровнем детализации:</span><span class="sxs-lookup"><span data-stu-id="80d28-127">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="80d28-128">Вывод списка всех версий пакетов, связанных с Azure, из настроенных веб-каналов:</span><span class="sxs-lookup"><span data-stu-id="80d28-128">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="80d28-129">Вывод списка всех версий пакетов, связанных с JSON, из указанного источника или веб-канала:</span><span class="sxs-lookup"><span data-stu-id="80d28-129">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="80d28-130">Список пакетов, связанных с JSON, из нескольких источников и веб-каналов:</span><span class="sxs-lookup"><span data-stu-id="80d28-130">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```
