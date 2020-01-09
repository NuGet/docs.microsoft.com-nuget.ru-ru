---
title: Справочник по PowerShell для обновления пакета NuGet
description: Справочник по командам PowerShell Update-Package в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e1bff9d4b7391d8be87afa4b8f2fbd51ae922140
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384860"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (консоль диспетчера пакетов в Visual Studio)

*Доступно только в [консоли диспетчера пакетов NuGet](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows.*

Обновляет пакет и его зависимости или все пакеты в проекте до более новой версии.

## <a name="syntax"></a>Синтаксис

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

В NuGet 2.8 + `Update-Package` можно использовать для понижения уровня существующего пакета в проекте. Например, при наличии установленного Microsoft. AspNet. MVC 5.1.0-RC1 Следующая команда понизить ее до 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Параметры

|  Параметр | Описание |
| --- | --- |
| Id | Идентификатор обновляемого пакета. Если этот параметр опущен, обновляет все пакеты. Сам переключатель-ID является необязательным. |
| игноредепенденЦиес | Пропускает обновление зависимостей пакета. |
| ИмяПроекта | Имя проекта, содержащего пакеты для обновления, по умолчанию — для всех проектов. |
| {2&gt;Version&lt;2} | Версия, используемая для обновления, по умолчанию — последняя версия. В NuGet 3.0 + значение версии должно быть одним из *самых низких, наибольших, хигхестминор*или *хигхестпатч* (эквивалентно-безопасности). |
| Safe | Ограничивает обновления только версиями с той же основной и дополнительной версией, что и текущий установленный пакет. |
| Source | URL-адрес или путь к папке для источника пакета для поиска. Пути к локальным папкам могут быть абсолютными или относительно текущей папки. Если этот параметр опущен, `Update-Package` выполняет поиск выбранного в данный момент источника пакета. |
| инклудепререлеасе | Включает предварительные пакеты для обновлений. |
| Переустановка | Ресинталлс пакеты, используя установленные в настоящее время версии. Дополнительные сведения см. в разделе [Ограничение версий для обновления](../../consume-packages/reinstalling-and-updating-packages.md). |
| филеконфликтактион | Действие, предпринимаемое при запросе перезаписи или пропуска существующих файлов, на которые ссылается проект. Возможные значения: *overwrite, ignore, None, овервритеалл*и *IgnoreAll* (3.0 +). |
| депенденциверсион | Используемая версия пакетов зависимостей, которая может быть одной из следующих:<br/><ul><li>*Самый низкий* (по умолчанию): самая низкая версия</li><li>*Хигхестпатч*: версия с наименьшим основным, наименьшим незначительным, самым высоким исправлением</li><li>*Хигхестминор*: версия с наименьшим основным, наибольшим незначительным, самым высоким исправлением</li><li>*Высший* (по умолчанию для Update-Package без параметров): самая высокая версия</li></ul>Значение по умолчанию можно задать с помощью параметра [`dependencyVersion`](../nuget-config-file.md#config-section) в файле `Nuget.Config`. |
| тохигхестпатч | эквивалентно-Сейф. |
| тохигхестминор | Ограничивает обновления только версиями с той же основной версией, что и текущий установленный пакет. |
| Whatif | Показывает, что произойдет при выполнении команды без фактического выполнения обновления. |

Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.

### <a name="common-parameters"></a>Общие параметры

`Update-Package` поддерживает следующие [Общие параметры PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.

### <a name="examples"></a>Примеры

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
