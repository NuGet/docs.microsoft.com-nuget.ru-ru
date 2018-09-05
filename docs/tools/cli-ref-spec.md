---
title: Спецификации команду интерфейса командной строки NuGet
description: Справочник по командам спецификаций nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68b165751ab6794d2a01d7e466619b1ce4d7ed72
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546453"
---
# <a name="spec-command-nuget-cli"></a>спецификации команда (NuGet CLI)

**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** все

Создает `.nuspec` файла для нового пакета. Если в той же папке, что файл проекта (`.csproj`, `.vbproj`, `.fsproj`), `spec` создает токенами `.nuspec` файл. Дополнительные сведения см. в разделе [Создание пакета](../create-packages/creating-a-package.md).

## <a name="usage"></a>Использование

```cli
nuget spec [<packageID>] [options]
```

где `<packageID>` — это дополнительный пакет идентификатор, чтобы сохранить в `.nuspec` файл.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| AssemblyPath | Указывает путь к сборке, используемый для метаданных. |
| Force | Перезаписываются все существующие `.nuspec` файл. |
| ForceEnglishOutput | *(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры. |
| Справка | Отображает справку для команды. |
| Неинтерактивная | Подавление для пользователя данные или подтверждения. |
| Уровень детализации | Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*. |

Также см. в разделе [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
