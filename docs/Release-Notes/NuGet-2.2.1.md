---
title: "Заметки о выпуске NuGet 2.2.1 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 39ceaeb3-2d33-4b1c-b195-eba36c6cbf9a
description: "Заметки о выпуске для NuGet 2.2.1, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 2.2.1 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c31150572b4b6e066643ebcf0d92be16b25c6e19
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="f3b04-104">Заметки о выпуске NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="f3b04-104">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="f3b04-105">[Заметки о выпуске NuGet 2.2](../release-notes/nuget-2.2.md) | [заметки о выпуске NuGet 2.5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="f3b04-105">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="f3b04-106">NuGet 2.2.1 был выпущен 15 февраля 2013 г.</span><span class="sxs-lookup"><span data-stu-id="f3b04-106">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="f3b04-107">Номер версии расширения VS, 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="f3b04-107">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="f3b04-108">Локализация обновления</span><span class="sxs-lookup"><span data-stu-id="f3b04-108">Localization Refresh</span></span>
<span data-ttu-id="f3b04-109">Когда NuGet поставляется как часть Visual Studio 2012, он был полностью локализованы на английский + 13 языков.</span><span class="sxs-lookup"><span data-stu-id="f3b04-109">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="f3b04-110">С этого момента отправки NuGet 2.1 и 2.2, но локализации не были обновлены.</span><span class="sxs-lookup"><span data-stu-id="f3b04-110">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="f3b04-111">В выпуске NuGet 2.2.1 обновляет локализация.</span><span class="sxs-lookup"><span data-stu-id="f3b04-111">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="f3b04-112">Пользовательский Интерфейс и консоль PowerShell NuGet, локализованы на следующие языки:</span><span class="sxs-lookup"><span data-stu-id="f3b04-112">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="f3b04-113">Китайский (упрощенное письмо)</span><span class="sxs-lookup"><span data-stu-id="f3b04-113">Chinese (Simplified)</span></span>
1. <span data-ttu-id="f3b04-114">Китайский (традиционное письмо)</span><span class="sxs-lookup"><span data-stu-id="f3b04-114">Chinese (Traditional)</span></span>
1. <span data-ttu-id="f3b04-115">Чешский</span><span class="sxs-lookup"><span data-stu-id="f3b04-115">Czech</span></span>
1. <span data-ttu-id="f3b04-116">Английский</span><span class="sxs-lookup"><span data-stu-id="f3b04-116">English</span></span>
1. <span data-ttu-id="f3b04-117">Французский</span><span class="sxs-lookup"><span data-stu-id="f3b04-117">French</span></span>
1. <span data-ttu-id="f3b04-118">Немецкий</span><span class="sxs-lookup"><span data-stu-id="f3b04-118">German</span></span>
1. <span data-ttu-id="f3b04-119">Итальянский</span><span class="sxs-lookup"><span data-stu-id="f3b04-119">Italian</span></span>
1. <span data-ttu-id="f3b04-120">Японский</span><span class="sxs-lookup"><span data-stu-id="f3b04-120">Japanese</span></span>
1. <span data-ttu-id="f3b04-121">Корейский</span><span class="sxs-lookup"><span data-stu-id="f3b04-121">Korean</span></span>
1. <span data-ttu-id="f3b04-122">Польский</span><span class="sxs-lookup"><span data-stu-id="f3b04-122">Polish</span></span>
1. <span data-ttu-id="f3b04-123">Португальский (Бразилия)</span><span class="sxs-lookup"><span data-stu-id="f3b04-123">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="f3b04-124">Русский</span><span class="sxs-lookup"><span data-stu-id="f3b04-124">Russian</span></span>
1. <span data-ttu-id="f3b04-125">Испанский</span><span class="sxs-lookup"><span data-stu-id="f3b04-125">Spanish</span></span>
1. <span data-ttu-id="f3b04-126">Турецкий</span><span class="sxs-lookup"><span data-stu-id="f3b04-126">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="f3b04-127">Шаблоны Visual Studio поддерживает несколько репозиториев предварительно установленного пакета</span><span class="sxs-lookup"><span data-stu-id="f3b04-127">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="f3b04-128">Если создать шаблоны Visual Studio можно использовать NuGet [выполнить предварительную установку пакетов](../visual-studio-extensibility/visual-studio-templates.md) как часть шаблона.</span><span class="sxs-lookup"><span data-stu-id="f3b04-128">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="f3b04-129">До этого момента, эта функция имеет ограничение необходимость все пакеты из одного источника.</span><span class="sxs-lookup"><span data-stu-id="f3b04-129">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="f3b04-130">С помощью NuGet 2.2.1, что пакеты, установленные из нескольких репозиториев (в шаблоне, расширение VSIX или папке на диске, определенные в реестре).</span><span class="sxs-lookup"><span data-stu-id="f3b04-130">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="f3b04-131">Основным сценарием для этой функции — пользовательские шаблоны проектов ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f3b04-131">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="f3b04-132">Встроенные шаблоны ASP.NET использовать предустановленных пакетов, получают пакеты с локального диска.</span><span class="sxs-lookup"><span data-stu-id="f3b04-132">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="f3b04-133">Теперь можно создать пользовательский шаблон проекта ASP.NET, который использует существующие пакеты, установленные с помощью ASP.NET, но добавление дополнительных пакетов NuGet в шаблон.</span><span class="sxs-lookup"><span data-stu-id="f3b04-133">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="f3b04-134">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="f3b04-134">Bug Fixes</span></span>
<span data-ttu-id="f3b04-135">NuGet 2.2.1 включает несколько целевых исправления ошибок.</span><span class="sxs-lookup"><span data-stu-id="f3b04-135">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="f3b04-136">Список рабочих элементов исправления в NuGet 2.2.1 представление [NuGet отслеживания проблем в этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="f3b04-136">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="f3b04-137">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="f3b04-137">Known Issues</span></span>

<span data-ttu-id="f3b04-138">При расширении шаблоны проектов ASP.NET все репозитории предустановленных пакетов необходимо использовать то же значение для `isPreunzipped` атрибута.</span><span class="sxs-lookup"><span data-stu-id="f3b04-138">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
