---
title: Команда восстановления интерфейса командной строки NuGet
description: Справочник по команде nuget.exe Restore
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 108317aba2107948180ab0149c0c5ba5150cf9b8
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622834"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="89275-103">команда Restore (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="89275-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="89275-104">Область **применения:** &bullet; **Поддерживаемые версии** для использования пакетов: 2.7 +</span><span class="sxs-lookup"><span data-stu-id="89275-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="89275-105">Скачивает и устанавливает все пакеты, отсутствующие в `packages` папке.</span><span class="sxs-lookup"><span data-stu-id="89275-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="89275-106">При использовании с NuGet 4.0 + и форматом PackageReference при необходимости создает `<project>.nuget.props` файл в `obj` папке.</span><span class="sxs-lookup"><span data-stu-id="89275-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="89275-107">(Файл можно опустить из системы управления версиями.)</span><span class="sxs-lookup"><span data-stu-id="89275-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="89275-108">В Mac OSX и Linux с интерфейсом командной строки в Mono восстановление пакетов с помощью PackageReference не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="89275-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="89275-109">Использование</span><span class="sxs-lookup"><span data-stu-id="89275-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="89275-110">где `<projectPath>` указывает расположение решения или `packages.config` файла.</span><span class="sxs-lookup"><span data-stu-id="89275-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="89275-111">Подробные сведения о поведении см. в разделе [Примечания](#remarks) ниже.</span><span class="sxs-lookup"><span data-stu-id="89275-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="89275-112">Параметры</span><span class="sxs-lookup"><span data-stu-id="89275-112">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="89275-113">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="89275-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="89275-114">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="89275-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DirectDownload`**

  <span data-ttu-id="89275-115">*(4.0 +)* Скачивает пакеты напрямую, не заполняя кэши двоичными файлами или метаданными.</span><span class="sxs-lookup"><span data-stu-id="89275-115">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span>

- **`-DisableParallelProcessing`**

   <span data-ttu-id="89275-116">Отключает восстановление нескольких пакетов параллельно.</span><span class="sxs-lookup"><span data-stu-id="89275-116">Disables restoring multiple packages in parallel.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="89275-117">*(3.2 +)* Список источников пакетов, используемых в качестве резервных при условии, что пакет не найден в основном источнике или по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="89275-117">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> <span data-ttu-id="89275-118">Используйте точку с запятой для разделения записей списка.</span><span class="sxs-lookup"><span data-stu-id="89275-118">Use a semicolon to separate list entries.</span></span>

- **`-Force`**

  <span data-ttu-id="89275-119">В проектах на основе PackageReference принудительно разрешаются все зависимости, даже если последнее восстановление прошло успешно.</span><span class="sxs-lookup"><span data-stu-id="89275-119">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="89275-120">Установка этого флага аналогична удалению `project.assets.json` файла.</span><span class="sxs-lookup"><span data-stu-id="89275-120">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="89275-121">Это не позволяет обходить HTTP-кэш.</span><span class="sxs-lookup"><span data-stu-id="89275-121">This does not bypass the http-cache.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="89275-122">*(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="89275-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-ForceEvaluate`**

  <span data-ttu-id="89275-123">Принудительно применяет восстановление, чтобы повторно рассчитать все зависимости, если файл блокировки уже существует.</span><span class="sxs-lookup"><span data-stu-id="89275-123">Forces restore to reevaluate all dependencies even if a lock file already exists.</span></span>

- **`-?|-help`**

  <span data-ttu-id="89275-124">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="89275-124">Displays help information for the command.</span></span>

