---
title: "Справочник по PowerShell для добавления BindingRedirect NuGet | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 90f4dcb0-6e5a-4948-8ea9-62e0d061d95a
description: "Справочник по PowerShell BindingRedirect добавить команду в консоли диспетчера пакетов NuGet в Visual Studio."
keywords: "Пакет NuGet консоли диспетчера, команд NuGet Powershell, справочник по NuGet Powershell, добавить BindingRedirect"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6a3232af925f75713168421e68f2773060c5ebaa
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Добавить BindingRedirect (консоль диспетчера пакетов в Visual Studio)

*Доступен только в пределах [консоль диспетчера пакетов NuGet](Package-Manager-Console.md) в Visual Studio в Windows.*

Проверяет все сборки по пути вывода для проекта и добавляет перенаправления привязки в файле конфигурации приложения или веб-узла, при необходимости. Эта команда выполняется автоматически при установке пакета.

Привязку перенаправления и почему они используются Подробнее [Перенаправление версий сборок](/dotnet/framework/configure-apps/redirect-assembly-versions) в документации по .NET.

## <a name="syntax"></a>Синтаксис

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --- | --- |
| ИмяПроекта | (Обязательно) Проект, к которому необходимо добавить переадресации привязок. Параметр - имя_проекта сам является необязательным. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

## <a name="common-parameters"></a>Общие параметры

`Add-BindingRedirect`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```