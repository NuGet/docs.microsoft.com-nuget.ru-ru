---
title: Заметки о выпуске 3,5 бета
description: Заметки о выпуске для бета-версии 2 NuGet 3,5, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776396"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="01f95-103">Заметки о выпуске NuGet 3,5 для версии 2</span><span class="sxs-lookup"><span data-stu-id="01f95-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="01f95-104">[NuGet 3,5 — заметки о](../release-notes/nuget-3.5-Beta.md)  |  выпуске бета-версии [NuGet 3,5 — заметки о выпуске RC](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="01f95-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="01f95-105">Бета-версия 2 пакета NuGet 3,5 RTM была выпущена 27 июня 2016 для Visual Studio 2013 и nuget.exe</span><span class="sxs-lookup"><span data-stu-id="01f95-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="01f95-106">Полный журнал изменений</span><span class="sxs-lookup"><span data-stu-id="01f95-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="01f95-107">Список проблем</span><span class="sxs-lookup"><span data-stu-id="01f95-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="01f95-108">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="01f95-108">Bug Fixes</span></span>

* <span data-ttu-id="01f95-109">В .NET Core для веб-каналов, прошедших проверку подлинности, изменено сообщение об ошибке с нехваткой поддержки декрпитион паролей. [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="01f95-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="01f95-110">Get-Package консоли диспетчера пакетов завершается сбоем, если проект .NET Core открыт, [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="01f95-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="01f95-111">Исправление неправильной обработки 403 в команде NuGet Push [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="01f95-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="01f95-112">Устранение проблем при удалении пакетов в решении, привязанном к системе управления версиями TFS, если Дисаблесаурцеконтролинтегратион имеет значение true- [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="01f95-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="01f95-113">Исправление обновления пакета для учета нецелевых пакетов — [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="01f95-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="01f95-114">Используйте уровень детализации MSBuild, чтобы задать уровень ведения журнала для действий пользовательского интерфейса диспетчера пакетов NuGet — [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="01f95-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="01f95-115">Исправление ошибки конфигурации NuGet недопустимо в проектах веб-сайтов — Visual Studio 2015 VSIX (v 3.4.3) — [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="01f95-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="01f95-116">Устранение проблем с пакетами в `.csproj` случае включения файлов содержимого [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="01f95-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="01f95-117">Дефаултпушсаурце в `NuGetDefaults.Config` ( `ProgramData\NuGet` ) не работает — [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="01f95-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="01f95-118">Исправление проблемы в выпуске NuGet 3.4.3. значение не может быть null при создании пакета — [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="01f95-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="01f95-119">Инструкция RESTORE использует сохраненные учетные данные из Nuget.Config для веб-каналов VSTS — [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="01f95-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="01f95-120">Производительность — устранение чрезмерного выделения памяти в версии компарсион Code — [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="01f95-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="01f95-121">Устранение проблем, возникающих, когда несколько экземпляров nuget.exe пытаются установить один и тот же пакет параллельно [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="01f95-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="01f95-122">Сведения о зависимостях кэша производительности для операций с несколькими проектами [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="01f95-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="01f95-123">Устранена проблема, из-за которой невозможно добавить источники пакетов из параметров, если исходный список пуст — [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="01f95-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="01f95-124">Исправьте ошибочную ошибку при попытке установить пакет, зависящий от интерфейсов времени разработки, [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="01f95-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="01f95-125">Установка пакета из консоли PackageManager с параметром "ALL" пытается только первый источник — [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="01f95-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="01f95-126">Устранение проблем с пакетами, имеющими файлы со временем записи в будущем (моно) — [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="01f95-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="01f95-127">Отображать исключение при сбое поиска проектов в команде Update [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="01f95-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="01f95-128">Содержимое пакета не восстанавливается надлежащим образом при установке пакета из канала NuGet v 3.3 + с аргументом-with, если пакет содержит `.nupkg` файлы — [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="01f95-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="01f95-129">Устранить проблему с установкой пакета (все источники), если пакет отсутствует в 1 Источник — [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="01f95-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="01f95-130">Установка блокируется, если один источник не проходит авторизацию [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="01f95-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="01f95-131">`.nuspec` диапазон версий должен переопределять Инклудереференцедпрожектс Version- [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="01f95-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="01f95-132">Сбой обновления 3.3.0 NuGet с "дополнительным ограничением... определено в packages.config не разрешает эту операцию. "</span><span class="sxs-lookup"><span data-stu-id="01f95-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="01f95-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="01f95-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="01f95-134">nuget.exe обновление удаляет строгое имя сборки и частный атрибут.</span><span class="sxs-lookup"><span data-stu-id="01f95-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="01f95-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="01f95-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="01f95-136">Устранение проблем с относительным путем к файлу для "Дефаултпушсаурце" — [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="01f95-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="01f95-137">Улучшение сообщений об ошибках распознавателя обновлений — [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="01f95-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="01f95-138">Изменения в возможностях и работе</span><span class="sxs-lookup"><span data-stu-id="01f95-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="01f95-139">nuget.exe параметр времени ожидания push-уведомлений не работает [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="01f95-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="01f95-140">nuget.exeное восстановление не создает `.props` и `.targets` файлы для `.nuproj` проектов (регрессия в v 3.4.3.855) — [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="01f95-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="01f95-141">Требуется API расширяемости для сравнения платформ с Imports- [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="01f95-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="01f95-142">Скрывать параметры зависимости при использовании `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="01f95-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="01f95-143">Вывод заголовка nuget.exe версии в подробных выходных данных — [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="01f95-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="01f95-144">NuGet должен добавить поддержку для/рунтимес/{Рид}/нативеассетс/{ТКСМ}/- [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="01f95-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>