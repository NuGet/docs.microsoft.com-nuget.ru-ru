---
title: Заметки о выпуске NuGet 5,0 RTM
description: Заметки о выпуске NuGet 5,0, включая известные проблемы, исправления ошибок, новые функции и DCR.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 52c71c6fe1a1854d5aed229abf2ce7ddc2685ae9
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611339"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="2198b-103">Заметки о выпуске NuGet 5,0</span><span class="sxs-lookup"><span data-stu-id="2198b-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="2198b-104">Средства распространения NuGet:</span><span class="sxs-lookup"><span data-stu-id="2198b-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="2198b-105">Версия NuGet</span><span class="sxs-lookup"><span data-stu-id="2198b-105">NuGet version</span></span> | <span data-ttu-id="2198b-106">Доступно в версии Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2198b-106">Available in Visual Studio version</span></span>| <span data-ttu-id="2198b-107">Доступно в пакетах SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="2198b-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="2198b-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="2198b-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="2198b-109">Visual Studio 2019 версии 16,0</span><span class="sxs-lookup"><span data-stu-id="2198b-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="2198b-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="2198b-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="2198b-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="2198b-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="2198b-112">Visual Studio 2019 версии 16.0.4</span><span class="sxs-lookup"><span data-stu-id="2198b-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="2198b-113">[2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="2198b-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="2198b-114"><sup>1</sup> Устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core</span><span class="sxs-lookup"><span data-stu-id="2198b-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="2198b-115"><sup>2</sup> Доступно в качестве необязательной установки с помощью Visual Studio 2019 с рабочей нагрузкой .NET Core</span><span class="sxs-lookup"><span data-stu-id="2198b-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="2198b-116">Сводка: новые возможности в 5,0</span><span class="sxs-lookup"><span data-stu-id="2198b-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="2198b-117">Поддержка восстановления [отфильтрованных решений](https://docs.microsoft.com/visualstudio/ide/filtered-solutions?view=vs-2019) в Visual Studio 2019 — [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="2198b-117">Support for restoring [filtered solutions](https://docs.microsoft.com/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="2198b-118">`BuildTransitive` папка позволяет пакетам транзитно публиковать целевые объекты и свойства в ведущем проекте — [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="2198b-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="2198b-119">Улучшенная поддержка сценариев PackageReference в интерфейсах API IVs NuGet — [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="2198b-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="2198b-120">`nuget.exe pack project.json` устарела — [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="2198b-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="2198b-121">Подключаемый модуль поставщика учетных данных поколения 1 был заменен [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) и скоро станет устаревшим — [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="2198b-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="2198b-122">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="2198b-122">Issues fixed in this release</span></span>

<span data-ttu-id="2198b-123">**Ошибки**</span><span class="sxs-lookup"><span data-stu-id="2198b-123">**Bugs**</span></span>

* <span data-ttu-id="2198b-124">При выполнении восстановления NoOp Избегайте использования \*. дгспек. JSON Write в каталоге obj — [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="2198b-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="2198b-125">Разрешения для файлов, созданных в ~/.нужет, слишком открыты [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="2198b-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="2198b-126">`dotnet list package --outdated` не работает с источниками, требующими проверки подлинности [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="2198b-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="2198b-127">NuGet. VisualStudio. Ивспаккажеинсталлер — вызов в проекте без ссылок на пакеты всегда использует Packages. config, даже если значение по умолчанию — PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="2198b-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="2198b-128">PMC: не удается выполнить переустановку пакета обновления ("не удается найти пакет") в списке пакетов.</span><span class="sxs-lookup"><span data-stu-id="2198b-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="2198b-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="2198b-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="2198b-130">Добавьте уведомление третьих сторон в наш репозиторий и VSIX- [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="2198b-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="2198b-131">NuGet. VisualStudio. Ивспаккажеинсталлер. Инсталлпаккаже должен установить последнюю версию, если не задана версия [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="2198b-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="2198b-132">--Интерактивная поддержка для команды DotNet NuGet Push- [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="2198b-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="2198b-133">При восстановлении с файлом блокировки предупреждение NU1603 не должно быть создано.</span><span class="sxs-lookup"><span data-stu-id="2198b-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="2198b-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="2198b-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="2198b-135">NuGet не должен печатать путь проекта во время восстановления с минимальным протоколированием [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="2198b-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="2198b-136">--Интерактивная поддержка для команды DotNet Remove Package- [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="2198b-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="2198b-137">Добавление обратной передачи NuGet. Packaging. Core с TypeForwardedTo attr- [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="2198b-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="2198b-138">plugins_cache требует более короткий путь, чтобы хорошо работать [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="2198b-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="2198b-139">Предпочитать путь для обнаружения MSBuild, если пользователь не запросил конкретную версию MSBuild- [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="2198b-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="2198b-140">`nuget.exe /?` должны перечислять правильные версии MSBuild — [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="2198b-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="2198b-141">NuGet. targets (498, 5): ошибка: не удалось найти часть пути "/ТМП/нужетскратч-on Mono- [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="2198b-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="2198b-142">При восстановлении необязательно перечисление содержимого всех версий пакетов, на которые имеются ссылки, в кэше компьютера — [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="2198b-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="2198b-143">Автоматическое обнаружение MSBuild всегда выбирает 16,0 после установки VS 2019 Preview — [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="2198b-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="2198b-144">пакет DotNet List в решении выводит дублирующиеся записи для платформы [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="2198b-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="2198b-145">Исключение "пустое имя пути незаконно" при вызове Ивспаккажеинсталлер. Инсталлпаккаже для старых проектов и папки пакетов не существует.</span><span class="sxs-lookup"><span data-stu-id="2198b-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="2198b-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="2198b-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="2198b-147">MSBuild/t: восстановление с минимальным уровнем детализации должно быть более минимальным [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="2198b-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="2198b-148">Пользовательский интерфейс NuGet в VS "область элементов" имеет нечитаемые вкладки из-за проблем с цветом. [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="2198b-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="2198b-149">Разъяснение NuGet. Core & NuGet. Clients License. txt — [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="2198b-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="2198b-150">Инструкция RESTORE не обязательно перечисляет глобальный каталог пакетов при попытке определить тип [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="2198b-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="2198b-151">Ошибки при применении блокировки файлов должны отображаться в Список ошибок окне [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="2198b-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="2198b-152">Устранение проблем NuGet. Configuration — [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="2198b-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="2198b-153">Адаптация к MSBuild обновление расположения установки — [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="2198b-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="2198b-154">NuGet. Build. Tasks. Pack должен быть зависимостью разработки — [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="2198b-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="2198b-155">Добавить точку расширения пакета для включения отладочных символов — [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="2198b-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="2198b-156">`dotnet pack` должны сохранять диапазон версий зависимостей в созданном nupkg (даже если используется плавающая версия) — [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="2198b-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="2198b-157">`dotnet restore` сбой в источнике, прошедшем проверку подлинности, когда в конфигурации уровня пользователя также есть исходный [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="2198b-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="2198b-158">Пакет не должен ограничивать набор Буилдактионс для файлов содержимого — [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="2198b-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="2198b-159">При использовании ProjectReference, который требует, чтобы Ассеттаржетфаллбакк был выполнен, должен предупредить.</span><span class="sxs-lookup"><span data-stu-id="2198b-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="2198b-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="2198b-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="2198b-161">Взаимоблокировка из-за проблем с потоками при вызове CPS (Коммонпрожектсистем) — [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="2198b-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="2198b-162">`dotnet add package` не использует учетные данные из глобальной конфигурации для источника, указанного в файле Local config- [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="2198b-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="2198b-163">Проблемы с потоками при вызове MEF по асинхронным путям кода — [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="2198b-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="2198b-164">Подписывание: ошибка, обнаруженная дважды и без стека вызовов — [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="2198b-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="2198b-165">При установке подписанного пакета с ненадежным сертификатом подписи отображается ошибка — [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="2198b-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="2198b-166">Неправильное восстановление NuGet Нупс, когда 2 проекта совместно используют каталог obj- [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="2198b-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="2198b-167">Не удается использовать PAT с `dotnet restore` в Linux с пакетами из веб-канала с проверкой подлинности — [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="2198b-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="2198b-168">Сбой dotnet restore из-за отключенного веб-канала на уровне компьютера — [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="2198b-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="2198b-169">**DCR**</span><span class="sxs-lookup"><span data-stu-id="2198b-169">**DCRs**</span></span>

* <span data-ttu-id="2198b-170">Предупреждение о последующем удалении "пакет DotNet Project. JSON" — [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="2198b-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="2198b-171">Добавление предупреждения об устаревании для подключаемого модуля учетных данных Gen1. [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="2198b-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="2198b-172">Подписывание: включено репозиторий, чтобы требовать проверку клиента каждого пакета в качестве подписывания репозитория с помощью Репоситорисигнатурес/5.0.0 Resource- [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="2198b-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="2198b-173">ограничение количества HTTP-запросов на источник с помощью NuGet. config — [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="2198b-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="2198b-174">NuGet должен ориентироваться на Net472 (чтобы упростить очистку сборки VSIX 16,0). [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="2198b-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="2198b-175">PMC: команда Remove Опенпаккажепаже- [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="2198b-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="2198b-176">Преобразование NetCoreApp 3,0 в NetStandard 2,1- [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="2198b-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="2198b-177">Добавление поддержки netstandard 2.0 в пакеты NuGet. \* — [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="2198b-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="2198b-178">Разрешить авторам пакетов определять транзитивное поведение ресурсов сборки — [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="2198b-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="2198b-179">Поддержка функции фильтра решений VS 2019.</span><span class="sxs-lookup"><span data-stu-id="2198b-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="2198b-180">Также поддерживает проект, не являющийся решением, или выгруженные проекты.</span><span class="sxs-lookup"><span data-stu-id="2198b-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="2198b-181">Необходимо восстановить полное решение (с помощью CLI или VS), [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="2198b-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="2198b-182">Сборки NuGet 5,0, для которых требуется 4.7.2 .NET (через TFM Change) — [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="2198b-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="2198b-183">Нужетлиценседата из NuGet. Packaging должен быть общедоступным типом.</span><span class="sxs-lookup"><span data-stu-id="2198b-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="2198b-184">Обновление метаданных лицензий, принимаемых из спдкс.</span><span class="sxs-lookup"><span data-stu-id="2198b-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="2198b-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="2198b-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="2198b-186">Удаление устаревших API параметров — [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="2198b-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="2198b-187">Обход времени ожидания восстановления в системах с 1 процессором [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="2198b-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="2198b-188">NuGet предпочитает проверку подлинности NTLM, даже если в NuGet. config есть учетные данные, чтобы фильтровать типы проверки подлинности для учетных данных [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="2198b-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="2198b-189">Включение Ембединтероптипес для PackageReference (соответствующие функции Packages. config) — [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="2198b-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="2198b-190">**[Список всех проблем, исправленных в этом выпуске — 5,0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="2198b-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="2198b-191">Сводка. новые возможности в 5.0.2</span><span class="sxs-lookup"><span data-stu-id="2198b-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="2198b-192">Безопасность (при запуске с помощью DotNet. exe или Mono. exe). папка obj должна быть создана с правильными разрешениями [#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="2198b-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="2198b-193">Сбой восстановления NuGet. exe в Mono/MacOS с пользовательскими NuGet. config и `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span><span class="sxs-lookup"><span data-stu-id="2198b-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="2198b-194">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="2198b-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="2198b-195">Пакеты в FallbackFolders, устанавливаемые пакетом SDK для .NET Core, являются пользовательской установкой и не проходят проверку подписи.</span><span class="sxs-lookup"><span data-stu-id="2198b-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="2198b-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="2198b-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="2198b-197">Проблемы</span><span class="sxs-lookup"><span data-stu-id="2198b-197">Issue</span></span>
<span data-ttu-id="2198b-198">При использовании dotnet.exe 2.x для восстановления проекта с несколькими целевыми объектами (netcoreapp 1.x и netcoreapp 2.x) резервная папка обрабатывается как веб-канал файла.</span><span class="sxs-lookup"><span data-stu-id="2198b-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="2198b-199">Это значит, что при восстановлении NuGet пытается установить пакет из резервной папки в папку глобальных пакетов и выполнить обычную проверки подписи, что приводит к ошибке.</span><span class="sxs-lookup"><span data-stu-id="2198b-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="2198b-200">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="2198b-200">Workaround</span></span>
<span data-ttu-id="2198b-201">Отключите использование резервной папки, задав для параметра `RestoreAdditionalProjectSources` значение Nothing:</span><span class="sxs-lookup"><span data-stu-id="2198b-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="2198b-202">Используйте это с осторожностью, так как пакеты, которые будут восстановлены из резервной папки, теперь будут скачаны из NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="2198b-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>
