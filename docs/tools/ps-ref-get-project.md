---
title: Справочник по PowerShell Get проектами NuGet
description: Справочник по GetProject PowerShell команду в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 849261711fafcadbab38bf6fe99340c4b79e1e21
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550441"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="c7748-103">Get-Project (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="c7748-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="c7748-104">*Доступен только в пределах [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="c7748-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="c7748-105">Отображает сведения о по умолчанию или указанный проект.</span><span class="sxs-lookup"><span data-stu-id="c7748-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="c7748-106">`Get-Project` в частности возвращается референта объекта Visual Studio DTE (среду средств разработки) для проекта.</span><span class="sxs-lookup"><span data-stu-id="c7748-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="c7748-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="c7748-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="c7748-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="c7748-108">Parameters</span></span>

| <span data-ttu-id="c7748-109">Параметр</span><span class="sxs-lookup"><span data-stu-id="c7748-109">Parameter</span></span> | <span data-ttu-id="c7748-110">Описание</span><span class="sxs-lookup"><span data-stu-id="c7748-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c7748-111">name</span><span class="sxs-lookup"><span data-stu-id="c7748-111">Name</span></span> | <span data-ttu-id="c7748-112">Указывает проект для отображения, по умолчанию принимается значение по умолчанию проекта, выбранного в консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="c7748-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="c7748-113">-Имя коммутатора является необязательным.</span><span class="sxs-lookup"><span data-stu-id="c7748-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="c7748-114">Все</span><span class="sxs-lookup"><span data-stu-id="c7748-114">All</span></span> | <span data-ttu-id="c7748-115">Отображает сведения для каждого проекта в решении; порядок проектов не является детерминированным.</span><span class="sxs-lookup"><span data-stu-id="c7748-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="c7748-116">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="c7748-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="c7748-117">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="c7748-117">Common Parameters</span></span>

<span data-ttu-id="c7748-118">`Get-Project` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладки, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c7748-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="c7748-119">Примеры</span><span class="sxs-lookup"><span data-stu-id="c7748-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```