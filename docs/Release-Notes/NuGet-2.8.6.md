---
title: "Заметки о выпуске NuGet 2.8.6 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 920c551c-18a7-40f4-a32b-ce84de6ea766
description: "Заметки о выпуске для NuGet 2.8.6, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 2.8.6 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4dfd0a76967280cc6a16b37fe2b2a3362231fce5
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
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