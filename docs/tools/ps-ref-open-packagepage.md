---
title: Справочник по PowerShell NuGet открытым PackagePage
description: Справочник по PowerShell открытым PackagePage команду в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0325aa4ddd718a901dd6a09cdf86cae260e326ab
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547172"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (консоль диспетчера пакетов в Visual Studio)

*Рекомендуется использовать в 3.0 +; доступен только в пределах [консоли диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*

Запускает браузер по умолчанию проекта, лицензий или URL-адрес отчета о нарушении для указанного пакета.

## <a name="syntax"></a>Синтаксис

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Идентификатор | Идентификатор пакета нужного пакета. — Идентификатор сам является необязательным. |
| Версия | Версия пакета, по умолчанию до последней версии. |
| Исходный код | Источник пакета по умолчанию используется источник, выбранный в раскрывающемся списке источнике. |
| Лицензия | Открывает в браузере URL-адрес для лицензии пакета. Если не указаны ни - лицензии, ни - ReportAbuse, в браузере откроется URL-адрес для пакета проекта. |
| ReportAbuse | Открывает в браузере URL-адрес пакета отчетов о нарушении. Если не указаны ни - лицензии, ни - ReportAbuse, в браузере откроется URL-адрес для пакета проекта. |
| Пропустить | Отображает URL-адрес; Используйте с помощью - WhatIf, чтобы открывать обозреватель. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

## <a name="common-parameters"></a>Общие параметры

`Open-PackagePage` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладки, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```