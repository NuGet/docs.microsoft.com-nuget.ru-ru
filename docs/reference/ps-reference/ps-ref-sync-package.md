---
title: Справочник по Sync-Package PowerShell для NuGet
description: Справочник по Sync-Package команде PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 4261b0a20a4fd4183f7b08096c3477e6f9d0a02d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777410"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (консоль диспетчера пакетов в Visual Studio)

*Версия 3.0 +; доступно только в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows.*

Возвращает версию установленного пакета из указанного проекта (или по умолчанию) и синхронизирует версию с остальными проектами в решении.

## <a name="syntax"></a>Синтаксис

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Id | Необходимости Идентификатор пакета для синхронизации. Сам переключатель-ID является необязательным. |
| игноредепенденЦиес | Установить только этот пакет, но не его зависимости. |
| ProjectName | Проект, из которого необходимо синхронизировать пакет, по умолчанию используется проект по умолчанию. |
| Версия | Версия пакета для синхронизации, используемая по умолчанию для текущей установленной версии. |
| Источник | URL-адрес или путь к папке для источника пакета для поиска. Пути к локальным папкам могут быть абсолютными или относительно текущей папки. Если этот параметр опущен, `Sync-Package` Поиск выполняется в текущем выбранном источнике пакета. |
| инклудепререлеасе | Включает предварительные пакеты в синхронизацию. |
| филеконфликтактион | Действие, предпринимаемое при запросе перезаписи или пропуска существующих файлов, на которые ссылается проект. Возможные значения: *overwrite, ignore, None, овервритеалл* и *(3.0 +)* *IgnoreAll*. |
| депенденциверсион | Используемая версия пакетов зависимостей, которая может быть одной из следующих:<br/><ul><li>*Самый низкий* (по умолчанию): самая низкая версия</li><li>*Хигхестпатч*: версия с наименьшим основным, наименьшим незначительным, самым высоким исправлением</li><li>*Хигхестминор*: версия с наименьшим основным, наибольшим незначительным, самым высоким исправлением</li><li>*Высший* (по умолчанию для Update-Package без параметров): самая высокая версия</li></ul>Значение по умолчанию можно задать с помощью [`dependencyVersion`](../nuget-config-file.md#config-section) параметра в `Nuget.Config` файле. |
| WhatIf | Показывает, что произойдет при выполнении команды без фактического выполнения синхронизации. |

Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.

## <a name="common-parameters"></a>Общие параметры

`Sync-Package` поддерживает следующие [Общие параметры PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.

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