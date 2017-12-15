---
title: "Команда list NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: "Справочник по команду nuget.exe"
keywords: "Справочник по список NuGet, команда список пакетов"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a>Команда List (NuGet CLI)

**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все

Отображает список пакетов из данного источника. Если не указан ни один из источников, все источники, определенные в файле Глобальная конфигурация `%AppData%\NuGet\NuGet.Config`, используются. Если `NuGet.Config` указывает нет источников, затем `list` использует стандартный канал (nuget.org).

## <a name="usage"></a>Использование

```
nuget list [search terms] [options]
```

где отображается список будет отфильтрован условия поиска необязательно. Условия поиска применяются к имена пакетов, теги и описание пакета.

## <a name="options"></a>Параметры
| Параметр | Описание |
| --- | --- |
| AllVersions | Вывести все версии пакета. По умолчанию отображается только последняя версия пакета. |
| ConfigFile | *(2.5 +)*  NuGet файла конфигурации для применения. Если не указан, *%AppData%\NuGet\NuGet.Config* используется. |
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Справка | Отображает справку по команде. |
| IncludeDelisted | *(3.2 +)*  Отображение отсутствующие в списке пакетов. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Предварительный выпуск | Содержит предварительные версии пакетов в списке. |
| Исходный код | Указывает список источников пакетов для поиска. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
