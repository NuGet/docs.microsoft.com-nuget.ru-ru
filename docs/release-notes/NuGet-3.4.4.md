---
title: Заметки о выпуске NuGet 3.4.4
description: Заметки о выпуске для NuGet 3.4.4, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547477"
---
# <a name="nuget-344-release-notes"></a>Заметки о выпуске NuGet 3.4.4

[Заметки о выпуске NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [заметки о выпуске бета-версии 3.5 NuGet](../release-notes/nuget-3.5-Beta.md)

Основная цель этой версии — это улучшение с качеством 3.4.3 версию nuget.exe с несколько исправлений в расширение Visual Studio.

Можно загрузить VSIX и nuget.exe [здесь](https://dist.nuget.org/index.html).

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Полный журнал изменений](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Список проблем](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Изменения

- Улучшения в пакете: Усовершенствования упаковка символов, упаковки с `project.json` и дополнительные [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- Отображение исключений при сбое, поиск проектов в команде обновления [\#605](https://github.com/NuGet/NuGet.Client/pull/605)
- Чтение входных данных в тип пакета `.nuspec` и `project.json` при упаковке [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- Сделайте NuGet.Shared не отдельного проекта. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Используйте время ожидания Push-уведомлений как время ожидания ответа HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- Файлы пакета с будущих периодов не будет использовать для них времени [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- Обновление `NuGet.Core.dll` версии 2.12.0, чтобы устранить проблему XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- Поддерживает./NuGet.CommandLine.XPlat - v \<детализации\> \<режим\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- Ошибка отображения при восстановлении без `project.json` или `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- Исправление версии зависимостей, если необходимые версии отличаются [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)