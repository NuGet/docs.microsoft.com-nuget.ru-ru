---
title: Заметки о выпуске версии-кандидата NuGet 4.0
description: Заметки о выпуске для версии-кандидата NuGet 4.0, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 8124b11d0489a2c72ffcfdde28e8528c1da1f677
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821890"
---
# <a name="nuget-40-rc-release-notes"></a><span data-ttu-id="fdd42-103">Заметки о выпуске версии-кандидата NuGet 4.0</span><span class="sxs-lookup"><span data-stu-id="fdd42-103">NuGet 4.0 RC Release Notes</span></span>

[<span data-ttu-id="fdd42-104">Заметки о выпуске версии-кандидата 3.5</span><span class="sxs-lookup"><span data-stu-id="fdd42-104">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="fdd42-105">В [версии-кандидате NuGet 4.0 для Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) реализована поддержка сценариев использования .NET Core, учтены основные пожелания клиентов и улучшена производительность в различных ситуациях.</span><span class="sxs-lookup"><span data-stu-id="fdd42-105">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="fdd42-106">В этой версии появился ряд усовершенствований, таких как поддержка формата PackageReference, использование команд NuGet в качестве целей MSBuild, восстановление пакетов в фоновом режиме и других.</span><span class="sxs-lookup"><span data-stu-id="fdd42-106">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="fdd42-107">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="fdd42-107">Bug Fixes</span></span>

- <span data-ttu-id="fdd42-108">Изменение поведения команды `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span><span class="sxs-lookup"><span data-stu-id="fdd42-108">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

- <span data-ttu-id="fdd42-109">Сбой команды nuget.exe restore на компьютерах только со средой Visual Studio 15 — [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="fdd42-109">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

- <span data-ttu-id="fdd42-110">При выборе команды "Файл" > "Новый проект" > ".NET Core" должна блокироваться сборка во время восстановления — [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="fdd42-110">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

- <span data-ttu-id="fdd42-111">Невозможно восстановить веб-приложение ASP.NET Core, перенесенное из Visual Studio 2015 в Visual Studio 15.</span><span class="sxs-lookup"><span data-stu-id="fdd42-111">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="fdd42-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="fdd42-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

- <span data-ttu-id="fdd42-113">[Сбой теста] Пакет jQuery Validation невозможно удалить с помощью пользовательского интерфейса диспетчера пакетов — [#3755](https://github.com/NuGet/Home/issues/3755)</span><span class="sxs-lookup"><span data-stu-id="fdd42-113">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

- <span data-ttu-id="fdd42-114">При установке пакета в проекте универсальной платформы Windows на основе файла `project.json` родительские проекты также должны восстанавливаться — [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="fdd42-114">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

- <span data-ttu-id="fdd42-115">Уровень детализации при записи источников пакетов в журнал для целей NuGet следует изменить с обычного на высокий — [#3719](https://github.com/NuGet/Home/issues/3719)</span><span class="sxs-lookup"><span data-stu-id="fdd42-115">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

- <span data-ttu-id="fdd42-116">dotnet</span><span class="sxs-lookup"><span data-stu-id="fdd42-116">dotnet</span></span>
  - <span data-ttu-id="fdd42-117">Команда dotnetcore pack3 должна включать документацию XML по умолчанию — [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="fdd42-117">dotnetcore pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

- <span data-ttu-id="fdd42-118">Операция пакетного обновления из пользовательского интерфейса завершается сбоем, если источник без пакета является первым в списке и выбран параметр "Весь источник" — [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="fdd42-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

- <span data-ttu-id="fdd42-119">Команда nuget pack включает не все файлы — [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="fdd42-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

- <span data-ttu-id="fdd42-120">Проблема нехватки памяти — [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="fdd42-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

- <span data-ttu-id="fdd42-121">В разделе ProjectFileDependencyGroups файла ресурсов следует использовать имена библиотек для проектов — [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="fdd42-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

- <span data-ttu-id="fdd42-122">Команда dotnet restore и рекурсивные каталоги — [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="fdd42-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

- <span data-ttu-id="fdd42-123">Сбои Restore3 записываются в журнал как предупреждения, а не как ошибки — [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="fdd42-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

- <span data-ttu-id="fdd42-124">Ошибка Team Foundation Server: "Не удалось найти элемент [файл] в рабочей области или у вас нет разрешения на доступ к нему" — [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="fdd42-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

- <span data-ttu-id="fdd42-125">Если ввести "nuget <packagename>" в поле быстрого поиска Visual Studio, префикс "nuget " сохраняется — [#2719](https://github.com/NuGet/Home/issues/2719)</span><span class="sxs-lookup"><span data-stu-id="fdd42-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

- <span data-ttu-id="fdd42-126">System.Xml.XmlException. Нераспознанный корневой элемент в части "Core Properties".</span><span class="sxs-lookup"><span data-stu-id="fdd42-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="fdd42-127">Строка 2, позиция 2.</span><span class="sxs-lookup"><span data-stu-id="fdd42-127">Line 2, position 2.</span></span><span data-ttu-id="fdd42-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="fdd42-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

- <span data-ttu-id="fdd42-129">Сборка файлов `.nuspec` с экранированными символами &lt; или &gt; в текстовых полях больше не выполняется — [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="fdd42-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

- <span data-ttu-id="fdd42-130">При выполнении команды nuget.exe delete не запрашиваются учетные данные (используется неинтерактивный режим) — [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="fdd42-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

- <span data-ttu-id="fdd42-131">При выполнении команды nuget.exe delete выводится предупреждение о ключе API для локальных источников, хотя это не имеет смысла — [#2625](https://github.com/NuGet/Home/issues/2625)</span><span class="sxs-lookup"><span data-stu-id="fdd42-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

- <span data-ttu-id="fdd42-132">Требуются более понятные сведения об ошибке при установке пакета EF с параметром -pre — [#2566](https://github.com/NuGet/Home/issues/2566)</span><span class="sxs-lookup"><span data-stu-id="fdd42-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

- <span data-ttu-id="fdd42-133">После изменения выбранных решений в диспетчере пакетов произошло аварийное завершение работы Visual Studio — [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="fdd42-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

- <span data-ttu-id="fdd42-134">dotnet</span><span class="sxs-lookup"><span data-stu-id="fdd42-134">dotnet</span></span>
  - <span data-ttu-id="fdd42-135">Команда dotnetcore restore выполняет поиск идентификаторов с учетом регистра в локальных репозиториях в формате плоского списка при использовании гибких версий — [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="fdd42-135">dotnetcore restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

- <span data-ttu-id="fdd42-136">Команда nuget.exe delete неправильно работает для веб-канала версии 2 — [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="fdd42-136">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

- <span data-ttu-id="fdd42-137">Требуется более понятное сообщение об ошибке истечения срока действия для команды nuget.exe push — [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="fdd42-137">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

- <span data-ttu-id="fdd42-138">Восстановление средства завершается сбоем при отсутствии надлежащих операторов импорта без вывода сообщений об ошибках.</span><span class="sxs-lookup"><span data-stu-id="fdd42-138">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="fdd42-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="fdd42-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

- <span data-ttu-id="fdd42-140">NuGet запрашивает учетные данные при наличии закрытого веб-канала, даже если установка производится с сайта nuget.org — [#2346](https://github.com/NuGet/Home/issues/2346)</span><span class="sxs-lookup"><span data-stu-id="fdd42-140">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

- <span data-ttu-id="fdd42-141">Пакет ApplicationInsights 2.0 имеется в списке, но пока не существует — [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="fdd42-141">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

- <span data-ttu-id="fdd42-142">UIDelay в ветви предварительной версии 5 среды Visual Studio 15 — [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="fdd42-142">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

- <span data-ttu-id="fdd42-143">Первое событие OnBuild отсутствует при восстановлении во время сборки для проекта универсальной платформы Windows — [#3489](https://github.com/NuGet/Home/issues/3489)</span><span class="sxs-lookup"><span data-stu-id="fdd42-143">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

- <span data-ttu-id="fdd42-144">Нарушение работы PowerShell5 при установке EntityFramework.</span><span class="sxs-lookup"><span data-stu-id="fdd42-144">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="fdd42-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="fdd42-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

- <span data-ttu-id="fdd42-146">Необходимо добавить источник при подробном ведении журнала (рекомендуется для версии 3.5) — [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="fdd42-146">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

- <span data-ttu-id="fdd42-147">Параметр NoCache не учитывается в версии клиента NuGet 3.4 и более поздних — [#3074](https://github.com/NuGet/Home/issues/3074)</span><span class="sxs-lookup"><span data-stu-id="fdd42-147">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

- <span data-ttu-id="fdd42-148">Если в Visual Studio не удается загрузить поставщик учетных данных, не следует прерывать работу NuGet — [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="fdd42-148">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>

## <a name="features"></a><span data-ttu-id="fdd42-149">Функции</span><span class="sxs-lookup"><span data-stu-id="fdd42-149">Features</span></span>

- <span data-ttu-id="fdd42-150">Настройка непрерывной интеграции для выполнения на 86-разрядных компьютерах — [#3868](https://github.com/NuGet/Home/issues/3868)</span><span class="sxs-lookup"><span data-stu-id="fdd42-150">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

- <span data-ttu-id="fdd42-151">Автоматическое восстановление, 3 из 3: пользовательский интерфейс без блокировки — [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="fdd42-151">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

- <span data-ttu-id="fdd42-152">Автоматическое восстановление, 2 из 3: восстановление в фоновом режиме при назначении — [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="fdd42-152">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

- <span data-ttu-id="fdd42-153">Восстановление ссылок проекта в соответствии с поведением сборки (рекурсивная обработка) — [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="fdd42-153">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

- <span data-ttu-id="fdd42-154">Поддержка DPL в Visual Studio 15 — minbar — [#3614](https://github.com/NuGet/Home/issues/3614)</span><span class="sxs-lookup"><span data-stu-id="fdd42-154">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

- <span data-ttu-id="fdd42-155">Перенос файла параметров в папку Program Files — [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="fdd42-155">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

- <span data-ttu-id="fdd42-156">Создаваемым свойствам и целям восстановления требуется поддержка кроссплатформенного нацеливания — [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="fdd42-156">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

- <span data-ttu-id="fdd42-157">Поддержка восстановления NuGet для PackageTargetFallback (прежнее название — Imports) — [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="fdd42-157">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

- <span data-ttu-id="fdd42-158">Реализация ToolsRef — [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="fdd42-158">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

- <span data-ttu-id="fdd42-159">Restore3 для RID — [#3465](https://github.com/NuGet/Home/issues/3465)</span><span class="sxs-lookup"><span data-stu-id="fdd42-159">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

- <span data-ttu-id="fdd42-160">Поддержка добавления, удаления и обновления ссылок на пакеты в пользовательском интерфейсе NuGet — [#3457](https://github.com/NuGet/Home/issues/3457)</span><span class="sxs-lookup"><span data-stu-id="fdd42-160">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

- <span data-ttu-id="fdd42-161">Автоматическое восстановление, 1 из 3: реализация API номинации путем кэширования сведений о восстановлении проектов — [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="fdd42-161">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

- <span data-ttu-id="fdd42-162">[0] Задача и цели восстановления NuGet — [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="fdd42-162">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

- <span data-ttu-id="fdd42-163">[1] Обеспечение восстановления на уровне решения в MSBuild — [#2993](https://github.com/NuGet/Home/issues/2993)</span><span class="sxs-lookup"><span data-stu-id="fdd42-163">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

- <span data-ttu-id="fdd42-164">Поддержка общедоступной расширяемости для поставщика учетных данных в Visual Studio — [#2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="fdd42-164">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

- <span data-ttu-id="fdd42-165">Рекурсивное восстановление NuGet — [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="fdd42-165">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

- <span data-ttu-id="fdd42-166">Невозможно загрузить Microsoft.TeamFoundation.Client в dev15; необходимо обновить Microsoft.TeamFoundation.Client до версии 15.0 для предварительной версии Visual Studio 15 — [#2392](https://github.com/NuGet/Home/issues/2392)</span><span class="sxs-lookup"><span data-stu-id="fdd42-166">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

- <span data-ttu-id="fdd42-167">Невозможно установить пакет C++ в проекте универсальной платформы Windows на C++ в предварительной версии Visual Studio 15 — [#2369](https://github.com/NuGet/Home/issues/2369)</span><span class="sxs-lookup"><span data-stu-id="fdd42-167">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

- <span data-ttu-id="fdd42-168">Формат Nupkg должен поддерживать папку \buildCrossTargeting\ и импортировать `.targets` / `.props` при кроссплатформенном нацеливании MSBuild.</span><span class="sxs-lookup"><span data-stu-id="fdd42-168">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="fdd42-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="fdd42-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

- <span data-ttu-id="fdd42-170">Структура ToolsReference — [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="fdd42-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

- <span data-ttu-id="fdd42-171">Исправлен пользовательский интерфейс NuGet для поддержки восстановления со ссылками PackageReference в `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span><span class="sxs-lookup"><span data-stu-id="fdd42-171">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

- <span data-ttu-id="fdd42-172">Добавлена кнопка очистки кэша в параметры диспетчера пакетов Visual Studio — [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="fdd42-172">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="fdd42-173">Запросы на изменение структуры</span><span class="sxs-lookup"><span data-stu-id="fdd42-173">DCRs</span></span>

- <span data-ttu-id="fdd42-174">Восстановление решения должно блокироваться во время автоматического восстановления.</span><span class="sxs-lookup"><span data-stu-id="fdd42-174">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="fdd42-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="fdd42-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

- <span data-ttu-id="fdd42-176">Установка NetCore из пользовательского интерфейса диспетчера пакетов NuGet производится для каждого моникера целевой платформы, а не только для тех, которые поддерживаются пакетом — [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="fdd42-176">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

- <span data-ttu-id="fdd42-177">Интерфейс API назначения на восстановление должен также поддерживать DotNetCliToolsReferences.</span><span class="sxs-lookup"><span data-stu-id="fdd42-177">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="fdd42-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="fdd42-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

- <span data-ttu-id="fdd42-179">Расширение VSIX для Visual Studio 15 помечено как systemcomponent — [#3700](https://github.com/NuGet/Home/issues/3700)</span><span class="sxs-lookup"><span data-stu-id="fdd42-179">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

- <span data-ttu-id="fdd42-180">Переход от ссылок на MS.VS.Services.Client к ссылкам на MS.VS.Services.Client.Interactive — [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="fdd42-180">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

- <span data-ttu-id="fdd42-181">Свойство $(RestoreLegacyPackagesDirectory) должно учитываться командой восстановления на уровне проекта — [#3618](https://github.com/NuGet/Home/issues/3618)</span><span class="sxs-lookup"><span data-stu-id="fdd42-181">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

- <span data-ttu-id="fdd42-182">При восстановлении в проекте с одним значением TargetFramework не должны применяться условия к свойствам — [#3588](https://github.com/NuGet/Home/issues/3588)</span><span class="sxs-lookup"><span data-stu-id="fdd42-182">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

- <span data-ttu-id="fdd42-183">dotnet</span><span class="sxs-lookup"><span data-stu-id="fdd42-183">dotnet</span></span>
  - <span data-ttu-id="fdd42-184">Команда dotnetcore restore3 foo.csproj должна учитывать зависимости projectref и восстанавливать их так же,</span><span class="sxs-lookup"><span data-stu-id="fdd42-184">dotnetcore restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="fdd42-185">как при сборке.</span><span class="sxs-lookup"><span data-stu-id="fdd42-185">Like build.</span></span><span data-ttu-id="fdd42-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="fdd42-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

- <span data-ttu-id="fdd42-187">Зависимости "type": "platform" представлены как "type":"package" в файле блокировки — [#2695](https://github.com/NuGet/Home/issues/2695)</span><span class="sxs-lookup"><span data-stu-id="fdd42-187">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

- <span data-ttu-id="fdd42-188">В режиме подробного вывода nuget.exe должен отображаться URL-адрес скачивания — [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="fdd42-188">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

- <span data-ttu-id="fdd42-189">Перенос NuGet xplat в Microsoft.NetCore.App и netcoreapp1.0 — [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="fdd42-189">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

- <span data-ttu-id="fdd42-190">Принудительная отправка — при отправке из командной строки должна быть возможность переопределить сервер символов — [#2348](https://github.com/NuGet/Home/issues/2348)</span><span class="sxs-lookup"><span data-stu-id="fdd42-190">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

- <span data-ttu-id="fdd42-191">Объединение кода для определения пути к папке глобальных пакетов — [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="fdd42-191">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

- <span data-ttu-id="fdd42-192">suppressParent необходимо заменить на лучшее имя — [#2196](https://github.com/NuGet/Home/issues/2196)</span><span class="sxs-lookup"><span data-stu-id="fdd42-192">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

- <span data-ttu-id="fdd42-193">Определение имени зависимости `project.json`, которое следует использовать для проектов MSBuild — [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="fdd42-193">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

- <span data-ttu-id="fdd42-194">Добавление поддержки SemVer 2.0.0 в NuGet.Core — [#3383](https://github.com/NuGet/Home/issues/3383)</span><span class="sxs-lookup"><span data-stu-id="fdd42-194">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

- <span data-ttu-id="fdd42-195">Доступность файлов NUPKG транзитивной зависимости с `.targets` в MSBuild — [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="fdd42-195">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

- <span data-ttu-id="fdd42-196">Операция восстановления NuGet из командной строки выполняется значительно медленнее, чем в Visual Studio — [#3330](https://github.com/NuGet/Home/issues/3330)</span><span class="sxs-lookup"><span data-stu-id="fdd42-196">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

- <span data-ttu-id="fdd42-197">Отключение учета регистра при сравнении идентификаторов и версий пакетов — [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="fdd42-197">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

- <span data-ttu-id="fdd42-198">Параметр NoCache не работает при восстановлении или установке на основе `packages.config` (GlobalPackagesFolder) — [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="fdd42-198">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

- <span data-ttu-id="fdd42-199">Ресурсам FindPackageByIdResource требуется контекст кэша по умолчанию и средство ведения журнала — [#1357](https://github.com/NuGet/Home/issues/1357)</span><span class="sxs-lookup"><span data-stu-id="fdd42-199">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
