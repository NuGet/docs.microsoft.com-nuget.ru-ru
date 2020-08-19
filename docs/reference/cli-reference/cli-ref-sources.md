---
title: Команда NuGet CLI Sources Command
description: Справочник по команде nuget.exe sources
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 73c9cea8200a1ab1937d25a9a611ae7f2a943dba
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622594"
---
# <a name="sources-command-nuget-cli"></a>Команда "источники" (интерфейс командной строки NuGet)

Область **применения:** использование пакетов, публикация &bullet; **поддерживаемых версий:** все

Управляет списком источников, расположенных в файле конфигурации пользовательской области или в указанном файле конфигурации. Файл конфигурации пользовательской области находится в папке `%appdata%\NuGet\NuGet.Config` (Windows) и `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Обратите внимание, что URL-адрес источника для nuget.org — `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Использование

```cli
nuget sources <operation> -Name <name> -Source <source>
```

Если `<operation>` один из *списков, добавить, удалить, включить, отключить* или *Обновить*, `<name>` — это имя источника, а `<source>` — URL-адрес источника. В каждый момент времени можно обрабатывать только один источник.

## <a name="options"></a>Параметры

- **`-ConfigFile`**

  Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.

- **`-Format`**

  Применяется к `list` действию и может быть `Detailed` (по умолчанию) или `Short` .

- **`-?|-help`**

  Отображает справочные сведения для команды.

- **`-Name`**

  Имя источника.

- **`-NonInteractive`**

  Подавляет запросы на ввод или подтверждение пользователя.

- **`-Password`**

  Указывает пароль для проверки подлинности в источнике.

- **`-src|-Source`**

  Путь к источнику пакетов.

- **`-StorePasswordInClearText`**

  Указывает, что пароль следует хранить в незашифрованном тексте, а не в стандартном способе хранения зашифрованной формы.

- **`-UserName`**

  Указывает имя пользователя для проверки подлинности в источнике.

- **`-ValidAuthenticationTypes`**

  Разделенный запятыми список допустимых типов проверки подлинности для этого источника. По умолчанию все типы проверки подлинности являются допустимыми. Например, `basic,negotiate`.

- **`-Verbosity [normal|quiet|detailed]`**

  Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .

> [!Note]
> Не забудьте добавить пароль исходного кода в том же контексте пользователя, что и nuget.exe позже используется для доступа к источнику пакета. Пароль будет сохранен в зашифрованном виде в файле конфигурации и может быть расшифрован только в том же контексте пользователя, в котором он был зашифрован. Например, при использовании сервера сборки для восстановления пакетов NuGet пароль должен быть зашифрован с помощью того же пользователя Windows, под которым будет выполняться задача сервера сборки.

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
