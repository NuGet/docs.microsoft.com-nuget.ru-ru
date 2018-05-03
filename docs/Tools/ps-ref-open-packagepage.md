---
title: Справочник по PowerShell NuGet Open-PackagePage
description: Ссылка для команды PowerShell PackagePage откройте консоль диспетчера пакетов NuGet в Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: df4bea390105a7e3fc5d2abd476f2908d92bbcf8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (консоль диспетчера пакетов в Visual Studio)

*Рекомендуется использовать в 3.0 +; доступен только в пределах [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*

Запускает браузер по умолчанию проекта, лицензии или URL-адрес отчетов о нарушении для указанного пакета.

## <a name="syntax"></a>Синтаксис

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Идентификатор | Идентификатор пакета нужный пакет. — Идентификатор коммутатора сам является необязательным. |
| Версия | Версия пакета, по умолчанию используется последняя версия. |
| Исходный код | Источник пакета по умолчанию используется источник, выбранный в источнике раскрывающегося списка. |
| Лицензия | Открывает в браузере URL-адрес пакета лицензий. Если указан параметр - лицензии ни - ReportAbuse, в браузере будет открыта URL-адрес для пакета проекта. |
| ReportAbuse | Открывает в браузере URL-адрес пакета отчетов о нарушении. Если указан параметр - лицензии ни - ReportAbuse, в браузере будет открыта URL-адрес для пакета проекта. |
| Пропустить | Отображает URL-адрес; Используйте с - WhatIf, чтобы открыть браузер. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

## <a name="common-parameters"></a>Общие параметры

`Open-PackagePage` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

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