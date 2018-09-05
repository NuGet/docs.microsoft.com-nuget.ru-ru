---
title: Справочник по PowerShell NuGet Update-Package
description: Ссылка для команды PowerShell Update-Package в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d47e1978ab7d827e0b8b97cd4e7237019185b50f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546080"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (консоль диспетчера пакетов в Visual Studio)

*Доступен только в пределах [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*

Обновляет пакет и его зависимостей или все пакеты в проекте, до более новой версии.

## <a name="syntax"></a>Синтаксис

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

В NuGet 2.8 + `Update-Package` можно использовать для возврата к предыдущей версии существующего пакета в проекте. Например если у вас установлен 5.1.0-rc1 Microsoft.AspNet.MVC, следующую команду бы понизить его до 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Параметры

|  Параметр | Описание |
| --- | --- |
| Идентификатор | Идентификатор пакета для обновления. Если этот параметр опущен, обновляет все пакеты. — Идентификатор сам является необязательным. |
| IgnoreDependencies | Пропускает обновление зависимостей пакетов. |
| ИмяПроекта | Имя проекта, содержащего пакеты для обновления, установка значений по умолчанию для всех проектов. |
| Версия | Версия, используемая для обновления, установка значений по умолчанию до последней версии. В NuGet 3.0 +, значение версии должно быть одно из *Lowest, самое высокое, HighestMinor*, или *HighestPatch* (эквивалент метода - Safe). |
| Safe | Ограничивает обновления до версии с той же версии основного и дополнительного номера, что и установленный пакет. |
| Исходный код | Путь к URL-адрес или папке источника пакета для поиска. Пути к локальной папке может быть абсолютным или относительным для текущей папки. Если этот параметр опущен, `Update-Package` выполняет поиск в текущем выбранном источнике пакета. |
| IncludePrerelease | Включает в себя предварительные выпуски пакетов обновлений. |
| Переустановка | Resintalls пакетов с помощью их текущей установленной версии. Дополнительные сведения см. в разделе [Ограничение версий для обновления](../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | Действие, выполняемое при появлении запроса на перезапись или игнорировать существующие файлы, связанные с проектом. Возможные значения: *перезаписи, игнорировать, None, OverwriteAll*, и *IgnoreAll* (3.0 или более поздней). |
| DependencyVersion | Версия пакеты зависимостей для использования, которые может принимать одно из следующих:<br/><ul><li>*Наименьшее* (по умолчанию): самую раннюю версию</li><li>*HighestPatch*: версии с улучшением минимально основных, минимально незначительные, самый высокий</li><li>*HighestMinor*: версия с наименьшим основных, наибольший исправления незначительных: наибольшая</li><li>*Самый высокий* (по умолчанию для Update-Package без параметров): самую старшую версию</li></ul>Можно задать значение по умолчанию с помощью [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) в `Nuget.Config` файл. |
| ToHighestPatch | Ограничивает обновления до версий только с той же дополнительный номер версии, что установленный пакет. |
| ToHighestMinor | Ограничивает обновления до версий только с той же основной версией, что и установленный пакет. |
| WhatIf | Показывает, что произойдет при выполнении команды без фактического выполнения обновления. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

### <a name="common-parameters"></a>Общие параметры

`Update-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладки, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

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
