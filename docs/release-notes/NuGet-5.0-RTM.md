---
title: Заметки о выпуске NuGet 5.0 RTM
description: Заметки о выпуске для NuGet 5.0, включая известные проблемы, исправления ошибок, новые функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 5e48ff19ea5c4908d7eb0a3cb19a31b738e348eb
ms.sourcegitcommit: 8793f528a11bd8e8fb229cd12e9abba50d61e104
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2019
ms.locfileid: "58921589"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="95598-103">Заметки о выпуске 5.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="95598-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="95598-104">Средства распространения NuGet:</span><span class="sxs-lookup"><span data-stu-id="95598-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="95598-105">Версия NuGet</span><span class="sxs-lookup"><span data-stu-id="95598-105">NuGet version</span></span> | <span data-ttu-id="95598-106">Доступно в версии Visual Studio</span><span class="sxs-lookup"><span data-stu-id="95598-106">Available in Visual Studio version</span></span>| <span data-ttu-id="95598-107">Доступно в пакетах SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="95598-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [**<span data-ttu-id="95598-108">5.0.0</span><span class="sxs-lookup"><span data-stu-id="95598-108">5.0.0</span></span>**](https://nuget.org/downloads) | [<span data-ttu-id="95598-109">Версия 16.0 2019 г. Visual Studio</span><span class="sxs-lookup"><span data-stu-id="95598-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="95598-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="95598-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="95598-111"><sup>1</sup>устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core</span><span class="sxs-lookup"><span data-stu-id="95598-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="95598-112"><sup>2</sup>доступно в виде необязательно установку с помощью Visual Studio 2019 с рабочей нагрузкой .NET Core</span><span class="sxs-lookup"><span data-stu-id="95598-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="95598-113">Сводка: Новые возможности в версии 5.0</span><span class="sxs-lookup"><span data-stu-id="95598-113">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="95598-114">Поддержка восстановления [отфильтрованные решения](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) в Visual Studio 2019 г. - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="95598-114">Support for restoring [filtered solutions](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* `BuildTransitive` <span data-ttu-id="95598-115">Папка включает пакеты транзитивно участвовать целевых объектов и свойств, проект ведущего приложения — [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="95598-115">folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="95598-116">Улучшенная поддержка сценариев PackageReference в NuGet IV API - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="95598-116">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* `nuget.exe pack project.json` <span data-ttu-id="95598-117">является устаревшим - [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="95598-117">has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="95598-118">Подключаемый модуль поставщика учетных данных Gen 1 был замещен стандартом [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) и вскоре будет объявлен устаревшим - [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="95598-118">Gen 1 Credential Provider plugin has been superseded by [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="95598-119">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="95598-119">Issues fixed in this release</span></span>

**<span data-ttu-id="95598-120">Ошибки</span><span class="sxs-lookup"><span data-stu-id="95598-120">Bugs</span></span>**

* <span data-ttu-id="95598-121">При выполнении восстановления NoOp, избегайте использования \*. dgspec.json записи в каталоге obj - [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="95598-121">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="95598-122">Разрешения на файлы, созданные внутри ~/.nuget слишком открыты - [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="95598-122">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* `dotnet list package --outdated` <span data-ttu-id="95598-123">не работает с источниками, которым требуется проверка подлинности - [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="95598-123">doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="95598-124">NuGet.VisualStudio.IVsPackageInstaller - вызов метода для проекта без пакета ссылается на всегда использует packages.config, даже если значение по умолчанию имеет значение PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="95598-124">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="95598-125">В КОНСОЛИ ДИСПЕТЧЕРА ПАКЕТОВ: Update-Package переустановите завершается сбоем («не удалось найти пакет») на delisted пакетов.</span><span class="sxs-lookup"><span data-stu-id="95598-125">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="95598-126"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="95598-126"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="95598-127">Добавить уведомление третьих лиц в репозиторий, а также VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="95598-127">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="95598-128">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage следует установить последнюю версию, если версия, не учитывая - [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="95598-128">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="95598-129">--интерактивной поддержки dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="95598-129">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="95598-130">При восстановлении с помощью блокировки файла, не должны вызываться NU1603 предупреждение.</span><span class="sxs-lookup"><span data-stu-id="95598-130">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="95598-131"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="95598-131"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="95598-132">NuGet не следует печатать путь проекта во время восстановления при минимальном ведении журнала - [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="95598-132">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="95598-133">--пакет удаляется интерактивной поддержки для команды dotnet - [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="95598-133">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="95598-134">Добавьте обратно NuGet.Packaging.Core с TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="95598-134">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="95598-135">plugins_cache требуется более короткий путь к работают хорошо - [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="95598-135">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="95598-136">Предпочитать путь для обнаружения msbuild, если пользователь не запросить определенные msbuild версии - [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="95598-136">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* `nuget.exe /?` <span data-ttu-id="95598-137">должно отобразиться правильное msbuild версии — [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="95598-137">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="95598-138">NuGet.targets(498,5): ошибка: Не удалось найти часть пути "/ tmp/NuGetScratch - в mono — [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="95598-138">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="95598-139">Восстановление без необходимости выполняет перечисление содержимого всех версий пакета, на которые имеются ссылки в кэше машины - [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="95598-139">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="95598-140">Автоматическое обнаружение MSBuild всегда выбирает 16.0 после установки VS 2019 предварительной версии — [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="95598-140">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="95598-141">DotNet пакета списка над решением, выводит повторяющиеся записи для framework — [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="95598-141">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="95598-142">Исключение «пустой путь не является допустимым» при вызывающий IVsPackageInstaller.InstallPackage прежние проектов и пакетов папка не существует.</span><span class="sxs-lookup"><span data-stu-id="95598-142">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="95598-143"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="95598-143"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="95598-144">минимальной детализации MSBuild/t: RESTORE должно быть более минимальным - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="95598-144">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="95598-145">VS 16.0 в пользовательский Интерфейс NuGet может быть прочитан появляются из-за проблем цвет - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="95598-145">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="95598-146">NuGet.Core & разъяснение NuGet.Clients License.txt - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="95598-146">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="95598-147">Восстановление без необходимости перечисляет папку глобальных пакетов, пытаясь определить тип - [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="95598-147">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="95598-148">Ошибки из принудительного применения блокировки файла, будет показан в окно списка ошибок - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="95598-148">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="95598-149">Устранение проблем NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="95598-149">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="95598-150">Адаптироваться к MSBuild, обновление его установки расположение - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="95598-150">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="95598-151">NuGet.Build.Tasks.Pack должен быть объект как зависимость разработки - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="95598-151">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="95598-152">Добавьте пакет точку расширения для включения отладочных символов - [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="95598-152">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* `dotnet pack` <span data-ttu-id="95598-153">необходимо сохранять диапазон версий зависимости в созданный nupkg (даже при использовании версии с плавающей запятой) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="95598-153">should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* `dotnet restore` <span data-ttu-id="95598-154">происходит сбой на прошедшего проверку подлинности источника при конфигурации уровня пользователя также имеет источник - [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="95598-154">fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="95598-155">Пакет не следует ограничивать набор BuildActions для файлов содержимого - [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="95598-155">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="95598-156">С помощью ProjectReference, который требует AssetTargetFallback для успешного выполнения, следует предупредить.</span><span class="sxs-lookup"><span data-stu-id="95598-156">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="95598-157"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="95598-157"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="95598-158">Взаимоблокировка из-за проблем многопоточности, при вызове в CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="95598-158">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* `dotnet add package` <span data-ttu-id="95598-159">не использует учетные данные из глобального файла конфигурации для источника, указанного в локальном файле конфигурации - [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="95598-159">doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="95598-160">Потоков проблемы с MEF, вызываемого на async кодовых пути - [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="95598-160">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="95598-161">Подписи: сообщение об ошибке дважды и без стека вызовов - [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="95598-161">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="95598-162">Установка подписанного пакета с помощью сертификата недоверенном подписи должно отображаться ошибка — [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="95598-162">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="95598-163">Восстановление NuGet неправильно ничего не делают при 2 проекта совместный доступ к каталогу obj - [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="95598-163">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="95598-164">Нельзя использовать личный маркер доступа с `dotnet restore` на платформе Linux с помощью пакетов из прошедшего проверку подлинности веб-канала - [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="95598-164">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="95598-165">Команда DotNet restore завершается ошибкой из-за расширенных веб-канала - отключено машины [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="95598-165">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

**<span data-ttu-id="95598-166">Запросы на изменение структуры</span><span class="sxs-lookup"><span data-stu-id="95598-166">DCRs</span></span>**

* <span data-ttu-id="95598-167">Предупреждать о будущих удаления «dotnet pack project.json —» [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="95598-167">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="95598-168">Добавить предупреждение об устаревании для подключаемый модуль учетных данных Gen1 - [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="95598-168">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="95598-169">Подписи. Автоматический включен репозиторий, чтобы требовать проверку клиента каждый пакет как репозиторий — с помощью ресурса RepositorySignatures/5.0.0 - [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="95598-169">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="95598-170">Максимальное число запросов http на каждый источник через NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="95598-170">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="95598-171">NuGet должны быть нацелены на Net472 (для очистки 16.0 сборку VSIX) — [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="95598-171">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="95598-172">В КОНСОЛИ ДИСПЕТЧЕРА ПАКЕТОВ: Удалить команду OpenPackagePage - [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="95598-172">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="95598-173">Создание NetCoreApp 3.0 сопоставляются NetStandard 2.1 — [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="95598-173">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="95598-174">Добавление поддержки netstandard2.0 к пакетам NuGet.\* - [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="95598-174">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="95598-175">Авторы пакета для определения поведения транзитивное активы сборки - [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="95598-175">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="95598-176">Поддерживает функцию фильтра решения VS 2019 г.</span><span class="sxs-lookup"><span data-stu-id="95598-176">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="95598-177">Также поддерживает проект не в решении или выгруженные проекты.</span><span class="sxs-lookup"><span data-stu-id="95598-177">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="95598-178">Сначала потребуется восстановление полного решения (с помощью интерфейса командной строки или Visual STUDIO) - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="95598-178">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="95598-179">Сборки NuGet 5.0 требуется .NET Framework 4.7.2 (посредством изменения TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="95598-179">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="95598-180">NuGetLicenseData из NuGet.Packaging должен быть открытым.</span><span class="sxs-lookup"><span data-stu-id="95598-180">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="95598-181">Обновите метаданные лицензии, полученные из spdx.</span><span class="sxs-lookup"><span data-stu-id="95598-181">Update license metadata ingested from spdx.</span></span><span data-ttu-id="95598-182"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="95598-182"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="95598-183">Удалить устаревшие параметры API - [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="95598-183">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="95598-184">Обходной путь восстановления тайм-аутов на системах с 1 ЦП — [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="95598-184">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="95598-185">Проверку подлинности NTLM, является предпочтительным NuGet, даже при наличии учетных данных в NuGet.config: Добавление параметра-config для фильтрации типов проверки подлинности учетных данных — [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="95598-185">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="95598-186">Включить EmbedInteropTypes для PackageReference (соответствующие возможности Packages.Config) - [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="95598-186">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

**[<span data-ttu-id="95598-187">Список всех проблем, исправленных в этом выпуске - 5.0 RTM</span><span class="sxs-lookup"><span data-stu-id="95598-187">List of all issues fixed in this release - 5.0 RTM</span></span>](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="known-issues"></a><span data-ttu-id="95598-188">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="95598-188">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="95598-189">Пакеты в FallbackFolders, устанавливаемые пакетом SDK для .NET Core, являются пользовательской установкой и не проходят проверку подписи.</span><span class="sxs-lookup"><span data-stu-id="95598-189">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="95598-190"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="95598-190"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="95598-191">Проблемы</span><span class="sxs-lookup"><span data-stu-id="95598-191">Issue</span></span>
<span data-ttu-id="95598-192">При использовании dotnet.exe 2.x для восстановления проекта с несколькими целевыми объектами (netcoreapp 1.x и netcoreapp 2.x) резервная папка обрабатывается как веб-канал файла.</span><span class="sxs-lookup"><span data-stu-id="95598-192">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="95598-193">Это значит, что при восстановлении NuGet пытается установить пакет из резервной папки в папку глобальных пакетов и выполнить обычную проверки подписи, что приводит к ошибке.</span><span class="sxs-lookup"><span data-stu-id="95598-193">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="95598-194">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="95598-194">Workaround</span></span>
<span data-ttu-id="95598-195">Отключить использование резервной папки, задав `RestoreAdditionalProjectSources` значение nothing:</span><span class="sxs-lookup"><span data-stu-id="95598-195">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="95598-196">Используйте это с осторожностью, поскольку теперь пакеты, которые будет восстановлен из резервной папки будут загружены с сайта NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="95598-196">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>
