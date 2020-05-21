---
title: Заметки о выпуске NuGet 5,6
description: Заметки о выпуске NuGet 5,6, включая новые функции, исправления ошибок и DCR.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727809"
---
# <a name="nuget-56-release-notes"></a><span data-ttu-id="7813a-103">Заметки о выпуске NuGet 5,6</span><span class="sxs-lookup"><span data-stu-id="7813a-103">NuGet 5.6 Release Notes</span></span>

<span data-ttu-id="7813a-104">Средства распространения NuGet:</span><span class="sxs-lookup"><span data-stu-id="7813a-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="7813a-105">Версия NuGet</span><span class="sxs-lookup"><span data-stu-id="7813a-105">NuGet version</span></span> | <span data-ttu-id="7813a-106">Доступно в версии Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7813a-106">Available in Visual Studio version</span></span>| <span data-ttu-id="7813a-107">Доступно в пакетах SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="7813a-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="7813a-108">**5.6.0**</span><span class="sxs-lookup"><span data-stu-id="7813a-108">**5.6.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="7813a-109">Visual Studio 2019 версии 16.6</span><span class="sxs-lookup"><span data-stu-id="7813a-109">Visual Studio 2019 version 16.6</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="7813a-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="7813a-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="7813a-111"><sup>1</sup> Устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core</span><span class="sxs-lookup"><span data-stu-id="7813a-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-56"></a><span data-ttu-id="7813a-112">Сводка: новые возможности в 5,6</span><span class="sxs-lookup"><span data-stu-id="7813a-112">Summary: What's New in 5.6</span></span>

