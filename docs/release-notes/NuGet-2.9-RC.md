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
# <a name="nuget-29-rc-release-notes"></a>NuGet 2,9 — заметки о выпуске RC

[Заметки о](../release-notes/nuget-2.8.7.md)  |  выпуске 2.8.7 NuGet [Заметки о выпуске NuGet 3,0 Preview](../release-notes/nuget-3.0-preview.md)

Версия NuGet 2,9 была выпущена 10 сентября 2015 в качестве обновления для 2.8.7 VSIX для Visual Studio 2012 и 2013.

### <a name="updates-in-this-release"></a>Обновления в этом выпуске

* Пропускается обработка пакетов, если содержащиеся в них `.nuspec` документы имеют неправильный формат — [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Исправлена обработка мултипартвебрекуест для сценариев \r\n для UNIX/Linux — [776](https://github.com/NuGet/Home/issues/776)
* Исправлена интеграция с событиями сборки в Visual Studio 2013 Community Edition — [1180](https://github.com/NuGet/Home/issues/1180)


Полный список исправлений в этом выпуске можно найти на сайте GitHub в [2.8.8 вехе](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed) .
