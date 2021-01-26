---
title: Заметки о выпуске 3,5 RC
description: Заметки о выпуске для версии-КАНДИДАТа NuGet 3,5, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780202"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="7c2db-103">Заметки о выпуске для версии-КАНДИДАТа NuGet 3,5</span><span class="sxs-lookup"><span data-stu-id="7c2db-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="7c2db-104">[Заметка о выпуске NuGet 3,5 — бета-версия](../release-notes/nuget-3.5-Beta2.md)  |  [Заметки о выпуске NuGet 3,5-RTM](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="7c2db-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="7c2db-105">выпуск 3,5 предназначен для повышения качества и производительности клиентов NuGet.</span><span class="sxs-lookup"><span data-stu-id="7c2db-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="7c2db-106">Кроме того, мы отгрузили несколько функций, таких как поддержка [резервных папок](https://github.com/NuGet/Home/issues/2899), поддержка [PackageType](https://github.com/NuGet/Home/issues/2476) в `.nuspec` и многое другое.</span><span class="sxs-lookup"><span data-stu-id="7c2db-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="7c2db-107">Список проблем</span><span class="sxs-lookup"><span data-stu-id="7c2db-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="7c2db-108">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="7c2db-108">Bug Fixes</span></span>

* <span data-ttu-id="7c2db-109">Установка или восстановление пакета завершается ошибкой с "пакет содержит несколько `.nuspec` файлов".</span><span class="sxs-lookup"><span data-stu-id="7c2db-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="7c2db-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="7c2db-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="7c2db-111">пакет NuGet принудительно добавляет `.tt` файлы в папку содержимого независимо от того, что [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="7c2db-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="7c2db-112">`project.json`Если в JSON-файле нет паккоптионс и владельца, то пакет NuGet Pack CSPROJ (с) завершается сбоем. [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="7c2db-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="7c2db-113">пакет NuGet для `project.json` игнорирует теги паккоптионс, такие как Summary, authors, Owners и т. д. [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="7c2db-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="7c2db-114">пакет NuGet игнорирует зависимости в выходных данных `.nuspec` для `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="7c2db-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="7c2db-115">Обновление нескольких пакетов с помощью отката оставляет проект в неработающем состоянии — [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="7c2db-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="7c2db-116">ContentFiles не добавляются для проектов netstandard — [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="7c2db-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="7c2db-117">Не удалось правильно упаковать библиотеку .NET Standard, [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="7c2db-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="7c2db-118">Файл-> создание проекта > библиотеки классов (переносимые) в VS2015 и Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="7c2db-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="7c2db-119">Ошибка NuGet-1.0.0-\* не является допустимой строкой версии — [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="7c2db-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="7c2db-120">Find-Package не удается отобразить, но Install-Package Works — [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="7c2db-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="7c2db-121">Ошибка при выполнении установки-пакета jQuery. Validation на dev15- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="7c2db-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="7c2db-122">При установке VS 2015 с обновлением 3 на VS, использующем NuGet версии 3.5.0, возникает ошибка. [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="7c2db-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="7c2db-123">Пользовательский интерфейс диспетчера пакетов: не отображает новую версию после обновления пакета [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="7c2db-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="7c2db-124">-ApiKey при удалении Командная строка не считывается и не отправляется в 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="7c2db-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="7c2db-125">Неправильная строка: стабильный выпуск пакета не должен иметь предварительную зависимость.</span><span class="sxs-lookup"><span data-stu-id="7c2db-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="7c2db-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="7c2db-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="7c2db-127">Создание исключения для получения Нуллреф проекта PCL (net46 и Windows 10).</span><span class="sxs-lookup"><span data-stu-id="7c2db-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="7c2db-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="7c2db-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="7c2db-129">Обновление NuGet должно предоставлять информативное сообщение, если более поздняя версия ограничена ограничением Алловедверсионс- [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="7c2db-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="7c2db-130">Подключаемый модуль учетных данных завершил работу с ошибкой 1/ошибка при скачивании пакета при использовании поставщиков учетных данных с несколькими источниками [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="7c2db-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="7c2db-131">пакет NuGet-отсутствует Newtonsoft.Jsдля зависимости пакета — [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="7c2db-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="7c2db-132">Ошибка в Ексекутесинчронизедкоре в Linux/MacOS + Mono- [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="7c2db-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="7c2db-133">VS не поддерживает переменные среды в Репоситорипас (nuget.exe) — [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="7c2db-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="7c2db-134">Устранение проблем с специальными возможностями — [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="7c2db-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="7c2db-135">Переносные платформы с профилем переноса переносов отклоняются.</span><span class="sxs-lookup"><span data-stu-id="7c2db-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="7c2db-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="7c2db-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="7c2db-137">Диспетчер пакетов NuGet должен очистить, что список параметров в сведениях о пакетах не применяется к `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="7c2db-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="7c2db-138">Сбой обновления 3.3.0 NuGet с "дополнительным ограничением... определено в packages.config не разрешает эту операцию. "</span><span class="sxs-lookup"><span data-stu-id="7c2db-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="7c2db-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="7c2db-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="7c2db-140">При установке пакета из локального источника, который не существует, выдается фиктивное сообщение — [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="7c2db-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="7c2db-141">Фильтр "доступные для обновления" показывает обновления, нарушающие ограничение версии — [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="7c2db-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="7c2db-142">Повышение производительности</span><span class="sxs-lookup"><span data-stu-id="7c2db-142">Performance Improvements</span></span>

* <span data-ttu-id="7c2db-143">Производительность: улучшение анализа целевой платформы ContentModel — [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="7c2db-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="7c2db-144">Производительность. Избегайте чтения `runtime.json` файлов для восстановления, не имеющих [#3150](https://github.com/NuGet/Home/issues/3150)RID.</span><span class="sxs-lookup"><span data-stu-id="7c2db-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="7c2db-145">На виртуальных машинах восстановление примера веб-приложения ASP.NET с интервалом от более 15 секунд до 3 секунд.</span><span class="sxs-lookup"><span data-stu-id="7c2db-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="7c2db-146">Производительность: [#2956](https://github.com/NuGet/Home/issues/2956)время загрузки консоли диспетчера пакетов init.ps1.</span><span class="sxs-lookup"><span data-stu-id="7c2db-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="7c2db-147">Время на открытие Паккажеманажерконсоле в некоторых случаях от 132s до 10.</span><span class="sxs-lookup"><span data-stu-id="7c2db-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="7c2db-148">Устранение проблем с производительностью в обновлении NuGet — [#3044](https://github.com/NuGet/Home/issues/3044): в образце проекта время, затрачиваемое на установку пакетов, уменьшенных с 140S до 68S.</span><span class="sxs-lookup"><span data-stu-id="7c2db-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="7c2db-149">Запросы на изменение структуры</span><span class="sxs-lookup"><span data-stu-id="7c2db-149">DCRs</span></span>

* <span data-ttu-id="7c2db-150">NuGet должен уведомить пользователей о том, что обновление или установка в PCL TFM на основе библиотеки, может вызвать проблемы. [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="7c2db-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="7c2db-151">Предупреждать о неправильной установке или обновлении для проекта w/TFM = "DotNet" — [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="7c2db-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="7c2db-152">Добавление поддержки netcoreapp11 и netstandard17 — [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="7c2db-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="7c2db-153">Печать содержимого заголовка NuGet-Warning в консоли в nuget.exe- [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="7c2db-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="7c2db-154">Использование атрибута AssemblyMetadata для `.nuspec` замены токенов — [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="7c2db-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="7c2db-155">Удалите свойство locked из файла блокировки — [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="7c2db-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="7c2db-156">Пакеты символов никогда не следует использовать при установке или обновлении #2807</span><span class="sxs-lookup"><span data-stu-id="7c2db-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="7c2db-157">Компоненты</span><span class="sxs-lookup"><span data-stu-id="7c2db-157">Features</span></span>

* <span data-ttu-id="7c2db-158">Поддержка резервных папок пакетов — [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="7c2db-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="7c2db-159">Разработайте и реализуйте понятие типа пакета для поддержки пакетов средств — [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="7c2db-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="7c2db-160">API для получения пути к папке глобальных пакетов — [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="7c2db-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="7c2db-161">Поддержка обновления собственных пакетов — [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="7c2db-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
