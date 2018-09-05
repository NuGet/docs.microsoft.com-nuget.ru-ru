---
title: 3.5 заметки о выпуске версии-Кандидата
description: Заметки о выпуске для NuGet 3.5 RC, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548542"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="655d1-103">Заметки о выпуске версии-Кандидата NuGet 3.5</span><span class="sxs-lookup"><span data-stu-id="655d1-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="655d1-104">[Заметки о выпуске NuGet 3.5 Beta2](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-заметки о выпуске RTM](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="655d1-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="655d1-105">3,5 выпуск ориентирован на повышение качества и производительности клиенты NuGet.</span><span class="sxs-lookup"><span data-stu-id="655d1-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="655d1-106">Кроме того, мы уже на подходе несколько функций, таких как поддержка [резервные папки](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) поддержки в `.nuspec` и многое другое.</span><span class="sxs-lookup"><span data-stu-id="655d1-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="655d1-107">Список проблем</span><span class="sxs-lookup"><span data-stu-id="655d1-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="655d1-108">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="655d1-108">Bug Fixes</span></span>

* <span data-ttu-id="655d1-109">Происходит сбой установки или восстановления пакета с помощью «пакет содержит несколько `.nuspec` файлы.»</span><span class="sxs-lookup"><span data-stu-id="655d1-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="655d1-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="655d1-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="655d1-111">пакет NuGet принудительно добавляет `.tt` файлы в папку content, независимо от того, что - [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="655d1-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="655d1-112">csproj пакет NuGet (с `project.json`) вызывает сбой, если нет packOptions и владельца в файле JSON - [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="655d1-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="655d1-113">пакет NuGet для `project.json` игнорирует теги packOptions Сводка, авторы, владельцы д - [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="655d1-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="655d1-114">пакет NuGet игнорирует зависимости в выходных данных `.nuspec` для `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="655d1-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="655d1-115">Обновление нескольких пакетов с откатом оставляет проект в поврежденном состоянии - [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="655d1-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="655d1-116">ContentFiles при любом не добавляются для проектов netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="655d1-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="655d1-117">Невозможно упаковать библиотеки, предназначенные для .net Standard правильно - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="655d1-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="655d1-118">Файл "->" новый проект "->" происходит сбой проекта библиотеки классов (переносимая) в Visual Studio 2015 и Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="655d1-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="655d1-119">Ошибка NuGet — 1.0.0-\* не является допустимой строкой версии - [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="655d1-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="655d1-120">Find-Package не отображается, однако работает Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="655d1-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="655d1-121">Ошибка при «Install-Package jquery.validation» в dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="655d1-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="655d1-122">При установленной Visual STUDIO 2015 с обновлением 3 на виртуальном СЕРВЕРЕ, используемые NuGet, возникает ошибка версии 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="655d1-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="655d1-123">Пользовательский Интерфейс диспетчера пакетов: не отображает новой версии после обновления пакета- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="655d1-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="655d1-124">-ApiKey в командной строке удаления не чтения/отправляется в 3.5.0 бета-версии - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="655d1-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="655d1-125">Неправильная строка: стабильный выпуск пакета не должен зависеть предварительной зависимость.</span><span class="sxs-lookup"><span data-stu-id="655d1-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="655d1-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="655d1-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="655d1-127">Создание проекта переносимой библиотеки Классов (net46 и windows 10), get исключение NullRef.</span><span class="sxs-lookup"><span data-stu-id="655d1-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="655d1-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="655d1-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="655d1-129">Обновления NuGet должен предоставить информационное сообщение, если более поздней версии ограничивается ограничению allowedVersions — [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="655d1-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="655d1-130">Подключаемый модуль учетных данных завершил работу с ошибкой -1 / произошла ошибка при загрузке пакета при использовании поставщиков учетных данных с несколькими источниками - [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="655d1-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="655d1-131">пакет NuGet - Newtonsoft.Json отсутствует зависимость пакета - [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="655d1-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="655d1-132">Ошибка в ExecuteSynchronizedCore на Linux и Mac OS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="655d1-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="655d1-133">VS не поддерживает переменные среды в repositoryPath (nuget.exe делает) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="655d1-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="655d1-134">Устранить проблемы со специальными возможностями - [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="655d1-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="655d1-135">Переносимые платформы с дефисами профили, будут отклонены.</span><span class="sxs-lookup"><span data-stu-id="655d1-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="655d1-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="655d1-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="655d1-137">Диспетчер пакетов NuGet должны содержаться этого списка параметры в пакетах, подробно не применяется к `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="655d1-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="655d1-138">NuGet 3.3.0, происходит сбой обновления с помощью "... дополнительное ограничение определенных в packages.config предотвращает эту операцию."</span><span class="sxs-lookup"><span data-stu-id="655d1-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="655d1-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="655d1-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="655d1-140">При установке пакета из локального источника, который не существует вызывает исключение поддельное сообщение - [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="655d1-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="655d1-141">Фильтр «Обновить имеющиеся» показывает обновления, которые нарушают ограничение по версии - [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="655d1-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="655d1-142">Улучшения производительности</span><span class="sxs-lookup"><span data-stu-id="655d1-142">Performance Improvements</span></span>

* <span data-ttu-id="655d1-143">Производительность: Повысить ContentModel target framework синтаксический разбор - [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="655d1-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="655d1-144">Производительность: Избежать чтения `runtime.json` файлы для восстановления, не имеют идентификаторов RID [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="655d1-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="655d1-145">На компьютерах, CI восстановление пример, в который длительность 15 секунд для 3 сек сокращена веб-приложение ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="655d1-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="655d1-146">Производительность: Время загрузки консоль диспетчера пакетов init.ps1, возникает [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="655d1-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="655d1-147">В некоторых случаях из 132s 10s улучшение временных показателей открытия PackageManagerConsole.</span><span class="sxs-lookup"><span data-stu-id="655d1-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="655d1-148">Решайте проблемы с производительностью ReSharper в обновлении NuGet - [#3044](https://github.com/NuGet/Home/issues/3044): на пример проекта, чтобы установить пакеты сокращает время из 140s для 68s.</span><span class="sxs-lookup"><span data-stu-id="655d1-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="655d1-149">Запросы на изменение структуры</span><span class="sxs-lookup"><span data-stu-id="655d1-149">DCRs</span></span>

* <span data-ttu-id="655d1-150">NuGet требуются, чтобы пользователи знали, что обновление или установка в dotnet моникера целевой платформы на основе переносимой библиотеки Классов может привести к ошибкам - [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="655d1-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="655d1-151">Предупреждение bad установку или обновление для проекта с tfm = «dotnet» - [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="655d1-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="655d1-152">Добавление поддержки netcoreapp11 и netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="655d1-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="655d1-153">Печать содержимого заголовка NuGet предупреждения на консоль в nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="655d1-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="655d1-154">Используйте атрибут AssemblyMetadata для `.nuspec` маркер замены - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="655d1-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="655d1-155">Удалите заблокированного свойства из файла блокировки - [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="655d1-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="655d1-156">Пакеты символов никогда не следует использовать при установке или обновить #2807</span><span class="sxs-lookup"><span data-stu-id="655d1-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="655d1-157">Функции</span><span class="sxs-lookup"><span data-stu-id="655d1-157">Features</span></span>

* <span data-ttu-id="655d1-158">Поддержка папки резервной пакета - [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="655d1-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="655d1-159">Разрабатывать и реализовывать понятие типа пакета для поддержки пакетов средство — [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="655d1-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="655d1-160">API для получения пути к папке установки глобальных пакетов - [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="655d1-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="655d1-161">Собственные пакеты обновления, поддержка — [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="655d1-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
