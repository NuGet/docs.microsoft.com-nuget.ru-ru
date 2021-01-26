---
title: Команда настройки интерфейса командной строки NuGet
description: Справочник по команде nuget.exe config
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3d50c12e34f71d7a62fe177da1dbb33eb702347a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775957"
---
# <a name="config-command-nuget-cli"></a>Команда config (интерфейс командной строки NuGet)

**Применимо к:** все &bullet; **Поддерживаемые версии**: все

Возвращает или задает значения конфигурации NuGet. Дополнительные сведения об использовании см. в разделе [Общие конфигурации NuGet](../../consume-packages/configuring-nuget-behavior.md). Дополнительные сведения о допустимых именах ключей см. в [справочнике по файлу конфигурации NuGet](../nuget-config-file.md).

## <a name="usage"></a>Использование

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

где `<name>` и `<value>` Укажите пару "ключ-значение", которая должна быть задана в конфигурации. При необходимости можно указать столько пар. Чтобы удалить значение, укажите имя и `=` знак, но не значение.

Сведения о допустимых именах ключей см. в [справочнике по файлу конфигурации NuGet](../nuget-config-file.md).

В NuGet 3.4 + `<value>` может использовать [переменные среды](cli-ref-environment-variables.md).

## <a name="options"></a>Варианты


- **`AsPath`**

  Возвращает значение конфигурации в виде пути, которое игнорируется, если `-Set` используется.

- **`-ConfigFile`**

  Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.

- **`-?|-help`**

  Отображает справочные сведения для команды.

- **`-NonInteractive`**

  Подавляет запросы на ввод или подтверждение пользователя.

- **`-Set`**

  Один для нескольких пар "ключ-значение", которые должны быть установлены в конфигурации.

- **`-Verbosity [normal|quiet|detailed]`**

  Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .

См. также [переменные среды](cli-ref-environment-variables.md)

### <a name="examples"></a>Примеры

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
