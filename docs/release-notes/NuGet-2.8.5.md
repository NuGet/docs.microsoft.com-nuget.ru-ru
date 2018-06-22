---
title: Заметки о выпуске NuGet 2.8.5
description: Заметки о выпуске для NuGet 2.8.5, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820083"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="663a5-103">Заметки о выпуске NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="663a5-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="663a5-104">[Заметки о выпуске NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 заметки о выпуске](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="663a5-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="663a5-105">NuGet 2.8.5 был выпущен 30 марта 2015 г.</span><span class="sxs-lookup"><span data-stu-id="663a5-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="663a5-106">Это незначительное обновление с нашей 2.8.3 VSIX с некоторыми целевых исправления.</span><span class="sxs-lookup"><span data-stu-id="663a5-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="663a5-107">В этом выпуске добавлена поддержка для диалогового окна диспетчера пакетов NuGet [DNX моникеров целевой платформы](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="663a5-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="663a5-108">Эти новые моникеров платформы, которые поддерживаются следующие.</span><span class="sxs-lookup"><span data-stu-id="663a5-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="663a5-109">**core50** — «base» целевой framework моникером, совместимый с Core CLR.</span><span class="sxs-lookup"><span data-stu-id="663a5-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="663a5-110">**dnx452** — TFM конкретных на основе DNX приложений с помощью полного 4.5.2 версия платформы</span><span class="sxs-lookup"><span data-stu-id="663a5-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="663a5-111">**dnx46** — TFM конкретных на основе DNX приложений с помощью полного 4,6 версия платформы</span><span class="sxs-lookup"><span data-stu-id="663a5-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="663a5-112">**dnxcore50** — TFM конкретных на основе DNX приложений с помощью версии Core 5.0 структуры</span><span class="sxs-lookup"><span data-stu-id="663a5-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="663a5-113">Один исправлена ошибка, предотвращено пакетов при установке в проектах FSharp должным образом:</span><span class="sxs-lookup"><span data-stu-id="663a5-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400