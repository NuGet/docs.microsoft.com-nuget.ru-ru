---
title: Справочник по PowerShell для удаления пакета NuGet
description: Ссылка для команды PowerShell Uninstall-Package в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: c95479103be2cba3b4eb6964ea761870477863bd
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842474"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (консоль диспетчера пакетов в Visual Studio)

*В этом разделе описываются команды в [консоль диспетчера пакетов](package-manager-console.md) в Visual Studio в Windows. Общая команда удалением пакета PowerShell, см. в разделе [Справочник по PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Удаляет пакет из проекта, при необходимости удаления его зависимости. Если этого пакета зависят другие пакеты, команда завершится ошибкой, если не – Force задан параметр.

## <a name="syntax"></a>Синтаксис

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Если этого пакета зависят другие пакеты, команда завершится ошибкой, если не – Force задан параметр.

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Идентификатор | (Обязательно) Идентификатор пакета для удаления. — Идентификатор сам является необязательным. |
| Версия | Версия пакета для удаления, установка значений по умолчанию для текущей установленной версии. |
| RemoveDependencies | Удалите пакет и его неиспользуемые зависимости. То есть если зависят от него зависит другой пакет, он пропускается. |
| ИмяПроекта | Проект, из которого необходимо удалить пакет, по умолчанию используется тип проекта по умолчанию. |
| Force | Заставляет пакета, который требуется удалить, даже если он зависят другие пакеты. |
| WhatIf | Показывает, что произойдет при выполнении команды без фактического выполнения удаления. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

## <a name="common-parameters"></a>Общие параметры

`Uninstall-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
