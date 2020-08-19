---
title: Команда NuGet CLI init
description: Справочник по команде nuget.exe init
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3b830d678a473c917b70bd46900bdb0206d3652e
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623088"
---
# <a name="init-command-nuget-cli"></a>команда init (интерфейс командной строки NuGet)

Область **применения:** &bullet; **Поддерживаемые версии** для создания пакетов: 3.3 +

Копирует все пакеты из неструктурированной папки в конечную папку с помощью иерархического макета, как описано в [команде Add](cli-ref-add.md). То есть использование `init` эквивалентно использованию `add` команды для каждого пакета в папке.

Как и в `add` случае, назначение должно быть локальной папкой или UNC-путем. Репозитории пакетов HTTP, такие как nuget.org или частные серверы, не поддерживаются.

## <a name="usage"></a>Использование

```cli
nuget init <source> <destination> [options]
```

где `<source>` — это папка, содержащая пакеты, а `<destination>` — Локальная папка или путь в формате UNC, в который копируются пакеты.

## <a name="options"></a>Параметры

- **`-ConfigFile`**

  Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-Expand`**

  Добавляет все файлы в каждом пакете, который добавляется в источник пакета; то же, что и `-Expand` `add` команда.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.

- **`-?|-help`**

  Отображает справочные сведения для команды.

- **`-NonInteractive`**

  Подавляет запросы на ввод или подтверждение пользователя.

- **`-Verbosity [normal|quiet|detailed]`**

  Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
