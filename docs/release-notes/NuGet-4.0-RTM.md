---
title: Заметки о выпуске версии-кандидата NuGet 4.0
description: Заметки о выпуске для NuGet 4.0 RTM, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: f1c5408f75966068e8fa11e63118426bbf562047
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2018
ms.locfileid: "32045091"
---
# <a name="nuget-40-rtm-release-notes"></a><span data-ttu-id="75db5-103">Заметки о выпуске версии NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="75db5-103">NuGet 4.0 RTM Release Notes</span></span>

<span data-ttu-id="75db5-104">В состав [Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) входит версия NuGet 4.0, в которую добавлена поддержка платформы .NET Core, а также представлено множество исправлений, направленных на повышение качества и производительности.</span><span class="sxs-lookup"><span data-stu-id="75db5-104">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="75db5-105">Кроме того, в этой версии появился ряд усовершенствований, таких как поддержка формата PackageReference, использование команд NuGet в качестве целей MSBuild, восстановление пакетов в фоновом режиме и других.</span><span class="sxs-lookup"><span data-stu-id="75db5-105">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="75db5-106">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="75db5-106">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="75db5-107">Сбой восстановления NuGet может завершиться ошибкой, если в решении есть несколько проектов, ссылающихся на другой проект</span><span class="sxs-lookup"><span data-stu-id="75db5-107">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="75db5-108">Проблеми</span><span class="sxs-lookup"><span data-stu-id="75db5-108">Issue</span></span>

<span data-ttu-id="75db5-109">Восстановление NuGet может не работать, если в решении есть проекты, которые ссылаются на один и тот же проект с разным регистром или с другими относительными путями.</span><span class="sxs-lookup"><span data-stu-id="75db5-109">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="75db5-110">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="75db5-110">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="75db5-111">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="75db5-111">Workaround</span></span>

<span data-ttu-id="75db5-112">Исправьте регистр и относительные пути, чтобы они совпадали во всех ссылках на проект.</span><span class="sxs-lookup"><span data-stu-id="75db5-112">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="75db5-113">При использовании консоли диспетчера пакетов клавиша ВВОД может не работать</span><span class="sxs-lookup"><span data-stu-id="75db5-113">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="75db5-114">Проблеми</span><span class="sxs-lookup"><span data-stu-id="75db5-114">Issue</span></span>

<span data-ttu-id="75db5-115">Периодически клавиша ВВОД не работает в консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="75db5-115">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="75db5-116">В этом случае проверьте ход исправления и укажите дополнительные сведения для воспроизведения ошибки.</span><span class="sxs-lookup"><span data-stu-id="75db5-116">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="75db5-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="75db5-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="75db5-118">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="75db5-118">Workaround</span></span>

<span data-ttu-id="75db5-119">Перезапустите Visual Studio и откройте консоль управления пакетами перед тем, как открыть решение.</span><span class="sxs-lookup"><span data-stu-id="75db5-119">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="75db5-120">Кроме того, попробуйте удалить файл `project.lock.json` и выполнить восстановление еще раз.</span><span class="sxs-lookup"><span data-stu-id="75db5-120">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="75db5-121">При использовании пакета, содержащего сборку с недопустимой подписью, в проектах .NET Core может возникнуть бесконечный цикл восстановления</span><span class="sxs-lookup"><span data-stu-id="75db5-121">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>

#### <a name="issue"></a><span data-ttu-id="75db5-122">Проблеми</span><span class="sxs-lookup"><span data-stu-id="75db5-122">Issue</span></span>

<span data-ttu-id="75db5-123">Иногда при использовании пакета, содержащего сборку с недопустимой подписью, или если для версии пакета задан тикер DateTime, возникает бесконечный цикл автоматического восстановления пакета.</span><span class="sxs-lookup"><span data-stu-id="75db5-123">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="75db5-124">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="75db5-124">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="75db5-125">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="75db5-125">Workaround</span></span>

<span data-ttu-id="75db5-126">Сейчас для этой проблемы не существует обходного решения.</span><span class="sxs-lookup"><span data-stu-id="75db5-126">There is no workaround at this time.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="75db5-127">Вы не можете просмотреть, добавить или обновить DotNetCLITools с помощью диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="75db5-127">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="75db5-128">Проблеми</span><span class="sxs-lookup"><span data-stu-id="75db5-128">Issue</span></span>

<span data-ttu-id="75db5-129">Диспетчер пакетов NuGet не отображается и не позволяет добавить или обновить DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="75db5-129">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="75db5-130">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="75db5-130">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="75db5-131">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="75db5-131">Workaround</span></span>

<span data-ttu-id="75db5-132">DotNetCLIToolReferences нужно изменить вручную в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="75db5-132">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="75db5-133">При установке свойства PackageId для проектов произойдет сбой восстановления NuGet</span><span class="sxs-lookup"><span data-stu-id="75db5-133">NuGet restore will fail when you set PackageId property for projects</span></span>

