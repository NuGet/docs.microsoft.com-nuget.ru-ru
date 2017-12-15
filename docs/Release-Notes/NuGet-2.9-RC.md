---
title: "Заметки о выпуске 2.9 RC NuGet | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 04d76a22-63b0-41d1-9c27-799f4b35058f
description: "Заметки о выпуске для RC 2.9 NuGet, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "Версия-Кандидат 2.9 NuGet заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 64b4cd17394ddb902c7101b9117039f381dc8488
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-29-rc-release-notes"></a>Заметки о выпуске 2.9 RC NuGet

[Заметки о выпуске NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 заметки о выпуске предварительной версии](../release-notes/nuget-3.0-preview.md)

NuGet 2.9 было выпущено 10 сентября 2015 г. обновление 2.8.7 VSIX для Visual Studio 2012 и 2013.

### <a name="updates-in-this-release"></a>Обновления в этом выпуске

* Теперь пропуск обработки пакетов, если их автономной `.nuspec` документ имеет неправильный формат - [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Исправлена обработка multipartwebrequest \r\n для Unix/Linux сценариев - [776](https://github.com/NuGet/Home/issues/776)
* Исправлена интеграция с события построения в Visual Studio 2013 Community edition — [1180](https://github.com/NuGet/Home/issues/1180)


Полный список исправлений в этом выпуске можно найти на GitHub в [2.8.8 вехи](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
