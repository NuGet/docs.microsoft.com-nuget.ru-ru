---
title: "Справочник по PowerShell удалить пакет NuGet | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: f4f5dc79-8e8e-4012-8986-873a5d9283d9
description: "Ссылка для команды PowerShell удалением пакета в консоли диспетчера пакетов NuGet в Visual Studio."
keywords: "Пакет NuGet консоли диспетчера, команд NuGet Powershell, справочник по NuGet Powershell, удалением пакета"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0899198a354a56615a48a1f7f428674a205f386b
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="82c73-104">Uninstall-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="82c73-104">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="82c73-105">*В этом разделе описываются команды в [консоль диспетчера пакетов NuGet](Package-Manager-Console.md) в Visual Studio в Windows. Общая команда PowerShell Uninstall-Package. в разделе [PowerShell PackageManagement ссылка](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="82c73-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="82c73-106">Удаляет пакет из проекта, при необходимости удаления его зависимости.</span><span class="sxs-lookup"><span data-stu-id="82c73-106">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="82c73-107">Если для данного пакета зависят другие пакеты, команда будет выполнена, если указан параметр-Force.</span><span class="sxs-lookup"><span data-stu-id="82c73-107">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="82c73-108">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="82c73-108">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="82c73-109">Если для данного пакета зависят другие пакеты, команда будет выполнена, если указан параметр-Force.</span><span class="sxs-lookup"><span data-stu-id="82c73-109">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="82c73-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="82c73-110">Parameters</span></span>

| <span data-ttu-id="82c73-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="82c73-111">Parameter</span></span> | <span data-ttu-id="82c73-112">Описание:</span><span class="sxs-lookup"><span data-stu-id="82c73-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="82c73-113">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="82c73-113">Id</span></span> | <span data-ttu-id="82c73-114">(Обязательно) Идентификатор пакета для удаления.</span><span class="sxs-lookup"><span data-stu-id="82c73-114">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="82c73-115">— Идентификатор коммутатора сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="82c73-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="82c73-116">Версия</span><span class="sxs-lookup"><span data-stu-id="82c73-116">Version</span></span> | <span data-ttu-id="82c73-117">Версия пакета для удаления, установка значений по умолчанию для текущей установленной версии.</span><span class="sxs-lookup"><span data-stu-id="82c73-117">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="82c73-118">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="82c73-118">RemoveDependencies</span></span> | <span data-ttu-id="82c73-119">Удалите пакет и его неиспользуемые зависимости.</span><span class="sxs-lookup"><span data-stu-id="82c73-119">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="82c73-120">То есть если какой-либо зависимостью связан другой пакет зависит от него, он пропускается.</span><span class="sxs-lookup"><span data-stu-id="82c73-120">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="82c73-121">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="82c73-121">ProjectName</span></span> | <span data-ttu-id="82c73-122">Проект, из которого необходимо удалить пакет, установка значений по умолчанию для проекта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="82c73-122">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="82c73-123">Force</span><span class="sxs-lookup"><span data-stu-id="82c73-123">Force</span></span> | <span data-ttu-id="82c73-124">Принудительное пакета будет удалена, даже если он зависят другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="82c73-124">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="82c73-125">WhatIf</span><span class="sxs-lookup"><span data-stu-id="82c73-125">WhatIf</span></span> | <span data-ttu-id="82c73-126">Показывает, что произойдет при запуске команды без фактического выполнения удаления.</span><span class="sxs-lookup"><span data-stu-id="82c73-126">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="82c73-127">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="82c73-127">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="82c73-128">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="82c73-128">Common Parameters</span></span>

<span data-ttu-id="82c73-129">`Uninstall-Package`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="82c73-129">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="82c73-130">Примеры</span><span class="sxs-lookup"><span data-stu-id="82c73-130">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
