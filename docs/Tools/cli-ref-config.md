---
title: "Команды NuGet CLI config | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a50295ff-8be9-47d9-a260-822e899334cb
description: "Ссылка для выполнения команды конфигурации nuget.exe"
keywords: "Справочник по конфигурации NuGet, команда конфигурации"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f49751d9747687177e3b6c1890ee9d2919be8d0e
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/10/2018
---
# <a name="config-command-nuget-cli"></a>Команда config (NuGet CLI)

**Применяется к:** все &bullet; **поддерживаемые версии**: все

Возвращает или задает значения конфигурации NuGet. Дополнительные использования см. [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md). Дополнительные сведения на допустимые имена ключей [ссылку на файл конфигурации NuGet](../Schema/nuget-config-file.md).

## <a name="usage"></a>Использование

```
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

где `<name>` и `<value>` укажите пару "ключ значение" для установки в конфигурации. При желании можно указать столько пар. Чтобы удалить значение, укажите имя и `=` входа, но нет значения.

Допустимые имена ключей, в разделе [ссылку на файл конфигурации NuGet](../Schema/nuget-config-file.md).

В NuGet 3.4 + `<value>` можно использовать [переменных среды](cli-ref-environment-variables.md).

## <a name="options"></a>Параметры

| Параметр | Описание: |
| --- | --- |
| AsPath | Возвращает значение конфигурации как путь, игнорируются, когда `-Set` используется. |
| ConfigFile | *(2.5 +)*  NuGet файл конфигурации для изменения. Если не указан, *%AppData%\NuGet\NuGet.Config* используется. |
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Справка | Отображает справку по команде. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*. |

См. также [переменные среды](cli-ref-environment-variables.md)

### <a name="examples"></a>Примеры

```
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
