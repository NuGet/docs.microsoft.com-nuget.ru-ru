---
title: "Команда help NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 780d7f52-d6c6-45cd-8a62-218ff8c0b270
description: "Справочник по командам справки nuget.exe"
keywords: "Справка NuGet, команда «Справка»"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 55dc263fedd7ed5a3e48b76dbc9a3ccc220655cf
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="help-or--command-nuget-cli"></a>Справка или? команда (NuGet CLI)

**Применяется к:** все &bullet; **поддерживаемые версии**: все

Отображаются общие справочные сведения и справочные сведения о конкретных команд.

## <a name="usage"></a>Использование

```
nuget help [command] [options]
nuget ? [command] [options]
```

где [команда] определяет той или иной команды для отображения справки.

> [!Warning]
> Для некоторых команд, следует учитывать для указания *справки* во-первых, как с `nuget help install`, так как пакет с именем «Справка» на nuget.org. Если вы предоставляете команде `nuget install help`, вы не сможете получить справку в команду установки, но установит пакет с именем справки.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Все | Печать подробная справка для всех доступных команд; игнорируется, если задан той или иной команды. |
| ConfigFile | *(2.5 +)*  NuGet файла конфигурации для применения. Если не указан, *%AppData%\NuGet\NuGet.Config* используется. |
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Справка | Отображает справку для саму команду справки. |
| Markdown | Печать подробной справки в формате markdown при использовании с `-All`. В противном случае значение не обрабатывается. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
