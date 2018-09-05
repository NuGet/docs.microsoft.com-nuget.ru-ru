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
# <a name="nuget-29-rc-release-notes"></a>Заметки о выпуске NuGet 2.9 RC выпуска

[Заметки о выпуске NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [заметки о выпуске предварительной версии NuGet 3.0](../release-notes/nuget-3.0-preview.md)

NuGet 2.9 был выпущен 10 сентября 2015 г., как обновление для 2.8.7 VSIX для Visual Studio 2012 и 2013.

### <a name="updates-in-this-release"></a>Обновления в этом выпуске

* Теперь пропуск обработки пакетов, если их автономной `.nuspec` документ имеет неправильный формат - [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Исправлена обработка multipartwebrequest \r\n для сценариев Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)
* Исправлена интеграция с события построения в Visual Studio 2013 Community edition — [1180](https://github.com/NuGet/Home/issues/1180)


Полный список исправлений в этом выпуске можно найти на сайте GitHub в [2.8.8 вехи](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
