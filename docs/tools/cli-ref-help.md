---
title: Команда help интерфейса командной строки NuGet
description: Справочник по команде help nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546567"
---
# <a name="help-or--command-nuget-cli"></a>help or ? Команда (NuGet CLI)

**Применяется к:** все &bullet; **поддерживаемые версии**: все

Отображаются общие справочные сведения и справочные сведения о конкретных команд.

## <a name="usage"></a>Использование

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

где [команда] определяет определенной команды для отображения справки.

> [!Warning]
> При этом часть команд, следует учитывать указать *помочь* первыми, как с `nuget help install`, так как имеется пакет с именем «Справка» на сайте nuget.org. Если вы предоставите команда `nuget install help`, не получить справку по команде install, а установит пакет с именем справки.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Все | Печать подробная справка для всех доступных команд; игнорируется, если предоставляется определенную команду. |
| ConfigFile | Чтобы применить файл конфигурации NuGet. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).|
| ForceEnglishOutput | *(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры. |
| Справка | Отображает справку по команде help сам. |
| Markdown | Печать подробная справка в формате markdown, при использовании с `-All`. В противном случае учитывается. |
| Неинтерактивная | Подавление для пользователя данные или подтверждения. |
| Уровень детализации | Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*. |

Также см. в разделе [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
