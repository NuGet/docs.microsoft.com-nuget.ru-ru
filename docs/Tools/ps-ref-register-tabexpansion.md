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
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="fd825-104">Register-TabExpansion (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="fd825-104">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="fd825-105">*Доступен только в пределах [консоль диспетчера пакетов NuGet](Package-Manager-Console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="fd825-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="fd825-106">Регистрирует расширение по клавише tab для параметров указанной команды, таким образом, что при использовании вкладки при вводе команды развернутой значения отображаются как доступные варианты соответствующий параметр.</span><span class="sxs-lookup"><span data-stu-id="fd825-106">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="fd825-107">Будут перезаписаны все предыдущие расширения для команды.</span><span class="sxs-lookup"><span data-stu-id="fd825-107">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="fd825-108">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="fd825-108">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="fd825-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="fd825-109">Parameters</span></span>

| <span data-ttu-id="fd825-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="fd825-110">Parameter</span></span> | <span data-ttu-id="fd825-111">Описание:</span><span class="sxs-lookup"><span data-stu-id="fd825-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fd825-112">name</span><span class="sxs-lookup"><span data-stu-id="fd825-112">Name</span></span> | <span data-ttu-id="fd825-113">(Обязательно) Команда, для которого необходимо зарегистрировать расширения.</span><span class="sxs-lookup"><span data-stu-id="fd825-113">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="fd825-114">-Имя коммутатора сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="fd825-114">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="fd825-115">Определение</span><span class="sxs-lookup"><span data-stu-id="fd825-115">Definition</span></span> | <span data-ttu-id="fd825-116">(Обязательно) Объект, описывающий аргументов в синтаксисе `@{'<parameter>' = {'<value1>', '<value2>', ...}}` где `<parameter>` имя параметра для изменения и каждого `<value>` предоставляет определенное расширение.</span><span class="sxs-lookup"><span data-stu-id="fd825-116">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="fd825-117">Принимаются одинарные и двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="fd825-117">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="fd825-118">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="fd825-118">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="fd825-119">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="fd825-119">Common Parameters</span></span>

<span data-ttu-id="fd825-120">`Register-TabExpansion`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="fd825-120">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="fd825-121">Примеры</span><span class="sxs-lookup"><span data-stu-id="fd825-121">Examples</span></span>

<span data-ttu-id="fd825-122">Рассмотрим решения, содержащего имена трех проектов EventManager, программы и SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="fd825-122">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="fd825-123">Часто разработчик использует `Update-Package` команду в разное время с каждым из этих проектов.</span><span class="sxs-lookup"><span data-stu-id="fd825-123">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="fd825-124">Она находит удобно иметь `Update-Package` команды предоставляют расширения автоматического завершения для `-ProjectName` аргумент, поэтому ей не нужно каждый раз вводить имя проекта.</span><span class="sxs-lookup"><span data-stu-id="fd825-124">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="fd825-125">Следующая команда, затем регистрирует эти имена трех проектов как расширение для `-ProjectName` параметр:</span><span class="sxs-lookup"><span data-stu-id="fd825-125">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="fd825-126">Разработчик может вводить `Update-Package -ProjectName `, нажмите клавишу Tab и расширения, будет предложена в качестве параметров автоматического заполнения в разделе:</span><span class="sxs-lookup"><span data-stu-id="fd825-126">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Пример использования TabExpansion регистра](media/Register-TabExpansion-Example.png)
