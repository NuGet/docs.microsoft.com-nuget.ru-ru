---
title: Удаление NuGet — Справочник по PowerShell для пакета
description: Ссылка на команду uninstall-package PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 05b7bf0e8abad0904b9e851ea6b7a5317e74229d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384419"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (консоль диспетчера пакетов в Visual Studio)

*В этом разделе описывается команда в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows. Сведения об универсальной команде PowerShell uninstall-package см. в справочнике по модульу [PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

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
| Id | Необходимости Идентификатор пакета для удаления. Сам переключатель-ID является необязательным. |
| {2&gt;Version&lt;2} | Версия пакета для удаления, используемая по умолчанию для текущей установленной версии. |
| ремоведепенденЦиес | Удалите пакет и его неиспользуемые зависимости. То есть, если какая-либо зависимость имеет другой зависимый от нее пакет, он пропускается. |
| ИмяПроекта | Проект, из которого удаляется пакет, по умолчанию используется проект по умолчанию. |
| Force | Принудительно удаляет пакет, даже если от него зависят другие пакеты. |
| Whatif | Показывает, что произойдет при выполнении команды без фактического выполнения удаления. |

Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.

## <a name="common-parameters"></a>Общие параметры

`Uninstall-Package` поддерживает следующие [Общие параметры PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
