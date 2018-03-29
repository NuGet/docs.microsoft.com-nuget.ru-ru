---
title: Справочник по PowerShell пакет обновления NuGet | Документы Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Ссылка для команды PowerShell пакета обновления в консоли диспетчера пакетов NuGet в Visual Studio.
keywords: Пакет NuGet консоли диспетчера, команд NuGet Powershell, справочник по NuGet Powershell, пакет обновления
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 05772159d62f73e7d25f71ad36809f5ae8ef6aae
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="e4c63-104">Обновление (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e4c63-104">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e4c63-105">*Доступен только в пределах [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="e4c63-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e4c63-106">Обновляет пакет и его зависимости, а также все пакеты в проекте, до более новой версии.</span><span class="sxs-lookup"><span data-stu-id="e4c63-106">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="e4c63-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="e4c63-107">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="e4c63-108">В NuGet 2.8 + `Update-Package` можно использовать для возврата к предыдущей версии существующего пакета в проекте.</span><span class="sxs-lookup"><span data-stu-id="e4c63-108">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="e4c63-109">Например при наличии 5.1.0-rc1 Microsoft.AspNet.MVC установлен следующая команда будет понизить его до 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="e4c63-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="e4c63-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="e4c63-110">Parameters</span></span>

|  <span data-ttu-id="e4c63-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="e4c63-111">Parameter</span></span> | <span data-ttu-id="e4c63-112">Описание</span><span class="sxs-lookup"><span data-stu-id="e4c63-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e4c63-113">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="e4c63-113">Id</span></span> | <span data-ttu-id="e4c63-114">Идентификатор пакета для обновления.</span><span class="sxs-lookup"><span data-stu-id="e4c63-114">The identifier of the package to update.</span></span> <span data-ttu-id="e4c63-115">Если не указано, все пакеты обновления.</span><span class="sxs-lookup"><span data-stu-id="e4c63-115">If omitted, updates all packages.</span></span> <span data-ttu-id="e4c63-116">— Идентификатор коммутатора сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="e4c63-116">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="e4c63-117">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="e4c63-117">IgnoreDependencies</span></span> | <span data-ttu-id="e4c63-118">Пропускает обновление зависимости пакета.</span><span class="sxs-lookup"><span data-stu-id="e4c63-118">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="e4c63-119">Название проекта</span><span class="sxs-lookup"><span data-stu-id="e4c63-119">ProjectName</span></span> | <span data-ttu-id="e4c63-120">Имя проекта, содержащего пакеты для обновления, установка значений по умолчанию для всех проектов.</span><span class="sxs-lookup"><span data-stu-id="e4c63-120">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="e4c63-121">Версия</span><span class="sxs-lookup"><span data-stu-id="e4c63-121">Version</span></span> | <span data-ttu-id="e4c63-122">Версия, используемая для обновления, установка значений по умолчанию до последней версии.</span><span class="sxs-lookup"><span data-stu-id="e4c63-122">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="e4c63-123">В NuGet 3.0 + значение версии должно быть одним из *Lowest, самое высокое, HighestMinor*, или *HighestPatch* (эквивалентно - безопасный).</span><span class="sxs-lookup"><span data-stu-id="e4c63-123">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="e4c63-124">Safe</span><span class="sxs-lookup"><span data-stu-id="e4c63-124">Safe</span></span> | <span data-ttu-id="e4c63-125">Ограничивает только версии с той же номерами основной и дополнительной версии, в настоящее время установленного пакета обновления.</span><span class="sxs-lookup"><span data-stu-id="e4c63-125">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="e4c63-126">Исходный код</span><span class="sxs-lookup"><span data-stu-id="e4c63-126">Source</span></span> | <span data-ttu-id="e4c63-127">Путь URL-адрес или папку источника пакета для поиска.</span><span class="sxs-lookup"><span data-stu-id="e4c63-127">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="e4c63-128">Пути к локальной папке может быть абсолютным или относительным для текущей папки.</span><span class="sxs-lookup"><span data-stu-id="e4c63-128">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="e4c63-129">Если не указано, `Update-Package` выполняет поиск в текущем выбранном источнике пакетов.</span><span class="sxs-lookup"><span data-stu-id="e4c63-129">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="e4c63-130">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="e4c63-130">IncludePrerelease</span></span> | <span data-ttu-id="e4c63-131">Включает предварительные версии пакетов обновления.</span><span class="sxs-lookup"><span data-stu-id="e4c63-131">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="e4c63-132">Переустановка</span><span class="sxs-lookup"><span data-stu-id="e4c63-132">Reinstall</span></span> | <span data-ttu-id="e4c63-133">Resintalls пакетов с помощью текущей установленной версии.</span><span class="sxs-lookup"><span data-stu-id="e4c63-133">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="e4c63-134">Дополнительные сведения см. в разделе [Ограничение версий для обновления](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="e4c63-134">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="e4c63-135">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="e4c63-135">FileConflictAction</span></span> | <span data-ttu-id="e4c63-136">Действие, выполняемое при появлении запроса, чтобы игнорировать существующие файлы, связанные с проектом или перезаписать.</span><span class="sxs-lookup"><span data-stu-id="e4c63-136">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="e4c63-137">Возможными значениями являются *перезаписи, пропустить, None, OverwriteAll*, и *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="e4c63-137">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="e4c63-138">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="e4c63-138">DependencyVersion</span></span> | <span data-ttu-id="e4c63-139">Версия пакеты зависимостей для использования, которые может принимать одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="e4c63-139">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="e4c63-140">*Наименьший* (по умолчанию): самая ранняя версия</span><span class="sxs-lookup"><span data-stu-id="e4c63-140">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="e4c63-141">*HighestPatch*: версия с исправлением минимально основных минимально дополнительный: наибольшая</span><span class="sxs-lookup"><span data-stu-id="e4c63-141">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="e4c63-142">*HighestMinor*: версия с наименьшим основной, наивысший дополнительный номер: наибольшая исправления</span><span class="sxs-lookup"><span data-stu-id="e4c63-142">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="e4c63-143">*Наибольший* (по умолчанию для пакета обновления без параметров): самую новую версию</span><span class="sxs-lookup"><span data-stu-id="e4c63-143">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="e4c63-144">Можно задать значение по умолчанию с помощью [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) в `Nuget.Config` файла.</span><span class="sxs-lookup"><span data-stu-id="e4c63-144">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="e4c63-145">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="e4c63-145">ToHighestPatch</span></span> | <span data-ttu-id="e4c63-146">Ограничивает только версии с той же дополнительный номер версии, в настоящее время установленного пакета обновления.</span><span class="sxs-lookup"><span data-stu-id="e4c63-146">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="e4c63-147">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="e4c63-147">ToHighestMinor</span></span> | <span data-ttu-id="e4c63-148">Ограничивает только версии с одной и той же основной версии, установленный пакет обновления.</span><span class="sxs-lookup"><span data-stu-id="e4c63-148">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="e4c63-149">WhatIf</span><span class="sxs-lookup"><span data-stu-id="e4c63-149">WhatIf</span></span> | <span data-ttu-id="e4c63-150">Показывает, что произойдет при запуске команды без фактического выполнения обновления.</span><span class="sxs-lookup"><span data-stu-id="e4c63-150">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="e4c63-151">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="e4c63-151">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="e4c63-152">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="e4c63-152">Common Parameters</span></span>

<span data-ttu-id="e4c63-153">`Update-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e4c63-153">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="e4c63-154">Примеры</span><span class="sxs-lookup"><span data-stu-id="e4c63-154">Examples</span></span>

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
