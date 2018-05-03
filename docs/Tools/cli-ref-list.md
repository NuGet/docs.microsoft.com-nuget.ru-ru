---
title: Команда list NuGet CLI
description: Справочник по команду nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4a44c70937e7cb49e472c53e9857e9f44d269f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="list-command-nuget-cli"></a>Команда List (NuGet CLI)

**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все

Отображает список пакетов из данного источника. Если не указан ни один из источников, все источники, определенные в файле Глобальная конфигурация `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config`, используются. Если `NuGet.Config` указывает нет источников, затем `list` использует стандартный канал (nuget.org).

## <a name="usage"></a>Использование

```cli
nuget list [search terms] [options]
```

где отображается список будет отфильтрован условия поиска необязательно. Условия поиска, применяются к имена пакетов, теги и описание пакета, так же как при использовании их в nuget.org.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| AllVersions | Вывести все версии пакета. По умолчанию отображается только последняя версия пакета. |
| ConfigFile | Файл конфигурации NuGet вступили в силу. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).|
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

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
