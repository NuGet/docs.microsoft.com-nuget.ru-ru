---
title: Справка по синхронизации NuGet — пакет PowerShell
description: Ссылка на команду PowerShell Sync-Package в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 12a3d5f32056539a75da9e17b15d67e72a8a42c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384907"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="3d2f2-103">Sync-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3d2f2-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3d2f2-104">*Версия 3.0 +; доступно только в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="3d2f2-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="3d2f2-105">Возвращает версию установленного пакета из указанного проекта (или по умолчанию) и синхронизирует версию с остальными проектами в решении.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="3d2f2-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="3d2f2-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="3d2f2-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="3d2f2-107">Parameters</span></span>

| <span data-ttu-id="3d2f2-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="3d2f2-108">Parameter</span></span> | <span data-ttu-id="3d2f2-109">Описание</span><span class="sxs-lookup"><span data-stu-id="3d2f2-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3d2f2-110">Id</span><span class="sxs-lookup"><span data-stu-id="3d2f2-110">Id</span></span> | <span data-ttu-id="3d2f2-111">Необходимости Идентификатор пакета для синхронизации. Сам переключатель-ID является необязательным.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="3d2f2-112">игноредепенденЦиес</span><span class="sxs-lookup"><span data-stu-id="3d2f2-112">IgnoreDependencies</span></span> | <span data-ttu-id="3d2f2-113">Установить только этот пакет, но не его зависимости.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="3d2f2-114">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="3d2f2-114">ProjectName</span></span> | <span data-ttu-id="3d2f2-115">Проект, из которого необходимо синхронизировать пакет, по умолчанию используется проект по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="3d2f2-116">{2&gt;Version&lt;2}</span><span class="sxs-lookup"><span data-stu-id="3d2f2-116">Version</span></span> | <span data-ttu-id="3d2f2-117">Версия пакета для синхронизации, используемая по умолчанию для текущей установленной версии.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="3d2f2-118">Source</span><span class="sxs-lookup"><span data-stu-id="3d2f2-118">Source</span></span> | <span data-ttu-id="3d2f2-119">URL-адрес или путь к папке для источника пакета для поиска.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="3d2f2-120">Пути к локальным папкам могут быть абсолютными или относительно текущей папки.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="3d2f2-121">Если этот параметр опущен, `Sync-Package` выполняет поиск выбранного в данный момент источника пакета.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="3d2f2-122">инклудепререлеасе</span><span class="sxs-lookup"><span data-stu-id="3d2f2-122">IncludePrerelease</span></span> | <span data-ttu-id="3d2f2-123">Включает предварительные пакеты в синхронизацию.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="3d2f2-124">филеконфликтактион</span><span class="sxs-lookup"><span data-stu-id="3d2f2-124">FileConflictAction</span></span> | <span data-ttu-id="3d2f2-125">Действие, предпринимаемое при запросе перезаписи или пропуска существующих файлов, на которые ссылается проект.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="3d2f2-126">Возможные значения: *overwrite, ignore, None, овервритеалл*и *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="3d2f2-127">депенденциверсион</span><span class="sxs-lookup"><span data-stu-id="3d2f2-127">DependencyVersion</span></span> | <span data-ttu-id="3d2f2-128">Используемая версия пакетов зависимостей, которая может быть одной из следующих:</span><span class="sxs-lookup"><span data-stu-id="3d2f2-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="3d2f2-129">*Самый низкий* (по умолчанию): самая низкая версия</span><span class="sxs-lookup"><span data-stu-id="3d2f2-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="3d2f2-130">*Хигхестпатч*: версия с наименьшим основным, наименьшим незначительным, самым высоким исправлением</span><span class="sxs-lookup"><span data-stu-id="3d2f2-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="3d2f2-131">*Хигхестминор*: версия с наименьшим основным, наибольшим незначительным, самым высоким исправлением</span><span class="sxs-lookup"><span data-stu-id="3d2f2-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="3d2f2-132">*Высший* (по умолчанию для Update-Package без параметров): самая высокая версия</span><span class="sxs-lookup"><span data-stu-id="3d2f2-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="3d2f2-133">Значение по умолчанию можно задать с помощью параметра [`dependencyVersion`](../nuget-config-file.md#config-section) в файле `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="3d2f2-134">Whatif</span><span class="sxs-lookup"><span data-stu-id="3d2f2-134">WhatIf</span></span> | <span data-ttu-id="3d2f2-135">Показывает, что произойдет при выполнении команды без фактического выполнения синхронизации.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="3d2f2-136">Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3d2f2-137">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="3d2f2-137">Common Parameters</span></span>

<span data-ttu-id="3d2f2-138">`Sync-Package` поддерживает следующие [Общие параметры PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-138">`Sync-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3d2f2-139">Примеры</span><span class="sxs-lookup"><span data-stu-id="3d2f2-139">Examples</span></span>

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
