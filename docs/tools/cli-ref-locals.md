---
title: Локальные переменные команду NuGet CLI
description: Ссылка для команды локальные nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 90e8c85e7a3e0e9520933e2ddd6dd84447475f2b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818205"
---
# <a name="locals-command-nuget-cli"></a>Команда locals (NuGet CLI)

**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** 3.3 +

Очищает или перечисляет локальные ресурсы NuGet, такие как *кэша http*, *глобального пакеты* папки и временные папки. `locals` Команда также может использоваться для отображения списка из этих расположений. Дополнительные сведения см. в разделе [управление глобального пакетами и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Использование

```cli
nuget locals <folder> [options]
```

где `<folder>` является одним из `all`, `http-cache`, `packages-cache` *(3.5 и более ранних)*, `global-packages`, и `temp` *(3.4 +)*.

## <a name="options"></a>Параметры

| Параметр | Описание: |
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
