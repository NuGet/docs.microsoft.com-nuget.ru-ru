---
title: Заметки о выпуске NuGet 3.4.4
description: Заметки о выпуске для NuGet 3.4.4, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 891d5c7ee884d31f405118739b57a169b9cd93b3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820871"
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
- Отображение исключений при сбое, поиск проектов в команде обновления [\#605] ()https://github.com/NuGet/NuGet.Client/pull/605
- Чтение входных данных типа пакета `.nuspec` и `project.json` при упаковки [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- Сделайте NuGet.Shared не отдельного проекта. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Использование времени ожидания принудительной как время ожидания ответа HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- Файлы пакета со временем в будущем не будет их использовать времени [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- Обновление `NuGet.Core.dll` версии 2.12.0 устранению XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- Поддерживает./NuGet.CommandLine.XPlat - v \<детализации\> \<режим\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- Ошибка отображения при восстановлении без `project.json` или `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- Исправления версии зависимостей, когда требуемые версии отличаются [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)