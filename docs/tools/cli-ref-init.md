---
title: Команды интерфейса командной строки NuGet init
description: Справочник по командам init nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551414"
---
# <a name="init-command-nuget-cli"></a>команда init (NuGet CLI)

**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** 3.3 +

Копирует все пакеты из папки на жестком диске в папку назначения, с помощью иерархического представления, как описано для [добавьте команду](cli-ref-add.md). То есть с помощью `init` равнозначно использованию `add` на каждый пакет в папке.

Как и в `add`, назначением должна быть локальная папка или UNC-пути; Репозиториями пакетов HTTP, например nuget.org или частные серверы не поддерживаются.

## <a name="usage"></a>Использование

```cli
nuget init <source> <destination> [options]
```

где `<source>` — это папка, содержащая пакеты и `<destination>` — это локальная папка или путь UNC, в который копируются пакеты.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ConfigFile | Чтобы применить файл конфигурации NuGet. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).|
| ForceEnglishOutput | *(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры. |
| Expand | Добавляет все файлы в каждом пакете, который добавляется к источнику пакета; Совпадение с кодом `-Expand` с `add` команды. |
| Справка | Отображает справку для команды. |
| Неинтерактивная | Подавление для пользователя данные или подтверждения. |
| Уровень детализации | Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*. |

Также см. в разделе [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
