---
title: Команда NuGet CLI init
description: Справочник по команде NuGet. exe init
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327781"
---
# <a name="init-command-nuget-cli"></a>команда init (интерфейс командной строки NuGet)

Область **применения:** &bullet; **Поддерживаемые версии** для создания пакетов: 3.3+

Копирует все пакеты из неструктурированной папки в конечную папку с помощью иерархического макета, как описано в [команде Add](cli-ref-add.md). То есть использование `init` эквивалентно `add` использованию команды для каждого пакета в папке.

Как и в случае, назначение должно быть локальной папкой или UNC-путем. `add` Репозитории пакетов HTTP, такие как nuget.org или частные серверы, не поддерживаются.

## <a name="usage"></a>Использование

```cli
nuget init <source> <destination> [options]
```

где `<source>` — это папка, содержащая пакеты `<destination>` , а — локальная папка или путь в формате UNC, в который копируются пакеты.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ConfigFile | Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).|
| форцеенглишаутпут | *(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке. |
| Expand | Добавляет все файлы в каждом пакете, который добавляется в источник пакета; то же `-Expand` , что `add` и команда. |
| Help | Отображает справочные сведения для команды. |
| NonInteractive | Подавляет запросы на ввод или подтверждение пользователя. |
| Verbosity | Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