* <span data-ttu-id="7813a-113">Поддержка предварительных пакетов с плавающими версиями.</span><span class="sxs-lookup"><span data-stu-id="7813a-113">Support prerelease packages with floating versions.</span></span> <span data-ttu-id="7813a-114">`Version="*-*"`, `Version="1.*-*"` и аналогичные данные с плавающей запятой до последних версий, включая предварительные версии, в пределах указанного диапазона — [#912](https://github.com/NuGet/Home/issues/912)</span><span class="sxs-lookup"><span data-stu-id="7813a-114">`Version="*-*"`, `Version="1.*-*"`, and similar float to latest versions, including prerelease versions, within specified range  - [#912](https://github.com/NuGet/Home/issues/912)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="7813a-115">Исправления в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="7813a-115">Issues fixed in this release</span></span>

<span data-ttu-id="7813a-116">**Появились**</span><span class="sxs-lookup"><span data-stu-id="7813a-116">**Bugs:**</span></span>

* <span data-ttu-id="7813a-117">`nuget push *.nupkg`завершается ошибкой, если снупкг не существует — [#8148](https://github.com/NuGet/Home/issues/8148)</span><span class="sxs-lookup"><span data-stu-id="7813a-117">`nuget push *.nupkg` fails when snupkg does not exist - [#8148](https://github.com/NuGet/Home/issues/8148)</span></span>

* <span data-ttu-id="7813a-118">И несколько других путей кода, не зависящие от языкового стандарта.</span><span class="sxs-lookup"><span data-stu-id="7813a-118">Pack, and several other code paths, fail dependent on locale.</span></span> <span data-ttu-id="7813a-119">Использование RegexOptions. CultureInvariant- [#8246](https://github.com/NuGet/Home/issues/8246)</span><span class="sxs-lookup"><span data-stu-id="7813a-119">Use RegexOptions.CultureInvariant - [#8246](https://github.com/NuGet/Home/issues/8246)</span></span>

* <span data-ttu-id="7813a-120">Производительность: спецификация разгрузки для выгруженных сценариев проекта не должна быть создана в предварительном восстановлении — [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="7813a-120">Perf: DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="7813a-121">Восстановление: повышение производительности с помощью кэширования схемы зависимости решений — [#9201](https://github.com/NuGet/Home/issues/9201)</span><span class="sxs-lookup"><span data-stu-id="7813a-121">Restore: Improve performance by caching solution dependency graph spec - [#9201](https://github.com/NuGet/Home/issues/9201)</span></span>

* <span data-ttu-id="7813a-122">Пользовательский интерфейс PM не работает для проектов стилей SDK после установки пакета с помощью консоли PM [#9203](https://github.com/NuGet/Home/issues/9203)</span><span class="sxs-lookup"><span data-stu-id="7813a-122">PM UI doesn't work for SDK style projects after installing a package with PM Console - [#9203](https://github.com/NuGet/Home/issues/9203)</span></span>

* <span data-ttu-id="7813a-123">Не удается отобразить внедренный значок в пользовательском интерфейсе PM с локальным веб-каналом пакетов — в зависимости от/VS \- [#9225](https://github.com/NuGet/Home/issues/9225)</span><span class="sxs-lookup"><span data-stu-id="7813a-123">Embedded icon can’t be shown in PM UI with local package feed - depending on / vs \ - [#9225](https://github.com/NuGet/Home/issues/9225)</span></span>

* <span data-ttu-id="7813a-124">Нужетверсион. Трипарсестрикт () должен возвращать значение false, если не удается выполнить синтаксический анализ — [#9255](https://github.com/NuGet/Home/issues/9255)</span><span class="sxs-lookup"><span data-stu-id="7813a-124">NuGetVersion.TryParseStrict() should return false if it fails to parse - [#9255](https://github.com/NuGet/Home/issues/9255)</span></span>

* <span data-ttu-id="7813a-125">`nuget.exe push`Справка для `-source` , должен предлагать использование имени источника, а не исходного URL-адреса — [#9265](https://github.com/NuGet/Home/issues/9265)</span><span class="sxs-lookup"><span data-stu-id="7813a-125">`nuget.exe push` help for `-source`, should suggest usage of source name, not source URL - [#9265](https://github.com/NuGet/Home/issues/9265)</span></span>

* <span data-ttu-id="7813a-126">`dotnet nuget add package SourceUri`создает неверное имя источника пакета по умолчанию — [#9277](https://github.com/NuGet/Home/issues/9277)</span><span class="sxs-lookup"><span data-stu-id="7813a-126">`dotnet nuget add package SourceUri`  creates bad default package source name - [#9277](https://github.com/NuGet/Home/issues/9277)</span></span>

* <span data-ttu-id="7813a-127">Средство чтения с экрана не объявляет о поиске... сообщение при переключении вкладок — [#9307](https://github.com/NuGet/Home/issues/9307)</span><span class="sxs-lookup"><span data-stu-id="7813a-127">Screen reader doesn't announce "Searching..." message when switching tabs - [#9307](https://github.com/NuGet/Home/issues/9307)</span></span>

* <span data-ttu-id="7813a-128">Специальные возможности: цвет прямоугольника с фокусом недоступен на вкладках пользовательского интерфейса в темной теме — [#9336](https://github.com/NuGet/Home/issues/9336)</span><span class="sxs-lookup"><span data-stu-id="7813a-128">Accessibility: Focus-rectangle color is not accessible PM UI tabs in dark theme - [#9336](https://github.com/NuGet/Home/issues/9336)</span></span>

* <span data-ttu-id="7813a-129">не удается восстановить NuGet. exe 5,5 с помощью MSBuild 14 или более [#9458](https://github.com/NuGet/Home/issues/9458)</span><span class="sxs-lookup"><span data-stu-id="7813a-129">nuget.exe 5.5 fails to restore with MSBuild 14 or below - [#9458](https://github.com/NuGet/Home/issues/9458)</span></span>

* <span data-ttu-id="7813a-130">Не регистрировать время миллисекунд в сообщениях о восстановлении — [#8977](https://github.com/NuGet/Home/issues/8977)</span><span class="sxs-lookup"><span data-stu-id="7813a-130">Don't log millisecond times in restore messages - [#8977](https://github.com/NuGet/Home/issues/8977)</span></span>

* <span data-ttu-id="7813a-131">Сделать Иаутпутконсоле асинхронным — [#9268](https://github.com/NuGet/Home/issues/9268)</span><span class="sxs-lookup"><span data-stu-id="7813a-131">Make IOutputConsole async - [#9268](https://github.com/NuGet/Home/issues/9268)</span></span>

* <span data-ttu-id="7813a-132">На некоторых языках и региональных параметрах, отличных от английского, отработка версий MSBuild работает плохо. [#9322](https://github.com/NuGet/Home/issues/9322)</span><span class="sxs-lookup"><span data-stu-id="7813a-132">MSBuild version picking works poorly on some non-english cultures - [#9322](https://github.com/NuGet/Home/issues/9322)</span></span>

* <span data-ttu-id="7813a-133">Отсутствует формат по умолчанию для `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)</span><span class="sxs-lookup"><span data-stu-id="7813a-133">Missing format default on `dotnet nuget list source` - [#9337](https://github.com/NuGet/Home/issues/9337)</span></span>

* <span data-ttu-id="7813a-134">Perf: Рестореоператионлогжер имеет ненужное сходство потоков — [#9288](https://github.com/NuGet/Home/issues/9288)</span><span class="sxs-lookup"><span data-stu-id="7813a-134">Perf: RestoreOperationLogger has unnecessary thread affinity - [#9288](https://github.com/NuGet/Home/issues/9288)</span></span>

* <span data-ttu-id="7813a-135">Автоматическое создание документов для `dotnet nuget` команд — [#9146](https://github.com/NuGet/Home/issues/9146)</span><span class="sxs-lookup"><span data-stu-id="7813a-135">Automated creation of docs for `dotnet nuget` commands - [#9146](https://github.com/NuGet/Home/issues/9146)</span></span>

* <span data-ttu-id="7813a-136">Уровень детализации по умолчанию не должен сообщать о восстановлении NOOP для каждого проекта [#8792](https://github.com/NuGet/Home/issues/8792)</span><span class="sxs-lookup"><span data-stu-id="7813a-136">Default verbosity should not report each project's noop restore - [#8792](https://github.com/NuGet/Home/issues/8792)</span></span>

* <span data-ttu-id="7813a-137">`-DependencyVersion`Параметр поддержки для `NuGet.exe update` , аналогично команде Install [#7694](https://github.com/NuGet/Home/issues/7694)</span><span class="sxs-lookup"><span data-stu-id="7813a-137">Support `-DependencyVersion` parameter for `NuGet.exe update`, similar to install command - [#7694](https://github.com/NuGet/Home/issues/7694)</span></span>


<span data-ttu-id="7813a-138">**DCR**</span><span class="sxs-lookup"><span data-stu-id="7813a-138">**DCRs:**</span></span>

* <span data-ttu-id="7813a-139">Добавление начальной поддержки для целевой платформы NET 5.0 — [#9584](https://github.com/NuGet/Home/issues/9584)</span><span class="sxs-lookup"><span data-stu-id="7813a-139">Add initial support for net5.0 target framework - [#9584](https://github.com/NuGet/Home/issues/9584)</span></span>

* <span data-ttu-id="7813a-140">Сортировка пакетов по ИДЕНТИФИКАТОРу на вкладке "обновления" пользовательского интерфейса PM — [#9278](https://github.com/NuGet/Home/issues/9278)</span><span class="sxs-lookup"><span data-stu-id="7813a-140">Sort packages by ID in the Updates tab of the PM UI - [#9278](https://github.com/NuGet/Home/issues/9278)</span></span>


<span data-ttu-id="7813a-141">**[Список всех проблем, исправленных в этом выпуске — 5,6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span><span class="sxs-lookup"><span data-stu-id="7813a-141">**[List of all issues fixed in this release - 5.6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span></span>
