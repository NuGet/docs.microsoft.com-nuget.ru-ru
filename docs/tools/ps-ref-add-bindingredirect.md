---
title: Справочник по PowerShell для добавления BindingRedirect NuGet
description: Справочник по PowerShell BindingRedirect добавить команду в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f3addd95b64d78eac201deeb2c64915ea935cd71
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817627"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (консоль диспетчера пакетов в Visual Studio)

*Доступен только в пределах [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*

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

`Add-BindingRedirect` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```