---
title: "Команда восстановления NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee41020-e548-4e61-b8cd-c82b77ac6af7
description: "Справочник по команде восстановления nuget.exe"
keywords: "NuGet восстановления ссылок, пакеты команды restore"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b435a3c2ffe08e3c2f8fc6a4dacb06cf674e4fb9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="bb068-104">Команда RESTORE (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="bb068-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="bb068-105">**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="bb068-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="bb068-106">NuGet 2.7 +: Загружает и устанавливает все пакеты, отсутствующие на `packages` папки.</span><span class="sxs-lookup"><span data-stu-id="bb068-106">NuGet 2.7+: Downloads and installs any packages missing from the `packages` folder.</span></span>

<span data-ttu-id="bb068-107">NuGet 3.3 + с проектами с помощью `project.json`: приводит к возникновению ошибки `project.lock.json` файла и `<project>.nuget.props` файла, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="bb068-107">NuGet 3.3+ with projects using `project.json`: Generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="bb068-108">(Можно опустить оба файла из системы управления версиями.)</span><span class="sxs-lookup"><span data-stu-id="bb068-108">(Both files can be omitted from source control.)</span></span>

<span data-ttu-id="bb068-109">NuGet 4.0 + с проектом, в какой пакет включаются ссылки на файл проекта напрямую: приводит к возникновению ошибки `<project>.nuget.props` файла, при необходимости в `obj` папки.</span><span class="sxs-lookup"><span data-stu-id="bb068-109">NuGet 4.0+ with project in which package references are included in the project file directly: Generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="bb068-110">(Можно опустить файл из системы управления версиями.)</span><span class="sxs-lookup"><span data-stu-id="bb068-110">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="bb068-111">В Mac OSX и Linux с CLI на моно восстановление пакетов не поддерживается в формате PackageReference.</span><span class="sxs-lookup"><span data-stu-id="bb068-111">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with the PackageReference format.</span></span>

## <a name="usage"></a><span data-ttu-id="bb068-112">Использование</span><span class="sxs-lookup"><span data-stu-id="bb068-112">Usage</span></span>

```
nuget restore <projectPath> [options]
```

<span data-ttu-id="bb068-113">где `<projectPath>` указывает расположение решения, `packages.config` файл, или `project.json` файла.</span><span class="sxs-lookup"><span data-stu-id="bb068-113">where `<projectPath>` specifies the location of a solution, a `packages.config` file, or a `project.json` file.</span></span> <span data-ttu-id="bb068-114">В разделе [примечания](#remarks) ниже поведения подробности.</span><span class="sxs-lookup"><span data-stu-id="bb068-114">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="bb068-115">Параметры</span><span class="sxs-lookup"><span data-stu-id="bb068-115">Options</span></span>

| <span data-ttu-id="bb068-116">Параметр</span><span class="sxs-lookup"><span data-stu-id="bb068-116">Option</span></span> | <span data-ttu-id="bb068-117">Описание</span><span class="sxs-lookup"><span data-stu-id="bb068-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bb068-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="bb068-118">ConfigFile</span></span> | <span data-ttu-id="bb068-119">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="bb068-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="bb068-120">Если не указан, *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="bb068-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="bb068-121">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="bb068-121">DirectDownload</span></span> | <span data-ttu-id="bb068-122">*(4.0 +)*  Загружает пакеты непосредственно, без заполнения кэши с двоичные файлы и метаданные.</span><span class="sxs-lookup"><span data-stu-id="bb068-122">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="bb068-123">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="bb068-123">DisableParallelProcessing</span></span> | <span data-ttu-id="bb068-124">Отключает восстановление нескольких пакетов в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="bb068-124">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="bb068-125">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="bb068-125">FallbackSource</span></span> | <span data-ttu-id="bb068-126">*(3.2 +)*  Список источников пакетов для использования как в случае ошибки в случае, если пакет не найден в основной или источник по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bb068-126">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="bb068-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="bb068-127">ForceEnglishOutput</span></span> | <span data-ttu-id="bb068-128">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="bb068-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="bb068-129">Справка</span><span class="sxs-lookup"><span data-stu-id="bb068-129">Help</span></span> | <span data-ttu-id="bb068-130">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="bb068-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="bb068-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="bb068-131">MSBuildPath</span></span> | <span data-ttu-id="bb068-132">*(4.0 +)*  Указывает путь к MSBuild для команды, переназначает `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="bb068-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="bb068-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="bb068-133">MSBuildVersion</span></span> | <span data-ttu-id="bb068-134">*(3.2 +)*  Указывает версию MSBuild для использования с помощью этой команды.</span><span class="sxs-lookup"><span data-stu-id="bb068-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="bb068-135">Поддерживаемые значения: 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="bb068-135">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="bb068-136">По умолчанию выбирается MSBuild в пути в противном случае по умолчанию наибольшую установленную версию MSBuild.</span><span class="sxs-lookup"><span data-stu-id="bb068-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="bb068-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="bb068-137">NoCache</span></span> | <span data-ttu-id="bb068-138">Запрещает NuGet с помощью пакетов из кэшей локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="bb068-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="bb068-139">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="bb068-139">NonInteractive</span></span> | <span data-ttu-id="bb068-140">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="bb068-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="bb068-141">Выходной каталог</span><span class="sxs-lookup"><span data-stu-id="bb068-141">OutputDirectory</span></span> | <span data-ttu-id="bb068-142">Указывает папку, в которой устанавливаются пакеты.</span><span class="sxs-lookup"><span data-stu-id="bb068-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="bb068-143">Если папка не указана, используется текущая папка.</span><span class="sxs-lookup"><span data-stu-id="bb068-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="bb068-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="bb068-144">PackageSaveMode</span></span> | <span data-ttu-id="bb068-145">Указывает типы файлов для сохранения после установки пакета: один из `nuspec`, `nupkg`, или `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="bb068-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="bb068-146">Пакетыструктура</span><span class="sxs-lookup"><span data-stu-id="bb068-146">PackagesDirectory</span></span> | <span data-ttu-id="bb068-147">Эквивалентно `OutputDirectory`.</span><span class="sxs-lookup"><span data-stu-id="bb068-147">Same as `OutputDirectory`.</span></span> |
| <span data-ttu-id="bb068-148">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="bb068-148">Project2ProjectTimeOut</span></span> | <span data-ttu-id="bb068-149">Время ожидания в секундах для разрешения ссылок проекта на проект.</span><span class="sxs-lookup"><span data-stu-id="bb068-149">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="bb068-150">Рекурсивные</span><span class="sxs-lookup"><span data-stu-id="bb068-150">Recursive</span></span> | <span data-ttu-id="bb068-151">*(4.0 +)*  Восстанавливает все ссылки на проекты для проектов UWP и .NET Core.</span><span class="sxs-lookup"><span data-stu-id="bb068-151">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="bb068-152">Не применяется для проектов с помощью `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="bb068-152">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="bb068-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="bb068-153">RequireConsent</span></span> | <span data-ttu-id="bb068-154">Восстановление пакетов проверяет, включена ли перед загрузкой и установкой пакетов.</span><span class="sxs-lookup"><span data-stu-id="bb068-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="bb068-155">Дополнительные сведения см. в разделе [восстановление пакетов](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="bb068-155">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="bb068-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="bb068-156">SolutionDirectory</span></span> | <span data-ttu-id="bb068-157">Указывает папку решения.</span><span class="sxs-lookup"><span data-stu-id="bb068-157">Specifies the solution folder.</span></span> <span data-ttu-id="bb068-158">Не является допустимым при восстановлении пакетами для решения.</span><span class="sxs-lookup"><span data-stu-id="bb068-158">Not valid when restoring packages for a solution.</span></span> |
| <span data-ttu-id="bb068-159">Исходный код</span><span class="sxs-lookup"><span data-stu-id="bb068-159">Source</span></span> | <span data-ttu-id="bb068-160">Указывает список источников пакетов (в виде URL-адреса) для восстановления.</span><span class="sxs-lookup"><span data-stu-id="bb068-160">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="bb068-161">Если не указано, команда использует источники, предоставляемые в файлах конфигурации см. в разделе [NuGet Настройка поведения](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="bb068-161">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="bb068-162">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="bb068-162">Verbosity</span></span> |<span data-ttu-id="bb068-163">> указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="bb068-163">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="bb068-164">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="bb068-164">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="bb068-165">Примечания</span><span class="sxs-lookup"><span data-stu-id="bb068-165">Remarks</span></span>

<span data-ttu-id="bb068-166">Команда восстановления выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="bb068-166">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="bb068-167">Определите режим работы команды restore.</span><span class="sxs-lookup"><span data-stu-id="bb068-167">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="bb068-168">Тип файла projectPath</span><span class="sxs-lookup"><span data-stu-id="bb068-168">projectPath file type</span></span> | <span data-ttu-id="bb068-169">Поведение</span><span class="sxs-lookup"><span data-stu-id="bb068-169">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="bb068-170">Решения (папка)</span><span class="sxs-lookup"><span data-stu-id="bb068-170">Solution (folder)</span></span> | <span data-ttu-id="bb068-171">Ищет NuGet `.sln` файл и используется, если элемент найден; в противном случае он приводит к ошибке.</span><span class="sxs-lookup"><span data-stu-id="bb068-171">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="bb068-172">`(SolutionDir)\.nuget`используются в качестве начальной папки.</span><span class="sxs-lookup"><span data-stu-id="bb068-172">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="bb068-173">`.sln`файл</span><span class="sxs-lookup"><span data-stu-id="bb068-173">`.sln` file</span></span> | <span data-ttu-id="bb068-174">Восстановление пакетов, определенных для этого решения; выдает ошибку, если `-SolutionDirectory` используется.</span><span class="sxs-lookup"><span data-stu-id="bb068-174">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="bb068-175">`$(SolutionDir)\.nuget`используются в качестве начальной папки.</span><span class="sxs-lookup"><span data-stu-id="bb068-175">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="bb068-176">`packages.config`, `project.json`, или файл проекта</span><span class="sxs-lookup"><span data-stu-id="bb068-176">`packages.config`, `project.json`, or project file</span></span> | <span data-ttu-id="bb068-177">Восстановите пакеты, перечисленные в файле, разрешения и установка зависимостей.</span><span class="sxs-lookup"><span data-stu-id="bb068-177">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="bb068-178">Другие типы файлов</span><span class="sxs-lookup"><span data-stu-id="bb068-178">Other file type</span></span> | <span data-ttu-id="bb068-179">Файл считается `.sln` файл, что и выше; Если не решение, дает NuGet произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="bb068-179">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="bb068-180">(projectPath не указан)</span><span class="sxs-lookup"><span data-stu-id="bb068-180">(projectPath not specified)</span></span> | <span data-ttu-id="bb068-181">— NuGet ищет файлы решения в текущей папке.</span><span class="sxs-lookup"><span data-stu-id="bb068-181">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="bb068-182">Если найден один файл, что один используется для восстановления пакетов; Если обнаружены несколько решений, NuGet сообщает об ошибке.</span><span class="sxs-lookup"><span data-stu-id="bb068-182">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="bb068-183">-Если отсутствуют файлы решений, NuGet ищет `packages.config` или `project.json` и использует эти данные для восстановления пакетов.</span><span class="sxs-lookup"><span data-stu-id="bb068-183">- If there are no solution files, NuGet looks for a `packages.config` or `project.json` and uses that to restore packages.</span></span>
    |<span data-ttu-id="bb068-184">-Если отсутствует файл решения `packages.config`, или `project.json` найден, NuGet выдает ошибку.</span><span class="sxs-lookup"><span data-stu-id="bb068-184">- If no solution file, `packages.config`, or `project.json` is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="bb068-185">Определите «пакеты», используя следующий порядок приоритета (NuGet выдает ошибку, если найден ни один из этих папок):</span><span class="sxs-lookup"><span data-stu-id="bb068-185">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="bb068-186">`%userprofile%\.nuget\packages` Значение в `project.json`.</span><span class="sxs-lookup"><span data-stu-id="bb068-186">The `%userprofile%\.nuget\packages` value in `project.json`.</span></span>
    - <span data-ttu-id="bb068-187">Папка, указанная с `-PackagesDirectory`.</span><span class="sxs-lookup"><span data-stu-id="bb068-187">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="bb068-188">`repositoryPath` Значение в`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="bb068-188">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="bb068-189">Папка, указанная с`-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="bb068-189">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="bb068-190">При восстановлении пакетами для решения, NuGet выполняет следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="bb068-190">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="bb068-191">Загружает файл решения.</span><span class="sxs-lookup"><span data-stu-id="bb068-191">Loads the solution file.</span></span>
    - <span data-ttu-id="bb068-192">Восстанавливает уровня пакеты решения, перечисленные в `$(SolutionDir)\.nuget\packages.config` в `packages` папки.</span><span class="sxs-lookup"><span data-stu-id="bb068-192">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="bb068-193">Восстановить пакеты, перечисленные в `$(ProjectDir)\packages.config` в `packages` папки.</span><span class="sxs-lookup"><span data-stu-id="bb068-193">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="bb068-194">Для каждого указанного пакета, восстановление пакета в параллельном режиме, если `-DisableParallelProcessing` указано.</span><span class="sxs-lookup"><span data-stu-id="bb068-194">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="bb068-195">Примеры</span><span class="sxs-lookup"><span data-stu-id="bb068-195">Examples</span></span>

```
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
