---
title: Справочник по PowerShell NuGet Register-TabExpansion
description: Справочник по PowerShell Register-TabExpansion команду в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8adb80af85e2e32fa8c35e5272cf90ff0c0ddcbb
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842487"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (консоль диспетчера пакетов в Visual Studio)

*Доступен только в пределах [консоль диспетчера пакетов](package-manager-console.md) в Visual Studio в Windows.*

Регистрирует расширение функций клавиши tab для параметров указанной команды, таким образом, что при использовании Tab при вводе команды развернутого значения отображаются как доступные для в соответствующий параметр. Будут перезаписаны все предыдущие расширения для команды.

## <a name="syntax"></a>Синтаксис

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| name | (Обязательно) Команда, в котором требуется зарегистрировать расширения. -Имя коммутатора, сам является необязательным. |
| Определение | (Обязательно) Объект, описывающий аргумент в синтаксисе `@{'<parameter>' = {'<value1>', '<value2>', ...}}` где `<parameter>` — это имя параметра для изменения, и каждый `<value>` предоставляет определенное расширение. Принимаются одинарные и двойные кавычки. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

## <a name="common-parameters"></a>Общие параметры

`Register-TabExpansion` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

Рассмотрим решения, содержащего имена трех проектов EventManager, служебные программы и SpecialParser. Часто разработчик использует `Update-Package` команду в разное время с каждым из этих проектов. Она находит для удобства `Update-Package` команды предоставляют расширения автоматического завершения для `-ProjectName` аргумент, поэтому она не нужно вводить имя проекта каждый раз. 

Следующая команда, затем регистрирует эти имена трех проектов как расширение слова для `-ProjectName` параметр:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Разработчик может вводить `Update-Package -ProjectName `, нажмите клавишу Tab и расширения, предлагаемые как варианты автозавершения см. в разделе:

![Пример использования TabExpansion регистра](media/Register-TabExpansion-Example.png)
