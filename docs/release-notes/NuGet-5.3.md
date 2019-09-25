---
title: Заметки о выпуске NuGet 5,3
description: Заметки о выпуске NuGet 5,3, включая новые функции, исправления ошибок и DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 96d176beaa6b2f0c4f53488390e585b70c9ba846
ms.sourcegitcommit: 188ade66b7ac807ba1667c77cfb9325bf89a8a4a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2019
ms.locfileid: "71248163"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="ecc82-103">Заметки о выпуске NuGet 5,3</span><span class="sxs-lookup"><span data-stu-id="ecc82-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="ecc82-104">Средства распространения NuGet:</span><span class="sxs-lookup"><span data-stu-id="ecc82-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="ecc82-105">Версия NuGet</span><span class="sxs-lookup"><span data-stu-id="ecc82-105">NuGet version</span></span> | <span data-ttu-id="ecc82-106">Доступно в версии Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ecc82-106">Available in Visual Studio version</span></span>| <span data-ttu-id="ecc82-107">Доступно в пакетах SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="ecc82-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="ecc82-108">**5.3.0**</span><span class="sxs-lookup"><span data-stu-id="ecc82-108">**5.3.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="ecc82-109">Visual Studio 2019 версии 16,3</span><span class="sxs-lookup"><span data-stu-id="ecc82-109">Visual Studio 2019 version 16.3</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="ecc82-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0) <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="ecc82-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |

<span data-ttu-id="ecc82-111"><sup>1</sup> Устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core</span><span class="sxs-lookup"><span data-stu-id="ecc82-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53"></a><span data-ttu-id="ecc82-112">Сводка: Новые возможности в 5,3</span><span class="sxs-lookup"><span data-stu-id="ecc82-112">Summary: What's New in 5.3</span></span>

