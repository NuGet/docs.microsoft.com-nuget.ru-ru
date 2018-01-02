---
title: "Заметки о выпуске NuGet 4.4 RTM | Документы Майкрософт"
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5ffca6f6-a126-4407-b22f-1323e7dc44a3
description: "Заметки о выпуске для NuGet 4.3 RTM, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры."
keywords: "заметки о выпуске NuGet 4.3 RTM, исправления ошибок, известные проблемы, добавленные функции и запросы на изменение структуры"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 479f14db0b402476eccab23283a029a839cf51dd
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="44-rtm-release-notes"></a><span data-ttu-id="05886-104">Заметки о выпуске версии 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="05886-104">4.4 RTM Release Notes</span></span>

<span data-ttu-id="05886-105">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) включает в себя NuGet 4.4 RTM.</span><span class="sxs-lookup"><span data-stu-id="05886-105">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="known-issues"></a><span data-ttu-id="05886-106">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="05886-106">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="05886-107">Проблемы с .NET Standard 2.0, связанные с .NET Framework и NuGet</span><span class="sxs-lookup"><span data-stu-id="05886-107">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 
<span data-ttu-id="05886-108">Платформа .NET Standard и ее инструментарий были разработаны таким образом, чтобы проекты, предназначенные для .NET Framework 4.6.1, могли использовать пакеты NuGet и проекты, предназначенные для .NET Standard 2.0 или более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="05886-108">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="05886-109">[В этом документе](https://github.com/dotnet/standard/issues/481) кратко описаны проблемы, связанные с таким сценарием, план их решения, а также обходные пути, которые можно применить в текущем состоянии.</span><span class="sxs-lookup"><span data-stu-id="05886-109">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="05886-110">При использовании консоли диспетчера пакетов клавиша ВВОД может не работать</span><span class="sxs-lookup"><span data-stu-id="05886-110">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="05886-111">Проблема.</span><span class="sxs-lookup"><span data-stu-id="05886-111">Issue:</span></span>
<span data-ttu-id="05886-112">Периодически клавиша ВВОД не работает в консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="05886-112">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="05886-113">В этом случае проверьте ход исправления и укажите дополнительные сведения для воспроизведения ошибки.</span><span class="sxs-lookup"><span data-stu-id="05886-113">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="05886-114">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="05886-114">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="05886-115">Решение</span><span class="sxs-lookup"><span data-stu-id="05886-115">Workaround:</span></span>
<span data-ttu-id="05886-116">Перезапустите Visual Studio и откройте консоль управления пакетами перед тем, как открыть решение.</span><span class="sxs-lookup"><span data-stu-id="05886-116">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="05886-117">Кроме того, попробуйте удалить файл `project.lock.json` и выполнить восстановление еще раз.</span><span class="sxs-lookup"><span data-stu-id="05886-117">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-will-be-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="05886-118">Невозможно просмотреть, добавить или обновить DotNetCLITools с помощью диспетчера пакетов Nuget</span><span class="sxs-lookup"><span data-stu-id="05886-118">You will be unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="05886-119">Проблема.</span><span class="sxs-lookup"><span data-stu-id="05886-119">Issue:</span></span>
<span data-ttu-id="05886-120">Диспетчер пакетов NuGet не отображается и не позволяет добавить или обновить DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="05886-120">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="05886-121">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="05886-121">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="05886-122">Решение</span><span class="sxs-lookup"><span data-stu-id="05886-122">Workaround:</span></span>
<span data-ttu-id="05886-123">DotNetCLIToolReferences нужно изменить вручную в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="05886-123">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="05886-124">Изменение требуемой версии .NET Framework может привести к частичному отсутствию данных функции IntelliSense</span><span class="sxs-lookup"><span data-stu-id="05886-124">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="05886-125">Проблема.</span><span class="sxs-lookup"><span data-stu-id="05886-125">Issue:</span></span>
<span data-ttu-id="05886-126">Если изменить требуемую версию .NET Framework в Visual Studio, вы можете получить неполные данные функции IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="05886-126">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="05886-127">Это происходит, если использовать PackageReferences в качестве формата диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="05886-127">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="05886-128">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="05886-128">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="05886-129">Решение</span><span class="sxs-lookup"><span data-stu-id="05886-129">Workaround:</span></span>
<span data-ttu-id="05886-130">Выполните восстановление вручную.</span><span class="sxs-lookup"><span data-stu-id="05886-130">Do a manual restore.</span></span>


### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="05886-131">Пакет в проекте .NET Core, который содержит сборку с недопустимой подписью, может инициировать бесконечный цикл восстановления.</span><span class="sxs-lookup"><span data-stu-id="05886-131">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="05886-132">Проблема.</span><span class="sxs-lookup"><span data-stu-id="05886-132">Issue:</span></span>
<span data-ttu-id="05886-133">Иногда при использовании пакета, содержащего сборку с недопустимой подписью, или при использовании пакета, версия которого задается с помощью параметра DateTime, возникает бесконечный цикл автоматического восстановления пакета (dotnet/project-system#1457).</span><span class="sxs-lookup"><span data-stu-id="05886-133">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="05886-134">Инструкции по решению:</span><span class="sxs-lookup"><span data-stu-id="05886-134">Workaround:</span></span>
<span data-ttu-id="05886-135">Сейчас для этой проблемы не существует обходного решения.</span><span class="sxs-lookup"><span data-stu-id="05886-135">There is no workaround at this time.</span></span>


## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="05886-136">Проблемы, исправленные в рамках NuGet 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="05886-136">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="05886-137">Проблемы, исправленные в NuGet 4.3 RTM, описаны в разделе [Заметки о выпуске NuGet 4.3 RTM](../release-notes/nuget-4.3-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="05886-137">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

<span data-ttu-id="05886-138">**Функция:**</span><span class="sxs-lookup"><span data-stu-id="05886-138">**Feature:**</span></span>

* <span data-ttu-id="05886-139">Поддержка упрощенной загрузки решения в сценариях PMC и пользовательского интерфейса PM NuGet — [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="05886-139">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

* <span data-ttu-id="05886-140">Целевой объект pack MSBuild должен иметь общедоступный обработчик для запуска целевых объектов пользователя перед собой — [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="05886-140">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

* <span data-ttu-id="05886-141">Функция: добавление параметра dependencyVersion в установку NuGet — [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="05886-141">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

* <span data-ttu-id="05886-142">uap10.0.TODO.0 должен соответствовать .NET Standard 2.0 для NuGet — [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="05886-142">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

* <span data-ttu-id="05886-143">Поддержка SKU Visual Studio Build Tools с помощью msbuild /t:restore — [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="05886-143">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

* <span data-ttu-id="05886-144">Во время восстановления выдается ошибка, если поддержка .NET 4.6.1 для .NET Standard 2.0 требуется, но не установлена — [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="05886-144">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

* <span data-ttu-id="05886-145">Клиентский пользовательский интерфейс для резервирования префикса идентификатора пакета — [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="05886-145">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

* <span data-ttu-id="05886-146">Предоставление локализованных компонентов NuGet для поддержки локализации dotnet.exe — [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="05886-146">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

<span data-ttu-id="05886-147">**Ошибка:**</span><span class="sxs-lookup"><span data-stu-id="05886-147">**Bug:**</span></span>

* <span data-ttu-id="05886-148">Разный регистр в путях проекта может привести к потере PackageReferences во время восстановления — [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="05886-148">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

* <span data-ttu-id="05886-149">Перемещение кодов ошибок с номерами предупреждений в диапазон ошибок — [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="05886-149">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

* <span data-ttu-id="05886-150">Вводящая в заблуждение ошибка, когда неизвестно, совместима ли версия .NET Standard с целевой платформой — [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="05886-150">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

* <span data-ttu-id="05886-151">Файлы теста с вносящими путаницу лицензиями — [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="05886-151">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

* <span data-ttu-id="05886-152">Отсутствующие заголовки лицензии в шаблонах тестов EndToEnd — [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="05886-152">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

* <span data-ttu-id="05886-153">Операция восстановления packages.config показывает ошибки как NU1000 — [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="05886-153">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

* <span data-ttu-id="05886-154">Команда nuget.exe install должна иметь DisableParallelProcessing в Mono — [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="05886-154">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

* <span data-ttu-id="05886-155">Команда nuget.exe install отключает кэширование неправильно — [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="05886-155">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

* <span data-ttu-id="05886-156">VS: если запустить команду восстановления для packages.config при отключенном восстановлении, отображается неправильное сообщение — [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="05886-156">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

* <span data-ttu-id="05886-157">VS: если запустить команду восстановления при отключенном восстановлении, отображается вносящее путаницу сообщение — [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="05886-157">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

* <span data-ttu-id="05886-158">GetRestoreDotnetCliToolsTask завершается со сбоем при отсутствии метаданных версии — [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="05886-158">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

* <span data-ttu-id="05886-159">Команда dotnet add package может очистить пустые строки из файла CSPROJ — [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="05886-159">dotnet add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

* <span data-ttu-id="05886-160">Исходные имена параметров учетных данных в NuGet.Config чувствительны к регистру — [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="05886-160">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

* <span data-ttu-id="05886-161">Включение GeneratePackageOnBuild привело к удалению всего моего журнала пакетов — [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="05886-161">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

* <span data-ttu-id="05886-162">Команда restore не восстанавливает пакеты mono.cecil и semver, но все остальные пакеты восстанавливаются.</span><span class="sxs-lookup"><span data-stu-id="05886-162">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="05886-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="05886-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

* <span data-ttu-id="05886-164">Ошибки и предупреждения — ошибка при недоступном источнике.</span><span class="sxs-lookup"><span data-stu-id="05886-164">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="05886-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="05886-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

* <span data-ttu-id="05886-166">[DesignConsistency] Текст о состоянии установки NuGet выглядит неправильно при темной теме.</span><span class="sxs-lookup"><span data-stu-id="05886-166">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="05886-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="05886-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

* <span data-ttu-id="05886-168">При обновлении пакетов на уровне решения создаются действия обновления/установки для всех проектов — [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="05886-168">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

* <span data-ttu-id="05886-169">Команда dotnet pack работает по-разному в зависимости от того, используется ли TargetFramework или TargetFrameworks — [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="05886-169">dotnet pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

* <span data-ttu-id="05886-170">Включенные библиотеки DLL в папке Tools вызывают предупреждения — [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="05886-170">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

* <span data-ttu-id="05886-171">NuGet.ContentModel использует слишком много памяти для операций со строками — [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="05886-171">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

* <span data-ttu-id="05886-172">RuntimeEnvironmentHelper.IsLinux возвращает значение true для OSX — [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="05886-172">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

* <span data-ttu-id="05886-173">Команда "dotnet pack" помещает NUSPEC-файл в obj вместо obj\Debug — [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="05886-173">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

* <span data-ttu-id="05886-174">Крайне медленное обновление пакетов в NuGet — [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="05886-174">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

* <span data-ttu-id="05886-175">CPS не синхронизируется с операцией восстановления для больших решений, где не включено упрощенное восстановление решения (LSL) — [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="05886-175">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

* <span data-ttu-id="05886-176">SemVer 2.0 — пакет NuGet с указанной версией игнорирует метаданные (3.5.0-rtm-1938) — [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="05886-176">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

* <span data-ttu-id="05886-177">Команда "install package" с номером версии и флагом ExcludeVersion в NuGet.exe (3+) не обновляет пакет до более новой версии — [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="05886-177">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

* <span data-ttu-id="05886-178">Операция восстановления Project.json должна выдавать предупреждение, когда пакеты верхнего уровня нарушают ограничения — [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="05886-178">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

* <span data-ttu-id="05886-179">Параметр -ConfigFile не задает пользовательскую конфигурацию в команде install — [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="05886-179">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

* <span data-ttu-id="05886-180">Команда nuget.exe install не учитывает параметр "-DisableParallelProcessing" — [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="05886-180">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

* <span data-ttu-id="05886-181">Отключенные источники продолжают использоваться DotNet.exe или msbuild.exe — [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="05886-181">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

* <span data-ttu-id="05886-182">Исправьте зависания в сценарии LSL — [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="05886-182">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

<span data-ttu-id="05886-183">**Запрос на изменение структуры:**</span><span class="sxs-lookup"><span data-stu-id="05886-183">**DCR:**</span></span>

* <span data-ttu-id="05886-184">Поддержка TargetFramework для nuget.exe install — [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="05886-184">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

* <span data-ttu-id="05886-185">Добавление других строк UserAgent для задачи msbuild (netcore или классический msbuild) — [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="05886-185">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

* <span data-ttu-id="05886-186">PackagePathResolver.GetPackageDirectoryName должен быть виртуальным — [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="05886-186">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

* <span data-ttu-id="05886-187">[DesignConsistency] Вводящее в заблуждение сообщение при добавлении пакета NuGet — [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="05886-187">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

* <span data-ttu-id="05886-188">[Предупреждения и ошибки] NoWarn не переходит транзитивно по одноранговым ссылкам — [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="05886-188">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

* <span data-ttu-id="05886-189">Упрощенная загрузка решения: общее ядро для пользовательского интерфейса PM, PMC и векторов инициализации* — [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="05886-189">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs* - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

* <span data-ttu-id="05886-190">Упрощенная загрузка решения: поддержка PMC — [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="05886-190">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

* <span data-ttu-id="05886-191">Добавление поддержки для предварительного восстановления целевого объекта MSBuild, который активирует Visual Studio — [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="05886-191">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

* <span data-ttu-id="05886-192">Добавление общедоступного целевого объекта в NuGet.targets, на который можно сослаться с помощью BeforeTargets — [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="05886-192">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

* <span data-ttu-id="05886-193">Целевому объекту pack не удается правильно создать contentFiles с действиями сборки — [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="05886-193">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

* <span data-ttu-id="05886-194">RestoreOperationLogger.Do блокирует потоки пула потоков — [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="05886-194">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

<span data-ttu-id="05886-195">**Документы:**</span><span class="sxs-lookup"><span data-stu-id="05886-195">**Docs:**</span></span>

* <span data-ttu-id="05886-196">Документация для флагов DependencyVersion и Framework команды Install — [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="05886-196">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

* <span data-ttu-id="05886-197">Обновление документации по предупреждениям и ошибкам NuGet — [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="05886-197">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="link-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="05886-198">Ссылка на проблемы GitHub, исправленные в версии 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="05886-198">Link to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="05886-199">Список проблем 1</span><span class="sxs-lookup"><span data-stu-id="05886-199">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="05886-200">Список проблем 2</span><span class="sxs-lookup"><span data-stu-id="05886-200">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="05886-201">Список проблем 3</span><span class="sxs-lookup"><span data-stu-id="05886-201">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
