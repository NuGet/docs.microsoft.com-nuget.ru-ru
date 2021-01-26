---
title: Справочник по Uninstall-Package PowerShell для NuGet
description: Справочник по Uninstall-Package команде PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 961a9d68e5cba09030401fc871a93bf1145b23a3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777387"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="09108-103">Uninstall-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="09108-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="09108-104">*В этом разделе описывается команда в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows. Общие команды PowerShell Uninstall-Package см. в [справочнике по PackageManagement для PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="09108-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="09108-105">Удаляет пакет из проекта, при необходимости удаляя его зависимости.</span><span class="sxs-lookup"><span data-stu-id="09108-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="09108-106">Если от этого пакета зависят другие пакеты, команда не будет выполнена, если только для нее не был указан параметр –Force.</span><span class="sxs-lookup"><span data-stu-id="09108-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="09108-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="09108-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="09108-108">Если от этого пакета зависят другие пакеты, команда не будет выполнена, если только для нее не был указан параметр –Force.</span><span class="sxs-lookup"><span data-stu-id="09108-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="09108-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="09108-109">Parameters</span></span>

| <span data-ttu-id="09108-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="09108-110">Parameter</span></span> | <span data-ttu-id="09108-111">Описание</span><span class="sxs-lookup"><span data-stu-id="09108-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="09108-112">Id</span><span class="sxs-lookup"><span data-stu-id="09108-112">Id</span></span> | <span data-ttu-id="09108-113">Необходимости Идентификатор пакета для удаления.</span><span class="sxs-lookup"><span data-stu-id="09108-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="09108-114">Сам переключатель-ID является необязательным.</span><span class="sxs-lookup"><span data-stu-id="09108-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="09108-115">Версия</span><span class="sxs-lookup"><span data-stu-id="09108-115">Version</span></span> | <span data-ttu-id="09108-116">Версия пакета для удаления, используемая по умолчанию для текущей установленной версии.</span><span class="sxs-lookup"><span data-stu-id="09108-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="09108-117">ремоведепенденЦиес</span><span class="sxs-lookup"><span data-stu-id="09108-117">RemoveDependencies</span></span> | <span data-ttu-id="09108-118">Удалите пакет и его неиспользуемые зависимости.</span><span class="sxs-lookup"><span data-stu-id="09108-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="09108-119">То есть, если какая-либо зависимость имеет другой зависимый от нее пакет, он пропускается.</span><span class="sxs-lookup"><span data-stu-id="09108-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="09108-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="09108-120">ProjectName</span></span> | <span data-ttu-id="09108-121">Проект, из которого удаляется пакет, по умолчанию используется проект по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="09108-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="09108-122">Force</span><span class="sxs-lookup"><span data-stu-id="09108-122">Force</span></span> | <span data-ttu-id="09108-123">Принудительно удаляет пакет, даже если от него зависят другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="09108-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="09108-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="09108-124">WhatIf</span></span> | <span data-ttu-id="09108-125">Показывает, что произойдет при выполнении команды без фактического выполнения удаления.</span><span class="sxs-lookup"><span data-stu-id="09108-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="09108-126">Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="09108-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="09108-127">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="09108-127">Common Parameters</span></span>

<span data-ttu-id="09108-128">`Uninstall-Package` поддерживает следующие [Общие параметры PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="09108-128">`Uninstall-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="09108-129">Примеры</span><span class="sxs-lookup"><span data-stu-id="09108-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```