---
title: "Заметки о выпуске NuGet 2.8.5 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 60b96b2e-2a61-4f10-b5ad-3299f5a6d453
description: "Заметки о выпуске для NuGet 2.8.5, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 2.8.5 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3b297704968b8423f60e9de08e27860dc375c019
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="977f3-104">Заметки о выпуске NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="977f3-104">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="977f3-105">[Заметки о выпуске NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 заметки о выпуске](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="977f3-105">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="977f3-106">NuGet 2.8.5 был выпущен 30 марта 2015 г.</span><span class="sxs-lookup"><span data-stu-id="977f3-106">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="977f3-107">Это незначительное обновление с нашей 2.8.3 VSIX с некоторыми целевых исправления.</span><span class="sxs-lookup"><span data-stu-id="977f3-107">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="977f3-108">В этом выпуске добавлена поддержка для диалогового окна диспетчера пакетов NuGet [DNX моникеров целевой платформы](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="977f3-108">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="977f3-109">Эти новые моникеров платформы, которые поддерживаются следующие.</span><span class="sxs-lookup"><span data-stu-id="977f3-109">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="977f3-110">**core50** — «base» целевой framework моникером, совместимый с Core CLR.</span><span class="sxs-lookup"><span data-stu-id="977f3-110">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="977f3-111">**dnx452** — TFM конкретных на основе DNX приложений с помощью полного 4.5.2 версия платформы</span><span class="sxs-lookup"><span data-stu-id="977f3-111">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="977f3-112">**dnx46** — TFM конкретных на основе DNX приложений с помощью полного 4,6 версия платформы</span><span class="sxs-lookup"><span data-stu-id="977f3-112">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="977f3-113">**dnxcore50** — TFM конкретных на основе DNX приложений с помощью версии Core 5.0 структуры</span><span class="sxs-lookup"><span data-stu-id="977f3-113">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="977f3-114">Один исправлена ошибка, предотвращено пакетов при установке в проектах FSharp должным образом:</span><span class="sxs-lookup"><span data-stu-id="977f3-114">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

<span data-ttu-id="977f3-115">https://NuGet.CodePlex.com/WorkItem/4400</span><span class="sxs-lookup"><span data-stu-id="977f3-115">https://nuget.codeplex.com/workitem/4400</span></span>