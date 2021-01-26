---
title: Заметки о выпуске 3.4.4 NuGet
description: Заметки о выпуске NuGet 3.4.4, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780232"
---
# <a name="nuget-344-release-notes"></a>Заметки о выпуске 3.4.4 NuGet

[Заметки о](../release-notes/nuget-3.4.3.md)  |  выпуске 3.4.3 NuGet [NuGet 3,5 — заметки о выпуске бета-версии](../release-notes/nuget-3.5-Beta.md)

Основное внимание в этом выпуске было улучшение качества 3.4.3 версии nuget.exe с помощью нескольких исправлений для расширения Visual Studio.

Вы можете скачать VSIX и nuget.exe [здесь](https://dist.nuget.org/index.html).

## <a name="344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Полный журнал изменений](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Список проблем](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Изменения

- Улучшения в пакетах: улучшения упаковки символов, упаковка с `project.json` и более [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606)
- Отображать исключение при сбое поиска проектов в команде Update [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605
- Считывание типа пакета из входных данных `.nuspec` и `project.json` при упаковке [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)
- Сделайте NuGet. Shared не проектом. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Использовать время ожидания отправки для HTTP-ответа [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599)
- Файлы пакета со временем не будут использоваться в будущем [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)
- Обновление `NuGet.Core.dll` версии до 2.12.0 для исправления ошибки XML [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)
- Поддержка./нужет.коммандлине.ксплат-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)
- Отображать ошибку при восстановлении без `project.json` или `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590)
- Исправление версий зависимостей, если требуемые версии отличаются [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)