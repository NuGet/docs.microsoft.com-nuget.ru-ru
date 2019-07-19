---
title: Удаление NuGet — Справочник по PowerShell для пакета
description: Ссылка на команду uninstall-package PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5c963588d28cab42e5fb6a43b31a17e26e49d0d2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327281"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (консоль диспетчера пакетов в Visual Studio)

*В этом разделе описывается команда в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows. Сведения об универсальной команде PowerShell uninstall-package см. в справочнике по модульу [PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Удаляет пакет из проекта, при необходимости удаляя его зависимости. Если другие пакеты зависят от этого пакета, команда завершится ошибкой, если не указан параметр – Force.

## <a name="syntax"></a>Синтаксис

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Если другие пакеты зависят от этого пакета, команда завершится ошибкой, если не указан параметр – Force.

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Идентификатор | Необходимости Идентификатор пакета для удаления. Сам переключатель-ID является необязательным. |
| Версия | Версия пакета для удаления, используемая по умолчанию для текущей установленной версии. |
| ремоведепенденЦиес | Удалите пакет и его неиспользуемые зависимости. То есть, если какая-либо зависимость имеет другой зависимый от нее пакет, он пропускается. |
| ИмяПроекта | Проект, из которого удаляется пакет, по умолчанию используется проект по умолчанию. |
| Перевести | Принудительно удаляет пакет, даже если от него зависят другие пакеты. |
| WhatIf | Показывает, что произойдет при выполнении команды без фактического выполнения удаления. |

Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.

## <a name="common-parameters"></a>Общие параметры

`Uninstall-Package`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
