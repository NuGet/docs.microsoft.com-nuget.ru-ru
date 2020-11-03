---
title: Справочник по Register-TabExpansion PowerShell для NuGet
description: Справочник по Register-TabExpansion команде PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 9d5bae2878cb6bf0848bca9a5ed9af0fee61bb85
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237157"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="b8346-103">Register-TabExpansion (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="b8346-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b8346-104">*Доступно только в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="b8346-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="b8346-105">Регистрирует расширение вкладки для параметров указанной команды, например при использовании вкладки при вводе команды расширенные значения отображаются как доступные параметры для рассматриваемого параметра.</span><span class="sxs-lookup"><span data-stu-id="b8346-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="b8346-106">Все предыдущие расширения для команды перезаписываются.</span><span class="sxs-lookup"><span data-stu-id="b8346-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="b8346-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="b8346-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="b8346-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="b8346-108">Parameters</span></span>

| <span data-ttu-id="b8346-109">Параметр</span><span class="sxs-lookup"><span data-stu-id="b8346-109">Parameter</span></span> | <span data-ttu-id="b8346-110">Описание</span><span class="sxs-lookup"><span data-stu-id="b8346-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b8346-111">name</span><span class="sxs-lookup"><span data-stu-id="b8346-111">Name</span></span> | <span data-ttu-id="b8346-112">Необходимости Команда для регистрации расширений.</span><span class="sxs-lookup"><span data-stu-id="b8346-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="b8346-113">Сам переключатель-имя является необязательным.</span><span class="sxs-lookup"><span data-stu-id="b8346-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="b8346-114">Определение</span><span class="sxs-lookup"><span data-stu-id="b8346-114">Definition</span></span> | <span data-ttu-id="b8346-115">Необходимости Объект, описывающий аргумент в синтаксисе, `@{'<parameter>' = {'<value1>', '<value2>', ...}}` где `<parameter>` — имя изменяемого параметра, каждый из которых `<value>` предоставляет определенное расширение.</span><span class="sxs-lookup"><span data-stu-id="b8346-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="b8346-116">Принимаются одинарные и двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="b8346-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="b8346-117">Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="b8346-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="b8346-118">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="b8346-118">Common Parameters</span></span>

<span data-ttu-id="b8346-119">`Register-TabExpansion` поддерживает следующие [Общие параметры PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b8346-119">`Register-TabExpansion` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="b8346-120">Примеры</span><span class="sxs-lookup"><span data-stu-id="b8346-120">Examples</span></span>

<span data-ttu-id="b8346-121">Рассмотрим решение, содержащее три проекта с именами EventManager, Utilities и СпеЦиалпарсер.</span><span class="sxs-lookup"><span data-stu-id="b8346-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="b8346-122">Разработчик часто использует `Update-Package` команду в разное время с каждым из этих проектов.</span><span class="sxs-lookup"><span data-stu-id="b8346-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="b8346-123">Она легко находит `Update-Package` для аргумента автозавершение, `-ProjectName` поэтому ему не нужно вводить имя проекта каждый раз.</span><span class="sxs-lookup"><span data-stu-id="b8346-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="b8346-124">Следующая команда затем регистрирует эти три имени проекта в качестве расширения для `-ProjectName` параметра:</span><span class="sxs-lookup"><span data-stu-id="b8346-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="b8346-125">Затем разработчик может ввести `Update-Package -ProjectName ` , нажать клавишу TAB и увидеть расширения, предлагаемые в качестве параметров автоматического завершения:</span><span class="sxs-lookup"><span data-stu-id="b8346-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Пример использования Register-TabExpansion](media/Register-TabExpansion-Example.png)