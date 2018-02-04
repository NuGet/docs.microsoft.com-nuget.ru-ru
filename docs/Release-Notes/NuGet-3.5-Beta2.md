---
title: "3.5 заметки о выпуске бета-версия 2 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске, включая известные проблемы, исправленные ошибки, добавленные функции и DCR второй бета-версии 3.5 NuGet."
keywords: "Второй бета-версии 3.5 NuGet заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4073b669c19f9e96ebd35ba269919b5f42313e7c
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="3f8f1-104">Заметки о выпуске NuGet 3.5 бета-версия 2</span><span class="sxs-lookup"><span data-stu-id="3f8f1-104">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="3f8f1-105">[Заметки о выпуске 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md) | [заметки о выпуске 3.5 RC NuGet](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-105">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="3f8f1-106">NuGet 3.5 бета-версии 2 RTM был выпущен для Visual Studio 2013 и nuget.exe 27 июня 2016 г.</span><span class="sxs-lookup"><span data-stu-id="3f8f1-106">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="3f8f1-107">Полный журнал изменений</span><span class="sxs-lookup"><span data-stu-id="3f8f1-107">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="3f8f1-108">Список проблем</span><span class="sxs-lookup"><span data-stu-id="3f8f1-108">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="3f8f1-109">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="3f8f1-109">Bug Fixes</span></span>

* <span data-ttu-id="3f8f1-110">Обновленные возвращается сообщение об отсутствия поддержки decrpytion пароль в .NET Core для прошедших проверку подлинности веб-каналов - [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-110">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="3f8f1-111">Консоль диспетчера пакетов Get-Package завершается сбоем, если открыт проект .NET Core - [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-111">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="3f8f1-112">Исправьте неправильной обработкой 403 в команде принудительной NuGet [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-112">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="3f8f1-113">Устранение проблем в удаление пакетов в решении, привязанный к системе управления версиями TFS при disableSourceControlIntegration задано значение true - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-113">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="3f8f1-114">Исправьте пакет обновления в пакеты не целевой учетной записи - [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-114">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="3f8f1-115">Позволяет задать уровень ведения журнала для диспетчера пакетов Nuget действия пользовательского интерфейса — уровень детализации MSBuild [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-115">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="3f8f1-116">Исправление конфигурации NuGet — недопустимый ошибка в проекты веб-сайтов - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-116">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="3f8f1-117">Устранение проблемы пакета из `.csproj` при включенных файлов содержимого - [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-117">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="3f8f1-118">DefaultPushSource в `NuGetDefaults.Config` (`ProgramData\NuGet`) не работает — [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-118">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="3f8f1-119">Устранить проблему в выпуске Nuget 3.4.3 - значение не может быть null для создания пакета - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-119">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="3f8f1-120">Восстановление использует сохраненные учетные данные из Nuget.Config для веб-каналов VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-120">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="3f8f1-121">Производительность - исправление чрезмерного выделения в код версии сравнение - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-121">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="3f8f1-122">Устранение проблем, когда несколько экземпляров nuget.exe пытается установить тот же пакет параллельно - [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-122">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="3f8f1-123">Производительность - кэша сведений о зависимостях для нескольких проектов операций - [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-123">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="3f8f1-124">Исправьте проблему там, где пакет источники добавлены из параметров при пустом - исходного списка [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-124">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="3f8f1-125">Устранение ошибки Misleading при попытке установить пакет, который зависит от роли внешних разработки - [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-125">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="3f8f1-126">Установка пакета в консоли PackageManager с параметр «All» пытается первого источника - [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-126">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="3f8f1-127">Устранение проблем с пакетами, файлы со временем записи в будущем (моно) - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-127">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="3f8f1-128">Отображение исключений при сбое поиск проектов в команду update - [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-128">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="3f8f1-129">Содержимое пакета не является правильно восстановить при установке пакета из nuget v3.3 + веб-канала с аргументом - NoCache Если пакет содержит `.nupkg` файлы - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-129">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="3f8f1-130">Устраните проблему с пакетом установки (все источники), если отсутствует пакет из источника 1 - [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-130">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="3f8f1-131">Установить блоки, если один источник отказывает в авторизации - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-131">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="3f8f1-132">`.nuspec`диапазон, должны переопределять версия - IncludeReferencedProjects - версии [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-132">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="3f8f1-133">NuGet 3.3.0 при попытке установить "дополнительное ограничение... определенные в packages.config предотвращает эту операцию."</span><span class="sxs-lookup"><span data-stu-id="3f8f1-133">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="3f8f1-134"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-134"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="3f8f1-135">NuGet.exe обновления удаляет строгое имя сборки и атрибут Private.</span><span class="sxs-lookup"><span data-stu-id="3f8f1-135">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="3f8f1-136"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-136"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="3f8f1-137">Устранение проблем с относительным путем к файлу для «DefaultPushSource» - [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-137">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="3f8f1-138">Улучшения сообщений о сбое обновления Сопоставитель - [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-138">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="3f8f1-139">Возможности и изменения в поведении</span><span class="sxs-lookup"><span data-stu-id="3f8f1-139">Features and Behavior Changes</span></span>

* <span data-ttu-id="3f8f1-140">Принудительная, NuGet.exe не работает параметр времени ожидания - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-140">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="3f8f1-141">не позволяет создавать восстановления NuGet.exe `.props` и `.targets` файлы для `.nuproj` проекты (Регрессия в v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-141">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="3f8f1-142">Требуется API для сравнения платформы с imports - расширяемости [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-142">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="3f8f1-143">Скрыть параметры зависимостей при использовании `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-143">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="3f8f1-144">Распечатать заголовок версии nuget.exe в подробные выходные данные - [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-144">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="3f8f1-145">NuGet необходимо добавить поддержку /nativeassets/ /runtimes/ {rid} {txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="3f8f1-145">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>