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
---
# <a name="nuget-285-release-notes"></a>Заметки о выпуске NuGet 2.8.5

[Заметки о выпуске NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 заметки о выпуске](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 был выпущен 30 марта 2015 г. Это незначительное обновление с нашей 2.8.3 VSIX с некоторыми целевых исправления.

В этом выпуске добавлена поддержка для диалогового окна диспетчера пакетов NuGet [DNX моникеров целевой платформы](https://github.com/aspnet/dnx).  Эти новые моникеров платформы, которые поддерживаются следующие.

* **core50** — «base» целевой framework моникером, совместимый с Core CLR.
* **dnx452** — TFM конкретных на основе DNX приложений с помощью полного 4.5.2 версия платформы
* **dnx46** — TFM конкретных на основе DNX приложений с помощью полного 4,6 версия платформы
* **dnxcore50** — TFM конкретных на основе DNX приложений с помощью версии Core 5.0 структуры

Один исправлена ошибка, предотвращено пакетов при установке в проектах FSharp должным образом:

https://nuget.codeplex.com/workitem/4400