---
title: "Команду NuGet CLI принудительной | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a9709eee-add2-47fb-98e6-eec0697087f6
description: "Ссылка для команды push nuget.exe"
keywords: "Справочник по принудительной NuGet, команда push"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2828cdc41903d8a948870155b23721724bfa781e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="push-command-nuget-cli"></a>Команда Push (NuGet CLI)

**Применяется к:** пакета публикации &bullet; **поддерживаемые версии:** все; 4.1.0+, необходимые для nuget.org

> [!Important]
> Для принудительной отправки пакетов nuget.org необходимо использовать nuget.exe v4.1.0 +, которая реализует необходимые [протоколы NuGet](../api/nuget-protocols.md).

Отправляет пакет источник пакета и публикует его.

Конфигурация по умолчанию NuGet можно получить, загрузив `%AppData%\NuGet\NuGet.Config`, затем загрузки любой `Nuget.Config` или `.nuget\Nuget.Config` файлы, начиная с корневого каталога диска и заканчивается в текущем каталоге (см. [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Использование

```
nuget push <packagePath> [options]
```

где `<packagePath>` идентификатор пакета для отправки на сервер.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| apiKey | Ключ API для целевой репозиторий. Если не существует, указанная в *%AppData%\NuGet\NuGet.Config* используется. |
| ConfigFile | *(2.5 +)*  NuGet файла конфигурации для применения. Если не указан, *%AppData%\NuGet\NuGet.Config* используется. |
| DisableBuffering | Отключает буферизацию при принудительной установке на сервер HTTP (s), чтобы уменьшить использование памяти. Внимание: Если этот параметр используется, встроенная проверка подлинности Windows может не работать. |
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Справка | Отображает справку по команде. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| NoSymbols | *(3.5 +)*  Если существует пакет символов, оно не будет включено на сервере символов. |
| Исходный код | Определяет URL-адрес сервера. С помощью NuGet 2.5 + NuGet идентификации UNC-путь или локальную папку источника и просто скопируйте в нее файл вместо него с помощью протокола HTTP.  Кроме того, начиная с помощью NuGet 3.4.2 Это обязательный параметр если не `NuGet.Config` файл определяет *DefaultPushSource* значение (в разделе [NuGet Настройка поведения](../Consume-Packages/Configuring-NuGet-Behavior.md)). |
| SymbolSource | *(3.5 +)*  Указывает URL-адрес сервера символов; nuget.smbsrc.net используется при принудительной установке в nuget.org |
| SymbolApiKey | *(3.5 +)*  Указывает ключ API для URL-адрес, указанной в `-SymbolSource`. |
| Время ожидания | Указывает время ожидания в секундах для принудительной отправки на сервер. Значение по умолчанию — 300 секунд (5 минут). |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
