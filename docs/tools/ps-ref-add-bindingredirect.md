---
title: Справочник по PowerShell для добавления BindingRedirect NuGet
description: Справочник по PowerShell BindingRedirect добавить команду в консоли диспетчера пакетов NuGet в Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7f1f2ef23e54ee48b577a2796b7f7b5f4c7eb284
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="7c10f-103">Add-BindingRedirect (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="7c10f-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7c10f-104">*Доступен только в пределах [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="7c10f-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="7c10f-105">Проверяет все сборки по пути вывода для проекта и добавляет перенаправления привязки в файле конфигурации приложения или веб-узла, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="7c10f-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="7c10f-106">Эта команда выполняется автоматически при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="7c10f-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="7c10f-107">Привязку перенаправления и почему они используются Подробнее [Перенаправление версий сборок](/dotnet/framework/configure-apps/redirect-assembly-versions) в документации по .NET.</span><span class="sxs-lookup"><span data-stu-id="7c10f-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="7c10f-108">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="7c10f-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="7c10f-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="7c10f-109">Parameters</span></span>

| <span data-ttu-id="7c10f-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="7c10f-110">Parameter</span></span> | <span data-ttu-id="7c10f-111">Описание</span><span class="sxs-lookup"><span data-stu-id="7c10f-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7c10f-112">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="7c10f-112">ProjectName</span></span> | <span data-ttu-id="7c10f-113">(Обязательно) Проект, к которому необходимо добавить переадресации привязок.</span><span class="sxs-lookup"><span data-stu-id="7c10f-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="7c10f-114">Параметр - имя_проекта сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="7c10f-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="7c10f-115">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="7c10f-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7c10f-116">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="7c10f-116">Common Parameters</span></span>

<span data-ttu-id="7c10f-117">`Add-BindingRedirect` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="7c10f-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7c10f-118">Примеры</span><span class="sxs-lookup"><span data-stu-id="7c10f-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```