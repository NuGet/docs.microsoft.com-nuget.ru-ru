---
title: "3.5 заметки о выпуске версии-Кандидата | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске для RC NuGet 3.5, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "Версия-Кандидат 3.5 NuGet заметки о выпуске, исправления ошибок, известные проблемы, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fdb84da5f1648ce4508afe6ddcf04bddd41284d3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="73e0f-104">Заметки о выпуске версии-Кандидата NuGet 3.5</span><span class="sxs-lookup"><span data-stu-id="73e0f-104">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="73e0f-105">[Заметки о выпуске бета 2 3.5 NuGet](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM заметки о выпуске](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="73e0f-105">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="73e0f-106">3.5 выпуск предназначен для повышения качества и производительности клиентах NuGet.</span><span class="sxs-lookup"><span data-stu-id="73e0f-106">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="73e0f-107">Кроме того, мы доставленные несколько функций, таких как поддержка [резервной папки](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) поддержки в `.nuspec` и многое другое.</span><span class="sxs-lookup"><span data-stu-id="73e0f-107">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="73e0f-108">Список проблем</span><span class="sxs-lookup"><span data-stu-id="73e0f-108">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5 RC")

## <a name="bug-fixes"></a><span data-ttu-id="73e0f-109">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="73e0f-109">Bug Fixes</span></span>

* <span data-ttu-id="73e0f-110">Сбой установки или восстановления пакета с «пакет содержит несколько `.nuspec` файлы.»</span><span class="sxs-lookup"><span data-stu-id="73e0f-110">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="73e0f-111"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="73e0f-111"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="73e0f-112">пакет NuGet принудительно добавляет `.tt` файлы в папку контента, независимо от того, что - [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="73e0f-112">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="73e0f-113">csproj пакет NuGet (с `project.json`) аварийно завершает работу при наличии не packOptions и владельцем в файле JSON - [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="73e0f-113">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="73e0f-114">пакет NuGet для `project.json` игнорирует теги packOptions Сводка, авторов, владельцев и т. д - [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="73e0f-114">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="73e0f-115">пакет NuGet не учитывает зависимости в выходных данных `.nuspec` для `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="73e0f-115">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="73e0f-116">Обновление нескольких пакетов с помощью отката оставляет проект в поврежденном состоянии - [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="73e0f-116">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="73e0f-117">ContentFiles при выполнении любого не добавляются для проектов моникеров netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="73e0f-117">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="73e0f-118">Невозможно упаковать библиотеки, предназначенные для .net Standard правильно - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="73e0f-118">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="73e0f-119">Файл -> Новый проект библиотеки классов (переносимая) проекта завершается с ошибкой VS2015 и Dev15 - "->" [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="73e0f-119">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="73e0f-120">Ошибка NuGet - 1.0.0-\* не является допустимой строкой версии - [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="73e0f-120">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="73e0f-121">Find-Package не отображается, однако works Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="73e0f-121">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="73e0f-122">Ошибка при «Install-Package jquery.validation» на dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="73e0f-122">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="73e0f-123">При установленной VS 2015 с обновлением 3 на виртуальном СЕРВЕРЕ, используемые NuGet, возникает ошибка версии 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="73e0f-123">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="73e0f-124">Пакет пользовательского интерфейса диспетчера: не отображает новые версии после обновления пакета- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="73e0f-124">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="73e0f-125">-ApiKey в командной строке удаления не чтения и отправляется в 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="73e0f-125">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="73e0f-126">Неправильная строка: стабильный выпуск пакета не должен зависеть предварительной зависимостей.</span><span class="sxs-lookup"><span data-stu-id="73e0f-126">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="73e0f-127"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="73e0f-127"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="73e0f-128">Создание проекта PCL (net46 и windows 10) get NullRef исключение.</span><span class="sxs-lookup"><span data-stu-id="73e0f-128">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="73e0f-129"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="73e0f-129"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="73e0f-130">NuGet обновления должен предоставить информационное сообщение, когда более поздняя версия ограничен ограничением значение allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="73e0f-130">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="73e0f-131">Подключаемый модуль учетных данных завершился с ошибкой -1 / Ошибка загрузки пакета при использовании поставщиков учетных данных с несколькими источниками - [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="73e0f-131">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="73e0f-132">пакет NuGet - зависимость пакета отсутствует Newtonsoft.Json - [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="73e0f-132">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="73e0f-133">Ошибка в ExecuteSynchronizedCore на Linux или MacOS + моно - [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="73e0f-133">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="73e0f-134">VS не поддерживает переменные среды в repositoryPath (nuget.exe делает) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="73e0f-134">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="73e0f-135">Устранение проблемы доступа - [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="73e0f-135">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="73e0f-136">Переносимый платформы с дефисами профилей, отклоняются.</span><span class="sxs-lookup"><span data-stu-id="73e0f-136">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="73e0f-137"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="73e0f-137"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="73e0f-138">Диспетчер пакетов NuGet должны содержаться этого списка параметры в пакетах, подробно не применяется к `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="73e0f-138">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="73e0f-139">NuGet 3.3.0 при попытке установить "дополнительное ограничение... определенные в packages.config предотвращает эту операцию."</span><span class="sxs-lookup"><span data-stu-id="73e0f-139">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="73e0f-140"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="73e0f-140"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="73e0f-141">Установка пакета из локального источника, не существует вызывает поддельное сообщение — [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="73e0f-141">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="73e0f-142">«Обновление тупные» отображаются обновления, которые нарушают ограничения версии - [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="73e0f-142">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="73e0f-143">Улучшения производительности</span><span class="sxs-lookup"><span data-stu-id="73e0f-143">Performance Improvements</span></span>

* <span data-ttu-id="73e0f-144">Производительность: Повысить ContentModel target framework синтаксический разбор - [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="73e0f-144">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="73e0f-145">Производительность: Избегайте чтения `runtime.json` файлы для восстановления, которые не имеют идентификаторов RID [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="73e0f-145">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="73e0f-146">На компьютерах CI восстановление образец веб-приложения ASP.NET сжать через 15 секунд для 3 сек.</span><span class="sxs-lookup"><span data-stu-id="73e0f-146">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="73e0f-147">Производительность: Время загрузки консоль диспетчера пакетов init.ps1 [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="73e0f-147">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="73e0f-148">В некоторых случаях 132s десятках Повышение времени, чтобы открыть PackageManagerConsole.</span><span class="sxs-lookup"><span data-stu-id="73e0f-148">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="73e0f-149">Устранить проблемы с производительностью ReSharper в обновлении NuGet - [#3044](https://github.com/NuGet/Home/issues/3044): В образец проекта, чтобы установить пакеты сокращает время из 140s для 68s.</span><span class="sxs-lookup"><span data-stu-id="73e0f-149">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="73e0f-150">Запросы на изменение структуры</span><span class="sxs-lookup"><span data-stu-id="73e0f-150">DCRs</span></span>

* <span data-ttu-id="73e0f-151">NuGet необходимо сообщить пользователям, обновление или установка в tfm dotnet, в основе PCL может привести к ошибкам - [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="73e0f-151">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="73e0f-152">Предупреждать неправильный установку или обновление для проекта с tfm = «dotnet» - [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="73e0f-152">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="73e0f-153">Добавление поддержки netcoreapp11 и netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="73e0f-153">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="73e0f-154">Печать содержимого заголовка NuGet предупреждения на консоль в nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="73e0f-154">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="73e0f-155">Использование атрибута AssemblyMetadata для `.nuspec` токен замены - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="73e0f-155">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="73e0f-156">Удалите свойство заблокированные из файла блокировки - [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="73e0f-156">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="73e0f-157">Пакеты символов никогда не следует использовать в установку или обновление #2807</span><span class="sxs-lookup"><span data-stu-id="73e0f-157">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="73e0f-158">Функции</span><span class="sxs-lookup"><span data-stu-id="73e0f-158">Features</span></span>

* <span data-ttu-id="73e0f-159">Поддержка пакета резервной папки - [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="73e0f-159">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="73e0f-160">Разрабатывать и реализовывать понятие типа пакета для поддержки пакетов средство - [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="73e0f-160">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="73e0f-161">API-Интерфейс для получения пути к папке глобального пакетов - [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="73e0f-161">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="73e0f-162">Поддержка - обновлений пакетов машинного кода [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="73e0f-162">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
