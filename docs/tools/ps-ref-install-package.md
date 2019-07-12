---
title: Справочник по PowerShell NuGet Install-Package
description: Справочник по команду PowerShell Install-Package в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 755c87bbc68d3b688c81e16edbc1faabdc9e0520
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842497"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (консоль диспетчера пакетов в Visual Studio)

*В этом разделе описываются команды в [консоль диспетчера пакетов](package-manager-console.md) в Visual Studio в Windows. Общая команда PowerShell Install-Package, см. в разделе [Справочник по PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Устанавливает пакет и его зависимости в проект.

## <a name="syntax"></a>Синтаксис

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

В NuGet 2.8 + `Install-Package` возможность возврата существующего пакета в проекте. Например если у вас установлен 5.1.0-rc1 Microsoft.AspNet.MVC, следующую команду бы понизить его до 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Идентификатор | (Обязательно) Идентификатор пакета для установки. (*3.0 +* ) идентификатор может быть путь или URL-адрес `packages.config` файл или `.nupkg` файл. — Идентификатор сам является необязательным. |
| IgnoreDependencies | Установите только этот пакет, не к ее зависимостям. |
| ИмяПроекта | Проект, в который необходимо установить пакет, по умолчанию используется тип проекта по умолчанию. |
| Source | Путь к URL-адрес или папке источника пакета для поиска. Пути к локальной папке может быть абсолютным или относительным для текущей папки. Если этот параметр опущен, `Install-Package` выполняет поиск в текущем выбранном источнике пакета. |
| Версия | Версия пакета, чтобы установить, по умолчанию до последней версии. |
| IncludePrerelease | Считает, что предварительные версии пакетов для установки. Если этот параметр опущен, учитываются только стабильные пакеты. |
| FileConflictAction | Действие, выполняемое при появлении запроса на перезапись или игнорировать существующие файлы, связанные с проектом. Возможные значения: *перезаписи, игнорировать, None, OverwriteAll*, и *(3.0 или более поздней)* *IgnoreAll*. |
| DependencyVersion | Версия пакеты зависимостей для использования, которые может принимать одно из следующих:<br/><ul><li>*Наименьшее* (по умолчанию): самую раннюю версию</li><li>*HighestPatch*: версии с улучшением минимально основных, минимально незначительные, самый высокий</li><li>*HighestMinor*: версия с наименьшим основных, наибольший исправления незначительных: наибольшая</li><li>*Самый высокий* (по умолчанию для Update-Package без параметров): самую старшую версию</li></ul>Можно задать значение по умолчанию с помощью [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) в `Nuget.Config` файл. |
| WhatIf | Показывает, что произойдет при выполнении команды без фактического выполнения установки. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

## <a name="common-parameters"></a>Общие параметры

`Install-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
