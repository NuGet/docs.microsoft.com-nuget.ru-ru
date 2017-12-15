---
title: "Заметки о выпуске NuGet 2.8.1 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: eebbbae4-fc6a-4c05-9102-4ec66b4c64a4
description: "Заметки о выпуске для NuGet 2.8.1, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 2.8.1 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ac33369644d312591bfe8c06540935b2c6063c5d
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="445b9-104">Заметки о выпуске NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="445b9-104">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="445b9-105">[Заметки о выпуске NuGet 2.8](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 заметки о выпуске](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="445b9-105">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="445b9-106">NuGet 2.8.1 был выпущен 2 апреля 2014 г.</span><span class="sxs-lookup"><span data-stu-id="445b9-106">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="445b9-107">Возможности в выпуске</span><span class="sxs-lookup"><span data-stu-id="445b9-107">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="445b9-108">Поддержка проектов Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="445b9-108">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="445b9-109">Теперь этот выпуск поддерживает следующие новые моникеров целевой платформы которые могут использоваться в проекты, предназначенные для Windows Phone 8.1:</span><span class="sxs-lookup"><span data-stu-id="445b9-109">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="445b9-110">WindowsPhone81 / WP81 (для проектов на базе Silverlight для Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="445b9-110">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="445b9-111">WindowsPhoneApp81 / WPA81 (для проектов на базе WinRT приложения Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="445b9-111">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="445b9-112">Обновление расширения WebMatrix NuGet</span><span class="sxs-lookup"><span data-stu-id="445b9-112">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="445b9-113">Этот выпуск содержит обновления для клиента NuGet в WebMatrix для [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1, после чего он обладает например XDT преобразования.</span><span class="sxs-lookup"><span data-stu-id="445b9-113">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="445b9-114">Что более важно, 2.6.1 core обновления позволяет клиенту WebMatrix установить пакеты NuGet, которые содержат более поздних версиях `.nuspec` схемы, в том числе пакеты ASP.NET NuGet.</span><span class="sxs-lookup"><span data-stu-id="445b9-114">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="445b9-115">Дополнительные сведения об обновлении расширения WebMatrix видит конкретных [заметки о выпуске](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="445b9-115">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="445b9-116">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="445b9-116">Bug Fixes</span></span>
<span data-ttu-id="445b9-117">Помимо этих функций этого выпуска NuGet включает исправления других ошибок.</span><span class="sxs-lookup"><span data-stu-id="445b9-117">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="445b9-118">Произошли 16 общее проблемы, описанные в выпуске.</span><span class="sxs-lookup"><span data-stu-id="445b9-118">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="445b9-119">Полный список рабочих элементов исправления в NuGet 2.8.1, представление [NuGet отслеживания проблем в этом выпуске](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="445b9-119">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="445b9-120">Reshipping вместе с Visual Studio «14» CTP-версия</span><span class="sxs-lookup"><span data-stu-id="445b9-120">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="445b9-121">В Visual Studio «14» CTP-версии выпустила 3 июня 2014 г NuGet 2.8.1 поставляется в коробке.</span><span class="sxs-lookup"><span data-stu-id="445b9-121">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="445b9-122">Он поддерживает функции остаются в par с другими 2.8.1 VSIXes такой файл для Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="445b9-122">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
