---
title: Заметки о выпуске версии NuGet 4.4 RTM
description: Заметки о выпуске для NuGet 4.3 RTM, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 9ea11ad5476b02940b171fdc69ac0bf56598418d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548418"
---
# <a name="nuget-44-rtm-release-notes"></a><span data-ttu-id="493a4-103">Заметки о выпуске версии NuGet 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="493a4-103">NuGet 4.4 RTM Release Notes</span></span>

<span data-ttu-id="493a4-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) включает в себя NuGet 4.4 RTM.</span><span class="sxs-lookup"><span data-stu-id="493a4-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="known-issues"></a><span data-ttu-id="493a4-105">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="493a4-105">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="493a4-106">Проблемы с .NET Standard 2.0, связанные с .NET Framework и NuGet</span><span class="sxs-lookup"><span data-stu-id="493a4-106">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="493a4-107">Платформа .NET Standard и ее инструментарий были разработаны таким образом, чтобы проекты, предназначенные для .NET Framework 4.6.1, могли использовать пакеты NuGet и проекты, предназначенные для .NET Standard 2.0 или более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="493a4-107">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="493a4-108">[В этом документе](https://github.com/dotnet/standard/issues/481) кратко описаны проблемы, связанные с таким сценарием, план их решения, а также обходные пути, которые можно применить в текущем состоянии.</span><span class="sxs-lookup"><span data-stu-id="493a4-108">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="493a4-109">При использовании консоли диспетчера пакетов клавиша ВВОД может не работать</span><span class="sxs-lookup"><span data-stu-id="493a4-109">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="493a4-110">Проблеми</span><span class="sxs-lookup"><span data-stu-id="493a4-110">Issue</span></span>

<span data-ttu-id="493a4-111">Периодически клавиша ВВОД не работает в консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="493a4-111">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="493a4-112">В этом случае проверьте ход исправления и укажите дополнительные сведения для воспроизведения ошибки.</span><span class="sxs-lookup"><span data-stu-id="493a4-112">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="493a4-113">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="493a4-113">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="493a4-114">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="493a4-114">Workaround</span></span>

<span data-ttu-id="493a4-115">Перезапустите Visual Studio и откройте консоль управления пакетами перед тем, как открыть решение.</span><span class="sxs-lookup"><span data-stu-id="493a4-115">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="493a4-116">Кроме того, попробуйте удалить файл `project.lock.json` и выполнить восстановление еще раз.</span><span class="sxs-lookup"><span data-stu-id="493a4-116">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="493a4-117">Вы не можете просмотреть, добавить или обновить DotNetCLITools с помощью диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="493a4-117">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="493a4-118">Проблеми</span><span class="sxs-lookup"><span data-stu-id="493a4-118">Issue</span></span>

<span data-ttu-id="493a4-119">Диспетчер пакетов NuGet не отображается и не позволяет добавить или обновить DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="493a4-119">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="493a4-120">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="493a4-120">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="493a4-121">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="493a4-121">Workaround</span></span>

<span data-ttu-id="493a4-122">DotNetCLIToolReferences нужно изменить вручную в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="493a4-122">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="493a4-123">Изменение требуемой версии .NET Framework может привести к частичному отсутствию данных функции IntelliSense</span><span class="sxs-lookup"><span data-stu-id="493a4-123">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="493a4-124">Проблеми</span><span class="sxs-lookup"><span data-stu-id="493a4-124">Issue</span></span>

<span data-ttu-id="493a4-125">Если изменить требуемую версию .NET Framework в Visual Studio, вы можете получить неполные данные функции IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="493a4-125">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="493a4-126">Это происходит, если использовать PackageReferences в качестве формата диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="493a4-126">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="493a4-127">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="493a4-127">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="493a4-128">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="493a4-128">Workaround</span></span>

<span data-ttu-id="493a4-129">Выполните восстановление вручную.</span><span class="sxs-lookup"><span data-stu-id="493a4-129">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="493a4-130">Пакет в проекте .NET Core, который содержит сборку с недопустимой подписью, может инициировать бесконечный цикл восстановления.</span><span class="sxs-lookup"><span data-stu-id="493a4-130">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="493a4-131">Проблеми</span><span class="sxs-lookup"><span data-stu-id="493a4-131">Issue</span></span>

<span data-ttu-id="493a4-132">Иногда при использовании пакета, содержащего сборку с недопустимой подписью, или при использовании пакета, версия которого задается с помощью параметра DateTime, возникает бесконечный цикл автоматического восстановления пакета (dotnet/project-system#1457).</span><span class="sxs-lookup"><span data-stu-id="493a4-132">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="493a4-133">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="493a4-133">Workaround</span></span>

<span data-ttu-id="493a4-134">Сейчас для этой проблемы не существует обходного решения.</span><span class="sxs-lookup"><span data-stu-id="493a4-134">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="493a4-135">Проблемы, исправленные в рамках NuGet 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="493a4-135">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="493a4-136">Проблемы, исправленные в NuGet 4.3 RTM, описаны в разделе [Заметки о выпуске NuGet 4.3 RTM](../release-notes/nuget-4.3-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="493a4-136">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="493a4-137">Функции</span><span class="sxs-lookup"><span data-stu-id="493a4-137">Features</span></span>

- <span data-ttu-id="493a4-138">Поддержка упрощенной загрузки решения в сценариях PMC и пользовательского интерфейса PM NuGet — [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="493a4-138">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="493a4-139">Целевой объект pack MSBuild должен иметь общедоступный обработчик для запуска целевых объектов пользователя перед собой — [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="493a4-139">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="493a4-140">Функция: добавление параметра dependencyVersion в установку NuGet — [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="493a4-140">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="493a4-141">uap10.0.TODO.0 должен соответствовать .NET Standard 2.0 для NuGet — [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="493a4-141">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="493a4-142">Поддержка SKU Visual Studio Build Tools с помощью msbuild /t:restore — [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="493a4-142">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="493a4-143">Во время восстановления выдается ошибка, если поддержка .NET 4.6.1 для .NET Standard 2.0 требуется, но не установлена — [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="493a4-143">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="493a4-144">Клиентский пользовательский интерфейс для резервирования префикса идентификатора пакета — [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="493a4-144">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="493a4-145">Предоставление локализованных компонентов NuGet для поддержки локализации dotnet.exe — [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="493a4-145">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="493a4-146">Ошибки</span><span class="sxs-lookup"><span data-stu-id="493a4-146">Bugs</span></span>

- <span data-ttu-id="493a4-147">Разный регистр в путях проекта может привести к потере PackageReferences во время восстановления — [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="493a4-147">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="493a4-148">Перемещение кодов ошибок с номерами предупреждений в диапазон ошибок — [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="493a4-148">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="493a4-149">Вводящая в заблуждение ошибка, когда неизвестно, совместима ли версия .NET Standard с целевой платформой — [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="493a4-149">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="493a4-150">Файлы теста с вносящими путаницу лицензиями — [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="493a4-150">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="493a4-151">Отсутствующие заголовки лицензии в шаблонах тестов EndToEnd — [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="493a4-151">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="493a4-152">Операция восстановления packages.config показывает ошибки как NU1000 — [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="493a4-152">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="493a4-153">Команда nuget.exe install должна иметь DisableParallelProcessing в Mono — [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="493a4-153">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="493a4-154">Команда nuget.exe install отключает кэширование неправильно — [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="493a4-154">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="493a4-155">VS: если запустить команду восстановления для packages.config при отключенном восстановлении, отображается неправильное сообщение — [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="493a4-155">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="493a4-156">VS: если запустить команду восстановления при отключенном восстановлении, отображается вносящее путаницу сообщение — [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="493a4-156">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="493a4-157">GetRestoreDotnetCliToolsTask завершается со сбоем при отсутствии метаданных версии — [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="493a4-157">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="493a4-158">dotnet</span><span class="sxs-lookup"><span data-stu-id="493a4-158">dotnet</span></span>
  - <span data-ttu-id="493a4-159">Команда dotnetcore add package может очистить пустые строки из файла CSPROJ — [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="493a4-159">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="493a4-160">Исходные имена параметров учетных данных в NuGet.Config чувствительны к регистру — [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="493a4-160">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="493a4-161">Включение GeneratePackageOnBuild привело к удалению всего моего журнала пакетов — [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="493a4-161">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="493a4-162">Команда restore не восстанавливает пакеты mono.cecil и semver, но все остальные пакеты восстанавливаются.</span><span class="sxs-lookup"><span data-stu-id="493a4-162">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="493a4-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="493a4-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="493a4-164">Ошибки и предупреждения — ошибка при недоступном источнике.</span><span class="sxs-lookup"><span data-stu-id="493a4-164">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="493a4-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="493a4-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="493a4-166">[DesignConsistency] Текст о состоянии установки NuGet выглядит неправильно при темной теме.</span><span class="sxs-lookup"><span data-stu-id="493a4-166">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="493a4-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="493a4-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="493a4-168">При обновлении пакетов на уровне решения создаются действия обновления/установки для всех проектов — [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="493a4-168">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="493a4-169">dotnet</span><span class="sxs-lookup"><span data-stu-id="493a4-169">dotnet</span></span>
  - <span data-ttu-id="493a4-170">Команда dotnetcore pack работает по-разному в зависимости от того, используется ли TargetFramework или TargetFrameworks — [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="493a4-170">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="493a4-171">Включенные библиотеки DLL в папке Tools вызывают предупреждения — [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="493a4-171">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="493a4-172">NuGet.ContentModel использует слишком много памяти для операций со строками — [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="493a4-172">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="493a4-173">RuntimeEnvironmentHelper.IsLinux возвращает значение true для OSX — [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="493a4-173">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="493a4-174">Команда "dotnet pack" помещает NUSPEC-файл в obj вместо obj\Debug — [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="493a4-174">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="493a4-175">Крайне медленное обновление пакетов в NuGet — [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="493a4-175">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="493a4-176">CPS не синхронизируется с операцией восстановления для больших решений, где не включено упрощенное восстановление решения (LSL) — [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="493a4-176">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="493a4-177">SemVer 2.0 — пакет NuGet с указанной версией игнорирует метаданные (3.5.0-rtm-1938) — [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="493a4-177">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="493a4-178">Команда "install package" с номером версии и флагом ExcludeVersion в NuGet.exe (3+) не обновляет пакет до более новой версии — [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="493a4-178">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="493a4-179">Операция восстановления Project.json должна выдавать предупреждение, когда пакеты верхнего уровня нарушают ограничения — [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="493a4-179">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="493a4-180">Параметр -ConfigFile не задает пользовательскую конфигурацию в команде install — [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="493a4-180">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="493a4-181">Команда nuget.exe install не учитывает параметр "-DisableParallelProcessing" — [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="493a4-181">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="493a4-182">Отключенные источники продолжают использоваться DotNet.exe или msbuild.exe — [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="493a4-182">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="493a4-183">Исправьте зависания в сценарии LSL — [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="493a4-183">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="493a4-184">Запросы на изменение структуры</span><span class="sxs-lookup"><span data-stu-id="493a4-184">DCRs</span></span>

- <span data-ttu-id="493a4-185">Поддержка TargetFramework для nuget.exe install — [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="493a4-185">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="493a4-186">Добавление других строк UserAgent для задачи msbuild (netcore или классический msbuild) — [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="493a4-186">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="493a4-187">PackagePathResolver.GetPackageDirectoryName должен быть виртуальным — [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="493a4-187">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="493a4-188">[DesignConsistency] Вводящее в заблуждение сообщение при добавлении пакета NuGet — [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="493a4-188">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="493a4-189">[Предупреждения и ошибки] NoWarn не переходит транзитивно по одноранговым ссылкам — [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="493a4-189">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="493a4-190">Упрощенная загрузка решения: общее ядро для пользовательского интерфейса PM, PMC и векторов инициализации — [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="493a4-190">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="493a4-191">Упрощенная загрузка решения: поддержка PMC — [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="493a4-191">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="493a4-192">Добавление поддержки для предварительного восстановления целевого объекта MSBuild, который активирует Visual Studio — [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="493a4-192">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="493a4-193">Добавление общедоступного целевого объекта в NuGet.targets, на который можно сослаться с помощью BeforeTargets — [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="493a4-193">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="493a4-194">Целевому объекту pack не удается правильно создать contentFiles с действиями сборки — [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="493a4-194">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="493a4-195">RestoreOperationLogger.Do блокирует потоки пула потоков — [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="493a4-195">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="493a4-196">Docs</span><span class="sxs-lookup"><span data-stu-id="493a4-196">Docs</span></span>

- <span data-ttu-id="493a4-197">Документация для флагов DependencyVersion и Framework команды Install — [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="493a4-197">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="493a4-198">Обновление документации по предупреждениям и ошибкам NuGet — [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="493a4-198">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="493a4-199">Ссылки на проблемы GitHub, исправленные в версии 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="493a4-199">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="493a4-200">Список проблем 1</span><span class="sxs-lookup"><span data-stu-id="493a4-200">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="493a4-201">Список проблем 2</span><span class="sxs-lookup"><span data-stu-id="493a4-201">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="493a4-202">Список проблем 3</span><span class="sxs-lookup"><span data-stu-id="493a4-202">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
