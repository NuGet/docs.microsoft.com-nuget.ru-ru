---
title: Команда help NuGet CLI
description: Справочник по командам справки nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: dbfc803e24c824d30e128d6e86cfa3c43660668f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="help-or--command-nuget-cli"></a>help or ? Команда (NuGet CLI)

**Применяется к:** все &bullet; **поддерживаемые версии**: все

Отображаются общие справочные сведения и справочные сведения о конкретных команд.

## <a name="usage"></a>Использование

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

где [команда] определяет той или иной команды для отображения справки.

> [!Warning]
> Для некоторых команд, следует учитывать для указания *справки* во-первых, как с `nuget help install`, так как пакет с именем «Справка» на nuget.org. Если вы предоставляете команде `nuget install help`, не сможете получить справку в команду установки, а установит пакет с именем справки.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Все | Печать подробная справка для всех доступных команд; игнорируется, если задан той или иной команды. |
| ConfigFile | Файл конфигурации NuGet вступили в силу. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).|
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Справка | Отображает справку для саму команду справки. |
| Markdown | Печать подробной справки в формате markdown при использовании с `-All`. В противном случае значение не обрабатывается. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
