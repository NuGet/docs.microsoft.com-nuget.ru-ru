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
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="bb96e-103">Register-TabExpansion (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="bb96e-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="bb96e-104">*Доступно только в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="bb96e-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="bb96e-105">Регистрирует расширение вкладки для параметров указанной команды, например при использовании вкладки при вводе команды расширенные значения отображаются как доступные параметры для рассматриваемого параметра.</span><span class="sxs-lookup"><span data-stu-id="bb96e-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="bb96e-106">Все предыдущие расширения для команды перезаписываются.</span><span class="sxs-lookup"><span data-stu-id="bb96e-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="bb96e-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="bb96e-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="bb96e-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="bb96e-108">Parameters</span></span>

| <span data-ttu-id="bb96e-109">Параметр</span><span class="sxs-lookup"><span data-stu-id="bb96e-109">Parameter</span></span> | <span data-ttu-id="bb96e-110">Описание</span><span class="sxs-lookup"><span data-stu-id="bb96e-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bb96e-111">name</span><span class="sxs-lookup"><span data-stu-id="bb96e-111">Name</span></span> | <span data-ttu-id="bb96e-112">Необходимости Команда для регистрации расширений.</span><span class="sxs-lookup"><span data-stu-id="bb96e-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="bb96e-113">Сам переключатель-имя является необязательным.</span><span class="sxs-lookup"><span data-stu-id="bb96e-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="bb96e-114">Определение</span><span class="sxs-lookup"><span data-stu-id="bb96e-114">Definition</span></span> | <span data-ttu-id="bb96e-115">Необходимости Объект, описывающий аргумент в синтаксисе `@{'<parameter>' = {'<value1>', '<value2>', ...}}` , `<parameter>` где — имя изменяемого параметра, каждый `<value>` из которых предоставляет определенное расширение.</span><span class="sxs-lookup"><span data-stu-id="bb96e-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="bb96e-116">Принимаются одинарные и двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="bb96e-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="bb96e-117">Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="bb96e-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="bb96e-118">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="bb96e-118">Common Parameters</span></span>

<span data-ttu-id="bb96e-119">`Register-TabExpansion`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="bb96e-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="bb96e-120">Примеры</span><span class="sxs-lookup"><span data-stu-id="bb96e-120">Examples</span></span>

<span data-ttu-id="bb96e-121">Рассмотрим решение, содержащее три проекта с именами EventManager, Utilities и СпеЦиалпарсер.</span><span class="sxs-lookup"><span data-stu-id="bb96e-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="bb96e-122">Разработчик часто использует `Update-Package` команду в разное время с каждым из этих проектов.</span><span class="sxs-lookup"><span data-stu-id="bb96e-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="bb96e-123">Она легко `Update-Package` находит `-ProjectName` для аргумента автозавершение, поэтому ему не нужно вводить имя проекта каждый раз.</span><span class="sxs-lookup"><span data-stu-id="bb96e-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="bb96e-124">Следующая команда затем регистрирует эти три имени проекта в качестве расширения для `-ProjectName` параметра:</span><span class="sxs-lookup"><span data-stu-id="bb96e-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="bb96e-125">Затем разработчик может ввести `Update-Package -ProjectName `, нажать клавишу TAB и увидеть расширения, предлагаемые в качестве параметров автоматического завершения:</span><span class="sxs-lookup"><span data-stu-id="bb96e-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Пример использования командлета Register-TabExpansion](media/Register-TabExpansion-Example.png)
