---
title: Заметки о выпуске NuGet 2.8.6
description: Заметки о выпуске для NuGet 2.8.6, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546495"
---
# <a name="nuget-286-release-notes"></a>Заметки о выпуске NuGet 2.8.6

[Заметки о выпуске NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [заметки о выпуске NuGet 2.8.7](../release-notes/nuget-2.8.7.md)

NuGet 2.8.6 был выпущен 20 июля 2015 г. как незначительное обновление для наших 2.8.5 VSIX с некоторыми целевые исправления и улучшения для поддержки пакетов, которые затем могут доставляться с поддержкой модели разработки Windows 10 UWP.

Эта версия расширения диспетчера пакетов NuGet обеспечивает поддержку только для Visual Studio 2013.

В этом выпуске диалоговое окно диспетчера пакетов NuGet была добавлена поддержка для:

* Появился UAP моникер целевой платформы для поддержки разработки приложений для Windows 10.
* Конечные точки для версии 3 протокола NuGet
* Поддержка [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion атрибут источники репозиториев. Значение по умолчанию — «2»
* Откат к удаленному репозиторию Если необходимый пакет версия недоступна в локальном кэше