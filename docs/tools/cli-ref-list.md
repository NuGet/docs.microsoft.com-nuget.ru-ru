---
title: Команда list интерфейса командной строки NuGet
description: Справочник по командам списка nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549805"
---
# <a name="list-command-nuget-cli"></a>Команда List (NuGet CLI)

**Применяется к:** использование пакета, публикация &bullet; **поддерживаемые версии:** все

Отображает список пакетов из заданного источника. Если источники не указаны, все источники, определенные в файле Глобальная конфигурация `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config`, используются. Если `NuGet.Config` указывает нет источников, затем `list` использует веб-канал по умолчанию (nuget.org).

## <a name="usage"></a>Использование

```cli
nuget list [search terms] [options]
```

где необязательно слов будет отфильтровать отображаемый список. Условия поиска применяются к именам пакетов, теги и описания пакета так же, как это происходит при использовании их на сайте nuget.org.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| AllVersions | Список всех версий пакета. По умолчанию отображается только последняя версия пакета. |
| ConfigFile | Чтобы применить файл конфигурации NuGet. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).|
| ForceEnglishOutput | *(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры. |
| Справка | Отображает справку для команды. |
| IncludeDelisted | *(3.2 и более поздние)*  Отображения исключенные пакеты. |
| Неинтерактивная | Подавление для пользователя данные или подтверждения. |
| Предварительные выпуски | Включает в себя предварительные выпуски пакетов в списке. |
| Исходный код | Указывает список источников пакетов для поиска. |
| Уровень детализации | Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*. |

Также см. в разделе [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
