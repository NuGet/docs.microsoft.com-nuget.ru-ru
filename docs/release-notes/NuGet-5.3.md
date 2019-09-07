---
title: Заметки о выпуске NuGet 5,3
description: Заметки о выпуске NuGet 5,3, включая новые функции, исправления ошибок и DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: f16bfe5481009f7924a61f03233d288d25ac618f
ms.sourcegitcommit: f4bfdbf62302c95f1f39e81ccf998f8bbc6d56b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2019
ms.locfileid: "70774089"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="96f9c-103">Заметки о выпуске NuGet 5,3</span><span class="sxs-lookup"><span data-stu-id="96f9c-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="96f9c-104">Средства распространения NuGet:</span><span class="sxs-lookup"><span data-stu-id="96f9c-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="96f9c-105">Версия NuGet</span><span class="sxs-lookup"><span data-stu-id="96f9c-105">NuGet version</span></span> | <span data-ttu-id="96f9c-106">Доступно в версии Visual Studio</span><span class="sxs-lookup"><span data-stu-id="96f9c-106">Available in Visual Studio version</span></span>| <span data-ttu-id="96f9c-107">Доступно в пакетах SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="96f9c-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="96f9c-108">**5.3.0 — preview3**</span><span class="sxs-lookup"><span data-stu-id="96f9c-108">**5.3.0-preview3**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="96f9c-109">Visual Studio 2019 версии 16,3, предварительная версия 3</span><span class="sxs-lookup"><span data-stu-id="96f9c-109">Visual Studio 2019 version 16.3 Preview 3</span></span>](https://visualstudio.microsoft.com/vs/preview/) | <span data-ttu-id="96f9c-110">[3.0.100 — preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0) <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="96f9c-110">[3.0.100-preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |

<span data-ttu-id="96f9c-111"><sup>1</sup> Устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core</span><span class="sxs-lookup"><span data-stu-id="96f9c-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53-preview-3"></a><span data-ttu-id="96f9c-112">Сводка: Новые возможности 5,3 Preview 3</span><span class="sxs-lookup"><span data-stu-id="96f9c-112">Summary: What's New in 5.3 preview 3</span></span>

* <span data-ttu-id="96f9c-113">[Значок пакета можно встроить в пакет](../reference/msbuild-targets.md#packing-an-icon-image-file), вместо того чтобы использовать внешний URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="96f9c-113">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="96f9c-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="96f9c-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="96f9c-115">Улучшенная безопасность с помощью отслеживания и применения SHA для Packages. config — [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="96f9c-115">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="96f9c-116">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="96f9c-116">Issues fixed in this release</span></span>

<span data-ttu-id="96f9c-117">**Ошибки**</span><span class="sxs-lookup"><span data-stu-id="96f9c-117">**Bugs**</span></span>

* <span data-ttu-id="96f9c-118">VS: сборки полностью являются NGen-ED, а не частично NGen-ED- [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="96f9c-118">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="96f9c-119">Уменьшение использования памяти (Отмена подписки на события) — [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="96f9c-119">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="96f9c-120">Сообщение "Error_UnableToFindProjectInfo" не является правильным грамматически — [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="96f9c-120">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="96f9c-121">Улучшения NU1403 — проверка всех пакетов, включение ожидаемых/фактических значений SHA — [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="96f9c-121">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="96f9c-122">Множественное перечисление в Нужетпаккажеманажер. Превиевупдатепаккажесасинк- [#8401](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="96f9c-122">Multiple enumeration in NuGetPackageManager.PreviewUpdatePackagesAsync - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="96f9c-123">Отмена изменений "Public-> internal" в Плугинпроцесс- [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="96f9c-123">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="96f9c-124">Ивспаккажесаурцепровидер.-источники (...) имеют неверно определенное поведение исключений — [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="96f9c-124">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="96f9c-125">Снова сделать конструктор Плугинманажер открытым — [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="96f9c-125">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="96f9c-126">Метрики для контроля частоты обновления пользовательского интерфейса PM — [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="96f9c-126">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="96f9c-127">Уменьшение числа обновлений пользовательского интерфейса при установке с помощью пользовательского интерфейса диспетчера пакетов — [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="96f9c-127">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="96f9c-128">Данные телеметрии: значения DateTime используют форматы, зависящие от языка и региональных параметров. [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="96f9c-128">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="96f9c-129">Сокращение числа обновлений пользовательского интерфейса на вкладке Обзор в пользовательском интерфейсе диспетчера пакетов #6570 — [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="96f9c-129">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="96f9c-130">[Сбой теста] "Не удалось проанализировать файл конфигурации" будет предложено дважды [#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="96f9c-130">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="96f9c-131">Порождение ошибки NU5037 на странице с хорошим документом, в которой объясняются исправления клиентов (в пакете отсутствует необходимый файл nuspec) — [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="96f9c-131">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="96f9c-132">Не удается выполнить восстановление в заблокированном режиме при изменении Рунтимеидентифиер проекта — [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="96f9c-132">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="96f9c-133">Сделайте чтение параметров в VS Lazy- [#8156](https://github.com/NuGet/Home/issues/8156)</span><span class="sxs-lookup"><span data-stu-id="96f9c-133">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="96f9c-134">Регрессия в "Добавление источников NuGet" приводит к тому, что символ ":", шестнадцатеричное значение 0x3A, не может быть добавлен в имя "Errors- [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="96f9c-134">Regression in 'Nuget sources add' causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="96f9c-135">Поставщики учетных данных подключаемого модуля NuGet — скрытие окна процесса — [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="96f9c-135">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="96f9c-136">Принудительное применение Паккажепасресолвер является абсолютным путем [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="96f9c-136">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="96f9c-137">Сокращение числа обновлений пользовательского интерфейса на вкладках Установка и обновление пользовательского интерфейса диспетчера пакетов — [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="96f9c-137">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="96f9c-138">**Запрос на изменение структуры:**</span><span class="sxs-lookup"><span data-stu-id="96f9c-138">**DCR:**</span></span>

* <span data-ttu-id="96f9c-139">Обновление платформ Xamarin для соотнесения с NetStandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="96f9c-139">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="96f9c-140">Включить копирование содержимого окна предварительного просмотра диспетчера пакетов для установки или обновления — [#8324](https://github.com/NuGet/Home/issues/8324)</span><span class="sxs-lookup"><span data-stu-id="96f9c-140">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="96f9c-141">Включение восстановления в proj-файлах — [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="96f9c-141">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="96f9c-142">Представляем `NUGET_NETFX_PLUGIN_PATHS` и`NUGET_NETCORE_PLUGIN_PATHS` для поддержки конфигурации обоих элементов одновременно — [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="96f9c-142">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="96f9c-143">Включение нескольких версий для Паккажедовнлоад с помощью атрибута версии — [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="96f9c-143">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="96f9c-144">Добавление параметров-Солутиондиректори и-Паккажедиректори в NuGet. exe Pack — [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="96f9c-144">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

* <span data-ttu-id="96f9c-145">Включение детерминированного пакета NuGet — [#6229](https://github.com/NuGet/Home/issues/6229)</span><span class="sxs-lookup"><span data-stu-id="96f9c-145">Enable NuGet Pack to be deterministic - [#6229](https://github.com/NuGet/Home/issues/6229)</span></span>

<span data-ttu-id="96f9c-146">**[Список всех проблем, исправленных в этом выпуске — 5,3 Preview 3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="96f9c-146">**[List of all issues fixed in this release - 5.3 preview 3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>
