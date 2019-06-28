---
title: Команда обновления интерфейса командной строки NuGet
description: Справочник по командам обновления nuget.exe
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a242d02a54fd86899cbe274ab63538b53307c1bb
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425919"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="3a865-103">Команда update (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3a865-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="3a865-104">**Применяется к:** упаковать потребления &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="3a865-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="3a865-105">Обновляет все пакеты в проекте (с помощью `packages.config`) до их последней доступной версии.</span><span class="sxs-lookup"><span data-stu-id="3a865-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="3a865-106">Мы рекомендуем запустить [«restore»](cli-ref-restore.md) перед запуском `update`.</span><span class="sxs-lookup"><span data-stu-id="3a865-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="3a865-107">(Чтобы обновить отдельный пакет, используйте [ `nuget install` ](cli-ref-install.md) без указания номера версии, в котором регистр NuGet устанавливает последнюю версию.)</span><span class="sxs-lookup"><span data-stu-id="3a865-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="3a865-108">Примечание: `update` не работает с интерфейсом командной строки, выполняемые с Mono (Mac OSX или Linux) или при использовании формата PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3a865-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="3a865-109">`update` Команда также обновляет ссылки на сборки в файле проекта, предоставляемых те ссылается на уже существует.</span><span class="sxs-lookup"><span data-stu-id="3a865-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="3a865-110">Если обновленный пакет добавлена сборки, новая ссылка является *не* добавлен.</span><span class="sxs-lookup"><span data-stu-id="3a865-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="3a865-111">Новые зависимости пакета также нет ссылки на сборки, их добавления.</span><span class="sxs-lookup"><span data-stu-id="3a865-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="3a865-112">Чтобы включить эти операции, как часть обновления, обновите пакет в Visual Studio с помощью пользовательского интерфейса диспетчера пакетов или консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="3a865-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="3a865-113">Эта команда также может использоваться для обновления nuget.exe себя с помощью *-self* флаг.</span><span class="sxs-lookup"><span data-stu-id="3a865-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="3a865-114">Использование</span><span class="sxs-lookup"><span data-stu-id="3a865-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="3a865-115">где `<configPath>` определяет либо `packages.config` или файл решения, который содержит список зависимостей проекта.</span><span class="sxs-lookup"><span data-stu-id="3a865-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="3a865-116">Параметры</span><span class="sxs-lookup"><span data-stu-id="3a865-116">Options</span></span>

| <span data-ttu-id="3a865-117">Параметр</span><span class="sxs-lookup"><span data-stu-id="3a865-117">Option</span></span> | <span data-ttu-id="3a865-118">Описание</span><span class="sxs-lookup"><span data-stu-id="3a865-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3a865-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3a865-119">ConfigFile</span></span> | <span data-ttu-id="3a865-120">Чтобы применить файл конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="3a865-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3a865-121">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="3a865-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3a865-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="3a865-122">FileConflictAction</span></span> | <span data-ttu-id="3a865-123">Указывает действие, выполняемое при появлении запроса на перезапись или игнорировать существующие файлы, связанные с проектом.</span><span class="sxs-lookup"><span data-stu-id="3a865-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="3a865-124">Значения: *перезаписать, игнорировать, none*.</span><span class="sxs-lookup"><span data-stu-id="3a865-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="3a865-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3a865-125">ForceEnglishOutput</span></span> | <span data-ttu-id="3a865-126">*(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры.</span><span class="sxs-lookup"><span data-stu-id="3a865-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3a865-127">Help</span><span class="sxs-lookup"><span data-stu-id="3a865-127">Help</span></span> | <span data-ttu-id="3a865-128">Отображает справку для команды.</span><span class="sxs-lookup"><span data-stu-id="3a865-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="3a865-129">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="3a865-129">Id</span></span> | <span data-ttu-id="3a865-130">Задает список идентификаторов для обновления пакета.</span><span class="sxs-lookup"><span data-stu-id="3a865-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="3a865-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="3a865-131">MSBuildPath</span></span> | <span data-ttu-id="3a865-132">*(4.0 и более поздние)*  Указывает путь к MSBuild для использования с командой, имеют приоритет перед `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="3a865-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="3a865-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="3a865-133">MSBuildVersion</span></span> | <span data-ttu-id="3a865-134">*(3.2 и более поздние)*  Указывает версию MSBuild для использования с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="3a865-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="3a865-135">Поддерживаемые значения: 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span><span class="sxs-lookup"><span data-stu-id="3a865-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="3a865-136">По умолчанию выбирается MSBuild в пути в противном случае по умолчанию установленных самую новую версию MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3a865-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="3a865-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3a865-137">NonInteractive</span></span> | <span data-ttu-id="3a865-138">Подавление для пользователя данные или подтверждения.</span><span class="sxs-lookup"><span data-stu-id="3a865-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3a865-139">Предварительные выпуски</span><span class="sxs-lookup"><span data-stu-id="3a865-139">PreRelease</span></span> | <span data-ttu-id="3a865-140">Позволяет обновлять для предварительных версий.</span><span class="sxs-lookup"><span data-stu-id="3a865-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="3a865-141">Этот флаг не является обязательным при обновлении предварительные версии пакетов, которые уже установлены.</span><span class="sxs-lookup"><span data-stu-id="3a865-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="3a865-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="3a865-142">RepositoryPath</span></span> | <span data-ttu-id="3a865-143">Указывает локальную папку, где устанавливаются пакеты.</span><span class="sxs-lookup"><span data-stu-id="3a865-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="3a865-144">Safe</span><span class="sxs-lookup"><span data-stu-id="3a865-144">Safe</span></span> | <span data-ttu-id="3a865-145">Указывает, обновляет только с самой высокой версией, доступных в той же основной и вспомогательной версии, установленные пакеты будут установлены.</span><span class="sxs-lookup"><span data-stu-id="3a865-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="3a865-146">SELF</span><span class="sxs-lookup"><span data-stu-id="3a865-146">Self</span></span> | <span data-ttu-id="3a865-147">Обновляет nuget.exe до последней версии; все другие аргументы игнорируются.</span><span class="sxs-lookup"><span data-stu-id="3a865-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="3a865-148">Source</span><span class="sxs-lookup"><span data-stu-id="3a865-148">Source</span></span> | <span data-ttu-id="3a865-149">Указывает список источников пакетов (в качестве URL-адреса) для обновления.</span><span class="sxs-lookup"><span data-stu-id="3a865-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="3a865-150">Если не указано, команда использует эти источники, в файлах конфигурации, см. в разделе [NuGet распространенных конфигураций](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="3a865-150">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="3a865-151">Verbosity</span><span class="sxs-lookup"><span data-stu-id="3a865-151">Verbosity</span></span> | <span data-ttu-id="3a865-152">Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="3a865-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="3a865-153">Версия</span><span class="sxs-lookup"><span data-stu-id="3a865-153">Version</span></span> | <span data-ttu-id="3a865-154">При использовании с один идентификатор пакета, указывает версию пакета для обновления.</span><span class="sxs-lookup"><span data-stu-id="3a865-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="3a865-155">Также см. в разделе [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3a865-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3a865-156">Примеры</span><span class="sxs-lookup"><span data-stu-id="3a865-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
