---
title: Команда init NuGet CLI
description: Справочник по команде init nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4fda33aabd51fbbf0e5559baaa42af065366ba4
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817822"
---
# <a name="init-command-nuget-cli"></a>команда init (NuGet CLI)

**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** 3.3 +

Копирует все пакеты из папки на жестком диске в папку назначения с помощью иерархическом виде, как описано для [добавьте команду](cli-ref-add.md). То есть с использованием `init` эквивалентно использованию `add` на каждый пакет в папке.

Как и в `add`, то следует локальную папку или UNC-путь; HTTP пакета репозиториев, таких как nuget.org или закрытый серверы не поддерживаются.

## <a name="usage"></a>Использование

```cli
nuget init <source> <destination> [options]
```

где `<source>` — папка, содержащая пакеты и `<destination>` локальная папка или путь UNC, в который копируются пакеты.

## <a name="options"></a>Параметры

| Параметр | Описание: |
| --- | --- |
| ConfigFile | Файл конфигурации NuGet вступили в силу. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).|
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Expand | Добавляет все файлы в каждом пакете, который добавляется к источнику пакета; то же, что `-Expand` с `add` команды. |
| Справка | Отображает справку по команде. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
