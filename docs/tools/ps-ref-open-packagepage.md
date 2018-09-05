---
title: Справочник по PowerShell NuGet открытым PackagePage
description: Справочник по PowerShell открытым PackagePage команду в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0325aa4ddd718a901dd6a09cdf86cae260e326ab
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547172"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="3dea9-103">Open-PackagePage (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3dea9-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3dea9-104">*Рекомендуется использовать в 3.0 +; доступен только в пределах [консоли диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="3dea9-104">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="3dea9-105">Запускает браузер по умолчанию проекта, лицензий или URL-адрес отчета о нарушении для указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="3dea9-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="3dea9-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="3dea9-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="3dea9-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="3dea9-107">Parameters</span></span>

| <span data-ttu-id="3dea9-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="3dea9-108">Parameter</span></span> | <span data-ttu-id="3dea9-109">Описание</span><span class="sxs-lookup"><span data-stu-id="3dea9-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3dea9-110">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="3dea9-110">Id</span></span> | <span data-ttu-id="3dea9-111">Идентификатор пакета нужного пакета.</span><span class="sxs-lookup"><span data-stu-id="3dea9-111">The package ID of the desired package.</span></span> <span data-ttu-id="3dea9-112">— Идентификатор сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="3dea9-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="3dea9-113">Версия</span><span class="sxs-lookup"><span data-stu-id="3dea9-113">Version</span></span> | <span data-ttu-id="3dea9-114">Версия пакета, по умолчанию до последней версии.</span><span class="sxs-lookup"><span data-stu-id="3dea9-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="3dea9-115">Исходный код</span><span class="sxs-lookup"><span data-stu-id="3dea9-115">Source</span></span> | <span data-ttu-id="3dea9-116">Источник пакета по умолчанию используется источник, выбранный в раскрывающемся списке источнике.</span><span class="sxs-lookup"><span data-stu-id="3dea9-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="3dea9-117">Лицензия</span><span class="sxs-lookup"><span data-stu-id="3dea9-117">License</span></span> | <span data-ttu-id="3dea9-118">Открывает в браузере URL-адрес для лицензии пакета.</span><span class="sxs-lookup"><span data-stu-id="3dea9-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="3dea9-119">Если не указаны ни - лицензии, ни - ReportAbuse, в браузере откроется URL-адрес для пакета проекта.</span><span class="sxs-lookup"><span data-stu-id="3dea9-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="3dea9-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="3dea9-120">ReportAbuse</span></span> | <span data-ttu-id="3dea9-121">Открывает в браузере URL-адрес пакета отчетов о нарушении.</span><span class="sxs-lookup"><span data-stu-id="3dea9-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="3dea9-122">Если не указаны ни - лицензии, ни - ReportAbuse, в браузере откроется URL-адрес для пакета проекта.</span><span class="sxs-lookup"><span data-stu-id="3dea9-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="3dea9-123">Пропустить</span><span class="sxs-lookup"><span data-stu-id="3dea9-123">PassThru</span></span> | <span data-ttu-id="3dea9-124">Отображает URL-адрес; Используйте с помощью - WhatIf, чтобы открывать обозреватель.</span><span class="sxs-lookup"><span data-stu-id="3dea9-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="3dea9-125">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="3dea9-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3dea9-126">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="3dea9-126">Common Parameters</span></span>

<span data-ttu-id="3dea9-127">`Open-PackagePage` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладки, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3dea9-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3dea9-128">Примеры</span><span class="sxs-lookup"><span data-stu-id="3dea9-128">Examples</span></span>

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```