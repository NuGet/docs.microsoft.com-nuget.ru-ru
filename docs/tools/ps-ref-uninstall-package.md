---
title: Справочник по PowerShell для удаления пакета NuGet
description: Ссылка для команды PowerShell Uninstall-Package в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: c95479103be2cba3b4eb6964ea761870477863bd
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842474"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f42c0-103">Uninstall-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f42c0-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f42c0-104">*В этом разделе описываются команды в [консоль диспетчера пакетов](package-manager-console.md) в Visual Studio в Windows. Общая команда удалением пакета PowerShell, см. в разделе [Справочник по PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="f42c0-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="f42c0-105">Удаляет пакет из проекта, при необходимости удаления его зависимости.</span><span class="sxs-lookup"><span data-stu-id="f42c0-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="f42c0-106">Если этого пакета зависят другие пакеты, команда завершится ошибкой, если не – Force задан параметр.</span><span class="sxs-lookup"><span data-stu-id="f42c0-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="f42c0-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="f42c0-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="f42c0-108">Если этого пакета зависят другие пакеты, команда завершится ошибкой, если не – Force задан параметр.</span><span class="sxs-lookup"><span data-stu-id="f42c0-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="f42c0-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="f42c0-109">Parameters</span></span>

| <span data-ttu-id="f42c0-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="f42c0-110">Parameter</span></span> | <span data-ttu-id="f42c0-111">Описание</span><span class="sxs-lookup"><span data-stu-id="f42c0-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f42c0-112">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="f42c0-112">Id</span></span> | <span data-ttu-id="f42c0-113">(Обязательно) Идентификатор пакета для удаления.</span><span class="sxs-lookup"><span data-stu-id="f42c0-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="f42c0-114">— Идентификатор сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="f42c0-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="f42c0-115">Версия</span><span class="sxs-lookup"><span data-stu-id="f42c0-115">Version</span></span> | <span data-ttu-id="f42c0-116">Версия пакета для удаления, установка значений по умолчанию для текущей установленной версии.</span><span class="sxs-lookup"><span data-stu-id="f42c0-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="f42c0-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="f42c0-117">RemoveDependencies</span></span> | <span data-ttu-id="f42c0-118">Удалите пакет и его неиспользуемые зависимости.</span><span class="sxs-lookup"><span data-stu-id="f42c0-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="f42c0-119">То есть если зависят от него зависит другой пакет, он пропускается.</span><span class="sxs-lookup"><span data-stu-id="f42c0-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="f42c0-120">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="f42c0-120">ProjectName</span></span> | <span data-ttu-id="f42c0-121">Проект, из которого необходимо удалить пакет, по умолчанию используется тип проекта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f42c0-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="f42c0-122">Force</span><span class="sxs-lookup"><span data-stu-id="f42c0-122">Force</span></span> | <span data-ttu-id="f42c0-123">Заставляет пакета, который требуется удалить, даже если он зависят другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="f42c0-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="f42c0-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="f42c0-124">WhatIf</span></span> | <span data-ttu-id="f42c0-125">Показывает, что произойдет при выполнении команды без фактического выполнения удаления.</span><span class="sxs-lookup"><span data-stu-id="f42c0-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="f42c0-126">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="f42c0-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f42c0-127">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="f42c0-127">Common Parameters</span></span>

<span data-ttu-id="f42c0-128">`Uninstall-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f42c0-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f42c0-129">Примеры</span><span class="sxs-lookup"><span data-stu-id="f42c0-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
