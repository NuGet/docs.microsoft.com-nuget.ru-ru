---
title: Справочник по PowerShell для удаления пакета NuGet
description: Ссылка для команды PowerShell Uninstall-Package в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ae60473fbb716b23f40b0605be8aaa8515802315
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551647"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="ab694-103">Uninstall-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="ab694-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ab694-104">*В этом разделе описываются команды в [консоли диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows. Общая команда удалением пакета PowerShell, см. в разделе [Справочник по PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="ab694-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="ab694-105">Удаляет пакет из проекта, при необходимости удаления его зависимости.</span><span class="sxs-lookup"><span data-stu-id="ab694-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="ab694-106">Если этого пакета зависят другие пакеты, команда завершится ошибкой, если не – Force задан параметр.</span><span class="sxs-lookup"><span data-stu-id="ab694-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="ab694-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="ab694-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="ab694-108">Если этого пакета зависят другие пакеты, команда завершится ошибкой, если не – Force задан параметр.</span><span class="sxs-lookup"><span data-stu-id="ab694-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="ab694-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="ab694-109">Parameters</span></span>

| <span data-ttu-id="ab694-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="ab694-110">Parameter</span></span> | <span data-ttu-id="ab694-111">Описание</span><span class="sxs-lookup"><span data-stu-id="ab694-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ab694-112">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="ab694-112">Id</span></span> | <span data-ttu-id="ab694-113">(Обязательно) Идентификатор пакета для удаления.</span><span class="sxs-lookup"><span data-stu-id="ab694-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="ab694-114">— Идентификатор сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="ab694-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="ab694-115">Версия</span><span class="sxs-lookup"><span data-stu-id="ab694-115">Version</span></span> | <span data-ttu-id="ab694-116">Версия пакета для удаления, установка значений по умолчанию для текущей установленной версии.</span><span class="sxs-lookup"><span data-stu-id="ab694-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="ab694-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="ab694-117">RemoveDependencies</span></span> | <span data-ttu-id="ab694-118">Удалите пакет и его неиспользуемые зависимости.</span><span class="sxs-lookup"><span data-stu-id="ab694-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="ab694-119">То есть если зависят от него зависит другой пакет, он пропускается.</span><span class="sxs-lookup"><span data-stu-id="ab694-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="ab694-120">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="ab694-120">ProjectName</span></span> | <span data-ttu-id="ab694-121">Проект, из которого необходимо удалить пакет, по умолчанию используется тип проекта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ab694-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="ab694-122">Force</span><span class="sxs-lookup"><span data-stu-id="ab694-122">Force</span></span> | <span data-ttu-id="ab694-123">Заставляет пакета, который требуется удалить, даже если он зависят другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="ab694-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="ab694-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="ab694-124">WhatIf</span></span> | <span data-ttu-id="ab694-125">Показывает, что произойдет при выполнении команды без фактического выполнения удаления.</span><span class="sxs-lookup"><span data-stu-id="ab694-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="ab694-126">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="ab694-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ab694-127">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="ab694-127">Common Parameters</span></span>

<span data-ttu-id="ab694-128">`Uninstall-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладки, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="ab694-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ab694-129">Примеры</span><span class="sxs-lookup"><span data-stu-id="ab694-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
