---
title: Справочник по PowerShell Sync пакет NuGet
description: Ссылка для команды PowerShell пакета синхронизации в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8119664b1bafe9238b12b1819cc46dc1ee7bdd00
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547998"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (консоль диспетчера пакетов в Visual Studio)

*3.0 и более поздних версиях; доступен только в пределах [консоли диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*

Возвращает версию установленного пакета из указанного (или по умолчанию), проекта и синхронизирует версии для остальных проектов в решении.

## <a name="syntax"></a>Синтаксис

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Идентификатор | (Обязательно) Идентификатор пакета для синхронизации. — Идентификатор сам является необязательным. |
| IgnoreDependencies | Установите только этот пакет, не к ее зависимостям. |
| ИмяПроекта | Проект для синхронизации пакета, по умолчанию используется тип проекта по умолчанию. |
| Версия | Версия пакета для синхронизации, установка значений по умолчанию для текущей установленной версии. |
| Исходный код | Путь к URL-адрес или папке источника пакета для поиска. Пути к локальной папке может быть абсолютным или относительным для текущей папки. Если этот параметр опущен, `Sync-Package` выполняет поиск в текущем выбранном источнике пакета. |
| IncludePrerelease | Включает предварительные версии пакетов в синхронизации. |
| FileConflictAction | Действие, выполняемое при появлении запроса на перезапись или игнорировать существующие файлы, связанные с проектом. Возможные значения: *перезаписи, игнорировать, None, OverwriteAll*, и *(3.0 или более поздней)* *IgnoreAll*. |
| DependencyVersion | Версия пакеты зависимостей для использования, которые может принимать одно из следующих:<br/><ul><li>*Наименьшее* (по умолчанию): самую раннюю версию</li><li>*HighestPatch*: версии с улучшением минимально основных, минимально незначительные, самый высокий</li><li>*HighestMinor*: версия с наименьшим основных, наибольший исправления незначительных: наибольшая</li><li>*Самый высокий* (по умолчанию для Update-Package без параметров): самую старшую версию</li></ul>Можно задать значение по умолчанию с помощью [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) в `Nuget.Config` файл. |
| WhatIf | Показывает, что произойдет при выполнении команды без фактического выполнения синхронизации. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

## <a name="common-parameters"></a>Общие параметры

`Sync-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладки, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
