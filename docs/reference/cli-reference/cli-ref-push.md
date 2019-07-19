---
title: Команда отправки интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe Push
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327631"
---
# <a name="push-command-nuget-cli"></a>команда push (интерфейс командной строки NuGet)

Область **применения:** &bullet; **Поддерживаемые версии** публикации пакетов: ALL; 4.1.0 + требуется для NuGet.org

> [!Important]
> Чтобы отправить пакеты в nuget.org, необходимо использовать NuGet. exe v 4.1.0 +, который реализует необходимые [протоколы NuGet](../../api/nuget-protocols.md).

Отправляет пакет в источник пакета и публикует его.

Конфигурация NuGet по умолчанию получается путем `%AppData%\NuGet\NuGet.Config` загрузки (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux), а затем `Nuget.Config` загрузки `.nuget\Nuget.Config` любых файлов или, начиная с корневого диска и заканчивая текущим каталогом (см. Общие сведения о NuGet). [ конфигурации](../../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Использование

```cli
nuget push <packagePath> [options]
```

где `<packagePath>` идентифицирует пакет для отправки на сервер.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ApiKey | Ключ API для целевого репозитория. Если он отсутствует, используется указанный в файле конфигурации. |
| ConfigFile | Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).|
| дисаблебуфферинг | Отключает буферизацию при принудительной отправке на сервер HTTP (s) для уменьшения использования памяти. Внимание! при использовании этого параметра встроенная проверка подлинности Windows может не работать. |
| форцеенглишаутпут | *(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке. |
| Help | Отображает справочные сведения для команды. |
| NonInteractive | Подавляет запросы на ввод или подтверждение пользователя. |
| Символы с символами | *(3.5 +)* Если пакет символов существует, он не будет отправлен на сервер символов. |
| Source | Определяет URL-адрес сервера. NuGet определяет источник в формате UNC или локальную папку и просто копирует файл вместо отправки с помощью HTTP.  Кроме того, начиная с NuGet 3.4.2 этот параметр является обязательным, если только `NuGet.Config` в файле не указано значение *дефаултпушсаурце* (см. раздел [Настройка поведения NuGet](../../consume-packages/configuring-nuget-behavior.md)). |
| скипдупликате | *(5.1 и* более поздние версии) Если пакет и версия уже существуют, пропустите их и продолжайте работу со следующим пакетом в push-уведомлений, если таковые имеются. |
| SymbolSource | *(3.5 +)* Указывает URL-адрес сервера символов; nuget.smbsrc.net используется при принудительной отправке в nuget.org |
| симболапикэй | *(3.5 +)* Указывает ключ API для URL-адреса, указанного `-SymbolSource`в. |
| Время ожидания | Указывает время ожидания в секундах для отправки на сервер. Значение по умолчанию — 300 секунд (5 минут). |
| Verbosity | Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*. |

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
