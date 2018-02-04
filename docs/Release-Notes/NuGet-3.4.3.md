---
title: "Заметки о выпуске NuGet 3.4.3 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске для NuGet 3.4.3, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 3.4.3 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 68aab607659d15f96aefeab7bb90afc787710824
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-343-release-notes"></a>Заметки о выпуске NuGet 3.4.3

[Заметки о выпуске NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 заметки о выпуске](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 был выпущен 22 апреля 2016 г. Чтобы решить некоторые проблемы, которые были определены в 3,4 и последующих выпусках.

Можно загрузить VSIX и nuget.exe [здесь](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Обновления и улучшения

* Повышенная надежность Visual Studio. Мы исправили некоторые проблемы в NuGet, причиной сбоев в Visual Studio.

## <a name="fixes"></a>Исправления

* Исправлены некоторые проблемы авторизации с частной nuget защищенные паролем веб-каналов.
* Устранена проблема вокруг не удается восстановить PCL элемента из `project.json` в указанный средах выполнения.
* Некоторые клиенты были запущены в временные сбои при установке пакетов. Теперь эта проблема была исправлена в этом выпуске.
* Устранена проблема, вызвавшая восстановления сбоев в C + +/ CLI проекты с `project.json`.
* Некоторые пакеты (например ModernHttpClient) где не распаковал правильно при использовании nuget в моно. Теперь эта проблема была исправлена в этом выпуске.

Полный список исправлений и улучшений данного выпуска, см. список проблем [здесь](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).