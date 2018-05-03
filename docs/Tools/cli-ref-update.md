---
title: Команда обновления NuGet CLI
description: Ссылка для команды update nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e6964d92436ce1bac9e6af85f6dae75fcf40378d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="c1623-103">Команда обновления (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c1623-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="c1623-104">**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="c1623-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c1623-105">Обновляет все пакеты в проекте (с помощью `packages.config`) их последние версии.</span><span class="sxs-lookup"><span data-stu-id="c1623-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="c1623-106">Рекомендуется выполнять [«восстановление»](cli-ref-restore.md) перед запуском `update`.</span><span class="sxs-lookup"><span data-stu-id="c1623-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="c1623-107">(Чтобы обновить отдельный пакет, используйте [ `nuget install` ](cli-ref-install.md) без указания номера версии, в котором вариантов NuGet устанавливает последнюю версию.)</span><span class="sxs-lookup"><span data-stu-id="c1623-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="c1623-108">Примечание: `update` не работает с CLI, выполняемые с моно (Mac OSX и Linux) или при использовании формата PackageReference.</span><span class="sxs-lookup"><span data-stu-id="c1623-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="c1623-109">`update` Команда также обновляет ссылки на сборки в файл проекта, если те уже ссылается на существует.</span><span class="sxs-lookup"><span data-stu-id="c1623-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="c1623-110">Если обновленный пакет добавлены сборки, новая ссылка является *не* добавлен.</span><span class="sxs-lookup"><span data-stu-id="c1623-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="c1623-111">Новые зависимости пакета также нет ссылок на сборки, их добавить.</span><span class="sxs-lookup"><span data-stu-id="c1623-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="c1623-112">Чтобы включить эти операции как часть обновления, обновите пакет в Visual Studio с помощью пользовательского интерфейса диспетчера пакетов или консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="c1623-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="c1623-113">Эта команда также может использоваться для обновления nuget.exe себя с помощью *-self* флаг.</span><span class="sxs-lookup"><span data-stu-id="c1623-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="c1623-114">Использование</span><span class="sxs-lookup"><span data-stu-id="c1623-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="c1623-115">где `<configPath>` идентифицирует либо `packages.config` или файл решения, который содержит список зависимостей проекта.</span><span class="sxs-lookup"><span data-stu-id="c1623-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="c1623-116">Параметры</span><span class="sxs-lookup"><span data-stu-id="c1623-116">Options</span></span>

| <span data-ttu-id="c1623-117">Параметр</span><span class="sxs-lookup"><span data-stu-id="c1623-117">Option</span></span> | <span data-ttu-id="c1623-118">Описание</span><span class="sxs-lookup"><span data-stu-id="c1623-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c1623-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c1623-119">ConfigFile</span></span> | <span data-ttu-id="c1623-120">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="c1623-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c1623-121">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="c1623-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c1623-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="c1623-122">FileConflictAction</span></span> | <span data-ttu-id="c1623-123">Указывает действие, выполняемое при появлении запроса, чтобы игнорировать существующие файлы, связанные с проектом или перезаписать.</span><span class="sxs-lookup"><span data-stu-id="c1623-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="c1623-124">Значения: *перезаписать, игнорировать none*.</span><span class="sxs-lookup"><span data-stu-id="c1623-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="c1623-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c1623-125">ForceEnglishOutput</span></span> | <span data-ttu-id="c1623-126">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="c1623-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c1623-127">Справка</span><span class="sxs-lookup"><span data-stu-id="c1623-127">Help</span></span> | <span data-ttu-id="c1623-128">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="c1623-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="c1623-129">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="c1623-129">Id</span></span> | <span data-ttu-id="c1623-130">Задает список идентификаторов для обновления пакета.</span><span class="sxs-lookup"><span data-stu-id="c1623-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="c1623-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="c1623-131">MSBuildPath</span></span> | <span data-ttu-id="c1623-132">*(4.0 +)*  Указывает путь к MSBuild для команды, переназначает `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="c1623-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="c1623-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="c1623-133">MSBuildVersion</span></span> | <span data-ttu-id="c1623-134">*(3.2 +)*  Указывает версию MSBuild для использования с помощью этой команды.</span><span class="sxs-lookup"><span data-stu-id="c1623-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="c1623-135">Поддерживаемые значения: 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="c1623-135">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="c1623-136">По умолчанию выбирается MSBuild в пути в противном случае по умолчанию наибольшую установленную версию MSBuild.</span><span class="sxs-lookup"><span data-stu-id="c1623-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="c1623-137">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="c1623-137">NonInteractive</span></span> | <span data-ttu-id="c1623-138">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="c1623-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c1623-139">Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="c1623-139">PreRelease</span></span> | <span data-ttu-id="c1623-140">Допускает обновление для предварительных версий.</span><span class="sxs-lookup"><span data-stu-id="c1623-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="c1623-141">Этот флаг не требуется при обновлении предварительные версии пакетов, которые уже установлены.</span><span class="sxs-lookup"><span data-stu-id="c1623-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="c1623-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="c1623-142">RepositoryPath</span></span> | <span data-ttu-id="c1623-143">Указывает локальную папку, где установлены пакеты.</span><span class="sxs-lookup"><span data-stu-id="c1623-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="c1623-144">Safe</span><span class="sxs-lookup"><span data-stu-id="c1623-144">Safe</span></span> | <span data-ttu-id="c1623-145">Указывает, обновляет только с самой высокой версией, доступной в пределах той же основной и дополнительный номера версии, установленный пакет будет установлен.</span><span class="sxs-lookup"><span data-stu-id="c1623-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="c1623-146">Самообслуживания</span><span class="sxs-lookup"><span data-stu-id="c1623-146">Self</span></span> | <span data-ttu-id="c1623-147">Nuget.exe обновления до последней версии; все остальные аргументы учитываются.</span><span class="sxs-lookup"><span data-stu-id="c1623-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="c1623-148">Исходный код</span><span class="sxs-lookup"><span data-stu-id="c1623-148">Source</span></span> | <span data-ttu-id="c1623-149">Указывает список источников пакетов (в виде URL-адреса) для обновления.</span><span class="sxs-lookup"><span data-stu-id="c1623-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="c1623-150">Если не указано, команда использует источники, предоставляемые в файлах конфигурации см. в разделе [NuGet Настройка поведения](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="c1623-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="c1623-151">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="c1623-151">Verbosity</span></span> | <span data-ttu-id="c1623-152">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="c1623-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="c1623-153">Версия</span><span class="sxs-lookup"><span data-stu-id="c1623-153">Version</span></span> | <span data-ttu-id="c1623-154">Если для одного идентификатора пакета, указывает версию пакета для обновления.</span><span class="sxs-lookup"><span data-stu-id="c1623-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="c1623-155">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c1623-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c1623-156">Примеры</span><span class="sxs-lookup"><span data-stu-id="c1623-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
