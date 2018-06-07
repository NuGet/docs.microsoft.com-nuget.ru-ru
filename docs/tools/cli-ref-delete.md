---
title: Команды удаления NuGet CLI
description: Ссылка для команды delete nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0f33dd5475521da47972a6f032ac6ea86d98c83
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817182"
---
# <a name="delete-command-nuget-cli"></a>Удаление команды (NuGet CLI)

**Применяется к:** пакета публикации &bullet; **поддерживаемые версии:** все

Удаляет или unlists пакета из исходного пакета. Для nuget.org команды удаления [unlists пакета](../policies/deleting-packages.md).

## <a name="usage"></a>Использование

```cli
nuget delete <packageID> <packageVersion> [options]
```

где `<packageID>` и `<packageVersion>` определить точный пакета для удаления или исключить. Точное поведение зависит от источника. Для локальных папок например, пакет удаляется; для nuget.org пакета, отсутствующие в списке.

## <a name="options"></a>Параметры

| Параметр | Описание: |
| --- | --- |
| apiKey | Ключ API для целевой репозиторий. Если он отсутствует, используется заданный в файле конфигурации. |
| ConfigFile | Файл конфигурации NuGet вступили в силу. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).|
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Справка | Отображает справку по команде. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Исходный код | Определяет URL-адрес сервера. URL-адрес для nuget.org `https://api.nuget.org/v3/index.json`. Закрытый веб-каналы, замените на имя узла, например, *%hostname%/api/v3*. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
