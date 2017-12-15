---
title: "NuGet CLI удалить команду | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: c213a07a-711d-47e0-9ee6-1d582e6cdb69
description: "Ссылка для команды delete nuget.exe"
keywords: "NuGet ссылки, удалите пакет команд"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 92af9dc356f3932347864976496e0ba1216496c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="delete-command-nuget-cli"></a>Удаление команды (NuGet CLI)

**Применяется к:** пакета публикации &bullet; **поддерживаемые версии:** все

Удаляет или unlists пакета из исходного пакета. Для nuget.org команды удаления [unlists пакета](../policies/Deleting-Packages.md).

## <a name="usage"></a>Использование

```
nuget delete <packageID> <packageVersion> [options]
```

где `<packageID>` и `<packageVersion>` определить точный пакета для удаления или исключить. Точное поведение зависит от источника. Для локальных папок например, пакет удаляется; для nuget.org пакета, отсутствующие в списке.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| apiKey | Ключ API для целевой репозиторий. Если не существует, указанная в *%AppData%\NuGet\NuGet.Config* используется. |
| ConfigFile | *(2.5 +)*  NuGet файла конфигурации для применения. Если не указан, *%AppData%\NuGet\NuGet.Config* используется. |
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Справка | Отображает справку по команде. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Исходный код | Определяет URL-адрес сервера. URL-адрес для nuget.org `https://api.nuget.org/v3/index.json`. Закрытый веб-каналы, замените на имя узла, например, *%hostname%/api/v3*. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
