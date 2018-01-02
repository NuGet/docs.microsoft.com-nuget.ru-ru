---
title: "Заметки о выпуске версии-кандидата NuGet 4.0 | Документы Майкрософт"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 906cc4dd-7948-4e86-a093-21df830ce8c3
description: "Заметки о выпуске для NuGet 4.0 RTM, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры."
keywords: "заметки о выпуске NuGet 4.0 RTM, исправления ошибок, известные проблемы, добавленные функции и запросы на изменение структуры"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2cdee8b736fa2c651da803be9a10a6114936134a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="40-rtm-release-notes"></a><span data-ttu-id="58f54-104">Заметки о выпуске версии 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="58f54-104">4.0 RTM Release Notes</span></span>

<span data-ttu-id="58f54-105">В состав [Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) входит версия NuGet 4.0, в которую добавлена поддержка платформы .NET Core, а также представлено множество исправлений, направленных на повышение качества и производительности.</span><span class="sxs-lookup"><span data-stu-id="58f54-105">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="58f54-106">Кроме того, в этой версии появился ряд усовершенствований, таких как поддержка формата PackageReference, использование команд NuGet в качестве целей MSBuild, восстановление пакетов в фоновом режиме и других.</span><span class="sxs-lookup"><span data-stu-id="58f54-106">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="58f54-107">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="58f54-107">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="58f54-108">Сбой восстановления NuGet может завершиться ошибкой, если в решении есть несколько проектов, ссылающихся на другой проект</span><span class="sxs-lookup"><span data-stu-id="58f54-108">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="58f54-109">Проблема.</span><span class="sxs-lookup"><span data-stu-id="58f54-109">Issue:</span></span>
<span data-ttu-id="58f54-110">Восстановление NuGet может не работать, если в решении есть проекты, которые ссылаются на один и тот же проект с разным регистром или с другими относительными путями.</span><span class="sxs-lookup"><span data-stu-id="58f54-110">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="58f54-111">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="58f54-111">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="58f54-112">Решение</span><span class="sxs-lookup"><span data-stu-id="58f54-112">Workaround:</span></span>
<span data-ttu-id="58f54-113">Исправьте регистр и относительные пути, чтобы они совпадали во всех ссылках на проект.</span><span class="sxs-lookup"><span data-stu-id="58f54-113">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="58f54-114">При использовании консоли диспетчера пакетов клавиша ВВОД может не работать</span><span class="sxs-lookup"><span data-stu-id="58f54-114">While using Package Manager Console, 'Enter' key may not work</span></span>
#### <a name="issue"></a><span data-ttu-id="58f54-115">Проблема.</span><span class="sxs-lookup"><span data-stu-id="58f54-115">Issue:</span></span>
<span data-ttu-id="58f54-116">Периодически клавиша ВВОД не работает в консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="58f54-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="58f54-117">В этом случае проверьте ход исправления и укажите дополнительные сведения для воспроизведения ошибки.</span><span class="sxs-lookup"><span data-stu-id="58f54-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="58f54-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="58f54-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="58f54-119">Решение</span><span class="sxs-lookup"><span data-stu-id="58f54-119">Workaround:</span></span>
<span data-ttu-id="58f54-120">Перезапустите Visual Studio и откройте консоль управления пакетами перед тем, как открыть решение.</span><span class="sxs-lookup"><span data-stu-id="58f54-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="58f54-121">Кроме того, попробуйте удалить файл `project.lock.json` и выполнить восстановление еще раз.</span><span class="sxs-lookup"><span data-stu-id="58f54-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="58f54-122">При использовании пакета, содержащего сборку с недопустимой подписью, в проектах .NET Core может возникнуть бесконечный цикл восстановления</span><span class="sxs-lookup"><span data-stu-id="58f54-122">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>
#### <a name="issue"></a><span data-ttu-id="58f54-123">Проблема.</span><span class="sxs-lookup"><span data-stu-id="58f54-123">Issue:</span></span>
<span data-ttu-id="58f54-124">Иногда при использовании пакета, содержащего сборку с недопустимой подписью, или если для версии пакета задан тикер DateTime, возникает бесконечный цикл автоматического восстановления пакета.</span><span class="sxs-lookup"><span data-stu-id="58f54-124">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="58f54-125">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="58f54-125">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="58f54-126">Решение</span><span class="sxs-lookup"><span data-stu-id="58f54-126">Workaround:</span></span>
<span data-ttu-id="58f54-127">Сейчас для этой проблемы не существует обходного решения.</span><span class="sxs-lookup"><span data-stu-id="58f54-127">There is no workaround at this time.</span></span>

