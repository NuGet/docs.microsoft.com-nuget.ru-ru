---
title: Команда источники NuGet CLI | Документы Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Справочник по nuget.exe источники команды
keywords: NuGet источники ссылки, источники команды
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f682a5209556ec6741473ccf2648e8f38bb568b9
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="sources-command-nuget-cli"></a>Команда источников (NuGet CLI)

**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все

Управляет списком источников, расположенных в файле конфигурации области пользователя или указанного файла конфигурации. Файл конфигурации области пользователя находится в `%appdata%\NuGet\NuGet.Config` (Windows) и `~/.nuget/NuGet/NuGet.Config` (Mac и Linux).

Обратите внимание, что URL-адрес источника для nuget.org — `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Использование

```cli
nuget sources <operation> -Name <name> -Source <source>
```

где `<operation>` является одним из *списка, добавления, удаления, включение, отключение* или *обновление*, `<name>` имя источника, и `<source>` является URL-адрес источника.

## <a name="options"></a>Параметры

| Параметр | Описание |
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

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
