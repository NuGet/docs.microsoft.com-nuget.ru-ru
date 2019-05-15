---
title: Заметки о выпуске NuGet 5.0 RTM
description: Заметки о выпуске для NuGet 5.0, включая известные проблемы, исправления ошибок, новые функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 7e719a3bb5069c461820c6f884487af1eb04bf86
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610660"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="78b7a-103">Заметки о выпуске 5.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="78b7a-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="78b7a-104">Средства распространения NuGet:</span><span class="sxs-lookup"><span data-stu-id="78b7a-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="78b7a-105">Версия NuGet</span><span class="sxs-lookup"><span data-stu-id="78b7a-105">NuGet version</span></span> | <span data-ttu-id="78b7a-106">Доступно в версии Visual Studio</span><span class="sxs-lookup"><span data-stu-id="78b7a-106">Available in Visual Studio version</span></span>| <span data-ttu-id="78b7a-107">Доступно в пакетах SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="78b7a-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="78b7a-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="78b7a-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="78b7a-109">Версия 16.0 2019 г. Visual Studio</span><span class="sxs-lookup"><span data-stu-id="78b7a-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="78b7a-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="78b7a-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="78b7a-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="78b7a-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="78b7a-112">Версия 16.0.4 2019 г. Visual Studio</span><span class="sxs-lookup"><span data-stu-id="78b7a-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="78b7a-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="78b7a-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="78b7a-114"><sup>1</sup>устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core</span><span class="sxs-lookup"><span data-stu-id="78b7a-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="78b7a-115"><sup>2</sup>доступно в виде необязательно установку с помощью Visual Studio 2019 с рабочей нагрузкой .NET Core</span><span class="sxs-lookup"><span data-stu-id="78b7a-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="78b7a-116">Сводка: Новые возможности в версии 5.0</span><span class="sxs-lookup"><span data-stu-id="78b7a-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="78b7a-117">Поддержка восстановления [отфильтрованные решения](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) в Visual Studio 2019 г. - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="78b7a-117">Support for restoring [filtered solutions](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="78b7a-118">`BuildTransitive` Папка включает пакеты транзитивно участвовать целевых объектов и свойств, проект ведущего приложения — [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="78b7a-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="78b7a-119">Улучшенная поддержка сценариев PackageReference в NuGet IV API - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="78b7a-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="78b7a-120">`nuget.exe pack project.json` является устаревшим - [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="78b7a-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="78b7a-121">Подключаемый модуль поставщика учетных данных Gen 1 был замещен стандартом [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) и вскоре будет объявлен устаревшим - [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="78b7a-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="78b7a-122">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="78b7a-122">Issues fixed in this release</span></span>

<span data-ttu-id="78b7a-123">**Ошибки**</span><span class="sxs-lookup"><span data-stu-id="78b7a-123">**Bugs**</span></span>

* <span data-ttu-id="78b7a-124">При выполнении восстановления NoOp, избегайте использования \*. dgspec.json записи в каталоге obj - [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="78b7a-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="78b7a-125">Разрешения на файлы, созданные внутри ~/.nuget слишком открыты - [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="78b7a-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="78b7a-126">`dotnet list package --outdated` не работает с источниками, которым требуется проверка подлинности - [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="78b7a-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="78b7a-127">NuGet.VisualStudio.IVsPackageInstaller - вызов метода для проекта без пакета ссылается на всегда использует packages.config, даже если значение по умолчанию имеет значение PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="78b7a-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="78b7a-128">В КОНСОЛИ ДИСПЕТЧЕРА ПАКЕТОВ: Update-Package переустановите завершается сбоем («не удалось найти пакет») на delisted пакетов.</span><span class="sxs-lookup"><span data-stu-id="78b7a-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="78b7a-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="78b7a-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="78b7a-130">Добавить уведомление третьих лиц в репозиторий, а также VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="78b7a-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="78b7a-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage следует установить последнюю версию, если версия, не учитывая - [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="78b7a-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="78b7a-132">--интерактивной поддержки dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="78b7a-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="78b7a-133">При восстановлении с помощью блокировки файла, не должны вызываться NU1603 предупреждение.</span><span class="sxs-lookup"><span data-stu-id="78b7a-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="78b7a-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="78b7a-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="78b7a-135">NuGet не следует печатать путь проекта во время восстановления при минимальном ведении журнала - [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="78b7a-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="78b7a-136">--пакет удаляется интерактивной поддержки для команды dotnet - [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="78b7a-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="78b7a-137">Добавьте обратно NuGet.Packaging.Core с TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="78b7a-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="78b7a-138">plugins_cache требуется более короткий путь к работают хорошо - [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="78b7a-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="78b7a-139">Предпочитать путь для обнаружения msbuild, если пользователь не запросить определенные msbuild версии - [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="78b7a-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="78b7a-140">`nuget.exe /?` должно отобразиться правильное msbuild версии — [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="78b7a-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="78b7a-141">NuGet.targets(498,5): ошибка: Не удалось найти часть пути "/ tmp/NuGetScratch - в mono — [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="78b7a-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="78b7a-142">Восстановление без необходимости выполняет перечисление содержимого всех версий пакета, на которые имеются ссылки в кэше машины - [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="78b7a-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="78b7a-143">Автоматическое обнаружение MSBuild всегда выбирает 16.0 после установки VS 2019 предварительной версии — [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="78b7a-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="78b7a-144">DotNet пакета списка над решением, выводит повторяющиеся записи для framework — [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="78b7a-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="78b7a-145">Исключение «пустой путь не является допустимым» при вызывающий IVsPackageInstaller.InstallPackage прежние проектов и пакетов папка не существует.</span><span class="sxs-lookup"><span data-stu-id="78b7a-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="78b7a-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="78b7a-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="78b7a-147">минимальной детализации MSBuild/t: RESTORE должно быть более минимальным - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="78b7a-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="78b7a-148">VS 16.0 в пользовательский Интерфейс NuGet может быть прочитан появляются из-за проблем цвет - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="78b7a-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="78b7a-149">NuGet.Core & разъяснение NuGet.Clients License.txt - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="78b7a-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="78b7a-150">Восстановление без необходимости перечисляет папку глобальных пакетов, пытаясь определить тип - [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="78b7a-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="78b7a-151">Ошибки из принудительного применения блокировки файла, будет показан в окно списка ошибок - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="78b7a-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="78b7a-152">Устранение проблем NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="78b7a-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="78b7a-153">Адаптироваться к MSBuild, обновление его установки расположение - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="78b7a-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="78b7a-154">NuGet.Build.Tasks.Pack должен быть объект как зависимость разработки - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="78b7a-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="78b7a-155">Добавьте пакет точку расширения для включения отладочных символов - [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="78b7a-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="78b7a-156">`dotnet pack` необходимо сохранять диапазон версий зависимости в созданный nupkg (даже при использовании версии с плавающей запятой) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="78b7a-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="78b7a-157">`dotnet restore` происходит сбой на прошедшего проверку подлинности источника при конфигурации уровня пользователя также имеет источник - [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="78b7a-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="78b7a-158">Пакет не следует ограничивать набор BuildActions для файлов содержимого - [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="78b7a-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="78b7a-159">С помощью ProjectReference, который требует AssetTargetFallback для успешного выполнения, следует предупредить.</span><span class="sxs-lookup"><span data-stu-id="78b7a-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="78b7a-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="78b7a-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="78b7a-161">Взаимоблокировка из-за проблем многопоточности, при вызове в CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="78b7a-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="78b7a-162">`dotnet add package` не использует учетные данные из глобального файла конфигурации для источника, указанного в локальном файле конфигурации - [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="78b7a-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="78b7a-163">Потоков проблемы с MEF, вызываемого на async кодовых пути - [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="78b7a-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="78b7a-164">Подписи: сообщение об ошибке дважды и без стека вызовов - [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="78b7a-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="78b7a-165">Установка подписанного пакета с помощью сертификата недоверенном подписи должно отображаться ошибка — [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="78b7a-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="78b7a-166">Восстановление NuGet неправильно ничего не делают при 2 проекта совместный доступ к каталогу obj - [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="78b7a-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="78b7a-167">Нельзя использовать личный маркер доступа с `dotnet restore` на платформе Linux с помощью пакетов из прошедшего проверку подлинности веб-канала - [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="78b7a-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="78b7a-168">Команда DotNet restore завершается ошибкой из-за расширенных веб-канала - отключено машины [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="78b7a-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="78b7a-169">**Запросы на изменение структуры**</span><span class="sxs-lookup"><span data-stu-id="78b7a-169">**DCRs**</span></span>

* <span data-ttu-id="78b7a-170">Предупреждать о будущих удаления «dotnet pack project.json —» [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="78b7a-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="78b7a-171">Добавить предупреждение об устаревании для подключаемый модуль учетных данных Gen1 - [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="78b7a-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="78b7a-172">Подписи. Автоматический включен репозиторий, чтобы требовать проверку клиента каждый пакет как репозиторий — с помощью ресурса RepositorySignatures/5.0.0 - [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="78b7a-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="78b7a-173">Максимальное число запросов http на каждый источник через NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="78b7a-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="78b7a-174">NuGet должны быть нацелены на Net472 (для очистки 16.0 сборку VSIX) — [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="78b7a-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="78b7a-175">В КОНСОЛИ ДИСПЕТЧЕРА ПАКЕТОВ: Удалить команду OpenPackagePage - [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="78b7a-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="78b7a-176">Создание NetCoreApp 3.0 сопоставляются NetStandard 2.1 — [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="78b7a-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="78b7a-177">Добавление поддержки netstandard2.0 к пакетам NuGet.\* - [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="78b7a-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="78b7a-178">Авторы пакета для определения поведения транзитивное активы сборки - [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="78b7a-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="78b7a-179">Поддерживает функцию фильтра решения VS 2019 г.</span><span class="sxs-lookup"><span data-stu-id="78b7a-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="78b7a-180">Также поддерживает проект не в решении или выгруженные проекты.</span><span class="sxs-lookup"><span data-stu-id="78b7a-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="78b7a-181">Сначала потребуется восстановление полного решения (с помощью интерфейса командной строки или Visual STUDIO) - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="78b7a-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="78b7a-182">Сборки NuGet 5.0 требуется .NET Framework 4.7.2 (посредством изменения TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="78b7a-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="78b7a-183">NuGetLicenseData из NuGet.Packaging должен быть открытым.</span><span class="sxs-lookup"><span data-stu-id="78b7a-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="78b7a-184">Обновите метаданные лицензии, полученные из spdx.</span><span class="sxs-lookup"><span data-stu-id="78b7a-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="78b7a-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="78b7a-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="78b7a-186">Удалить устаревшие параметры API - [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="78b7a-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="78b7a-187">Обходной путь восстановления тайм-аутов на системах с 1 ЦП — [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="78b7a-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="78b7a-188">Проверку подлинности NTLM, является предпочтительным NuGet, даже при наличии учетных данных в NuGet.config: Добавление параметра-config для фильтрации типов проверки подлинности учетных данных — [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="78b7a-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="78b7a-189">Включить EmbedInteropTypes для PackageReference (соответствующие возможности Packages.Config) - [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="78b7a-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="78b7a-190">**[Список всех проблем, исправленных в этом выпуске - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="78b7a-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="78b7a-191">Сводка: Новые возможности в 5.0.2</span><span class="sxs-lookup"><span data-stu-id="78b7a-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="78b7a-192">Безопасность (при запуске через dotnet.exe или mono.exe) — папка obj должен будет создан и имеются необходимые разрешения [#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="78b7a-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="78b7a-193">Восстановление NuGet.exe в mono, Mac OS завершается с пользовательских nuget.config и `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span><span class="sxs-lookup"><span data-stu-id="78b7a-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="78b7a-194">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="78b7a-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="78b7a-195">Пакеты в FallbackFolders, устанавливаемые пакетом SDK для .NET Core, являются пользовательской установкой и не проходят проверку подписи.</span><span class="sxs-lookup"><span data-stu-id="78b7a-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="78b7a-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="78b7a-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="78b7a-197">Проблемы</span><span class="sxs-lookup"><span data-stu-id="78b7a-197">Issue</span></span>
<span data-ttu-id="78b7a-198">При использовании dotnet.exe 2.x для восстановления проекта с несколькими целевыми объектами (netcoreapp 1.x и netcoreapp 2.x) резервная папка обрабатывается как веб-канал файла.</span><span class="sxs-lookup"><span data-stu-id="78b7a-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="78b7a-199">Это значит, что при восстановлении NuGet пытается установить пакет из резервной папки в папку глобальных пакетов и выполнить обычную проверки подписи, что приводит к ошибке.</span><span class="sxs-lookup"><span data-stu-id="78b7a-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="78b7a-200">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="78b7a-200">Workaround</span></span>
<span data-ttu-id="78b7a-201">Отключить использование резервной папки, задав `RestoreAdditionalProjectSources` значение nothing:</span><span class="sxs-lookup"><span data-stu-id="78b7a-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="78b7a-202">Используйте это с осторожностью, поскольку теперь пакеты, которые будет восстановлен из резервной папки будут загружены с сайта NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="78b7a-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>
