---
title: Справочник по PowerShell Get-Project для NuGet
description: Справочник по команде "копроект PowerShell" в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 830746f032bb4eb916508ef320c5b3d0486b89a4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327361"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (консоль диспетчера пакетов в Visual Studio)

*Доступно только в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows.*

Отображает сведения об указанном по умолчанию или проекте. `Get-Project`в частности, функция возвращает референт в объект Visual Studio DTE (среда средств разработки) для проекта.

## <a name="syntax"></a>Синтаксис

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| name | Указывает отображаемый проект, по умолчанию выбран проект по умолчанию, выбранный в консоли диспетчера пакетов. Параметр-Name сам по себе не является обязательным. |
| Все | Отображает сведения для каждого проекта в решении; порядок проектов не является детерминированным. |

Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.

## <a name="common-parameters"></a>Общие параметры

`Get-Project`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```