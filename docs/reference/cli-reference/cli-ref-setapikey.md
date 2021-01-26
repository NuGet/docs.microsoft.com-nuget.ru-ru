---
title: Команда сетапикэй интерфейса командной строки NuGet
description: Справочник по команде nuget.exe сетапикэй
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3e0c2f84e336e0a642b1b5e815e74a1fb0878467
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780015"
---
# <a name="setapikey-command-nuget-cli"></a>Команда сетапикэй (интерфейс командной строки NuGet)

Область **применения:** использование пакетов, публикация &bullet; **поддерживаемых версий:** все

Сохраняет ключ API для данного URL-адреса сервера в, `NuGet.Config` чтобы его не нужно было указывать для последующих команд.

## <a name="usage"></a>Использование

```cli
nuget setapikey <key> -Source <url> [options]
```

где `<source>` идентифицирует сервер и `<key>` является ключом для сохранения. Если `<source>` аргумент не указан, предполагается NuGet.org. 

> [!NOTE]
> Ключ API не используется для проверки подлинности в частном веб-канале. Сведения об управлении учетными данными для проверки подлинности в источнике см. в описании [команды `nuget sources`](../cli-reference/cli-ref-sources.md).
> Ключи API можно получить с отдельных серверов NuGet. Чтобы создать Апикэйс для nuget.org и управлять им, обратитесь к [разделу Получение API-ключа](../../nuget-org/scoped-api-keys.md#acquire-an-api-key) .

## <a name="options"></a>Варианты

- **`-ConfigFile`**

  Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.

- **`-?|-help`**

  Отображает справочные сведения для команды.

- **`-NonInteractive`**

  Подавляет запросы на ввод или подтверждение пользователя.

- **`-src|-Source`**

  URL-адрес сервера, на котором действителен ключ API.

- **`-Verbosity [normal|quiet|detailed]`**

  Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
