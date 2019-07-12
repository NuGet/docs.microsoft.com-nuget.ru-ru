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
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="ce416-103">Register-TabExpansion (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="ce416-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ce416-104">*Доступен только в пределах [консоль диспетчера пакетов](package-manager-console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="ce416-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="ce416-105">Регистрирует расширение функций клавиши tab для параметров указанной команды, таким образом, что при использовании Tab при вводе команды развернутого значения отображаются как доступные для в соответствующий параметр.</span><span class="sxs-lookup"><span data-stu-id="ce416-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="ce416-106">Будут перезаписаны все предыдущие расширения для команды.</span><span class="sxs-lookup"><span data-stu-id="ce416-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="ce416-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="ce416-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="ce416-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="ce416-108">Parameters</span></span>

| <span data-ttu-id="ce416-109">Параметр</span><span class="sxs-lookup"><span data-stu-id="ce416-109">Parameter</span></span> | <span data-ttu-id="ce416-110">Описание</span><span class="sxs-lookup"><span data-stu-id="ce416-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ce416-111">name</span><span class="sxs-lookup"><span data-stu-id="ce416-111">Name</span></span> | <span data-ttu-id="ce416-112">(Обязательно) Команда, в котором требуется зарегистрировать расширения.</span><span class="sxs-lookup"><span data-stu-id="ce416-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="ce416-113">-Имя коммутатора, сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="ce416-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="ce416-114">Определение</span><span class="sxs-lookup"><span data-stu-id="ce416-114">Definition</span></span> | <span data-ttu-id="ce416-115">(Обязательно) Объект, описывающий аргумент в синтаксисе `@{'<parameter>' = {'<value1>', '<value2>', ...}}` где `<parameter>` — это имя параметра для изменения, и каждый `<value>` предоставляет определенное расширение.</span><span class="sxs-lookup"><span data-stu-id="ce416-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="ce416-116">Принимаются одинарные и двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="ce416-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="ce416-117">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="ce416-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ce416-118">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="ce416-118">Common Parameters</span></span>

<span data-ttu-id="ce416-119">`Register-TabExpansion` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="ce416-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ce416-120">Примеры</span><span class="sxs-lookup"><span data-stu-id="ce416-120">Examples</span></span>

<span data-ttu-id="ce416-121">Рассмотрим решения, содержащего имена трех проектов EventManager, служебные программы и SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="ce416-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="ce416-122">Часто разработчик использует `Update-Package` команду в разное время с каждым из этих проектов.</span><span class="sxs-lookup"><span data-stu-id="ce416-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="ce416-123">Она находит для удобства `Update-Package` команды предоставляют расширения автоматического завершения для `-ProjectName` аргумент, поэтому она не нужно вводить имя проекта каждый раз.</span><span class="sxs-lookup"><span data-stu-id="ce416-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="ce416-124">Следующая команда, затем регистрирует эти имена трех проектов как расширение слова для `-ProjectName` параметр:</span><span class="sxs-lookup"><span data-stu-id="ce416-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="ce416-125">Разработчик может вводить `Update-Package -ProjectName `, нажмите клавишу Tab и расширения, предлагаемые как варианты автозавершения см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="ce416-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Пример использования TabExpansion регистра](media/Register-TabExpansion-Example.png)
