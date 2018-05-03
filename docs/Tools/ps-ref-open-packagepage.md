---
title: Справочник по PowerShell NuGet Open-PackagePage
description: Ссылка для команды PowerShell PackagePage откройте консоль диспетчера пакетов NuGet в Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: df4bea390105a7e3fc5d2abd476f2908d92bbcf8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="493c5-103">Open-PackagePage (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="493c5-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="493c5-104">*Рекомендуется использовать в 3.0 +; доступен только в пределах [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="493c5-104">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="493c5-105">Запускает браузер по умолчанию проекта, лицензии или URL-адрес отчетов о нарушении для указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="493c5-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="493c5-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="493c5-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="493c5-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="493c5-107">Parameters</span></span>

| <span data-ttu-id="493c5-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="493c5-108">Parameter</span></span> | <span data-ttu-id="493c5-109">Описание</span><span class="sxs-lookup"><span data-stu-id="493c5-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="493c5-110">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="493c5-110">Id</span></span> | <span data-ttu-id="493c5-111">Идентификатор пакета нужный пакет.</span><span class="sxs-lookup"><span data-stu-id="493c5-111">The package ID of the desired package.</span></span> <span data-ttu-id="493c5-112">— Идентификатор коммутатора сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="493c5-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="493c5-113">Версия</span><span class="sxs-lookup"><span data-stu-id="493c5-113">Version</span></span> | <span data-ttu-id="493c5-114">Версия пакета, по умолчанию используется последняя версия.</span><span class="sxs-lookup"><span data-stu-id="493c5-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="493c5-115">Исходный код</span><span class="sxs-lookup"><span data-stu-id="493c5-115">Source</span></span> | <span data-ttu-id="493c5-116">Источник пакета по умолчанию используется источник, выбранный в источнике раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="493c5-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="493c5-117">Лицензия</span><span class="sxs-lookup"><span data-stu-id="493c5-117">License</span></span> | <span data-ttu-id="493c5-118">Открывает в браузере URL-адрес пакета лицензий.</span><span class="sxs-lookup"><span data-stu-id="493c5-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="493c5-119">Если указан параметр - лицензии ни - ReportAbuse, в браузере будет открыта URL-адрес для пакета проекта.</span><span class="sxs-lookup"><span data-stu-id="493c5-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="493c5-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="493c5-120">ReportAbuse</span></span> | <span data-ttu-id="493c5-121">Открывает в браузере URL-адрес пакета отчетов о нарушении.</span><span class="sxs-lookup"><span data-stu-id="493c5-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="493c5-122">Если указан параметр - лицензии ни - ReportAbuse, в браузере будет открыта URL-адрес для пакета проекта.</span><span class="sxs-lookup"><span data-stu-id="493c5-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="493c5-123">Пропустить</span><span class="sxs-lookup"><span data-stu-id="493c5-123">PassThru</span></span> | <span data-ttu-id="493c5-124">Отображает URL-адрес; Используйте с - WhatIf, чтобы открыть браузер.</span><span class="sxs-lookup"><span data-stu-id="493c5-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="493c5-125">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="493c5-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="493c5-126">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="493c5-126">Common Parameters</span></span>

<span data-ttu-id="493c5-127">`Open-PackagePage` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="493c5-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="493c5-128">Примеры</span><span class="sxs-lookup"><span data-stu-id="493c5-128">Examples</span></span>

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