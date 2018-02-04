---
title: "Локальные переменные команду NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Ссылка для команды локальные nuget.exe"
keywords: "Справочник по NuGet локальные переменные, локальные команды"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2018
---
# <a name="locals-command-nuget-cli"></a>Команда локальные переменные (NuGet CLI)

**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** 3.3 +

Очищает или перечисляет локальные ресурсы NuGet кэша HTTP-запроса, пакеты кэша и папке пакеты глобального уровня компьютера. `locals` Команда также может использоваться для отображения списка из этих расположений. Дополнительные сведения см. в разделе [Управление кэшем NuGet](../consume-packages/managing-the-nuget-cache.md).

## <a name="usage"></a>Использование

```cli
nuget locals <cache> [options]
```

где `<cache>` является одним из `all`, `http-cache`, `packages-cache`, `global-packages`, и `temp` *(3.4 +)*.

## <a name="options"></a>Параметры

| Параметр | Описание: |
| --- | --- |
| Clear | Удаляет указанный кэш. |
| ConfigFile | Файл конфигурации NuGet вступили в силу. Если не указан, *%AppData%\NuGet\NuGet.Config* используется. |
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Справка | Отображает справку по команде. |
| Список | Выводит расположение указанного кэша или расположение всех кэшей, при использовании с *все*. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget locals all -list
nuget locals http-cache -clear
```
