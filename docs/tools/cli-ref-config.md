---
title: Команды интерфейса командной строки NuGet config
description: Справочник по командам config nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0497c7b99a2de6bee37d6d0ead8b055578e60b7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426078"
---
# <a name="config-command-nuget-cli"></a>команды config (NuGet CLI)

**Применяется к:** все &bullet; **поддерживаемые версии**: все

Возвращает или задает значения конфигурации NuGet. Избыточное использование см. в разделе [NuGet распространенных конфигураций](../consume-packages/configuring-nuget-behavior.md). Дополнительные сведения о допустимых именах, см. [ссылку на файл конфигурации NuGet](../reference/nuget-config-file.md).

## <a name="usage"></a>Использование

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

где `<name>` и `<value>` укажите пару "ключ значение" для задания в конфигурации. При необходимости можно указать любое количество пар. Чтобы удалить значение, укажите имя и `=` входа, но без значения.

Допустимые имена ключей, см. в разделе [ссылку на файл конфигурации NuGet](../reference/nuget-config-file.md).

В NuGet 3.4 + `<value>` можно использовать [переменные среды](cli-ref-environment-variables.md).

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| AsPath | Возвращает значение конфигурации как путь, игнорируются, когда `-Set` используется. |
| ConfigFile | Чтобы изменить файл конфигурации NuGet. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).|
| ForceEnglishOutput | *(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры. |
| Help | Отображает справку для команды. |
| NonInteractive | Подавление для пользователя данные или подтверждения. |
| Verbosity | Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*. |

Также см. в разделе [переменные среды](cli-ref-environment-variables.md)

### <a name="examples"></a>Примеры

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
