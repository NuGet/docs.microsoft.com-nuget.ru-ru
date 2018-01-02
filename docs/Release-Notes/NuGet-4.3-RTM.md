---
title: "Заметки о выпуске NuGet 4.3 RTM | Документы Майкрософт"
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: da3bf363-4d9d-446c-b91d-41c4cf6e16a1
description: "Заметки о выпуске для NuGet 4.3 RTM, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры."
keywords: "заметки о выпуске NuGet 4.3 RTM, исправления ошибок, известные проблемы, добавленные функции и запросы на изменение структуры"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: d237c4a29d8a76bba10ff9bb641f2e06329c07a6
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="43-rtm-release-notes"></a><span data-ttu-id="44991-104">Заметки о выпуске версии 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="44991-104">4.3 RTM Release Notes</span></span>

<span data-ttu-id="44991-105">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) включает в себя NuGet 4.3 RTM, который добавляет поддержку новых сценариев, таких как .NET Standard 2.0/.NET Core 2.0, содержит множество исправлений, а также повышает производительность.</span><span class="sxs-lookup"><span data-stu-id="44991-105">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="44991-106">Кроме того, этот выпуск привносит несколько усовершенствований, таких как поддержка семантического версионирования 2.0.0, интеграция ошибок и предупреждений NuGet в MSBuild и многое другое.</span><span class="sxs-lookup"><span data-stu-id="44991-106">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="44991-107">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="44991-107">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="44991-108">Восстановление NuGet может в некоторых случаях считать отключенные источники пакетов включенными.</span><span class="sxs-lookup"><span data-stu-id="44991-108">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="44991-109">Проблема.</span><span class="sxs-lookup"><span data-stu-id="44991-109">Issue:</span></span>
<span data-ttu-id="44991-110">Следующие методы восстановления в командной строке обрабатывают отключенные источники пакетов как включенные.</span><span class="sxs-lookup"><span data-stu-id="44991-110">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="44991-111">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="44991-111">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="44991-112">`dotnet restore` (с использованием файла dotnet.exe, поставляемого с VS или пакетом SDK для NetCore 2.0.0)</span><span class="sxs-lookup"><span data-stu-id="44991-112">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="44991-113">Инструкции по решению:</span><span class="sxs-lookup"><span data-stu-id="44991-113">Workaround:</span></span>
1. <span data-ttu-id="44991-114">Используйте Visual Studio (2017 15.3 или более поздней версии) либо NuGet.exe (4.3.0 или более поздней версии)</span><span class="sxs-lookup"><span data-stu-id="44991-114">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="44991-115">Удалите отключенный источник и продолжите использовать msbuild или dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="44991-115">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="44991-116">Вы можете использовать для своего решения параметр Clear в NuGet.config, а затем задать необходимые для этого решения источники.</span><span class="sxs-lookup"><span data-stu-id="44991-116">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="44991-117">При использовании консоли диспетчера пакетов клавиша ВВОД может не работать</span><span class="sxs-lookup"><span data-stu-id="44991-117">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="44991-118">Проблема.</span><span class="sxs-lookup"><span data-stu-id="44991-118">Issue:</span></span>
<span data-ttu-id="44991-119">Периодически клавиша ВВОД не работает в консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="44991-119">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="44991-120">В этом случае проверьте ход исправления и укажите дополнительные сведения для воспроизведения ошибки.</span><span class="sxs-lookup"><span data-stu-id="44991-120">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="44991-121">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="44991-121">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="44991-122">Решение</span><span class="sxs-lookup"><span data-stu-id="44991-122">Workaround:</span></span>
<span data-ttu-id="44991-123">Перезапустите Visual Studio и откройте консоль управления пакетами перед тем, как открыть решение.</span><span class="sxs-lookup"><span data-stu-id="44991-123">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="44991-124">Кроме того, попробуйте удалить файл `project.lock.json` и выполнить восстановление еще раз.</span><span class="sxs-lookup"><span data-stu-id="44991-124">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-will-be-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="44991-125">Невозможно просмотреть, добавить или обновить DotNetCLITools с помощью диспетчера пакетов Nuget</span><span class="sxs-lookup"><span data-stu-id="44991-125">You will be unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="44991-126">Проблема.</span><span class="sxs-lookup"><span data-stu-id="44991-126">Issue:</span></span>
<span data-ttu-id="44991-127">Диспетчер пакетов NuGet не отображается и не позволяет добавить или обновить DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="44991-127">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="44991-128">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="44991-128">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="44991-129">Решение</span><span class="sxs-lookup"><span data-stu-id="44991-129">Workaround:</span></span>
<span data-ttu-id="44991-130">DotNetCLIToolReferences нужно изменить вручную в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="44991-130">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="44991-131">Изменение требуемой версии .NET Framework может привести к частичному отсутствию данных функции IntelliSense</span><span class="sxs-lookup"><span data-stu-id="44991-131">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="44991-132">Проблема.</span><span class="sxs-lookup"><span data-stu-id="44991-132">Issue:</span></span>
<span data-ttu-id="44991-133">Если изменить требуемую версию .NET Framework в Visual Studio, вы можете получить неполные данные функции IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="44991-133">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="44991-134">Это происходит, если использовать PackageReferences в качестве формата диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="44991-134">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="44991-135">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="44991-135">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="44991-136">Решение</span><span class="sxs-lookup"><span data-stu-id="44991-136">Workaround:</span></span>
<span data-ttu-id="44991-137">Выполните восстановление вручную.</span><span class="sxs-lookup"><span data-stu-id="44991-137">Do a manual restore.</span></span>


## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="44991-138">Проблемы, исправленные в рамках NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="44991-138">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="44991-139">Проблемы, исправленные в NuGet 4.0 RTM, описаны в разделе [Заметки о выпуске NuGet 4.0 RTM](../release-notes/nuget-4.0-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="44991-139">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

