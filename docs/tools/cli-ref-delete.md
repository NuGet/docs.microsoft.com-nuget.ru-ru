---
title: Команда delete интерфейса командной строки NuGet
description: Справочник по командам nuget.exe delete
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3ea2dc3e87d0a626704fe5623d39eaf5bd3f3446
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426111"
---
# <a name="delete-command-nuget-cli"></a>удалить команду (NuGet CLI)

**Применяется к:** пакета публикации &bullet; **поддерживаемые версии:** все

Удаляет или из списка пакетов из источника пакета. Для nuget.org, команда delete [из списка пакета](../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Использование

```cli
nuget delete <packageID> <packageVersion> [options]
```

где `<packageID>` и `<packageVersion>` идентифицировать точный пакет для удаления или удалить из списка. Точное поведение зависит от источника. Для локальных папок например, пакет удаляется; для пакета nuget.org, отсутствующие в списке.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ApiKey | Ключ API для целевого репозитория. Если не указано, используется, указанную в файле конфигурации. |
| ConfigFile | Чтобы применить файл конфигурации NuGet. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).|
| ForceEnglishOutput | *(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры. |
| Help | Отображает справку для команды. |
| NonInteractive | Подавление для пользователя данные или подтверждения. |
| Source | Определяет URL-адрес сервера. URL-адреса для nuget.org — `https://api.nuget.org/v3/index.json`. Для частных каналов замените имя узла, например, *%hostname%/api/v3*. |
| Verbosity | Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*. |

Также см. в разделе [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
