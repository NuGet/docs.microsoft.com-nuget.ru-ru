---
title: Справочник по PowerShell для Open-Паккажепаже
description: Справочник по команде PowerShell Open-Паккажепаже в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0237c23d81000a1d58264cc0ab48c73d819d0e5a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327381"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="609b7-103">Open-PackagePage (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="609b7-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="609b7-104">*Не рекомендуется в 3.0 +; доступно только в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="609b7-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="609b7-105">Запускает браузер по умолчанию с проектом, лицензией или URL-адресом сообщения о нарушении для указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="609b7-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="609b7-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="609b7-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="609b7-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="609b7-107">Parameters</span></span>

| <span data-ttu-id="609b7-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="609b7-108">Parameter</span></span> | <span data-ttu-id="609b7-109">Описание</span><span class="sxs-lookup"><span data-stu-id="609b7-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="609b7-110">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="609b7-110">Id</span></span> | <span data-ttu-id="609b7-111">Идентификатор пакета требуемого пакета.</span><span class="sxs-lookup"><span data-stu-id="609b7-111">The package ID of the desired package.</span></span> <span data-ttu-id="609b7-112">Сам переключатель-ID является необязательным.</span><span class="sxs-lookup"><span data-stu-id="609b7-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="609b7-113">Версия</span><span class="sxs-lookup"><span data-stu-id="609b7-113">Version</span></span> | <span data-ttu-id="609b7-114">Версия пакета, по умолчанию — последняя версия.</span><span class="sxs-lookup"><span data-stu-id="609b7-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="609b7-115">Source</span><span class="sxs-lookup"><span data-stu-id="609b7-115">Source</span></span> | <span data-ttu-id="609b7-116">Источник пакета, по умолчанию выбранный источник в раскрывающемся списке Источник.</span><span class="sxs-lookup"><span data-stu-id="609b7-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="609b7-117">Лицензия</span><span class="sxs-lookup"><span data-stu-id="609b7-117">License</span></span> | <span data-ttu-id="609b7-118">Открывает браузер для URL-адреса лицензии пакета.</span><span class="sxs-lookup"><span data-stu-id="609b7-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="609b7-119">Если ни лицензия, ни Репортабусе не указаны, браузер открывает URL-адрес проекта пакета.</span><span class="sxs-lookup"><span data-stu-id="609b7-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="609b7-120">репортабусе</span><span class="sxs-lookup"><span data-stu-id="609b7-120">ReportAbuse</span></span> | <span data-ttu-id="609b7-121">Открывает браузер для URL-адреса сообщения о нарушении в пакете.</span><span class="sxs-lookup"><span data-stu-id="609b7-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="609b7-122">Если ни лицензия, ни Репортабусе не указаны, браузер открывает URL-адрес проекта пакета.</span><span class="sxs-lookup"><span data-stu-id="609b7-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="609b7-123">Пропустить</span><span class="sxs-lookup"><span data-stu-id="609b7-123">PassThru</span></span> | <span data-ttu-id="609b7-124">Отображает URL-адрес. Используйте with-WhatIf, чтобы отключить Открытие браузера.</span><span class="sxs-lookup"><span data-stu-id="609b7-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="609b7-125">Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="609b7-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="609b7-126">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="609b7-126">Common Parameters</span></span>

<span data-ttu-id="609b7-127">`Open-PackagePage`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="609b7-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="609b7-128">Примеры</span><span class="sxs-lookup"><span data-stu-id="609b7-128">Examples</span></span>

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