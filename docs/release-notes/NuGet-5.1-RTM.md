---
title: Заметки о выпуске NuGet 5,1 RTM
description: Заметки о выпуске NuGet 5,1, включая новые функции, исправления ошибок и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: d6f6bffc6b5fda9ee1b9d9830f6d7d3c0f5be654
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780140"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="bacfc-103">Заметки о выпуске NuGet 5,1</span><span class="sxs-lookup"><span data-stu-id="bacfc-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="bacfc-104">Средства распространения NuGet:</span><span class="sxs-lookup"><span data-stu-id="bacfc-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="bacfc-105">Версия NuGet</span><span class="sxs-lookup"><span data-stu-id="bacfc-105">NuGet version</span></span> | <span data-ttu-id="bacfc-106">Доступно в версии Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bacfc-106">Available in Visual Studio version</span></span>| <span data-ttu-id="bacfc-107">Доступно в пакетах SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="bacfc-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="bacfc-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="bacfc-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="bacfc-109">Visual Studio 2019 версии 16.1</span><span class="sxs-lookup"><span data-stu-id="bacfc-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="bacfc-110">[2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="bacfc-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="bacfc-111"><sup>1</sup> Устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core</span><span class="sxs-lookup"><span data-stu-id="bacfc-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="bacfc-112"><sup>2</sup> Доступно в качестве необязательной установки с помощью Visual Studio 2019 с рабочей нагрузкой .NET Core</span><span class="sxs-lookup"><span data-stu-id="bacfc-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="bacfc-113">Сводка: новые возможности в 5,1</span><span class="sxs-lookup"><span data-stu-id="bacfc-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="bacfc-114">Поддержка пропуска отправки пакета, если он уже существует, чтобы обеспечить лучшую интеграцию с рабочими процессами CI/CD. [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="bacfc-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="bacfc-115">Теперь Visual Studio предоставляет удобную ссылку на страницу коллекции nuget.org пакета — [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="bacfc-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="bacfc-116">Поддержка новых ресурсов .NET Core 3,0, таких как [Целевые пакеты](https://github.com/dotnet/cli/issues/10006) и [пакеты среды выполнения](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="bacfc-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="bacfc-117">Поддержка пакета NuGet и восстановления для Фрамеворкреференцес для включения целевых объектов и ссылок на пакеты среды выполнения — [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="bacfc-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="bacfc-118">Поддержка сценария пакета "только для загрузки" с Паккажедовнлоад- [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="bacfc-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="bacfc-119">Исключите среду выполнения и целевые пакеты из результатов поиска & восстановить граф с помощью PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="bacfc-119">Exclude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="bacfc-120">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="bacfc-120">Issues fixed in this release</span></span>

<span data-ttu-id="bacfc-121">**Ошибки**</span><span class="sxs-lookup"><span data-stu-id="bacfc-121">**Bugs**</span></span>

* <span data-ttu-id="bacfc-122">Подключаемые модули: сведения об исключении теряются во время создания подключаемого модуля — [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="bacfc-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="bacfc-123">Диапазон PackageReference с исключающей нижней границей не работает, если нижняя граница существует в одном из источников.</span><span class="sxs-lookup"><span data-stu-id="bacfc-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="bacfc-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="bacfc-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="bacfc-125">Улучшение сообщения Испаккаблефалсиррор — [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="bacfc-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="bacfc-126">Пакеты заблокировать файл — повторно создать файл блокировки при изменении графа проекта — [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="bacfc-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="bacfc-127">Прожектсистем ошибка: пакеты NuGet, получив автоматическое удаление — [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="bacfc-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="bacfc-128">Добавьте целевой объект для возврата Фрамеворкреференце, аналогичного Коллектпаккажедовнлоадс и Коллектпаккажереференцес- [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="bacfc-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="bacfc-129">Кэш HTTP: ресурс Репоситориресаурцес не кэшируется с помощью версии [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="bacfc-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="bacfc-130">Ведение журнала: исключение стеки вызовов не сообщается с подробным уровнем детализации — [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="bacfc-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="bacfc-131">Изменение всех URL-адресов документов NuGet для использования HTTPS — [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="bacfc-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="bacfc-132">Улучшение предупреждающего сообщения NU3024 — [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="bacfc-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="bacfc-133">блокировка файла не обновляется, когда packagereference удалена — [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="bacfc-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="bacfc-134">Улучшение обработки вариантов ошибок при проверке элемента licenseurl и License в nuspec- [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="bacfc-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="bacfc-135">Пользовательский интерфейс PM. Щелкните правой кнопкой мыши заголовок вкладки и выберите пункт "открыть расположение файла", что приведет к ошибке- [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="bacfc-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="bacfc-136">Подключаемые модули: заносить в журнал, когда завершается процесс подключаемого модуля — [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="bacfc-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="bacfc-137">Подключаемые модули: высокая частота конфликтов при ведении журнала значений даты и времени — [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="bacfc-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="bacfc-138">Сбой manifest. ReadFrom в любой nuspec с Лиценсикспрессион- [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="bacfc-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="bacfc-139">Ресторелоккедмоде: непредвиденный NU1004, когда ProjectReference ссылается на проект с настраиваемым AssemblyName- [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="bacfc-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="bacfc-140">Более эффективное сообщение об ошибке при сбое запуска подключаемого модуля с исключением [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="bacfc-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="bacfc-141">При выполнении восстановления NoOp Избегайте использования \* .dgspec.jsпри записи в каталоге obj — [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="bacfc-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="bacfc-142">Женератепаспроперти = true: не удается создать свойство при несоответствии регистра — [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="bacfc-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="bacfc-143">Параметры: недопустимый символ в исходном пути пакета может привести к сбою в VS- [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="bacfc-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="bacfc-144">Если файл блокировки удален, инструкция RESTORE не создает файл блокировки на NoOp- [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="bacfc-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="bacfc-145">URL-адрес лицензии и лицензия приводит к ошибке чтения с помощью метаданных [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="bacfc-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="bacfc-146">Необработанные исключения в V2FeedParser — [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="bacfc-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="bacfc-147">nuget.exe возвращает нулевой код выхода для недопустимых аргументов — [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="bacfc-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="bacfc-148">Ошибки обновления и документация по предупреждениям, отражающие сценарии, связанные с подписыванием. [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="bacfc-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="bacfc-149">Для упрощения перемещения проектов в файле ресурсов следует использовать относительные пути [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="bacfc-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="bacfc-150">**Запросы на изменение структуры**</span><span class="sxs-lookup"><span data-stu-id="bacfc-150">**DCRs**</span></span>

* <span data-ttu-id="bacfc-151">Подключаемые модули: Включение ведения журнала диагностики — [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="bacfc-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="bacfc-152">Создайте карту Tizen 6 на NetStandard 2,1- [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="bacfc-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="bacfc-153">**[Список всех проблем, исправленных в этом выпуске — 5,1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="bacfc-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
