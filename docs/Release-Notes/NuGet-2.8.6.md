---
title: Заметки о выпуске NuGet 2.8.6
description: Заметки о выпуске для NuGet 2.8.6, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ee801a0edfe22888d65506cea557fd9c79dcf7bd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-286-release-notes"></a>Заметки о выпуске NuGet 2.8.6

[Заметки о выпуске NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 заметки о выпуске](../release-notes/nuget-2.8.7.md)

NuGet 2.8.6 был выпущен 20 июля 2015 г. как незначительное обновление для наших 2.8.5 VSIX с некоторыми целевой исправления и улучшения для поддержки пакетов, которые могут доставляться с поддержкой модели разработки Windows 10 UWP.

Эта версия расширения диспетчера пакетов NuGet обеспечивает поддержку только для Visual Studio 2013.

В этом выпуске диспетчер пакетов NuGet диалогового окна имел добавлена поддержка для:

* Появился UAP моникер целевой платформы для разработки приложений Windows 10.
* Протокол NuGet версии 3-конечные точки
* Поддержка [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion атрибут источникам репозиториев. Значение по умолчанию — «2»
* Будет использоваться предыдущий удаленный репозиторий, если версия требуемый пакет недоступен в локальном кэше