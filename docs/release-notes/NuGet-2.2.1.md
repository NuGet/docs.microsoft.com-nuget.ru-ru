---
title: Заметки о выпуске NuGet 2.2.1
description: Заметки о выпуске для NuGet 2.2.1, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550702"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="03223-103">Заметки о выпуске NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="03223-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="03223-104">[Заметки о выпуске NuGet 2.2](../release-notes/nuget-2.2.md) | [заметки о выпуске NuGet 2.5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="03223-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="03223-105">15 февраля 2013 г. была выпущена NuGet 2.2.1.</span><span class="sxs-lookup"><span data-stu-id="03223-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="03223-106">Номер версии расширения VS — 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="03223-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="03223-107">Обновление локализации</span><span class="sxs-lookup"><span data-stu-id="03223-107">Localization Refresh</span></span>
<span data-ttu-id="03223-108">Когда NuGet поставляется как часть Visual Studio 2012, он был полностью локализованы на английский + 13 языков.</span><span class="sxs-lookup"><span data-stu-id="03223-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="03223-109">С тех пор отправки NuGet 2.1 и 2.2, но локализации бы не был обновлен.</span><span class="sxs-lookup"><span data-stu-id="03223-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="03223-110">В выпуске NuGet 2.2.1 обновляет наша локализация.</span><span class="sxs-lookup"><span data-stu-id="03223-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="03223-111">Пользовательский Интерфейс и консоль PowerShell NuGet, локализованы на следующих языках:</span><span class="sxs-lookup"><span data-stu-id="03223-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="03223-112">Китайский (упрощенное письмо)</span><span class="sxs-lookup"><span data-stu-id="03223-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="03223-113">Китайский (традиционное письмо)</span><span class="sxs-lookup"><span data-stu-id="03223-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="03223-114">Чешский</span><span class="sxs-lookup"><span data-stu-id="03223-114">Czech</span></span>
1. <span data-ttu-id="03223-115">Английский</span><span class="sxs-lookup"><span data-stu-id="03223-115">English</span></span>
1. <span data-ttu-id="03223-116">Французский</span><span class="sxs-lookup"><span data-stu-id="03223-116">French</span></span>
1. <span data-ttu-id="03223-117">Немецкий</span><span class="sxs-lookup"><span data-stu-id="03223-117">German</span></span>
1. <span data-ttu-id="03223-118">Итальянский</span><span class="sxs-lookup"><span data-stu-id="03223-118">Italian</span></span>
1. <span data-ttu-id="03223-119">Японский</span><span class="sxs-lookup"><span data-stu-id="03223-119">Japanese</span></span>
1. <span data-ttu-id="03223-120">Корейский</span><span class="sxs-lookup"><span data-stu-id="03223-120">Korean</span></span>
1. <span data-ttu-id="03223-121">Польский</span><span class="sxs-lookup"><span data-stu-id="03223-121">Polish</span></span>
1. <span data-ttu-id="03223-122">Португальский (Бразилия)</span><span class="sxs-lookup"><span data-stu-id="03223-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="03223-123">Русский</span><span class="sxs-lookup"><span data-stu-id="03223-123">Russian</span></span>
1. <span data-ttu-id="03223-124">Испанский</span><span class="sxs-lookup"><span data-stu-id="03223-124">Spanish</span></span>
1. <span data-ttu-id="03223-125">Турецкий</span><span class="sxs-lookup"><span data-stu-id="03223-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="03223-126">Шаблоны Visual Studio поддерживают несколько репозиториев предварительно установленного пакета</span><span class="sxs-lookup"><span data-stu-id="03223-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="03223-127">Если вы создаете шаблоны Visual Studio, можно использовать NuGet для [выполнить предварительную установку пакетов](../visual-studio-extensibility/visual-studio-templates.md) как часть шаблона.</span><span class="sxs-lookup"><span data-stu-id="03223-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="03223-128">До сих пор эта функция имеет ограничение, все пакеты, необходимые для берутся из одного источника.</span><span class="sxs-lookup"><span data-stu-id="03223-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="03223-129">Однако с помощью NuGet 2.2.1 может иметь пакеты, установленные из нескольких репозиториев (в рамках шаблона, VSIX или папке на диске, определенные в реестре).</span><span class="sxs-lookup"><span data-stu-id="03223-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="03223-130">Основным сценарием для этой функции — настраиваемые шаблоны проектов ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="03223-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="03223-131">Встроенные шаблоны ASP.NET использовать предустановленных пакетов, получают пакеты с локального диска.</span><span class="sxs-lookup"><span data-stu-id="03223-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="03223-132">Теперь можно создать пользовательский шаблон проекта ASP.NET, который использует существующие пакеты, установленные ASP.NET, но добавить дополнительные пакеты NuGet в шаблон.</span><span class="sxs-lookup"><span data-stu-id="03223-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="03223-133">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="03223-133">Bug Fixes</span></span>
<span data-ttu-id="03223-134">NuGet 2.2.1 включает в себя несколько целевых исправлений ошибок.</span><span class="sxs-lookup"><span data-stu-id="03223-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="03223-135">Список рабочих элементов исправленные в NuGet 2.2.1 представление [Issue Tracker NuGet для этого выпуска](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="03223-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="03223-136">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="03223-136">Known Issues</span></span>

<span data-ttu-id="03223-137">При расширении шаблоны проектов ASP.NET, все репозитории предустановленных пакетов необходимо использовать то же значение для `isPreunzipped` атрибута.</span><span class="sxs-lookup"><span data-stu-id="03223-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
