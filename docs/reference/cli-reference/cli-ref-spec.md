---
title: Команда спецификации интерфейса командной строки NuGet
description: Справочник по команде nuget.exe Spec
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17603fa30a75c7906f867c96c5d77f31732eaa59
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622568"
---
# <a name="spec-command-nuget-cli"></a>Команда spec (интерфейс командной строки NuGet)

Область **применения:** &bullet; **Поддерживаемые версии** для создания пакетов: все

Создает `.nuspec` файл для нового пакета. При запуске в той же папке, что и файл проекта ( `.csproj` , `.vbproj` , `.fsproj` ), `spec` создает файл с маркерами `.nuspec` . Дополнительные сведения см. [в разделе Создание пакета](../../create-packages/creating-a-package.md).

## <a name="usage"></a>Использование

```cli
nuget spec [<packageID>] [options]
```

где `<packageID>` — это необязательный идентификатор пакета для сохранения в `.nuspec` файле.

## <a name="options"></a>Параметры

- **`-AssemblyPath`**

  Указывает путь к сборке, используемой для метаданных.

- **`-Force`**

  Перезаписывает существующий `.nuspec` файл.


- **`-ForceEnglishOutput`**

  *(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.

- **`-?|-help`**

  Отображает справочные сведения для команды.

- **`-NonInteractive`**

  Подавляет запросы на ввод или подтверждение пользователя.

- **`-Verbosity [normal|quiet|detailed]`**

  Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
