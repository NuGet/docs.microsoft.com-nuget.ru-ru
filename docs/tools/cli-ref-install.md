---
title: Команды установки NuGet CLI
description: Ссылка для установки команды nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 1c6ec1181f2f619eb8a4f2d87f7910f25b98e0f4
ms.sourcegitcommit: 00c4c809c69c16fcf4d81012eb53ea22f0691d0b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="a28e3-103">Команда install (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a28e3-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="a28e3-104">**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="a28e3-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a28e3-105">Загрузка и установка пакета в проект, установка значений по умолчанию для текущей папки, с помощью источников указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="a28e3-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="a28e3-106">Чтобы загрузить пакет непосредственно вне контекста проекта, посетите страницу пакета в [nuget.org](https://www.nuget.org) и выберите **загрузки** ссылку.</span><span class="sxs-lookup"><span data-stu-id="a28e3-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="a28e3-107">Если не указан ни один из источников, перечисленные в файле Глобальная конфигурация `%appdata%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac, Linux), используются.</span><span class="sxs-lookup"><span data-stu-id="a28e3-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="a28e3-108">В разделе [Настройка NuGet поведение](../consume-packages/configuring-nuget-behavior.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="a28e3-108">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="a28e3-109">Если не указано ни одного определенного пакета, `install` устанавливает все пакеты, перечисленные в проекте `packages.config` файл, сделав его аналогично [ `restore` ](cli-ref-restore.md).</span><span class="sxs-lookup"><span data-stu-id="a28e3-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="a28e3-110">`install` Команда не изменяла файл проекта или `packages.config`; таким образом, это похоже на `restore` в том, что он только добавляет пакеты на диск при этом не изменяется зависимостей проекта.</span><span class="sxs-lookup"><span data-stu-id="a28e3-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="a28e3-111">Чтобы добавить зависимость, добавьте пакет через пользовательский Интерфейс диспетчера пакетов или консоли в Visual Studio или изменить `packages.config` , а затем запустите либо `install` или `restore`.</span><span class="sxs-lookup"><span data-stu-id="a28e3-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="a28e3-112">Использование</span><span class="sxs-lookup"><span data-stu-id="a28e3-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="a28e3-113">где `<packageID>` имена пакета для установки (с использованием последней версии) или `<configFilePath>` идентифицирует `packages.config` файл, содержащий пакеты для установки.</span><span class="sxs-lookup"><span data-stu-id="a28e3-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="a28e3-114">Можно указать определенную версию с `-Version` параметр.</span><span class="sxs-lookup"><span data-stu-id="a28e3-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="a28e3-115">Параметры</span><span class="sxs-lookup"><span data-stu-id="a28e3-115">Options</span></span>

| <span data-ttu-id="a28e3-116">Параметр</span><span class="sxs-lookup"><span data-stu-id="a28e3-116">Option</span></span> | <span data-ttu-id="a28e3-117">Описание</span><span class="sxs-lookup"><span data-stu-id="a28e3-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a28e3-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a28e3-118">ConfigFile</span></span> | <span data-ttu-id="a28e3-119">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="a28e3-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a28e3-120">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="a28e3-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a28e3-121">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="a28e3-121">DependencyVersion</span></span> | <span data-ttu-id="a28e3-122">*(4.4 +)*  Указывает конкретную версию, переопределение поведения по умолчанию для разрешения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="a28e3-122">*(4.4+)* Specifies a specific version, overriding the default dependency resolution behavior.</span></span> |
| <span data-ttu-id="a28e3-123">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="a28e3-123">DisableParallelProcessing</span></span> | <span data-ttu-id="a28e3-124">Запрещение установки нескольких пакетов в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="a28e3-124">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="a28e3-125">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="a28e3-125">ExcludeVersion</span></span> | <span data-ttu-id="a28e3-126">Устанавливает пакет в папку с именем и имя пакета и не номер версии.</span><span class="sxs-lookup"><span data-stu-id="a28e3-126">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="a28e3-127">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="a28e3-127">FallbackSource</span></span> | <span data-ttu-id="a28e3-128">*(3.2 +)*  Список источников пакетов для использования как в случае ошибки в случае, если пакет не найден в основной или источник по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a28e3-128">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="a28e3-129">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a28e3-129">ForceEnglishOutput</span></span> | <span data-ttu-id="a28e3-130">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="a28e3-130">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a28e3-131">Платформа</span><span class="sxs-lookup"><span data-stu-id="a28e3-131">Framework</span></span> | <span data-ttu-id="a28e3-132">*(4.4 +)*  Требуемая версия .NET framework используется для выбора зависимостей.</span><span class="sxs-lookup"><span data-stu-id="a28e3-132">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="a28e3-133">Значение по умолчанию «Any» Если не указан.</span><span class="sxs-lookup"><span data-stu-id="a28e3-133">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="a28e3-134">Справка</span><span class="sxs-lookup"><span data-stu-id="a28e3-134">Help</span></span> | <span data-ttu-id="a28e3-135">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="a28e3-135">Displays help information for the command.</span></span> |
| <span data-ttu-id="a28e3-136">NoCache</span><span class="sxs-lookup"><span data-stu-id="a28e3-136">NoCache</span></span> | <span data-ttu-id="a28e3-137">Предотвращает использование кэшированных пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="a28e3-137">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="a28e3-138">В разделе [управление глобального пакетами и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="a28e3-138">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="a28e3-139">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a28e3-139">NonInteractive</span></span> | <span data-ttu-id="a28e3-140">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="a28e3-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a28e3-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="a28e3-141">OutputDirectory</span></span> | <span data-ttu-id="a28e3-142">Указывает папку, в которой устанавливаются пакеты.</span><span class="sxs-lookup"><span data-stu-id="a28e3-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="a28e3-143">Если папка не указана, используется текущая папка.</span><span class="sxs-lookup"><span data-stu-id="a28e3-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="a28e3-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="a28e3-144">PackageSaveMode</span></span> | <span data-ttu-id="a28e3-145">Указывает типы файлов для сохранения после установки пакета: один из `nuspec`, `nupkg`, или `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="a28e3-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="a28e3-146">PreRelease</span><span class="sxs-lookup"><span data-stu-id="a28e3-146">PreRelease</span></span> | <span data-ttu-id="a28e3-147">Позволяет предварительные пакеты для установки.</span><span class="sxs-lookup"><span data-stu-id="a28e3-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="a28e3-148">Этот флаг не является обязательным при восстановлении пакеты с `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="a28e3-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="a28e3-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="a28e3-149">RequireConsent</span></span> | <span data-ttu-id="a28e3-150">Восстановление пакетов проверяет, включена ли перед загрузкой и установкой пакетов.</span><span class="sxs-lookup"><span data-stu-id="a28e3-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="a28e3-151">Дополнительные сведения см. в разделе [восстановление пакетов](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="a28e3-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="a28e3-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="a28e3-152">SolutionDirectory</span></span> | <span data-ttu-id="a28e3-153">Задает корневую папку решения, для которого необходимо восстановить пакеты.</span><span class="sxs-lookup"><span data-stu-id="a28e3-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="a28e3-154">Исходный код</span><span class="sxs-lookup"><span data-stu-id="a28e3-154">Source</span></span> | <span data-ttu-id="a28e3-155">Указывает список источников пакетов (в виде URL-адреса) для использования.</span><span class="sxs-lookup"><span data-stu-id="a28e3-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="a28e3-156">Если не указано, команда использует источники, предоставляемые в файлах конфигурации см. в разделе [NuGet Настройка поведения](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="a28e3-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="a28e3-157">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="a28e3-157">Verbosity</span></span> | <span data-ttu-id="a28e3-158">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="a28e3-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="a28e3-159">Версия</span><span class="sxs-lookup"><span data-stu-id="a28e3-159">Version</span></span> | <span data-ttu-id="a28e3-160">Указывает версию пакета для установки.</span><span class="sxs-lookup"><span data-stu-id="a28e3-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="a28e3-161">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a28e3-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a28e3-162">Примеры</span><span class="sxs-lookup"><span data-stu-id="a28e3-162">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```