---
title: Команда интерфейса командной строки NuGet push
description: Справочник по командам nuget.exe Push-уведомлений
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bce04864224a66019a52cdfff8355f68dc424204
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/21/2019
ms.locfileid: "65975005"
---
# <a name="push-command-nuget-cli"></a>Команда Push (NuGet CLI)

**Применяется к:** пакета публикации &bullet; **поддерживаемые версии:** всем: 4.1.0, необходимые для nuget.org

> [!Important]
> Чтобы отправлять пакеты на сайте nuget.org необходимо использовать nuget.exe версии 4.1.0 +, которая реализует необходимые [протоколы NuGet](../api/nuget-protocols.md).

Отправляет пакет источник пакета и публикует его.

Конфигурацию NuGet по умолчанию можно получить, загрузив `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), затем загрузить любое `Nuget.Config` или `.nuget\Nuget.Config` файлы начиная с корневого каталога диска и заканчивая текущим каталогом (см. в разделе [Настройка Поведение NuGet](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Использование

```cli
nuget push <packagePath> [options]
```

где `<packagePath>` идентифицирует пакет для отправки на сервер.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ApiKey | Ключ API для целевого репозитория. Если не указано, используется, указанную в файле конфигурации. |
| ConfigFile | Чтобы применить файл конфигурации NuGet. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).|
| DisableBuffering | Отключает буферизацию при передаче на сервер HTTP (s), чтобы уменьшить использование памяти. Внимание: Если этот параметр используется, встроенная проверка подлинности Windows может не работать. |
| ForceEnglishOutput | *(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры. |
| Help | Отображает справку для команды. |
| NonInteractive | Подавление для пользователя данные или подтверждения. |
| NoSymbols | *(3.5 и более поздние)*  Если существует пакет символов, он не будет включено на сервере символов. |
| Source | Определяет URL-адрес сервера. NuGet идентифицирует UNC-путь или локальную папку источника и просто копирует в нее файл вместо передачи его с помощью HTTP.  Кроме того, начиная с NuGet 3.4.2, это является обязательным параметром Если `NuGet.Config` указывает файл *DefaultPushSource* значение (см. в разделе [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md)). |
| SkipDuplicate | Если уже существует пакет и версию, пропустить этот шаг и продолжить со следующего пакета Push-уведомления, если таковые имеются. |
| SymbolSource | *(3.5 и более поздние)*  Указывает URL-адрес сервера символов; nuget.smbsrc.net используется при передаче данных на сайте nuget.org |
| SymbolApiKey | *(3.5 и более поздние)*  Содержит ключ API для URL-адрес, указанной в `-SymbolSource`. |
| Время ожидания | Указывает время ожидания в секундах, для передачи на сервер. Значение по умолчанию — 300 секунд (5 минут). |
| Verbosity | Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*. |

Также см. в разделе [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
