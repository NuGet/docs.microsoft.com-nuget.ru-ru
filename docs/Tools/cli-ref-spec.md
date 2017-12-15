---
title: "Спецификация команду NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: "Справочник по спецификации команду nuget.exe"
keywords: "ссылка характеристик NuGet, команда характеристик"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a>Команда характеристик (NuGet CLI)

**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** все

Приводит к возникновению ошибки `.nuspec` файла для нового пакета. Если выполняются в той же папке, что и файл проекта (`.csproj`, `.vbproj`, `.fsproj`), `spec` создает токенами `.nuspec` файла. Дополнительные сведения см. в разделе [Создание пакета](../create-packages/creating-a-package.md).

## <a name="usage"></a>Использование

```
nuget spec [<packageID>] [options]
```

где `<packageID>` — это дополнительный пакет идентификатор, для сохранения в `.nuspec` файла.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| AssemblyPath | Указывает путь к сборке для использования метаданных. |
| Force | Перезаписывает все существующие `.nuspec` файла. |
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Справка | Отображает справку по команде. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
