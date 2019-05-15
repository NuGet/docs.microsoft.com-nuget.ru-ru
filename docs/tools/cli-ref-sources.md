---
title: Интерфейс командной строки NuGet источники команд
description: Справочник по nuget.exe источники команд
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610620"
---
# <a name="sources-command-nuget-cli"></a>Команда sources (NuGet CLI)

**Применяется к:** использование пакета, публикация &bullet; **поддерживаемые версии:** все

Управляет списком источников, расположенных в файле конфигурации области пользователя или указанного файла конфигурации. Файл конфигурации пользователя область находится в `%appdata%\NuGet\NuGet.Config` (Windows) и `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Обратите внимание, что URL-адрес источника для nuget.org — `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Использование

```cli
nuget sources <operation> -Name <name> -Source <source>
```

где `<operation>` является одним из *списка, добавления, удаления, включение, отключение* или *обновление*, `<name>` имя источника, и `<source>` является URL-адрес источника. Одновременно можно управлять только один источник.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ConfigFile | Чтобы применить файл конфигурации NuGet. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).|
| ForceEnglishOutput | *(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры. |
| Формат | Применяется к `list` действия и может быть `Detailed` (по умолчанию) или `Short`. |
| Help | Отображает справку для команды. |
| NonInteractive | Подавление для пользователя данные или подтверждения. |
| Пароль | Указывает пароль для проверки подлинности с источником. |
| StorePasswordInClearText | Указывает, чтобы сохранить пароль в незашифрованном вместо хранения в зашифрованной форме по умолчанию. |
| UserName | Указывает имя пользователя для проверки подлинности с источником. |
| Verbosity | Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*. |

> [!Note]
> Не забудьте добавить пароль источников, в том же контексте пользователя, как nuget.exe впоследствии будет использоваться для доступа к источнику пакета. Пароль будет храниться в зашифрованном виде в файле конфигурации и могут быть расшифрованы только в том же контексте пользователя, так как он был зашифрован. Так что, например при использовании сервера сборки для восстановления пакетов NuGet, который должен быть зашифрован пароль с тем же пользователем Windows, с которой будет выполняться задача сервера сборки.

Также см. в разделе [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
