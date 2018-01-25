---
title: "Справочник по PowerShell для добавления BindingRedirect NuGet | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Справочник по PowerShell BindingRedirect добавить команду в консоли диспетчера пакетов NuGet в Visual Studio."
keywords: "Пакет NuGet консоли диспетчера, команд NuGet Powershell, справочник по NuGet Powershell, добавить BindingRedirect"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b755970402f29a72b9a10f1a94e4a799e9cb71cf
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="08a84-104">Добавить BindingRedirect (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="08a84-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="08a84-105">*Доступен только в пределах [консоль диспетчера пакетов NuGet](Package-Manager-Console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="08a84-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="08a84-106">Проверяет все сборки по пути вывода для проекта и добавляет перенаправления привязки в файле конфигурации приложения или веб-узла, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="08a84-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="08a84-107">Эта команда выполняется автоматически при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="08a84-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="08a84-108">Привязку перенаправления и почему они используются Подробнее [Перенаправление версий сборок](/dotnet/framework/configure-apps/redirect-assembly-versions) в документации по .NET.</span><span class="sxs-lookup"><span data-stu-id="08a84-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="08a84-109">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="08a84-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="08a84-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="08a84-110">Parameters</span></span>

| <span data-ttu-id="08a84-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="08a84-111">Parameter</span></span> | <span data-ttu-id="08a84-112">Описание:</span><span class="sxs-lookup"><span data-stu-id="08a84-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="08a84-113">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="08a84-113">ProjectName</span></span> | <span data-ttu-id="08a84-114">(Обязательно) Проект, к которому необходимо добавить переадресации привязок.</span><span class="sxs-lookup"><span data-stu-id="08a84-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="08a84-115">Параметр - имя_проекта сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="08a84-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="08a84-116">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="08a84-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="08a84-117">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="08a84-117">Common Parameters</span></span>

<span data-ttu-id="08a84-118">`Add-BindingRedirect`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="08a84-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="08a84-119">Примеры</span><span class="sxs-lookup"><span data-stu-id="08a84-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```