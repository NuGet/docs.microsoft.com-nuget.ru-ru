---
title: Установка NuGet — Справочник по PowerShell для пакета
description: Справочник по команде PowerShell Install-Package в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: a65ba63ed070f40e82c43d12e5fad12d86f28112
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384445"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (консоль диспетчера пакетов в Visual Studio)

*В этом разделе описывается команда в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows. Для универсальной команды PowerShell Install-package см. Справочник по модульу [PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Устанавливает пакет и его зависимости в проект.

## <a name="syntax"></a>Синтаксис

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

В NuGet 2.8 + `Install-Package` может понизить уровень существующего пакета в проекте. Например, при наличии установленного Microsoft. AspNet. MVC 5.1.0-RC1 Следующая команда понизить ее до 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Id | Необходимости Идентификатор устанавливаемого пакета. (*3.0 +* ) Идентификатор может быть путем или URL-адресом `packages.config` файла или `.nupkg`ом файле. Сам переключатель-ID является необязательным. |
| игноредепенденЦиес | Установить только этот пакет, но не его зависимости. |
| ИмяПроекта | Проект, в который устанавливается пакет, по умолчанию используемый в качестве проекта по умолчанию. |
| Source | URL-адрес или путь к папке для источника пакета для поиска. Пути к локальным папкам могут быть абсолютными или относительно текущей папки. Если этот параметр опущен, `Install-Package` выполняет поиск выбранного в данный момент источника пакета. |
| {2&gt;Version&lt;2} | Версия устанавливаемого пакета, по умолчанию — последняя версия. |
| инклудепререлеасе | Учитываются предварительные пакеты для установки. Если пропущен, учитываются только стабильные версии пакетов. |
| филеконфликтактион | Действие, предпринимаемое при запросе перезаписи или пропуска существующих файлов, на которые ссылается проект. Возможные значения: *overwrite, ignore, None, овервритеалл*и *(3.0 +)* *IgnoreAll*. |
| депенденциверсион | Используемая версия пакетов зависимостей, которая может быть одной из следующих:<br/><ul><li>*Самый низкий* (по умолчанию): самая низкая версия</li><li>*Хигхестпатч*: версия с наименьшим основным, наименьшим незначительным, самым высоким исправлением</li><li>*Хигхестминор*: версия с наименьшим основным, наибольшим незначительным, самым высоким исправлением</li><li>*Высший* (по умолчанию для Update-Package без параметров): самая высокая версия</li></ul>Значение по умолчанию можно задать с помощью параметра [`dependencyVersion`](../nuget-config-file.md#config-section) в файле `Nuget.Config`. |
| Whatif | Показывает, что произойдет при выполнении команды без фактического выполнения установки. |

Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.

## <a name="common-parameters"></a>Общие параметры

`Install-Package` поддерживает следующие [Общие параметры PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
