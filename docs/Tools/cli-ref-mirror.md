---
title: "Команду NuGet CLI зеркальной | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 190d7010-172e-44b8-8a32-94a2a63be4f3
description: "Справочник по команда зеркало nuget.exe"
keywords: "Справочник по зеркальной NuGet, зеркальный команды"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67daa1aa278b42b7974c562ba4097a525e7bb105
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="mirror-command-nuget-cli"></a>Команда зеркальной (NuGet CLI)

**Применяется к:** пакета публикации &bullet; **поддерживаемые версии:** устаревшими в версии 3.2 +

Отражает пакет и его зависимости от репозиториев указанного источника в целевой репозиторий.

> [!NOTE]
> Чтобы включить эту команду для NuGet версии до версии 3.2, обратитесь к [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)выберите последнюю стабильный выпуск, загрузите `NuGet.ServerExtensions.dll` и `Nuget-Signed.exe` на локальный диск и переименования `Nuget-Signed.exe` для `nuget.exe`.

## <a name="usage"></a>Использование

```
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

где `<packageID>` является пакет, чтобы создать зеркало, или `<configFilePath>` идентифицирует `packages.config` файл, который содержит список пакетов, подлежащих зеркальному отображению.

`<listUrlTarget>` Указывает исходный репозиторий и `<publishUrlTarget>` указывает целевой репозиторий.

Если включено репозиторий целевой `https://machine/repo` , на котором выполняется [NuGet.Server](../hosting-packages/NuGet-Server.md), URL-адреса со списком и push будут `https://machine/repo/nuget` и `https://machine/repo/api/v2/package`соответственно.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| apiKey | Ключ API для целевой репозиторий. Если не существует, указанная в *%AppData%\NuGet\NuGet.Config* используется. |
| Справка | Отображает справку по команде. |
| NoCache | Запрещает NuGet с помощью пакетов из кэшей локального компьютера. |
| NOOP | Регистрирует, что выполняются, но не выполняет действий; предполагается успеха для принудительной операций. |
| Предварительный выпуск | Включает предварительные версии пакетов в процессе зеркального отображения. |
| Исходный код | Список источников пакетов, подлежащих зеркальному отображению. Если не заданы ни один из источников, тех, которые определены в *%AppData%\NuGet\NuGet.Config* используются, по умолчанию принимается nuget.org Если ничего не указано. |
| Время ожидания | Указывает время ожидания в секундах для принудительной отправки на сервер. Значение по умолчанию — 300 секунд (5 минут). |
| Версия | Версия пакета для установки. Если не указан, последняя версия является зеркальным. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
