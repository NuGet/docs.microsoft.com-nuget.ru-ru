---
title: Справочник по PowerShell для Open-Паккажепаже
description: Справочник по команде PowerShell Open-Паккажепаже в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0237c23d81000a1d58264cc0ab48c73d819d0e5a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327381"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (консоль диспетчера пакетов в Visual Studio)

*Не рекомендуется в 3.0 +; доступно только в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows.*

Запускает браузер по умолчанию с проектом, лицензией или URL-адресом сообщения о нарушении для указанного пакета.

## <a name="syntax"></a>Синтаксис

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Идентификатор | Идентификатор пакета требуемого пакета. Сам переключатель-ID является необязательным. |
| Версия | Версия пакета, по умолчанию — последняя версия. |
| Source | Источник пакета, по умолчанию выбранный источник в раскрывающемся списке Источник. |
| Лицензия | Открывает браузер для URL-адреса лицензии пакета. Если ни лицензия, ни Репортабусе не указаны, браузер открывает URL-адрес проекта пакета. |
| репортабусе | Открывает браузер для URL-адреса сообщения о нарушении в пакете. Если ни лицензия, ни Репортабусе не указаны, браузер открывает URL-адрес проекта пакета. |
| Пропустить | Отображает URL-адрес. Используйте with-WhatIf, чтобы отключить Открытие браузера. |

Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.

## <a name="common-parameters"></a>Общие параметры

`Open-PackagePage`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.

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