---
title: "NuGet CLI обновление команды | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 61fde945-6983-46a5-8636-da0fada4e641
description: "Ссылка для команды update nuget.exe"
keywords: "NuGet обновить ссылку, команда пакета обновления"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 654144e93a99a4a4f8d79c0db5660cfb7c6c308e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="0cd15-104">Команда обновления (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="0cd15-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="0cd15-105">**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="0cd15-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="0cd15-106">Обновляет все пакеты в проекте (с помощью `packages.config`) их последние версии.</span><span class="sxs-lookup"><span data-stu-id="0cd15-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="0cd15-107">Рекомендуется выполнять [«восстановление»](#restore) перед запуском `update`.</span><span class="sxs-lookup"><span data-stu-id="0cd15-107">It is recommended to run ['restore'](#restore) before running the `update`.</span></span> <span data-ttu-id="0cd15-108">(Чтобы обновить отдельный пакет, используйте [ `nuget install` ](cli-ref-install.md) без указания номера версии, в котором вариантов NuGet устанавливает последнюю версию.)</span><span class="sxs-lookup"><span data-stu-id="0cd15-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="0cd15-109">Примечание: `update` не работает с CLI, выполняемых в рамках моно (Mac OSX и Linux).</span><span class="sxs-lookup"><span data-stu-id="0cd15-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux).</span></span> <span data-ttu-id="0cd15-110">Команда также не работает с проектами с помощью `project.json` или PackageReference управления форматы.</span><span class="sxs-lookup"><span data-stu-id="0cd15-110">The command also does not work with projects using `project.json` or PackageReference management formats.</span></span>

<span data-ttu-id="0cd15-111">`update` Команда также обновляет ссылки на сборки в файл проекта, если те уже ссылается на существует.</span><span class="sxs-lookup"><span data-stu-id="0cd15-111">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="0cd15-112">Если обновленный пакет добавлены сборки, новая ссылка является *не* добавлен.</span><span class="sxs-lookup"><span data-stu-id="0cd15-112">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="0cd15-113">Новые зависимости пакета также нет ссылок на сборки, их добавить.</span><span class="sxs-lookup"><span data-stu-id="0cd15-113">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="0cd15-114">Чтобы включить эти операции как часть обновления, обновите пакет в Visual Studio с помощью пользовательского интерфейса диспетчера пакетов или консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="0cd15-114">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="0cd15-115">Эта команда также может использоваться для обновления nuget.exe себя с помощью *-self* флаг.</span><span class="sxs-lookup"><span data-stu-id="0cd15-115">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="0cd15-116">Использование</span><span class="sxs-lookup"><span data-stu-id="0cd15-116">Usage</span></span>

```
nuget update <configPath> [options]
```

<span data-ttu-id="0cd15-117">где `<configPath>` идентифицирует либо `packages.config` или файл решения, который содержит список зависимостей проекта.</span><span class="sxs-lookup"><span data-stu-id="0cd15-117">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="0cd15-118">Параметры</span><span class="sxs-lookup"><span data-stu-id="0cd15-118">Options</span></span>

| <span data-ttu-id="0cd15-119">Параметр</span><span class="sxs-lookup"><span data-stu-id="0cd15-119">Option</span></span> | <span data-ttu-id="0cd15-120">Описание</span><span class="sxs-lookup"><span data-stu-id="0cd15-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0cd15-121">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="0cd15-121">ConfigFile</span></span> | <span data-ttu-id="0cd15-122">*(2.5 +)*  NuGet файла конфигурации для применения.</span><span class="sxs-lookup"><span data-stu-id="0cd15-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="0cd15-123">Если не указан, *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="0cd15-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="0cd15-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="0cd15-124">FileConflictAction</span></span> | <span data-ttu-id="0cd15-125">*(2.5 +)*  Указывает действие, выполняемое при появлении запроса, чтобы игнорировать существующие файлы, связанные с проектом или перезаписать.</span><span class="sxs-lookup"><span data-stu-id="0cd15-125">*(2.5+)* Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="0cd15-126">Значения: *перезаписать, игнорировать none*.</span><span class="sxs-lookup"><span data-stu-id="0cd15-126">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="0cd15-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0cd15-127">ForceEnglishOutput</span></span> | <span data-ttu-id="0cd15-128">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="0cd15-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0cd15-129">Справка</span><span class="sxs-lookup"><span data-stu-id="0cd15-129">Help</span></span> | <span data-ttu-id="0cd15-130">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="0cd15-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="0cd15-131">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="0cd15-131">Id</span></span> | <span data-ttu-id="0cd15-132">Задает список идентификаторов для обновления пакета.</span><span class="sxs-lookup"><span data-stu-id="0cd15-132">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="0cd15-133">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="0cd15-133">MSBuildPath</span></span> | <span data-ttu-id="0cd15-134">*(4.0 +)*  Указывает путь к MSBuild для команды, переназначает `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="0cd15-134">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="0cd15-135">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="0cd15-135">MSBuildVersion</span></span> | <span data-ttu-id="0cd15-136">*(3.2 +)*  Указывает версию MSBuild для использования с помощью этой команды.</span><span class="sxs-lookup"><span data-stu-id="0cd15-136">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="0cd15-137">Поддерживаемые значения: 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="0cd15-137">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="0cd15-138">По умолчанию выбирается MSBuild в пути в противном случае по умолчанию наибольшую установленную версию MSBuild.</span><span class="sxs-lookup"><span data-stu-id="0cd15-138">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="0cd15-139">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="0cd15-139">NonInteractive</span></span> | <span data-ttu-id="0cd15-140">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="0cd15-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="0cd15-141">Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="0cd15-141">PreRelease</span></span> | <span data-ttu-id="0cd15-142">Допускает обновление для предварительных версий.</span><span class="sxs-lookup"><span data-stu-id="0cd15-142">Allows updating to prerelease versions.</span></span> <span data-ttu-id="0cd15-143">Этот флаг не требуется при обновлении предварительные версии пакетов, которые уже установлены.</span><span class="sxs-lookup"><span data-stu-id="0cd15-143">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="0cd15-144">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="0cd15-144">RepositoryPath</span></span> | <span data-ttu-id="0cd15-145">Указывает локальную папку, где установлены пакеты.</span><span class="sxs-lookup"><span data-stu-id="0cd15-145">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="0cd15-146">Safe</span><span class="sxs-lookup"><span data-stu-id="0cd15-146">Safe</span></span> | <span data-ttu-id="0cd15-147">Указывает, обновляет только с самой высокой версией, доступной в пределах той же основной и дополнительный номера версии, установленный пакет будет установлен.</span><span class="sxs-lookup"><span data-stu-id="0cd15-147">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="0cd15-148">Самообслуживания</span><span class="sxs-lookup"><span data-stu-id="0cd15-148">Self</span></span> | <span data-ttu-id="0cd15-149">*(1.4 +)*  Обновляет nuget.exe до последней версии; все остальные аргументы учитываются.</span><span class="sxs-lookup"><span data-stu-id="0cd15-149">*(1.4+)* Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="0cd15-150">Исходный код</span><span class="sxs-lookup"><span data-stu-id="0cd15-150">Source</span></span> | <span data-ttu-id="0cd15-151">Указывает список источников пакетов (в виде URL-адреса) для обновления.</span><span class="sxs-lookup"><span data-stu-id="0cd15-151">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="0cd15-152">Если не указано, команда использует источники, предоставляемые в файлах конфигурации см. в разделе [NuGet Настройка поведения](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="0cd15-152">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="0cd15-153">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="0cd15-153">Verbosity</span></span> | <span data-ttu-id="0cd15-154">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="0cd15-154">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="0cd15-155">Версия</span><span class="sxs-lookup"><span data-stu-id="0cd15-155">Version</span></span> | <span data-ttu-id="0cd15-156">Если для одного идентификатора пакета, указывает версию пакета для обновления.</span><span class="sxs-lookup"><span data-stu-id="0cd15-156">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="0cd15-157">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0cd15-157">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0cd15-158">Примеры</span><span class="sxs-lookup"><span data-stu-id="0cd15-158">Examples</span></span>

```
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