* <span data-ttu-id="ecc82-113">[Значок пакета можно встроить в пакет](../reference/msbuild-targets.md#packing-an-icon-image-file), вместо того чтобы использовать внешний URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="ecc82-113">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="ecc82-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="ecc82-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="ecc82-115">Улучшенная безопасность с помощью отслеживания и применения SHA для Packages. config — [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="ecc82-115">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ecc82-116">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="ecc82-116">Issues fixed in this release</span></span>

<span data-ttu-id="ecc82-117">**Ошибки**</span><span class="sxs-lookup"><span data-stu-id="ecc82-117">**Bugs**</span></span>

* <span data-ttu-id="ecc82-118">Пакеты NuGet, созданные с помощью пакета SDK 3.0.100-preview9, не могут использоваться пользователями пакета SDK 2,2... в зависимости от часового пояса [#8603](https://github.com/NuGet/Home/issues/8603)</span><span class="sxs-lookup"><span data-stu-id="ecc82-118">NuGet packages produced with 3.0.100-preview9 SDK cannot be used by 2.2 SDK users...depending on your timezone [#8603](https://github.com/NuGet/Home/issues/8603)</span></span>

* <span data-ttu-id="ecc82-119">Кавычки "символы в пути приводят к сбою" недопустимых `nuget restore` символов в пути "в [#8168](https://github.com/NuGet/Home/issues/8168)</span><span class="sxs-lookup"><span data-stu-id="ecc82-119">Quote " characters in PATH cause "Illegal characters in path" failure in `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span></span>

* <span data-ttu-id="ecc82-120">VS: сборки полностью являются NGen-ED, а не частично NGen-ED- [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="ecc82-120">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="ecc82-121">Уменьшение использования памяти (Отмена подписки на события) — [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="ecc82-121">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="ecc82-122">Сообщение "Error_UnableToFindProjectInfo" не является правильным грамматически — [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="ecc82-122">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="ecc82-123">Улучшения NU1403 — проверка всех пакетов, включение ожидаемых/фактических значений SHA — [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="ecc82-123">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="ecc82-124">Множественное перечисление в `NuGetPackageManager.PreviewUpdatePackagesAsync` [#8401](https://github.com/NuGet/Home/issues/8401)  - </span><span class="sxs-lookup"><span data-stu-id="ecc82-124">Multiple enumeration in `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="ecc82-125">Отмена изменений "Public-> internal" в Плугинпроцесс- [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="ecc82-125">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="ecc82-126">Ивспаккажесаурцепровидер.-источники (...) имеют неверно определенное поведение исключений — [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="ecc82-126">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="ecc82-127">Снова сделать конструктор Плугинманажер открытым — [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="ecc82-127">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="ecc82-128">Метрики для контроля частоты обновления пользовательского интерфейса PM — [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="ecc82-128">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="ecc82-129">Уменьшение числа обновлений пользовательского интерфейса при установке с помощью пользовательского интерфейса диспетчера пакетов — [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="ecc82-129">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="ecc82-130">Данные телеметрии: значения DateTime используют форматы, зависящие от языка и региональных параметров. [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="ecc82-130">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="ecc82-131">Сокращение числа обновлений пользовательского интерфейса на вкладке Обзор в пользовательском интерфейсе диспетчера пакетов #6570 — [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="ecc82-131">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="ecc82-132">[Сбой теста] "Не удалось проанализировать файл конфигурации" будет предложено дважды [#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="ecc82-132">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="ecc82-133">Порождение ошибки NU5037 на странице с хорошим документом, в которой объясняются исправления клиентов (в пакете отсутствует необходимый файл nuspec) — [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="ecc82-133">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="ecc82-134">Не удается выполнить восстановление в заблокированном режиме при изменении Рунтимеидентифиер проекта — [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="ecc82-134">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="ecc82-135">Сделайте чтение параметров в VS Lazy- [#8156](https://github.com/NuGet/Home/issues/8156)</span><span class="sxs-lookup"><span data-stu-id="ecc82-135">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="ecc82-136">Регрессия в `Nuget sources add` приводит к тому, что символ ":", шестнадцатеричное значение 0x3A, не может быть добавлен в имя "Errors- [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="ecc82-136">Regression in `Nuget sources add` causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="ecc82-137">Поставщики учетных данных подключаемого модуля NuGet — скрытие окна процесса — [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="ecc82-137">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="ecc82-138">Принудительное применение Паккажепасресолвер является абсолютным путем [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="ecc82-138">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="ecc82-139">Сокращение числа обновлений пользовательского интерфейса на вкладках Установка и обновление пользовательского интерфейса диспетчера пакетов — [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="ecc82-139">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="ecc82-140">**Запрос на изменение структуры:**</span><span class="sxs-lookup"><span data-stu-id="ecc82-140">**DCR:**</span></span>

* <span data-ttu-id="ecc82-141">Обновление платформ Xamarin для соотнесения с NetStandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="ecc82-141">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="ecc82-142">Включить копирование содержимого окна предварительного просмотра диспетчера пакетов для установки или обновления — [#8324](https://github.com/NuGet/Home/issues/8324)</span><span class="sxs-lookup"><span data-stu-id="ecc82-142">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="ecc82-143">Включение восстановления в proj-файлах — [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="ecc82-143">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="ecc82-144">Представляем `NUGET_NETFX_PLUGIN_PATHS` и`NUGET_NETCORE_PLUGIN_PATHS` для поддержки конфигурации обоих элементов одновременно — [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="ecc82-144">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="ecc82-145">Включение нескольких версий для Паккажедовнлоад с помощью атрибута версии — [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="ecc82-145">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="ecc82-146">Добавление параметров-Солутиондиректори и-Паккажедиректори в NuGet. exe Pack — [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="ecc82-146">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

<span data-ttu-id="ecc82-147">**[Список всех проблем, исправленных в этом выпуске — 5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="ecc82-147">**[List of all issues fixed in this release - 5.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>
