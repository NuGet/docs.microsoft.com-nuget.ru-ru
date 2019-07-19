---
title: Команда справки интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe Help
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327801"
---
# <a name="help-or--command-nuget-cli"></a>help or ? Команда (NuGet CLI)

**Применимо к:** &bullet; все **Поддерживаемые версии**: все

Отображает общие справочные сведения и справочные сведения о конкретных командах.

## <a name="usage"></a>Использование

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

WHERE [команда] определяет конкретную команду, для которой отображается справка.

> [!Warning]
> С помощью некоторых команд можно учитывать, чтобы сначала указать *справку* , как `nuget help install`в, так как в NuGet.org есть пакет с именем "Help". Если вы выдаете `nuget install help`команду, вы не получите справку по команде install, но вместо этого установите пакет с именем Help.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Все | Печать подробной справки по всем доступным командам; пропускается, если указана определенная команда. |
| ConfigFile | Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).|
| форцеенглишаутпут | *(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке. |
| Help | Отображает справочную информацию о самой команде справки. |
| Markdown | Печать подробной справки в формате Markdown при использовании `-All`с. В противном случае значение игнорируется. |
| NonInteractive | Подавляет запросы на ввод или подтверждение пользователя. |
| Verbosity | Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
