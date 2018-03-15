---
title: "Команда восстановления NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Справочник по команде восстановления nuget.exe"
keywords: "NuGet восстановления ссылок, пакеты команды restore"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2416ad652244e0ea60651147ad74a1513cdb75ff
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="02a5b-104">Команда RESTORE (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="02a5b-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="02a5b-105">**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="02a5b-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="02a5b-106">Загружает и устанавливает все пакеты, отсутствующие на `packages` папки.</span><span class="sxs-lookup"><span data-stu-id="02a5b-106">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="02a5b-107">При использовании NuGet 4.0 + и формат PackageReference, приводит к возникновению ошибки `<project>.nuget.props` файла, при необходимости в `obj` папки.</span><span class="sxs-lookup"><span data-stu-id="02a5b-107">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="02a5b-108">(Можно опустить файл из системы управления версиями.)</span><span class="sxs-lookup"><span data-stu-id="02a5b-108">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="02a5b-109">В Mac OSX и Linux с CLI на моно восстановление пакетов не поддерживается с PackageReference.</span><span class="sxs-lookup"><span data-stu-id="02a5b-109">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="02a5b-110">Использование</span><span class="sxs-lookup"><span data-stu-id="02a5b-110">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="02a5b-111">где `<projectPath>` указывает расположение решения или `packages.config` файла.</span><span class="sxs-lookup"><span data-stu-id="02a5b-111">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="02a5b-112">В разделе [примечания](#remarks) ниже поведения подробности.</span><span class="sxs-lookup"><span data-stu-id="02a5b-112">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="02a5b-113">Параметры</span><span class="sxs-lookup"><span data-stu-id="02a5b-113">Options</span></span>

| <span data-ttu-id="02a5b-114">Параметр</span><span class="sxs-lookup"><span data-stu-id="02a5b-114">Option</span></span> | <span data-ttu-id="02a5b-115">Описание:</span><span class="sxs-lookup"><span data-stu-id="02a5b-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="02a5b-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="02a5b-116">ConfigFile</span></span> | <span data-ttu-id="02a5b-117">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="02a5b-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="02a5b-118">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="02a5b-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="02a5b-119">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="02a5b-119">DirectDownload</span></span> | <span data-ttu-id="02a5b-120">*(4.0 +)*  Загружает пакеты непосредственно, без заполнения кэши с двоичные файлы и метаданные.</span><span class="sxs-lookup"><span data-stu-id="02a5b-120">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="02a5b-121">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="02a5b-121">DisableParallelProcessing</span></span> | <span data-ttu-id="02a5b-122">Отключает восстановление нескольких пакетов в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="02a5b-122">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="02a5b-123">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="02a5b-123">FallbackSource</span></span> | <span data-ttu-id="02a5b-124">*(3.2 +)*  Список источников пакетов для использования как в случае ошибки в случае, если пакет не найден в основной или источник по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="02a5b-124">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="02a5b-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="02a5b-125">ForceEnglishOutput</span></span> | <span data-ttu-id="02a5b-126">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="02a5b-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="02a5b-127">Справка</span><span class="sxs-lookup"><span data-stu-id="02a5b-127">Help</span></span> | <span data-ttu-id="02a5b-128">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="02a5b-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="02a5b-129">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="02a5b-129">MSBuildPath</span></span> | <span data-ttu-id="02a5b-130">*(4.0 +)*  Указывает путь к MSBuild для команды, переназначает `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="02a5b-130">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="02a5b-131">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="02a5b-131">MSBuildVersion</span></span> | <span data-ttu-id="02a5b-132">*(3.2 +)*  Указывает версию MSBuild для использования с помощью этой команды.</span><span class="sxs-lookup"><span data-stu-id="02a5b-132">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="02a5b-133">Поддерживаемые значения: 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="02a5b-133">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="02a5b-134">По умолчанию выбирается MSBuild в пути в противном случае по умолчанию наибольшую установленную версию MSBuild.</span><span class="sxs-lookup"><span data-stu-id="02a5b-134">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="02a5b-135">NoCache</span><span class="sxs-lookup"><span data-stu-id="02a5b-135">NoCache</span></span> | <span data-ttu-id="02a5b-136">Запрещает NuGet с помощью пакетов из кэшей локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="02a5b-136">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="02a5b-137">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="02a5b-137">NonInteractive</span></span> | <span data-ttu-id="02a5b-138">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="02a5b-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="02a5b-139">Выходной каталог</span><span class="sxs-lookup"><span data-stu-id="02a5b-139">OutputDirectory</span></span> | <span data-ttu-id="02a5b-140">Указывает папку, в которой устанавливаются пакеты.</span><span class="sxs-lookup"><span data-stu-id="02a5b-140">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="02a5b-141">Если папка не указана, используется текущая папка.</span><span class="sxs-lookup"><span data-stu-id="02a5b-141">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="02a5b-142">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="02a5b-142">PackageSaveMode</span></span> | <span data-ttu-id="02a5b-143">Указывает типы файлов для сохранения после установки пакета: один из `nuspec`, `nupkg`, или `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="02a5b-143">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="02a5b-144">Пакетыструктура</span><span class="sxs-lookup"><span data-stu-id="02a5b-144">PackagesDirectory</span></span> | <span data-ttu-id="02a5b-145">Эквивалентно `OutputDirectory`.</span><span class="sxs-lookup"><span data-stu-id="02a5b-145">Same as `OutputDirectory`.</span></span> |
| <span data-ttu-id="02a5b-146">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="02a5b-146">Project2ProjectTimeOut</span></span> | <span data-ttu-id="02a5b-147">Время ожидания в секундах для разрешения ссылок проекта на проект.</span><span class="sxs-lookup"><span data-stu-id="02a5b-147">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="02a5b-148">Рекурсивные</span><span class="sxs-lookup"><span data-stu-id="02a5b-148">Recursive</span></span> | <span data-ttu-id="02a5b-149">*(4.0 +)*  Восстанавливает все ссылки на проекты для проектов UWP и .NET Core.</span><span class="sxs-lookup"><span data-stu-id="02a5b-149">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="02a5b-150">Не применяется для проектов с помощью `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="02a5b-150">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="02a5b-151">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="02a5b-151">RequireConsent</span></span> | <span data-ttu-id="02a5b-152">Восстановление пакетов проверяет, включена ли перед загрузкой и установкой пакетов.</span><span class="sxs-lookup"><span data-stu-id="02a5b-152">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="02a5b-153">Дополнительные сведения см. в разделе [восстановление пакетов](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="02a5b-153">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="02a5b-154">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="02a5b-154">SolutionDirectory</span></span> | <span data-ttu-id="02a5b-155">Указывает папку решения.</span><span class="sxs-lookup"><span data-stu-id="02a5b-155">Specifies the solution folder.</span></span> <span data-ttu-id="02a5b-156">Не является допустимым при восстановлении пакетами для решения.</span><span class="sxs-lookup"><span data-stu-id="02a5b-156">Not valid when restoring packages for a solution.</span></span> |
| <span data-ttu-id="02a5b-157">Исходный код</span><span class="sxs-lookup"><span data-stu-id="02a5b-157">Source</span></span> | <span data-ttu-id="02a5b-158">Указывает список источников пакетов (в виде URL-адреса) для восстановления.</span><span class="sxs-lookup"><span data-stu-id="02a5b-158">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="02a5b-159">Если не указано, команда использует источники, предоставляемые в файлах конфигурации см. в разделе [NuGet Настройка поведения](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="02a5b-159">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="02a5b-160">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="02a5b-160">Verbosity</span></span> |<span data-ttu-id="02a5b-161">> указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="02a5b-161">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="02a5b-162">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="02a5b-162">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="02a5b-163">Примечания</span><span class="sxs-lookup"><span data-stu-id="02a5b-163">Remarks</span></span>

<span data-ttu-id="02a5b-164">Команда восстановления выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="02a5b-164">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="02a5b-165">Определите режим работы команды restore.</span><span class="sxs-lookup"><span data-stu-id="02a5b-165">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="02a5b-166">Тип файла projectPath</span><span class="sxs-lookup"><span data-stu-id="02a5b-166">projectPath file type</span></span> | <span data-ttu-id="02a5b-167">Поведение</span><span class="sxs-lookup"><span data-stu-id="02a5b-167">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="02a5b-168">Решения (папка)</span><span class="sxs-lookup"><span data-stu-id="02a5b-168">Solution (folder)</span></span> | <span data-ttu-id="02a5b-169">Ищет NuGet `.sln` файл и используется, если элемент найден; в противном случае он приводит к ошибке.</span><span class="sxs-lookup"><span data-stu-id="02a5b-169">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="02a5b-170">`(SolutionDir)\.nuget` используются в качестве начальной папки.</span><span class="sxs-lookup"><span data-stu-id="02a5b-170">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="02a5b-171">`.sln` Файл</span><span class="sxs-lookup"><span data-stu-id="02a5b-171">`.sln` file</span></span> | <span data-ttu-id="02a5b-172">Восстановление пакетов, определенных для этого решения; выдает ошибку, если `-SolutionDirectory` используется.</span><span class="sxs-lookup"><span data-stu-id="02a5b-172">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="02a5b-173">`$(SolutionDir)\.nuget` используются в качестве начальной папки.</span><span class="sxs-lookup"><span data-stu-id="02a5b-173">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="02a5b-174">`packages.config` или файл проекта</span><span class="sxs-lookup"><span data-stu-id="02a5b-174">`packages.config` or project file</span></span> | <span data-ttu-id="02a5b-175">Восстановите пакеты, перечисленные в файле, разрешения и установка зависимостей.</span><span class="sxs-lookup"><span data-stu-id="02a5b-175">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="02a5b-176">Другие типы файлов</span><span class="sxs-lookup"><span data-stu-id="02a5b-176">Other file type</span></span> | <span data-ttu-id="02a5b-177">Файл считается `.sln` файл, что и выше; Если не решение, дает NuGet произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="02a5b-177">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="02a5b-178">(projectPath не указан)</span><span class="sxs-lookup"><span data-stu-id="02a5b-178">(projectPath not specified)</span></span> | <span data-ttu-id="02a5b-179">— NuGet ищет файлы решения в текущей папке.</span><span class="sxs-lookup"><span data-stu-id="02a5b-179">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="02a5b-180">Если найден один файл, что один используется для восстановления пакетов; Если обнаружены несколько решений, NuGet сообщает об ошибке.</span><span class="sxs-lookup"><span data-stu-id="02a5b-180">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="02a5b-181">-Если отсутствуют файлы решений, NuGet ищет `packages.config` и использует эти данные для восстановления пакетов.</span><span class="sxs-lookup"><span data-stu-id="02a5b-181">- If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span>
    |<span data-ttu-id="02a5b-182">— Если ни одно решение или `packages.config` файл найден, NuGet выдает ошибку.</span><span class="sxs-lookup"><span data-stu-id="02a5b-182">- If no solution or `packages.config` file is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="02a5b-183">Определите «пакеты», используя следующий порядок приоритета (NuGet выдает ошибку, если найден ни один из этих папок):</span><span class="sxs-lookup"><span data-stu-id="02a5b-183">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="02a5b-184">Папка, указанная с `-PackagesDirectory`.</span><span class="sxs-lookup"><span data-stu-id="02a5b-184">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="02a5b-185">`repositoryPath` Значение в `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="02a5b-185">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="02a5b-186">Папка, указанная с `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="02a5b-186">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="02a5b-187">При восстановлении пакетами для решения, NuGet выполняет следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="02a5b-187">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="02a5b-188">Загружает файл решения.</span><span class="sxs-lookup"><span data-stu-id="02a5b-188">Loads the solution file.</span></span>
    - <span data-ttu-id="02a5b-189">Восстанавливает уровня пакеты решения, перечисленные в `$(SolutionDir)\.nuget\packages.config` в `packages` папки.</span><span class="sxs-lookup"><span data-stu-id="02a5b-189">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="02a5b-190">Восстановить пакеты, перечисленные в `$(ProjectDir)\packages.config` в `packages` папки.</span><span class="sxs-lookup"><span data-stu-id="02a5b-190">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="02a5b-191">Для каждого указанного пакета, восстановление пакета в параллельном режиме, если `-DisableParallelProcessing` указано.</span><span class="sxs-lookup"><span data-stu-id="02a5b-191">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="02a5b-192">Примеры</span><span class="sxs-lookup"><span data-stu-id="02a5b-192">Examples</span></span>

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
