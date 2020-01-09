---
title: Команда сетапикэй интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe сетапикэй
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383973"
---
# <a name="setapikey-command-nuget-cli"></a>Команда сетапикэй (интерфейс командной строки NuGet)

Область **применения:** использование пакетов, публикация &bullet; **Поддерживаемые версии:** все

Сохраняет ключ API для указанного URL-адреса сервера в `NuGet.Config`, чтобы его не нужно было указывать для последующих команд.

## <a name="usage"></a>Метрики

```cli
nuget setapikey <key> -Source <url> [options]
```

где `<source>` идентифицирует сервер, а `<key>` — ключ или пароль для сохранения. Если `<source>` опущен, предполагается nuget.org.

> [!NOTE]
> Ключ API не используется для проверки подлинности в частном веб-канале. Инструкции по управлению учетными данными для проверки подлинности в источнике см. в разделе [`nuget sources`](../cli-reference/cli-ref-sources.md) .

## <a name="options"></a>Options

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
