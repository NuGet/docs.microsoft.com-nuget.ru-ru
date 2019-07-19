---
title: Команда интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe Add
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327861"
---
# <a name="add-command-nuget-cli"></a>Команда add (NuGet CLI)

Область применения: **Поддерживаемые версии** **для**публикации &bullet; пакетов: 3.3+

Добавляет указанный пакет в источник пакета, отличный от HTTP (путь к папке или UNC-пути) в иерархическом макете, где папки создаются для идентификатора пакета и номера версии. Например:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

При восстановлении или обновлении источника пакета иерархическая структура обеспечивает значительно большую производительность.

Чтобы развернуть все файлы в пакете в источнике целевого пакета, используйте `-Expand` параметр. Это обычно приводит к появлению дополнительных вложенных папок в месте назначения, таких `tools` как `lib`и.

## <a name="usage"></a>Использование

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

где `<packagePath>` — это путь к добавляемому пакету, и `<sourcePath>` указывает источник пакета на основе папки, в который будет добавлен пакет. Источники HTTP не поддерживаются.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ConfigFile | Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).|
| Expand | Добавляет все файлы пакета в источник пакета. |
| форцеенглишаутпут | *(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке. |
| Help | Отображает справочные сведения для команды. |
| NonInteractive | Подавляет запросы на ввод или подтверждение пользователя. |
| Verbosity | Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
