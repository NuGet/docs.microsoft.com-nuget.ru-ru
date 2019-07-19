---
title: Зеркальная команда CLI NuGet
description: Справочник по команде NuGet. exe Mirror
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327671"
---
# <a name="mirror-command-nuget-cli"></a>Команда mirror (NuGet CLI)

Область **применения:** &bullet; **Поддерживаемые версии** публикации пакетов: не рекомендуется в 3.2 +

Отражает пакет и его зависимости от указанных исходных репозиториев в целевом репозитории.

> [!NOTE]
> Чтобы включить эту команду для версий NuGet до 3,2, перейдите на [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)страницу, выберите последний стабильный выпуск, `NuGet.ServerExtensions.dll` Скачайте `Nuget-Signed.exe` и перейдите на локальный диск и `Nuget-Signed.exe` переименуйте в `nuget.exe`.

## <a name="usage"></a>Использование

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

где `<packageID>` — это пакет для зеркального отображения `<configFilePath>` , или `packages.config` файл, в котором перечислены пакеты для зеркального отображения.

Указывает исходный репозиторий и `<publishUrlTarget>` указывает целевой репозиторий. `<listUrlTarget>`

Если целевой репозиторий находится на `https://machine/repo` [сервере NuGet. Server](../../hosting-packages/nuget-server.md), `https://machine/repo/nuget` `https://machine/repo/api/v2/package`URL-адреса списка и отправки отправляются соответственно.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ApiKey | Ключ API для целевого репозитория. Если он отсутствует, используется указанный в файле конфигурации (`%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| Help | Отображает справочные сведения для команды. |
| NoCache | Предотвращает использование кэшированных пакетов NuGet. См. раздел [Управление глобальными пакетами и папками кэша](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NOOP | Записывает в журнал то, что было сделано, но не выполняет действия. Предполагается успешность операций принудительной отправки. |
| Предварительной | Включает предварительные пакеты в операцию зеркального отображения. |
| Source | Список источников пакетов для зеркального отображения. Если источники не указаны, используются те, которые определены в файле конфигурации (см. ApiKey выше), по умолчанию используется значение nuget.org, если не указано ни одного. |
| Время ожидания | Указывает время ожидания в секундах для отправки на сервер. Значение по умолчанию — 300 секунд (5 минут). |
| Версия | Версия пакета для установки. Если не указано, отображается последняя версия. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
