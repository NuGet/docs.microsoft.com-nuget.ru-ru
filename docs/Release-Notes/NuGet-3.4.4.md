---
title: "Заметки о выпуске NuGet 3.4.4 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске для NuGet 3.4.4, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 3.4.4 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fabc10ae5c8e0bd43581f85c7763eb23e9483aaf
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-344-release-notes"></a>Заметки о выпуске NuGet 3.4.4

[Заметки о выпуске NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [заметки о выпуске 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md)

Основная цель данного выпуска — это улучшение с качеством 3.4.3 версии nuget.exe несколько исправлений в расширение Visual Studio.

Можно загрузить VSIX и nuget.exe [здесь](https://dist.nuget.org/index.html).

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Полный журнал изменений](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Список проблем](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Изменения

- Улучшения в пакет усовершенствования упаковкой символов, упаковки с `project.json` и дополнительные [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- Отображение исключений при сбое, поиск проектов в команде обновления [\#605] (https://github.com/NuGet/NuGet.Client/pull/605
- Чтение входных данных типа пакета `.nuspec` и `project.json` при упаковки [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- Сделайте NuGet.Shared не отдельного проекта. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Использование времени ожидания принудительной как время ожидания ответа HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- Файлы пакета со временем в будущем не будет их использовать времени [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- Обновление `NuGet.Core.dll` версии 2.12.0 устранению XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- Поддерживает./NuGet.CommandLine.XPlat - v \<детализации\> \<режим\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- Ошибка отображения при восстановлении без `project.json` или `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- Исправления версии зависимостей, когда требуемые версии отличаются [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)