---
title: Справочник по PowerShell NuGet Update-Package
description: Ссылка для команды PowerShell Update-Package в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5b5a11ee11d9e2cf6a90d56ac63b1f7bad750ea
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496493"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="13715-103">Update-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="13715-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="13715-104">*Доступен только в пределах [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="13715-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="13715-105">Обновляет пакет и его зависимостей или все пакеты в проекте, до более новой версии.</span><span class="sxs-lookup"><span data-stu-id="13715-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="13715-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="13715-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="13715-107">В NuGet 2.8 + `Update-Package` можно использовать для возврата к предыдущей версии существующего пакета в проекте.</span><span class="sxs-lookup"><span data-stu-id="13715-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="13715-108">Например если у вас установлен 5.1.0-rc1 Microsoft.AspNet.MVC, следующую команду бы понизить его до 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="13715-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="13715-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="13715-109">Parameters</span></span>

|  <span data-ttu-id="13715-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="13715-110">Parameter</span></span> | <span data-ttu-id="13715-111">Описание</span><span class="sxs-lookup"><span data-stu-id="13715-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="13715-112">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="13715-112">Id</span></span> | <span data-ttu-id="13715-113">Идентификатор пакета для обновления.</span><span class="sxs-lookup"><span data-stu-id="13715-113">The identifier of the package to update.</span></span> <span data-ttu-id="13715-114">Если этот параметр опущен, обновляет все пакеты.</span><span class="sxs-lookup"><span data-stu-id="13715-114">If omitted, updates all packages.</span></span> <span data-ttu-id="13715-115">— Идентификатор сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="13715-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="13715-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="13715-116">IgnoreDependencies</span></span> | <span data-ttu-id="13715-117">Пропускает обновление зависимостей пакетов.</span><span class="sxs-lookup"><span data-stu-id="13715-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="13715-118">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="13715-118">ProjectName</span></span> | <span data-ttu-id="13715-119">Имя проекта, содержащего пакеты для обновления, установка значений по умолчанию для всех проектов.</span><span class="sxs-lookup"><span data-stu-id="13715-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="13715-120">Версия</span><span class="sxs-lookup"><span data-stu-id="13715-120">Version</span></span> | <span data-ttu-id="13715-121">Версия, используемая для обновления, установка значений по умолчанию до последней версии.</span><span class="sxs-lookup"><span data-stu-id="13715-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="13715-122">В NuGet 3.0 +, значение версии должно быть одно из *Lowest, самое высокое, HighestMinor*, или *HighestPatch* (эквивалент метода - Safe).</span><span class="sxs-lookup"><span data-stu-id="13715-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="13715-123">Safe</span><span class="sxs-lookup"><span data-stu-id="13715-123">Safe</span></span> | <span data-ttu-id="13715-124">Ограничивает обновления до версии с той же версии основного и дополнительного номера, что и установленный пакет.</span><span class="sxs-lookup"><span data-stu-id="13715-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="13715-125">Source</span><span class="sxs-lookup"><span data-stu-id="13715-125">Source</span></span> | <span data-ttu-id="13715-126">Путь к URL-адрес или папке источника пакета для поиска.</span><span class="sxs-lookup"><span data-stu-id="13715-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="13715-127">Пути к локальной папке может быть абсолютным или относительным для текущей папки.</span><span class="sxs-lookup"><span data-stu-id="13715-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="13715-128">Если этот параметр опущен, `Update-Package` выполняет поиск в текущем выбранном источнике пакета.</span><span class="sxs-lookup"><span data-stu-id="13715-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="13715-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="13715-129">IncludePrerelease</span></span> | <span data-ttu-id="13715-130">Включает в себя предварительные выпуски пакетов обновлений.</span><span class="sxs-lookup"><span data-stu-id="13715-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="13715-131">Переустановка</span><span class="sxs-lookup"><span data-stu-id="13715-131">Reinstall</span></span> | <span data-ttu-id="13715-132">Resintalls пакетов с помощью их текущей установленной версии.</span><span class="sxs-lookup"><span data-stu-id="13715-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="13715-133">Дополнительные сведения см. в разделе [Ограничение версий для обновления](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="13715-133">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="13715-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="13715-134">FileConflictAction</span></span> | <span data-ttu-id="13715-135">Действие, выполняемое при появлении запроса на перезапись или игнорировать существующие файлы, связанные с проектом.</span><span class="sxs-lookup"><span data-stu-id="13715-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="13715-136">Возможные значения: *перезаписи, игнорировать, None, OverwriteAll*, и *IgnoreAll* (3.0 или более поздней).</span><span class="sxs-lookup"><span data-stu-id="13715-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="13715-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="13715-137">DependencyVersion</span></span> | <span data-ttu-id="13715-138">Версия пакеты зависимостей для использования, которые может принимать одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="13715-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="13715-139">*Наименьшее* (по умолчанию): самую раннюю версию</span><span class="sxs-lookup"><span data-stu-id="13715-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="13715-140">*HighestPatch*: версии с улучшением минимально основных, минимально незначительные, самый высокий</span><span class="sxs-lookup"><span data-stu-id="13715-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="13715-141">*HighestMinor*: версия с наименьшим основных, наибольший исправления незначительных: наибольшая</span><span class="sxs-lookup"><span data-stu-id="13715-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="13715-142">*Самый высокий* (по умолчанию для Update-Package без параметров): самую старшую версию</span><span class="sxs-lookup"><span data-stu-id="13715-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="13715-143">Можно задать значение по умолчанию с помощью [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) в `Nuget.Config` файл.</span><span class="sxs-lookup"><span data-stu-id="13715-143">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="13715-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="13715-144">ToHighestPatch</span></span> | <span data-ttu-id="13715-145">Эквивалент - Safe.</span><span class="sxs-lookup"><span data-stu-id="13715-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="13715-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="13715-146">ToHighestMinor</span></span> | <span data-ttu-id="13715-147">Ограничивает обновления до версий только с той же основной версией, что и установленный пакет.</span><span class="sxs-lookup"><span data-stu-id="13715-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="13715-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="13715-148">WhatIf</span></span> | <span data-ttu-id="13715-149">Показывает, что произойдет при выполнении команды без фактического выполнения обновления.</span><span class="sxs-lookup"><span data-stu-id="13715-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="13715-150">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="13715-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="13715-151">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="13715-151">Common Parameters</span></span>

<span data-ttu-id="13715-152">`Update-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="13715-152">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="13715-153">Примеры</span><span class="sxs-lookup"><span data-stu-id="13715-153">Examples</span></span>

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
