---
title: Справочник по PowerShell Sync пакет NuGet
description: Ссылка для команды PowerShell пакета синхронизации в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8119664b1bafe9238b12b1819cc46dc1ee7bdd00
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547998"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="992e4-103">Sync-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="992e4-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="992e4-104">*3.0 и более поздних версиях; доступен только в пределах [консоли диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="992e4-104">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="992e4-105">Возвращает версию установленного пакета из указанного (или по умолчанию), проекта и синхронизирует версии для остальных проектов в решении.</span><span class="sxs-lookup"><span data-stu-id="992e4-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="992e4-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="992e4-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="992e4-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="992e4-107">Parameters</span></span>

| <span data-ttu-id="992e4-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="992e4-108">Parameter</span></span> | <span data-ttu-id="992e4-109">Описание</span><span class="sxs-lookup"><span data-stu-id="992e4-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="992e4-110">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="992e4-110">Id</span></span> | <span data-ttu-id="992e4-111">(Обязательно) Идентификатор пакета для синхронизации. — Идентификатор сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="992e4-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="992e4-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="992e4-112">IgnoreDependencies</span></span> | <span data-ttu-id="992e4-113">Установите только этот пакет, не к ее зависимостям.</span><span class="sxs-lookup"><span data-stu-id="992e4-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="992e4-114">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="992e4-114">ProjectName</span></span> | <span data-ttu-id="992e4-115">Проект для синхронизации пакета, по умолчанию используется тип проекта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="992e4-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="992e4-116">Версия</span><span class="sxs-lookup"><span data-stu-id="992e4-116">Version</span></span> | <span data-ttu-id="992e4-117">Версия пакета для синхронизации, установка значений по умолчанию для текущей установленной версии.</span><span class="sxs-lookup"><span data-stu-id="992e4-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="992e4-118">Исходный код</span><span class="sxs-lookup"><span data-stu-id="992e4-118">Source</span></span> | <span data-ttu-id="992e4-119">Путь к URL-адрес или папке источника пакета для поиска.</span><span class="sxs-lookup"><span data-stu-id="992e4-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="992e4-120">Пути к локальной папке может быть абсолютным или относительным для текущей папки.</span><span class="sxs-lookup"><span data-stu-id="992e4-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="992e4-121">Если этот параметр опущен, `Sync-Package` выполняет поиск в текущем выбранном источнике пакета.</span><span class="sxs-lookup"><span data-stu-id="992e4-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="992e4-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="992e4-122">IncludePrerelease</span></span> | <span data-ttu-id="992e4-123">Включает предварительные версии пакетов в синхронизации.</span><span class="sxs-lookup"><span data-stu-id="992e4-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="992e4-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="992e4-124">FileConflictAction</span></span> | <span data-ttu-id="992e4-125">Действие, выполняемое при появлении запроса на перезапись или игнорировать существующие файлы, связанные с проектом.</span><span class="sxs-lookup"><span data-stu-id="992e4-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="992e4-126">Возможные значения: *перезаписи, игнорировать, None, OverwriteAll*, и *(3.0 или более поздней)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="992e4-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="992e4-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="992e4-127">DependencyVersion</span></span> | <span data-ttu-id="992e4-128">Версия пакеты зависимостей для использования, которые может принимать одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="992e4-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="992e4-129">*Наименьшее* (по умолчанию): самую раннюю версию</span><span class="sxs-lookup"><span data-stu-id="992e4-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="992e4-130">*HighestPatch*: версии с улучшением минимально основных, минимально незначительные, самый высокий</span><span class="sxs-lookup"><span data-stu-id="992e4-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="992e4-131">*HighestMinor*: версия с наименьшим основных, наибольший исправления незначительных: наибольшая</span><span class="sxs-lookup"><span data-stu-id="992e4-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="992e4-132">*Самый высокий* (по умолчанию для Update-Package без параметров): самую старшую версию</span><span class="sxs-lookup"><span data-stu-id="992e4-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="992e4-133">Можно задать значение по умолчанию с помощью [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) в `Nuget.Config` файл.</span><span class="sxs-lookup"><span data-stu-id="992e4-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="992e4-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="992e4-134">WhatIf</span></span> | <span data-ttu-id="992e4-135">Показывает, что произойдет при выполнении команды без фактического выполнения синхронизации.</span><span class="sxs-lookup"><span data-stu-id="992e4-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="992e4-136">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="992e4-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="992e4-137">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="992e4-137">Common Parameters</span></span>

<span data-ttu-id="992e4-138">`Sync-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладки, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="992e4-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="992e4-139">Примеры</span><span class="sxs-lookup"><span data-stu-id="992e4-139">Examples</span></span>

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
