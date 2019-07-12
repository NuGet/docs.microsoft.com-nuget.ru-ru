---
title: Справочник по PowerShell NuGet открытым PackagePage
description: Справочник по PowerShell открытым PackagePage команду в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fd738f15b461051c4e9413b3035456c687979b97
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842269"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="28e64-103">Open-PackagePage (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="28e64-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="28e64-104">*Рекомендуется использовать в 3.0 +; доступен только в пределах [консоль диспетчера пакетов](package-manager-console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="28e64-104">*Deprecated in 3.0+; available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="28e64-105">Запускает браузер по умолчанию проекта, лицензий или URL-адрес отчета о нарушении для указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="28e64-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="28e64-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="28e64-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="28e64-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="28e64-107">Parameters</span></span>

| <span data-ttu-id="28e64-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="28e64-108">Parameter</span></span> | <span data-ttu-id="28e64-109">Описание</span><span class="sxs-lookup"><span data-stu-id="28e64-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="28e64-110">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="28e64-110">Id</span></span> | <span data-ttu-id="28e64-111">Идентификатор пакета нужного пакета.</span><span class="sxs-lookup"><span data-stu-id="28e64-111">The package ID of the desired package.</span></span> <span data-ttu-id="28e64-112">— Идентификатор сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="28e64-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="28e64-113">Версия</span><span class="sxs-lookup"><span data-stu-id="28e64-113">Version</span></span> | <span data-ttu-id="28e64-114">Версия пакета, по умолчанию до последней версии.</span><span class="sxs-lookup"><span data-stu-id="28e64-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="28e64-115">Source</span><span class="sxs-lookup"><span data-stu-id="28e64-115">Source</span></span> | <span data-ttu-id="28e64-116">Источник пакета по умолчанию используется источник, выбранный в раскрывающемся списке источнике.</span><span class="sxs-lookup"><span data-stu-id="28e64-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="28e64-117">Лицензия</span><span class="sxs-lookup"><span data-stu-id="28e64-117">License</span></span> | <span data-ttu-id="28e64-118">Открывает в браузере URL-адрес для лицензии пакета.</span><span class="sxs-lookup"><span data-stu-id="28e64-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="28e64-119">Если не указаны ни - лицензии, ни - ReportAbuse, в браузере откроется URL-адрес для пакета проекта.</span><span class="sxs-lookup"><span data-stu-id="28e64-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="28e64-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="28e64-120">ReportAbuse</span></span> | <span data-ttu-id="28e64-121">Открывает в браузере URL-адрес пакета отчетов о нарушении.</span><span class="sxs-lookup"><span data-stu-id="28e64-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="28e64-122">Если не указаны ни - лицензии, ни - ReportAbuse, в браузере откроется URL-адрес для пакета проекта.</span><span class="sxs-lookup"><span data-stu-id="28e64-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="28e64-123">Пропустить</span><span class="sxs-lookup"><span data-stu-id="28e64-123">PassThru</span></span> | <span data-ttu-id="28e64-124">Отображает URL-адрес; Используйте с помощью - WhatIf, чтобы открывать обозреватель.</span><span class="sxs-lookup"><span data-stu-id="28e64-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="28e64-125">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="28e64-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="28e64-126">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="28e64-126">Common Parameters</span></span>

<span data-ttu-id="28e64-127">`Open-PackagePage` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="28e64-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="28e64-128">Примеры</span><span class="sxs-lookup"><span data-stu-id="28e64-128">Examples</span></span>

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