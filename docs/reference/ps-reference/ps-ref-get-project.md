---
title: Справочник по Get-Project PowerShell для NuGet
description: Справочник по команде "копроект PowerShell" в консоли диспетчера пакетов NuGet в Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 16b3ffc0a375b8027c615020243a7289520715f8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777476"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="de7b4-103">Get-Project (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="de7b4-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="de7b4-104">*Доступно только в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="de7b4-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="de7b4-105">Отображает сведения об указанном по умолчанию или проекте.</span><span class="sxs-lookup"><span data-stu-id="de7b4-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="de7b4-106">`Get-Project` в частности, функция возвращает референт в объект Visual Studio DTE (среда средств разработки) для проекта.</span><span class="sxs-lookup"><span data-stu-id="de7b4-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="de7b4-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="de7b4-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="de7b4-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="de7b4-108">Parameters</span></span>

| <span data-ttu-id="de7b4-109">Параметр</span><span class="sxs-lookup"><span data-stu-id="de7b4-109">Parameter</span></span> | <span data-ttu-id="de7b4-110">Описание</span><span class="sxs-lookup"><span data-stu-id="de7b4-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de7b4-111">Имя</span><span class="sxs-lookup"><span data-stu-id="de7b4-111">Name</span></span> | <span data-ttu-id="de7b4-112">Указывает отображаемый проект, по умолчанию выбран проект по умолчанию, выбранный в консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="de7b4-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="de7b4-113">Параметр-Name сам по себе не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="de7b4-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="de7b4-114">Все</span><span class="sxs-lookup"><span data-stu-id="de7b4-114">All</span></span> | <span data-ttu-id="de7b4-115">Отображает сведения для каждого проекта в решении; порядок проектов не является детерминированным.</span><span class="sxs-lookup"><span data-stu-id="de7b4-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="de7b4-116">Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="de7b4-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="de7b4-117">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="de7b4-117">Common Parameters</span></span>

<span data-ttu-id="de7b4-118">`Get-Project` поддерживает следующие [Общие параметры PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="de7b4-118">`Get-Project` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="de7b4-119">Примеры</span><span class="sxs-lookup"><span data-stu-id="de7b4-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```