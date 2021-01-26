---
title: Справочник по Add-BindingRedirect PowerShell для NuGet
description: Справочник по Add-BindingRedirect команде PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 62edf1bf8995a4e1ffb83acc7a7621a786cc53e4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777615"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="e9b70-103">Add-BindingRedirect (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e9b70-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e9b70-104">*Доступно только в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="e9b70-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e9b70-105">Проверяет все сборки в пути вывода для проекта и добавляет перенаправления привязок в файл приложения или веб-конфигурации, где это необходимо.</span><span class="sxs-lookup"><span data-stu-id="e9b70-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="e9b70-106">Эта команда выполняется автоматически при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="e9b70-106">This command is run automatically when installing a package.</span></span>

> [!NOTE]
> <span data-ttu-id="e9b70-107">Это относится только к сценариям с использованием файла packages.config.</span><span class="sxs-lookup"><span data-stu-id="e9b70-107">This only applies to scenarios using a packages.config file.</span></span> <span data-ttu-id="e9b70-108">Дополнительные сведения см. в разделе [ссылка на файл NuGet packages.config](~/reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="e9b70-108">For more information, see [NuGet packages.config file reference](~/reference/packages-config.md).</span></span>

<span data-ttu-id="e9b70-109">Дополнительные сведения о перенаправлениях привязок и их использовании см. в статье [Перенаправление версий сборки](/dotnet/framework/configure-apps/redirect-assembly-versions) в документации по .NET.</span><span class="sxs-lookup"><span data-stu-id="e9b70-109">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="e9b70-110">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="e9b70-110">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="e9b70-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="e9b70-111">Parameters</span></span>

| <span data-ttu-id="e9b70-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="e9b70-112">Parameter</span></span> | <span data-ttu-id="e9b70-113">Описание</span><span class="sxs-lookup"><span data-stu-id="e9b70-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e9b70-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="e9b70-114">ProjectName</span></span> | <span data-ttu-id="e9b70-115">Необходимости Проект, к которому добавляются перенаправления привязок.</span><span class="sxs-lookup"><span data-stu-id="e9b70-115">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="e9b70-116">Параметр-ProjectName является необязательным.</span><span class="sxs-lookup"><span data-stu-id="e9b70-116">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="e9b70-117">Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="e9b70-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e9b70-118">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="e9b70-118">Common Parameters</span></span>

<span data-ttu-id="e9b70-119">`Add-BindingRedirect` поддерживает следующие [Общие параметры PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e9b70-119">`Add-BindingRedirect` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e9b70-120">Примеры</span><span class="sxs-lookup"><span data-stu-id="e9b70-120">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```