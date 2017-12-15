---
title: "Команда setapikey NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a64c0462-973d-4100-ba3f-8902a2b127f7
description: "Справочник по командной setapikey nuget.exe"
keywords: "Справочник по setapikey NuGet, команда setapikey"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a07c35b8bdd57157391e391e04a90204342b1d5c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
## <a name="setapikey-command-nuget-cli"></a>Команда setapikey (NuGet CLI)

**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все

Сохраняет ключ API для URL-адрес данного сервера в `NuGet.Config` , чтобы его не нужно вводить для последующих команд.

## <a name="usage"></a>Использование

```
nuget setapikey <key> -Source <url> [options]
```

где `<source>` определяет сервер и `<key>` ключа или пароля для сохранения. Если `<source>` — этот параметр опущен, подразумевается nuget.org.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ConfigFile | *(2.5 +)*  NuGet файл конфигурации для изменения. Если не указан, *%AppData%\NuGet\NuGet.Config* используется. |
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Справка | Отображает справку по команде. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
