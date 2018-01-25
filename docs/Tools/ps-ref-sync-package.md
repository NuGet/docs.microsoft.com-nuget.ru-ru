---
title: "Справочник по PowerShell синхронизации пакет NuGet | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Ссылка для команды PowerShell пакета синхронизации в консоли диспетчера пакетов NuGet в Visual Studio."
keywords: "Пакет NuGet консоли диспетчера, команд NuGet Powershell, справочник по NuGet Powershell, пакета синхронизации"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 02233cd0532fab2338e65e0d58b9afc3e2dab6af
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="28aa9-104">Sync-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="28aa9-104">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="28aa9-105">*Версия 3.0 +; доступен только в пределах [консоль диспетчера пакетов NuGet](Package-Manager-Console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="28aa9-105">*Version 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="28aa9-106">Возвращает версию установленного пакета из указанного (или по умолчанию), проекта и синхронизируется с остальными проектами в решении.</span><span class="sxs-lookup"><span data-stu-id="28aa9-106">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="28aa9-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="28aa9-107">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="28aa9-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="28aa9-108">Parameters</span></span>

| <span data-ttu-id="28aa9-109">Параметр</span><span class="sxs-lookup"><span data-stu-id="28aa9-109">Parameter</span></span> | <span data-ttu-id="28aa9-110">Описание:</span><span class="sxs-lookup"><span data-stu-id="28aa9-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="28aa9-111">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="28aa9-111">Id</span></span> | <span data-ttu-id="28aa9-112">(Обязательно) Идентификатор пакета для синхронизации. — Идентификатор коммутатора сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="28aa9-112">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="28aa9-113">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="28aa9-113">IgnoreDependencies</span></span> | <span data-ttu-id="28aa9-114">Установите только этот пакет, а не его зависимости.</span><span class="sxs-lookup"><span data-stu-id="28aa9-114">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="28aa9-115">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="28aa9-115">ProjectName</span></span> | <span data-ttu-id="28aa9-116">Проект для синхронизации пакета, установка значений по умолчанию для проекта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="28aa9-116">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="28aa9-117">Версия</span><span class="sxs-lookup"><span data-stu-id="28aa9-117">Version</span></span> | <span data-ttu-id="28aa9-118">Версия пакета для синхронизации, установка значений по умолчанию для текущей установленной версии.</span><span class="sxs-lookup"><span data-stu-id="28aa9-118">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="28aa9-119">Исходный код</span><span class="sxs-lookup"><span data-stu-id="28aa9-119">Source</span></span> | <span data-ttu-id="28aa9-120">Путь URL-адрес или папку источника пакета для поиска.</span><span class="sxs-lookup"><span data-stu-id="28aa9-120">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="28aa9-121">Пути к локальной папке может быть абсолютным или относительным для текущей папки.</span><span class="sxs-lookup"><span data-stu-id="28aa9-121">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="28aa9-122">Если не указано, `Sync-Package` выполняет поиск в текущем выбранном источнике пакетов.</span><span class="sxs-lookup"><span data-stu-id="28aa9-122">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="28aa9-123">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="28aa9-123">IncludePrerelease</span></span> | <span data-ttu-id="28aa9-124">Включает предварительные версии пакетов в синхронизации.</span><span class="sxs-lookup"><span data-stu-id="28aa9-124">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="28aa9-125">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="28aa9-125">FileConflictAction</span></span> | <span data-ttu-id="28aa9-126">Действие, выполняемое при появлении запроса, чтобы игнорировать существующие файлы, связанные с проектом или перезаписать.</span><span class="sxs-lookup"><span data-stu-id="28aa9-126">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="28aa9-127">Возможными значениями являются *перезаписи, пропустить, None, OverwriteAll*, и *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="28aa9-127">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="28aa9-128">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="28aa9-128">DependencyVersion</span></span> | <span data-ttu-id="28aa9-129">Версия пакеты зависимостей для использования, которые может принимать одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="28aa9-129">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="28aa9-130">*Наименьший* (по умолчанию): самая ранняя версия</span><span class="sxs-lookup"><span data-stu-id="28aa9-130">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="28aa9-131">*HighestPatch*: версия с исправлением минимально основных минимально дополнительный: наибольшая</span><span class="sxs-lookup"><span data-stu-id="28aa9-131">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="28aa9-132">*HighestMinor*: версия с наименьшим основной, наивысший дополнительный номер: наибольшая исправления</span><span class="sxs-lookup"><span data-stu-id="28aa9-132">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="28aa9-133">*Наибольший* (по умолчанию для пакета обновления без параметров): самую новую версию</span><span class="sxs-lookup"><span data-stu-id="28aa9-133">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="28aa9-134">Можно задать значение по умолчанию с помощью [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) в `Nuget.Config` файла.</span><span class="sxs-lookup"><span data-stu-id="28aa9-134">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="28aa9-135">WhatIf</span><span class="sxs-lookup"><span data-stu-id="28aa9-135">WhatIf</span></span> | <span data-ttu-id="28aa9-136">Показывает, что произойдет при запуске команды без фактического выполнения синхронизации.</span><span class="sxs-lookup"><span data-stu-id="28aa9-136">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="28aa9-137">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="28aa9-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="28aa9-138">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="28aa9-138">Common Parameters</span></span>

<span data-ttu-id="28aa9-139">`Sync-Package`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="28aa9-139">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="28aa9-140">Примеры</span><span class="sxs-lookup"><span data-stu-id="28aa9-140">Examples</span></span>

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
