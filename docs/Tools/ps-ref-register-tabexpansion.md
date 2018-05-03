---
title: Справочник по PowerShell NuGet Register-TabExpansion
description: Ссылка для команды Register TabExpansion PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 02f6d4ecd246b7ce5425cf56ade10789cf03113c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (консоль диспетчера пакетов в Visual Studio)

*Доступен только в пределах [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*

Регистрирует расширение по клавише tab для параметров указанной команды, таким образом, что при использовании вкладки при вводе команды развернутой значения отображаются как доступные варианты соответствующий параметр. Будут перезаписаны все предыдущие расширения для команды.

## <a name="syntax"></a>Синтаксис

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| name | (Обязательно) Команда, для которого необходимо зарегистрировать расширения. -Имя коммутатора сам является необязательным. |
| Определение | (Обязательно) Объект, описывающий аргументов в синтаксисе `@{'<parameter>' = {'<value1>', '<value2>', ...}}` где `<parameter>` имя параметра для изменения и каждого `<value>` предоставляет определенное расширение. Принимаются одинарные и двойные кавычки. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

## <a name="common-parameters"></a>Общие параметры

`Register-TabExpansion` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

Рассмотрим решения, содержащего имена трех проектов EventManager, программы и SpecialParser. Часто разработчик использует `Update-Package` команду в разное время с каждым из этих проектов. Она находит удобно иметь `Update-Package` команды предоставляют расширения автоматического завершения для `-ProjectName` аргумент, поэтому ей не нужно каждый раз вводить имя проекта. 

Следующая команда, затем регистрирует эти имена трех проектов как расширение для `-ProjectName` параметр:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Разработчик может вводить `Update-Package -ProjectName `, нажмите клавишу Tab и расширения, будет предложена в качестве параметров автоматического заполнения в разделе:

![Пример использования TabExpansion регистра](media/Register-TabExpansion-Example.png)
