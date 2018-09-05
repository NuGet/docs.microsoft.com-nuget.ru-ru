---
title: Заметки о выпуске NuGet 2.8.1
description: Заметки о выпуске для NuGet 2.8.1, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545243"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="800b9-103">Заметки о выпуске NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="800b9-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="800b9-104">[Заметки о выпуске NuGet 2.8](../release-notes/nuget-2.8.md) | [заметки о выпуске NuGet 2.8.2](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="800b9-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="800b9-105">NuGet 2.8.1 был выпущен 2 апреля 2014 г.</span><span class="sxs-lookup"><span data-stu-id="800b9-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="800b9-106">Важные возможности в выпуске</span><span class="sxs-lookup"><span data-stu-id="800b9-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="800b9-107">Поддержка проектов Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="800b9-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="800b9-108">Теперь этот выпуск поддерживает следующие новые моникеров целевой платформы которых может использоваться для проектов, предназначенные для Windows Phone 8.1:</span><span class="sxs-lookup"><span data-stu-id="800b9-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="800b9-109">WindowsPhone81 / WP81 (для проектов на базе Silverlight Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="800b9-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="800b9-110">WindowsPhoneApp81 / WPA81 (для проектов на базе WinRT приложения Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="800b9-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="800b9-111">Обновление расширения WebMatrix NuGet</span><span class="sxs-lookup"><span data-stu-id="800b9-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="800b9-112">Этот выпуск обновляет в WebMatrix для клиента NuGet [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 и с его такие функции преобразования XDT.</span><span class="sxs-lookup"><span data-stu-id="800b9-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="800b9-113">Что более важно, 2.6.1 core обновления позволяет клиенту WebMatrix установки пакетов NuGet, которые содержат более поздних версиях `.nuspec` схемы, в том числе пакеты ASP.NET NuGet.</span><span class="sxs-lookup"><span data-stu-id="800b9-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="800b9-114">Дополнительные сведения об обновлении расширения WebMatrix см. в разделе их [заметки о выпуске](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="800b9-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="800b9-115">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="800b9-115">Bug Fixes</span></span>
<span data-ttu-id="800b9-116">Помимо этих функций в этот выпуск NuGet включает другие исправления ошибок.</span><span class="sxs-lookup"><span data-stu-id="800b9-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="800b9-117">Возникали 16 общее проблемы, описанной в выпуске.</span><span class="sxs-lookup"><span data-stu-id="800b9-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="800b9-118">Полный список рабочих элементов исправленные в NuGet 2.8.1, пожалуйста представление [Issue Tracker NuGet для этого выпуска](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="800b9-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="800b9-119">Reshipping с помощью Visual Studio «14» CTP-версии</span><span class="sxs-lookup"><span data-stu-id="800b9-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="800b9-120">В Visual Studio «14» CTP, выпущенную 3 июня 2014 года NuGet 2.8.1 поставляется в поле.</span><span class="sxs-lookup"><span data-stu-id="800b9-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="800b9-121">Он поддерживает функции остаются в одном уровне с другими 2.8.1 VSIXes, например в каталог для Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="800b9-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
