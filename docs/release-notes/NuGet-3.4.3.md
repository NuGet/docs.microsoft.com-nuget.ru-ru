---
title: Заметки о выпуске 3.4.3 NuGet
description: Заметки о выпуске NuGet 3.4.3, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776475"
---
# <a name="nuget-343-release-notes"></a>Заметки о выпуске 3.4.3 NuGet

[Заметки о](../release-notes/nuget-3.4.2.md)  |  выпуске 3.4.2 NuGet [Заметки о выпуске 3.4.4 NuGet](../release-notes/nuget-3.4.4.md)

3.4.3 NuGet выпущен 22 апреля 2016 для устранения нескольких проблем, обнаруженных в 3,4 и последующих выпусках.

Вы можете скачать VSIX и nuget.exe [здесь](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Обновления и улучшения

* Улучшена надежность Visual Studio. Мы устранили некоторые проблемы в NuGet, которые привели к сбоям в работе Visual Studio.

## <a name="fixes"></a>Исправления

* Устранены некоторые проблемы с авторизацией защищенных паролем частных веб-каналов NuGet.
* Исправлена проблема с тем, что не удалось восстановить PCL из `project.json` с указанными средами выполнения.
* Некоторые клиенты выполняли временные сбои при установке пакетов. Этот выпуск исправлен в этом выпуске.
* Исправлена проблема, которая привела к сбоям восстановления в проектах C++/CLI с `project.json` .
* Некоторые пакеты (например, Модернхттпклиент), где не выполняется неправильное распаковка при использовании NuGet в Mono. Этот выпуск исправлен в этом выпуске.

Полный список исправлений и улучшений в этом выпуске см. [здесь](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).