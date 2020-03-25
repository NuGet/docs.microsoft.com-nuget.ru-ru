---
title: Заметки о выпуске NuGet 5,5
description: Заметки о выпуске NuGet 5,5, включая новые функции, исправления ошибок и DCR.
author: karann-msft
ms.author: karann
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0e8ab66c937058e84420bc3e3a5031cbc133aad7
ms.sourcegitcommit: 1a63a84da2719c8141823ac89a20bf507fd22b00
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/24/2020
ms.locfileid: "80148285"
---
# <a name="nuget-55-release-notes"></a><span data-ttu-id="bb6cd-103">Заметки о выпуске NuGet 5,5</span><span class="sxs-lookup"><span data-stu-id="bb6cd-103">NuGet 5.5 Release Notes</span></span>

<span data-ttu-id="bb6cd-104">Средства распространения NuGet:</span><span class="sxs-lookup"><span data-stu-id="bb6cd-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="bb6cd-105">Версия NuGet</span><span class="sxs-lookup"><span data-stu-id="bb6cd-105">NuGet version</span></span> | <span data-ttu-id="bb6cd-106">Доступно в версии Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bb6cd-106">Available in Visual Studio version</span></span>| <span data-ttu-id="bb6cd-107">Доступно в пакетах SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="bb6cd-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="bb6cd-108">**5.5.0**</span><span class="sxs-lookup"><span data-stu-id="bb6cd-108">**5.5.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="bb6cd-109">Visual Studio 2019 версии 16,5</span><span class="sxs-lookup"><span data-stu-id="bb6cd-109">Visual Studio 2019 version 16.5</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="bb6cd-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="bb6cd-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="bb6cd-111"><sup>1</sup> Устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core</span><span class="sxs-lookup"><span data-stu-id="bb6cd-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-55"></a><span data-ttu-id="bb6cd-112">Сводка: новые возможности в 5,5</span><span class="sxs-lookup"><span data-stu-id="bb6cd-112">Summary: What's New in 5.5</span></span>

