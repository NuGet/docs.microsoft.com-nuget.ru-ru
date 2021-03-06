---
title: Команда интерфейса командной строки NuGet
description: Справочник по команде nuget.exe Add
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 096d2f7a61a3c861ce2084368500ab8e8b21f212
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776093"
---
# <a name="add-command-nuget-cli"></a>Команда "Добавить" (интерфейс командной строки NuGet)

Область **применения**: &bullet; **Поддерживаемые версии** публикации пакетов: 3.3 +

Добавляет указанный пакет в источник пакета, отличный от HTTP (путь к папке или UNC-пути) в иерархическом макете, где папки создаются для идентификатора пакета и номера версии. Пример:

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

При восстановлении или обновлении источника пакета иерархическая структура обеспечивает значительно большую производительность.

Чтобы развернуть все файлы в пакете в источнике целевого пакета, используйте `-Expand` параметр. Это обычно приводит к появлению дополнительных вложенных папок в месте назначения, таких как `tools` и `lib` .

## <a name="usage"></a>Использование

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

где `<packagePath>` — это путь к добавляемому пакету, и `<sourcePath>` указывает источник пакета на основе папки, в который будет добавлен пакет. Источники HTTP не поддерживаются.

## <a name="options"></a>Варианты

- **`-ConfigFile`**

  Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-Expand`**

  Добавляет все файлы пакета в источник пакета.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.
Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.

- **`-?|-help`**

  Отображает справочные сведения для команды.

- **`-NonInteractive`**

  Подавляет запросы на ввод или подтверждение пользователя.

- **`-src|-Source`**

   Указывает источник пакета, который представляет собой папку или общий UNC-ресурс, к которому будет добавлен nupkg. Источники HTTP не поддерживаются.

- **`-Verbosity [normal|quiet|detailed]`**

  Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
