---
title: Справочник по Find-Package PowerShell для NuGet
description: Справочник по Find-Package команде PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 263835da64340a13737b32ab54ab057cb640a080
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901763"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="2e376-103">Find-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="2e376-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="2e376-104">*Версия 3.0 +; в этом разделе описывается команда в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows. Общие команды PowerShell Find-Package см. в [справочнике по PackageManagement для PowerShell](/powershell/module/packagemanagement).*</span><span class="sxs-lookup"><span data-stu-id="2e376-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="2e376-105">Возвращает набор удаленных пакетов с указанным ИДЕНТИФИКАТОРом или ключевыми словами из источника пакета.</span><span class="sxs-lookup"><span data-stu-id="2e376-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="2e376-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="2e376-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="2e376-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="2e376-107">Parameters</span></span>

| <span data-ttu-id="2e376-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="2e376-108">Parameter</span></span> | <span data-ttu-id="2e376-109">Описание</span><span class="sxs-lookup"><span data-stu-id="2e376-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2e376-110">&lt;Ключевые слова ID&gt;</span><span class="sxs-lookup"><span data-stu-id="2e376-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="2e376-111">Необходимости Ключевые слова, используемые при поиске в источнике пакета.</span><span class="sxs-lookup"><span data-stu-id="2e376-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="2e376-112">Используйте параметр-ExactMatch, чтобы получить только те пакеты, идентификатор пакета которых соответствует ключевым словам.</span><span class="sxs-lookup"><span data-stu-id="2e376-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="2e376-113">Если ключевые слова не заданы, `Find-Package` возвращает список 20 основных пакетов по скачиваниям или число, указанное в параметре-first.</span><span class="sxs-lookup"><span data-stu-id="2e376-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="2e376-114">Обратите внимание, что-ID является необязательным и не-Op.</span><span class="sxs-lookup"><span data-stu-id="2e376-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="2e376-115">Источник</span><span class="sxs-lookup"><span data-stu-id="2e376-115">Source</span></span> | <span data-ttu-id="2e376-116">URL-адрес или путь к папке для источника пакета для поиска.</span><span class="sxs-lookup"><span data-stu-id="2e376-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="2e376-117">Пути к локальным папкам могут быть абсолютными или относительно текущей папки.</span><span class="sxs-lookup"><span data-stu-id="2e376-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="2e376-118">Если этот параметр опущен, `Find-Package` Поиск выполняется в текущем выбранном источнике пакета.</span><span class="sxs-lookup"><span data-stu-id="2e376-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="2e376-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="2e376-119">AllVersions</span></span> | <span data-ttu-id="2e376-120">Отображает все доступные версии каждого пакета, а не только последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="2e376-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="2e376-121">First</span><span class="sxs-lookup"><span data-stu-id="2e376-121">First</span></span> | <span data-ttu-id="2e376-122">Число пакетов, возвращаемых с начала списка; значение по умолчанию — 20.</span><span class="sxs-lookup"><span data-stu-id="2e376-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="2e376-123">Пропустить</span><span class="sxs-lookup"><span data-stu-id="2e376-123">Skip</span></span> | <span data-ttu-id="2e376-124">Опускает первые &lt; целочисленные &gt; пакеты из отображаемого списка.</span><span class="sxs-lookup"><span data-stu-id="2e376-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="2e376-125">инклудепререлеасе</span><span class="sxs-lookup"><span data-stu-id="2e376-125">IncludePrerelease</span></span> | <span data-ttu-id="2e376-126">Включает в результаты предварительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="2e376-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="2e376-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="2e376-127">ExactMatch</span></span> | <span data-ttu-id="2e376-128">Задается для использования &lt; ключевых слов в &gt; качестве идентификатора пакета с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="2e376-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="2e376-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="2e376-129">StartWith</span></span> | <span data-ttu-id="2e376-130">Возвращает пакеты, идентификатор пакета которых начинается с &lt; ключевых слов &gt; .</span><span class="sxs-lookup"><span data-stu-id="2e376-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="2e376-131">Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="2e376-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="2e376-132">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="2e376-132">Common Parameters</span></span>

<span data-ttu-id="2e376-133">`Find-Package` поддерживает следующие [Общие параметры PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="2e376-133">`Find-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="2e376-134">Примеры</span><span class="sxs-lookup"><span data-stu-id="2e376-134">Examples</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```