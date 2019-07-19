---
title: Команда спецификации интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe Spec
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327571"
---
# <a name="spec-command-nuget-cli"></a>Команда spec (интерфейс командной строки NuGet)

Область **применения:** &bullet; **Поддерживаемые версии** для создания пакетов: все

`.nuspec` Создает файл для нового пакета. При запуске в той же папке, что и файл проекта`.csproj`( `.vbproj`, `.fsproj`,) `spec` , создает `.nuspec` файл с маркерами. Дополнительные сведения см. [в разделе Создание пакета](../../create-packages/creating-a-package.md).

## <a name="usage"></a>Использование

```cli
nuget spec [<packageID>] [options]
```

где `<packageID>` — это необязательный идентификатор пакета для сохранения `.nuspec` в файле.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| AssemblyPath | Указывает путь к сборке, используемой для метаданных. |
| Перевести | Перезаписывает существующий `.nuspec` файл. |
| форцеенглишаутпут | *(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке. |
| Help | Отображает справочные сведения для команды. |
| NonInteractive | Подавляет запросы на ввод или подтверждение пользователя. |
| Verbosity | Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
