---
title: Заметки о выпуске NuGet 2.9 RC выпуска
description: Заметки о выпуске для NuGet 2.9 RC, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 17c1c3a0c91928602aa47b5ba599faeac0424a4a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548328"
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="c2df7-103">Заметки о выпуске NuGet 2.9 RC выпуска</span><span class="sxs-lookup"><span data-stu-id="c2df7-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="c2df7-104">[Заметки о выпуске NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [заметки о выпуске предварительной версии NuGet 3.0](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="c2df7-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="c2df7-105">NuGet 2.9 был выпущен 10 сентября 2015 г., как обновление для 2.8.7 VSIX для Visual Studio 2012 и 2013.</span><span class="sxs-lookup"><span data-stu-id="c2df7-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="c2df7-106">Обновления в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="c2df7-106">Updates in this release</span></span>

* <span data-ttu-id="c2df7-107">Теперь пропуск обработки пакетов, если их автономной `.nuspec` документ имеет неправильный формат - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="c2df7-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="c2df7-108">Исправлена обработка multipartwebrequest \r\n для сценариев Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="c2df7-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="c2df7-109">Исправлена интеграция с события построения в Visual Studio 2013 Community edition — [1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="c2df7-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="c2df7-110">Полный список исправлений в этом выпуске можно найти на сайте GitHub в [2.8.8 вехи](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="c2df7-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
