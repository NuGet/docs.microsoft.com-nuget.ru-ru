---
title: Справочник по PowerShell NuGet Install-Package | Документы Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Справочник по команду PowerShell Install-Package в консоли диспетчера пакетов NuGet в Visual Studio.
keywords: Пакет NuGet консоли диспетчера, команд NuGet Powershell, справочник по NuGet Powershell, Install-Package
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 99c965c2f8c12c7a59ee48e270172b719c1482ea
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (консоль диспетчера пакетов в Visual Studio)

*В этом разделе описываются команды в [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows. Общая команда PowerShell Install-Package. в разделе [PowerShell PackageManagement ссылка](/powershell/module/packagemanagement/?view=powershell-6).*

Устанавливает пакет и его зависимости в проект.

## <a name="syntax"></a>Синтаксис

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

В NuGet 2.8 + `Install-Package` может понизить уровень существующий пакет в проекте. Например при наличии 5.1.0-rc1 Microsoft.AspNet.MVC установлен следующая команда будет понизить его до 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Идентификатор | (Обязательно) Идентификатор пакета для установки. (*3.0 +*) может быть идентификатор или URL-адрес `packages.config` файл или `.nupkg` файла. — Идентификатор коммутатора сам является необязательным. |
| IgnoreDependencies | Установите только этот пакет, а не его зависимости. |
| Название проекта | Проект, в который необходимо установить пакет, установка значений по умолчанию для проекта по умолчанию. |
| Исходный код | Путь URL-адрес или папку источника пакета для поиска. Пути к локальной папке может быть абсолютным или относительным для текущей папки. Если не указано, `Install-Package` выполняет поиск в текущем выбранном источнике пакетов. |
| Версия | Версия пакета, чтобы установить, по умолчанию используется последняя версия. |
| IncludePrerelease | Считает, что предварительные версии пакетов для установки. Если не указано, рассматриваются только стабильные пакеты. |
| FileConflictAction | Действие, выполняемое при появлении запроса, чтобы игнорировать существующие файлы, связанные с проектом или перезаписать. Возможными значениями являются *перезаписи, пропустить, None, OverwriteAll*, и *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | Версия пакеты зависимостей для использования, которые может принимать одно из следующих действий:<br/><ul><li>*Наименьший* (по умолчанию): самая ранняя версия</li><li>*HighestPatch*: версия с исправлением минимально основных минимально дополнительный: наибольшая</li><li>*HighestMinor*: версия с наименьшим основной, наивысший дополнительный номер: наибольшая исправления</li><li>*Наибольший* (по умолчанию для пакета обновления без параметров): самую новую версию</li></ul>Можно задать значение по умолчанию с помощью [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) в `Nuget.Config` файла. |
| WhatIf | Показывает, что произойдет при запуске команды без фактического выполнения установки. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

## <a name="common-parameters"></a>Общие параметры

`Install-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

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
