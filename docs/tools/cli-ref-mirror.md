---
title: Команда зеркальной NuGet CLI
description: Справочник по команда зеркало nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4cec854f05fcd207bb15a50ea4ebdc201fdb3ac6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818156"
---
# <a name="mirror-command-nuget-cli"></a>Команда mirror (NuGet CLI)

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
| NoCache | Предотвращает использование кэшированных пакетов NuGet. В разделе [управление глобального пакетами и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
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
