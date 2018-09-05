---
title: Справочник по PowerShell NuGet Install-Package
description: Справочник по команду PowerShell Install-Package в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: e7ddf9ad97cbb4ec9cfc8b01f366511239f41416
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546030"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="188b3-103">Install-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="188b3-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="188b3-104">*В этом разделе описываются команды в [консоли диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows. Общая команда PowerShell Install-Package, см. в разделе [Справочник по PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="188b3-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="188b3-105">Устанавливает пакет и его зависимости в проект.</span><span class="sxs-lookup"><span data-stu-id="188b3-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="188b3-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="188b3-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="188b3-107">В NuGet 2.8 + `Install-Package` возможность возврата существующего пакета в проекте.</span><span class="sxs-lookup"><span data-stu-id="188b3-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="188b3-108">Например если у вас установлен 5.1.0-rc1 Microsoft.AspNet.MVC, следующую команду бы понизить его до 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="188b3-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="188b3-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="188b3-109">Parameters</span></span>

| <span data-ttu-id="188b3-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="188b3-110">Parameter</span></span> | <span data-ttu-id="188b3-111">Описание</span><span class="sxs-lookup"><span data-stu-id="188b3-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="188b3-112">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="188b3-112">Id</span></span> | <span data-ttu-id="188b3-113">(Обязательно) Идентификатор пакета для установки.</span><span class="sxs-lookup"><span data-stu-id="188b3-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="188b3-114">(*3.0 +*) идентификатор может быть путь или URL-адрес `packages.config` файл или `.nupkg` файл.</span><span class="sxs-lookup"><span data-stu-id="188b3-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="188b3-115">— Идентификатор сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="188b3-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="188b3-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="188b3-116">IgnoreDependencies</span></span> | <span data-ttu-id="188b3-117">Установите только этот пакет, не к ее зависимостям.</span><span class="sxs-lookup"><span data-stu-id="188b3-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="188b3-118">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="188b3-118">ProjectName</span></span> | <span data-ttu-id="188b3-119">Проект, в который необходимо установить пакет, по умолчанию используется тип проекта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="188b3-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="188b3-120">Исходный код</span><span class="sxs-lookup"><span data-stu-id="188b3-120">Source</span></span> | <span data-ttu-id="188b3-121">Путь к URL-адрес или папке источника пакета для поиска.</span><span class="sxs-lookup"><span data-stu-id="188b3-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="188b3-122">Пути к локальной папке может быть абсолютным или относительным для текущей папки.</span><span class="sxs-lookup"><span data-stu-id="188b3-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="188b3-123">Если этот параметр опущен, `Install-Package` выполняет поиск в текущем выбранном источнике пакета.</span><span class="sxs-lookup"><span data-stu-id="188b3-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="188b3-124">Версия</span><span class="sxs-lookup"><span data-stu-id="188b3-124">Version</span></span> | <span data-ttu-id="188b3-125">Версия пакета, чтобы установить, по умолчанию до последней версии.</span><span class="sxs-lookup"><span data-stu-id="188b3-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="188b3-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="188b3-126">IncludePrerelease</span></span> | <span data-ttu-id="188b3-127">Считает, что предварительные версии пакетов для установки.</span><span class="sxs-lookup"><span data-stu-id="188b3-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="188b3-128">Если этот параметр опущен, учитываются только стабильные пакеты.</span><span class="sxs-lookup"><span data-stu-id="188b3-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="188b3-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="188b3-129">FileConflictAction</span></span> | <span data-ttu-id="188b3-130">Действие, выполняемое при появлении запроса на перезапись или игнорировать существующие файлы, связанные с проектом.</span><span class="sxs-lookup"><span data-stu-id="188b3-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="188b3-131">Возможные значения: *перезаписи, игнорировать, None, OverwriteAll*, и *(3.0 или более поздней)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="188b3-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="188b3-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="188b3-132">DependencyVersion</span></span> | <span data-ttu-id="188b3-133">Версия пакеты зависимостей для использования, которые может принимать одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="188b3-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="188b3-134">*Наименьшее* (по умолчанию): самую раннюю версию</span><span class="sxs-lookup"><span data-stu-id="188b3-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="188b3-135">*HighestPatch*: версии с улучшением минимально основных, минимально незначительные, самый высокий</span><span class="sxs-lookup"><span data-stu-id="188b3-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="188b3-136">*HighestMinor*: версия с наименьшим основных, наибольший исправления незначительных: наибольшая</span><span class="sxs-lookup"><span data-stu-id="188b3-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="188b3-137">*Самый высокий* (по умолчанию для Update-Package без параметров): самую старшую версию</span><span class="sxs-lookup"><span data-stu-id="188b3-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="188b3-138">Можно задать значение по умолчанию с помощью [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) в `Nuget.Config` файл.</span><span class="sxs-lookup"><span data-stu-id="188b3-138">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="188b3-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="188b3-139">WhatIf</span></span> | <span data-ttu-id="188b3-140">Показывает, что произойдет при выполнении команды без фактического выполнения установки.</span><span class="sxs-lookup"><span data-stu-id="188b3-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="188b3-141">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="188b3-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="188b3-142">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="188b3-142">Common Parameters</span></span>

<span data-ttu-id="188b3-143">`Install-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладки, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="188b3-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="188b3-144">Примеры</span><span class="sxs-lookup"><span data-stu-id="188b3-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
