---
title: Команда NuGet CLI Locals
description: Справочник по команде NuGet. exe Locals
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327811"
---
# <a name="locals-command-nuget-cli"></a>Команда locals (NuGet CLI)

Область **применения:** &bullet; **Поддерживаемые версии** потребления пакетов: 3.3+

Очищает или перечисляет локальные ресурсы NuGet, такие как *HTTP-Cache*, папка *Global-Packages* и временная папка. `locals` Команду также можно использовать для вывода списка этих расположений. Дополнительные сведения см. [в разделе Управление глобальными пакетами и папками кэша](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Использование

```cli
nuget locals <folder> [options]
```

где `<folder>` — один из `all`, `http-cache` `global-packages` `temp` `plugins-cache` , `packages-cache` *(3,5 и более ранних версий)* ,, *(3.4 +)* и *(4.8 +)* .

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Clear | Очищает указанную папку. |
| ConfigFile | Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).|
| форцеенглишаутпут | *(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке. |
| Help | Отображает справочные сведения для команды. |
| Список | Отображает расположение указанной папки или расположения всех папок при использовании со *всеми*. |
| NonInteractive | Подавляет запросы на ввод или подтверждение пользователя. |
| Verbosity | Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Дополнительные примеры см. [в разделе Управление глобальными пакетами и папками кэша](../../consume-packages/managing-the-global-packages-and-cache-folders.md).
