---
title: "Команда установки NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Ссылка для установки команды nuget.exe"
keywords: "NuGet установите ссылку, установите пакет команд"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9e824b08486704371eebefb964f86315d82fc222
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/14/2018
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="aeed7-104">Установите команду (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="aeed7-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="aeed7-105">**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="aeed7-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="aeed7-106">Загрузка и установка пакета в проект, установка значений по умолчанию для текущей папки, с помощью источников указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="aeed7-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="aeed7-107">Чтобы загрузить пакет непосредственно вне контекста проекта, посетите страницу пакета в [nuget.org](https://www.nuget.org) и выберите **загрузки** ссылку.</span><span class="sxs-lookup"><span data-stu-id="aeed7-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="aeed7-108">Если не указан ни один из источников, перечисленные в файле глобальной конфигурации `%APPDATA%\NuGet\NuGet.Config`, используются.</span><span class="sxs-lookup"><span data-stu-id="aeed7-108">If no sources are specified, those listed in the global configuration file, `%APPDATA%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="aeed7-109">В разделе [Настройка NuGet поведение](../consume-packages/configuring-nuget-behavior.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="aeed7-109">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="aeed7-110">Если не указано ни одного определенного пакета, `install` устанавливает все пакеты, перечисленные в проекте `packages.config` файл, сделав его аналогично [ `restore` ](cli-ref-restore.md).</span><span class="sxs-lookup"><span data-stu-id="aeed7-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="aeed7-111">`install` Команда не изменяла файл проекта или `packages.config`; таким образом, это похоже на `restore` в том, что он только добавляет пакеты на диск при этом не изменяется зависимостей проекта.</span><span class="sxs-lookup"><span data-stu-id="aeed7-111">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="aeed7-112">Добавление зависимости, добавьте к проекту через пользовательский Интерфейс диспетчера пакетов или консоли в Visual Studio или измените `packages.config` , а затем запустите либо `install` или `restore`.</span><span class="sxs-lookup"><span data-stu-id="aeed7-112">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="aeed7-113">Использование</span><span class="sxs-lookup"><span data-stu-id="aeed7-113">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="aeed7-114">где `<packageID>` имена пакета для установки (с использованием последней версии) или `<configFilePath>` идентифицирует `packages.config` файл, содержащий пакеты для установки.</span><span class="sxs-lookup"><span data-stu-id="aeed7-114">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="aeed7-115">Можно указать определенную версию с `-Version` параметр.</span><span class="sxs-lookup"><span data-stu-id="aeed7-115">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="aeed7-116">Параметры</span><span class="sxs-lookup"><span data-stu-id="aeed7-116">Options</span></span>

| <span data-ttu-id="aeed7-117">Параметр</span><span class="sxs-lookup"><span data-stu-id="aeed7-117">Option</span></span> | <span data-ttu-id="aeed7-118">Описание:</span><span class="sxs-lookup"><span data-stu-id="aeed7-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aeed7-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="aeed7-119">ConfigFile</span></span> | <span data-ttu-id="aeed7-120">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="aeed7-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="aeed7-121">Если не указан, *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="aeed7-121">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="aeed7-122">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="aeed7-122">DependencyVersion</span></span> | <span data-ttu-id="aeed7-123">*(4.4 +)*  Указывает конкретную версию, переопределение поведения по умолчанию для разрешения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="aeed7-123">*(4.4+)* Specifies a specific version, overriding the default dependency resolution behavior.</span></span> |
| <span data-ttu-id="aeed7-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="aeed7-124">DisableParallelProcessing</span></span> | <span data-ttu-id="aeed7-125">Запрещение установки нескольких пакетов в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="aeed7-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="aeed7-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="aeed7-126">ExcludeVersion</span></span> | <span data-ttu-id="aeed7-127">Устанавливает пакет в папку с именем и имя пакета и не номер версии.</span><span class="sxs-lookup"><span data-stu-id="aeed7-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="aeed7-128">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="aeed7-128">FallbackSource</span></span> | <span data-ttu-id="aeed7-129">*(3.2 +)*  Список источников пакетов для использования как в случае ошибки в случае, если пакет не найден в основной или источник по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="aeed7-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="aeed7-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="aeed7-130">ForceEnglishOutput</span></span> | <span data-ttu-id="aeed7-131">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="aeed7-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="aeed7-132">Платформа</span><span class="sxs-lookup"><span data-stu-id="aeed7-132">Framework</span></span> | <span data-ttu-id="aeed7-133">*(4.4 +)*  Требуемая версия .NET framework используется для выбора зависимостей.</span><span class="sxs-lookup"><span data-stu-id="aeed7-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="aeed7-134">Значение по умолчанию «Any» Если не указан.</span><span class="sxs-lookup"><span data-stu-id="aeed7-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="aeed7-135">Справка</span><span class="sxs-lookup"><span data-stu-id="aeed7-135">Help</span></span> | <span data-ttu-id="aeed7-136">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="aeed7-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="aeed7-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="aeed7-137">NoCache</span></span> | <span data-ttu-id="aeed7-138">Запрещает NuGet с помощью пакетов из кэшей локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="aeed7-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="aeed7-139">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="aeed7-139">NonInteractive</span></span> | <span data-ttu-id="aeed7-140">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="aeed7-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="aeed7-141">Выходной каталог</span><span class="sxs-lookup"><span data-stu-id="aeed7-141">OutputDirectory</span></span> | <span data-ttu-id="aeed7-142">Указывает папку, в которой устанавливаются пакеты.</span><span class="sxs-lookup"><span data-stu-id="aeed7-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="aeed7-143">Если папка не указана, используется текущая папка.</span><span class="sxs-lookup"><span data-stu-id="aeed7-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="aeed7-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="aeed7-144">PackageSaveMode</span></span> | <span data-ttu-id="aeed7-145">Указывает типы файлов для сохранения после установки пакета: один из `nuspec`, `nupkg`, или `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="aeed7-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="aeed7-146">Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="aeed7-146">PreRelease</span></span> | <span data-ttu-id="aeed7-147">Позволяет предварительные пакеты для установки.</span><span class="sxs-lookup"><span data-stu-id="aeed7-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="aeed7-148">Этот флаг не является обязательным при восстановлении пакеты с `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="aeed7-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="aeed7-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="aeed7-149">RequireConsent</span></span> | <span data-ttu-id="aeed7-150">Восстановление пакетов проверяет, включена ли перед загрузкой и установкой пакетов.</span><span class="sxs-lookup"><span data-stu-id="aeed7-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="aeed7-151">Дополнительные сведения см. в разделе [восстановление пакетов](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="aeed7-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="aeed7-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="aeed7-152">SolutionDirectory</span></span> | <span data-ttu-id="aeed7-153">Задает корневую папку решения, для которого необходимо восстановить пакеты.</span><span class="sxs-lookup"><span data-stu-id="aeed7-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="aeed7-154">Исходный код</span><span class="sxs-lookup"><span data-stu-id="aeed7-154">Source</span></span> | <span data-ttu-id="aeed7-155">Указывает список источников пакетов (в виде URL-адреса) для использования.</span><span class="sxs-lookup"><span data-stu-id="aeed7-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="aeed7-156">Если не указано, команда использует источники, предоставляемые в файлах конфигурации см. в разделе [NuGet Настройка поведения](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="aeed7-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="aeed7-157">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="aeed7-157">Verbosity</span></span> | <span data-ttu-id="aeed7-158">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="aeed7-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="aeed7-159">Версия</span><span class="sxs-lookup"><span data-stu-id="aeed7-159">Version</span></span> | <span data-ttu-id="aeed7-160">Указывает версию пакета для установки.</span><span class="sxs-lookup"><span data-stu-id="aeed7-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="aeed7-161">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="aeed7-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="aeed7-162">Примеры</span><span class="sxs-lookup"><span data-stu-id="aeed7-162">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
