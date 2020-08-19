---
title: Команда сетапикэй интерфейса командной строки NuGet
description: Справочник по команде nuget.exe сетапикэй
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b84d4257c580f6e734c26ebfc589be27bea10c82
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622815"
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
> Ключ API не используется для проверки подлинности в частном веб-канале. Инструкции по управлению учетными данными для проверки подлинности в источнике см [ `nuget sources` . в разделе](../cli-reference/cli-ref-sources.md) .
> Ключи API можно получить с отдельных серверов NuGet. Чтобы создать Апикэйс для nuget.org и управлять им, обратитесь к [разделу Получение API-ключа](../../nuget-org/scoped-api-keys.md#acquire-an-api-key) .

## <a name="options"></a>Параметры

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
