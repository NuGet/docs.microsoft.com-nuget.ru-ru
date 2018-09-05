---
title: Заметки о выпуске NuGet 2.8.5
description: Заметки о выпуске для NuGet 2.8.5, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548629"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="053ad-103">Заметки о выпуске NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="053ad-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="053ad-104">[Заметки о выпуске NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [заметки о выпуске NuGet 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="053ad-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="053ad-105">NuGet 2.8.5 был выпущен 30 марта 2015 г.</span><span class="sxs-lookup"><span data-stu-id="053ad-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="053ad-106">Он представляет собой незначительное обновление для наших 2.8.3 VSIX с некоторыми целевых исправлений.</span><span class="sxs-lookup"><span data-stu-id="053ad-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="053ad-107">В этом выпуске добавлена поддержка для диалогового окна Диспетчер пакетов NuGet [моникеров целевой платформы DNX](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="053ad-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="053ad-108">Эти новые моникеры платформ, которые поддерживаются включают:</span><span class="sxs-lookup"><span data-stu-id="053ad-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="053ad-109">**core50** — «base» моникер целевой платформы (TFM), совместимого со средой CLR Core.</span><span class="sxs-lookup"><span data-stu-id="053ad-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="053ad-110">**dnx452** - TFM на основе DNX приложений с помощью полного 4.5.2 версия платформы</span><span class="sxs-lookup"><span data-stu-id="053ad-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="053ad-111">**dnx46** - TFM на основе DNX приложений с помощью полной 4.6 версия платформы</span><span class="sxs-lookup"><span data-stu-id="053ad-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="053ad-112">**dnxcore50** - TFM на основе DNX приложений с помощью версии Core 5.0 структуры</span><span class="sxs-lookup"><span data-stu-id="053ad-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="053ad-113">Один ошибка была исправлена, не позволяло пакетов при установке в проектах FSharp должным образом:</span><span class="sxs-lookup"><span data-stu-id="053ad-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400