---
title: "Заметки о выпуске NuGet 2.8.5 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске для NuGet 2.8.5, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 2.8.5 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ace56284e56f24394d49c0598ec3604b62caaf67
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
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