<span data-ttu-id="44991-140">**Функция:**</span><span class="sxs-lookup"><span data-stu-id="44991-140">**Feature:**</span></span>

* <span data-ttu-id="44991-141">Улучшение производительности восстановления NuGet: реализация оптимизированного NoOp для восстановлений из командной строки и VS — [#5080](https://github.com/NuGet/Home/issues/5080)</span><span class="sxs-lookup"><span data-stu-id="44991-141">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

* <span data-ttu-id="44991-142">NET Core 2.0: интерфейс командной строки VS/Dotnet должен запускаться с использованием имеющейся функциональности NuGet: резервные папки — [#4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="44991-142">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

* <span data-ttu-id="44991-143">NET Core 2.0: разрешение пользователям пропускать определенные предупреждения о восстановлении (или повышать их до ошибки) — [#4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="44991-143">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

* <span data-ttu-id="44991-144">NET Core 2.0: локализованные сборки в интерфейсе командной строки — [#4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="44991-144">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

* <span data-ttu-id="44991-145">NET Core 2.0: регистрация всех предупреждений/ошибок в файле ресурсов (включая PackageTargetFallback) — [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="44991-145">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

* <span data-ttu-id="44991-146">Включение поддержки TFM: NetStandard2.0, Tizen — [#4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="44991-146">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

* <span data-ttu-id="44991-147">Уменьшение числа проектов NuGet.Core и NuGet.Client (а, соответственно, и библиотек DLL) — [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="44991-147">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

* <span data-ttu-id="44991-148">Добавление возможности помечать предупреждения и ошибки NuGet — [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="44991-148">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>


<span data-ttu-id="44991-149">**Ошибка:**</span><span class="sxs-lookup"><span data-stu-id="44991-149">**Bug:**</span></span>

* <span data-ttu-id="44991-150">msbuild /t:pack завершается с ошибкой "Параметр "DevelopmentDependency" не поддерживается задачей "PackTask"" — [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="44991-150">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

* <span data-ttu-id="44991-151">Структура каталогов для файлов содержимого становится плоской, если не добавлять разделитель каталогов Windows в конце PackagePath — [#4795](https://github.com/NuGet/Home/issues/4795)</span><span class="sxs-lookup"><span data-stu-id="44991-151">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

* <span data-ttu-id="44991-152">Проекты NetCore не поддерживают настройку в качестве developmentDependency — [#4694](https://github.com/NuGet/Home/issues/4694)</span><span class="sxs-lookup"><span data-stu-id="44991-152">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

* <span data-ttu-id="44991-153">RestoreManagerPackage загружается синхронно, что привело к блокировке потока пользовательского интерфейса и взаимоблокировке VS — [#4679](https://github.com/NuGet/Home/issues/4679)</span><span class="sxs-lookup"><span data-stu-id="44991-153">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

* <span data-ttu-id="44991-154">Команда dotnet Restore (и, соответственно, msbuild /t:restore) пропускает проекты с явной зависимостью от проекта решения — [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="44991-154">dotnet Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

* <span data-ttu-id="44991-155">Если решение имеет ссылки, указывающие на один и тот же проект, написанный с разным регистром, восстановление может не работать.</span><span class="sxs-lookup"><span data-stu-id="44991-155">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="44991-156">Это также влияет на различные относительные пути без различий в регистре — [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="44991-156">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

* <span data-ttu-id="44991-157">Исполняемые файлы, восстановленные из пакетов NuGet, больше невозможно выполнить с помощью .NET Core 2.0 — [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="44991-157">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

* <span data-ttu-id="44991-158">NuGet.exe поглощает сведения об исключении при синтаксическом анализе файла решения — [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="44991-158">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

* <span data-ttu-id="44991-159">Пакет помещает файлы содержимого в неправильное расположение, если ContentTargetFolders содержит пути, заканчивающиеся на "/" в Windows — [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="44991-159">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

* <span data-ttu-id="44991-160">Не удается восстановить DotNetCliToolReference для пакета инструментов, ориентированного на netcoreapp1.1 — [#4396](https://github.com/NuGet/Home/issues/4396)</span><span class="sxs-lookup"><span data-stu-id="44991-160">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

* <span data-ttu-id="44991-161">Интерфейс командной строки обновления NuGet оставляет старое условие версии пакета в файле проекта (C++) — [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="44991-161">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

<span data-ttu-id="44991-162">**Запрос на изменение структуры:**</span><span class="sxs-lookup"><span data-stu-id="44991-162">**DCR:**</span></span>

* <span data-ttu-id="44991-163">Read DotnetCliToolTargetFramework из номинации CPS — [#5397](https://github.com/NuGet/Home/issues/5397)</span><span class="sxs-lookup"><span data-stu-id="44991-163">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

* <span data-ttu-id="44991-164">Проверка TPMinV должна работать для UWP в стиле pj — [#4763](https://github.com/NuGet/Home/issues/4763)</span><span class="sxs-lookup"><span data-stu-id="44991-164">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

* <span data-ttu-id="44991-165">Улучшение описания пользовательского интерфейса для пакетов с автоссылками — [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="44991-165">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

* <span data-ttu-id="44991-166">Функция восстановления NuGet выбирает ресурсы компиляции из раздела времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="44991-166">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="44991-167"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="44991-167"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

* <span data-ttu-id="44991-168">Помещение диагностики зависимостей в файл блокировок — [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="44991-168">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="link-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="44991-169">Ссылка на проблемы GitHub, исправленные в версии 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="44991-169">Link to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="44991-170">Список проблем</span><span class="sxs-lookup"><span data-stu-id="44991-170">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
