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
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="cdca4-103">Register-TabExpansion (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="cdca4-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="cdca4-104">*Доступно только в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="cdca4-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="cdca4-105">Регистрирует расширение вкладки для параметров указанной команды, например при использовании вкладки при вводе команды расширенные значения отображаются как доступные параметры для рассматриваемого параметра.</span><span class="sxs-lookup"><span data-stu-id="cdca4-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="cdca4-106">Все предыдущие расширения для команды перезаписываются.</span><span class="sxs-lookup"><span data-stu-id="cdca4-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="cdca4-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="cdca4-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="cdca4-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="cdca4-108">Parameters</span></span>

| <span data-ttu-id="cdca4-109">Параметр</span><span class="sxs-lookup"><span data-stu-id="cdca4-109">Parameter</span></span> | <span data-ttu-id="cdca4-110">Описание</span><span class="sxs-lookup"><span data-stu-id="cdca4-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cdca4-111">Name</span><span class="sxs-lookup"><span data-stu-id="cdca4-111">Name</span></span> | <span data-ttu-id="cdca4-112">Необходимости Команда для регистрации расширений.</span><span class="sxs-lookup"><span data-stu-id="cdca4-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="cdca4-113">Сам переключатель-имя является необязательным.</span><span class="sxs-lookup"><span data-stu-id="cdca4-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="cdca4-114">Определение</span><span class="sxs-lookup"><span data-stu-id="cdca4-114">Definition</span></span> | <span data-ttu-id="cdca4-115">Необходимости Объект, описывающий аргумент в синтаксисе `@{'<parameter>' = {'<value1>', '<value2>', ...}}` где `<parameter>` — имя изменяемого параметра, а каждый `<value>` предоставляет определенное расширение.</span><span class="sxs-lookup"><span data-stu-id="cdca4-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="cdca4-116">Принимаются одинарные и двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="cdca4-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="cdca4-117">Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="cdca4-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="cdca4-118">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="cdca4-118">Common Parameters</span></span>

<span data-ttu-id="cdca4-119">`Register-TabExpansion` поддерживает следующие [Общие параметры PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="cdca4-119">`Register-TabExpansion` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="cdca4-120">Примеры</span><span class="sxs-lookup"><span data-stu-id="cdca4-120">Examples</span></span>

<span data-ttu-id="cdca4-121">Рассмотрим решение, содержащее три проекта с именами EventManager, Utilities и СпеЦиалпарсер.</span><span class="sxs-lookup"><span data-stu-id="cdca4-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="cdca4-122">Разработчик часто использует команду `Update-Package` в разное время с каждым из этих проектов.</span><span class="sxs-lookup"><span data-stu-id="cdca4-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="cdca4-123">Она очень удобна для того, чтобы команда `Update-Package` предоставляющую автоматическое завершение для аргумента `-ProjectName`, поэтому ей не нужно вводить имя проекта каждый раз.</span><span class="sxs-lookup"><span data-stu-id="cdca4-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="cdca4-124">Следующая команда затем регистрирует эти три имени проекта в качестве расширения для параметра `-ProjectName`:</span><span class="sxs-lookup"><span data-stu-id="cdca4-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="cdca4-125">Затем разработчик может ввести `Update-Package -ProjectName `, нажать клавишу TAB и увидеть расширения, предлагаемые в качестве параметров автозавершения:</span><span class="sxs-lookup"><span data-stu-id="cdca4-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Пример использования командлета Register-TabExpansion](media/Register-TabExpansion-Example.png)
