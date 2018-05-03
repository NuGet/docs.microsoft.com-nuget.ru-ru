---
title: Справочник по PowerShell для добавления BindingRedirect NuGet
description: Справочник по PowerShell BindingRedirect добавить команду в консоли диспетчера пакетов NuGet в Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7f1f2ef23e54ee48b577a2796b7f7b5f4c7eb284
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Добавить BindingRedirect (консоль диспетчера пакетов в Visual Studio)

*Доступен только в пределах [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*

Проверяет все сборки по пути вывода для проекта и добавляет перенаправления привязки в файле конфигурации приложения или веб-узла, при необходимости. Эта команда выполняется автоматически при установке пакета.

Привязку перенаправления и почему они используются Подробнее [Перенаправление версий сборок](/dotnet/framework/configure-apps/redirect-assembly-versions) в документации по .NET.

## <a name="syntax"></a>Синтаксис

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ИмяПроекта | (Обязательно) Проект, к которому необходимо добавить переадресации привязок. Параметр - имя_проекта сам является необязательным. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

## <a name="common-parameters"></a>Общие параметры

`Add-BindingRedirect` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```