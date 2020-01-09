---
title: Удаление NuGet — Справочник по PowerShell для пакета
description: Ссылка на команду uninstall-package PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 05b7bf0e8abad0904b9e851ea6b7a5317e74229d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384419"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="e6778-103">Uninstall-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e6778-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e6778-104">*В этом разделе описывается команда в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows. Сведения об универсальной команде PowerShell uninstall-package см. в справочнике по модульу [PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="e6778-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="e6778-105">Удаляет пакет из проекта, при необходимости удаляя его зависимости.</span><span class="sxs-lookup"><span data-stu-id="e6778-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="e6778-106">Если от этого пакета зависят другие пакеты, команда не будет выполнена, если только для нее не был указан параметр –Force.</span><span class="sxs-lookup"><span data-stu-id="e6778-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="e6778-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="e6778-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="e6778-108">Если от этого пакета зависят другие пакеты, команда не будет выполнена, если только для нее не был указан параметр –Force.</span><span class="sxs-lookup"><span data-stu-id="e6778-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="e6778-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="e6778-109">Parameters</span></span>

| <span data-ttu-id="e6778-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="e6778-110">Parameter</span></span> | <span data-ttu-id="e6778-111">Описание</span><span class="sxs-lookup"><span data-stu-id="e6778-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e6778-112">Id</span><span class="sxs-lookup"><span data-stu-id="e6778-112">Id</span></span> | <span data-ttu-id="e6778-113">Необходимости Идентификатор пакета для удаления.</span><span class="sxs-lookup"><span data-stu-id="e6778-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="e6778-114">Сам переключатель-ID является необязательным.</span><span class="sxs-lookup"><span data-stu-id="e6778-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="e6778-115">{2&gt;Version&lt;2}</span><span class="sxs-lookup"><span data-stu-id="e6778-115">Version</span></span> | <span data-ttu-id="e6778-116">Версия пакета для удаления, используемая по умолчанию для текущей установленной версии.</span><span class="sxs-lookup"><span data-stu-id="e6778-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="e6778-117">ремоведепенденЦиес</span><span class="sxs-lookup"><span data-stu-id="e6778-117">RemoveDependencies</span></span> | <span data-ttu-id="e6778-118">Удалите пакет и его неиспользуемые зависимости.</span><span class="sxs-lookup"><span data-stu-id="e6778-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="e6778-119">То есть, если какая-либо зависимость имеет другой зависимый от нее пакет, он пропускается.</span><span class="sxs-lookup"><span data-stu-id="e6778-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="e6778-120">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="e6778-120">ProjectName</span></span> | <span data-ttu-id="e6778-121">Проект, из которого удаляется пакет, по умолчанию используется проект по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e6778-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="e6778-122">Force</span><span class="sxs-lookup"><span data-stu-id="e6778-122">Force</span></span> | <span data-ttu-id="e6778-123">Принудительно удаляет пакет, даже если от него зависят другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="e6778-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="e6778-124">Whatif</span><span class="sxs-lookup"><span data-stu-id="e6778-124">WhatIf</span></span> | <span data-ttu-id="e6778-125">Показывает, что произойдет при выполнении команды без фактического выполнения удаления.</span><span class="sxs-lookup"><span data-stu-id="e6778-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="e6778-126">Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="e6778-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e6778-127">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="e6778-127">Common Parameters</span></span>

<span data-ttu-id="e6778-128">`Uninstall-Package` поддерживает следующие [Общие параметры PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e6778-128">`Uninstall-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e6778-129">Примеры</span><span class="sxs-lookup"><span data-stu-id="e6778-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
