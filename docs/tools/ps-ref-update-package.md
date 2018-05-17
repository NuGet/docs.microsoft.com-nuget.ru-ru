---
title: Справочник по PowerShell пакет обновления NuGet
description: Ссылка для команды PowerShell пакета обновления в консоли диспетчера пакетов NuGet в Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 621e59633117a29c58fe643860ee7e2b40a4fbe2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="c3f64-103">Update-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="c3f64-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="c3f64-104">*Доступен только в пределах [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="c3f64-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="c3f64-105">Обновляет пакет и его зависимости, а также все пакеты в проекте, до более новой версии.</span><span class="sxs-lookup"><span data-stu-id="c3f64-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="c3f64-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="c3f64-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="c3f64-107">В NuGet 2.8 + `Update-Package` можно использовать для возврата к предыдущей версии существующего пакета в проекте.</span><span class="sxs-lookup"><span data-stu-id="c3f64-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="c3f64-108">Например при наличии 5.1.0-rc1 Microsoft.AspNet.MVC установлен следующая команда будет понизить его до 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="c3f64-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="c3f64-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="c3f64-109">Parameters</span></span>

|  <span data-ttu-id="c3f64-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="c3f64-110">Parameter</span></span> | <span data-ttu-id="c3f64-111">Описание</span><span class="sxs-lookup"><span data-stu-id="c3f64-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c3f64-112">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="c3f64-112">Id</span></span> | <span data-ttu-id="c3f64-113">Идентификатор пакета для обновления.</span><span class="sxs-lookup"><span data-stu-id="c3f64-113">The identifier of the package to update.</span></span> <span data-ttu-id="c3f64-114">Если не указано, все пакеты обновления.</span><span class="sxs-lookup"><span data-stu-id="c3f64-114">If omitted, updates all packages.</span></span> <span data-ttu-id="c3f64-115">— Идентификатор коммутатора сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="c3f64-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="c3f64-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="c3f64-116">IgnoreDependencies</span></span> | <span data-ttu-id="c3f64-117">Пропускает обновление зависимости пакета.</span><span class="sxs-lookup"><span data-stu-id="c3f64-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="c3f64-118">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="c3f64-118">ProjectName</span></span> | <span data-ttu-id="c3f64-119">Имя проекта, содержащего пакеты для обновления, установка значений по умолчанию для всех проектов.</span><span class="sxs-lookup"><span data-stu-id="c3f64-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="c3f64-120">Версия</span><span class="sxs-lookup"><span data-stu-id="c3f64-120">Version</span></span> | <span data-ttu-id="c3f64-121">Версия, используемая для обновления, установка значений по умолчанию до последней версии.</span><span class="sxs-lookup"><span data-stu-id="c3f64-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="c3f64-122">В NuGet 3.0 + значение версии должно быть одним из *Lowest, самое высокое, HighestMinor*, или *HighestPatch* (эквивалентно - безопасный).</span><span class="sxs-lookup"><span data-stu-id="c3f64-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="c3f64-123">Safe</span><span class="sxs-lookup"><span data-stu-id="c3f64-123">Safe</span></span> | <span data-ttu-id="c3f64-124">Ограничивает только версии с той же номерами основной и дополнительной версии, в настоящее время установленного пакета обновления.</span><span class="sxs-lookup"><span data-stu-id="c3f64-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="c3f64-125">Исходный код</span><span class="sxs-lookup"><span data-stu-id="c3f64-125">Source</span></span> | <span data-ttu-id="c3f64-126">Путь URL-адрес или папку источника пакета для поиска.</span><span class="sxs-lookup"><span data-stu-id="c3f64-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="c3f64-127">Пути к локальной папке может быть абсолютным или относительным для текущей папки.</span><span class="sxs-lookup"><span data-stu-id="c3f64-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="c3f64-128">Если не указано, `Update-Package` выполняет поиск в текущем выбранном источнике пакетов.</span><span class="sxs-lookup"><span data-stu-id="c3f64-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="c3f64-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="c3f64-129">IncludePrerelease</span></span> | <span data-ttu-id="c3f64-130">Включает предварительные версии пакетов обновления.</span><span class="sxs-lookup"><span data-stu-id="c3f64-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="c3f64-131">Переустановка</span><span class="sxs-lookup"><span data-stu-id="c3f64-131">Reinstall</span></span> | <span data-ttu-id="c3f64-132">Resintalls пакетов с помощью текущей установленной версии.</span><span class="sxs-lookup"><span data-stu-id="c3f64-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="c3f64-133">Дополнительные сведения см. в разделе [Ограничение версий для обновления](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="c3f64-133">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="c3f64-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="c3f64-134">FileConflictAction</span></span> | <span data-ttu-id="c3f64-135">Действие, выполняемое при появлении запроса, чтобы игнорировать существующие файлы, связанные с проектом или перезаписать.</span><span class="sxs-lookup"><span data-stu-id="c3f64-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="c3f64-136">Возможными значениями являются *перезаписи, пропустить, None, OverwriteAll*, и *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="c3f64-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="c3f64-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="c3f64-137">DependencyVersion</span></span> | <span data-ttu-id="c3f64-138">Версия пакеты зависимостей для использования, которые может принимать одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="c3f64-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="c3f64-139">*Наименьший* (по умолчанию): самая ранняя версия</span><span class="sxs-lookup"><span data-stu-id="c3f64-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="c3f64-140">*HighestPatch*: версия с исправлением минимально основных минимально дополнительный: наибольшая</span><span class="sxs-lookup"><span data-stu-id="c3f64-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="c3f64-141">*HighestMinor*: версия с наименьшим основной, наивысший дополнительный номер: наибольшая исправления</span><span class="sxs-lookup"><span data-stu-id="c3f64-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="c3f64-142">*Наибольший* (по умолчанию для пакета обновления без параметров): самую новую версию</span><span class="sxs-lookup"><span data-stu-id="c3f64-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="c3f64-143">Можно задать значение по умолчанию с помощью [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) в `Nuget.Config` файла.</span><span class="sxs-lookup"><span data-stu-id="c3f64-143">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="c3f64-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="c3f64-144">ToHighestPatch</span></span> | <span data-ttu-id="c3f64-145">Ограничивает только версии с той же дополнительный номер версии, в настоящее время установленного пакета обновления.</span><span class="sxs-lookup"><span data-stu-id="c3f64-145">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="c3f64-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="c3f64-146">ToHighestMinor</span></span> | <span data-ttu-id="c3f64-147">Ограничивает только версии с одной и той же основной версии, установленный пакет обновления.</span><span class="sxs-lookup"><span data-stu-id="c3f64-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="c3f64-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="c3f64-148">WhatIf</span></span> | <span data-ttu-id="c3f64-149">Показывает, что произойдет при запуске команды без фактического выполнения обновления.</span><span class="sxs-lookup"><span data-stu-id="c3f64-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="c3f64-150">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="c3f64-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="c3f64-151">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="c3f64-151">Common Parameters</span></span>

<span data-ttu-id="c3f64-152">`Update-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c3f64-152">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="c3f64-153">Примеры</span><span class="sxs-lookup"><span data-stu-id="c3f64-153">Examples</span></span>

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```