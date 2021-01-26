---
title: Команда удаления интерфейса командной строки NuGet
description: Ссылка на команду nuget.exe Delete
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 96c75366ae69b34f5cd1f55feb53087b5d0ea324
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775946"
---
# <a name="delete-command-nuget-cli"></a>команда Delete (интерфейс командной строки NuGet)

Область **применения:** &bullet; **Поддерживаемые версии** публикации пакетов: все

Удаляет пакет из источника пакета или выводит из него список. Для nuget.org команда Delete удаляет [из списка пакет](../../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Использование

```cli
nuget delete <packageID> <packageVersion> [options]
```

где `<packageID>` и `<packageVersion>` выявление точного пакета, который нужно удалить или отменить из списка. Точное поведение зависит от источника. Например, для локальных папок пакет удаляется. для nuget.org пакет не входит в список.

## <a name="options"></a>Варианты

- **`-ApiKey`**

  Ключ API для целевого репозитория. Если он отсутствует, используется указанный в файле конфигурации.

- **`-ConfigFile`**

  Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.

- **`-?|-help`**

  Отображает справочные сведения для команды.

- **`-NonInteractive`**

  Подавляет запросы на ввод или подтверждение пользователя.

 - **`-np|-NoPrompt`**

   Не выводить запрос при удалении.

 - **`-NoServiceEndpoint`** Не добавляет "API/v2/Packages" к исходному URL-адресу.

- **`-src|-Source`**

  Определяет URL-адрес сервера. URL-адрес для nuget.org — `https://api.nuget.org/v3/index.json` . Для частных веб-каналов замените имя узла, например, *% HostName%/API/V3*.

- **`-Verbosity [normal|quiet|detailed]`**

  Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
