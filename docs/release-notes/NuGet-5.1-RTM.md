---
ms.openlocfilehash: 48306e77a017c11fa7dc0d695e0177edf4e79d1e
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/21/2019
ms.locfileid: "65975838"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="72c82-101">Заметки о выпуске 5.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="72c82-101">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="72c82-102">Средства распространения NuGet:</span><span class="sxs-lookup"><span data-stu-id="72c82-102">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="72c82-103">Версия NuGet</span><span class="sxs-lookup"><span data-stu-id="72c82-103">NuGet version</span></span> | <span data-ttu-id="72c82-104">Доступно в версии Visual Studio</span><span class="sxs-lookup"><span data-stu-id="72c82-104">Available in Visual Studio version</span></span>| <span data-ttu-id="72c82-105">Доступно в пакетах SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="72c82-105">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="72c82-106">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="72c82-106">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="72c82-107">Версия 16.1 2019 г. Visual Studio</span><span class="sxs-lookup"><span data-stu-id="72c82-107">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="72c82-108">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="72c82-108">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="72c82-109"><sup>1</sup>устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core</span><span class="sxs-lookup"><span data-stu-id="72c82-109"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="72c82-110"><sup>2</sup>доступно в виде необязательно установку с помощью Visual Studio 2019 с рабочей нагрузкой .NET Core</span><span class="sxs-lookup"><span data-stu-id="72c82-110"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="72c82-111">Сводка: Новые возможности в версии 5.1</span><span class="sxs-lookup"><span data-stu-id="72c82-111">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="72c82-112">Поддержка для пропуска отправка пакета, если он уже существует для обеспечения более эффективную интеграцию с Непрерывной интеграции и рабочие процессы — [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="72c82-112">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="72c82-113">Visual Studio предоставляет удобную ссылку на страницу коллекции nuget.org пакета - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="72c82-113">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="72c82-114">Поддержка новых средств .NET Core 3.0, таких как [целевые пакеты](https://github.com/dotnet/cli/issues/10006) и [пакеты среды выполнения](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="72c82-114">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="72c82-115">Pack и restore NuGet поддержка FrameworkReferences для включения целевая и среды выполнения ссылки на пакет - [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="72c82-115">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="72c82-116">«Скачать только» пакет сценарию поддержки с PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="72c82-116">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="72c82-117">Среда выполнения Exlcude и целевые пакеты в результатах поиска и восстановления граф с использованием PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="72c82-117">Exlcude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="72c82-118">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="72c82-118">Issues fixed in this release</span></span>

<span data-ttu-id="72c82-119">**Ошибки**</span><span class="sxs-lookup"><span data-stu-id="72c82-119">**Bugs**</span></span>

* <span data-ttu-id="72c82-120">Подключаемые модули: сведения об исключении потеряны во время создания подключаемого модуля - [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="72c82-120">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="72c82-121">Диапазон PackageReference с эксклюзивные нижняя граница не работает, если нижняя граница присутствует на один из источников.</span><span class="sxs-lookup"><span data-stu-id="72c82-121">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="72c82-122"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="72c82-122"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="72c82-123">Улучшить сообщение IsPackableFalseError - [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="72c82-123">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="72c82-124">Блокировка файла - файле повторное создание блокировки при изменении схемы проекта — [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="72c82-124">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="72c82-125">Ошибка ProjectSystem: Удалено пакетов NuGet, получение auto - [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="72c82-125">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="72c82-126">Добавить целевой объект для возвращения FrameworkReference аналогичную CollectPackageDownloads и CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="72c82-126">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="72c82-127">Кэш HTTP:  RepositoryResources ресурсов не кэшируется с версиями образом - [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="72c82-127">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="72c82-128">Ведение журнала: исключение стеки вызовов, не передаются с подробным уровнем детализации - [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="72c82-128">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="72c82-129">Изменить все NuGet документация URL-адреса для использования протокола HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="72c82-129">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="72c82-130">Улучшить NU3024 предупреждающее сообщение - [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="72c82-130">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="72c82-131">Файл блокировки не обновляется при packagereference removed — [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="72c82-131">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="72c82-132">Улучшения вариантов обработки ошибок при проверке элемента licenseurl и лицензии в nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="72c82-132">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="72c82-133">Пользовательского интерфейса PM - щелкните правой кнопкой мыши заголовок вкладки и выберите команду «Открыть расположение файла» приведет к ошибке - [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="72c82-133">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="72c82-134">Подключаемые модули: журнал при завершении работы подключаемого модуля процесса - [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="72c82-134">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="72c82-135">Подключаемые модули: частота высокой конфликтов в значения даты и времени для ведения журнала - [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="72c82-135">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="72c82-136">Manifest.ReadFrom завершается сбоем в любой nuspec с LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="72c82-136">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="72c82-137">RestoreLockedMode: Непредвиденная NU1004 при ProjectReference ссылается на проект с помощью пользовательских AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="72c82-137">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="72c82-138">Улучшенное сообщение об ошибке при сбое запуска подключаемого модуля с исключением - [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="72c82-138">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="72c82-139">При выполнении восстановления NoOp, избегайте использования \*. dgspec.json записи в каталоге obj - [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="72c82-139">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="72c82-140">GeneratePathProperty = true не удается создать свойство на несоответствие регистра - [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="72c82-140">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="72c82-141">Параметры: недопустимый символ в исходный путь к пакету могут вызвать сбой VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="72c82-141">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="72c82-142">Если удаляется файл блокировки, восстановление не создает файл блокировки на NoOp - [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="72c82-142">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="72c82-143">URL-адрес лицензии и лицензии причины, ошибка с метаданными - чтения [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="72c82-143">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="72c82-144">Необработанные исключения в V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="72c82-144">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="72c82-145">NuGet.exe возвращает нулевой код выхода для недопустимые аргументы - [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="72c82-145">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="72c82-146">Обновление ошибки и предупреждение документация, в соответствии с подписи связанные сценарии - [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="72c82-146">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="72c82-147">Файл ресурсов следует использовать относительные пути для включения более легко - проектами [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="72c82-147">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="72c82-148">**Запросы на изменение структуры**</span><span class="sxs-lookup"><span data-stu-id="72c82-148">**DCRs**</span></span>

* <span data-ttu-id="72c82-149">Подключаемые модули: включить ведение журнала диагностики - [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="72c82-149">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="72c82-150">Создание Tizen 6 сопоставляются NetStandard 2.1 — [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="72c82-150">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="72c82-151">**[Список всех проблем, исправленных в этом выпуске — 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="72c82-151">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
