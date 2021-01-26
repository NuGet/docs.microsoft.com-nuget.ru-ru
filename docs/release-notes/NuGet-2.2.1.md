---
title: Заметки о выпуске NuGet 2.2.1
description: Заметки о выпуске NuGet 2.2.1, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776802"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="8dae9-103">Заметки о выпуске NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="8dae9-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="8dae9-104">[Заметки о](../release-notes/nuget-2.2.md)  |  выпуске NuGet 2,2 [Заметки о выпуске NuGet 2,5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="8dae9-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="8dae9-105">Версия NuGet 2.2.1 была выпущена 15 февраля 2013 г.</span><span class="sxs-lookup"><span data-stu-id="8dae9-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="8dae9-106">Номер версии расширения VS — 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="8dae9-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="8dae9-107">Обновление локализации</span><span class="sxs-lookup"><span data-stu-id="8dae9-107">Localization Refresh</span></span>
<span data-ttu-id="8dae9-108">Когда NuGet поставляется в составе Visual Studio 2012, он был полностью локализован на английский + 13 других языков.</span><span class="sxs-lookup"><span data-stu-id="8dae9-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="8dae9-109">С этого момента, NuGet 2,1 и 2,2 поставляются, но локализация не обновлялась.</span><span class="sxs-lookup"><span data-stu-id="8dae9-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="8dae9-110">Выпуск NuGet 2.2.1 обновляет нашу локализацию.</span><span class="sxs-lookup"><span data-stu-id="8dae9-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="8dae9-111">Пользовательский интерфейс и консоль PowerShell для NuGet локализованы на следующие языки:</span><span class="sxs-lookup"><span data-stu-id="8dae9-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="8dae9-112">Китайский (упрощенное письмо)</span><span class="sxs-lookup"><span data-stu-id="8dae9-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="8dae9-113">Китайский (традиционное письмо)</span><span class="sxs-lookup"><span data-stu-id="8dae9-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="8dae9-114">Чешский</span><span class="sxs-lookup"><span data-stu-id="8dae9-114">Czech</span></span>
1. <span data-ttu-id="8dae9-115">Английский</span><span class="sxs-lookup"><span data-stu-id="8dae9-115">English</span></span>
1. <span data-ttu-id="8dae9-116">Французский</span><span class="sxs-lookup"><span data-stu-id="8dae9-116">French</span></span>
1. <span data-ttu-id="8dae9-117">Немецкий</span><span class="sxs-lookup"><span data-stu-id="8dae9-117">German</span></span>
1. <span data-ttu-id="8dae9-118">Итальянский</span><span class="sxs-lookup"><span data-stu-id="8dae9-118">Italian</span></span>
1. <span data-ttu-id="8dae9-119">Японский</span><span class="sxs-lookup"><span data-stu-id="8dae9-119">Japanese</span></span>
1. <span data-ttu-id="8dae9-120">Корейский</span><span class="sxs-lookup"><span data-stu-id="8dae9-120">Korean</span></span>
1. <span data-ttu-id="8dae9-121">Польский</span><span class="sxs-lookup"><span data-stu-id="8dae9-121">Polish</span></span>
1. <span data-ttu-id="8dae9-122">Португальский (Бразилия)</span><span class="sxs-lookup"><span data-stu-id="8dae9-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="8dae9-123">Русский</span><span class="sxs-lookup"><span data-stu-id="8dae9-123">Russian</span></span>
1. <span data-ttu-id="8dae9-124">Испанский</span><span class="sxs-lookup"><span data-stu-id="8dae9-124">Spanish</span></span>
1. <span data-ttu-id="8dae9-125">Турецкий</span><span class="sxs-lookup"><span data-stu-id="8dae9-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="8dae9-126">Шаблоны Visual Studio поддерживают несколько предварительно установленных репозиториев пакетов</span><span class="sxs-lookup"><span data-stu-id="8dae9-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="8dae9-127">Если вы создаете шаблоны Visual Studio, вы можете использовать NuGet для [предварительной установки пакетов](../visual-studio-extensibility/visual-studio-templates.md) в составе шаблона.</span><span class="sxs-lookup"><span data-stu-id="8dae9-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="8dae9-128">До настоящего момента эта функция имела ограничение на то, что все пакеты, необходимые для появления из одного и того же источника.</span><span class="sxs-lookup"><span data-stu-id="8dae9-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="8dae9-129">При использовании NuGet 2.2.1 можно установить пакеты из нескольких репозиториев (в шаблоне, в VSIX или в папке на диске, определенном в реестре).</span><span class="sxs-lookup"><span data-stu-id="8dae9-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="8dae9-130">Основным сценарием для этой функции являются пользовательские шаблоны проектов ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8dae9-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="8dae9-131">Встроенные шаблоны ASP.NET используют Предустановленные пакеты, получая пакеты с локального диска.</span><span class="sxs-lookup"><span data-stu-id="8dae9-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="8dae9-132">Теперь можно создать пользовательский шаблон проекта ASP.NET, использующий существующие пакеты, установленные ASP.NET, но добавить дополнительные пакеты NuGet в шаблон.</span><span class="sxs-lookup"><span data-stu-id="8dae9-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="8dae9-133">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="8dae9-133">Bug Fixes</span></span>
<span data-ttu-id="8dae9-134">NuGet 2.2.1 включает в себя несколько исправлений, предназначенных для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="8dae9-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="8dae9-135">Список рабочих элементов, исправленных в NuGet 2.2.1, см. в [этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="8dae9-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="8dae9-136">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="8dae9-136">Known Issues</span></span>

<span data-ttu-id="8dae9-137">При расширении шаблонов проектов ASP.NET все предварительно установленные репозитории пакетов должны использовать одно и то же значение для `isPreunzipped` атрибута.</span><span class="sxs-lookup"><span data-stu-id="8dae9-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
