---
title: Команда установки интерфейса командной строки NuGet
description: Справочник по команде nuget.exe install
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 34b79bfa7a0dddf5da6b5c465293caec49129f6c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779270"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="0c6ec-103">команда install (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="0c6ec-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="0c6ec-104">Область **применения:** &bullet; **Поддерживаемые версии** для использования пакетов: все</span><span class="sxs-lookup"><span data-stu-id="0c6ec-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="0c6ec-105">Скачивает и устанавливает пакет в проект по умолчанию для текущей папки с использованием указанных источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="0c6ec-106">Чтобы загрузить пакет непосредственно за пределами контекста проекта, посетите страницу пакета на сайте [NuGet.org](https://www.nuget.org) и выберите ссылку для **скачивания** .</span><span class="sxs-lookup"><span data-stu-id="0c6ec-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="0c6ec-107">Если источники не указаны, используются указанные в глобальном файле конфигурации `%appdata%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="0c6ec-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="0c6ec-108">Дополнительные сведения см. в разделе [Общие конфигурации NuGet](../../consume-packages/configuring-nuget-behavior.md) .</span><span class="sxs-lookup"><span data-stu-id="0c6ec-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="0c6ec-109">Если конкретные пакеты не указаны, `install` устанавливает все пакеты, перечисленные в `packages.config` файле проекта, делая его похожим на [`restore`](cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="0c6ec-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="0c6ec-110">`install`Команда не изменяет файл проекта или `packages.config` ; в этом случае он похож на тот `restore` , что он добавляет только пакеты на диск, но не изменяет зависимости проекта.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="0c6ec-111">Чтобы добавить зависимость, либо добавьте пакет через пользовательский интерфейс или консоль диспетчера пакетов в Visual Studio, либо измените, `packages.config` а затем запустите либо `install` `restore` .</span><span class="sxs-lookup"><span data-stu-id="0c6ec-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="0c6ec-112">Использование</span><span class="sxs-lookup"><span data-stu-id="0c6ec-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="0c6ec-113">где `<packageID>` имя устанавливаемого пакета (с использованием последней версии) или `<configFilePath>` файл, в котором `packages.config` перечислены пакеты для установки.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="0c6ec-114">Можно указать конкретную версию с помощью `-Version` параметра.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="0c6ec-115">Варианты</span><span class="sxs-lookup"><span data-stu-id="0c6ec-115">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="0c6ec-116">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="0c6ec-117">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="0c6ec-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DependencyVersion`**

  <span data-ttu-id="0c6ec-118">*(4.4 +)* Используемая версия пакетов зависимостей, которая может быть одной из следующих:</span><span class="sxs-lookup"><span data-stu-id="0c6ec-118">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="0c6ec-119">*Самый низкий* (по умолчанию): самая низкая версия</span><span class="sxs-lookup"><span data-stu-id="0c6ec-119">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="0c6ec-120">*Хигхестпатч*: версия с наименьшим основным, наименьшим незначительным, самым высоким исправлением</span><span class="sxs-lookup"><span data-stu-id="0c6ec-120">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="0c6ec-121">*Хигхестминор*: версия с наименьшим основным, наибольшим незначительным, самым высоким исправлением</span><span class="sxs-lookup"><span data-stu-id="0c6ec-121">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="0c6ec-122">*Наибольшее*: самая высокая версия</span><span class="sxs-lookup"><span data-stu-id="0c6ec-122">*Highest*: the highest version</span></span></li><li><span data-ttu-id="0c6ec-123">*Ignore*: пакеты зависимостей не будут использоваться</span><span class="sxs-lookup"><span data-stu-id="0c6ec-123">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-DirectDownload`**

  <span data-ttu-id="0c6ec-124">Скачайте напрямую, не заполняя никакие кэши метаданными или двоичными файлами.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-124">Download directly without populating any caches with metadata or binaries.</span></span>

- **`-DisableParallelProcessing`**

  <span data-ttu-id="0c6ec-125">Отключает параллельную установку нескольких пакетов.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-125">Disables installing multiple packages in parallel.</span></span>

- **`-x|-ExcludeVersion`**

  <span data-ttu-id="0c6ec-126">Устанавливает пакет в папку с именем только с именем пакета, а не с номером версии.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-126">Installs the package to a folder named with only the package name and not the version number.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="0c6ec-127">*(3.2 +)* Список источников пакетов, используемых в качестве резервных при условии, что пакет не найден в основном источнике или по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-127">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="0c6ec-128">*(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Framework`**

  <span data-ttu-id="0c6ec-129">*(4.4 +)* Целевая платформа, используемая для выбора зависимостей.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-129">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="0c6ec-130">Если не указано, по умолчанию используется значение Any.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-130">Defaults to 'Any' if not specified.</span></span>

- **`-?|-help`**

  <span data-ttu-id="0c6ec-131">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-131">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="0c6ec-132">Предотвращает использование кэшированных пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="0c6ec-133">См. раздел [Управление глобальными пакетами и папками кэша](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="0c6ec-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="0c6ec-134">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="0c6ec-135">Указывает папку, в которой устанавливаются пакеты.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="0c6ec-136">Если папка не указана, используется текущая папка.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-136">If no folder is specified, the current folder is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="0c6ec-137">Указывает типы файлов, которые необходимо сохранить после установки пакета: один из `nuspec` , `nupkg` или `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="0c6ec-137">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="0c6ec-138">Разрешает установку пакетов предварительного выпуска.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-138">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="0c6ec-139">Этот флаг не требуется при восстановлении пакетов с помощью `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="0c6ec-139">This flag is not required when restoring packages with `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="0c6ec-140">Проверяет, что восстановление пакетов включено перед загрузкой и установкой пакетов.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-140">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="0c6ec-141">Дополнительные сведения см. в разделе [восстановление пакетов](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="0c6ec-141">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="0c6ec-142">Указывает корневую папку решения, для которого восстанавливаются пакеты.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-142">Specifies root folder of the solution for which to restore packages.</span></span>

- **`-Source`**

   <span data-ttu-id="0c6ec-143">Указывает список источников пакетов (в виде URL-адресов) для использования.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-143">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="0c6ec-144">Если этот параметр не указан, команда использует источники, предоставленные в файлах конфигурации, см. раздел [Общие конфигурации NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="0c6ec-144">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="0c6ec-145">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="0c6ec-145">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="0c6ec-146">Указывает версию устанавливаемого пакета.</span><span class="sxs-lookup"><span data-stu-id="0c6ec-146">Specifies the version of the package to install.</span></span>

<span data-ttu-id="0c6ec-147">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0c6ec-147">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0c6ec-148">Примеры</span><span class="sxs-lookup"><span data-stu-id="0c6ec-148">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
