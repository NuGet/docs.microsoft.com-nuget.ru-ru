---
title: Команда списка CLI NuGet
description: Справочник по команде NuGet. exe List
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813342"
---
# <a name="list-command-nuget-cli"></a>Команда list (интерфейс командной строки NuGet)

Область **применения:** использование пакетов, публикация &bullet; **Поддерживаемые версии:** все

Отображает список пакетов из заданного источника. Если источники не указаны, используются все источники, определенные в глобальном файле конфигурации `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config`. Если `NuGet.Config` не указывает источники, `list` использует канал по умолчанию (nuget.org).

## <a name="usage"></a>Метрики

```cli
nuget list [search terms] [options]
```

где необязательные условия поиска будут фильтровать отображаемый список. Условия поиска применяются к именам пакетов, тегов и описаний пакетов так же, как и при их использовании в nuget.org.

## <a name="options"></a>Options

| Параметр | Описание |
| --- | --- |
| AllVersions | Вывод списка всех версий пакета. По умолчанию отображается только последняя версия пакета. |
| ConfigFile | Файл конфигурации NuGet, который необходимо применить. Если не указано, используется `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке. |
| Справка | Отображает справочные сведения для команды. |
| IncludeDelisted | *(3.2 +)* Отображение пакетов, которые не были перечислены. |
| NonInteractive | Подавляет запросы на ввод или подтверждение пользователя. |
| PreRelease | Включает в список предварительные пакеты. |
| Source | Указывает список источников пакетов для поиска. |
| Уровень детализации | Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

Список всех пакетов из настроенных веб-каналов:
```
nuget list
```
Перечисление пакетов, связанных с Azure, с подробным уровнем детализации:
```
nuget list Azure -Verbosity detailed
```
Вывод списка всех версий пакетов, связанных с Azure, из настроенных веб-каналов:
```
nuget list Azure -AllVersions
```
Вывод списка всех версий пакетов, связанных с JSON, из указанного источника или веб-канала:
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
Список пакетов, связанных с JSON, из нескольких источников и веб-каналов:
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

