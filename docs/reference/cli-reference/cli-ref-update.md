---
title: Команда обновления интерфейса командной строки NuGet
description: Справочник по команде nuget.exe Update
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 84f939188ac190f6d539f8ee2b422049a274f178
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622581"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="0bf12-103">команда Update (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="0bf12-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="0bf12-104">Область **применения:** &bullet; **Поддерживаемые версии** для использования пакетов: все</span><span class="sxs-lookup"><span data-stu-id="0bf12-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="0bf12-105">При этом все пакеты в проекте, использующем файл `packages.config`, обновляются до последней доступной версии.</span><span class="sxs-lookup"><span data-stu-id="0bf12-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="0bf12-106">Рекомендуется выполнить [инструкцию RESTORE](cli-ref-restore.md) перед запуском `update` .</span><span class="sxs-lookup"><span data-stu-id="0bf12-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="0bf12-107">(Чтобы обновить отдельный пакет, используйте [`nuget install`](cli-ref-install.md) без указания номера версии. в этом случае NuGet устанавливает последнюю версию.)</span><span class="sxs-lookup"><span data-stu-id="0bf12-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="0bf12-108">Примечание. не `update` работает с интерфейсом командной строки, работающим под управлением Mono (Mac OSX или Linux) или при использовании формата PackageReference.</span><span class="sxs-lookup"><span data-stu-id="0bf12-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="0bf12-109">`update`Команда также обновляет ссылки на сборки в файле проекта при условии, что эти ссылки уже существуют.</span><span class="sxs-lookup"><span data-stu-id="0bf12-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="0bf12-110">Если обновленный пакет содержит добавленную сборку, Новая ссылка *не* добавляется.</span><span class="sxs-lookup"><span data-stu-id="0bf12-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="0bf12-111">Для новых зависимостей пакетов также не добавляются ссылки на сборки.</span><span class="sxs-lookup"><span data-stu-id="0bf12-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="0bf12-112">Чтобы включить эти операции в состав обновления, обновите пакет в Visual Studio с помощью пользовательского интерфейса диспетчера пакетов или консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="0bf12-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="0bf12-113">Эту команду также можно использовать для обновления nuget.exe, используя флаг *-Self* .</span><span class="sxs-lookup"><span data-stu-id="0bf12-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="0bf12-114">Использование</span><span class="sxs-lookup"><span data-stu-id="0bf12-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="0bf12-115">где `<configPath>` определяет либо `packages.config` файл решения, либо список зависимостей проекта.</span><span class="sxs-lookup"><span data-stu-id="0bf12-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="0bf12-116">Параметры</span><span class="sxs-lookup"><span data-stu-id="0bf12-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="0bf12-117">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="0bf12-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="0bf12-118">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="0bf12-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="0bf12-119">Указывает действие по умолчанию, если файл из пакета уже существует в целевом проекте.</span><span class="sxs-lookup"><span data-stu-id="0bf12-119">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="0bf12-120">Установите значение `Overwrite` , чтобы всегда перезаписывать файлы.</span><span class="sxs-lookup"><span data-stu-id="0bf12-120">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="0bf12-121">Задайте для значение `Ignore` , чтобы пропустить файлы.</span><span class="sxs-lookup"><span data-stu-id="0bf12-121">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="0bf12-122">`PromptUser`Действие, используемое по умолчанию, запрашивает каждый конфликтующий файл, если не `OverwriteAll` `IgnoreAll` указан параметр или, который будет применяться ко всем оставшимся файлам.</span><span class="sxs-lookup"><span data-stu-id="0bf12-122">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="0bf12-123">*(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="0bf12-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="0bf12-124">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="0bf12-124">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="0bf12-125">Указывает список идентификаторов пакетов для обновления.</span><span class="sxs-lookup"><span data-stu-id="0bf12-125">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="0bf12-126">*(4.0 +)* Указывает путь MSBuild для использования с командой, который имеет приоритет над `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="0bf12-126">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="0bf12-127">*(3.2 +)* Указывает версию MSBuild, которая будет использоваться с этой командой.</span><span class="sxs-lookup"><span data-stu-id="0bf12-127">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="0bf12-128">Поддерживаемые значения: 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="0bf12-128">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="0bf12-129">По умолчанию в пути выбирается MSBuild, в противном случае — по умолчанию — самая высокая установленная версия MSBuild.</span><span class="sxs-lookup"><span data-stu-id="0bf12-129">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="0bf12-130">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="0bf12-130">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="0bf12-131">Разрешает обновление до предварительных версий.</span><span class="sxs-lookup"><span data-stu-id="0bf12-131">Allows updating to prerelease versions.</span></span> <span data-ttu-id="0bf12-132">Этот флаг не требуется при обновлении уже установленных пакетов предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="0bf12-132">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="0bf12-133">Указывает локальную папку, в которую устанавливаются пакеты.</span><span class="sxs-lookup"><span data-stu-id="0bf12-133">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="0bf12-134">Указывает, что будут установлены только обновления с самой высокой версией в той же основной и дополнительной версии, что и установленный пакет.</span><span class="sxs-lookup"><span data-stu-id="0bf12-134">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="0bf12-135">Обновляет nuget.exe до последней версии; все остальные аргументы игнорируются.</span><span class="sxs-lookup"><span data-stu-id="0bf12-135">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span>

- **`-Source`**

  <span data-ttu-id="0bf12-136">Указывает список источников пакетов (в виде URL-адресов), используемых для обновлений.</span><span class="sxs-lookup"><span data-stu-id="0bf12-136">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="0bf12-137">Если этот параметр не указан, команда использует источники, предоставленные в файлах конфигурации, см. раздел [Общие конфигурации NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="0bf12-137">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="0bf12-138">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="0bf12-138">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="0bf12-139">При использовании с одним ИДЕНТИФИКАТОРом пакета указывает версию пакета для обновления.</span><span class="sxs-lookup"><span data-stu-id="0bf12-139">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="0bf12-140">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0bf12-140">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0bf12-141">Примеры</span><span class="sxs-lookup"><span data-stu-id="0bf12-141">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
