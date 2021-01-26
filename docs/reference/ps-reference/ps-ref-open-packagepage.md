---
title: Справочник по Open-PackagePage PowerShell для NuGet
description: Справочник по Open-PackagePage команде PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d34a91007197f8004e4923deedb1cdb26d662d53
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780411"
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
| Версия | Версия пакета, по умолчанию — последняя версия. |
| Источник | Источник пакета, по умолчанию выбранный источник в раскрывающемся списке Источник. |
| Лицензия | Открывает браузер для URL-адреса лицензии пакета. Если ни лицензия, ни Репортабусе не указаны, браузер открывает URL-адрес проекта пакета. |
| репортабусе | Открывает браузер для URL-адреса сообщения о нарушении в пакете. Если ни лицензия, ни Репортабусе не указаны, браузер открывает URL-адрес проекта пакета. |
| PassThru | Отображает URL-адрес. Используйте with-WhatIf, чтобы отключить Открытие браузера. |

Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.

## <a name="common-parameters"></a>Общие параметры

`Open-PackagePage` поддерживает следующие [Общие параметры PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.

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