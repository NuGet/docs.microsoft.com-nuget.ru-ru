---
title: "Справочник по PowerShell пакет обновления NuGet | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Ссылка для команды PowerShell пакета обновления в консоли диспетчера пакетов NuGet в Visual Studio."
keywords: "Пакет NuGet консоли диспетчера, команд NuGet Powershell, справочник по NuGet Powershell, пакет обновления"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 293d9a7fdcce633eb5a97e5f76398deb5c13bdb4
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/08/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Обновление (консоль диспетчера пакетов в Visual Studio)

*Доступен только в пределах [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*

Обновляет пакет и его зависимости, а также все пакеты в проекте, до более новой версии.

## <a name="syntax"></a>Синтаксис

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

В NuGet 2.8 + `Update-Package` можно использовать для возврата к предыдущей версии существующего пакета в проекте. Например при наличии 5.1.0-rc1 Microsoft.AspNet.MVC установлен следующая команда будет понизить его до 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Параметры

|  Параметр | Описание: |
| --- | --- |
| Идентификатор | Идентификатор пакета для обновления. Если не указано, все пакеты обновления. — Идентификатор коммутатора сам является необязательным. |
| IgnoreDependencies | Пропускает обновление зависимости пакета. |
| ИмяПроекта | Имя проекта, содержащего пакеты для обновления, установка значений по умолчанию для всех проектов. |
| Версия | Версия, используемая для обновления, установка значений по умолчанию до последней версии. В NuGet 3.0 + значение версии должно быть одним из *Lowest, самое высокое, HighestMinor*, или *HighestPatch* (эквивалентно - безопасный). |
| Safe | Ограничивает только версии с той же номерами основной и дополнительной версии, в настоящее время установленного пакета обновления. |
| Исходный код | Путь URL-адрес или папку источника пакета для поиска. Пути к локальной папке может быть абсолютным или относительным для текущей папки. Если не указано, `Uninstall-Package` выполняет поиск в текущем выбранном источнике пакетов. |
| IncludePrerelease | Включает предварительные версии пакетов обновления. |
| Переустановка | Resintalls пакетов с помощью текущей установленной версии. Дополнительные сведения см. в разделе [Ограничение версий для обновления](../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | Действие, выполняемое при появлении запроса, чтобы игнорировать существующие файлы, связанные с проектом или перезаписать. Возможными значениями являются *перезаписи, пропустить, None, OverwriteAll*, и *IgnoreAll* (3.0 +). |
| DependencyVersion | Версия пакеты зависимостей для использования, которые может принимать одно из следующих действий:<br/><ul><li>*Наименьший* (по умолчанию): самая ранняя версия</li><li>*HighestPatch*: версия с исправлением минимально основных минимально дополнительный: наибольшая</li><li>*HighestMinor*: версия с наименьшим основной, наивысший дополнительный номер: наибольшая исправления</li><li>*Наибольший* (по умолчанию для пакета обновления без параметров): самую новую версию</li></ul>Можно задать значение по умолчанию с помощью [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) в `Nuget.Config` файла. |
| ToHighestPatch | Ограничивает только версии с той же дополнительный номер версии, в настоящее время установленного пакета обновления. |
| ToHighestMinor | Ограничивает только версии с одной и той же основной версии, установленный пакет обновления. |
| WhatIf | Показывает, что произойдет при запуске команды без фактического выполнения обновления. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

### <a name="common-parameters"></a>Общие параметры

`Update-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

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