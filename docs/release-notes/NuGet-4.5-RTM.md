---
title: Заметки о выпуске версии NuGet 4.5 RTM
description: Заметки о выпуске для NuGet 4.5 RTM, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 1d04c508d029a6d92bbd480fe3bd7dc14727970e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-45-rtm-release-notes"></a><span data-ttu-id="56453-103">Заметки о выпуске версии NuGet 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="56453-103">NuGet 4.5 RTM Release Notes</span></span>

<span data-ttu-id="56453-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) включает в себя [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="56453-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="known-issues"></a><span data-ttu-id="56453-105">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="56453-105">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="56453-106">Проблемы с .NET Standard 2.0, связанные с .NET Framework и NuGet</span><span class="sxs-lookup"><span data-stu-id="56453-106">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="56453-107">Платформа .NET Standard и ее инструментарий были разработаны таким образом, чтобы проекты, предназначенные для .NET Framework 4.6.1, могли использовать пакеты NuGet и проекты, предназначенные для .NET Standard 2.0 или более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="56453-107">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="56453-108">[В этом документе](https://github.com/dotnet/standard/issues/481) кратко описаны проблемы, связанные с таким сценарием, план их решения, а также обходные пути, которые можно применить в текущем состоянии.</span><span class="sxs-lookup"><span data-stu-id="56453-108">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="56453-109">Вы не можете просмотреть, добавить или обновить DotNetCLITools с помощью диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="56453-109">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="56453-110">Проблеми</span><span class="sxs-lookup"><span data-stu-id="56453-110">Issue</span></span>

<span data-ttu-id="56453-111">Диспетчер пакетов NuGet не отображается и не позволяет добавить или обновить DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="56453-111">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="56453-112">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="56453-112">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="56453-113">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="56453-113">Workaround</span></span>

<span data-ttu-id="56453-114">DotNetCLIToolReferences нужно изменить вручную в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="56453-114">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="56453-115">Изменение требуемой версии .NET Framework может привести к частичному отсутствию данных функции IntelliSense</span><span class="sxs-lookup"><span data-stu-id="56453-115">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="56453-116">Проблеми</span><span class="sxs-lookup"><span data-stu-id="56453-116">Issue</span></span>

<span data-ttu-id="56453-117">Если изменить требуемую версию .NET Framework в Visual Studio, вы можете получить неполные данные функции IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="56453-117">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="56453-118">Это происходит, если использовать PackageReferences в качестве формата диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="56453-118">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="56453-119">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="56453-119">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="56453-120">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="56453-120">Workaround</span></span>

<span data-ttu-id="56453-121">Выполните восстановление вручную.</span><span class="sxs-lookup"><span data-stu-id="56453-121">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="56453-122">Пакет в проекте .NET Core, который содержит сборку с недопустимой подписью, может инициировать бесконечный цикл восстановления.</span><span class="sxs-lookup"><span data-stu-id="56453-122">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="56453-123">Проблеми</span><span class="sxs-lookup"><span data-stu-id="56453-123">Issue</span></span>

<span data-ttu-id="56453-124">Иногда при использовании пакета, содержащего сборку с недопустимой подписью, или при использовании пакета, версия которого задается с помощью параметра DateTime, возникает бесконечный цикл автоматического восстановления пакета [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span><span class="sxs-lookup"><span data-stu-id="56453-124">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="56453-125">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="56453-125">Workaround</span></span>

<span data-ttu-id="56453-126">Сейчас для этой проблемы не существует обходного решения.</span><span class="sxs-lookup"><span data-stu-id="56453-126">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="56453-127">Проблемы, исправленные в рамках NuGet 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="56453-127">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="56453-128">Проблемы, исправленные в NuGet 4.4 RTM, описаны в разделе [Заметки о выпуске NuGet 4.4 RTM](../release-notes/nuget-4.4-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="56453-128">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="56453-129">Функции</span><span class="sxs-lookup"><span data-stu-id="56453-129">Features</span></span>

- <span data-ttu-id="56453-130">Отключение автоматической отправки пакета символов — [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="56453-130">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="56453-131">Ошибки</span><span class="sxs-lookup"><span data-stu-id="56453-131">Bugs</span></span>

- <span data-ttu-id="56453-132">[Регрессия] в 15.5p1: Portable0.0 пропускается — [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="56453-132">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="56453-133">Отсутствуют ресурсы в пакетах после восстановления — [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="56453-133">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="56453-134">Поставщики учетных данных подключаемых модулей не работают с URI, содержащими пробелы, — [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="56453-134">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="56453-135">Если не удалось восстановить пакет, ошибка должна присутствовать в выходных данных, даже если включен режим минимальной детализации — [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="56453-135">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="56453-136">dotnet</span><span class="sxs-lookup"><span data-stu-id="56453-136">dotnet</span></span>
  - <span data-ttu-id="56453-137">Команда dotnetcore restore на уровне решения не следует ProjectReference, когда для ReferenceOutputAssembly задано значение false, что ведет к случайным сбоям сборки — [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="56453-137">dotnetcore restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="56453-138">Автозавершение в PMC неправильно работает с методами объекта — [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="56453-138">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="56453-139">Восстановление nuget.exe завершается с ошибкой при использовании набора инструментов Visual Studio 2015 — [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="56453-139">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="56453-140">Производительность: для создания экземпляра PMC расходуется много ресурсов в Visual Studio 2017 — [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="56453-140">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="56453-141">Медленное получение сведений о зависимостях при низкоскоростном соединении — [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="56453-141">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="56453-142">Команда uninstall-package с параметром -RemoveDependencies завершается ошибкой, если несколько пакетов совместно используют одну зависимость — [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="56453-142">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="56453-143">Финализация NuGet.Core.nupkg для публикации — [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="56453-143">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="56453-144">Пакет NuGet разрешает идентификатор зависимости из имени каталога, когда -IncludeProjectReferences используется для csproj + project.json — [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="56453-144">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="56453-145">Инициализатор типа для "NuGet.ProxyCache" выдал исключение — [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="56453-145">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="56453-146">Проблема с производительностью восстановления NuGet при использовании Kudu — [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="56453-146">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="56453-147">Клиенту пользовательского интерфейса не удается показать ошибки или предупреждения, когда выполняется поиск по большим двоичным объектам регистрации — [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="56453-147">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="56453-148">Команда Get-Packages -Updates создает неправильный запрос — [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="56453-148">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="56453-149">Ссылки на проблемы GitHub, исправленные в версии 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="56453-149">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="56453-150">Список проблем</span><span class="sxs-lookup"><span data-stu-id="56453-150">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
