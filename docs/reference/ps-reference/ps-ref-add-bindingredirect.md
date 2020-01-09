---
title: Справочник по PowerShell Add-BindingRedirect для NuGet
description: Справочник по команде PowerShell Add-BindingRedirect в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d3d156cf882229260e8cf55f8ece2804aec36dc9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384988"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="1c7e1-103">Add-BindingRedirect (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="1c7e1-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="1c7e1-104">*Доступно только в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="1c7e1-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="1c7e1-105">Проверяет все сборки в пути вывода для проекта и добавляет перенаправления привязок в файл приложения или веб-конфигурации, где это необходимо.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="1c7e1-106">Эта команда выполняется автоматически при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="1c7e1-107">Дополнительные сведения о перенаправлениях привязок и их использовании см. в статье [Перенаправление версий сборки](/dotnet/framework/configure-apps/redirect-assembly-versions) в документации по .NET.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="1c7e1-108">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="1c7e1-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="1c7e1-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="1c7e1-109">Parameters</span></span>

| <span data-ttu-id="1c7e1-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="1c7e1-110">Parameter</span></span> | <span data-ttu-id="1c7e1-111">Описание</span><span class="sxs-lookup"><span data-stu-id="1c7e1-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1c7e1-112">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="1c7e1-112">ProjectName</span></span> | <span data-ttu-id="1c7e1-113">Необходимости Проект, к которому добавляются перенаправления привязок.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="1c7e1-114">Параметр-ProjectName является необязательным.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="1c7e1-115">Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="1c7e1-116">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="1c7e1-116">Common Parameters</span></span>

<span data-ttu-id="1c7e1-117">`Add-BindingRedirect` поддерживает следующие [Общие параметры PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="1c7e1-118">Примеры</span><span class="sxs-lookup"><span data-stu-id="1c7e1-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```