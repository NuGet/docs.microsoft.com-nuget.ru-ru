---
title: Установка NuGet — Справочник по PowerShell для пакета
description: Справочник по команде PowerShell Install-Package в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 1899662049735189ab4dcb728df5d56afdc5f7c5
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327341"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="b2635-103">Install-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="b2635-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b2635-104">*В этом разделе описывается команда в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows. Для универсальной команды PowerShell Install-package см. Справочник по модульу [PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="b2635-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="b2635-105">Устанавливает пакет и его зависимости в проект.</span><span class="sxs-lookup"><span data-stu-id="b2635-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="b2635-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="b2635-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="b2635-107">В NuGet 2.8 + `Install-Package` может понизить уровень существующего пакета в проекте.</span><span class="sxs-lookup"><span data-stu-id="b2635-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="b2635-108">Например, при наличии установленного Microsoft. AspNet. MVC 5.1.0-RC1 Следующая команда понизить ее до 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="b2635-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="b2635-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="b2635-109">Parameters</span></span>

| <span data-ttu-id="b2635-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="b2635-110">Parameter</span></span> | <span data-ttu-id="b2635-111">Описание</span><span class="sxs-lookup"><span data-stu-id="b2635-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b2635-112">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="b2635-112">Id</span></span> | <span data-ttu-id="b2635-113">Необходимости Идентификатор устанавливаемого пакета.</span><span class="sxs-lookup"><span data-stu-id="b2635-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="b2635-114">(*3.0 +* ) Идентификатор может быть путем или URL-адресом `packages.config` файла `.nupkg` или файла.</span><span class="sxs-lookup"><span data-stu-id="b2635-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="b2635-115">Сам переключатель-ID является необязательным.</span><span class="sxs-lookup"><span data-stu-id="b2635-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="b2635-116">игноредепенденЦиес</span><span class="sxs-lookup"><span data-stu-id="b2635-116">IgnoreDependencies</span></span> | <span data-ttu-id="b2635-117">Установить только этот пакет, но не его зависимости.</span><span class="sxs-lookup"><span data-stu-id="b2635-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="b2635-118">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="b2635-118">ProjectName</span></span> | <span data-ttu-id="b2635-119">Проект, в который устанавливается пакет, по умолчанию используемый в качестве проекта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b2635-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="b2635-120">Source</span><span class="sxs-lookup"><span data-stu-id="b2635-120">Source</span></span> | <span data-ttu-id="b2635-121">URL-адрес или путь к папке для источника пакета для поиска.</span><span class="sxs-lookup"><span data-stu-id="b2635-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="b2635-122">Пути к локальным папкам могут быть абсолютными или относительно текущей папки.</span><span class="sxs-lookup"><span data-stu-id="b2635-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="b2635-123">Если этот параметр опущен `Install-Package` , поиск выполняется в текущем выбранном источнике пакета.</span><span class="sxs-lookup"><span data-stu-id="b2635-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="b2635-124">Версия</span><span class="sxs-lookup"><span data-stu-id="b2635-124">Version</span></span> | <span data-ttu-id="b2635-125">Версия устанавливаемого пакета, по умолчанию — последняя версия.</span><span class="sxs-lookup"><span data-stu-id="b2635-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="b2635-126">инклудепререлеасе</span><span class="sxs-lookup"><span data-stu-id="b2635-126">IncludePrerelease</span></span> | <span data-ttu-id="b2635-127">Учитываются предварительные пакеты для установки.</span><span class="sxs-lookup"><span data-stu-id="b2635-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="b2635-128">Если этот параметр опущен, учитываются только стабильные пакеты.</span><span class="sxs-lookup"><span data-stu-id="b2635-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="b2635-129">филеконфликтактион</span><span class="sxs-lookup"><span data-stu-id="b2635-129">FileConflictAction</span></span> | <span data-ttu-id="b2635-130">Действие, предпринимаемое при запросе перезаписи или пропуска существующих файлов, на которые ссылается проект.</span><span class="sxs-lookup"><span data-stu-id="b2635-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="b2635-131">Возможные значения: *overwrite, ignore, None, овервритеалл*и *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="b2635-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="b2635-132">депенденциверсион</span><span class="sxs-lookup"><span data-stu-id="b2635-132">DependencyVersion</span></span> | <span data-ttu-id="b2635-133">Используемая версия пакетов зависимостей, которая может быть одной из следующих:</span><span class="sxs-lookup"><span data-stu-id="b2635-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="b2635-134">*Самый низкий* (по умолчанию): самая низкая версия</span><span class="sxs-lookup"><span data-stu-id="b2635-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="b2635-135">*Хигхестпатч*: версия с наименьшим основным, наименьшим незначительным, самым высоким исправлением</span><span class="sxs-lookup"><span data-stu-id="b2635-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="b2635-136">*Хигхестминор*: версия с наименьшим основным, наибольшим незначительным, самым высоким исправлением</span><span class="sxs-lookup"><span data-stu-id="b2635-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="b2635-137">*Самый высокий* (по умолчанию для Update-Package без параметров): самая высокая версия</span><span class="sxs-lookup"><span data-stu-id="b2635-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="b2635-138">Значение по умолчанию можно задать с помощью [`dependencyVersion`](../nuget-config-file.md#config-section) параметра `Nuget.Config` в файле.</span><span class="sxs-lookup"><span data-stu-id="b2635-138">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="b2635-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="b2635-139">WhatIf</span></span> | <span data-ttu-id="b2635-140">Показывает, что произойдет при выполнении команды без фактического выполнения установки.</span><span class="sxs-lookup"><span data-stu-id="b2635-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="b2635-141">Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="b2635-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="b2635-142">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="b2635-142">Common Parameters</span></span>

<span data-ttu-id="b2635-143">`Install-Package`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b2635-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="b2635-144">Примеры</span><span class="sxs-lookup"><span data-stu-id="b2635-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
