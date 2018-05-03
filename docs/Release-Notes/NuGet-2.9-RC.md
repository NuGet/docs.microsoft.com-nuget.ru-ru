---
title: Заметки о выпуске 2.9 RC NuGet
description: Заметки о выпуске для RC 2.9 NuGet, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 15665e7c3f9f638b434b0d7be2f7ff3215c787c6
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="28c3a-103">Заметки о выпуске 2.9 RC NuGet</span><span class="sxs-lookup"><span data-stu-id="28c3a-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="28c3a-104">[Заметки о выпуске NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 заметки о выпуске предварительной версии](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="28c3a-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="28c3a-105">NuGet 2.9 было выпущено 10 сентября 2015 г. обновление 2.8.7 VSIX для Visual Studio 2012 и 2013.</span><span class="sxs-lookup"><span data-stu-id="28c3a-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="28c3a-106">Обновления в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="28c3a-106">Updates in this release</span></span>

* <span data-ttu-id="28c3a-107">Теперь пропуск обработки пакетов, если их автономной `.nuspec` документ имеет неправильный формат - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="28c3a-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="28c3a-108">Исправлена обработка multipartwebrequest \r\n для Unix/Linux сценариев - [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="28c3a-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="28c3a-109">Исправлена интеграция с события построения в Visual Studio 2013 Community edition — [1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="28c3a-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="28c3a-110">Полный список исправлений в этом выпуске можно найти на GitHub в [2.8.8 вехи](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="28c3a-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
