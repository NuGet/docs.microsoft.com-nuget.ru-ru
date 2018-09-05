---
title: Зеркальный команды интерфейса командной строки NuGet
description: Справочник по командам зеркальной nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550210"
---
# <a name="mirror-command-nuget-cli"></a>Команда mirror (NuGet CLI)

**Применяется к:** пакета публикации &bullet; **поддерживаемые версии:** устаревшей в 3.2 +

Отражает пакет и его зависимости из указанного источника репозиториев в целевом репозитории.

> [!NOTE]
> Чтобы включить эту команду для версии NuGet до версии 3.2, перейдите к [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)выберите последний стабильный выпуск, скачайте `NuGet.ServerExtensions.dll` и `Nuget-Signed.exe` на локальный диск и переименования `Nuget-Signed.exe` для `nuget.exe`.

## <a name="usage"></a>Использование

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

где `<packageID>` — пакет, чтобы создать зеркало, или `<configFilePath>` идентифицирует `packages.config` файл, который содержит список пакетов, подлежащих зеркальному отображению.

`<listUrlTarget>` Указывает исходный репозиторий и `<publishUrlTarget>` указывает целевого репозитория.

Если ваш целевой репозиторий находится в `https://machine/repo` , на котором выполняется [NuGet.Server](../hosting-packages/nuget-server.md), списка и Push-URL-адреса будут `https://machine/repo/nuget` и `https://machine/repo/api/v2/package`, соответственно.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ApiKey | Ключ API для целевого репозитория. Если не существует, заданный в файле конфигурации используется (`%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| Справка | Отображает справку для команды. |
| NoCache | Запрещает использовать кэшированные пакеты NuGet. См. в разделе [управление папкой установки глобальных пакетов и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NOOP | Журналы, что можно сделать, но не выполняет действий; предполагается, что успех для операции отправки. |
| Предварительные выпуски | Включает в себя предварительные выпуски пакетов в процессе зеркального отображения. |
| Исходный код | Список источников пакетов, подлежащих зеркальному отображению. Если источники не указаны, тех, которые определены в файле конфигурации (см. в разделе ApiKey выше), используются, установка значений по умолчанию на сайте nuget.org, если не указан ни один. |
| Время ожидания | Указывает время ожидания в секундах, для передачи на сервер. Значение по умолчанию — 300 секунд (5 минут). |
| Версия | Версия устанавливаемого пакета. Если не указан, зеркально последней версии. |

Также см. в разделе [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
