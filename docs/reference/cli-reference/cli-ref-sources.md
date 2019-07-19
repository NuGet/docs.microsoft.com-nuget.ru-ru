---
title: Команда NuGet CLI Sources Command
description: Справочник по команде NuGet. exe sources
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327601"
---
# <a name="sources-command-nuget-cli"></a>Команда sources (NuGet CLI)

Область **применения:** использование пакетов, публикация &bullet; **поддерживаемых версий:** все

Управляет списком источников, расположенных в файле конфигурации пользовательской области или в указанном файле конфигурации. Файл конфигурации пользовательской области находится в папке `%appdata%\NuGet\NuGet.Config` (Windows) и `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Обратите внимание, что URL-адрес источника для nuget.org — `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Использование

```cli
nuget sources <operation> -Name <name> -Source <source>
```

Если `<operation>` один из *списков, добавить, удалить, включить, отключить* или *Обновить*, `<name>` — это имя источника, а `<source>` — URL-адрес источника. В каждый момент времени можно обрабатывать только один источник.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ConfigFile | Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).|
| форцеенглишаутпут | *(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке. |
| Формат | Применяется к `list` действию и может быть `Detailed` (по умолчанию) или `Short`. |
| Help | Отображает справочные сведения для команды. |
| NonInteractive | Подавляет запросы на ввод или подтверждение пользователя. |
| Пароль | Указывает пароль для проверки подлинности в источнике. |
| сторепассвординклеартекст | Указывает, что пароль следует хранить в незашифрованном тексте, а не в стандартном способе хранения зашифрованной формы. |
| UserName | Указывает имя пользователя для проверки подлинности в источнике. |
| Verbosity | Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*. |

> [!Note]
> Не забудьте добавить пароль источников в том же контексте пользователя, что и NuGet. exe позднее используется для доступа к источнику пакета. Пароль будет сохранен в зашифрованном виде в файле конфигурации и может быть расшифрован только в том же контексте пользователя, в котором он был зашифрован. Например, при использовании сервера сборки для восстановления пакетов NuGet пароль должен быть зашифрован с помощью того же пользователя Windows, под которым будет выполняться задача сервера сборки.

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
