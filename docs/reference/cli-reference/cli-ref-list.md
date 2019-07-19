---
title: Команда списка CLI NuGet
description: Справочник по команде NuGet. exe List
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327741"
---
# <a name="list-command-nuget-cli"></a>Команда list (интерфейс командной строки NuGet)

Область **применения:** использование пакетов, публикация &bullet; **поддерживаемых версий:** все

Отображает список пакетов из заданного источника. Если источники не указаны, используются все источники, определенные в глобальном файле `%AppData%\NuGet\NuGet.Config` конфигурации (Windows) или. `~/.nuget/NuGet/NuGet.Config` Если `NuGet.Config` не указывает источники `list` , использует канал по умолчанию (NuGet.org).

## <a name="usage"></a>Использование

```cli
nuget list [search terms] [options]
```

где необязательные условия поиска будут фильтровать отображаемый список. Условия поиска применяются к именам пакетов, тегов и описаний пакетов так же, как и при их использовании в nuget.org.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| AllVersions | Вывод списка всех версий пакета. По умолчанию отображается только последняя версия пакета. |
| ConfigFile | Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).|
| форцеенглишаутпут | *(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке. |
| Help | Отображает справочные сведения для команды. |
| инклудеделистед | *(3.2 +)* Отображение пакетов, которые не были перечислены. |
| NonInteractive | Подавляет запросы на ввод или подтверждение пользователя. |
| Предварительной | Включает в список предварительные пакеты. |
| Source | Указывает список источников пакетов для поиска. |
| Verbosity | Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
