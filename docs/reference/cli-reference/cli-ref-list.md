---
title: Команда списка CLI NuGet
description: Справочник по команде nuget.exe List
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a6a4ee434c43ad4865dba12f039b5d545a90d3c4
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238170"
---
# <a name="list-command-nuget-cli"></a>Команда list (интерфейс командной строки NuGet)

Область **применения:** использование пакетов, публикация &bullet; **поддерживаемых версий:** все

Отображает список пакетов из заданного источника. Если источники не указаны, используются все источники, определенные в глобальном файле конфигурации `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` . Если `NuGet.Config` не указывает источники, `list` использует канал по умолчанию (NuGet.org).

## <a name="usage"></a>Использование

```cli
nuget list [search terms] [options]
```

где необязательные условия поиска будут фильтровать отображаемый список. [Условия поиска](../../consume-packages/finding-and-choosing-packages.md#search-syntax) применяются к именам пакетов, тегов и описаний пакетов так же, как и при их использовании в NuGet.org. 

## <a name="options"></a>Параметры

- **`-AllVersions`**

  Вывод списка всех версий пакета. По умолчанию отображается только последняя версия пакета.

- **`-ConfigFile`**

  Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.

- **`-?|-help`**

  Отображает справочные сведения для команды.

- **`-IncludeDelisted`**

  *(3.2 +)* Отображение пакетов, которые не были перечислены.

- **`-NonInteractive`**

  Подавляет запросы на ввод или подтверждение пользователя.

- **`-PreRelease`**

  Включает в список предварительные пакеты.

- **`-Source`**

  Указывает список источников пакетов для поиска.

- **`-Verbosity [normal|quiet|detailed]`**

  Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .

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