---
title: Команда справки интерфейса командной строки NuGet
description: Справочник по команде nuget.exe Help
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5d91638c4a6f167ea8a04e5dfa2905cb55084ddd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779352"
---
# <a name="help-or--command-nuget-cli"></a>help или ? команда (интерфейс командной строки NuGet)

**Применимо к:** все &bullet; **Поддерживаемые версии**: все

Отображает общие справочные сведения и справочные сведения о конкретных командах.

## <a name="usage"></a>Использование

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

WHERE [команда] определяет конкретную команду, для которой отображается справка.

> [!Warning]
> С помощью некоторых команд можно учитывать, чтобы сначала указать *справку* , как в `nuget help install` , так как в NuGet.org есть пакет с именем "Help". Если вы выдаете команду `nuget install help` , вы не получите справку по команде install, но вместо этого установите пакет с именем Help.

## <a name="options"></a>Варианты

- **`-All`**

  Печать подробной справки по всем доступным командам; пропускается, если указана определенная команда.

- **`-ConfigFile`**

  Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.

- **`-?|-help`**

  Отображает справочные сведения для команды.

- **`-Markdown`**

  Печать подробной справки в формате Markdown при использовании с `-All` . В противном случае значение игнорируется.

- **`-NonInteractive`**

  Подавляет запросы на ввод или подтверждение пользователя.

- **`-Verbosity [normal|quiet|detailed]`**

  Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
