---
title: Справочник по Add-BindingRedirect PowerShell для NuGet
description: Справочник по Add-BindingRedirect команде PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 382ba9b179428c70e3eb16db86a363e095207d61
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237261"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="31a8d-103">Add-BindingRedirect (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="31a8d-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="31a8d-104">*Доступно только в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="31a8d-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="31a8d-105">Проверяет все сборки в пути вывода для проекта и добавляет перенаправления привязок в файл приложения или веб-конфигурации, где это необходимо.</span><span class="sxs-lookup"><span data-stu-id="31a8d-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="31a8d-106">Эта команда выполняется автоматически при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="31a8d-106">This command is run automatically when installing a package.</span></span>

> [!NOTE]
> <span data-ttu-id="31a8d-107">Это относится только к сценариям с использованием файла packages.config.</span><span class="sxs-lookup"><span data-stu-id="31a8d-107">This only applies to scenarios using a packages.config file.</span></span> <span data-ttu-id="31a8d-108">Дополнительные сведения см. в разделе [ссылка на файл NuGet packages.config](~/reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="31a8d-108">For more information, see [NuGet packages.config file reference](~/reference/packages-config.md).</span></span>

<span data-ttu-id="31a8d-109">Дополнительные сведения о перенаправлениях привязок и их использовании см. в статье [Перенаправление версий сборки](/dotnet/framework/configure-apps/redirect-assembly-versions) в документации по .NET.</span><span class="sxs-lookup"><span data-stu-id="31a8d-109">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="31a8d-110">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="31a8d-110">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="31a8d-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="31a8d-111">Parameters</span></span>

| <span data-ttu-id="31a8d-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="31a8d-112">Parameter</span></span> | <span data-ttu-id="31a8d-113">Описание</span><span class="sxs-lookup"><span data-stu-id="31a8d-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="31a8d-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="31a8d-114">ProjectName</span></span> | <span data-ttu-id="31a8d-115">Необходимости Проект, к которому добавляются перенаправления привязок.</span><span class="sxs-lookup"><span data-stu-id="31a8d-115">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="31a8d-116">Параметр-ProjectName является необязательным.</span><span class="sxs-lookup"><span data-stu-id="31a8d-116">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="31a8d-117">Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="31a8d-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="31a8d-118">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="31a8d-118">Common Parameters</span></span>

<span data-ttu-id="31a8d-119">`Add-BindingRedirect` поддерживает следующие [Общие параметры PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="31a8d-119">`Add-BindingRedirect` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="31a8d-120">Примеры</span><span class="sxs-lookup"><span data-stu-id="31a8d-120">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```