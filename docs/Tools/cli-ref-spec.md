---
title: "Спецификация команду NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Справочник по спецификации команду nuget.exe"
keywords: "ссылка характеристик NuGet, команда характеристик"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc7e772e737a0f74929d13e2b126f7796b6d0dc7
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="spec-command-nuget-cli"></a>Команда характеристик (NuGet CLI)

**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** все

Приводит к возникновению ошибки `.nuspec` файла для нового пакета. Если выполняются в той же папке, что и файл проекта (`.csproj`, `.vbproj`, `.fsproj`), `spec` создает токенами `.nuspec` файла. Дополнительные сведения см. в разделе [Создание пакета](../create-packages/creating-a-package.md).

## <a name="usage"></a>Использование

```cli
nuget spec [<packageID>] [options]
```

где `<packageID>` — это дополнительный пакет идентификатор, для сохранения в `.nuspec` файла.

## <a name="options"></a>Параметры

| Параметр | Описание: |
| --- | --- |
| AssemblyPath | Указывает путь к сборке для использования метаданных. |
| Force | Перезаписывает все существующие `.nuspec` файла. |
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Справка | Отображает справку по команде. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
