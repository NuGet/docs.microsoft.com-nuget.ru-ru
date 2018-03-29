---
title: Справочник по PowerShell NuGet Open-PackagePage | Документы Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Ссылка для команды PowerShell PackagePage откройте консоль диспетчера пакетов NuGet в Visual Studio.
keywords: Пакет NuGet консоли диспетчера, команд NuGet Powershell, справочник по NuGet Powershell, откройте PackagePage
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 5e0955e58daacf381666c676c8fcf22c698e9db6
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="3265b-104">Open-PackagePage (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3265b-104">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3265b-105">*Рекомендуется использовать в 3.0 +; доступен только в пределах [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="3265b-105">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="3265b-106">Запускает браузер по умолчанию проекта, лицензии или URL-адрес отчетов о нарушении для указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="3265b-106">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="3265b-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="3265b-107">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="3265b-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="3265b-108">Parameters</span></span>

| <span data-ttu-id="3265b-109">Параметр</span><span class="sxs-lookup"><span data-stu-id="3265b-109">Parameter</span></span> | <span data-ttu-id="3265b-110">Описание</span><span class="sxs-lookup"><span data-stu-id="3265b-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3265b-111">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="3265b-111">Id</span></span> | <span data-ttu-id="3265b-112">Идентификатор пакета нужный пакет.</span><span class="sxs-lookup"><span data-stu-id="3265b-112">The package ID of the desired package.</span></span> <span data-ttu-id="3265b-113">— Идентификатор коммутатора сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="3265b-113">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="3265b-114">Версия</span><span class="sxs-lookup"><span data-stu-id="3265b-114">Version</span></span> | <span data-ttu-id="3265b-115">Версия пакета, по умолчанию используется последняя версия.</span><span class="sxs-lookup"><span data-stu-id="3265b-115">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="3265b-116">Исходный код</span><span class="sxs-lookup"><span data-stu-id="3265b-116">Source</span></span> | <span data-ttu-id="3265b-117">Источник пакета по умолчанию используется источник, выбранный в источнике раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="3265b-117">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="3265b-118">Лицензия</span><span class="sxs-lookup"><span data-stu-id="3265b-118">License</span></span> | <span data-ttu-id="3265b-119">Открывает в браузере URL-адрес пакета лицензий.</span><span class="sxs-lookup"><span data-stu-id="3265b-119">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="3265b-120">Если указан параметр - лицензии ни - ReportAbuse, в браузере будет открыта URL-адрес для пакета проекта.</span><span class="sxs-lookup"><span data-stu-id="3265b-120">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="3265b-121">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="3265b-121">ReportAbuse</span></span> | <span data-ttu-id="3265b-122">Открывает в браузере URL-адрес пакета отчетов о нарушении.</span><span class="sxs-lookup"><span data-stu-id="3265b-122">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="3265b-123">Если указан параметр - лицензии ни - ReportAbuse, в браузере будет открыта URL-адрес для пакета проекта.</span><span class="sxs-lookup"><span data-stu-id="3265b-123">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="3265b-124">Пропустить</span><span class="sxs-lookup"><span data-stu-id="3265b-124">PassThru</span></span> | <span data-ttu-id="3265b-125">Отображает URL-адрес; Используйте с - WhatIf, чтобы открыть браузер.</span><span class="sxs-lookup"><span data-stu-id="3265b-125">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="3265b-126">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="3265b-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3265b-127">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="3265b-127">Common Parameters</span></span>

<span data-ttu-id="3265b-128">`Open-PackagePage` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3265b-128">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3265b-129">Примеры</span><span class="sxs-lookup"><span data-stu-id="3265b-129">Examples</span></span>

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