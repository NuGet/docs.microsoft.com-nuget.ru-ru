---
title: Заметки о выпуске 2.8.6 NuGet
description: Заметки о выпуске NuGet 2.8.6, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776706"
---
# <a name="nuget-286-release-notes"></a>Заметки о выпуске 2.8.6 NuGet

[Заметки о](../release-notes/nuget-2.8.5.md)  |  выпуске 2.8.5 NuGet [Заметки о выпуске 2.8.7 NuGet](../release-notes/nuget-2.8.7.md)

2.8.6 NuGet была выпущена 20 июля 2015 в качестве дополнительного обновления для нашего 2.8.5 VSIX с некоторыми целевыми исправлениями и улучшениями для поддержки пакетов, которые могут доставляться с поддержкой модели разработки Windows 10 UWP.

Эта версия расширения диспетчера пакетов NuGet обеспечивает поддержку только для Visual Studio 2013.

В этом выпуске в диалоговом окне диспетчера пакетов NuGet добавлена поддержка:

* Введен моникер целевой платформы UAP для поддержки разработки приложений Windows 10.
* Конечные точки протокола NuGet версии 3
* Поддержка атрибута [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) протоколверсион в источниках репозитория. Значение по умолчанию — 2.
* Возврат к удаленному репозиторию, если требуемая версия пакета недоступна в локальном кэше