- **`-LockFilePath`**

  <span data-ttu-id="89275-125">Расположение выходных данных для записи файла блокировки проекта.</span><span class="sxs-lookup"><span data-stu-id="89275-125">Output location where project lock file is written.</span></span> <span data-ttu-id="89275-126">По умолчанию используется значение `PROJECT_ROOT\packages.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="89275-126">By default, this is `PROJECT_ROOT\packages.lock.json`.</span></span>

- **`-LockedMode`**

  <span data-ttu-id="89275-127">Не разрешать обновление файла блокировки проекта.</span><span class="sxs-lookup"><span data-stu-id="89275-127">Don't allow updating project lock file.</span></span>

- **`-MSBuildPath`**

   <span data-ttu-id="89275-128">*(4.0 +)* Указывает путь MSBuild для использования с командой, который имеет приоритет над `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="89275-128">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="89275-129">*(3.2 +)* Указывает версию MSBuild, которая будет использоваться с этой командой.</span><span class="sxs-lookup"><span data-stu-id="89275-129">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="89275-130">Поддерживаемые значения: 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="89275-130">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="89275-131">По умолчанию в пути выбирается MSBuild, в противном случае — по умолчанию — самая высокая установленная версия MSBuild.</span><span class="sxs-lookup"><span data-stu-id="89275-131">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoCache`**

  <span data-ttu-id="89275-132">Предотвращает использование кэшированных пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="89275-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="89275-133">См. раздел [Управление глобальными пакетами и папками кэша](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="89275-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="89275-134">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="89275-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="89275-135">Указывает папку, в которой устанавливаются пакеты.</span><span class="sxs-lookup"><span data-stu-id="89275-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="89275-136">Если папка не указана, используется текущая папка.</span><span class="sxs-lookup"><span data-stu-id="89275-136">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="89275-137">Требуется при восстановлении с `packages.config` файлом, если не `PackagesDirectory` `SolutionDirectory` используется или.</span><span class="sxs-lookup"><span data-stu-id="89275-137">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="89275-138">Указывает типы файлов, которые необходимо сохранить после установки пакета: один из `nuspec` , `nupkg` или `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="89275-138">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="89275-139">Эквивалентно `OutputDirectory`.</span><span class="sxs-lookup"><span data-stu-id="89275-139">Same as `OutputDirectory`.</span></span> <span data-ttu-id="89275-140">Требуется при восстановлении с `packages.config` файлом, если не `OutputDirectory` `SolutionDirectory` используется или.</span><span class="sxs-lookup"><span data-stu-id="89275-140">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span>

- **`-Project2ProjectTimeOut`**

  <span data-ttu-id="89275-141">Время ожидания в секундах для разрешения ссылок между проектами.</span><span class="sxs-lookup"><span data-stu-id="89275-141">Timeout in seconds for resolving project-to-project references.</span></span>

