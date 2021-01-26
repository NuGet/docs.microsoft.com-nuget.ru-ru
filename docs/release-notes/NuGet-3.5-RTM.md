---
title: Заметки о выпуске версии-кандидата 3.5
description: Заметки о выпуске NuGet 3,5, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776350"
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="be54b-103">Заметки о выпуске NuGet 3,5</span><span class="sxs-lookup"><span data-stu-id="be54b-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="be54b-104">[NuGet 3,5 — заметки о](../release-notes/nuget-3.5-RC.md)  |  ВЫпуске RC [Заметки о выпуске для версии-кандидата NuGet 4,0](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="be54b-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="be54b-105">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="be54b-105">Bug Fixes</span></span>

* <span data-ttu-id="be54b-106">Пакет не использует MSBuild 14,1 на Mono- [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="be54b-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="be54b-107">На вкладке "обновление" не выбирается последняя доступная версия для обновления вместо выбора текущей установленной версии — [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="be54b-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="be54b-108">Устраните сбой после проверки подлинности закрытого веб-канала MyGet v2 и выбора команды "отобразить дополнительные результаты x" — [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="be54b-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="be54b-109">Сообщения журнала, как кажется, находятся в порядке, соответствующем пользовательскому интерфейсу [#3446](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="be54b-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="be54b-110">v 3.4.4. при восстановлении NuGet создается сообщение о том, что формат данного пути не поддерживается — [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="be54b-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="be54b-111">Для NuGet cmdLine 3,6 Beta не учитывается-Prop Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="be54b-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="be54b-112">Неиквмная установка NuGet в больших проектах — [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="be54b-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="be54b-113">nuget.exe обновление — самостоятельное обновление [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="be54b-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="be54b-114">3,5. Установка и восстановление из общего UNC-ресурса имеет регрессию производительности от 3.4.4 [#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="be54b-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="be54b-115">Ошибка при установке MOQ из пользовательского интерфейса управления пакетами для проекта net451 — [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="be54b-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="be54b-116">Вкладка "установить" на уровне решения не отображает версию пакета [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="be54b-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="be54b-117">xproj `project.json` обновление с установленной вкладки теряет состояние [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="be54b-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="be54b-118">Пакет NuGet On `.csproj` игнорирует пустой элемент Files в `.nuspec` file- [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="be54b-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="be54b-119">Проекты веб-сайтов, размещенные в IIS, не должны вызывать сбой при восстановлении [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="be54b-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="be54b-120">Учетные данные не получены из Nuget.Config при перенаправлении конечных точек v3 в v2- [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="be54b-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="be54b-121">Пакету NuGet не удается разрешить сборку при получении метаданных переносимой сборки — [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="be54b-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="be54b-122">NuGet не удается найти `msbuild.exe` на Mono- [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="be54b-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="be54b-123">nuget.exe Pack не допускает предварительной версии тега, начинающегося с Numbers- [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="be54b-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="be54b-124">Сбой установки пакета NuGet в VS2015E- [#1298](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="be54b-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="be54b-125">фильтр Алловедверсионс не работает на уровне решения — [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="be54b-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="be54b-126">Случайное восстановление завершается ошибкой, если уже был добавлен элемент с тем же ключом.</span><span class="sxs-lookup"><span data-stu-id="be54b-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="be54b-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="be54b-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="be54b-128">Не удается установить NuGet. Common в `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="be54b-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="be54b-129">При использовании пользовательского интерфейса для поиска источника v2 Финдпаккажесбид вызывается дважды для каждого идентификатора — [#2517](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="be54b-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="be54b-130">Пакеты не могут зависеть от проектов — [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="be54b-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="be54b-131">nuget.exe Pack-исключение документировано, но не поддерживается — [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="be54b-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="be54b-132">Проблемы с сообщениями об ошибках при недопустимых разделах "contentFiles" `.nuspec` — [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="be54b-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="be54b-133">Push-уведомления всегда отправляет весь пакет дважды с аутентифицированными источниками пакетов — [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="be54b-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="be54b-134">При вызове nuget.exe обновить \*. csproj не было указано никаких сведений, а в проекте нет `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="be54b-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="be54b-135">`packages.config` При восстановлении не выполняется повторная попытка выполнения кодов состояния 5xx из источников v2. [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="be54b-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="be54b-136">Двойная точка в файле src в `.nuspec` не работает — [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="be54b-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="be54b-137">Для восстановления CoreCLR необходимо игнорировать потоки с шифрованием [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="be54b-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="be54b-138">nuget.exe обработки Push 403 — неправильный запрос учетных данных [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="be54b-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="be54b-139">Обновление NuGet с помощью диспетчера пакетов удаляет свойства из `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="be54b-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="be54b-140">NuGet. PackageManagement. VisualStudio пытается загрузить "NuGet. TeamFoundationServer14", но имя этой библиотеки DLL изменилось на "NuGet. TeamFoundationServer" — [#2857](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="be54b-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="be54b-141">В пользовательском интерфейсе диспетчера пакетов не отображается только что обновленная версия — [#2828](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="be54b-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="be54b-142">Update — пакет пытается использовать PackageID, Version вместо Package. Version- [#2771](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="be54b-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="be54b-143">Если в проекте не используется NuGet ( `packages.config` или `project.json` ) — [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="be54b-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="be54b-144">Ошибка TFS "[файл] не найдена в рабочей области, или у вас нет разрешения на доступ к нему" во время обновления или удаления, если решение или проект привязаны к системе управления версиями TFS — [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="be54b-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="be54b-145">пакет обновления не получает зависимости для нецелевых пакетов — [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="be54b-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="be54b-146">Невозможно задать уровень детализации журналов для действий пользовательского интерфейса диспетчера пакетов NuGet — [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="be54b-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="be54b-147">Недопустимая конфигурация NuGet — Visual Studio 2015 VSIX (v 3.4.3) — [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="be54b-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="be54b-148">Дефаултпушсаурце в `NuGetDefaults.Config` ( `ProgramData\NuGet` ) не работает — [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="be54b-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="be54b-149">выпуск NuGet 3.4.3 — получение значения не может быть NULL в сборке пакета — [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="be54b-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="be54b-150">RESTORE не использует сохраненные учетные данные из Nuget.Config для веб-каналов VSTS — [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="be54b-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="be54b-151">[dotnet restore]--ConfigFile относится к папке проекта, а не к командлету dir- [#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="be54b-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="be54b-152">Избыточное выделение в коде версии компарсион — [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="be54b-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="be54b-153">Несколько экземпляров nuget.exe пытаются установить один и тот же пакет параллельно, вызывает двойную запись [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="be54b-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="be54b-154">Сведения о зависимостях не кэшируются для операций с несколькими проектами. [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="be54b-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="be54b-155">Установите и обновите Скачанные пакеты, не проверяя папку Packages First — [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="be54b-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="be54b-156">Если список источников пакетов пуст, невозможно добавить источник пакетов через пользовательский интерфейс (NuGet 3.4. x) — [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="be54b-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="be54b-157">Ошибка при попытке установить пакет, зависящий от интерфейсов времени разработки, [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="be54b-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="be54b-158">Установка пакета из консоли PackageManager с параметром "ALL" пытается только первый источник — [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="be54b-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="be54b-159">Последняя бета-версия не распаковка Модернхттпклиент- [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="be54b-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="be54b-160">VS2015 сбой при запуске с помощью самосозданного 3.4.1 NuGet- [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="be54b-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="be54b-161">Команда Update может быть более подробной, если я запросил это так...- [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="be54b-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="be54b-162">Локально построенное расширение VSIX должно иметь те же файлы и библиотеки DLL, что и сборка CI.</span><span class="sxs-lookup"><span data-stu-id="be54b-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="be54b-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="be54b-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="be54b-164">Исправление предупреждений о понижении NuGet в сборке — [#2396](https://github.com/NuGet/Home/issues/2396)</span><span class="sxs-lookup"><span data-stu-id="be54b-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="be54b-165">Проверка подлинности источника пакета (3 раза) заблокирована бессрочно [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="be54b-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="be54b-166">Содержимое пакета не восстанавливается надлежащим образом при установке пакета из канала NuGet v 3.3 + с аргументом-with, если пакет содержит `.nupkg` файлы — [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="be54b-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="be54b-167">Установка NuGet со всеми источниками пакетов, но пакет отсутствует в 1 источник, сбой [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="be54b-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="be54b-168">[Перфватсон] Уиделай: nuget.packagemanagement.visualstudio.dll! NuGet. PackageManagement. VisualStudio. Всмсбуилднужетпрожектсистем + \* lt; &gt; c__DisplayClass_0 + &lt; &lt; AddReference &gt; B__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="be54b-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="be54b-169">Установка блокируется, если один источник не проходит авторизацию [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="be54b-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="be54b-170">`.nuspec` диапазон версий должен переопределять Инклудереференцедпрожектс Version- [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="be54b-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="be54b-171">Update-Package "очень медленный" — "попытка собрать сведения о зависимостях" — [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="be54b-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="be54b-172">Пакет NuGet скрытый переход на более раннюю версию при обновлении зависимостей пакетом [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="be54b-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="be54b-173">nuget.exe обновление удаляет строгое имя сборки и частный атрибут.</span><span class="sxs-lookup"><span data-stu-id="be54b-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="be54b-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="be54b-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="be54b-175">Относительный путь к файлу для "Дефаултпушсаурце" — [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="be54b-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="be54b-176">Улучшение сообщений об ошибках сопоставителя — [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="be54b-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="be54b-177">Обновление-пакет в v3 завершается сбоем с пакетами, отсутствующими в указанном источнике, [#1013](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="be54b-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="be54b-178">Использование относительных путей для источников пакетов является проблемой при использовании [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="be54b-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="be54b-179">Отсутствует зависимость в NUPKG-файле, созданном из проекта, если косвенная зависимость уже существует с требованием более ранней версии [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="be54b-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="be54b-180">При удалении проекта закрывается соответствующее окно пользовательского интерфейса, но Переименование проекта не приводит к переименованию окна пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="be54b-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="be54b-181">Обратите внимание, что PMC прослушивает события переименования проекта и удаления проекта — [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="be54b-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="be54b-182">[Веб-Рабочая нагрузка виллов] Создание "зависаний" для Razor V3 WSP- [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="be54b-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="be54b-183">Установка или восстановление определенного пакета завершается сбоем с "пакетом содержит несколько файлов nuspec".</span><span class="sxs-lookup"><span data-stu-id="be54b-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="be54b-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="be54b-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="be54b-185">Строчные коды & `packages.config` сценарии — [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="be54b-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="be54b-186">[3,5 — бета-версия] При восстановлении пакета не удается восстановить "устаревшие" пакеты — [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="be54b-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="be54b-187">пакет NuGet принудительно добавляет TT-файлы в папку содержимого независимо от того, что [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="be54b-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="be54b-188">Обновление-пакет для веб-приложения ASP.NET создает предупреждение, связанное с файлом: source- [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="be54b-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="be54b-189">`project.json`Если в JSON-файле нет паккоптионс и владельца, то пакет NuGet Pack CSPROJ (с) завершается сбоем. [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="be54b-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="be54b-190">пакет NuGet для `project.json` игнорирует теги паккоптионс, такие как Summary, authors, Owners и т. д. [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="be54b-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="be54b-191">NullReferenceException через NuGet. Packaging. Фисикалпаккажефиле. Вышестояще- [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="be54b-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="be54b-192">Пакет NuGet игнорирует зависимости в выходных данных `.nuspec` для `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="be54b-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="be54b-193">Обновление нескольких пакетов с помощью отката оставляет проект в неработающем состоянии — [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="be54b-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="be54b-194">ContentFiles не добавляются для проектов netstandard — [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="be54b-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="be54b-195">Не удалось правильно упаковать библиотеку .NET Standard, [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="be54b-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="be54b-196">Файл-> создание проекта > библиотеки классов (переносимые) в VS2015 и Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="be54b-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="be54b-197">Ошибка nuGet-1.0.0-\* не является допустимой строкой версии — [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="be54b-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="be54b-198">Find-Package не удается отобразить, но Install-Package Works — [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="be54b-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="be54b-199">Ошибка при выполнении установки-пакета jQuery. Validation на dev15- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="be54b-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="be54b-200">пакет NuGet для xproj по умолчанию имеет недопустимый целевой путь — [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="be54b-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="be54b-201">При установке VS 2015 с обновлением 3 на VS, использующем NuGet версии 3.5.0, возникает ошибка. [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="be54b-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="be54b-202">"Заблокировано packages.config" в `project.json` проекте (UWP, a. k. сборка интегрирована) — [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="be54b-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="be54b-203">Обновите интерфейс командной строки DotNet, установленный сценарием сборки, на preview2-003121, который является официальной сборкой preview2.</span><span class="sxs-lookup"><span data-stu-id="be54b-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="be54b-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="be54b-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="be54b-205">Пользовательский интерфейс диспетчера пакетов: не отображает новую версию после обновления пакета [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="be54b-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="be54b-206">-ApiKey при удалении Командная строка не считывается и не отправляется в 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="be54b-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="be54b-207">Неправильная строка: стабильный выпуск пакета не должен иметь предварительную зависимость.</span><span class="sxs-lookup"><span data-stu-id="be54b-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="be54b-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="be54b-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="be54b-209">Кэш Оптимизедзиппаккаже оставляет пустые папки — [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="be54b-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="be54b-210">Создание исключения для получения Нуллреф проекта PCL (net46 и Windows 10).</span><span class="sxs-lookup"><span data-stu-id="be54b-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="be54b-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="be54b-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="be54b-212">Обновление NuGet должно предоставлять информативное сообщение, если более поздняя версия ограничена ограничением Алловедверсионс- [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="be54b-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="be54b-213">Проблемы с восстановлением NuGet v3 — [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="be54b-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="be54b-214">Подключаемый модуль учетных данных завершил работу с ошибкой 1/ошибка при скачивании пакета при использовании поставщиков учетных данных с несколькими источниками [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="be54b-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="be54b-215">`project.json` Восстановление NuGet вызывает повторную компиляцию при отсутствии изменений [#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="be54b-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="be54b-216">Пакеты символов не следует использовать при установке или обновлении — [#2807](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="be54b-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="be54b-217">VS не поддерживает переменные среды в Репоситорипас (nuget.exe) — [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="be54b-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="be54b-218">Пометка элементов UIElement без метки в пользовательском интерфейсе диспетчера пакетов для специальных возможностей — [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="be54b-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="be54b-219">Переносные платформы с профилем переноса переносов отклоняются.</span><span class="sxs-lookup"><span data-stu-id="be54b-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="be54b-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="be54b-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="be54b-221">Диспетчер пакетов NuGet должен очистить, что список параметров в сведениях о пакетах не применяется к `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="be54b-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="be54b-222">nuget.exe принудительная отправка или удаление не использует ключ API — [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="be54b-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="be54b-223">Удалите свойство locked из файла блокировки — [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="be54b-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="be54b-224">Сбой обновления 3.3.0 NuGet с "дополнительным ограничением... определено в packages.config не разрешает эту операцию. "</span><span class="sxs-lookup"><span data-stu-id="be54b-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="be54b-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="be54b-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="be54b-226">При установке пакета из локального источника, который не существует, выдается фиктивное сообщение — [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="be54b-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="be54b-227">В фильтре "обновление доступно" отображаются обновления, нарушающие ограничение версии — [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="be54b-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="be54b-228">Не удалось обновить собственные пакеты — [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="be54b-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="be54b-229">Компоненты</span><span class="sxs-lookup"><span data-stu-id="be54b-229">Features</span></span>

* <span data-ttu-id="be54b-230">Поддержка установки свойства CopyLocal в значение false для ссылок, добавляемых NuGet- [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="be54b-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="be54b-231">Поддержка nuget.exe для MSBuild 15- [#1937](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="be54b-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="be54b-232">Поддержка Pack для.`csproj`</span><span class="sxs-lookup"><span data-stu-id="be54b-232">Pack support for .`csproj`</span></span><span data-ttu-id="be54b-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="be54b-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="be54b-234">Отключить действие пользователя при выполнении действий пользователя — [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="be54b-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="be54b-235">NuGet должен добавить поддержку для `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="be54b-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="be54b-236">Добавлена совместимость платформы в NuGet 2. x (которые уже находятся в 3. x) — [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="be54b-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="be54b-237">Поддержка резервных папок пакетов — [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="be54b-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="be54b-238">Разработайте и реализуйте понятие типа пакета для поддержки пакетов средств — [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="be54b-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="be54b-239">Добавьте API, чтобы получить путь к папке глобальных пакетов — [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="be54b-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="be54b-240">Включение SemVer 2.0.0 в пакетной [#3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="be54b-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="be54b-241">Запросы на изменение структуры</span><span class="sxs-lookup"><span data-stu-id="be54b-241">DCRs</span></span>

* <span data-ttu-id="be54b-242">nuget.exe параметр времени ожидания push-уведомлений не работает [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="be54b-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="be54b-243">Текст описания пакета должен быть выбираемым [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="be54b-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="be54b-244">Разрешить nuget.exe создавать `.props` и `.targets` файлы для `.nuproj` проектов [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="be54b-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="be54b-245">Добавление API расширяемости для сравнения платформ с помощью Imports- [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="be54b-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="be54b-246">Скрывать параметры зависимости при использовании `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="be54b-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="be54b-247">Вывод заголовка nuget.exe версии в подробных выходных данных — [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="be54b-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="be54b-248">NuGet должен уведомить пользователей о том, что обновление или установка в PCL TFM на основе библиотеки, может вызвать проблемы. [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="be54b-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="be54b-249">Предупреждать о неправильной установке или обновлении для проекта w/TFM = "DotNet" — [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="be54b-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="be54b-250">Устранение проблем с производительностью с помощью сопоставителя и NuGet для обновления [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="be54b-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="be54b-251">Добавление поддержки netcoreapp11 и netstandard17 — [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="be54b-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="be54b-252">Использование атрибута AssemblyMetadata для `.nuspec` замены токенов — [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="be54b-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
