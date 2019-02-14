---
title: Заметки о выпуске предварительной версии 5.0 NuGet
description: Заметки о выпуске для предварительных версий NuGet 5.0, включая известные проблемы, исправления ошибок, новые функции и запросы на изменение структуры.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 5889ea52f993fa8fe841f8eb83b6da659cdede93
ms.sourcegitcommit: 1ab750ff17e55c763d646c50e7630138804ce8b8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247663"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="dce6b-103">Заметки о выпуске NuGet Предварительная версия 5.0</span><span class="sxs-lookup"><span data-stu-id="dce6b-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="dce6b-104">NuGet 5.0 предварительных выпусков</span><span class="sxs-lookup"><span data-stu-id="dce6b-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="dce6b-105">13 февраля 2019 г. - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="dce6b-105">February 13, 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span></span>
* <span data-ttu-id="dce6b-106">23 января 2019 г. - [NuGet 5.0 предварительной версии 2](#summary-whats-new-in-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="dce6b-106">January 23, 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span></span>

## <a name="summary-whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="dce6b-107">Сводка: Новые возможности в предварительной версии NuGet 5.0 3</span><span class="sxs-lookup"><span data-stu-id="dce6b-107">Summary: What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="dce6b-108">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="dce6b-108">Issues fixed in this release</span></span> 

<span data-ttu-id="dce6b-109">**Ошибок:**</span><span class="sxs-lookup"><span data-stu-id="dce6b-109">**Bugs:**</span></span>

* <span data-ttu-id="dce6b-110">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="dce6b-110">nuget.exe /?</span></span> <span data-ttu-id="dce6b-111">должно отобразиться правильное msbuild версии — [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="dce6b-111">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="dce6b-112">NuGet.targets(498,5): ошибка: Не удалось найти часть пути "/ tmp/NuGetScratch - в mono — [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="dce6b-112">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="dce6b-113">Восстановление без необходимости выполняет перечисление содержимого всех версий пакета, на которые имеются ссылки в кэше машины - [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="dce6b-113">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="dce6b-114">Автоматическое обнаружение MSBuild всегда выбирает 16.0 после установки VS 2019 предварительной версии — [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="dce6b-114">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="dce6b-115">DotNet пакета списка над решением, выводит повторяющиеся записи для framework — [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="dce6b-115">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="dce6b-116">Исключение «пустой путь не является допустимым» при вызывающий IVsPackageInstaller.InstallPackage прежние проектов и пакетов папка не существует.</span><span class="sxs-lookup"><span data-stu-id="dce6b-116">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="dce6b-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="dce6b-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="dce6b-118">минимальной детализации MSBuild/t: RESTORE должно быть более минимальным - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="dce6b-118">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="dce6b-119">**Запросы на изменение структуры**</span><span class="sxs-lookup"><span data-stu-id="dce6b-119">**DCRs**</span></span>

* <span data-ttu-id="dce6b-120">Авторы пакета для определения поведения транзитивное активы сборки - [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="dce6b-120">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="dce6b-121">Включить восстановление в Visual STUDIO завершится успешно, если проект не является частью решения или не загружен, но ранее был восстановлен - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="dce6b-121">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="dce6b-122">Сводка: Новые возможности в версии 5.0 предварительной версии 2</span><span class="sxs-lookup"><span data-stu-id="dce6b-122">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="dce6b-123">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="dce6b-123">Issues fixed in this release</span></span>

<span data-ttu-id="dce6b-124">**Ошибок:**</span><span class="sxs-lookup"><span data-stu-id="dce6b-124">**Bugs:**</span></span>

* <span data-ttu-id="dce6b-125">VS 16.0 в пользовательский Интерфейс NuGet может быть прочитан появляются из-за проблем цвет - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="dce6b-125">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="dce6b-126">NuGet.Core & разъяснение NuGet.Clients License.txt - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="dce6b-126">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="dce6b-127">Восстановление без необходимости перечисляет папку глобальных пакетов, пытаясь определить тип - [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="dce6b-127">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="dce6b-128">Ошибки из принудительного применения блокировки файла, будет показан в окно списка ошибок - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="dce6b-128">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="dce6b-129">Устранение проблем NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="dce6b-129">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="dce6b-130">Адаптироваться к MSBuild обновление его в папку установки.</span><span class="sxs-lookup"><span data-stu-id="dce6b-130">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="dce6b-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="dce6b-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="dce6b-132">NuGet.Build.Tasks.Pack должен быть объект как зависимость разработки - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="dce6b-132">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="dce6b-133">Добавьте пакет точку расширения для включения отладочных символов - [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="dce6b-133">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="dce6b-134">DotNet pack должен сохранить диапазон версий зависимости в созданный nupkg.</span><span class="sxs-lookup"><span data-stu-id="dce6b-134">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="dce6b-135">(даже при использовании версии с плавающей запятой) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="dce6b-135">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="dce6b-136">Команда DotNet restore завершается ошибкой в источнике, прошедшего проверку подлинности, если конфигурации уровня пользователя также имеет источник - [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="dce6b-136">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="dce6b-137">Пакет не следует ограничивать набор BuildActions для файлов содержимого - [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="dce6b-137">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="dce6b-138">С помощью projectreference, который требует AssetTargetFallback для успешного выполнения, следует предупредить.</span><span class="sxs-lookup"><span data-stu-id="dce6b-138">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="dce6b-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="dce6b-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="dce6b-140">Взаимоблокировка из-за проблем многопоточности, при вызове в CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="dce6b-140">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="dce6b-141">Команда DotNet add, пакет не будет использовать учетные данные из глобального файла конфигурации для источника, указанного в локальном файле конфигурации - [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="dce6b-141">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="dce6b-142">Проблемы с MEF, потока вызван для асинхронного путям кода может отсутствовать - [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="dce6b-142">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="dce6b-143">Подписи: сообщение об ошибке дважды и без стека вызовов - [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="dce6b-143">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="dce6b-144">Установка подписанного пакета с помощью сертификата недоверенном подписи должно отображаться ошибка — [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="dce6b-144">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="dce6b-145">Восстановление NuGet неправильно ничего не делают при 2 проекта совместный доступ к каталогу obj - [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="dce6b-145">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="dce6b-146">Нельзя использовать личный маркер доступа с dotnet restore на платформе Linux с пакетами из прошедшего проверку подлинности веб-канала - [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="dce6b-146">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="dce6b-147">Команда DotNet restore завершается ошибкой из-за расширенных веб-канала - отключено машины [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="dce6b-147">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="dce6b-148">**Запросы на изменение структуры**</span><span class="sxs-lookup"><span data-stu-id="dce6b-148">**DCRs**</span></span>

* <span data-ttu-id="dce6b-149">Сборки NuGet 5.0 требуется .NET Framework 4.7.2 (посредством изменения TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="dce6b-149">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="dce6b-150">NuGetLicenseData из NuGet.Packaging должен быть открытым.</span><span class="sxs-lookup"><span data-stu-id="dce6b-150">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="dce6b-151">Обновите метаданные лицензии, полученные из spdx.</span><span class="sxs-lookup"><span data-stu-id="dce6b-151">Update license metadata ingested from spdx.</span></span><span data-ttu-id="dce6b-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="dce6b-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="dce6b-153">Удалить устаревшие параметры API - [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="dce6b-153">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="dce6b-154">Обходной путь восстановления тайм-аутов на системах с 1 ЦП — [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="dce6b-154">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="dce6b-155">Проверку подлинности NTLM, является предпочтительным NuGet, даже при наличии учетных данных в NuGet.config: Добавление параметра-config для фильтрации типов проверки подлинности учетных данных — [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="dce6b-155">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="dce6b-156">Включить EmbedInteropTypes для PackageReference (соответствующие возможности Packages.Config) - [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="dce6b-156">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="dce6b-157">Список всех ошибок, исправленных в этом выпуске 5.0.0-preview2</span><span class="sxs-lookup"><span data-stu-id="dce6b-157">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="dce6b-158">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="dce6b-158">Known issues</span></span>

#### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="dce6b-159">Выполнение команды dotnet nuget push с параметром --interactive выдает сообщение об ошибке на компьютере Mac.</span><span class="sxs-lookup"><span data-stu-id="dce6b-159">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="dce6b-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="dce6b-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>
<span data-ttu-id="dce6b-161">**Проблема** `--interactive` аргумент не перенаправляется интерфейсом командной строки dotnet и приводит к ошибке `error: Missing value for option 'interactive'` 
 **решение** выполнить любые другие команды dotnet с интерактивной например `dotnet restore --interactive` и пройти проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="dce6b-161">**Issue** The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`
**Workaround** Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="dce6b-162">Результат проверки подлинности затем может быть кэширован поставщиком учетных данных.</span><span class="sxs-lookup"><span data-stu-id="dce6b-162">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="dce6b-163">Затем выполните `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="dce6b-163">Then run `dotnet nuget push`.</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="dce6b-164">Пакеты в FallbackFolders, устанавливаемые пакетом SDK для .NET Core, являются пользовательской установкой и не проходят проверку подписи.</span><span class="sxs-lookup"><span data-stu-id="dce6b-164">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="dce6b-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="dce6b-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="dce6b-166">**Проблема** при использовании dotnet.exe 2.x для восстановления этой netcoreapp нескольких целевых объектов проекта 1.x и netcoreapp 2.x, папке резервной обрабатывается как файл веб-канала.</span><span class="sxs-lookup"><span data-stu-id="dce6b-166">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="dce6b-167">Это значит, что при восстановлении NuGet пытается установить пакет из резервной папки в папку глобальных пакетов и выполнить обычную проверки подписи, что приводит к ошибке.</span><span class="sxs-lookup"><span data-stu-id="dce6b-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="dce6b-168">**Инструкции по решению** отключить использование резервной папки, задав `RestoreAdditionalProjectSources` значение nothing.</span><span class="sxs-lookup"><span data-stu-id="dce6b-168">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="dce6b-169">`<RestoreAdditionalProjectSources/>` Соблюдайте при этом осторожность, так как это приведет к скачиванию большого количества пакетов с NuGet.org, которые иначе были бы восстановлены из резервной папки.</span><span class="sxs-lookup"><span data-stu-id="dce6b-169">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