* <span data-ttu-id="bb6cd-113">Улучшена поддержка специальных возможностей и средств чтения с экрана для пользовательского интерфейса диспетчера пакетов NuGet в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bb6cd-113">Improved accessibility and screen reader experience for the NuGet package manager UI in Visual Studio</span></span>
    * <span data-ttu-id="bb6cd-114">Проблемы специальных возможностей в средствах чтения с экрана, отсутствует Алттекст и доступное имя для установленного текстового поля и т. д., [#9059](https://github.com/NuGet/Home/issues/9059)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-114">Accessibility issues in Screen Reader experiences, missing altText and accessible name for Installed textbox, etc., - [#9059](https://github.com/NuGet/Home/issues/9059)</span></span>
    * <span data-ttu-id="bb6cd-115">Проблемы специальных возможностей в интерфейсе чтения с экрана в списке пакетов — [#9077](https://github.com/NuGet/Home/issues/9077)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-115">Accessibility issues in Screen Reader experiences in Packages List - [#9077](https://github.com/NuGet/Home/issues/9077)</span></span>
    * <span data-ttu-id="bb6cd-116">Проблемы специальных возможностей в средствах чтения с экрана, связанные с вкладками "Обзор", "установить", "Обновить" — [#9078](https://github.com/NuGet/Home/issues/9078)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-116">Accessibility issues in Screen Reader experiences related to "browse","install","update" Tabs - [#9078](https://github.com/NuGet/Home/issues/9078)</span></span>
    * <span data-ttu-id="bb6cd-117">Программа "Экранный диктор" не объявляет "пустое", "нет ДепенденЦиес", "нужет. org", метку ссылки MIT [#9157](https://github.com/NuGet/Home/issues/9157)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-117">Narrator does not announce "Blank","No Dependencies","nuget.org","MIT" link label [#9157](https://github.com/NuGet/Home/issues/9157)</span></span>

* <span data-ttu-id="bb6cd-118">Поддержка автономных значков отображая в пользовательском интерфейсе диспетчера пакетов Visual Studio для пакетов, размещенных в локальных веб-каналах. [#8189](https://github.com/NuGet/Home/issues/8189)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-118">Support for surfacing self-contained icons in Visual Studio package manager UI for packages hosted on local feeds - [#8189](https://github.com/NuGet/Home/issues/8189)</span></span>

* <span data-ttu-id="bb6cd-119">Значительно улучшена производительность восстановления без операций с помощью `RestoreUseStaticGraphEvaluation`, которая ускоряет оценку путем вызова API-интерфейсов статических графов MSBuild — [8791](https://github.com/NuGet/Home/issues/8791)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-119">Significantly improved no-op restore performance using `RestoreUseStaticGraphEvaluation` which speeds up evaluations by calling MSBuild Static Graph APIs - [8791](https://github.com/NuGet/Home/issues/8791)</span></span>

* <span data-ttu-id="bb6cd-120">Улучшена надежность DotNet. exe с помощью подключаемых модулей межплатформенной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="bb6cd-120">Improved dotnet.exe reliability with cross-platform authentication plugins</span></span>
    * <span data-ttu-id="bb6cd-121">Сбой dotnet restore с Таскканцеледексцептион- [#7842](https://github.com/NuGet/Home/issues/7842)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-121">dotnet restore failing with TaskCanceledException - [#7842](https://github.com/NuGet/Home/issues/7842)</span></span>
    * <span data-ttu-id="bb6cd-122">Подключаемый модуль: "задача отменена" — проблема с проверкой подлинности ADO по этой причине.</span><span class="sxs-lookup"><span data-stu-id="bb6cd-122">Plugin:  "A task was cancelled" - problem with ADO authentication due to this.</span></span><span data-ttu-id="bb6cd-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span></span>

* <span data-ttu-id="bb6cd-124">Добавление `dotnet nuget <add|remove|update|disable|enable|list> source` команды [#4126](https://github.com/NuGet/Home/issues/4126)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-124">add `dotnet nuget <add|remove|update|disable|enable|list> source` command - [#4126](https://github.com/NuGet/Home/issues/4126)</span></span>

* <span data-ttu-id="bb6cd-125">Поддержка для `--skip-duplicate` с помощью команды DotNet NuGet Push- [#8778](https://github.com/NuGet/Home/issues/8778)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-125">Suport for `--skip-duplicate`  using dotnet nuget push - [#8778](https://github.com/NuGet/Home/issues/8778)</span></span>

* <span data-ttu-id="bb6cd-126">Поддержка `packages.config` с помощью MSBuild/Restore- [#8506](https://github.com/NuGet/Home/issues/8506)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-126">Support `packages.config` with msbuild /restore - [#8506](https://github.com/NuGet/Home/issues/8506)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="bb6cd-127">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="bb6cd-127">Issues fixed in this release</span></span>

<span data-ttu-id="bb6cd-128">**Ошибки**</span><span class="sxs-lookup"><span data-stu-id="bb6cd-128">**Bugs**</span></span>

* <span data-ttu-id="bb6cd-129">Самостоятельное обновление с помощью API V3 — [#4197](https://github.com/NuGet/Home/issues/4197)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-129">Rework Self-Updater with V3 Apis - [#4197](https://github.com/NuGet/Home/issues/4197)</span></span>

* <span data-ttu-id="bb6cd-130">Неправильная версия зависимости пакета, если для версии зависимости пакета задано значение "\*" — [#6697](https://github.com/NuGet/Home/issues/6697)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-130">Wrong package dependency version If package dependency version is set to '\*' - [#6697](https://github.com/NuGet/Home/issues/6697)</span></span>

* <span data-ttu-id="bb6cd-131">Сообщение об ошибке Еррорунсафепаккажеентри не указывает на источник проблемы — [#7505](https://github.com/NuGet/Home/issues/7505)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-131">ErrorUnsafePackageEntry error message is not pointing to source of problem - [#7505](https://github.com/NuGet/Home/issues/7505)</span></span>

* <span data-ttu-id="bb6cd-132">Файл блокировки не учитывается в сценариях "\*" — [#8073](https://github.com/NuGet/Home/issues/8073)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-132">Lock file is not honored in "\*" scenarios  - [#8073](https://github.com/NuGet/Home/issues/8073)</span></span>

* <span data-ttu-id="bb6cd-133">NuGet. exe не разрешается в последнюю версию пакета при использовании \* in PackageReference (восстановление MSBuild/DotNet/VS) — [#8432](https://github.com/NuGet/Home/issues/8432)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-133">NuGet.exe does not resolve to the latest version of a package when using \* in PackageReference (MSBuild/Dotnet/VS restore do) - [#8432](https://github.com/NuGet/Home/issues/8432)</span></span>

* <span data-ttu-id="bb6cd-134">пакет списка DotNet с несколькими нацеливанием на проект WPF — [#8463](https://github.com/NuGet/Home/issues/8463)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-134">dotnet list package with multi targeting WPF project - [#8463](https://github.com/NuGet/Home/issues/8463)</span></span>

* <span data-ttu-id="bb6cd-135">Улучшение Конкурренциутилитиес (сокращение загрузки ЦП) — [#8653](https://github.com/NuGet/Home/issues/8653)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-135">Improve ConcurrencyUtilities (reduce CPU usage) - [#8653](https://github.com/NuGet/Home/issues/8653)</span></span>

* <span data-ttu-id="bb6cd-136">Спецификация разгрузки для выгруженных сценариев проекта не должна быть создана в предварительном восстановлении — [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-136">DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="bb6cd-137">Пакеты NuGet Visual Studio (RestoreManagerPackage) должны быть автоматической загрузкой событий сборки решения — [#8796](https://github.com/NuGet/Home/issues/8796)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-137">The Visual Studio NuGet packages (RestoreManagerPackage) needs to auto load on solution build events - [#8796](https://github.com/NuGet/Home/issues/8796)</span></span>

* <span data-ttu-id="bb6cd-138">Блокировка в процессе инициализации VSSettings- [#8842](https://github.com/NuGet/Home/issues/8842)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-138">Deadlock in VSSettings init - [#8842](https://github.com/NuGet/Home/issues/8842)</span></span>

* <span data-ttu-id="bb6cd-139">Панель элементов VisualStudio не заполняется из пакета NuGet, если проект помещен в папку решения — [#8868](https://github.com/NuGet/Home/issues/8868)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-139">VisualStudio ToolBox is not populated from a NuGet package if a project is placed in a solution folder - [#8868](https://github.com/NuGet/Home/issues/8868)</span></span>

* <span data-ttu-id="bb6cd-140">VS: бессрочный сбой восстановления решения из-за состояния гонки — [#8881](https://github.com/NuGet/Home/issues/8881)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-140">VS:  solution restore perpetually fails due to race condition - [#8881](https://github.com/NuGet/Home/issues/8881)</span></span>

* <span data-ttu-id="bb6cd-141">Константа "Загрузка.." на вкладке "установленные" и "Поиск</span><span class="sxs-lookup"><span data-stu-id="bb6cd-141">Constant "loading.." on installed tab, and "searching</span></span> <term><span data-ttu-id="bb6cd-142">.. "на вкладке" обновления "— [#8890](https://github.com/NuGet/Home/issues/8890)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-142">.." on updates tab - [#8890](https://github.com/NuGet/Home/issues/8890)</span></span>

* <span data-ttu-id="bb6cd-143">Отсутствие внедренных значков в пользовательском интерфейсе VS PM после истечения срока действия кэша — [#9069](https://github.com/NuGet/Home/issues/9069)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-143">Missing Embedded Icons in VS PM UI after cache expires - [#9069](https://github.com/NuGet/Home/issues/9069)</span></span>

* <span data-ttu-id="bb6cd-144">Запуск пользовательского интерфейса Фиреандфоржет PM — [#9112](https://github.com/NuGet/Home/issues/9112)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-144">FireAndForget PM UI startup - [#9112](https://github.com/NuGet/Home/issues/9112)</span></span>

* <span data-ttu-id="bb6cd-145">Восстановление: недопустимая реализация Инклудиксклудефилес. Equals (...) — [#9167](https://github.com/NuGet/Home/issues/9167)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-145">Restore: IncludeExcludeFiles.Equals(...) implementation is incorrect - [#9167](https://github.com/NuGet/Home/issues/9167)</span></span>

* <span data-ttu-id="bb6cd-146">RESTORE: Паккажеспек. Clone () создает неравенство клона- [#9211](https://github.com/NuGet/Home/issues/9211)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-146">Restore: PackageSpec.Clone() creates unequal clone - [#9211](https://github.com/NuGet/Home/issues/9211)</span></span>

* <span data-ttu-id="bb6cd-147">Отображается список ошибок, хотя флажок "всегда показывать Список ошибок, если сборка завершается с ошибками" не установлен — [#8190](https://github.com/NuGet/Home/issues/8190)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-147">Error list shown although "Always show Error List if build finishes with errors" is not checked - [#8190](https://github.com/NuGet/Home/issues/8190)</span></span>

* <span data-ttu-id="bb6cd-148">Статическое восстановление графа не должно передавать пустое SolutionPath- [#9061](https://github.com/NuGet/Home/issues/9061)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-148">Static Graph restore should not pass empty SolutionPath - [#9061](https://github.com/NuGet/Home/issues/9061)</span></span>

* <span data-ttu-id="bb6cd-149">Восстановление: время, вычисленное для каждого проекта 4 раз, [#9042](https://github.com/NuGet/Home/issues/9042)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-149">Restore: closure computed for each project 4 times - [#9042](https://github.com/NuGet/Home/issues/9042)</span></span>

* <span data-ttu-id="bb6cd-150">RESTORE: Депенденциграфспек. Load (...) не требует JObject- [#9040](https://github.com/NuGet/Home/issues/9040)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-150">Restore: DependencyGraphSpec.Load(...) does not need JObject - [#9040](https://github.com/NuGet/Home/issues/9040)</span></span>

* <span data-ttu-id="bb6cd-151">Восстановление: большие строки, созданные в куче больших объектов (LOH) — [#9031](https://github.com/NuGet/Home/issues/9031)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-151">Restore: large strings created on large object heap (LOH) - [#9031](https://github.com/NuGet/Home/issues/9031)</span></span>

* <span data-ttu-id="bb6cd-152">Пользовательский NuGet. exe на более новом Mono может быть нарушен из-за сопоставителя SDK для MSBuild — [8848](https://github.com/NuGet/Home/issues/8848)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-152">Custom nuget.exe on newer mono might break due to the MSBuild SDK Resolver - [8848](https://github.com/NuGet/Home/issues/8848)</span></span>

* <span data-ttu-id="bb6cd-153">Восстановление завершается ошибкой, если NuGet. дгспек. JSON используется другим процессом — [8692](https://github.com/NuGet/Home/issues/8692)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-153">restore fails when nuget.dgspec.json is "used by another process" - [8692](https://github.com/NuGet/Home/issues/8692)</span></span>

<span data-ttu-id="bb6cd-154">**DCR**</span><span class="sxs-lookup"><span data-stu-id="bb6cd-154">**DCRs**</span></span>

* <span data-ttu-id="bb6cd-155">Логика в _GetRestoreProjectStyle должна быть в задаче [#8804](https://github.com/NuGet/Home/issues/8804)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-155">Logic in _GetRestoreProjectStyle should be in a task - [#8804](https://github.com/NuGet/Home/issues/8804)</span></span>

* <span data-ttu-id="bb6cd-156">По умолчанию на вкладке "установленные" добавьте сведения об устаревании, [#8541](https://github.com/NuGet/Home/issues/8541)</span><span class="sxs-lookup"><span data-stu-id="bb6cd-156">Add deprecation information by default on the installed tab - [#8541](https://github.com/NuGet/Home/issues/8541)</span></span>

<span data-ttu-id="bb6cd-157">**[Список всех проблем, исправленных в этом выпуске — 5,5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span><span class="sxs-lookup"><span data-stu-id="bb6cd-157">**[List of all issues fixed in this release - 5.5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span></span>
