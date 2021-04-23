---
title: Справочник по Uninstall-Package PowerShell для NuGet
description: Справочник по Uninstall-Package команде PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 371e95c341efbce1c4a15facefc15cd51b266141
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901789"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (консоль диспетчера пакетов в Visual Studio)

*В этом разделе описывается команда в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows. Общие команды PowerShell Uninstall-Package см. в [справочнике по PackageManagement для PowerShell](/powershell/module/packagemanagement).*

Удаляет пакет из проекта, при необходимости удаляя его зависимости. Если от этого пакета зависят другие пакеты, команда не будет выполнена, если только для нее не был указан параметр –Force.

## <a name="syntax"></a>Синтаксис

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Если от этого пакета зависят другие пакеты, команда не будет выполнена, если только для нее не был указан параметр –Force.

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Идентификатор | Необходимости Идентификатор пакета для удаления. Сам переключатель-ID является необязательным. |
| Версия | Версия пакета для удаления, используемая по умолчанию для текущей установленной версии. |
| ремоведепенденЦиес | Удалите пакет и его неиспользуемые зависимости. То есть, если какая-либо зависимость имеет другой зависимый от нее пакет, он пропускается. |
| ProjectName | Проект, из которого удаляется пакет, по умолчанию используется проект по умолчанию. |
| Force | Принудительно удаляет пакет, даже если от него зависят другие пакеты. |
| WhatIf | Показывает, что произойдет при выполнении команды без фактического выполнения удаления. |

Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.

## <a name="common-parameters"></a>Общие параметры

`Uninstall-Package` поддерживает следующие [Общие параметры PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```