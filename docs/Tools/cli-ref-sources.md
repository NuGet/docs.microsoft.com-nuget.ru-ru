---
title: "Команда источники NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: "Справочник по nuget.exe источники команды"
keywords: "NuGet источники ссылки, источники команды"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2eca8557840c467a60f5f708efe242cd83609164
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/10/2018
---
# <a name="sources-command-nuget-cli"></a>Команда источников (NuGet CLI)

**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все

Управляет списком источников, расположенных в `%AppData%\NuGet\NuGet.Config` или указанного файла конфигурации.

Обратите внимание, что URL-адрес источника для nuget.org `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Использование

```
nuget sources <operation> -Name <name> -Source <source>
```

где `<operation>` является одним из *списка, добавления, удаления, включение, отключение* или *обновление*, `<name>` имя источника, и `<source>` является URL-адрес источника.

## <a name="options"></a>Параметры

| Параметр | Описание: |
| --- | --- |
| ConfigFile | *(2.5 +)*  NuGet файла конфигурации для применения. Если не указан, *%AppData%\NuGet\NuGet.Config* используется. |
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Формат | Применяется к `list` действия и может быть `Detailed` (по умолчанию) или `Short`. |
| Справка | Отображает справку по команде. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Пароль | Указывает пароль для проверки подлинности с источником. |
| StorePasswordInClearText | Указывает, чтобы сохранить пароль в незашифрованном вместо поведения по умолчанию хранение в зашифрованном виде. |
| UserName | Указывает имя пользователя для проверки подлинности с источником. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*. |

> [!Note]
> Убедитесь в том, что добавление источников в один и тот же контекст пользователя пароль как nuget.exe впоследствии будет использоваться для доступа к источнику пакета. Пароль будет сохранен в файле конфигурации зашифрованы и могут быть расшифрованы только в том же контексте пользователя, он был зашифрован. Так, например при использовании сервера сборки для восстановления пакетов NuGet, который должен быть зашифрован пароль с тем же пользователем Windows, под которой будет выполняться задача построения сервера.

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
