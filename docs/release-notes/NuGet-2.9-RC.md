---
title: NuGet 2,9 — заметки о выпуске RC
description: Заметки о выпуске для версии-КАНДИДАТа NuGet 2,9, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b9d32f09fae7e12f81cf92b5b6e6b36c71d55f26
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780322"
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="72800-103">NuGet 2,9 — заметки о выпуске RC</span><span class="sxs-lookup"><span data-stu-id="72800-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="72800-104">[Заметки о](../release-notes/nuget-2.8.7.md)  |  выпуске 2.8.7 NuGet [Заметки о выпуске NuGet 3,0 Preview](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="72800-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="72800-105">Версия NuGet 2,9 была выпущена 10 сентября 2015 в качестве обновления для 2.8.7 VSIX для Visual Studio 2012 и 2013.</span><span class="sxs-lookup"><span data-stu-id="72800-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="72800-106">Обновления в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="72800-106">Updates in this release</span></span>

* <span data-ttu-id="72800-107">Пропускается обработка пакетов, если содержащиеся в них `.nuspec` документы имеют неправильный формат — [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="72800-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="72800-108">Исправлена обработка мултипартвебрекуест для сценариев \r\n для UNIX/Linux — [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="72800-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="72800-109">Исправлена интеграция с событиями сборки в Visual Studio 2013 Community Edition — [1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="72800-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="72800-110">Полный список исправлений в этом выпуске можно найти на сайте GitHub в [2.8.8 вехе](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed) .</span><span class="sxs-lookup"><span data-stu-id="72800-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
