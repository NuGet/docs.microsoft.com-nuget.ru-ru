---
title: Команда источники NuGet CLI
description: Справочник по nuget.exe источники команды
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7c416d92c11328ecb020154981b0ddcc5ba9c5e8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818351"
---
# <a name="sources-command-nuget-cli"></a>Команда sources (NuGet CLI)

**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все

Управляет списком источников, расположенных в файле конфигурации области пользователя или указанного файла конфигурации. Файл конфигурации области пользователя находится в `%appdata%\NuGet\NuGet.Config` (Windows) и `~/.nuget/NuGet/NuGet.Config` (Mac и Linux).

Обратите внимание, что URL-адрес источника для nuget.org — `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Использование

```cli
nuget sources <operation> -Name <name> -Source <source>
```

где `<operation>` является одним из *списка, добавления, удаления, включение, отключение* или *обновление*, `<name>` имя источника, и `<source>` является URL-адрес источника.

## <a name="options"></a>Параметры

| Параметр | Описание: |
| --- | --- |
| ConfigFile | Файл конфигурации NuGet вступили в силу. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).|
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Формат | Применяется к `list` действия и может быть `Detailed` (по умолчанию) или `Short`. |
| Справка | Отображает справку по команде. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Пароль | Указывает пароль для проверки подлинности с источником. |
| StorePasswordInClearText | Указывает, чтобы сохранить пароль в незашифрованном вместо поведения по умолчанию хранение в зашифрованном виде. |
| UserName | Указывает имя пользователя для проверки подлинности с источником. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*. |

> [!Note]
> Убедитесь в том, что добавление источников в один и тот же контекст пользователя пароль как nuget.exe впоследствии будет использоваться для доступа к источнику пакета. Пароль будет сохранен в файле конфигурации зашифрованы и могут быть расшифрованы только в том же контексте пользователя, он был зашифрован. Так, например при использовании сервера сборки для восстановления пакетов NuGet, который должен быть зашифрован пароль с тем же пользователем Windows, под которой будет выполняться задача построения сервера.

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
