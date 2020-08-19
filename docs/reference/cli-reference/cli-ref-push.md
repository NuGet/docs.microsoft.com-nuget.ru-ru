---
title: Команда отправки интерфейса командной строки NuGet
description: Справочник по команде nuget.exe Push
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d53a2e7f41219e68e59b195d1d5a9d1f62ad7c63
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622850"
---
# <a name="push-command-nuget-cli"></a>команда push (интерфейс командной строки NuGet)

Область **применения:** &bullet; **Поддерживаемые версии** публикации пакетов: ALL; 4.1.0 + требуется для NuGet.org

> [!Important]
> Чтобы отправить пакеты в nuget.org, необходимо использовать nuget.exe v 4.1.0 +, который реализует необходимые [протоколы NuGet](../../api/nuget-protocols.md).

Отправляет пакет в источник пакета и публикует его.

Конфигурация NuGet по умолчанию получается путем загрузки `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), а затем загрузки любых `Nuget.Config` файлов или, `.nuget\Nuget.Config` начиная с корневого диска и заканчивая текущим каталогом (см. раздел [Общие конфигурации NuGet](../../consume-packages/configuring-nuget-behavior.md)).

## <a name="usage"></a>Использование

```cli
nuget push <packagePath> [options]
```

где `<packagePath>` идентифицирует пакет для отправки на сервер.

## <a name="options"></a>Параметры

- **`-ApiKey`**

  Ключ API для целевого репозитория. Если он отсутствует, используется указанный в файле конфигурации.

- **`-ConfigFile`**

  Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-DisableBuffering`**

  Отключает буферизацию при принудительной отправке на сервер HTTP (s) для уменьшения использования памяти. Внимание! при использовании этого параметра встроенная проверка подлинности Windows может не работать.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.

- **`-?|-help`**

  Отображает справочные сведения для команды.

- **`-NonInteractive`**

  Подавляет запросы на ввод или подтверждение пользователя.

- **`-NoServiceEndpoint`**

  Не добавляет `api/v2/packages` к исходному URL-адресу.

- **`-NoSymbols`**

  *(3.5 +)* Если пакет символов существует, он не будет отправлен на сервер символов.

- **`-src|-Source`**

  Определяет URL-адрес сервера. NuGet определяет источник в формате UNC или локальную папку и просто копирует файл вместо отправки с помощью HTTP.  Кроме того, начиная с NuGet 3.4.2 этот параметр является обязательным, если только в `NuGet.Config` файле не указано значение *дефаултпушсаурце* (см. раздел [Настройка поведения NuGet](../../consume-packages/configuring-nuget-behavior.md)).

- **`-SkipDuplicate`**

  *(5.1 и более поздние версии)* Если пакет и версия уже существуют, пропустите их и продолжайте работу со следующим пакетом в push-уведомлений, если таковые имеются.

- **`-SymbolSource`**

  *(3.5 +)* Указывает URL-адрес сервера символов; nuget.smbsrc.net используется при принудительной отправке в nuget.org

- **`-SymbolApiKey`**

  *(3.5 +)* Указывает ключ API для URL-адреса, указанного в `-SymbolSource` .

- **`-Timeout`**

  Указывает время ожидания в секундах для отправки на сервер.  Значение по умолчанию — 300 секунд (5 минут).

- **`-Verbosity [normal|quiet|detailed]`**

  Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .


См. также [переменные среды](cli-ref-environment-variables.md)

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
