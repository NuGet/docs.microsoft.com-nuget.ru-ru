---
title: Справочник по PowerShell Add-BindingRedirect для NuGet
description: Справочник по команде PowerShell Add-BindingRedirect в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d3d156cf882229260e8cf55f8ece2804aec36dc9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384988"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (консоль диспетчера пакетов в Visual Studio)

*Доступно только в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows.*

Проверяет все сборки в пути вывода для проекта и добавляет перенаправления привязок в файл приложения или веб-конфигурации, где это необходимо. Эта команда выполняется автоматически при установке пакета.

Дополнительные сведения о перенаправлениях привязок и их использовании см. в статье [Перенаправление версий сборки](/dotnet/framework/configure-apps/redirect-assembly-versions) в документации по .NET.

## <a name="syntax"></a>Синтаксис

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ИмяПроекта | Необходимости Проект, к которому добавляются перенаправления привязок. Параметр-ProjectName является необязательным. |

Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.

## <a name="common-parameters"></a>Общие параметры

`Add-BindingRedirect` поддерживает следующие [Общие параметры PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```