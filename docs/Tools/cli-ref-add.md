---
title: "Команда add NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 4f68a016-ad4e-41fc-b869-88910fc5121e
description: "Справочник по nuget.exe Добавление команды"
keywords: "NuGet добавить ссылку, добавьте команду пакета"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bf9a6e51dfbf1716ba40273487b76ae04c18e948
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="add-command-nuget-cli"></a>Добавьте команду (NuGet CLI)

**Применяется к**: пакета публикации &bullet; **поддерживаемые версии**: 3.3 +

Добавляет источник пакетов не HTTP (папка или UNC-путь) в иерархическом виде, в которой будут созданы папки для пакета идентификатор и номер версии указанного пакета. Пример:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

При восстановлении или обновлении к источнику пакета, в иерархическом виде предоставляет значительно повысить производительность.

Чтобы развернуть все файлы в пакете в целевой источник пакета, используйте `-Expand` переключения. Это обычно приводит дополнительные вложенные папки отображаются в месте назначения, такие как `tools` и `lib`.

## <a name="usage"></a>Использование

```
nuget add <packagePath> -Source <sourcePath> [options]
```

где `<packagePath>` является путем к пакету, чтобы добавить, и `<sourcePath>` указывает источник пакета на основе папок, в которую будет добавляться пакета. Источники HTTP не поддерживаются.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ConfigFile | Файл конфигурации NuGet вступили в силу. Если не указан, *%AppData%\NuGet\NuGet.Config* используется.| 
| Expand | Добавляет все файлы в пакете источника пакета. |
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Справка | Отображает справку по команде. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
