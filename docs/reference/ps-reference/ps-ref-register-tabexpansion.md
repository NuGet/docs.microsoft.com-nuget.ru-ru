---
title: Справочник NuGet Register-TabExpansion PowerShell
description: Справочник по команде PowerShell Register-TabExpansion в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 14cda695677e1052c78169fda097b72b460a9d43
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327301"
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
| name | Необходимости Команда для регистрации расширений. Сам переключатель-имя является необязательным. |
| Определение | Необходимости Объект, описывающий аргумент в синтаксисе `@{'<parameter>' = {'<value1>', '<value2>', ...}}` , `<parameter>` где — имя изменяемого параметра, каждый `<value>` из которых предоставляет определенное расширение. Принимаются одинарные и двойные кавычки. |

Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.

## <a name="common-parameters"></a>Общие параметры

`Register-TabExpansion`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

Рассмотрим решение, содержащее три проекта с именами EventManager, Utilities и СпеЦиалпарсер. Разработчик часто использует `Update-Package` команду в разное время с каждым из этих проектов. Она легко `Update-Package` находит `-ProjectName` для аргумента автозавершение, поэтому ему не нужно вводить имя проекта каждый раз. 

Следующая команда затем регистрирует эти три имени проекта в качестве расширения для `-ProjectName` параметра:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Затем разработчик может ввести `Update-Package -ProjectName `, нажать клавишу TAB и увидеть расширения, предлагаемые в качестве параметров автоматического завершения:

![Пример использования командлета Register-TabExpansion](media/Register-TabExpansion-Example.png)
