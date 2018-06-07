---
title: Справочник по PowerShell NuGet Register-TabExpansion
description: Ссылка для команды Register TabExpansion PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8011c0e6aa951a32114d460803c493810964a7e0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818422"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="2cd75-103">Register-TabExpansion (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="2cd75-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="2cd75-104">*Доступен только в пределах [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="2cd75-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="2cd75-105">Регистрирует расширение по клавише tab для параметров указанной команды, таким образом, что при использовании вкладки при вводе команды развернутой значения отображаются как доступные варианты соответствующий параметр.</span><span class="sxs-lookup"><span data-stu-id="2cd75-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="2cd75-106">Будут перезаписаны все предыдущие расширения для команды.</span><span class="sxs-lookup"><span data-stu-id="2cd75-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="2cd75-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="2cd75-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="2cd75-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="2cd75-108">Parameters</span></span>

| <span data-ttu-id="2cd75-109">Параметр</span><span class="sxs-lookup"><span data-stu-id="2cd75-109">Parameter</span></span> | <span data-ttu-id="2cd75-110">Описание:</span><span class="sxs-lookup"><span data-stu-id="2cd75-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2cd75-111">name</span><span class="sxs-lookup"><span data-stu-id="2cd75-111">Name</span></span> | <span data-ttu-id="2cd75-112">(Обязательно) Команда, для которого необходимо зарегистрировать расширения.</span><span class="sxs-lookup"><span data-stu-id="2cd75-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="2cd75-113">-Имя коммутатора сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="2cd75-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="2cd75-114">Определение</span><span class="sxs-lookup"><span data-stu-id="2cd75-114">Definition</span></span> | <span data-ttu-id="2cd75-115">(Обязательно) Объект, описывающий аргументов в синтаксисе `@{'<parameter>' = {'<value1>', '<value2>', ...}}` где `<parameter>` имя параметра для изменения и каждого `<value>` предоставляет определенное расширение.</span><span class="sxs-lookup"><span data-stu-id="2cd75-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="2cd75-116">Принимаются одинарные и двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="2cd75-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="2cd75-117">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="2cd75-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="2cd75-118">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="2cd75-118">Common Parameters</span></span>

<span data-ttu-id="2cd75-119">`Register-TabExpansion` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="2cd75-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="2cd75-120">Примеры</span><span class="sxs-lookup"><span data-stu-id="2cd75-120">Examples</span></span>

<span data-ttu-id="2cd75-121">Рассмотрим решения, содержащего имена трех проектов EventManager, программы и SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="2cd75-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="2cd75-122">Часто разработчик использует `Update-Package` команду в разное время с каждым из этих проектов.</span><span class="sxs-lookup"><span data-stu-id="2cd75-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="2cd75-123">Она находит удобно иметь `Update-Package` команды предоставляют расширения автоматического завершения для `-ProjectName` аргумент, поэтому ей не нужно каждый раз вводить имя проекта.</span><span class="sxs-lookup"><span data-stu-id="2cd75-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="2cd75-124">Следующая команда, затем регистрирует эти имена трех проектов как расширение для `-ProjectName` параметр:</span><span class="sxs-lookup"><span data-stu-id="2cd75-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="2cd75-125">Разработчик может вводить `Update-Package -ProjectName `, нажмите клавишу Tab и расширения, будет предложена в качестве параметров автоматического заполнения в разделе:</span><span class="sxs-lookup"><span data-stu-id="2cd75-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Пример использования TabExpansion регистра](media/Register-TabExpansion-Example.png)
