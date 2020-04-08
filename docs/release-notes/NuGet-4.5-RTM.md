---
title: Заметки о выпуске версии NuGet 4.5 RTM
description: Заметки о выпуске для NuGet 4.5 RTM, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 321aedb471bc6f86e9c03878093b199267e31195
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496584"
---
# <a name="nuget-45-release-notes"></a><span data-ttu-id="6a450-103">Заметки о выпуске NuGet 4.5</span><span class="sxs-lookup"><span data-stu-id="6a450-103">NuGet 4.5 Release Notes</span></span>

<span data-ttu-id="6a450-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) включает в себя [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="6a450-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-450"></a><span data-ttu-id="6a450-105">Сводка: Новые возможности версии 4.5.0</span><span class="sxs-lookup"><span data-stu-id="6a450-105">Summary: What's New in 4.5.0</span></span>

## <a name="summary-whats-new-in-452"></a><span data-ttu-id="6a450-106">Сводка: Новые возможности версии 4.5.2</span><span class="sxs-lookup"><span data-stu-id="6a450-106">Summary: What's New in 4.5.2</span></span>

* <span data-ttu-id="6a450-107">Исправление безопасности: разрешения на файлы, созданные внутри ~/.nuget, слишком открыты [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="6a450-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-453"></a><span data-ttu-id="6a450-108">Сводка: Новые возможности версии 4.5.3</span><span class="sxs-lookup"><span data-stu-id="6a450-108">Summary: What's New in 4.5.3</span></span>

* <span data-ttu-id="6a450-109">Исправление безопасности: файлы внутри NUPKG могут иметь относительный путь выше каталога NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="6a450-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="6a450-110">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="6a450-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="6a450-111">Проблемы с .NET Standard 2.0, связанные с .NET Framework и NuGet</span><span class="sxs-lookup"><span data-stu-id="6a450-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="6a450-112">Платформа .NET Standard и ее инструментарий были разработаны таким образом, чтобы проекты, предназначенные для .NET Framework 4.6.1, могли использовать пакеты NuGet и проекты, предназначенные для .NET Standard 2.0 или более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="6a450-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="6a450-113">[В этом документе](https://github.com/dotnet/standard/issues/481) кратко описаны проблемы, связанные с таким сценарием, план их решения, а также обходные пути, которые можно применить в текущем состоянии.</span><span class="sxs-lookup"><span data-stu-id="6a450-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="6a450-114">Вы не можете просмотреть, добавить или обновить DotNetCLITools с помощью диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="6a450-114">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="6a450-115">Проблемы</span><span class="sxs-lookup"><span data-stu-id="6a450-115">Issue</span></span>

<span data-ttu-id="6a450-116">Диспетчер пакетов NuGet не отображается и не позволяет добавить или обновить DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="6a450-116">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="6a450-117">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="6a450-117">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="6a450-118">Возможное решение</span><span class="sxs-lookup"><span data-stu-id="6a450-118">Workaround</span></span>

<span data-ttu-id="6a450-119">DotNetCLIToolReferences нужно изменить вручную в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="6a450-119">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="6a450-120">Изменение требуемой версии .NET Framework может привести к частичному отсутствию данных функции IntelliSense</span><span class="sxs-lookup"><span data-stu-id="6a450-120">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="6a450-121">Проблемы</span><span class="sxs-lookup"><span data-stu-id="6a450-121">Issue</span></span>

<span data-ttu-id="6a450-122">Если изменить требуемую версию .NET Framework в Visual Studio, вы можете получить неполные данные функции IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="6a450-122">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="6a450-123">Это происходит, если использовать PackageReferences в качестве формата диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="6a450-123">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="6a450-124">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="6a450-124">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="6a450-125">Возможное решение</span><span class="sxs-lookup"><span data-stu-id="6a450-125">Workaround</span></span>

<span data-ttu-id="6a450-126">Выполните восстановление вручную.</span><span class="sxs-lookup"><span data-stu-id="6a450-126">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="6a450-127">Пакет в проекте .NET Core, который содержит сборку с недопустимой подписью, может инициировать бесконечный цикл восстановления.</span><span class="sxs-lookup"><span data-stu-id="6a450-127">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="6a450-128">Проблемы</span><span class="sxs-lookup"><span data-stu-id="6a450-128">Issue</span></span>

<span data-ttu-id="6a450-129">Иногда при использовании пакета, содержащего сборку с недопустимой подписью, или при использовании пакета, версия которого задается с помощью параметра DateTime, возникает бесконечный цикл автоматического восстановления пакета [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span><span class="sxs-lookup"><span data-stu-id="6a450-129">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="6a450-130">Возможное решение</span><span class="sxs-lookup"><span data-stu-id="6a450-130">Workaround</span></span>

<span data-ttu-id="6a450-131">Сейчас для этой проблемы не существует обходного решения.</span><span class="sxs-lookup"><span data-stu-id="6a450-131">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="6a450-132">Проблемы, исправленные в рамках NuGet 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="6a450-132">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="6a450-133">Проблемы, исправленные в NuGet 4.4 RTM, описаны в разделе [Заметки о выпуске NuGet 4.4 RTM](../release-notes/nuget-4.4-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="6a450-133">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="6a450-134">Функции</span><span class="sxs-lookup"><span data-stu-id="6a450-134">Features</span></span>

- <span data-ttu-id="6a450-135">Отключение автоматической отправки пакета символов — [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="6a450-135">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="6a450-136">Ошибки</span><span class="sxs-lookup"><span data-stu-id="6a450-136">Bugs</span></span>

- <span data-ttu-id="6a450-137">[Регрессия] в 15.5p1: Portable0.0 пропускается — [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="6a450-137">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="6a450-138">Отсутствуют ресурсы в пакетах после восстановления — [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="6a450-138">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="6a450-139">Поставщики учетных данных подключаемых модулей не работают с URI, содержащими пробелы, — [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="6a450-139">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="6a450-140">Если не удалось восстановить пакет, ошибка должна присутствовать в выходных данных, даже если включен режим минимальной детализации — [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="6a450-140">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="6a450-141">dotnet</span><span class="sxs-lookup"><span data-stu-id="6a450-141">dotnet</span></span>
  - <span data-ttu-id="6a450-142">Команда dotnetcore restore на уровне решения не следует ProjectReference, когда для ReferenceOutputAssembly задано значение false, что ведет к случайным сбоям сборки — [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="6a450-142">dotnetcore restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="6a450-143">Автозавершение в PMC неправильно работает с методами объекта — [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="6a450-143">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="6a450-144">Восстановление nuget.exe завершается с ошибкой при использовании набора инструментов Visual Studio 2015 — [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="6a450-144">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="6a450-145">Производительность: для создания экземпляра PMC расходуется много ресурсов в Visual Studio 2017 — [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="6a450-145">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="6a450-146">Медленное получение сведений о зависимостях при низкоскоростном соединении — [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="6a450-146">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="6a450-147">Команда uninstall-package с параметром -RemoveDependencies завершается ошибкой, если несколько пакетов совместно используют одну зависимость — [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="6a450-147">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="6a450-148">Финализация NuGet.Core.nupkg для публикации — [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="6a450-148">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="6a450-149">Пакет NuGet разрешает идентификатор зависимости из имени каталога, когда -IncludeProjectReferences используется для csproj + project.json — [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="6a450-149">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="6a450-150">Инициализатор типа для "NuGet.ProxyCache" выдал исключение — [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="6a450-150">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="6a450-151">Проблема с производительностью восстановления NuGet при использовании Kudu — [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="6a450-151">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="6a450-152">Клиенту пользовательского интерфейса не удается показать ошибки или предупреждения, когда выполняется поиск по большим двоичным объектам регистрации — [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="6a450-152">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="6a450-153">Команда Get-Packages -Updates создает неправильный запрос — [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="6a450-153">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="6a450-154">Ссылки на проблемы GitHub, исправленные в версии 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="6a450-154">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="6a450-155">Список проблем</span><span class="sxs-lookup"><span data-stu-id="6a450-155">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
