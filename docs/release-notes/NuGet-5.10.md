---
title: Заметки о выпуске NuGet 5,10
description: Заметки о выпуске NuGet 5,10, включая новые функции, исправления ошибок и DCR.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356503"
---
# <a name="nuget-510-release-notes"></a><span data-ttu-id="1c6b1-103">Заметки о выпуске NuGet 5,10</span><span class="sxs-lookup"><span data-stu-id="1c6b1-103">NuGet 5.10 Release Notes</span></span>

<span data-ttu-id="1c6b1-104">Средства распространения NuGet:</span><span class="sxs-lookup"><span data-stu-id="1c6b1-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="1c6b1-105">Версия NuGet</span><span class="sxs-lookup"><span data-stu-id="1c6b1-105">NuGet version</span></span> | <span data-ttu-id="1c6b1-106">Доступно в версии Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1c6b1-106">Available in Visual Studio version</span></span> | <span data-ttu-id="1c6b1-107">Доступно в пакетах SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="1c6b1-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="1c6b1-108">**5.10.0**</span><span class="sxs-lookup"><span data-stu-id="1c6b1-108">**5.10.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="1c6b1-109">Visual Studio 2019 версии 16,10</span><span class="sxs-lookup"><span data-stu-id="1c6b1-109">Visual Studio 2019 version 16.10</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="1c6b1-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="1c6b1-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |

<span data-ttu-id="1c6b1-111"><sup>1</sup> установлен с Visual Studio 2019 с рабочей нагрузкой .NET Core</span><span class="sxs-lookup"><span data-stu-id="1c6b1-111"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="1c6b1-112">Для Visual Studio 16,10, MSBuild 16,10 и .NET 5.0.300 + требуется NuGet.exe 5,10 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1c6b1-112">Visual Studio 16.10, MSBuild 16.10, and .NET 5.0.300+ requires NuGet.exe 5.10 or later.</span></span>

## <a name="summary-whats-new-in-510"></a><span data-ttu-id="1c6b1-113">Сводка: новые возможности в 5,10</span><span class="sxs-lookup"><span data-stu-id="1c6b1-113">Summary: What's New in 5.10</span></span>