#### <a name="issue"></a><span data-ttu-id="75db5-134">Проблеми</span><span class="sxs-lookup"><span data-stu-id="75db5-134">Issue</span></span>

<span data-ttu-id="75db5-135">Для проектов .NET Core восстановление NuGet в Visual Studio не связано со свойством PackageId проектов.</span><span class="sxs-lookup"><span data-stu-id="75db5-135">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="75db5-136">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="75db5-136">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="75db5-137">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="75db5-137">Workaround</span></span>

<span data-ttu-id="75db5-138">Выполните восстановление с использованием командной строки.</span><span class="sxs-lookup"><span data-stu-id="75db5-138">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="75db5-139">Если в проекте нет папки obj, произойдет сбой восстановления пакета</span><span class="sxs-lookup"><span data-stu-id="75db5-139">When your project does not have 'obj' folder, package restore may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="75db5-140">Проблеми</span><span class="sxs-lookup"><span data-stu-id="75db5-140">Issue</span></span>

<span data-ttu-id="75db5-141">Visual Studio не удается восстановить PackageReferences, если папка obj удалена.</span><span class="sxs-lookup"><span data-stu-id="75db5-141">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="75db5-142">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="75db5-142">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="75db5-143">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="75db5-143">Workaround</span></span>

<span data-ttu-id="75db5-144">Создайте папку obj вручную, и восстановление должно заработать.</span><span class="sxs-lookup"><span data-stu-id="75db5-144">Create 'obj' folder manually and the restore should work.</span></span>

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="75db5-145">Обновление пакетов вручную с использованием Update-Package в консоли может завершиться ошибкой</span><span class="sxs-lookup"><span data-stu-id="75db5-145">Manually updating packages using Update-Package in console may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="75db5-146">Проблеми</span><span class="sxs-lookup"><span data-stu-id="75db5-146">Issue</span></span>

<span data-ttu-id="75db5-147">Использование Update-Package вручную в консоли работает только один раз для только что преобразованных проектов PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="75db5-147">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="75db5-148">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="75db5-148">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="75db5-149">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="75db5-149">Workaround</span></span>

<span data-ttu-id="75db5-150">Сейчас для этой проблемы не существует обходного решения.</span><span class="sxs-lookup"><span data-stu-id="75db5-150">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="75db5-151">Изменение требуемой версии .NET Framework может привести к частичному отсутствию данных функции IntelliSense</span><span class="sxs-lookup"><span data-stu-id="75db5-151">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="75db5-152">Проблеми</span><span class="sxs-lookup"><span data-stu-id="75db5-152">Issue</span></span>

<span data-ttu-id="75db5-153">Если изменить требуемую версию .NET Framework в Visual Studio, вы можете получить неполные данные функции IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="75db5-153">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="75db5-154">Это происходит, если использовать PackageReferences в качестве формата диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="75db5-154">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="75db5-155">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="75db5-155">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="75db5-156">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="75db5-156">Workaround</span></span>

<span data-ttu-id="75db5-157">Выполните восстановление вручную.</span><span class="sxs-lookup"><span data-stu-id="75db5-157">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="75db5-158">Операция MSBuild /t:restore завершается ошибкой, если проект, предназначенный для .NET 4.6.1, ссылается на другой проект, предназначенный для .NET Standard</span><span class="sxs-lookup"><span data-stu-id="75db5-158">msbuild /t:restore fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="75db5-159">Проблеми</span><span class="sxs-lookup"><span data-stu-id="75db5-159">Issue</span></span>

<span data-ttu-id="75db5-160">Операция MSBuild /t:restore завершается ошибкой, если проект на основе PackageReferenece, предназначенный для .NET 4.6.1, ссылается на другой проект на основе PackageReferenece, предназначенный для .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="75db5-160">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="75db5-161">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="75db5-161">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="75db5-162">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="75db5-162">Workaround</span></span>

