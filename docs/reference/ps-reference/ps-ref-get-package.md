---
title: Справочник по Get-Package PowerShell для NuGet
description: Справочник по Get-Package команде PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7c91faecaac2967c7a01dd81e72b9097e7bd6cae
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901737"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (консоль диспетчера пакетов в Visual Studio)

*В этом разделе описывается команда в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows. Общие команды PowerShell Get-Package см. в [справочнике по PackageManagement для PowerShell](/powershell/module/packagemanagement).*

Получение списка пакетов, установленных в локальном репозитории, список пакетов, доступных из источника пакета при использовании с параметром-ListAvailable, или список доступных обновлений при использовании с параметром-Update.

## <a name="syntax"></a>Синтаксис

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Без параметров `Get-Package` отображает список пакетов, установленных в проекте по умолчанию.

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Источник | URL-адрес или путь к папке для пакета. Пути к локальным папкам могут быть абсолютными или относительно текущей папки. Если этот параметр опущен, `Get-Package` Поиск выполняется в текущем выбранном источнике пакета. При использовании с параметром-ListAvailable по умолчанию принимает значение nuget.org. |
| ListAvailable | Выводит список пакетов, доступных из источника пакета, по умолчанию — nuget.org. Показывает значение по умолчанию для пакетов 50, если не указаны значения-PageSize и/или-First. |
| Обновления | Перечисляет пакеты с обновлением, доступным в источнике пакета. |
| ProjectName | Проект, из которого получаются установленные пакеты. Если этот параметр опущен, то возвращает установленные проекты для всего решения. |
| Фильтр | Строка фильтра, используемая для уменьшения списка пакетов путем его применения к ИДЕНТИФИКАТОРу, описанию и тегам пакета. |
| First | Число пакетов, возвращаемых с начала списка. Если не указано, по умолчанию используется значение 50. |
| Пропустить | Опускает первые &lt; целочисленные &gt; пакеты из отображаемого списка.  |
| AllVersions | Отображает все доступные версии каждого пакета, а не только последнюю версию. |
| инклудепререлеасе | Включает в результаты предварительные пакеты. |
| PageSize | *(3.0 +)* Если используется с параметром-ListAvailable (обязательно), число пакетов, которые необходимо вывести в список, прежде чем будет предложено продолжить. |

Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.

## <a name="common-parameters"></a>Общие параметры

`Get-Package` поддерживает следующие [Общие параметры PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.

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