* <span data-ttu-id="1c6b1-114">Подписывание: реализуйте команду DotNet Trusted-Signs- [#8053](https://github.com/NuGet/Home/issues/8053)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-114">Signing: implement dotnet trusted-signers command - [#8053](https://github.com/NuGet/Home/issues/8053)</span></span>

* <span data-ttu-id="1c6b1-115">Сделать проверку по умолчанию отключенной в Linux, но включена по умолчанию в Windows — [#10713](https://github.com/NuGet/Home/issues/10713)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-115">Make default validation disabled on Linux, but enabled by default on Windows - [#10713](https://github.com/NuGet/Home/issues/10713)</span></span>

* <span data-ttu-id="1c6b1-116">Добавление переменной ENV для проверки подписи пакета в .NET 5 + Linux/MAC- [#10742](https://github.com/NuGet/Home/issues/10742)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-116">Add an ENV Variable for Package Signing Verification on .NET 5+ Linux/MAC - [#10742](https://github.com/NuGet/Home/issues/10742)</span></span>

* <span data-ttu-id="1c6b1-117">Улучшение установки новой производительности пакета для крупных решений — [#10166](https://github.com/NuGet/Home/issues/10166)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-117">Improve install new package performance for large solutions - [#10166](https://github.com/NuGet/Home/issues/10166)</span></span>

* <span data-ttu-id="1c6b1-118">Добавьте тип проекта `nfproj` в список суппортедпрожектекстенсионс для интерфейса командной строки NuGet.</span><span class="sxs-lookup"><span data-stu-id="1c6b1-118">Add the project type `nfproj` to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="1c6b1-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="1c6b1-120">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="1c6b1-120">Issues fixed in this release</span></span>

* <span data-ttu-id="1c6b1-121">Подавлять <requireLicenseAcceptance> элемент при упаковке проекта [#5133](https://github.com/NuGet/Home/issues/5133)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-121">Suppress the <requireLicenseAcceptance> element when packing a project - [#5133](https://github.com/NuGet/Home/issues/5133)</span></span>

* <span data-ttu-id="1c6b1-122">[КПВМ] предупреждение о предварительной версии должно отображаться в DotNet CLI- [#10226](https://github.com/NuGet/Home/issues/10226)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-122">[CPVM] preview warning should be shown on dotnet cli - [#10226](https://github.com/NuGet/Home/issues/10226)</span></span>

* <span data-ttu-id="1c6b1-123">Обновите маркеры цвета фона и переднего плана ПМУИ на Коммондокументколорс- [#10608](https://github.com/NuGet/Home/issues/10608)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-123">Update the background and foreground color tokens of the PMUI to CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)</span></span>

* <span data-ttu-id="1c6b1-124">[Ошибка Bash] Ошибка "операция отменена пользователем" отображается в список ошибокном окне при быстром переключении между вкладками в пользовательском интерфейсе PM: [#10671](https://github.com/NuGet/Home/issues/10671)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-124">[Bug Bash] Error “operation canceled by user” show in Error List window when switching between tabs quickly in PM UI - [#10671](https://github.com/NuGet/Home/issues/10671)</span></span>

* <span data-ttu-id="1c6b1-125">Пользовательский интерфейс PM: улучшение производительности установки пакетов на уровне решения — [#10210](https://github.com/NuGet/Home/issues/10210)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-125">PM UI:  Improve package installation performance on the solution level - [#10210](https://github.com/NuGet/Home/issues/10210)</span></span>

* <span data-ttu-id="1c6b1-126">Замена службы Жетсервицеасинк везде в NuGet. Clients — [#3784](https://github.com/NuGet/Home/issues/3784)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-126">Replace GetService with GetServiceAsync everywhere in NuGet.Clients - [#3784](https://github.com/NuGet/Home/issues/3784)</span></span>

* <span data-ttu-id="1c6b1-127">NuGet.exe проблемы с производительностью пакета с `..` относительным путем [#5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-127">NuGet.exe pack performance problem with `..` relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>

* <span data-ttu-id="1c6b1-128">Производительность пакета NuGet снижается с увеличением уровней в исходных путях — [#5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-128">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>

* <span data-ttu-id="1c6b1-129">NuGet не выдает ошибку при упаковке nuspec с повторяющимися файлами.</span><span class="sxs-lookup"><span data-stu-id="1c6b1-129">NuGet doesn't error when packaging nuspec with duplicate files.</span></span><span data-ttu-id="1c6b1-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span></span>

* <span data-ttu-id="1c6b1-131">Пакет NuGet "указанное значение DateTimeOffset не может быть преобразовано в метку времени ZIP-файла" — [#7001](https://github.com/NuGet/Home/issues/7001)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-131">NuGet pack "The DateTimeOffset specified cannot be converted into a Zip file timestamp" - [#7001](https://github.com/NuGet/Home/issues/7001)</span></span>

* <span data-ttu-id="1c6b1-132">Метки времени файла упакованного пакета сдвигаются по часовому поясу — [#7395](https://github.com/NuGet/Home/issues/7395)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-132">Timestamps of file of packed package is shifted by the timezone - [#7395](https://github.com/NuGet/Home/issues/7395)</span></span>

* <span data-ttu-id="1c6b1-133">NU1004 должен содержать более практичные сведения — [#7696](https://github.com/NuGet/Home/issues/7696)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-133">NU1004 should contain more actionable information  - [#7696](https://github.com/NuGet/Home/issues/7696)</span></span>

* <span data-ttu-id="1c6b1-134">[Ошибка Bash] [Сбой теста] Пустой или неправильно сформированный файл блокировки не должен обновляться при запуске "dotnet restore--use-Lock-File--заблокированный режим"- [#8640](https://github.com/NuGet/Home/issues/8640)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-134">[Bug Bash][Test Failure] The empty/malformed lock file should not be updated when running ‘dotnet restore --use-lock-file --locked-mode’ - [#8640](https://github.com/NuGet/Home/issues/8640)</span></span>

* <span data-ttu-id="1c6b1-135">Нужетверсионранже позволяет логически синтаксически неправильные диапазоны для анализа. [#9145](https://github.com/NuGet/Home/issues/9145)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-135">NuGetVersionRange allows logically incorrect ranges to be parsed - [#9145](https://github.com/NuGet/Home/issues/9145)</span></span>

* <span data-ttu-id="1c6b1-136">В пользовательском интерфейсе PM не удается отобразить различимый цвет фона между выбранными и источниками пакетов с наведением. [#9538](https://github.com/NuGet/Home/issues/9538)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-136">PM UI can’t show distinguishable background color between selected and hovered package sources - [#9538](https://github.com/NuGet/Home/issues/9538)</span></span>

* <span data-ttu-id="1c6b1-137">Флажок выбора проектов для установки не читается средством чтения с экрана — [#9578](https://github.com/NuGet/Home/issues/9578)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-137">Checkbox for selecting projects to install to isn't being read by screen reader - [#9578](https://github.com/NuGet/Home/issues/9578)</span></span>

* <span data-ttu-id="1c6b1-138">Список версий панели сведений выбор по умолчанию должен быть установлен или Латестстабле на вкладках "установленные" и "обновления"- [#9887](https://github.com/NuGet/Home/issues/9887)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-138">Details Pane Versions Dropdown default selection should be Installed/LatestStable on Installed/Updates tabs - [#9887](https://github.com/NuGet/Home/issues/9887)</span></span>

* <span data-ttu-id="1c6b1-139">Удаление учетной записи обхода для некоторых пакетов SDK для .NET 5 таржетплатформмоникер ` ,Version= `  -  [#9913](https://github.com/NuGet/Home/issues/9913)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-139">Remove workaround account for some .NET 5 SDKs report TargetPlatformMoniker of ` ,Version= ` - [#9913](https://github.com/NuGet/Home/issues/9913)</span></span>

* <span data-ttu-id="1c6b1-140">Проверка NuGet в DotNet слишком тихий [#10316](https://github.com/NuGet/Home/issues/10316)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-140">dotnet nuget verify is too quiet - [#10316](https://github.com/NuGet/Home/issues/10316)</span></span>

* <span data-ttu-id="1c6b1-141">Версионранже не удается проанализировать диапазоны из одной цифры — [#10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-141">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>

* <span data-ttu-id="1c6b1-142">Диспетчер решений VS создает исключение null для во время отладки — [#10352](https://github.com/NuGet/Home/issues/10352)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-142">VS Solution manager throws null exception for during debugging - [#10352](https://github.com/NuGet/Home/issues/10352)</span></span>

* <span data-ttu-id="1c6b1-143">Перемещение сообщений об исключениях интерфейса командной строки в строковые файлы ресурсов — [#10392](https://github.com/NuGet/Home/issues/10392)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-143">Move CLI exception messages to String Resource files - [#10392](https://github.com/NuGet/Home/issues/10392)</span></span>

* <span data-ttu-id="1c6b1-144">Удаление неработающего кода (Табитембуттонаутоматионпир) — [#10435](https://github.com/NuGet/Home/issues/10435)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-144">Remove dead code (TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)</span></span>

* <span data-ttu-id="1c6b1-145">Контекстное меню обновления должно перейти к первому выбранному элементу — [#10498](https://github.com/NuGet/Home/issues/10498)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-145">Update context menu should scroll to first selected item - [#10498](https://github.com/NuGet/Home/issues/10498)</span></span>

* <span data-ttu-id="1c6b1-146">Сведения о ПМУИе решения перекрываются горизонтальной чертой [#10533](https://github.com/NuGet/Home/issues/10533)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-146">Solution PMUI Details has overlapping horizontal bar - [#10533](https://github.com/NuGet/Home/issues/10533)</span></span>

* <span data-ttu-id="1c6b1-147">Подписывание: сведения о первичной подписи не отображаются, когда истек срок действия сертификата и отметка времени без доверия — [#10535](https://github.com/NuGet/Home/issues/10535)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-147">Signing:  primary signature details not displayed when certificate expired and timestamp untrusted - [#10535](https://github.com/NuGet/Home/issues/10535)</span></span>

* <span data-ttu-id="1c6b1-148">Отсутствие включенных источников предотвращает отображение пользовательского интерфейса PM [#10541](https://github.com/NuGet/Home/issues/10541)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-148">Having no enabled sources prevents the PM UI from showing - [#10541](https://github.com/NuGet/Home/issues/10541)</span></span>

* <span data-ttu-id="1c6b1-149">Метаданные пакета (сведения, нерекомендуемый) иногда не извлекаются из nuget.org в Кодеспацес- [#10549](https://github.com/NuGet/Home/issues/10549)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-149">Package Metadata (details, deprecation) are sometimes not pulled from nuget.org in CodeSpaces - [#10549](https://github.com/NuGet/Home/issues/10549)</span></span>

* <span data-ttu-id="1c6b1-150">Инициализация ПМУИ завершается с исключением во время сеанса отладки — [#10559](https://github.com/NuGet/Home/issues/10559)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-150">PMUI initialization fails with exception during debug session - [#10559](https://github.com/NuGet/Home/issues/10559)</span></span>

* <span data-ttu-id="1c6b1-151">Восстановление NuGet приводит к сбою проверки целостности пакета в системе с обратным порядком байтов — [#10567](https://github.com/NuGet/Home/issues/10567)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-151">nuget restore results in a package integrity check failure on big endian system - [#10567](https://github.com/NuGet/Home/issues/10567)</span></span>

* <span data-ttu-id="1c6b1-152">Вместо Паккагинжексцептион- [#10595](https://github.com/NuGet/Home/issues/10595) создается исключение</span><span class="sxs-lookup"><span data-stu-id="1c6b1-152">FormatException is thrown instead of PackagingException - [#10595](https://github.com/NuGet/Home/issues/10595)</span></span>

* <span data-ttu-id="1c6b1-153">КПВМ — проблемы параллелизма в алгоритме прохода графа — [#10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-153">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>

* <span data-ttu-id="1c6b1-154">Добавление телеметрии версии для PowerShell для PMC — [#10609](https://github.com/NuGet/Home/issues/10609)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-154">Add PMC powershell version telemetry - [#10609](https://github.com/NuGet/Home/issues/10609)</span></span>

* <span data-ttu-id="1c6b1-155">Повышение производительности Нужетверсион сортировки — [#10611](https://github.com/NuGet/Home/issues/10611)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-155">Improve NuGetVersion sort performance - [#10611](https://github.com/NuGet/Home/issues/10611)</span></span>

* <span data-ttu-id="1c6b1-156">В добавлении доверенных подписывающих аргументов есть непоследовательные аргументы — [#10647](https://github.com/NuGet/Home/issues/10647)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-156">Trusted-signers Add has inconsistent arguments - [#10647](https://github.com/NuGet/Home/issues/10647)</span></span>

* <span data-ttu-id="1c6b1-157">Vs2019 v 16.9.0: переключение вкладок в диспетчере пакетов NuGet с "Updates" на "installed" не приводит к обновлению кадра.</span><span class="sxs-lookup"><span data-stu-id="1c6b1-157">Vs2019 v16.9.0: Switching tabs in NuGet Package Manager from "Updates" to "Installed" doesn't update the frame.</span></span><span data-ttu-id="1c6b1-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span></span>

* <span data-ttu-id="1c6b1-159">Удалите "v" из номера версии в ПМУИ- [#10677](https://github.com/NuGet/Home/issues/10677)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-159">Remove the "v" from the version number in PMUI - [#10677](https://github.com/NuGet/Home/issues/10677)</span></span>

* <span data-ttu-id="1c6b1-160">Инужетпрожектсервице. Жетинсталледпаккажесасинк вызывает исключение перед получением системы проекта CPS предварительного утверждения- [#10681](https://github.com/NuGet/Home/issues/10681)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-160">INuGetProjectService.GetInstalledPackagesAsync throws before receiving CPS project system nomination - [#10681](https://github.com/NuGet/Home/issues/10681)</span></span>

* <span data-ttu-id="1c6b1-161">Встроенные значки вызывают отказ в доступе из источника "Microsoft Visual Studio автономные пакеты" на вкладке "Обзор" — [#10687](https://github.com/NuGet/Home/issues/10687)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-161">Embedded Icons cause Access Denied from source "Microsoft Visual Studio Offline Packages" on Browse tab - [#10687](https://github.com/NuGet/Home/issues/10687)</span></span>

* <span data-ttu-id="1c6b1-162">Инужетпрожектсервице. Жетинсталледпаккажесасинк вызывает исключение, если Мсбуилдпрожектекстенсионспас не задано — [#10739](https://github.com/NuGet/Home/issues/10739)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-162">INuGetProjectService.GetInstalledPackagesAsync throws when MSBuildProjectExtensionsPath is not set - [#10739](https://github.com/NuGet/Home/issues/10739)</span></span>

* <span data-ttu-id="1c6b1-163">"команда DotNet NuGet Remove Source nuget.org" не работает при первом [#10745](https://github.com/NuGet/Home/issues/10745)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-163">"dotnet nuget remove source nuget.org" doesn't work the first time - [#10745](https://github.com/NuGet/Home/issues/10745)</span></span>

* <span data-ttu-id="1c6b1-164">NuGet блокирует поток ThreadPool в асинхронном методе, делая синхронный вызов потока пользовательского интерфейса [#10775](https://github.com/NuGet/Home/issues/10775)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-164">Nuget blocks a threadpool thread in an async method making a synchronous call to the UI thread - [#10775](https://github.com/NuGet/Home/issues/10775)</span></span>

* <span data-ttu-id="1c6b1-165">Сервис — параметры > — строка диспетчера пакетов NuGet > усечена — [#10779](https://github.com/NuGet/Home/issues/10779)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-165">Tools -> Options -> NuGet Package Manager string is truncated - [#10779](https://github.com/NuGet/Home/issues/10779)</span></span>

* <span data-ttu-id="1c6b1-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` является неиспользуемым кодом и повредит производительность — [#10790](https://github.com/NuGet/Home/issues/10790)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` is dead code and hurting performance - [#10790](https://github.com/NuGet/Home/issues/10790)</span></span>

* <span data-ttu-id="1c6b1-167">Использование внедренного значка в пакетах SDK для NuGet — [#10795](https://github.com/NuGet/Home/issues/10795)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-167">Use embedded icon in NuGet SDK packages - [#10795](https://github.com/NuGet/Home/issues/10795)</span></span>

* <span data-ttu-id="1c6b1-168">Обновление списка лицензий СПДКС — [#10806](https://github.com/NuGet/Home/issues/10806)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-168">Update the SPDX license list - [#10806](https://github.com/NuGet/Home/issues/10806)</span></span>

<span data-ttu-id="1c6b1-169">**[Список всех проблем, исправленных в этом выпуске — 5,10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span><span class="sxs-lookup"><span data-stu-id="1c6b1-169">**[List of all issues fixed in this release - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span></span>
  
<span data-ttu-id="1c6b1-170">**[Список фиксаций в этом выпуске — 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span><span class="sxs-lookup"><span data-stu-id="1c6b1-170">**[List of commits in this release - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span></span>
  
### <a name="community-contributions"></a><span data-ttu-id="1c6b1-171">Материалы сообщества</span><span class="sxs-lookup"><span data-stu-id="1c6b1-171">Community contributions</span></span>

<span data-ttu-id="1c6b1-172">Благодарим всех участников, которые помогли сделать эту версию NuGet более Awesome!</span><span class="sxs-lookup"><span data-stu-id="1c6b1-172">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="1c6b1-173">Куда</span><span class="sxs-lookup"><span data-stu-id="1c6b1-173">Who</span></span>|<span data-ttu-id="1c6b1-174">Вытягивание</span><span class="sxs-lookup"><span data-stu-id="1c6b1-174">PRs</span></span>|<span data-ttu-id="1c6b1-175">Проблемы</span><span class="sxs-lookup"><span data-stu-id="1c6b1-175">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="1c6b1-176">-Луи-z</span><span class="sxs-lookup"><span data-stu-id="1c6b1-176">louis-z</span></span>](https://github.com/louis-z) | [<span data-ttu-id="1c6b1-177">3991</span><span class="sxs-lookup"><span data-stu-id="1c6b1-177">3991</span></span>](https://github.com/NuGet/NuGet.Client/pull/3991) | <span data-ttu-id="1c6b1-178">Версионранже не удается проанализировать диапазоны из одной цифры — [#10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-178">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>
[<span data-ttu-id="1c6b1-179">омажид</span><span class="sxs-lookup"><span data-stu-id="1c6b1-179">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="1c6b1-180">3860</span><span class="sxs-lookup"><span data-stu-id="1c6b1-180">3860</span></span>](https://github.com/NuGet/NuGet.Client/pull/3860) | <span data-ttu-id="1c6b1-181">NuGet. build.sh клиента работает [#10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-181">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="1c6b1-182">Nirmal4G</span><span class="sxs-lookup"><span data-stu-id="1c6b1-182">Nirmal4G</span></span>](https://github.com/Nirmal4G) | [<span data-ttu-id="1c6b1-183">3623</span><span class="sxs-lookup"><span data-stu-id="1c6b1-183">3623</span></span>](https://github.com/NuGet/NuGet.Client/pull/3623) | <span data-ttu-id="1c6b1-184">NuGet. build.sh клиента работает [#10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-184">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="1c6b1-185">блаккгад</span><span class="sxs-lookup"><span data-stu-id="1c6b1-185">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="1c6b1-186">3953</span><span class="sxs-lookup"><span data-stu-id="1c6b1-186">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="1c6b1-187">Производительность пакета NuGet снижается с увеличением уровней в исходных путях — [#5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-187">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>
[<span data-ttu-id="1c6b1-188">блаккгад</span><span class="sxs-lookup"><span data-stu-id="1c6b1-188">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="1c6b1-189">3953</span><span class="sxs-lookup"><span data-stu-id="1c6b1-189">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="1c6b1-190">NuGet.exe проблем с производительностью пакета...</span><span class="sxs-lookup"><span data-stu-id="1c6b1-190">NuGet.exe pack performance problem with ..</span></span> <span data-ttu-id="1c6b1-191">относительный путь — [#5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-191">relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>
[<span data-ttu-id="1c6b1-192">Марцин — кристианк</span><span class="sxs-lookup"><span data-stu-id="1c6b1-192">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="1c6b1-193">3940</span><span class="sxs-lookup"><span data-stu-id="1c6b1-193">3940</span></span>](https://github.com/NuGet/NuGet.Client/pull/3940) | <span data-ttu-id="1c6b1-194">КПВМ — проблемы параллелизма в алгоритме прохода графа — [#10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-194">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>
[<span data-ttu-id="1c6b1-195">жосесимоес</span><span class="sxs-lookup"><span data-stu-id="1c6b1-195">josesimoes</span></span>](https://github.com/josesimoes) | [<span data-ttu-id="1c6b1-196">3943</span><span class="sxs-lookup"><span data-stu-id="1c6b1-196">3943</span></span>](https://github.com/NuGet/NuGet.Client/pull/3943) | <span data-ttu-id="1c6b1-197">Добавьте тип проекта нфпрож в список Суппортедпрожектекстенсионс для интерфейса командной строки NuGet.</span><span class="sxs-lookup"><span data-stu-id="1c6b1-197">Add the project type nfproj to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="1c6b1-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="1c6b1-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

## <a name="feedback-welcome"></a><span data-ttu-id="1c6b1-199">Добро пожаловать на отзыв</span><span class="sxs-lookup"><span data-stu-id="1c6b1-199">Feedback welcome</span></span>

<span data-ttu-id="1c6b1-200">Ваши отзывы очень важны для нас.</span><span class="sxs-lookup"><span data-stu-id="1c6b1-200">Your feedback is important to us.</span></span>  <span data-ttu-id="1c6b1-201">Если в этом выпуске возникли какие либо проблемы, ознакомьтесь с нашими [проблемами в GitHub](https://github.com/NuGet/Home/issues) и [сообществом разработчиков Visual Studio](https://developercommunity.visualstudio.com/) за существующими проблемами.</span><span class="sxs-lookup"><span data-stu-id="1c6b1-201">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="1c6b1-202">При возникновении новых проблем в NuGet сообщите о [проблемах GitHub](https://github.com/NuGet/Home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="1c6b1-202">For new issues within NuGet, please report a [GitHub Issue](https://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="1c6b1-203">Чтобы получить общие сведения о проблемах с NuGet, сообщите нам об этом с помощью параметра [сообщить о проблеме](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) в ИЗБРАННОЙ среде IDE в разделе **Справка > сообщить о проблеме**.</span><span class="sxs-lookup"><span data-stu-id="1c6b1-203">For general NuGet experience issues, let us know via the [Report a Problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>
