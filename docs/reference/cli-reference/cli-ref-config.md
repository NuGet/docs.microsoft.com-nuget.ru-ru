---
title: Команда настройки интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe config
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433317"
---
# <a name="config-command-nuget-cli"></a>Команда config (интерфейс командной строки NuGet)

**Применимо к:** &bullet; все **Поддерживаемые версии**: все

Возвращает или задает значения конфигурации NuGet. Дополнительные сведения об использовании см. в разделе [Общие конфигурации NuGet](../../consume-packages/configuring-nuget-behavior.md). Дополнительные сведения о допустимых именах ключей см. в [справочнике по файлу конфигурации NuGet](../nuget-config-file.md).

## <a name="usage"></a>Использование

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

где `<name>` и`<value>` укажите пару "ключ-значение", которая должна быть задана в конфигурации. При необходимости можно указать столько пар. Чтобы удалить значение, укажите имя и `=` знак, но не значение.

Сведения о допустимых именах ключей см. в справочнике по [файлу конфигурации NuGet](../nuget-config-file.md).

В NuGet 3.4 + `<value>` может использовать [переменные среды](cli-ref-environment-variables.md).

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| аспас | Возвращает значение конфигурации в виде пути, которое игнорируется `-Set` , если используется. |
| ConfigFile | Файл конфигурации NuGet для изменения. Если этот параметр не указан, используется файл по умолчанию —`%AppData%\NuGet\NuGet.Config` (Windows) или `~/.config/NuGet/NuGet.Config` (Mac/Linux `~/.nuget/NuGet/NuGet.Config` ) или (зависит от дистрибутива ОС).|
| форцеенглишаутпут | *(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке. |
| Help | Отображает справочные сведения для команды. |
| NonInteractive | Подавляет запросы на ввод или подтверждение пользователя. |
| Verbosity | Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*. |

См. также [переменные среды](cli-ref-environment-variables.md)

### <a name="examples"></a>Примеры

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
