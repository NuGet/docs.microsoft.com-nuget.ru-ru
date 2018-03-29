---
title: Справочник по PowerShell для добавления BindingRedirect NuGet | Документы Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Справочник по PowerShell BindingRedirect добавить команду в консоли диспетчера пакетов NuGet в Visual Studio.
keywords: Пакет NuGet консоли диспетчера, команд NuGet Powershell, справочник по NuGet Powershell, добавить BindingRedirect
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 2a337bd61295f436b49c56c1680d07ccc6a8c403
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="f3567-104">Добавить BindingRedirect (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f3567-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f3567-105">*Доступен только в пределах [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="f3567-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f3567-106">Проверяет все сборки по пути вывода для проекта и добавляет перенаправления привязки в файле конфигурации приложения или веб-узла, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="f3567-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="f3567-107">Эта команда выполняется автоматически при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="f3567-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="f3567-108">Привязку перенаправления и почему они используются Подробнее [Перенаправление версий сборок](/dotnet/framework/configure-apps/redirect-assembly-versions) в документации по .NET.</span><span class="sxs-lookup"><span data-stu-id="f3567-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="f3567-109">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="f3567-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f3567-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="f3567-110">Parameters</span></span>

| <span data-ttu-id="f3567-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="f3567-111">Parameter</span></span> | <span data-ttu-id="f3567-112">Описание</span><span class="sxs-lookup"><span data-stu-id="f3567-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f3567-113">Название проекта</span><span class="sxs-lookup"><span data-stu-id="f3567-113">ProjectName</span></span> | <span data-ttu-id="f3567-114">(Обязательно) Проект, к которому необходимо добавить переадресации привязок.</span><span class="sxs-lookup"><span data-stu-id="f3567-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="f3567-115">Параметр - имя_проекта сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="f3567-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="f3567-116">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="f3567-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f3567-117">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="f3567-117">Common Parameters</span></span>

<span data-ttu-id="f3567-118">`Add-BindingRedirect` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f3567-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f3567-119">Примеры</span><span class="sxs-lookup"><span data-stu-id="f3567-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```