---
title: Интерфейс командной строки NuGet добавьте команду
description: Справочник по nuget.exe добавьте команду
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545838"
---
# <a name="add-command-nuget-cli"></a>Команда add (NuGet CLI)

**Применяется к**: Упаковка публикации &bullet; **поддерживаемые версии**: 3.3 +

Добавляет указанный пакет источник пакетов, отличные от HTTP (папка или UNC-путь) в виде иерархического представления, при котором создаются папки, для номера идентификатора и версии пакета. Пример:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

При восстановлении или обновлении в источнике пакета, иерархического представления обеспечивает значительно более высокую производительность.

Чтобы развернуть все файлы в пакете к источнику пакета назначения, используйте `-Expand` переключения. Это обычно приводит появление в месте назначения, такие как дополнительные подпапки `tools` и `lib`.

## <a name="usage"></a>Использование

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

где `<packagePath>` — это путь к пакету, чтобы добавить, и `<sourcePath>` указывает источник пакетов на основе папки, в которую будут добавлены пакета. HTTP-источники не поддерживаются.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ConfigFile | Чтобы применить файл конфигурации NuGet. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).|
| Expand | Добавляет все файлы в пакете к источнику пакета. |
| ForceEnglishOutput | *(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры. |
| Справка | Отображает справку для команды. |
| Неинтерактивная | Подавление для пользователя данные или подтверждения. |
| Уровень детализации | Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*. |

Также см. в разделе [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
