---
title: Справочник по PowerShell для поиска NuGet
description: Справочник по командам PowerShell Find-Package в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4bb6d090b97dd55fc1be0625855aab27a0d181c4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327391"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="a0c03-103">Find-Package (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="a0c03-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a0c03-104">*Версия 3.0 +; в этом разделе описывается команда в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows. Сведения об универсальной команде PowerShell Find-package см. в справочнике по модульу [PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="a0c03-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="a0c03-105">Возвращает набор удаленных пакетов с указанным ИДЕНТИФИКАТОРом или ключевыми словами из источника пакета.</span><span class="sxs-lookup"><span data-stu-id="a0c03-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="a0c03-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="a0c03-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a0c03-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="a0c03-107">Parameters</span></span>

| <span data-ttu-id="a0c03-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="a0c03-108">Parameter</span></span> | <span data-ttu-id="a0c03-109">Описание</span><span class="sxs-lookup"><span data-stu-id="a0c03-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a0c03-110">Ключевые &lt;слова ID&gt;</span><span class="sxs-lookup"><span data-stu-id="a0c03-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="a0c03-111">Необходимости Ключевые слова, используемые при поиске в источнике пакета.</span><span class="sxs-lookup"><span data-stu-id="a0c03-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="a0c03-112">Используйте параметр-ExactMatch, чтобы получить только те пакеты, идентификатор пакета которых соответствует ключевым словам.</span><span class="sxs-lookup"><span data-stu-id="a0c03-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="a0c03-113">Если ключевые слова не заданы `Find-Package` , возвращает список 20 основных пакетов по скачиваниям или число, указанное в параметре-first.</span><span class="sxs-lookup"><span data-stu-id="a0c03-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="a0c03-114">Обратите внимание, что-ID является необязательным и не-Op.</span><span class="sxs-lookup"><span data-stu-id="a0c03-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="a0c03-115">Source</span><span class="sxs-lookup"><span data-stu-id="a0c03-115">Source</span></span> | <span data-ttu-id="a0c03-116">URL-адрес или путь к папке для источника пакета для поиска.</span><span class="sxs-lookup"><span data-stu-id="a0c03-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="a0c03-117">Пути к локальным папкам могут быть абсолютными или относительно текущей папки.</span><span class="sxs-lookup"><span data-stu-id="a0c03-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="a0c03-118">Если этот параметр опущен `Find-Package` , поиск выполняется в текущем выбранном источнике пакета.</span><span class="sxs-lookup"><span data-stu-id="a0c03-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="a0c03-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="a0c03-119">AllVersions</span></span> | <span data-ttu-id="a0c03-120">Отображает все доступные версии каждого пакета, а не только последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="a0c03-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="a0c03-121">Первая</span><span class="sxs-lookup"><span data-stu-id="a0c03-121">First</span></span> | <span data-ttu-id="a0c03-122">Число пакетов, возвращаемых с начала списка; значение по умолчанию — 20.</span><span class="sxs-lookup"><span data-stu-id="a0c03-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="a0c03-123">Skip</span><span class="sxs-lookup"><span data-stu-id="a0c03-123">Skip</span></span> | <span data-ttu-id="a0c03-124">Опускает первые &lt;целочисленные&gt; пакеты из отображаемого списка.</span><span class="sxs-lookup"><span data-stu-id="a0c03-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="a0c03-125">инклудепререлеасе</span><span class="sxs-lookup"><span data-stu-id="a0c03-125">IncludePrerelease</span></span> | <span data-ttu-id="a0c03-126">Включает в результаты предварительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="a0c03-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="a0c03-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="a0c03-127">ExactMatch</span></span> | <span data-ttu-id="a0c03-128">Задается &lt;для&gt; использования ключевых слов в качестве идентификатора пакета с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="a0c03-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="a0c03-129">стартвис</span><span class="sxs-lookup"><span data-stu-id="a0c03-129">StartWith</span></span> | <span data-ttu-id="a0c03-130">Возвращает пакеты, идентификатор пакета которых начинается &lt;с&gt;ключевых слов.</span><span class="sxs-lookup"><span data-stu-id="a0c03-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="a0c03-131">Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="a0c03-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a0c03-132">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="a0c03-132">Common Parameters</span></span>

<span data-ttu-id="a0c03-133">`Find-Package`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="a0c03-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a0c03-134">Примеры</span><span class="sxs-lookup"><span data-stu-id="a0c03-134">Examples</span></span>

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
