---
title: Справочник по PowerShell Get-Project для NuGet
description: Справочник по команде "копроект PowerShell" в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 3343952535c2d3c822f5cac24cb30c8f5bfa5be3
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384624"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="4d42a-103">Get-Project (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4d42a-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4d42a-104">*Доступно только в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="4d42a-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="4d42a-105">Отображает сведения об указанном по умолчанию или проекте.</span><span class="sxs-lookup"><span data-stu-id="4d42a-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="4d42a-106">`Get-Project` специально возвращает объект референт в Visual Studio DTE (среда средств разработки) для проекта.</span><span class="sxs-lookup"><span data-stu-id="4d42a-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="4d42a-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="4d42a-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="4d42a-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="4d42a-108">Parameters</span></span>

| <span data-ttu-id="4d42a-109">Параметр</span><span class="sxs-lookup"><span data-stu-id="4d42a-109">Parameter</span></span> | <span data-ttu-id="4d42a-110">Описание</span><span class="sxs-lookup"><span data-stu-id="4d42a-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4d42a-111">Name</span><span class="sxs-lookup"><span data-stu-id="4d42a-111">Name</span></span> | <span data-ttu-id="4d42a-112">Указывает отображаемый проект, по умолчанию выбран проект по умолчанию, выбранный в консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="4d42a-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="4d42a-113">Параметр-Name сам по себе не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="4d42a-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="4d42a-114">Все .</span><span class="sxs-lookup"><span data-stu-id="4d42a-114">All</span></span> | <span data-ttu-id="4d42a-115">Отображает сведения для каждого проекта в решении; порядок проектов не является детерминированным.</span><span class="sxs-lookup"><span data-stu-id="4d42a-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="4d42a-116">Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="4d42a-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4d42a-117">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="4d42a-117">Common Parameters</span></span>

<span data-ttu-id="4d42a-118">`Get-Project` поддерживает следующие [Общие параметры PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="4d42a-118">`Get-Project` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4d42a-119">Примеры</span><span class="sxs-lookup"><span data-stu-id="4d42a-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```