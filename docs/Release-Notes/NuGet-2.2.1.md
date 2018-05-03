---
title: Заметки о выпуске NuGet 2.2.1
description: Заметки о выпуске для NuGet 2.2.1, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fddeb4e8c9fb2d85ba1876360862461e8ef025af
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="2d25b-103">Заметки о выпуске NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="2d25b-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="2d25b-104">[Заметки о выпуске NuGet 2.2](../release-notes/nuget-2.2.md) | [заметки о выпуске NuGet 2.5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="2d25b-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="2d25b-105">NuGet 2.2.1 был выпущен 15 февраля 2013 г.</span><span class="sxs-lookup"><span data-stu-id="2d25b-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="2d25b-106">Номер версии расширения VS, 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="2d25b-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="2d25b-107">Локализация обновления</span><span class="sxs-lookup"><span data-stu-id="2d25b-107">Localization Refresh</span></span>
<span data-ttu-id="2d25b-108">Когда NuGet поставляется как часть Visual Studio 2012, он был полностью локализованы на английский + 13 языков.</span><span class="sxs-lookup"><span data-stu-id="2d25b-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="2d25b-109">С этого момента отправки NuGet 2.1 и 2.2, но локализации не были обновлены.</span><span class="sxs-lookup"><span data-stu-id="2d25b-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="2d25b-110">В выпуске NuGet 2.2.1 обновляет локализация.</span><span class="sxs-lookup"><span data-stu-id="2d25b-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="2d25b-111">Пользовательский Интерфейс и консоль PowerShell NuGet, локализованы на следующие языки:</span><span class="sxs-lookup"><span data-stu-id="2d25b-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="2d25b-112">Китайский (упрощенное письмо)</span><span class="sxs-lookup"><span data-stu-id="2d25b-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="2d25b-113">Китайский (традиционное письмо)</span><span class="sxs-lookup"><span data-stu-id="2d25b-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="2d25b-114">Чешский</span><span class="sxs-lookup"><span data-stu-id="2d25b-114">Czech</span></span>
1. <span data-ttu-id="2d25b-115">Английский</span><span class="sxs-lookup"><span data-stu-id="2d25b-115">English</span></span>
1. <span data-ttu-id="2d25b-116">Французский</span><span class="sxs-lookup"><span data-stu-id="2d25b-116">French</span></span>
1. <span data-ttu-id="2d25b-117">Немецкий</span><span class="sxs-lookup"><span data-stu-id="2d25b-117">German</span></span>
1. <span data-ttu-id="2d25b-118">Итальянский</span><span class="sxs-lookup"><span data-stu-id="2d25b-118">Italian</span></span>
1. <span data-ttu-id="2d25b-119">Японский</span><span class="sxs-lookup"><span data-stu-id="2d25b-119">Japanese</span></span>
1. <span data-ttu-id="2d25b-120">Корейский</span><span class="sxs-lookup"><span data-stu-id="2d25b-120">Korean</span></span>
1. <span data-ttu-id="2d25b-121">Польский</span><span class="sxs-lookup"><span data-stu-id="2d25b-121">Polish</span></span>
1. <span data-ttu-id="2d25b-122">Португальский (Бразилия)</span><span class="sxs-lookup"><span data-stu-id="2d25b-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="2d25b-123">Русский</span><span class="sxs-lookup"><span data-stu-id="2d25b-123">Russian</span></span>
1. <span data-ttu-id="2d25b-124">Испанский</span><span class="sxs-lookup"><span data-stu-id="2d25b-124">Spanish</span></span>
1. <span data-ttu-id="2d25b-125">Турецкий</span><span class="sxs-lookup"><span data-stu-id="2d25b-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="2d25b-126">Шаблоны Visual Studio поддерживает несколько репозиториев предварительно установленного пакета</span><span class="sxs-lookup"><span data-stu-id="2d25b-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="2d25b-127">Если создать шаблоны Visual Studio можно использовать NuGet [выполнить предварительную установку пакетов](../visual-studio-extensibility/visual-studio-templates.md) как часть шаблона.</span><span class="sxs-lookup"><span data-stu-id="2d25b-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="2d25b-128">До этого момента, эта функция имеет ограничение необходимость все пакеты из одного источника.</span><span class="sxs-lookup"><span data-stu-id="2d25b-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="2d25b-129">С помощью NuGet 2.2.1, что пакеты, установленные из нескольких репозиториев (в шаблоне, расширение VSIX или папке на диске, определенные в реестре).</span><span class="sxs-lookup"><span data-stu-id="2d25b-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="2d25b-130">Основным сценарием для этой функции — пользовательские шаблоны проектов ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2d25b-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="2d25b-131">Встроенные шаблоны ASP.NET использовать предустановленных пакетов, получают пакеты с локального диска.</span><span class="sxs-lookup"><span data-stu-id="2d25b-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="2d25b-132">Теперь можно создать пользовательский шаблон проекта ASP.NET, который использует существующие пакеты, установленные с помощью ASP.NET, но добавление дополнительных пакетов NuGet в шаблон.</span><span class="sxs-lookup"><span data-stu-id="2d25b-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="2d25b-133">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="2d25b-133">Bug Fixes</span></span>
<span data-ttu-id="2d25b-134">NuGet 2.2.1 включает несколько целевых исправления ошибок.</span><span class="sxs-lookup"><span data-stu-id="2d25b-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="2d25b-135">Список рабочих элементов исправления в NuGet 2.2.1 представление [NuGet отслеживания проблем в этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="2d25b-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="2d25b-136">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="2d25b-136">Known Issues</span></span>

<span data-ttu-id="2d25b-137">При расширении шаблоны проектов ASP.NET все репозитории предустановленных пакетов необходимо использовать то же значение для `isPreunzipped` атрибута.</span><span class="sxs-lookup"><span data-stu-id="2d25b-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
