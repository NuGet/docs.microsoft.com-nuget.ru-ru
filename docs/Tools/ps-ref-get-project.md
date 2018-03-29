---
title: Справочник по PowerShell NuGet Get проект | Документы Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Ссылка для команды GetProject PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
keywords: Пакет NuGet консоли диспетчера, команд NuGet Powershell, справочник по NuGet Powershell, Get-проект
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9fcdcf7c550408cd7dfd73787ee14821c46a1df9
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="a234c-104">Get проект (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="a234c-104">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a234c-105">*Доступен только в пределах [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="a234c-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="a234c-106">Отображает сведения о значения по умолчанию или указанный проект.</span><span class="sxs-lookup"><span data-stu-id="a234c-106">Displays information about the default or specified project.</span></span> <span data-ttu-id="a234c-107">`Get-Project` специально возвращает объект ссылки на объект Visual Studio DTE (среду средств разработки) для проекта.</span><span class="sxs-lookup"><span data-stu-id="a234c-107">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="a234c-108">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="a234c-108">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a234c-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="a234c-109">Parameters</span></span>

| <span data-ttu-id="a234c-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="a234c-110">Parameter</span></span> | <span data-ttu-id="a234c-111">Описание</span><span class="sxs-lookup"><span data-stu-id="a234c-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a234c-112">Имя</span><span class="sxs-lookup"><span data-stu-id="a234c-112">Name</span></span> | <span data-ttu-id="a234c-113">Указывает проект для отображения, по умолчанию принимается по умолчанию проекта, выбранного в консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="a234c-113">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="a234c-114">-Имя коммутатора является необязательным.</span><span class="sxs-lookup"><span data-stu-id="a234c-114">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="a234c-115">Все</span><span class="sxs-lookup"><span data-stu-id="a234c-115">All</span></span> | <span data-ttu-id="a234c-116">Отображает сведения для каждого проекта в решении; порядок проектов не является детерминированным.</span><span class="sxs-lookup"><span data-stu-id="a234c-116">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="a234c-117">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="a234c-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a234c-118">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="a234c-118">Common Parameters</span></span>

<span data-ttu-id="a234c-119">`Get-Project` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="a234c-119">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a234c-120">Примеры</span><span class="sxs-lookup"><span data-stu-id="a234c-120">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```