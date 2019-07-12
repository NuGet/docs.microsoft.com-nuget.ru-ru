---
title: Справочник по PowerShell добавьте BindingRedirect NuGet
description: Ссылка для команды PowerShell Add-BindingRedirect в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5f318ddfb2bb8498ab3e608f8036be05dcb0706
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842543"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="71a6b-103">Add-BindingRedirect (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="71a6b-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="71a6b-104">*Доступен только в пределах [консоль диспетчера пакетов](package-manager-console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="71a6b-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="71a6b-105">Проверяет все сборки по пути вывода проекта и добавляет переадресацию привязок в файле конфигурации приложения или веб-там, где необходимо.</span><span class="sxs-lookup"><span data-stu-id="71a6b-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="71a6b-106">Эта команда выполняется автоматически при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="71a6b-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="71a6b-107">Дополнительные сведения о привязке перенаправления и почему они используются, см. в разделе [Перенаправление версий сборок](/dotnet/framework/configure-apps/redirect-assembly-versions) в документации по .NET.</span><span class="sxs-lookup"><span data-stu-id="71a6b-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="71a6b-108">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="71a6b-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="71a6b-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="71a6b-109">Parameters</span></span>

| <span data-ttu-id="71a6b-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="71a6b-110">Parameter</span></span> | <span data-ttu-id="71a6b-111">Описание</span><span class="sxs-lookup"><span data-stu-id="71a6b-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="71a6b-112">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="71a6b-112">ProjectName</span></span> | <span data-ttu-id="71a6b-113">(Обязательно) Проект, к которому необходимо добавить переадресации привязок.</span><span class="sxs-lookup"><span data-stu-id="71a6b-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="71a6b-114">Параметр - имя_проекта сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="71a6b-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="71a6b-115">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="71a6b-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="71a6b-116">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="71a6b-116">Common Parameters</span></span>

<span data-ttu-id="71a6b-117">`Add-BindingRedirect` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="71a6b-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="71a6b-118">Примеры</span><span class="sxs-lookup"><span data-stu-id="71a6b-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```