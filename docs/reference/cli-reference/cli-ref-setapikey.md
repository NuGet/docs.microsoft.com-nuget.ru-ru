---
title: Команда сетапикэй интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe сетапикэй
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231231"
---
# <a name="setapikey-command-nuget-cli"></a>Команда сетапикэй (интерфейс командной строки NuGet)

Область **применения:** использование пакетов, публикация &bullet; **Поддерживаемые версии:** все

Сохраняет ключ API для указанного URL-адреса сервера в `NuGet.Config`, чтобы его не нужно было указывать для последующих команд.

## <a name="usage"></a>Использование

```cli
nuget setapikey <key> -Source <url> [options]
```

где `<source>` идентифицирует сервер, а `<key>` — ключ для сохранения. Если `<source>` опущен, предполагается nuget.org. 

> [!NOTE]
> Ключ API не используется для проверки подлинности в частном веб-канале. Инструкции по управлению учетными данными для проверки подлинности в источнике см. в разделе [`nuget sources`](../cli-reference/cli-ref-sources.md) .
> Ключи API можно получить с отдельных серверов NuGet. Чтобы создать Апикэйс для nuget.org и управлять им, см. [раздел Publish-API-Key](../../quickstart/includes/publish-api-key.md) .

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ConfigFile | Файл конфигурации NuGet, который необходимо применить. Если не указано, используется `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке. |
| Справка | Отображает справочные сведения для команды. |
| NonInteractive | Подавляет запросы на ввод или подтверждение пользователя. |
| Уровень детализации | Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
