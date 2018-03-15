---
title: "Команду NuGet CLI зеркальной | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Справочник по команда зеркало nuget.exe"
keywords: "Справочник по зеркальной NuGet, зеркальный команды"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0c1969cc04b2e2cead5e9dadf9739fdabdf65f6c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="mirror-command-nuget-cli"></a>Команда зеркальной (NuGet CLI)

**Применяется к:** пакета публикации &bullet; **поддерживаемые версии:** устаревшими в версии 3.2 +

Отражает пакет и его зависимости от репозиториев указанного источника в целевой репозиторий.

> [!NOTE]
> Чтобы включить эту команду для NuGet версии до версии 3.2, обратитесь к [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)выберите последнюю стабильный выпуск, загрузите `NuGet.ServerExtensions.dll` и `Nuget-Signed.exe` на локальный диск и переименования `Nuget-Signed.exe` для `nuget.exe`.

## <a name="usage"></a>Использование

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

где `<packageID>` является пакет, чтобы создать зеркало, или `<configFilePath>` идентифицирует `packages.config` файл, который содержит список пакетов, подлежащих зеркальному отображению.

`<listUrlTarget>` Указывает исходный репозиторий и `<publishUrlTarget>` указывает целевой репозиторий.

Если включено репозиторий целевой `https://machine/repo` , на котором выполняется [NuGet.Server](../hosting-packages/nuget-server.md), URL-адреса со списком и push будут `https://machine/repo/nuget` и `https://machine/repo/api/v2/package`соответственно.

## <a name="options"></a>Параметры

| Параметр | Описание: |
| --- | --- |
| apiKey | Ключ API для целевой репозиторий. Если не существует, заданный в файле конфигурации используется (`%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac и Linux)). |
| Справка | Отображает справку по команде. |
| NoCache | Запрещает NuGet с помощью пакетов из кэшей локального компьютера. |
| NOOP | Регистрирует, что выполняются, но не выполняет действий; предполагается успеха для принудительной операций. |
| Предварительный выпуск | Включает предварительные версии пакетов в процессе зеркального отображения. |
| Исходный код | Список источников пакетов, подлежащих зеркальному отображению. Если не заданы ни один из источников, тех, которые определены в файле конфигурации (см. выше ApiKey), используются, по умолчанию nuget.org, если не указан ни один. |
| Время ожидания | Указывает время ожидания в секундах для принудительной отправки на сервер. Значение по умолчанию — 300 секунд (5 минут). |
| Версия | Версия пакета для установки. Если не указан, последняя версия является зеркальным. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