- **`-Recursive`**

  <span data-ttu-id="89275-142">*(4.0 +)* Восстанавливает все проекты ссылок для проектов UWP и .NET Core.</span><span class="sxs-lookup"><span data-stu-id="89275-142">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="89275-143">Не применяется к проектам с помощью `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="89275-143">Does not apply to projects using `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="89275-144">Проверяет, что восстановление пакетов включено перед загрузкой и установкой пакетов.</span><span class="sxs-lookup"><span data-stu-id="89275-144">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="89275-145">Дополнительные сведения см. в разделе [восстановление пакетов](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="89275-145">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="89275-146">Указывает папку решения.</span><span class="sxs-lookup"><span data-stu-id="89275-146">Specifies the solution folder.</span></span> <span data-ttu-id="89275-147">Недопустимый при восстановлении пакетов для решения.</span><span class="sxs-lookup"><span data-stu-id="89275-147">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="89275-148">Требуется при восстановлении с `packages.config` файлом, если не `PackagesDirectory` `OutputDirectory` используется или.</span><span class="sxs-lookup"><span data-stu-id="89275-148">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span>

- **`-Source`**

  <span data-ttu-id="89275-149">Указывает список источников пакетов (в виде URL-адресов), используемых для восстановления.</span><span class="sxs-lookup"><span data-stu-id="89275-149">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="89275-150">Если этот параметр не указан, команда использует источники, предоставленные в файлах конфигурации, см. раздел [Настройка поведения NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="89275-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="89275-151">Используйте точку с запятой для разделения записей списка.</span><span class="sxs-lookup"><span data-stu-id="89275-151">Use a semicolon to separate list entries.</span></span>

- **`-UseLockFile`**

  <span data-ttu-id="89275-152">Включает создание файла блокировки проекта и использование этого файла при восстановлении.</span><span class="sxs-lookup"><span data-stu-id="89275-152">Enables project lock file to be generated and used with restore.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="89275-153">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="89275-153">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="89275-154">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="89275-154">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="89275-155">Комментарии</span><span class="sxs-lookup"><span data-stu-id="89275-155">Remarks</span></span>

<span data-ttu-id="89275-156">Команда Restore выполняет следующие действия.</span><span class="sxs-lookup"><span data-stu-id="89275-156">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="89275-157">Определите режим работы команды Restore.</span><span class="sxs-lookup"><span data-stu-id="89275-157">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="89275-158">Тип файла projectPath</span><span class="sxs-lookup"><span data-stu-id="89275-158">projectPath file type</span></span> | <span data-ttu-id="89275-159">Поведение</span><span class="sxs-lookup"><span data-stu-id="89275-159">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="89275-160">Решение (папка)</span><span class="sxs-lookup"><span data-stu-id="89275-160">Solution (folder)</span></span> | <span data-ttu-id="89275-161">NuGet ищет `.sln` файл и использует его, если он найден; в противном случае выдает ошибку.</span><span class="sxs-lookup"><span data-stu-id="89275-161">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="89275-162">`(SolutionDir)\.nuget` используется в качестве начальной папки.</span><span class="sxs-lookup"><span data-stu-id="89275-162">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="89275-163">Файл `.sln`</span><span class="sxs-lookup"><span data-stu-id="89275-163">`.sln` file</span></span> | <span data-ttu-id="89275-164">Восстановление пакетов, идентифицируемых решением; выдает ошибку, если `-SolutionDirectory` используется.</span><span class="sxs-lookup"><span data-stu-id="89275-164">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="89275-165">`$(SolutionDir)\.nuget` используется в качестве начальной папки.</span><span class="sxs-lookup"><span data-stu-id="89275-165">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="89275-166">`packages.config` или файл проекта</span><span class="sxs-lookup"><span data-stu-id="89275-166">`packages.config` or project file</span></span> | <span data-ttu-id="89275-167">Восстановление пакетов, перечисленных в файле, разрешение и установку зависимостей.</span><span class="sxs-lookup"><span data-stu-id="89275-167">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="89275-168">Другой тип файла</span><span class="sxs-lookup"><span data-stu-id="89275-168">Other file type</span></span> | <span data-ttu-id="89275-169">Предполагается, что файл является `.sln` файлом, как показано выше. Если это не решение, NuGet выдает ошибку.</span><span class="sxs-lookup"><span data-stu-id="89275-169">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="89275-170">(не указано projectPath)</span><span class="sxs-lookup"><span data-stu-id="89275-170">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="89275-171">NuGet ищет файлы решений в текущей папке.</span><span class="sxs-lookup"><span data-stu-id="89275-171">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="89275-172">Если найден один файл, то он используется для восстановления пакетов. Если найдено несколько решений, NuGet выдает ошибку.</span><span class="sxs-lookup"><span data-stu-id="89275-172">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="89275-173">Если файлы решения отсутствуют, NuGet ищет `packages.config` и использует их для восстановления пакетов.</span><span class="sxs-lookup"><span data-stu-id="89275-173">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="89275-174">Если решение или `packages.config` файл не найдены, NuGet выдает ошибку.</span><span class="sxs-lookup"><span data-stu-id="89275-174">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="89275-175">Определите папку Packages, используя следующий порядок приоритета (NuGet выдает ошибку, если ни одна из этих папок не найдена):</span><span class="sxs-lookup"><span data-stu-id="89275-175">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="89275-176">Папка, указанная в параметре `-PackagesDirectory` .</span><span class="sxs-lookup"><span data-stu-id="89275-176">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="89275-177">`repositoryPath`Значение в`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="89275-177">The `repositoryPath` value in `Nuget.Config`</span></span>
    - <span data-ttu-id="89275-178">Папка, указанная с помощью `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="89275-178">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="89275-179">При восстановлении пакетов для решения NuGet выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="89275-179">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="89275-180">Загружает файл решения.</span><span class="sxs-lookup"><span data-stu-id="89275-180">Loads the solution file.</span></span>
    - <span data-ttu-id="89275-181">Восстанавливает пакеты уровня решения, перечисленные в `$(SolutionDir)\.nuget\packages.config` `packages` папке.</span><span class="sxs-lookup"><span data-stu-id="89275-181">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="89275-182">Восстановление пакетов, перечисленных в `$(ProjectDir)\packages.config` папке, в `packages` папку.</span><span class="sxs-lookup"><span data-stu-id="89275-182">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="89275-183">Для каждого указанного пакета восстановите пакет параллельно, если `-DisableParallelProcessing` не указано иное.</span><span class="sxs-lookup"><span data-stu-id="89275-183">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="89275-184">Примеры</span><span class="sxs-lookup"><span data-stu-id="89275-184">Examples</span></span>

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
