---
title: Зеркальная команда CLI NuGet
description: Справочник по команде nuget.exe Mirror
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6ecd5c11383f78fdaeb01090366a8ffe294b4f8b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779172"
---
# <a name="mirror-command-nuget-cli"></a>Команда Mirror (интерфейс командной строки NuGet)

Область **применения:** &bullet; **Поддерживаемые версии** публикации пакетов: не рекомендуется в 3.2 +

Отражает пакет и его зависимости от указанных исходных репозиториев в целевом репозитории.

> [!NOTE]
> NuGet.ServerExtensions.dll и NuGet-Signed.exe, которые ранее поддерживали эту команду в NuGet 2. x (путем переименования NuGet-Signed.exe в nuget.exe), больше не доступны для загрузки. Чтобы использовать команду, аналогичную этой, попробуйте [нужетмиррор](https://www.nuget.org/packages/NuGetMirror/).

## <a name="usage"></a>Использование

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

где `<packageID>` — это пакет для зеркального отображения, или `<configFilePath>` `packages.config` файл, в котором перечислены пакеты для зеркального отображения.

`<listUrlTarget>`Указывает исходный репозиторий и `<publishUrlTarget>` указывает целевой репозиторий.

Если целевой репозиторий находится на `https://machine/repo` [сервере NuGet. Server](../../hosting-packages/nuget-server.md), URL-адреса списка и отправки отправляются `https://machine/repo/nuget` `https://machine/repo/api/v2/package` соответственно.

## <a name="options"></a>Варианты

- **`-ApiKey`**

  Ключ API для целевого репозитория. Если он отсутствует, используется указанный в файле конфигурации ( `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).

- **`-Help`**

  Отображает справочные сведения для команды.

- **`-NoCache`**

  Предотвращает использование кэшированных пакетов NuGet. См. раздел [Управление глобальными пакетами и папками кэша](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-Noop`**

  Записывает в журнал то, что было сделано, но не выполняет действия. Предполагается успешность операций принудительной отправки.

- **`-PreRelease`**

  Включает предварительные пакеты в операцию зеркального отображения.

- **`-Source`**

  Список источников пакетов для зеркального отображения. Если источники не указаны, используются те, которые определены в файле конфигурации (см. ApiKey выше), по умолчанию используется значение nuget.org, если не указано ни одного.

- **`-Timeout`**

  Указывает время ожидания в секундах для отправки на сервер.  Значение по умолчанию — 300 секунд (5 минут).

- **`-Version`**

  Версия пакета для установки. Если не указано, отображается последняя версия.

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
