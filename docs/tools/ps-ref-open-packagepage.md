---
title: Справочник по PowerShell NuGet Open-PackagePage
description: Ссылка для команды PowerShell PackagePage откройте консоль диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e64a83c01a7baac330c99fe40ba52f328a2133b8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817724"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="f8af4-103">Open-PackagePage (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f8af4-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f8af4-104">*Рекомендуется использовать в 3.0 +; доступен только в пределах [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="f8af4-104">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f8af4-105">Запускает браузер по умолчанию проекта, лицензии или URL-адрес отчетов о нарушении для указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="f8af4-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="f8af4-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="f8af4-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f8af4-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="f8af4-107">Parameters</span></span>

| <span data-ttu-id="f8af4-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="f8af4-108">Parameter</span></span> | <span data-ttu-id="f8af4-109">Описание:</span><span class="sxs-lookup"><span data-stu-id="f8af4-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f8af4-110">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="f8af4-110">Id</span></span> | <span data-ttu-id="f8af4-111">Идентификатор пакета нужный пакет.</span><span class="sxs-lookup"><span data-stu-id="f8af4-111">The package ID of the desired package.</span></span> <span data-ttu-id="f8af4-112">— Идентификатор коммутатора сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="f8af4-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="f8af4-113">Версия</span><span class="sxs-lookup"><span data-stu-id="f8af4-113">Version</span></span> | <span data-ttu-id="f8af4-114">Версия пакета, по умолчанию используется последняя версия.</span><span class="sxs-lookup"><span data-stu-id="f8af4-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="f8af4-115">Исходный код</span><span class="sxs-lookup"><span data-stu-id="f8af4-115">Source</span></span> | <span data-ttu-id="f8af4-116">Источник пакета по умолчанию используется источник, выбранный в источнике раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="f8af4-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="f8af4-117">Лицензия</span><span class="sxs-lookup"><span data-stu-id="f8af4-117">License</span></span> | <span data-ttu-id="f8af4-118">Открывает в браузере URL-адрес пакета лицензий.</span><span class="sxs-lookup"><span data-stu-id="f8af4-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="f8af4-119">Если указан параметр - лицензии ни - ReportAbuse, в браузере будет открыта URL-адрес для пакета проекта.</span><span class="sxs-lookup"><span data-stu-id="f8af4-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="f8af4-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="f8af4-120">ReportAbuse</span></span> | <span data-ttu-id="f8af4-121">Открывает в браузере URL-адрес пакета отчетов о нарушении.</span><span class="sxs-lookup"><span data-stu-id="f8af4-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="f8af4-122">Если указан параметр - лицензии ни - ReportAbuse, в браузере будет открыта URL-адрес для пакета проекта.</span><span class="sxs-lookup"><span data-stu-id="f8af4-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="f8af4-123">Пропустить</span><span class="sxs-lookup"><span data-stu-id="f8af4-123">PassThru</span></span> | <span data-ttu-id="f8af4-124">Отображает URL-адрес; Используйте с - WhatIf, чтобы открыть браузер.</span><span class="sxs-lookup"><span data-stu-id="f8af4-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="f8af4-125">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="f8af4-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f8af4-126">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="f8af4-126">Common Parameters</span></span>

<span data-ttu-id="f8af4-127">`Open-PackagePage` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f8af4-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f8af4-128">Примеры</span><span class="sxs-lookup"><span data-stu-id="f8af4-128">Examples</span></span>

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