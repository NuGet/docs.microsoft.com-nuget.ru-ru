---
title: Заметки о выпуске 2.8.1 NuGet
description: Заметки о выпуске NuGet 2.8.1, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776769"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="35530-103">Заметки о выпуске 2.8.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="35530-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="35530-104">[Заметки о](../release-notes/nuget-2.8.md)  |  выпуске NuGet 2,8 [Заметки о выпуске 2.8.2 NuGet](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="35530-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="35530-105">2.8.1 NuGet выпущен 2 апреля 2014 г.</span><span class="sxs-lookup"><span data-stu-id="35530-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="35530-106">Важные функции в выпуске</span><span class="sxs-lookup"><span data-stu-id="35530-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="35530-107">Поддержка проектов Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="35530-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="35530-108">Этот выпуск теперь поддерживает следующие новые моникеры целевой платформы, которые можно использовать для назначения проектов Windows Phone 8,1:</span><span class="sxs-lookup"><span data-stu-id="35530-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="35530-109">WindowsPhone81/WP81 (для проектов Windows Phone на основе Silverlight)</span><span class="sxs-lookup"><span data-stu-id="35530-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="35530-110">WindowsPhoneApp81/WPA81 (для проектов приложений на основе WinRT Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="35530-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="35530-111">Обновление расширения WebMatrix для NuGet</span><span class="sxs-lookup"><span data-stu-id="35530-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="35530-112">Этот выпуск обновляет клиент NuGet, находящийся в WebMatrix, в [NuGet. Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 и включает в себя такие функции, как преобразование xdt.</span><span class="sxs-lookup"><span data-stu-id="35530-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="35530-113">Что более важно, обновление 2.6.1 Core позволяет клиенту WebMatrix устанавливать пакеты NuGet, содержащие более новые версии `.nuspec` схемы, включая пакеты nuget ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="35530-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="35530-114">Дополнительные сведения об обновлении расширения WebMatrix см. в соответствующих [заметках о выпуске](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="35530-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="35530-115">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="35530-115">Bug Fixes</span></span>
<span data-ttu-id="35530-116">Помимо этих функций, в этом выпуске NuGet имеются другие исправления ошибок.</span><span class="sxs-lookup"><span data-stu-id="35530-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="35530-117">В выпуске было решено 16 общих проблем.</span><span class="sxs-lookup"><span data-stu-id="35530-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="35530-118">Полный список рабочих элементов, исправленных в NuGet 2.8.1, см. в [этом выпуске](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="35530-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="35530-119">Перепоставка с помощью Visual Studio "14" CTP</span><span class="sxs-lookup"><span data-stu-id="35530-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="35530-120">В Visual Studio «14» CTP-версии, выпущенной 3 июня 2014, в поле поставляются пакеты NuGet 2.8.1.</span><span class="sxs-lookup"><span data-stu-id="35530-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="35530-121">Функции, которые он поддерживает, остаются в неизменном виде с другими 2.8.1 VSIX, такими как для Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="35530-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
