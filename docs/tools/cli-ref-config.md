---
title: Команды интерфейса командной строки NuGet config
description: Справочник по командам config nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 376b69186ad22d4d94a1df51146b833a1f6f9bd9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546482"
---
# <a name="config-command-nuget-cli"></a>команды config (NuGet CLI)

**Применяется к:** все &bullet; **поддерживаемые версии**: все

Возвращает или задает значения конфигурации NuGet. Избыточное использование см. в разделе [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md). Дополнительные сведения о допустимых именах, см. [ссылку на файл конфигурации NuGet](../reference/nuget-config-file.md).

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
