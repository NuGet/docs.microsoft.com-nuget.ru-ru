---
title: Локальные переменные команду NuGet CLI
description: Ссылка для команды локальные nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ac07dc306bc23c2fedd33c5627e8d34a6098387c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="locals-command-nuget-cli"></a>Команда локальные переменные (NuGet CLI)

**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** 3.3 +

Очищает или перечисляет локальные ресурсы NuGet, такие как *кэша http*, *глобального пакеты* папки и временные папки. `locals` Команда также может использоваться для отображения списка из этих расположений. Дополнительные сведения см. в разделе [управление глобального пакетами и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Использование

```cli
nuget locals <folder> [options]
```

где `<folder>` является одним из `all`, `http-cache`, `packages-cache` *(3.5 и более ранних)*, `global-packages`, и `temp` *(3.4 +)*.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Clear | Удаляет указанную папку. |
| ConfigFile | Файл конфигурации NuGet вступили в силу. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).|
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Справка | Отображает справку по команде. |
| Список | Выводит расположение указанная папка или расположение всех папок, при использовании с *все*. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Дополнительные примеры см. в разделе [управление глобального пакетами и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).
