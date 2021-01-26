---
title: Справочник по Open-PackagePage PowerShell для NuGet
description: Справочник по Open-PackagePage команде PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d34a91007197f8004e4923deedb1cdb26d662d53
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780411"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="6f69b-103">Open-PackagePage (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="6f69b-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="6f69b-104">*Не рекомендуется в 3.0 +; доступно только в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="6f69b-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="6f69b-105">Запускает браузер по умолчанию с проектом, лицензией или URL-адресом сообщения о нарушении для указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="6f69b-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="6f69b-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="6f69b-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="6f69b-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="6f69b-107">Parameters</span></span>

| <span data-ttu-id="6f69b-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="6f69b-108">Parameter</span></span> | <span data-ttu-id="6f69b-109">Описание</span><span class="sxs-lookup"><span data-stu-id="6f69b-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6f69b-110">Id</span><span class="sxs-lookup"><span data-stu-id="6f69b-110">Id</span></span> | <span data-ttu-id="6f69b-111">Идентификатор пакета требуемого пакета.</span><span class="sxs-lookup"><span data-stu-id="6f69b-111">The package ID of the desired package.</span></span> <span data-ttu-id="6f69b-112">Сам переключатель-ID является необязательным.</span><span class="sxs-lookup"><span data-stu-id="6f69b-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="6f69b-113">Версия</span><span class="sxs-lookup"><span data-stu-id="6f69b-113">Version</span></span> | <span data-ttu-id="6f69b-114">Версия пакета, по умолчанию — последняя версия.</span><span class="sxs-lookup"><span data-stu-id="6f69b-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="6f69b-115">Источник</span><span class="sxs-lookup"><span data-stu-id="6f69b-115">Source</span></span> | <span data-ttu-id="6f69b-116">Источник пакета, по умолчанию выбранный источник в раскрывающемся списке Источник.</span><span class="sxs-lookup"><span data-stu-id="6f69b-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="6f69b-117">Лицензия</span><span class="sxs-lookup"><span data-stu-id="6f69b-117">License</span></span> | <span data-ttu-id="6f69b-118">Открывает браузер для URL-адреса лицензии пакета.</span><span class="sxs-lookup"><span data-stu-id="6f69b-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="6f69b-119">Если ни лицензия, ни Репортабусе не указаны, браузер открывает URL-адрес проекта пакета.</span><span class="sxs-lookup"><span data-stu-id="6f69b-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="6f69b-120">репортабусе</span><span class="sxs-lookup"><span data-stu-id="6f69b-120">ReportAbuse</span></span> | <span data-ttu-id="6f69b-121">Открывает браузер для URL-адреса сообщения о нарушении в пакете.</span><span class="sxs-lookup"><span data-stu-id="6f69b-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="6f69b-122">Если ни лицензия, ни Репортабусе не указаны, браузер открывает URL-адрес проекта пакета.</span><span class="sxs-lookup"><span data-stu-id="6f69b-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="6f69b-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="6f69b-123">PassThru</span></span> | <span data-ttu-id="6f69b-124">Отображает URL-адрес. Используйте with-WhatIf, чтобы отключить Открытие браузера.</span><span class="sxs-lookup"><span data-stu-id="6f69b-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="6f69b-125">Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="6f69b-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="6f69b-126">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="6f69b-126">Common Parameters</span></span>

<span data-ttu-id="6f69b-127">`Open-PackagePage` поддерживает следующие [Общие параметры PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6f69b-127">`Open-PackagePage` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="6f69b-128">Примеры</span><span class="sxs-lookup"><span data-stu-id="6f69b-128">Examples</span></span>

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