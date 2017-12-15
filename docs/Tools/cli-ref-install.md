---
title: "Команда установки NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 59ac622f-837c-4545-bc93-a56330e02d71
description: "Ссылка для установки команды nuget.exe"
keywords: "NuGet установите ссылку, установите пакет команд"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88c123a7f2a3d628713cefcc4b110fb0205093b4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="6ef5a-104">Установите команду (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6ef5a-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="6ef5a-105">**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="6ef5a-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="6ef5a-106">Загрузка и установка пакета в проект, установка значений по умолчанию для текущей папки, с помощью источников указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="6ef5a-107">Чтобы загрузить пакет непосредственно вне контекста проекта, посетите страницу пакета в [nuget.org](https://www.nuget.org) и выберите **загрузки** ссылку.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span> 

<span data-ttu-id="6ef5a-108">Если не указан ни один из источников, перечисленные в файле глобальной конфигурации `%APPDATA%\NuGet\NuGet.Config`, используются.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-108">If no sources are specified, those listed in the global configuration file, `%APPDATA%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="6ef5a-109">В разделе [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-109">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="6ef5a-110">Если не указано ни одного определенного пакета, `install` устанавливает все пакеты, перечисленные в проекте `packages.config` файл, сделав его аналогично [ `restore` ](#restore).</span><span class="sxs-lookup"><span data-stu-id="6ef5a-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](#restore).</span></span> <span data-ttu-id="6ef5a-111">( `install` Команда не работает с `project.json`.)</span><span class="sxs-lookup"><span data-stu-id="6ef5a-111">(The `install` command does not work with `project.json`.)</span></span>

<span data-ttu-id="6ef5a-112">`install` Команда не изменяла файл проекта или `packages.config`; таким образом, это похоже на `restore` в том, что он только добавляет пакеты на диск при этом не изменяется зависимостей проекта.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-112">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="6ef5a-113">Добавление зависимости, добавьте к проекту через пользовательский Интерфейс диспетчера пакетов или консоли в Visual Studio или измените `packages.config` , а затем запустите либо `install` или `restore`.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-113">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span> <span data-ttu-id="6ef5a-114">Для проектов с помощью `project.json`, можно изменить этот файл и запустить `restore`.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-114">For projects using `project.json`, you can modify that file and then run `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="6ef5a-115">Использование</span><span class="sxs-lookup"><span data-stu-id="6ef5a-115">Usage</span></span>

```
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="6ef5a-116">где `<packageID>` имена пакета для установки (с использованием последней версии) или `<configFilePath>` идентифицирует `packages.config` файл, содержащий пакеты для установки.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-116">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="6ef5a-117">Можно указать определенную версию с `-Version` параметр.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-117">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="6ef5a-118">Параметры</span><span class="sxs-lookup"><span data-stu-id="6ef5a-118">Options</span></span>

| <span data-ttu-id="6ef5a-119">Параметр</span><span class="sxs-lookup"><span data-stu-id="6ef5a-119">Option</span></span> | <span data-ttu-id="6ef5a-120">Описание</span><span class="sxs-lookup"><span data-stu-id="6ef5a-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6ef5a-121">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6ef5a-121">ConfigFile</span></span> | <span data-ttu-id="6ef5a-122">*(2.5 +)*  NuGet файла конфигурации для применения.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="6ef5a-123">Если не указан, *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="6ef5a-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="6ef5a-124">DisableParallelProcessing</span></span> | <span data-ttu-id="6ef5a-125">Запрещение установки нескольких пакетов в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="6ef5a-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="6ef5a-126">ExcludeVersion</span></span> | <span data-ttu-id="6ef5a-127">Устанавливает пакет в папку с именем и имя пакета и не номер версии.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="6ef5a-128">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="6ef5a-128">FallbackSource</span></span> | <span data-ttu-id="6ef5a-129">*(3.2 +)*  Список источников пакетов для использования как в случае ошибки в случае, если пакет не найден в основной или источник по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="6ef5a-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6ef5a-130">ForceEnglishOutput</span></span> | <span data-ttu-id="6ef5a-131">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6ef5a-132">Платформа</span><span class="sxs-lookup"><span data-stu-id="6ef5a-132">Framework</span></span> | <span data-ttu-id="6ef5a-133">*(4.4 +)*  Требуемая версия .NET framework используется для выбора зависимостей.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="6ef5a-134">Значение по умолчанию «Any» Если не указан.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="6ef5a-135">Справка</span><span class="sxs-lookup"><span data-stu-id="6ef5a-135">Help</span></span> | <span data-ttu-id="6ef5a-136">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="6ef5a-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="6ef5a-137">NoCache</span></span> | <span data-ttu-id="6ef5a-138">Запрещает NuGet с помощью пакетов из кэшей локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="6ef5a-139">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="6ef5a-139">NonInteractive</span></span> | <span data-ttu-id="6ef5a-140">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="6ef5a-141">Выходной каталог</span><span class="sxs-lookup"><span data-stu-id="6ef5a-141">OutputDirectory</span></span> | <span data-ttu-id="6ef5a-142">Указывает папку, в которой устанавливаются пакеты.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="6ef5a-143">Если папка не указана, используется текущая папка.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="6ef5a-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="6ef5a-144">PackageSaveMode</span></span> | <span data-ttu-id="6ef5a-145">Указывает типы файлов для сохранения после установки пакета: один из `nuspec`, `nupkg`, или `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="6ef5a-146">Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="6ef5a-146">PreRelease</span></span> | <span data-ttu-id="6ef5a-147">Позволяет предварительные пакеты для установки.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="6ef5a-148">Этот флаг не является обязательным при восстановлении пакеты с `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="6ef5a-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="6ef5a-149">RequireConsent</span></span> | <span data-ttu-id="6ef5a-150">Восстановление пакетов проверяет, включена ли перед загрузкой и установкой пакетов.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="6ef5a-151">Дополнительные сведения см. в разделе [восстановление пакетов](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="6ef5a-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="6ef5a-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="6ef5a-152">SolutionDirectory</span></span> | <span data-ttu-id="6ef5a-153">Задает корневую папку решения, для которого необходимо восстановить пакеты.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="6ef5a-154">Исходный код</span><span class="sxs-lookup"><span data-stu-id="6ef5a-154">Source</span></span> | <span data-ttu-id="6ef5a-155">Указывает список источников пакетов (в виде URL-адреса) для использования.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="6ef5a-156">Если не указано, команда использует источники, предоставляемые в файлах конфигурации см. в разделе [NuGet Настройка поведения](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="6ef5a-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="6ef5a-157">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="6ef5a-157">Verbosity</span></span> | <span data-ttu-id="6ef5a-158">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="6ef5a-159">Версия</span><span class="sxs-lookup"><span data-stu-id="6ef5a-159">Version</span></span> | <span data-ttu-id="6ef5a-160">Указывает версию пакета для установки.</span><span class="sxs-lookup"><span data-stu-id="6ef5a-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="6ef5a-161">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6ef5a-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6ef5a-162">Примеры</span><span class="sxs-lookup"><span data-stu-id="6ef5a-162">Examples</span></span>

```
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
