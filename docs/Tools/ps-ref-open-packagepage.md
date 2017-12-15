---
title: "Справочник по PowerShell NuGet Open-PackagePage | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: e9f84530-6b3d-43b0-a832-0acb2997f6fc
description: "Ссылка для команды PowerShell PackagePage откройте консоль диспетчера пакетов NuGet в Visual Studio."
keywords: "Пакет NuGet консоли диспетчера, команд NuGet Powershell, справочник по NuGet Powershell, откройте PackagePage"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ec4310ea9d13926b1cb3b227b17016742a70bc16
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="6ca2d-104">Open-PackagePage (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="6ca2d-104">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="6ca2d-105">*Рекомендуется использовать в 3.0 +; доступен только в пределах [консоль диспетчера пакетов NuGet](Package-Manager-Console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="6ca2d-105">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="6ca2d-106">Запускает браузер по умолчанию проекта, лицензии или URL-адрес отчетов о нарушении для указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="6ca2d-106">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="6ca2d-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="6ca2d-107">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="6ca2d-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="6ca2d-108">Parameters</span></span>

| <span data-ttu-id="6ca2d-109">Параметр</span><span class="sxs-lookup"><span data-stu-id="6ca2d-109">Parameter</span></span> | <span data-ttu-id="6ca2d-110">Описание</span><span class="sxs-lookup"><span data-stu-id="6ca2d-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6ca2d-111">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="6ca2d-111">Id</span></span> | <span data-ttu-id="6ca2d-112">Идентификатор пакета нужный пакет.</span><span class="sxs-lookup"><span data-stu-id="6ca2d-112">The package ID of the desired package.</span></span> <span data-ttu-id="6ca2d-113">— Идентификатор коммутатора сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="6ca2d-113">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="6ca2d-114">Версия</span><span class="sxs-lookup"><span data-stu-id="6ca2d-114">Version</span></span> | <span data-ttu-id="6ca2d-115">Версия пакета, по умолчанию используется последняя версия.</span><span class="sxs-lookup"><span data-stu-id="6ca2d-115">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="6ca2d-116">Исходный код</span><span class="sxs-lookup"><span data-stu-id="6ca2d-116">Source</span></span> | <span data-ttu-id="6ca2d-117">Источник пакета по умолчанию используется источник, выбранный в источнике раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="6ca2d-117">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="6ca2d-118">Лицензия</span><span class="sxs-lookup"><span data-stu-id="6ca2d-118">License</span></span> | <span data-ttu-id="6ca2d-119">Открывает в браузере URL-адрес пакета лицензий.</span><span class="sxs-lookup"><span data-stu-id="6ca2d-119">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="6ca2d-120">Если указан параметр - лицензии ни - ReportAbuse, в браузере будет открыта URL-адрес для пакета проекта.</span><span class="sxs-lookup"><span data-stu-id="6ca2d-120">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="6ca2d-121">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="6ca2d-121">ReportAbuse</span></span> | <span data-ttu-id="6ca2d-122">Открывает в браузере URL-адрес пакета отчетов о нарушении.</span><span class="sxs-lookup"><span data-stu-id="6ca2d-122">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="6ca2d-123">Если указан параметр - лицензии ни - ReportAbuse, в браузере будет открыта URL-адрес для пакета проекта.</span><span class="sxs-lookup"><span data-stu-id="6ca2d-123">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="6ca2d-124">Пропустить</span><span class="sxs-lookup"><span data-stu-id="6ca2d-124">PassThru</span></span> | <span data-ttu-id="6ca2d-125">Отображает URL-адрес; Используйте с - WhatIf, чтобы открыть браузер.</span><span class="sxs-lookup"><span data-stu-id="6ca2d-125">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="6ca2d-126">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="6ca2d-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="6ca2d-127">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="6ca2d-127">Common Parameters</span></span>

<span data-ttu-id="6ca2d-128">`Open-PackagePage`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6ca2d-128">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="6ca2d-129">Примеры</span><span class="sxs-lookup"><span data-stu-id="6ca2d-129">Examples</span></span>

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