### <a name="you-will-be-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="58f54-128">Невозможно просмотреть, добавить или обновить DotNetCLITools с помощью диспетчера пакетов Nuget</span><span class="sxs-lookup"><span data-stu-id="58f54-128">You will be unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>
#### <a name="issue"></a><span data-ttu-id="58f54-129">Проблема.</span><span class="sxs-lookup"><span data-stu-id="58f54-129">Issue:</span></span>
<span data-ttu-id="58f54-130">Диспетчер пакетов NuGet не отображается и не позволяет добавить или обновить DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="58f54-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="58f54-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="58f54-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

* #### <a name="workaround"></a><span data-ttu-id="58f54-132">Решение</span><span class="sxs-lookup"><span data-stu-id="58f54-132">Workaround:</span></span>
<span data-ttu-id="58f54-133">DotNetCLIToolReferences нужно изменить вручную в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="58f54-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="58f54-134">При установке свойства PackageId для проектов произойдет сбой восстановления NuGet</span><span class="sxs-lookup"><span data-stu-id="58f54-134">NuGet restore will fail when you set PackageId property for projects</span></span>
#### <a name="issue"></a><span data-ttu-id="58f54-135">Проблема.</span><span class="sxs-lookup"><span data-stu-id="58f54-135">Issue:</span></span>
<span data-ttu-id="58f54-136">Для проектов .NET Core восстановление NuGet в Visual Studio не связано со свойством PackageId проектов.</span><span class="sxs-lookup"><span data-stu-id="58f54-136">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="58f54-137">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="58f54-137">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="58f54-138">Решение</span><span class="sxs-lookup"><span data-stu-id="58f54-138">Workaround:</span></span>
<span data-ttu-id="58f54-139">Выполните восстановление с использованием командной строки.</span><span class="sxs-lookup"><span data-stu-id="58f54-139">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="58f54-140">Если в проекте нет папки obj, произойдет сбой восстановления пакета</span><span class="sxs-lookup"><span data-stu-id="58f54-140">When your project does not have 'obj' folder, package restore may fail</span></span>
#### <a name="issue"></a><span data-ttu-id="58f54-141">Проблема.</span><span class="sxs-lookup"><span data-stu-id="58f54-141">Issue:</span></span>
<span data-ttu-id="58f54-142">Visual Studio не удается восстановить PackageReferences, если папка obj удалена.</span><span class="sxs-lookup"><span data-stu-id="58f54-142">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="58f54-143">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="58f54-143">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="58f54-144">Решение</span><span class="sxs-lookup"><span data-stu-id="58f54-144">Workaround:</span></span>
<span data-ttu-id="58f54-145">Создайте папку obj вручную, и восстановление должно заработать.</span><span class="sxs-lookup"><span data-stu-id="58f54-145">Create 'obj' folder manually and the restore should work.</span></span> 

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="58f54-146">Обновление пакетов вручную с использованием Update-Package в консоли может завершиться ошибкой</span><span class="sxs-lookup"><span data-stu-id="58f54-146">Manually updating packages using Update-Package in console may fail</span></span>
#### <a name="issue"></a><span data-ttu-id="58f54-147">Проблема.</span><span class="sxs-lookup"><span data-stu-id="58f54-147">Issue:</span></span>
<span data-ttu-id="58f54-148">Использование Update-Package вручную в консоли работает только один раз для только что преобразованных проектов PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="58f54-148">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="58f54-149">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="58f54-149">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="58f54-150">Решение</span><span class="sxs-lookup"><span data-stu-id="58f54-150">Workaround:</span></span>
<span data-ttu-id="58f54-151">Сейчас для этой проблемы не существует обходного решения.</span><span class="sxs-lookup"><span data-stu-id="58f54-151">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="58f54-152">Изменение требуемой версии .NET Framework может привести к частичному отсутствию данных функции IntelliSense</span><span class="sxs-lookup"><span data-stu-id="58f54-152">Retargeting target framework version may lead to incomplete Intellisense</span></span>
#### <a name="issue"></a><span data-ttu-id="58f54-153">Проблема.</span><span class="sxs-lookup"><span data-stu-id="58f54-153">Issue:</span></span>
<span data-ttu-id="58f54-154">Если изменить требуемую версию .NET Framework в Visual Studio, вы можете получить неполные данные функции IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="58f54-154">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="58f54-155">Это происходит, если использовать PackageReferences в качестве формата диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="58f54-155">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="58f54-156">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="58f54-156">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="58f54-157">Решение</span><span class="sxs-lookup"><span data-stu-id="58f54-157">Workaround:</span></span>
<span data-ttu-id="58f54-158">Выполните восстановление вручную.</span><span class="sxs-lookup"><span data-stu-id="58f54-158">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="58f54-159">Операция `msbuild /t:restore` завершается ошибкой, если проект, предназначенный для .NET 4.6.1, ссылается на другой проект, предназначенный для .NET Standard</span><span class="sxs-lookup"><span data-stu-id="58f54-159">`msbuild /t:restore` fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="58f54-160">Проблема.</span><span class="sxs-lookup"><span data-stu-id="58f54-160">Issue:</span></span>
<span data-ttu-id="58f54-161">Операция MSBuild /t:restore завершается ошибкой, если проект на основе PackageReferenece, предназначенный для .NET 4.6.1, ссылается на другой проект на основе PackageReferenece, предназначенный для .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="58f54-161">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="58f54-162">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="58f54-162">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="58f54-163">Решение</span><span class="sxs-lookup"><span data-stu-id="58f54-163">Workaround:</span></span>
<span data-ttu-id="58f54-164">Сейчас для этой проблемы не существует обходного решения.</span><span class="sxs-lookup"><span data-stu-id="58f54-164">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="58f54-165">Проблемы, исправленные в рамках NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="58f54-165">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="58f54-166">Проблемы, исправленные в NuGet 4.0 RC, описаны в разделе [Заметки о выпуске NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="58f54-166">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

<span data-ttu-id="58f54-167">**Ошибка:**</span><span class="sxs-lookup"><span data-stu-id="58f54-167">**Bug:**</span></span>

* <span data-ttu-id="58f54-168">Восстановление NuGet в Visual Studio не связано со свойством PackageId проектов — [4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="58f54-168">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

* <span data-ttu-id="58f54-169">Ошибка NuGet ProjectSystemCache при добавлении пакета в пакет vsix — [4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="58f54-169">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

* <span data-ttu-id="58f54-170">Операция упаковки вызывает исключение при использовании IncludeSource в проекте с несколькими моникерами целевой платформы — [4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="58f54-170">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

* <span data-ttu-id="58f54-171">Работа VS 2017 RC3 завершается сбоем при использовании обновления из среды управления пакетами на уровне решения — [4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="58f54-171">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

* <span data-ttu-id="58f54-172">Не удается удалить вновь установленный пакет — [4435](https://github.com/NuGet/Home/issues/4435)</span><span class="sxs-lookup"><span data-stu-id="58f54-172">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

* <span data-ttu-id="58f54-173">При переносе в PackageRef наблюдается неожиданное поведение функции восстановления гибридных решений — [4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="58f54-173">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

* <span data-ttu-id="58f54-174">При выполнении построения вскоре после запуска операции NuGet (установка, обновление, восстановление) возможно зависание VS — [4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="58f54-174">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

* <span data-ttu-id="58f54-175">Зависание пользовательского интерфейса — взаимоблокировка при инициализации NuGet.SolutionRestoreManager.RestoreManagerPackage — [4371](https://github.com/NuGet/Home/issues/4371)</span><span class="sxs-lookup"><span data-stu-id="58f54-175">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

* <span data-ttu-id="58f54-176">Команда add package должна добавлять версию в качестве атрибута вместо элемента — [4325](https://github.com/NuGet/Home/issues/4325)</span><span class="sxs-lookup"><span data-stu-id="58f54-176">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

* <span data-ttu-id="58f54-177">dotnet restore foo.sln — сбой в случаях, когда конфигурации в SLN приводит к дублированию проектов в графе восстановления с разными конфигурациями — [4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="58f54-177">Dotnet Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

* <span data-ttu-id="58f54-178">Пакеты только с содержимым — [3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="58f54-178">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

* <span data-ttu-id="58f54-179">Отказ по умолчанию от параметра селектора формата пакета — [4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="58f54-179">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

* <span data-ttu-id="58f54-180">Производительность: CreateUAP_CSharp_VS.01.1. Время создания проекта Duration_TotalElapsedTime ухудшилось на 3153,570 мс (149,1 %).</span><span class="sxs-lookup"><span data-stu-id="58f54-180">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="58f54-181">Базовая версия 26129.02 — [4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="58f54-181">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

* <span data-ttu-id="58f54-182">Производительность: для решения ManagedLangs_CS_DDRIT.0300. Время повторного построения Duration_TotalElapsedTime ухудшилось на 1,5 с.</span><span class="sxs-lookup"><span data-stu-id="58f54-182">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="58f54-183">Базовая версия 26105 — [4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="58f54-183">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

* <span data-ttu-id="58f54-184">Сбой заявки в проектах с несколькими моникерами целевой платформы — [4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="58f54-184">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

* <span data-ttu-id="58f54-185">Производительность: WebForms_DDRIT.1200. Время закрытия решения VM_ImagesInMemory_Total_devenv ухудшилось на 3,000 значения счетчика (0,5 %).</span><span class="sxs-lookup"><span data-stu-id="58f54-185">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="58f54-186">Базовая версия 26123.04 — [4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="58f54-186">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

* <span data-ttu-id="58f54-187">vsfeedback — предупреждения упаковки при нацеливании на netcoreapp1.1 — [4397](https://github.com/NuGet/Home/issues/4397)</span><span class="sxs-lookup"><span data-stu-id="58f54-187">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

* <span data-ttu-id="58f54-188">Исключение PathTooLongException при попытке добавить пакет NuGet в пустое веб-приложение ASP.NET Core — [4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="58f54-188">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

* <span data-ttu-id="58f54-189">Упаковка выполняется слишком часто — команда dotnet pack завершается сбоем при наличии циклической зависимости в целевом графе зависимостей, включающем целевую операцию упаковки — [4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="58f54-189">Pack runs too often -- dotnet pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

* <span data-ttu-id="58f54-190">Упаковка выполняется слишком часто — при создании пакета NuGet не включаются все конфигурации — [4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="58f54-190">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

* <span data-ttu-id="58f54-191">Исключение NullReferenceException при добавлении nuget с packageref в проект C++ — [4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="58f54-191">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

* <span data-ttu-id="58f54-192">Специальные возможности: экранный диктор не воспроизводит название флажка, позволяющего выбрать проекты, в которые требуется установить пакет — [4366](https://github.com/NuGet/Home/issues/4366)</span><span class="sxs-lookup"><span data-stu-id="58f54-192">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

* <span data-ttu-id="58f54-193">NuGet VS17 периодически не может подключиться к веб-каналам VSO/VSTS — ошибка VS 365798 — [4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="58f54-193">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

* <span data-ttu-id="58f54-194">contentFiles выводит данные в неверное расположение, если PackagePath задает путь в виде "contentFiles" — [4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="58f54-194">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

* <span data-ttu-id="58f54-195">При упаковке целевого объекта добавляется свойство PackageVersion с VersionSuffix — [4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="58f54-195">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

* <span data-ttu-id="58f54-196">Не удается указать путь к пакету при использовании dotnet pack — [4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="58f54-196">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

* <span data-ttu-id="58f54-197">NuGet выводит серию предупреждений о повторяющихся операциях импорта во время восстановления — [4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="58f54-197">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

* <span data-ttu-id="58f54-198">Диалоговое окно для выбора формата диспетчера пакетов NuGet плохо выглядит при установке темной темы — [4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="58f54-198">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

* <span data-ttu-id="58f54-199">Сбой VS при восстановлении сборки — [4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="58f54-199">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

* <span data-ttu-id="58f54-200">Взаимоблокировка Visual Studio при добавлении моникера целевой платформы в targetframeworks, сохранении и последующем выполнении перестроения.</span><span class="sxs-lookup"><span data-stu-id="58f54-200">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="58f54-201">10 % времени — [4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="58f54-201">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

* <span data-ttu-id="58f54-202">nuget pack не выводит сообщение об успехе в случае успешной упаковки проекта — [4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="58f54-202">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

* <span data-ttu-id="58f54-203">PackTask завершается сбоем из-за того, что не удается найти System.IO.Compression 4.1 — [4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="58f54-203">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

* <span data-ttu-id="58f54-204">Упаковка выполняется слишком часто — PackTask часто завершается сбоем из-за конфликтов при доступе к файлу — [4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="58f54-204">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

* <span data-ttu-id="58f54-205">NuGet открывает окно вывода во время фонового восстановления — [4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="58f54-205">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

* <span data-ttu-id="58f54-206">Исключение ServiceProvider как потенциально опасного шаблона написания кода (может приводить к зависаниям) — [4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="58f54-206">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

* <span data-ttu-id="58f54-207">Производительность или зависание пользовательского интерфейса — повышение производительности считывания DownloadTimeoutStream — [4266](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="58f54-207">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

* <span data-ttu-id="58f54-208">Взаимоблокировка Visual Studio при попытке закрыть проект до завершения операции восстановления NuGet — [4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="58f54-208">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

* <span data-ttu-id="58f54-209">Проблемы с PackTask и упаковкой — `.nuspec` - [4250](https://github.com/NuGet/Home/issues/4250)</span><span class="sxs-lookup"><span data-stu-id="58f54-209">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

* <span data-ttu-id="58f54-210">[vsfeedback] Не удается разрешить пакеты nuget для нового проекта (требуется перезапуск Visual Studio) — [4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="58f54-210">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

* <span data-ttu-id="58f54-211">[vsfeedback] Раскрывающийся список "Версия", в котором отображаются доступные версии пакета, плохо синхронизируется с выбранным пакетом nuGet... — [4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="58f54-211">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

* <span data-ttu-id="58f54-212">Nuget.Client должен использовать CPS JoinableTaskFactory при взаимодействии с CPS для предотвращения взаимоблокировок — [4185](https://github.com/NuGet/Home/issues/4185)</span><span class="sxs-lookup"><span data-stu-id="58f54-212">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

* <span data-ttu-id="58f54-213">NuGet 3.5.0 не распаковывает `.targets` из пакета — [4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="58f54-213">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

* <span data-ttu-id="58f54-214">dotnet pack не поддерживает заголовок в `.csproj` - [4150](https://github.com/NuGet/Home/issues/4150)</span><span class="sxs-lookup"><span data-stu-id="58f54-214">dotnet pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

* <span data-ttu-id="58f54-215">Install-Package приводит к появлению диалогового окна ошибки в версии VS2017 RC — [4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="58f54-215">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

* <span data-ttu-id="58f54-216">Не работает обновление пакета для проекта .Net Core, поскольку пользовательский интерфейс не получает обновление CPS из назначения.</span><span class="sxs-lookup"><span data-stu-id="58f54-216">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="58f54-217"> - [4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="58f54-217"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

* <span data-ttu-id="58f54-218">Предупреждение об улучшении неразрешенных ссылок — [3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="58f54-218">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

* <span data-ttu-id="58f54-219">dotnet pack — ProjectReference теряет сведения о версии — [3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="58f54-219">dotnet pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

* <span data-ttu-id="58f54-220">Общее ухудшение времени создания и повторного построения проекта приложения для универсальной платформы Windows — [3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="58f54-220">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

* <span data-ttu-id="58f54-221">Сообщение об успешном восстановлении отображается даже при возникновении ошибок в процессе восстановления.</span><span class="sxs-lookup"><span data-stu-id="58f54-221">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="58f54-222"> - [3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="58f54-222"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

* <span data-ttu-id="58f54-223">Повторная публикация Nuget.CommandLine 3.4.4 на веб-сайте Nuget.org — [2931](https://github.com/NuGet/Home/issues/2931)</span><span class="sxs-lookup"><span data-stu-id="58f54-223">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

* <span data-ttu-id="58f54-224">При переносе проекты изменяются с `project.json` на `.csproj` — восстановление завершается сбоем — [4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="58f54-224">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

* <span data-ttu-id="58f54-225">Сбой при восстановлении только что созданного тестового проекта xunit — [4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="58f54-225">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

* <span data-ttu-id="58f54-226">При открытии проектов Core возможно зависание пользовательского интерфейса — [4269](https://github.com/NuGet/Home/issues/4269)</span><span class="sxs-lookup"><span data-stu-id="58f54-226">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

* <span data-ttu-id="58f54-227">Исправление файла целевых объектов для задач построения — [4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="58f54-227">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

* <span data-ttu-id="58f54-228">Список ошибок содержит ошибку после построения решения, которое выгружает указанный по ссылке проект — [4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="58f54-228">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

* <span data-ttu-id="58f54-229">MSB4057: целевой объект "_GenerateRestoreGraphProjectEntry" не существует в проекте.</span><span class="sxs-lookup"><span data-stu-id="58f54-229">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="58f54-230"> - [4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="58f54-230"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

* <span data-ttu-id="58f54-231">vsfeedback: пользовательский интерфейс диспетчера nuget для решения завершает работу со сбоем при выборе всех проектов — [4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="58f54-231">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

* <span data-ttu-id="58f54-232">nuget.exe msbuildpath завершается сбоем при наличии конечного знака косой черты — [4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="58f54-232">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

* <span data-ttu-id="58f54-233">vsfeedback: операция восстановления NuGet выдает несколько предупреждений о ссылке на проект для проекта LinqToTwitter — [4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="58f54-233">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

* <span data-ttu-id="58f54-234">При упаковке из `.csproj` не включается атрибут minClientVersion — [4135](https://github.com/NuGet/Home/issues/4135)</span><span class="sxs-lookup"><span data-stu-id="58f54-234">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

* <span data-ttu-id="58f54-235">NuGet.Build.Tasks.Pack.dll поставляется с отложенной подписью в VS2017 (d15rel 26014.00) — [4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="58f54-235">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

* <span data-ttu-id="58f54-236">VSFeedback: восстановление завершается сбоем для проекта VS 2015, созданного с помощью CMake 3.7.1 — [4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="58f54-236">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

* <span data-ttu-id="58f54-237">VSFeedback: ошибки восстановления могут скрывать более полные сообщения об ошибках, которые могут выдаваться при построении — [4113](https://github.com/NuGet/Home/issues/4113)</span><span class="sxs-lookup"><span data-stu-id="58f54-237">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

* <span data-ttu-id="58f54-238">[VSFeedback] Ошибка при восстановлении пакетов NuGet для проекта веб-сайта: значение не может быть null.</span><span class="sxs-lookup"><span data-stu-id="58f54-238">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="58f54-239"> - [4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="58f54-239"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

* <span data-ttu-id="58f54-240">Операция переноса вызывает исключение ссылки на объект в NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker — [4067](https://github.com/NuGet/Home/issues/4067)</span><span class="sxs-lookup"><span data-stu-id="58f54-240">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

* <span data-ttu-id="58f54-241">Команда dotnet pack должна выполнять упаковку средств с версиями, для которых было выполнено построение пакета — [4063](https://github.com/NuGet/Home/issues/4063)</span><span class="sxs-lookup"><span data-stu-id="58f54-241">dotnet pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

* <span data-ttu-id="58f54-242">Новая операция фонового восстановления записывает в строку состояния значение в миллисекундах, тогда как восстановление занимает секунды — [4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="58f54-242">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

* <span data-ttu-id="58f54-243">Опечатка в сообщении о сбое при разрешении всех ссылок проекта —[4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="58f54-243">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

* <span data-ttu-id="58f54-244">Включение рабочих процессов PCM в сценариях ссылок на пакет —[4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="58f54-244">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

* <span data-ttu-id="58f54-245">Не удается найти установленные пакеты в пользовательском интерфейсе диспетчера пакетов — [4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="58f54-245">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

* <span data-ttu-id="58f54-246">dotnet pack завершается сбоем при пустом PackagePath —[3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="58f54-246">dotnet pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

* <span data-ttu-id="58f54-247">Задача восстановления завершается сбоем в многопользовательском сценарии — [3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="58f54-247">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

* <span data-ttu-id="58f54-248">Не удается изменить тип содержимого при упаковке с использованием задачи упаковки NuGet — [3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="58f54-248">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

* <span data-ttu-id="58f54-249">Неверная копия по умолчанию ContentFiles для MsBuild /t:pack — [3894](https://github.com/NuGet/Home/issues/3894)</span><span class="sxs-lookup"><span data-stu-id="58f54-249">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

* <span data-ttu-id="58f54-250">При восстановлении установки пакета в журналах дублируется сообщение о восстановлении пакетов — [3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="58f54-250">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

* <span data-ttu-id="58f54-251">Снятие защитных функций — восстановление раздела сред выполнения должно применяться только к текущему проекту — [3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="58f54-251">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

* <span data-ttu-id="58f54-252">Задача упаковки помещает файлы содержимого одновременно в "content/" и "contentFiles/" — [3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="58f54-252">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

* <span data-ttu-id="58f54-253">dotnet pack3 выполняет дополнительное разделение тегов — [3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="58f54-253">dotnet pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

* <span data-ttu-id="58f54-254">dotnet pack: упаковка проектов с использованием ссылок на проекты приводит к дублированию предупреждения об импорте — [3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="58f54-254">dotnet pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

* <span data-ttu-id="58f54-255">Не всегда отображается журнал восстановления в VS — [3633](https://github.com/NuGet/Home/issues/3633)</span><span class="sxs-lookup"><span data-stu-id="58f54-255">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

* <span data-ttu-id="58f54-256">В тексте справки по локальным компонентам nuget по-прежнему упоминается кэш пакетов — [3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="58f54-256">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

* <span data-ttu-id="58f54-257">Restore3 связывает PackageReferences с TargetFrameworks.</span><span class="sxs-lookup"><span data-stu-id="58f54-257">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="58f54-258"> - [3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="58f54-258"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

* <span data-ttu-id="58f54-259">Nuget выбирает неожиданную версию MSBuild в командной строке разработчика VS "15",</span><span class="sxs-lookup"><span data-stu-id="58f54-259">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="58f54-260">предварительная версия 4 — [3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="58f54-260">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

* <span data-ttu-id="58f54-261">Запись файлов целевых объектов или свойств при завершившемся сбоем восстановлении — [3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="58f54-261">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

* <span data-ttu-id="58f54-262">NuGet во время восстановления не учитывает те же оболочки совместимости, что и MSBuild при выполнении в командной строке VS 15 — [3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="58f54-262">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

* <span data-ttu-id="58f54-263">Повторное включение PackFromProjectWithDevelopmentDependencySet для VS15 — [3272](https://github.com/NuGet/Home/issues/3272)</span><span class="sxs-lookup"><span data-stu-id="58f54-263">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

* <span data-ttu-id="58f54-264">Проблемы с Blend при работе с NuGet — [4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="58f54-264">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

* <span data-ttu-id="58f54-265">Интеграция версии 4.0.0.2067 в репозитории интерфейса командной строки и SDK для поставки вместе с RC2 — [4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="58f54-265">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

* <span data-ttu-id="58f54-266">VS зависает при создании нового консольного приложения Core, закрытии решения, а также открытии и закрытии решения — [4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="58f54-266">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

* <span data-ttu-id="58f54-267">Зависание при открытии проекта d15prerel.25916.01 — [3982](https://github.com/NuGet/Home/issues/3982)</span><span class="sxs-lookup"><span data-stu-id="58f54-267">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

* <span data-ttu-id="58f54-268">Исправление сообщения в справке и документации по dotnet и локальным компонентам nuget.exe — [3919](https://github.com/NuGet/Home/issues/3919)</span><span class="sxs-lookup"><span data-stu-id="58f54-268">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

* <span data-ttu-id="58f54-269">Проверка PackTask на наличие проблем, связанных с начальным или конечным пробелом — [3906](https://github.com/NuGet/Home/issues/3906)</span><span class="sxs-lookup"><span data-stu-id="58f54-269">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

* <span data-ttu-id="58f54-270">dotnet pack выполняет упаковку из obj, а не из bin — [3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="58f54-270">dotnet pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

* <span data-ttu-id="58f54-271">dotnet pack всегда присваивает ProjectReference версию 1.0.0 — [3874](https://github.com/NuGet/Home/issues/3874)</span><span class="sxs-lookup"><span data-stu-id="58f54-271">dotnet pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

* <span data-ttu-id="58f54-272">dotnet pack завершается сбоем со ссылками на проект и <TargetFramework> - [3865](https://github.com/NuGet/Home/issues/3865)</span><span class="sxs-lookup"><span data-stu-id="58f54-272">dotnet pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

* <span data-ttu-id="58f54-273">Исключение LockRecursionException в ProjectSystemCache.TryGetProjectNameByShortName — [3861](https://github.com/NuGet/Home/issues/3861)</span><span class="sxs-lookup"><span data-stu-id="58f54-273">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

* <span data-ttu-id="58f54-274">Обрезка пробелов из свойств MSBuild — [3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="58f54-274">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

* <span data-ttu-id="58f54-275">Объединение двух событий проекта, возникающих при загрузке проекта — [3759](https://github.com/NuGet/Home/issues/3759)</span><span class="sxs-lookup"><span data-stu-id="58f54-275">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

* <span data-ttu-id="58f54-276">Библиотеки P2P в файле `project.assets.json` файл имеют неправильную версию — [3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="58f54-276">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

* <span data-ttu-id="58f54-277">Восстановление завершается сбоем из-за отсутствия ответа веб-канала и недоступности пакета — [3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="58f54-277">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

* <span data-ttu-id="58f54-278">nuget.exe может зависнуть при большом объеме выходных данных ошибки MSBuild — [3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="58f54-278">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

* <span data-ttu-id="58f54-279">Задача восстановления при построении для Blend завершается сбоем в первый раз и успешно выполняется во второй (исправлен сценарий для VS) — [2121](https://github.com/NuGet/Home/issues/2121)</span><span class="sxs-lookup"><span data-stu-id="58f54-279">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

<span data-ttu-id="58f54-280">**Запрос на изменение структуры:**</span><span class="sxs-lookup"><span data-stu-id="58f54-280">**DCR:**</span></span>

* <span data-ttu-id="58f54-281">перенос vsix из v2 vsix в v3 vsix — [4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="58f54-281">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

* <span data-ttu-id="58f54-282">NuGet должен предусматривать механизм получения пути к файлу блокировки в MSBuild — [3351](https://github.com/NuGet/Home/issues/3351)</span><span class="sxs-lookup"><span data-stu-id="58f54-282">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

* <span data-ttu-id="58f54-283">Добавление ресурсов построения в проверку совместимости моникера целевой платформы и файл ресурсов — [3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="58f54-283">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

* <span data-ttu-id="58f54-284">Определение нового объекта ProjectCapability "Pack" в целевых объектах упаковки для реализации связанных с пакетом возможностей — [4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="58f54-284">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

* <span data-ttu-id="58f54-285">Запуск пакета в качестве целевого объекта после построения с условием на основе свойства MSBuild "GeneratePackageOnBuild" — [4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="58f54-285">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

* <span data-ttu-id="58f54-286">Использование свойства NuGet RestoreProjectStyle для создания отдельных проектов NuGet — [4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="58f54-286">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

* <span data-ttu-id="58f54-287">Адаптивное восстановление для изменений переходных ссылок проекта — [4076](https://github.com/NuGet/Home/issues/4076)</span><span class="sxs-lookup"><span data-stu-id="58f54-287">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

* <span data-ttu-id="58f54-288">Добавление свойств NuGet в целевой файл для проектов, не предназначенных для универсальной платформы Windows — [4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="58f54-288">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

* <span data-ttu-id="58f54-289">Поддержка TargetPlatformVersion для универсальной платформы Windows — [3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="58f54-289">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

* <span data-ttu-id="58f54-290">Передача метаданных ссылок проекта в систему проектов NuGet — [3922](https://github.com/NuGet/Home/issues/3922)</span><span class="sxs-lookup"><span data-stu-id="58f54-290">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

* <span data-ttu-id="58f54-291">Добавление пользовательского интерфейса для режима упаковки — [3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="58f54-291">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

* <span data-ttu-id="58f54-292">Для прежних версий `.csproj` требуется установка NugetTargetMoniker и RuntimeIdentifiers в proj/targets — [3854](https://github.com/NuGet/Home/issues/3854)</span><span class="sxs-lookup"><span data-stu-id="58f54-292">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

* <span data-ttu-id="58f54-293">Установка пакета может перекрываться с автоматическим восстановлением — [3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="58f54-293">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

* <span data-ttu-id="58f54-294">Контекстное меню QueryStatus не появляется в том случае, если не загружен VSPackage — [3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="58f54-294">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

* <span data-ttu-id="58f54-295">Для операций восстановления решения и сборки диалоговое окно по-прежнему отображается — [3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="58f54-295">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

* <span data-ttu-id="58f54-296">Изоляция версии VSSDK при построении решения NuGet.Clients — [3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="58f54-296">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

<span data-ttu-id="58f54-297">**Функция:**</span><span class="sxs-lookup"><span data-stu-id="58f54-297">**Feature:**</span></span>

* <span data-ttu-id="58f54-298">Локализация строк в NuGet.Core.sln — [2041](https://github.com/NuGet/Home/issues/2041)</span><span class="sxs-lookup"><span data-stu-id="58f54-298">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

* <span data-ttu-id="58f54-299">Nuget вызывает принудительную загрузку проектов веб-приложений в режиме LSL — [4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="58f54-299">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

* <span data-ttu-id="58f54-300">Поддержка автоматически задаваемых ссылок проектов для блокировки изменений версии в пользовательском интерфейсе для пакетов "sdk installed" — [4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="58f54-300">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

* <span data-ttu-id="58f54-301">Передача правильного значения PackageSpec.Version для любых зависимостей проектов (PackageRef) — [3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="58f54-301">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

* <span data-ttu-id="58f54-302">Поддержка удаления ссылок в `.csproj` из командной строки — [4101](https://github.com/NuGet/Home/issues/4101)</span><span class="sxs-lookup"><span data-stu-id="58f54-302">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

* <span data-ttu-id="58f54-303">Поддержка восстановления пакетов PackageReference (обычные и xplat) и загрузки упрощенного решения — [4003](https://github.com/NuGet/Home/issues/4003)</span><span class="sxs-lookup"><span data-stu-id="58f54-303">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

* <span data-ttu-id="58f54-304">Поддержка добавления ссылок в `.csproj` из командной строки — [3751](https://github.com/NuGet/Home/issues/3751)</span><span class="sxs-lookup"><span data-stu-id="58f54-304">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

* <span data-ttu-id="58f54-305">Поддержка восстановления NuGet для загрузки упрощенного решения для `packages.config` или `project.json` - [3711](https://github.com/NuGet/Home/issues/3711)</span><span class="sxs-lookup"><span data-stu-id="58f54-305">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

* <span data-ttu-id="58f54-306">Поддержка contentFiles в создаваемых nuget файлах целевых объектов — [3683](https://github.com/NuGet/Home/issues/3683)</span><span class="sxs-lookup"><span data-stu-id="58f54-306">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

* <span data-ttu-id="58f54-307">Установка Mono CI для проверки nuget.exe на Mac с использованием MSBuild — [3646](https://github.com/NuGet/Home/issues/3646)</span><span class="sxs-lookup"><span data-stu-id="58f54-307">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

* <span data-ttu-id="58f54-308">Отказ от зависимостей NuGet от v2 NuGet.Core — [3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="58f54-308">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>


## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="58f54-309">Ссылки на проблемы GitHub, исправленные в версии RTM</span><span class="sxs-lookup"><span data-stu-id="58f54-309">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="58f54-310">Список проблем 1</span><span class="sxs-lookup"><span data-stu-id="58f54-310">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RTM")  
[<span data-ttu-id="58f54-311">Список проблем 2</span><span class="sxs-lookup"><span data-stu-id="58f54-311">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC4")  
[<span data-ttu-id="58f54-312">Список проблем 3</span><span class="sxs-lookup"><span data-stu-id="58f54-312">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC3")  
[<span data-ttu-id="58f54-313">Список проблем 4</span><span class="sxs-lookup"><span data-stu-id="58f54-313">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC2")  
[<span data-ttu-id="58f54-314">Список проблем 5</span><span class="sxs-lookup"><span data-stu-id="58f54-314">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC")

