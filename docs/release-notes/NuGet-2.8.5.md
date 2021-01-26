---
title: Заметки о выпуске 2.8.5 NuGet
description: Заметки о выпуске NuGet 2.8.5, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780357"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="1314d-103">Заметки о выпуске 2.8.5 NuGet</span><span class="sxs-lookup"><span data-stu-id="1314d-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="1314d-104">[Заметки о](../release-notes/nuget-2.8.3.md)  |  выпуске 2.8.3 NuGet [Заметки о выпуске 2.8.6 NuGet](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="1314d-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="1314d-105">2.8.5 NuGet выпущен 30 марта 2015 г.</span><span class="sxs-lookup"><span data-stu-id="1314d-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="1314d-106">Это незначительное обновление нашего 2.8.3 VSIX с некоторыми целевыми исправлениями.</span><span class="sxs-lookup"><span data-stu-id="1314d-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="1314d-107">В этом выпуске для [моникеров целевой платформы DNX](https://github.com/aspnet/dnx)было добавлено диалоговое окно поддержка диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="1314d-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="1314d-108">Эти новые моникеры платформы, которые поддерживаются, включают:</span><span class="sxs-lookup"><span data-stu-id="1314d-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="1314d-109">**core50** — моникер целевой платформы "Base" (TFM), совместимый с базовой средой CLR.</span><span class="sxs-lookup"><span data-stu-id="1314d-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="1314d-110">**dnx452** — TFM, относящийся к приложениям на основе DNX с использованием полной версии платформы 4.5.2.</span><span class="sxs-lookup"><span data-stu-id="1314d-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="1314d-111">**dnx46** — TFM, относящийся к приложениям на основе DNX с использованием полной версии 4,6 платформы.</span><span class="sxs-lookup"><span data-stu-id="1314d-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="1314d-112">**dnxcore50** — TFM, относящийся к приложениям на основе DNX с использованием основной версии 5,0 платформы.</span><span class="sxs-lookup"><span data-stu-id="1314d-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="1314d-113">Была исправлена одна ошибка, препятствующая правильной установке пакетов в проекты FSharp:</span><span class="sxs-lookup"><span data-stu-id="1314d-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400