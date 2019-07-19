---
title: Команда удаления интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe Delete
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327841"
---
# <a name="delete-command-nuget-cli"></a>команда Delete (интерфейс командной строки NuGet)

Область **применения:** &bullet; **Поддерживаемые версии** публикации пакетов: все

Удаляет пакет из источника пакета или выводит из него список. Для nuget.org команда Delete удаляет [из списка пакет](../../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Использование

```cli
nuget delete <packageID> <packageVersion> [options]
```

где `<packageID>` и`<packageVersion>` выявление точного пакета, который нужно удалить или отменить из списка. Точное поведение зависит от источника. Например, для локальных папок пакет удаляется. для nuget.org пакет не входит в список.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ApiKey | Ключ API для целевого репозитория. Если он отсутствует, используется указанный в файле конфигурации. |
| ConfigFile | Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).|
| форцеенглишаутпут | *(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке. |
| Help | Отображает справочные сведения для команды. |
| NonInteractive | Подавляет запросы на ввод или подтверждение пользователя. |
| Source | Определяет URL-адрес сервера. URL-адрес для nuget.org `https://api.nuget.org/v3/index.json`—. Для частных веб-каналов замените имя узла, например, *% HostName%/API/V3*. |
| Verbosity | Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
