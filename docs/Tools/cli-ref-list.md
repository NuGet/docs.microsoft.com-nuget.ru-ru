---
title: "Команда list NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Справочник по команду nuget.exe"
keywords: "Справочник по список NuGet, команда список пакетов"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5a1f68aaffd26a0f903aa3a7a4a450a0121191c3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2018
---
# <a name="list-command-nuget-cli"></a>Команда List (NuGet CLI)

**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все

Отображает список пакетов из данного источника. Если не указан ни один из источников, все источники, определенные в файле Глобальная конфигурация `%AppData%\NuGet\NuGet.Config`, используются. Если `NuGet.Config` указывает нет источников, затем `list` использует стандартный канал (nuget.org).

## <a name="usage"></a>Использование

```cli
nuget list [search terms] [options]
```

где отображается список будет отфильтрован условия поиска необязательно. Условия поиска применяются к имена пакетов, теги и описание пакета.

## <a name="options"></a>Параметры

| Параметр | Описание: |
| --- | --- |
| AllVersions | Вывести все версии пакета. По умолчанию отображается только последняя версия пакета. |
| ConfigFile | Файл конфигурации NuGet вступили в силу. Если не указан, *%AppData%\NuGet\NuGet.Config* используется. |
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Справка | Отображает справку по команде. |
| IncludeDelisted | *(3.2 +)*  Отображение отсутствующие в списке пакетов. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Предварительный выпуск | Содержит предварительные версии пакетов в списке. |
| Исходный код | Указывает список источников пакетов для поиска. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget list

nuget list -Verbosity detailed -AllVersions
```
