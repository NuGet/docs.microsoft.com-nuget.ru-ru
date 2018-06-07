---
title: Команда config NuGet CLI
description: Ссылка для выполнения команды конфигурации nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 9deab9fcca740ea99da61b7d54700a29c1813e88
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818169"
---
# <a name="config-command-nuget-cli"></a>Команда config (NuGet CLI)

**Применяется к:** все &bullet; **поддерживаемые версии**: все

Возвращает или задает значения конфигурации NuGet. Дополнительные использования см. [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md). Дополнительные сведения на допустимые имена ключей [ссылку на файл конфигурации NuGet](../reference/nuget-config-file.md).

## <a name="usage"></a>Использование

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

где `<name>` и `<value>` укажите пару "ключ значение" для установки в конфигурации. При желании можно указать столько пар. Чтобы удалить значение, укажите имя и `=` входа, но нет значения.

Допустимые имена ключей, в разделе [ссылку на файл конфигурации NuGet](../reference/nuget-config-file.md).

В NuGet 3.4 + `<value>` можно использовать [переменных среды](cli-ref-environment-variables.md).

## <a name="options"></a>Параметры

| Параметр | Описание: |
| --- | --- |
| AsPath | Возвращает значение конфигурации как путь, игнорируются, когда `-Set` используется. |
| ConfigFile | Файл конфигурации NuGet для изменения. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).|
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Справка | Отображает справку по команде. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*. |

См. также [переменные среды](cli-ref-environment-variables.md)

### <a name="examples"></a>Примеры

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
