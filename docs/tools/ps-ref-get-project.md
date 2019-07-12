---
title: Справочник по PowerShell Get проектами NuGet
description: Справочник по GetProject PowerShell команду в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 2ceb1557eafd213c148d3ab870925ef5bbbee145
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842281"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (консоль диспетчера пакетов в Visual Studio)

*Доступен только в пределах [консоль диспетчера пакетов](package-manager-console.md) в Visual Studio в Windows.*

Отображает сведения о по умолчанию или указанный проект. `Get-Project` в частности возвращается референта объекта Visual Studio DTE (среду средств разработки) для проекта.

## <a name="syntax"></a>Синтаксис

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| name | Указывает проект для отображения, по умолчанию принимается значение по умолчанию проекта, выбранного в консоли диспетчера пакетов. -Имя коммутатора является необязательным. |
| Все | Отображает сведения для каждого проекта в решении; порядок проектов не является детерминированным. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

## <a name="common-parameters"></a>Общие параметры

`Get-Project` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```