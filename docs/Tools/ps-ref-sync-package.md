---
title: "Справочник по PowerShell синхронизации пакет NuGet | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Ссылка для команды PowerShell пакета синхронизации в консоли диспетчера пакетов NuGet в Visual Studio."
keywords: "Пакет NuGet консоли диспетчера, команд NuGet Powershell, справочник по NuGet Powershell, пакета синхронизации"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 02233cd0532fab2338e65e0d58b9afc3e2dab6af
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (консоль диспетчера пакетов в Visual Studio)

*Версия 3.0 +; доступен только в пределах [консоль диспетчера пакетов NuGet](Package-Manager-Console.md) в Visual Studio в Windows.*

Возвращает версию установленного пакета из указанного (или по умолчанию), проекта и синхронизируется с остальными проектами в решении.

## <a name="syntax"></a>Синтаксис

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --- | --- |
| Идентификатор | (Обязательно) Идентификатор пакета для синхронизации. — Идентификатор коммутатора сам является необязательным. |
| IgnoreDependencies | Установите только этот пакет, а не его зависимости. |
| ИмяПроекта | Проект для синхронизации пакета, установка значений по умолчанию для проекта по умолчанию. |
| Версия | Версия пакета для синхронизации, установка значений по умолчанию для текущей установленной версии. |
| Исходный код | Путь URL-адрес или папку источника пакета для поиска. Пути к локальной папке может быть абсолютным или относительным для текущей папки. Если не указано, `Sync-Package` выполняет поиск в текущем выбранном источнике пакетов. |
| IncludePrerelease | Включает предварительные версии пакетов в синхронизации. |
| FileConflictAction | Действие, выполняемое при появлении запроса, чтобы игнорировать существующие файлы, связанные с проектом или перезаписать. Возможными значениями являются *перезаписи, пропустить, None, OverwriteAll*, и *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | Версия пакеты зависимостей для использования, которые может принимать одно из следующих действий:<br/><ul><li>*Наименьший* (по умолчанию): самая ранняя версия</li><li>*HighestPatch*: версия с исправлением минимально основных минимально дополнительный: наибольшая</li><li>*HighestMinor*: версия с наименьшим основной, наивысший дополнительный номер: наибольшая исправления</li><li>*Наибольший* (по умолчанию для пакета обновления без параметров): самую новую версию</li></ul>Можно задать значение по умолчанию с помощью [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) в `Nuget.Config` файла. |
| WhatIf | Показывает, что произойдет при запуске команды без фактического выполнения синхронизации. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

## <a name="common-parameters"></a>Общие параметры

`Sync-Package`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

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
