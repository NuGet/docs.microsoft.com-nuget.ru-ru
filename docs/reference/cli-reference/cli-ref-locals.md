---
title: Команда NuGet CLI Locals
description: Справочник по команде nuget.exe Locals
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 25feb29c7b96c47681cedd8208b8595952d3ca49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779204"
---
# <a name="locals-command-nuget-cli"></a>Команда Locals (интерфейс командной строки NuGet)

Область **применения:** &bullet; **Поддерживаемые версии** потребления пакетов: 3.3 +

Очищает или перечисляет локальные ресурсы NuGet, такие как *HTTP-Cache*, папка *Global-Packages* и временная папка. `locals`Команду также можно использовать для вывода списка этих расположений. Дополнительные сведения см. [в разделе Управление глобальными пакетами и папками кэша](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Использование

```cli
nuget locals <folder> [options]
```

где `<folder>` — один из `all` , `http-cache` , `packages-cache` *(3,5 и более ранних версий)*, `global-packages` , `temp` *(3.4 +)* и `plugins-cache` *(4.8 +)*.

## <a name="options"></a>Варианты

- **`-Clear`**

  Очищает указанную папку.

- **`-ConfigFile`**

  Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.

- **`-?|-help`**

  Отображает справочные сведения для команды.

- **`-List`**

  Отображает расположение указанной папки или расположения всех папок при использовании со *всеми*.

- **`-NonInteractive`**

  Подавляет запросы на ввод или подтверждение пользователя.

- **`-Verbosity [normal|quiet|detailed]`**

  Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Дополнительные примеры см. [в разделе Управление глобальными пакетами и папками кэша](../../consume-packages/managing-the-global-packages-and-cache-folders.md).
