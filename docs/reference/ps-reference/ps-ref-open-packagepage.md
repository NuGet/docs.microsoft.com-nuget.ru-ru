---
title: Справочник по PowerShell для Open-Паккажепаже
description: Справочник по команде PowerShell Open-Паккажепаже в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 39199ebfc37756ed40158a1c07afca7709067350
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384432"
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
| Id | Идентификатор пакета требуемого пакета. Сам переключатель-ID является необязательным. |
| {2&gt;Version&lt;2} | Версия пакета, по умолчанию — последняя версия. |
| Source | Источник пакета, по умолчанию выбранный источник в раскрывающемся списке Источник. |
| лицензия | Открывает браузер для URL-адреса лицензии пакета. Если ни лицензия, ни Репортабусе не указаны, браузер открывает URL-адрес проекта пакета. |
| репортабусе | Открывает браузер для URL-адреса сообщения о нарушении в пакете. Если ни лицензия, ни Репортабусе не указаны, браузер открывает URL-адрес проекта пакета. |
| PassThru | Отображает URL-адрес. Используйте with-WhatIf, чтобы отключить Открытие браузера. |

Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.

## <a name="common-parameters"></a>Общие параметры

`Open-PackagePage` поддерживает следующие [Общие параметры PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.

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