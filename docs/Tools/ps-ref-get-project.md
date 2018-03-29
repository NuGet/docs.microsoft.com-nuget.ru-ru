---
title: Справочник по PowerShell NuGet Get проект | Документы Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Ссылка для команды GetProject PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
keywords: Пакет NuGet консоли диспетчера, команд NuGet Powershell, справочник по NuGet Powershell, Get-проект
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9fcdcf7c550408cd7dfd73787ee14821c46a1df9
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get проект (консоль диспетчера пакетов в Visual Studio)

*Доступен только в пределах [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*

Отображает сведения о значения по умолчанию или указанный проект. `Get-Project` специально возвращает объект ссылки на объект Visual Studio DTE (среду средств разработки) для проекта.

## <a name="syntax"></a>Синтаксис

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Имя | Указывает проект для отображения, по умолчанию принимается по умолчанию проекта, выбранного в консоли диспетчера пакетов. -Имя коммутатора является необязательным. |
| Все | Отображает сведения для каждого проекта в решении; порядок проектов не является детерминированным. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

## <a name="common-parameters"></a>Общие параметры

`Get-Project` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```