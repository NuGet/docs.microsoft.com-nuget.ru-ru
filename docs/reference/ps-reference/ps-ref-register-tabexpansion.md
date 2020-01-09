---
title: Справочник NuGet Register-TabExpansion PowerShell
description: Справочник по команде PowerShell Register-TabExpansion в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 37aed96760e642b03c02bf31fe47a54f0e3cb74a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384458"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (консоль диспетчера пакетов в Visual Studio)

*Доступно только в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows.*

Регистрирует расширение вкладки для параметров указанной команды, например при использовании вкладки при вводе команды расширенные значения отображаются как доступные параметры для рассматриваемого параметра. Все предыдущие расширения для команды перезаписываются.

## <a name="syntax"></a>Синтаксис

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Name | Необходимости Команда для регистрации расширений. Сам переключатель-имя является необязательным. |
| Определение | Необходимости Объект, описывающий аргумент в синтаксисе `@{'<parameter>' = {'<value1>', '<value2>', ...}}` где `<parameter>` — имя изменяемого параметра, а каждый `<value>` предоставляет определенное расширение. Принимаются одинарные и двойные кавычки. |

Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.

## <a name="common-parameters"></a>Общие параметры

`Register-TabExpansion` поддерживает следующие [Общие параметры PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

Рассмотрим решение, содержащее три проекта с именами EventManager, Utilities и СпеЦиалпарсер. Разработчик часто использует команду `Update-Package` в разное время с каждым из этих проектов. Она очень удобна для того, чтобы команда `Update-Package` предоставляющую автоматическое завершение для аргумента `-ProjectName`, поэтому ей не нужно вводить имя проекта каждый раз. 

Следующая команда затем регистрирует эти три имени проекта в качестве расширения для параметра `-ProjectName`:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Затем разработчик может ввести `Update-Package -ProjectName `, нажать клавишу TAB и увидеть расширения, предлагаемые в качестве параметров автозавершения:

![Пример использования командлета Register-TabExpansion](media/Register-TabExpansion-Example.png)
