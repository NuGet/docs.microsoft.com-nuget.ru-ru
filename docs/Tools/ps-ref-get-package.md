---
title: "Справочник по PowerShell Get пакет NuGet | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 42476008-64b3-480e-a966-98b2fa38b681
description: "Ссылка для команды Get-Package PowerShell в консоли диспетчера пакетов NuGet в Visual Studio."
keywords: "Пакет NuGet консоли диспетчера, команд NuGet Powershell, справочник по NuGet Powershell, Get-Package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3f93ab82e9fb769ee20070aa39ba8e3e05953839
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (консоль диспетчера пакетов в Visual Studio)

*В этом разделе описываются команды в [консоль диспетчера пакетов NuGet](Package-Manager-Console.md) в Visual Studio в Windows. Общая команда PowerShell Get-Package. в разделе [PowerShell PackageManagement ссылка](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*

Возвращает список пакетов, установленных в локальном хранилище, список пакетов из источника пакета при использовании с параметром - ListAvailable или список доступных обновлений, при использовании с параметром - Update.

## <a name="syntax"></a>Синтаксис

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Без параметров `Get-Package` отображается список пакетов, установленных в проекте по умолчанию.

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Исходный код | Путь URL-адрес или папку для пакета. Пути к локальной папке может быть абсолютным или относительным для текущей папки. Если не указано, `Get-Package` выполняет поиск в текущем выбранном источнике пакетов. При использовании с флагом-ListAvailable, по умолчанию nuget.org. |
| ListAvailable | Список пакетов, доступных в источнике пакетов, по умолчанию принимается nuget.org. Показывает значение по умолчанию 50 пакетов, пока не будут указаны - PageSize или - первый. |
| Обновления | Список пакетов, которые имеют в источнике пакета доступно обновление. |
| ИмяПроекта | Проект, из которого берутся установленные пакеты. Если не указано, возвращает установленных проекты для всего решения. |
| Фильтр | Строку фильтра, используемого для ограничения списка пакетов, применив его идентификатор пакета, описанию и тегам. |
| First | Число пакетов, возвращаемых из начала списка. Если не указано, по умолчанию — 50. |
| Skip | Пропускает первый &lt;int&gt; пакеты из списка.  |
| AllVersions | Отображает все доступные версии каждого пакета, а не только последняя версия. |
| IncludePrerelease | Предварительные выпуски пакетов включает в результаты. |
| PageSize | *(3.0 +)*  При использовании с флагом-ListAvailable (обязательно), количество пакетов, чтобы вывести список перед выдачей запроса на продолжение. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

## <a name="common-parameters"></a>Общие параметры

`Get-Package`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```

