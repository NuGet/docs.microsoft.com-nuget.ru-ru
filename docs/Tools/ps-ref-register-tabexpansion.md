---
title: "Справочник по PowerShell NuGet Register-TabExpansion | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Ссылка для команды Register TabExpansion PowerShell в консоли диспетчера пакетов NuGet в Visual Studio."
keywords: "Пакет NuGet консоли диспетчера, команд NuGet Powershell, справочник по NuGet Powershell, TabExpansion регистра"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5691c07f9efef4bfd12680421f3b02c5a523eb6f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (консоль диспетчера пакетов в Visual Studio)

*Доступен только в пределах [консоль диспетчера пакетов NuGet](Package-Manager-Console.md) в Visual Studio в Windows.*

Регистрирует расширение по клавише tab для параметров указанной команды, таким образом, что при использовании вкладки при вводе команды развернутой значения отображаются как доступные варианты соответствующий параметр. Будут перезаписаны все предыдущие расширения для команды.

## <a name="syntax"></a>Синтаксис

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --- | --- |
| name | (Обязательно) Команда, для которого необходимо зарегистрировать расширения. -Имя коммутатора сам является необязательным. |
| Определение | (Обязательно) Объект, описывающий аргументов в синтаксисе `@{'<parameter>' = {'<value1>', '<value2>', ...}}` где `<parameter>` имя параметра для изменения и каждого `<value>` предоставляет определенное расширение. Принимаются одинарные и двойные кавычки. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

## <a name="common-parameters"></a>Общие параметры

`Register-TabExpansion`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

Рассмотрим решения, содержащего имена трех проектов EventManager, программы и SpecialParser. Часто разработчик использует `Update-Package` команду в разное время с каждым из этих проектов. Она находит удобно иметь `Update-Package` команды предоставляют расширения автоматического завершения для `-ProjectName` аргумент, поэтому ей не нужно каждый раз вводить имя проекта. 

Следующая команда, затем регистрирует эти имена трех проектов как расширение для `-ProjectName` параметр:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Разработчик может вводить `Update-Package -ProjectName `, нажмите клавишу Tab и расширения, будет предложена в качестве параметров автоматического заполнения в разделе:

![Пример использования TabExpansion регистра](media/Register-TabExpansion-Example.png)