<span data-ttu-id="75db5-163">Сейчас для этой проблемы не существует обходного решения.</span><span class="sxs-lookup"><span data-stu-id="75db5-163">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="75db5-164">Проблемы, исправленные в рамках NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="75db5-164">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="75db5-165">Проблемы, исправленные в NuGet 4.0 RC, описаны в разделе [Заметки о выпуске NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="75db5-165">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

### <a name="features"></a><span data-ttu-id="75db5-166">Функции</span><span class="sxs-lookup"><span data-stu-id="75db5-166">Features</span></span>

- <span data-ttu-id="75db5-167">Локализация строк в NuGet.Core.sln — [2041](https://github.com/NuGet/Home/issues/2041)</span><span class="sxs-lookup"><span data-stu-id="75db5-167">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

- <span data-ttu-id="75db5-168">Nuget вызывает принудительную загрузку проектов веб-приложений в режиме LSL — [4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="75db5-168">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

- <span data-ttu-id="75db5-169">Поддержка автоматически задаваемых ссылок проектов для блокировки изменений версии в пользовательском интерфейсе для пакетов "sdk installed" — [4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="75db5-169">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

- <span data-ttu-id="75db5-170">Передача правильного значения PackageSpec.Version для любых зависимостей проектов (PackageRef) — [3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="75db5-170">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

- <span data-ttu-id="75db5-171">Поддержка удаления ссылок в `.csproj` из командной строки — [4101](https://github.com/NuGet/Home/issues/4101)</span><span class="sxs-lookup"><span data-stu-id="75db5-171">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

- <span data-ttu-id="75db5-172">Поддержка восстановления пакетов PackageReference (обычные и xplat) и загрузки упрощенного решения — [4003](https://github.com/NuGet/Home/issues/4003)</span><span class="sxs-lookup"><span data-stu-id="75db5-172">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

- <span data-ttu-id="75db5-173">Поддержка добавления ссылок в `.csproj` из командной строки — [3751](https://github.com/NuGet/Home/issues/3751)</span><span class="sxs-lookup"><span data-stu-id="75db5-173">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

- <span data-ttu-id="75db5-174">Поддержка восстановления NuGet для загрузки упрощенного решения для `packages.config` или `project.json` - [3711](https://github.com/NuGet/Home/issues/3711)</span><span class="sxs-lookup"><span data-stu-id="75db5-174">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

- <span data-ttu-id="75db5-175">Поддержка contentFiles в создаваемых nuget файлах целевых объектов — [3683](https://github.com/NuGet/Home/issues/3683)</span><span class="sxs-lookup"><span data-stu-id="75db5-175">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

- <span data-ttu-id="75db5-176">Установка Mono CI для проверки nuget.exe на Mac с использованием MSBuild — [3646](https://github.com/NuGet/Home/issues/3646)</span><span class="sxs-lookup"><span data-stu-id="75db5-176">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

- <span data-ttu-id="75db5-177">Отказ от зависимостей NuGet от v2 NuGet.Core — [3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="75db5-177">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>

### <a name="bugs"></a><span data-ttu-id="75db5-178">Ошибки</span><span class="sxs-lookup"><span data-stu-id="75db5-178">Bugs</span></span>

- <span data-ttu-id="75db5-179">Восстановление NuGet в Visual Studio не связано со свойством PackageId проектов — [4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="75db5-179">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

- <span data-ttu-id="75db5-180">Ошибка NuGet ProjectSystemCache при добавлении пакета в пакет vsix — [4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="75db5-180">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

- <span data-ttu-id="75db5-181">Операция упаковки вызывает исключение при использовании IncludeSource в проекте с несколькими моникерами целевой платформы — [4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="75db5-181">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

- <span data-ttu-id="75db5-182">Работа VS 2017 RC3 завершается сбоем при использовании обновления из среды управления пакетами на уровне решения — [4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="75db5-182">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

- <span data-ttu-id="75db5-183">Не удается удалить вновь установленный пакет — [4435](https://github.com/NuGet/Home/issues/4435)</span><span class="sxs-lookup"><span data-stu-id="75db5-183">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

- <span data-ttu-id="75db5-184">При переносе в PackageRef наблюдается неожиданное поведение функции восстановления гибридных решений — [4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="75db5-184">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

- <span data-ttu-id="75db5-185">При выполнении построения вскоре после запуска операции NuGet (установка, обновление, восстановление) возможно зависание VS — [4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="75db5-185">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

- <span data-ttu-id="75db5-186">Зависание пользовательского интерфейса — взаимоблокировка при инициализации NuGet.SolutionRestoreManager.RestoreManagerPackage — [4371](https://github.com/NuGet/Home/issues/4371)</span><span class="sxs-lookup"><span data-stu-id="75db5-186">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

- <span data-ttu-id="75db5-187">Команда add package должна добавлять версию в качестве атрибута вместо элемента — [4325](https://github.com/NuGet/Home/issues/4325)</span><span class="sxs-lookup"><span data-stu-id="75db5-187">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

- <span data-ttu-id="75db5-188">dotnet</span><span class="sxs-lookup"><span data-stu-id="75db5-188">dotnet</span></span>
  - <span data-ttu-id="75db5-189">Команда dotnetcore restore foo.sln — сбой в случаях, когда конфигурации в SLN приводят к дублированию проектов в графе восстановления с разными конфигурациями — [4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="75db5-189">dotnetcore Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

- <span data-ttu-id="75db5-190">Пакеты только с содержимым — [3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="75db5-190">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

- <span data-ttu-id="75db5-191">Отказ по умолчанию от параметра селектора формата пакета — [4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="75db5-191">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

- <span data-ttu-id="75db5-192">Производительность: CreateUAP_CSharp_VS.01.1. Время создания проекта Duration_TotalElapsedTime ухудшилось на 3153,570 мс (149,1 %).</span><span class="sxs-lookup"><span data-stu-id="75db5-192">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="75db5-193">Базовая версия 26129.02 — [4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="75db5-193">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

- <span data-ttu-id="75db5-194">Производительность: для решения ManagedLangs_CS_DDRIT.0300. Время повторного построения Duration_TotalElapsedTime ухудшилось на 1,5 с.</span><span class="sxs-lookup"><span data-stu-id="75db5-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="75db5-195">Базовая версия 26105 — [4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="75db5-195">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

- <span data-ttu-id="75db5-196">Сбой заявки в проектах с несколькими моникерами целевой платформы — [4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="75db5-196">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

- <span data-ttu-id="75db5-197">Производительность: WebForms_DDRIT.1200. Время закрытия решения VM_ImagesInMemory_Total_devenv ухудшилось на 3,000 значения счетчика (0,5 %).</span><span class="sxs-lookup"><span data-stu-id="75db5-197">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="75db5-198">Базовая версия 26123.04 — [4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="75db5-198">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

- <span data-ttu-id="75db5-199">vsfeedback — предупреждения упаковки при нацеливании на netcoreapp1.1 — [4397](https://github.com/NuGet/Home/issues/4397)</span><span class="sxs-lookup"><span data-stu-id="75db5-199">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

- <span data-ttu-id="75db5-200">Исключение PathTooLongException при попытке добавить пакет NuGet в пустое веб-приложение ASP.NET Core — [4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="75db5-200">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

- <span data-ttu-id="75db5-201">Упаковка выполняется слишком часто — dotnet</span><span class="sxs-lookup"><span data-stu-id="75db5-201">Pack runs too often -- dotnet</span></span>
  - <span data-ttu-id="75db5-202">Команда dotnetcore pack завершается сбоем при наличии циклической зависимости в целевом графе зависимостей, включающем целевую операцию упаковки — [4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="75db5-202">dotnetcore pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

- <span data-ttu-id="75db5-203">Упаковка выполняется слишком часто — при создании пакета NuGet не включаются все конфигурации — [4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="75db5-203">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

- <span data-ttu-id="75db5-204">Исключение NullReferenceException при добавлении nuget с packageref в проект C++ — [4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="75db5-204">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

- <span data-ttu-id="75db5-205">Специальные возможности: экранный диктор не воспроизводит название флажка, позволяющего выбрать проекты, в которые требуется установить пакет — [4366](https://github.com/NuGet/Home/issues/4366)</span><span class="sxs-lookup"><span data-stu-id="75db5-205">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

- <span data-ttu-id="75db5-206">NuGet VS17 периодически не может подключиться к веб-каналам VSO/VSTS — ошибка VS 365798 — [4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="75db5-206">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

- <span data-ttu-id="75db5-207">contentFiles выводит данные в неверное расположение, если PackagePath задает путь в виде "contentFiles" — [4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="75db5-207">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

- <span data-ttu-id="75db5-208">При упаковке целевого объекта добавляется свойство PackageVersion с VersionSuffix — [4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="75db5-208">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

- <span data-ttu-id="75db5-209">Не удается указать путь к пакету при использовании dotnet pack — [4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="75db5-209">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

- <span data-ttu-id="75db5-210">NuGet выводит серию предупреждений о повторяющихся операциях импорта во время восстановления — [4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="75db5-210">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

- <span data-ttu-id="75db5-211">Диалоговое окно для выбора формата диспетчера пакетов NuGet плохо выглядит при установке темной темы — [4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="75db5-211">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

- <span data-ttu-id="75db5-212">Сбой VS при восстановлении сборки — [4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="75db5-212">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

- <span data-ttu-id="75db5-213">Взаимоблокировка Visual Studio при добавлении моникера целевой платформы в targetframeworks, сохранении и последующем выполнении перестроения.</span><span class="sxs-lookup"><span data-stu-id="75db5-213">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="75db5-214">10 % времени — [4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="75db5-214">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

- <span data-ttu-id="75db5-215">nuget pack не выводит сообщение об успехе в случае успешной упаковки проекта — [4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="75db5-215">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

- <span data-ttu-id="75db5-216">PackTask завершается сбоем из-за того, что не удается найти System.IO.Compression 4.1 — [4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="75db5-216">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

- <span data-ttu-id="75db5-217">Упаковка выполняется слишком часто — PackTask часто завершается сбоем из-за конфликтов при доступе к файлу — [4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="75db5-217">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

- <span data-ttu-id="75db5-218">NuGet открывает окно вывода во время фонового восстановления — [4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="75db5-218">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

- <span data-ttu-id="75db5-219">Исключение ServiceProvider как потенциально опасного шаблона написания кода (может приводить к зависаниям) — [4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="75db5-219">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

- <span data-ttu-id="75db5-220">Производительность или зависание пользовательского интерфейса — повышение производительности считывания DownloadTimeoutStream — [4266](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="75db5-220">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

- <span data-ttu-id="75db5-221">Взаимоблокировка Visual Studio при попытке закрыть проект до завершения операции восстановления NuGet — [4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="75db5-221">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

- <span data-ttu-id="75db5-222">Проблемы с PackTask и упаковкой — `.nuspec` - [4250](https://github.com/NuGet/Home/issues/4250)</span><span class="sxs-lookup"><span data-stu-id="75db5-222">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

- <span data-ttu-id="75db5-223">[vsfeedback] Не удается разрешить пакеты nuget для нового проекта (требуется перезапуск Visual Studio) — [4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="75db5-223">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

- <span data-ttu-id="75db5-224">[vsfeedback] Раскрывающийся список "Версия", в котором отображаются доступные версии пакета, плохо синхронизируется с выбранным пакетом nuGet... — [4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="75db5-224">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

- <span data-ttu-id="75db5-225">Nuget.Client должен использовать CPS JoinableTaskFactory при взаимодействии с CPS для предотвращения взаимоблокировок — [4185](https://github.com/NuGet/Home/issues/4185)</span><span class="sxs-lookup"><span data-stu-id="75db5-225">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

- <span data-ttu-id="75db5-226">NuGet 3.5.0 не распаковывает `.targets` из пакета — [4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="75db5-226">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

- <span data-ttu-id="75db5-227">dotnet</span><span class="sxs-lookup"><span data-stu-id="75db5-227">dotnet</span></span>
  - <span data-ttu-id="75db5-228">dotnetcore pack не поддерживает заголовок в `.csproj` - [4150](https://github.com/NuGet/Home/issues/4150)</span><span class="sxs-lookup"><span data-stu-id="75db5-228">dotnetcore pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

- <span data-ttu-id="75db5-229">Install-Package приводит к появлению диалогового окна ошибки в версии VS2017 RC — [4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="75db5-229">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

- <span data-ttu-id="75db5-230">Не работает обновление пакета для проекта .Net Core, поскольку пользовательский интерфейс не получает обновление CPS из назначения.</span><span class="sxs-lookup"><span data-stu-id="75db5-230">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="75db5-231"> - [4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="75db5-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

- <span data-ttu-id="75db5-232">Предупреждение об улучшении неразрешенных ссылок — [3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="75db5-232">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

- <span data-ttu-id="75db5-233">dotnet</span><span class="sxs-lookup"><span data-stu-id="75db5-233">dotnet</span></span>
  - <span data-ttu-id="75db5-234">dotnetcore pack — ProjectReference теряет сведения о версии — [3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="75db5-234">dotnetcore pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

- <span data-ttu-id="75db5-235">Общее ухудшение времени создания и повторного построения проекта приложения для универсальной платформы Windows — [3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="75db5-235">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

- <span data-ttu-id="75db5-236">Сообщение об успешном восстановлении отображается даже при возникновении ошибок в процессе восстановления.</span><span class="sxs-lookup"><span data-stu-id="75db5-236">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="75db5-237"> - [3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="75db5-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

- <span data-ttu-id="75db5-238">Повторная публикация Nuget.CommandLine 3.4.4 на веб-сайте Nuget.org — [2931](https://github.com/NuGet/Home/issues/2931)</span><span class="sxs-lookup"><span data-stu-id="75db5-238">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

- <span data-ttu-id="75db5-239">При переносе проекты изменяются с `project.json` на `.csproj` — восстановление завершается сбоем — [4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="75db5-239">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

- <span data-ttu-id="75db5-240">Сбой при восстановлении только что созданного тестового проекта xunit — [4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="75db5-240">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

- <span data-ttu-id="75db5-241">При открытии проектов Core возможно зависание пользовательского интерфейса — [4269](https://github.com/NuGet/Home/issues/4269)</span><span class="sxs-lookup"><span data-stu-id="75db5-241">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

- <span data-ttu-id="75db5-242">Исправление файла целевых объектов для задач построения — [4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="75db5-242">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

- <span data-ttu-id="75db5-243">Список ошибок содержит ошибку после построения решения, которое выгружает указанный по ссылке проект — [4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="75db5-243">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

- <span data-ttu-id="75db5-244">MSB4057: целевой объект "_GenerateRestoreGraphProjectEntry" не существует в проекте.</span><span class="sxs-lookup"><span data-stu-id="75db5-244">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="75db5-245"> - [4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="75db5-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

- <span data-ttu-id="75db5-246">vsfeedback: пользовательский интерфейс диспетчера nuget для решения завершает работу со сбоем при выборе всех проектов — [4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="75db5-246">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

- <span data-ttu-id="75db5-247">nuget.exe msbuildpath завершается сбоем при наличии конечного знака косой черты — [4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="75db5-247">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

- <span data-ttu-id="75db5-248">vsfeedback: операция восстановления NuGet выдает несколько предупреждений о ссылке на проект для проекта LinqToTwitter — [4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="75db5-248">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

- <span data-ttu-id="75db5-249">При упаковке из `.csproj` не включается атрибут minClientVersion — [4135](https://github.com/NuGet/Home/issues/4135)</span><span class="sxs-lookup"><span data-stu-id="75db5-249">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

- <span data-ttu-id="75db5-250">NuGet.Build.Tasks.Pack.dll поставляется с отложенной подписью в VS2017 (d15rel 26014.00) — [4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="75db5-250">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

- <span data-ttu-id="75db5-251">VSFeedback: восстановление завершается сбоем для проекта VS 2015, созданного с помощью CMake 3.7.1 — [4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="75db5-251">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

- <span data-ttu-id="75db5-252">VSFeedback: ошибки восстановления могут скрывать более полные сообщения об ошибках, которые могут выдаваться при построении — [4113](https://github.com/NuGet/Home/issues/4113)</span><span class="sxs-lookup"><span data-stu-id="75db5-252">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

- <span data-ttu-id="75db5-253">[VSFeedback] Ошибка при восстановлении пакетов NuGet для проекта веб-сайта: значение не может быть null.</span><span class="sxs-lookup"><span data-stu-id="75db5-253">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="75db5-254"> - [4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="75db5-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

- <span data-ttu-id="75db5-255">Операция переноса вызывает исключение ссылки на объект в NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker — [4067](https://github.com/NuGet/Home/issues/4067)</span><span class="sxs-lookup"><span data-stu-id="75db5-255">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

- <span data-ttu-id="75db5-256">dotnet</span><span class="sxs-lookup"><span data-stu-id="75db5-256">dotnet</span></span>
  - <span data-ttu-id="75db5-257">Команда dotnetcore pack должна выполнять упаковку средств с версиями, для которых было выполнено построение пакета — [4063](https://github.com/NuGet/Home/issues/4063)</span><span class="sxs-lookup"><span data-stu-id="75db5-257">dotnetcore pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

- <span data-ttu-id="75db5-258">Новая операция фонового восстановления записывает в строку состояния значение в миллисекундах, тогда как восстановление занимает секунды — [4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="75db5-258">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

- <span data-ttu-id="75db5-259">Опечатка в сообщении о сбое при разрешении всех ссылок проекта —[4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="75db5-259">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

- <span data-ttu-id="75db5-260">Включение рабочих процессов PCM в сценариях ссылок на пакет —[4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="75db5-260">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

- <span data-ttu-id="75db5-261">Не удается найти установленные пакеты в пользовательском интерфейсе диспетчера пакетов — [4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="75db5-261">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

- <span data-ttu-id="75db5-262">dotnet</span><span class="sxs-lookup"><span data-stu-id="75db5-262">dotnet</span></span>
  - <span data-ttu-id="75db5-263">dotnetcore pack завершается сбоем при пустом PackagePath —[3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="75db5-263">dotnetcore pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

- <span data-ttu-id="75db5-264">Задача восстановления завершается сбоем в многопользовательском сценарии — [3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="75db5-264">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

- <span data-ttu-id="75db5-265">Не удается изменить тип содержимого при упаковке с использованием задачи упаковки NuGet — [3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="75db5-265">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

- <span data-ttu-id="75db5-266">Неверная копия по умолчанию ContentFiles для MsBuild /t:pack — [3894](https://github.com/NuGet/Home/issues/3894)</span><span class="sxs-lookup"><span data-stu-id="75db5-266">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

- <span data-ttu-id="75db5-267">При восстановлении установки пакета в журналах дублируется сообщение о восстановлении пакетов — [3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="75db5-267">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

- <span data-ttu-id="75db5-268">Снятие защитных функций — восстановление раздела сред выполнения должно применяться только к текущему проекту — [3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="75db5-268">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

- <span data-ttu-id="75db5-269">Задача упаковки помещает файлы содержимого одновременно в "content/" и "contentFiles/" — [3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="75db5-269">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

- <span data-ttu-id="75db5-270">dotnet</span><span class="sxs-lookup"><span data-stu-id="75db5-270">dotnet</span></span>
  - <span data-ttu-id="75db5-271">dotnetcore pack3 выполняет дополнительное разделение тегов — [3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="75db5-271">dotnetcore pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

- <span data-ttu-id="75db5-272">dotnet</span><span class="sxs-lookup"><span data-stu-id="75db5-272">dotnet</span></span>
  - <span data-ttu-id="75db5-273">dotnetcore pack: упаковка проектов с использованием ссылок на проекты приводит к дублированию предупреждения об импорте — [3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="75db5-273">dotnetcore pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

- <span data-ttu-id="75db5-274">Не всегда отображается журнал восстановления в VS — [3633](https://github.com/NuGet/Home/issues/3633)</span><span class="sxs-lookup"><span data-stu-id="75db5-274">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

- <span data-ttu-id="75db5-275">В тексте справки по локальным компонентам nuget по-прежнему упоминается кэш пакетов — [3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="75db5-275">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

- <span data-ttu-id="75db5-276">Restore3 связывает PackageReferences с TargetFrameworks.</span><span class="sxs-lookup"><span data-stu-id="75db5-276">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="75db5-277"> - [3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="75db5-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

- <span data-ttu-id="75db5-278">Nuget выбирает неожиданную версию MSBuild в командной строке разработчика VS "15",</span><span class="sxs-lookup"><span data-stu-id="75db5-278">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="75db5-279">предварительная версия 4 — [3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="75db5-279">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

- <span data-ttu-id="75db5-280">Запись файлов целевых объектов или свойств при завершившемся сбоем восстановлении — [3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="75db5-280">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

- <span data-ttu-id="75db5-281">NuGet во время восстановления не учитывает те же оболочки совместимости, что и MSBuild при выполнении в командной строке VS 15 — [3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="75db5-281">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

- <span data-ttu-id="75db5-282">Повторное включение PackFromProjectWithDevelopmentDependencySet для VS15 — [3272](https://github.com/NuGet/Home/issues/3272)</span><span class="sxs-lookup"><span data-stu-id="75db5-282">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

- <span data-ttu-id="75db5-283">Проблемы с Blend при работе с NuGet — [4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="75db5-283">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

- <span data-ttu-id="75db5-284">Интеграция версии 4.0.0.2067 в репозитории интерфейса командной строки и SDK для поставки вместе с RC2 — [4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="75db5-284">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

- <span data-ttu-id="75db5-285">VS зависает при создании нового консольного приложения Core, закрытии решения, а также открытии и закрытии решения — [4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="75db5-285">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

- <span data-ttu-id="75db5-286">Зависание при открытии проекта d15prerel.25916.01 — [3982](https://github.com/NuGet/Home/issues/3982)</span><span class="sxs-lookup"><span data-stu-id="75db5-286">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

- <span data-ttu-id="75db5-287">Исправление сообщения в справке и документации по dotnet и локальным компонентам nuget.exe — [3919](https://github.com/NuGet/Home/issues/3919)</span><span class="sxs-lookup"><span data-stu-id="75db5-287">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

- <span data-ttu-id="75db5-288">Проверка PackTask на наличие проблем, связанных с начальным или конечным пробелом — [3906](https://github.com/NuGet/Home/issues/3906)</span><span class="sxs-lookup"><span data-stu-id="75db5-288">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

- <span data-ttu-id="75db5-289">dotnet</span><span class="sxs-lookup"><span data-stu-id="75db5-289">dotnet</span></span>
  - <span data-ttu-id="75db5-290">dotnetcore pack выполняет упаковку из obj, а не из bin — [3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="75db5-290">dotnetcore pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

- <span data-ttu-id="75db5-291">dotnet</span><span class="sxs-lookup"><span data-stu-id="75db5-291">dotnet</span></span>
  - <span data-ttu-id="75db5-292">dotnetcore pack всегда присваивает ProjectReference версию 1.0.0 — [3874](https://github.com/NuGet/Home/issues/3874)</span><span class="sxs-lookup"><span data-stu-id="75db5-292">dotnetcore pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

- <span data-ttu-id="75db5-293">dotnet</span><span class="sxs-lookup"><span data-stu-id="75db5-293">dotnet</span></span>
  - <span data-ttu-id="75db5-294">dotnetcore pack завершается сбоем со ссылками на проект и <TargetFramework> - [3865](https://github.com/NuGet/Home/issues/3865)</span><span class="sxs-lookup"><span data-stu-id="75db5-294">dotnetcore pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

- <span data-ttu-id="75db5-295">Исключение LockRecursionException в ProjectSystemCache.TryGetProjectNameByShortName — [3861](https://github.com/NuGet/Home/issues/3861)</span><span class="sxs-lookup"><span data-stu-id="75db5-295">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

- <span data-ttu-id="75db5-296">Обрезка пробелов из свойств MSBuild — [3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="75db5-296">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

- <span data-ttu-id="75db5-297">Объединение двух событий проекта, возникающих при загрузке проекта — [3759](https://github.com/NuGet/Home/issues/3759)</span><span class="sxs-lookup"><span data-stu-id="75db5-297">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

- <span data-ttu-id="75db5-298">Библиотеки P2P в файле `project.assets.json` файл имеют неправильную версию — [3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="75db5-298">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

- <span data-ttu-id="75db5-299">Восстановление завершается сбоем из-за отсутствия ответа веб-канала и недоступности пакета — [3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="75db5-299">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

- <span data-ttu-id="75db5-300">nuget.exe может зависнуть при большом объеме выходных данных ошибки MSBuild — [3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="75db5-300">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

- <span data-ttu-id="75db5-301">Задача восстановления при построении для Blend завершается сбоем в первый раз и успешно выполняется во второй (исправлен сценарий для VS) — [2121](https://github.com/NuGet/Home/issues/2121)</span><span class="sxs-lookup"><span data-stu-id="75db5-301">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

### <a name="dcrs"></a><span data-ttu-id="75db5-302">Запросы на изменение структуры</span><span class="sxs-lookup"><span data-stu-id="75db5-302">DCRs</span></span>

- <span data-ttu-id="75db5-303">перенос vsix из v2 vsix в v3 vsix — [4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="75db5-303">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

- <span data-ttu-id="75db5-304">NuGet должен предусматривать механизм получения пути к файлу блокировки в MSBuild — [3351](https://github.com/NuGet/Home/issues/3351)</span><span class="sxs-lookup"><span data-stu-id="75db5-304">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

- <span data-ttu-id="75db5-305">Добавление ресурсов построения в проверку совместимости моникера целевой платформы и файл ресурсов — [3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="75db5-305">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

- <span data-ttu-id="75db5-306">Определение нового объекта ProjectCapability "Pack" в целевых объектах упаковки для реализации связанных с пакетом возможностей — [4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="75db5-306">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

- <span data-ttu-id="75db5-307">Запуск пакета в качестве целевого объекта после построения с условием на основе свойства MSBuild "GeneratePackageOnBuild" — [4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="75db5-307">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

- <span data-ttu-id="75db5-308">Использование свойства NuGet RestoreProjectStyle для создания отдельных проектов NuGet — [4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="75db5-308">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

- <span data-ttu-id="75db5-309">Адаптивное восстановление для изменений переходных ссылок проекта — [4076](https://github.com/NuGet/Home/issues/4076)</span><span class="sxs-lookup"><span data-stu-id="75db5-309">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

- <span data-ttu-id="75db5-310">Добавление свойств NuGet в целевой файл для проектов, не предназначенных для универсальной платформы Windows — [4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="75db5-310">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

- <span data-ttu-id="75db5-311">Поддержка TargetPlatformVersion для универсальной платформы Windows — [3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="75db5-311">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

- <span data-ttu-id="75db5-312">Передача метаданных ссылок проекта в систему проектов NuGet — [3922](https://github.com/NuGet/Home/issues/3922)</span><span class="sxs-lookup"><span data-stu-id="75db5-312">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

- <span data-ttu-id="75db5-313">Добавление пользовательского интерфейса для режима упаковки — [3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="75db5-313">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

- <span data-ttu-id="75db5-314">Для прежних версий `.csproj` требуется установка NugetTargetMoniker и RuntimeIdentifiers в proj/targets — [3854](https://github.com/NuGet/Home/issues/3854)</span><span class="sxs-lookup"><span data-stu-id="75db5-314">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

- <span data-ttu-id="75db5-315">Установка пакета может перекрываться с автоматическим восстановлением — [3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="75db5-315">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

- <span data-ttu-id="75db5-316">Контекстное меню QueryStatus не появляется в том случае, если не загружен VSPackage — [3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="75db5-316">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

- <span data-ttu-id="75db5-317">Для операций восстановления решения и сборки диалоговое окно по-прежнему отображается — [3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="75db5-317">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

- <span data-ttu-id="75db5-318">Изоляция версии VSSDK при построении решения NuGet.Clients — [3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="75db5-318">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="75db5-319">Ссылки на проблемы GitHub, исправленные в версии RTM</span><span class="sxs-lookup"><span data-stu-id="75db5-319">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="75db5-320">Список проблем 1</span><span class="sxs-lookup"><span data-stu-id="75db5-320">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[<span data-ttu-id="75db5-321">Список проблем 2</span><span class="sxs-lookup"><span data-stu-id="75db5-321">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[<span data-ttu-id="75db5-322">Список проблем 3</span><span class="sxs-lookup"><span data-stu-id="75db5-322">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[<span data-ttu-id="75db5-323">Список проблем 4</span><span class="sxs-lookup"><span data-stu-id="75db5-323">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[<span data-ttu-id="75db5-324">Список проблем 5</span><span class="sxs-lookup"><span data-stu-id="75db5-324">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
