---
title: Справочник по PowerShell Get пакет NuGet
description: Ссылка для команды PowerShell Get-Package в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a28b29614dfe5abdeb24438b3451d96634a120db
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551446"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (консоль диспетчера пакетов в Visual Studio)

*В этом разделе описываются команды в [консоли диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows. Общая команда PowerShell Get-Package, см. в разделе [Справочник по PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Извлекает список пакетов, установленных в локальном репозитории, содержит список пакетов из источника пакета при использовании с параметром - ListAvailable или список доступных обновлений, при использовании с параметром - Update.

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
| Исходный код | Путь URL-адрес или папку для пакета. Пути к локальной папке может быть абсолютным или относительным для текущей папки. Если этот параметр опущен, `Get-Package` выполняет поиск в текущем выбранном источнике пакета. При использовании с параметром - ListAvailable, по умолчанию на сайте nuget.org. |
| ListAvailable | Список пакетов, доступных из источника пакета, установка значений по умолчанию на сайте nuget.org. Показывает 50 пакетов по умолчанию, если не указаны - PageSize и (или) - первый. |
| Обновления | Список пакетов, для которых доступно обновление из источника пакета. |
| ИмяПроекта | Проект, из которого необходимо получить установленные пакеты. Если не указано, возвращает сведения об установленных проекты для всего решения. |
| Фильтр | Строка фильтра, используемая для сужения списка пакетов, применяя его к идентификатор пакета, описание и теги. |
| First | Количество возвращаемых пакетов из начала списка. Если не указан, значение по умолчанию — 50. |
| Skip | Пропускает первый &lt;int&gt; пакеты из отображаемого списка.  |
| AllVersions | Отображает все доступные версии каждого пакета, а не только последнюю версию. |
| IncludePrerelease | Включает в себя предварительные выпуски пакетов в результатах. |
| PageSize | *(3.0 и более поздние)*  При использовании - ListAvailable (обязательно), число пакетов в списке перед передачей указаниям, чтобы продолжить. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

## <a name="common-parameters"></a>Общие параметры

`Get-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладки, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

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
