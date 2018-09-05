---
title: Команда locals для NuGet CLI
description: Справочник по командам nuget.exe "Локальные"
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ea216c4651ba9619bc3b6a7ab52546fd299b0bb6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545032"
---
# <a name="locals-command-nuget-cli"></a>Команда locals (NuGet CLI)

**Применяется к:** упаковать потребления &bullet; **поддерживаемые версии:** 3.3 +

Очищает или перечисляет локальные ресурсы NuGet, такие как *http-cache*, *глобальных пакетов* папки и временной папки. `locals` Команда также может использоваться для отображения списка из этих расположений. Дополнительные сведения см. в разделе [управление папкой установки глобальных пакетов и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Использование

```cli
nuget locals <folder> [options]
```

где `<folder>` является одним из `all`, `http-cache`, `packages-cache` *(3.5 и более ранних версий)*, `global-packages`, `temp` *(версии 3.4 и более)*, и `plugins-cache` *(4.8 +)*.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Clear | Удаляет указанную папку. |
| ConfigFile | Чтобы применить файл конфигурации NuGet. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).|
| ForceEnglishOutput | *(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры. |
| Справка | Отображает справку для команды. |
| Список | Вносит в список расположение указанная папка или расположение всех папок, при использовании с *все*. |
| Неинтерактивная | Подавление для пользователя данные или подтверждения. |
| Уровень детализации | Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*. |

Также см. в разделе [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Дополнительные примеры см. в разделе [управление папкой установки глобальных пакетов и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).
