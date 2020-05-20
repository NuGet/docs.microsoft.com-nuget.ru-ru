---
title: Поддержка NuGet в системе проектов Visual Studio
description: Интеграция NuGet в систему проектов Visual Studio для сторонних типов проектов.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 00a64d95c943e9e5cb3a279358a6495125a1bd87
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495922"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="f232a-103">Поддержка NuGet в системе проектов Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f232a-103">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="f232a-104">Для поддержки сторонних типов проектов в Visual Studio в NuGet 3.x и более поздних версиях поддерживается [общая система проектов (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md). Кроме того, в NuGet 3.2 и более поздних версиях поддерживаются системы проектов, отличные от CPS.</span><span class="sxs-lookup"><span data-stu-id="f232a-104">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="f232a-105">Для интеграции с NuGet в системе проектов должна быть заявлена поддержка всех возможностей, описываемых в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="f232a-105">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="f232a-106">Чтобы пакеты можно было устанавливать в проекте, не объявляйте возможности, которых на самом деле нет в проекте.</span><span class="sxs-lookup"><span data-stu-id="f232a-106">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="f232a-107">Многие компоненты Visual Studio и других расширений используют возможности проектов, которые не обеспечиваются клиентом NuGet.</span><span class="sxs-lookup"><span data-stu-id="f232a-107">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="f232a-108">Неправильное объявление возможностей проекта может привести к тому, что эти компоненты не будут функционировать и у пользователей начнут возникать проблемы.</span><span class="sxs-lookup"><span data-stu-id="f232a-108">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="f232a-109">Объявление возможностей проекта</span><span class="sxs-lookup"><span data-stu-id="f232a-109">Advertise project capabilities</span></span>

<span data-ttu-id="f232a-110">Клиент NuGet определяет, какие пакеты совместимы с типом проекта, на основе [возможностей проекта](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), которые представлены в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="f232a-110">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="f232a-111">Функция</span><span class="sxs-lookup"><span data-stu-id="f232a-111">Capability</span></span> | <span data-ttu-id="f232a-112">Description</span><span class="sxs-lookup"><span data-stu-id="f232a-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f232a-113">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="f232a-113">AssemblyReferences</span></span> | <span data-ttu-id="f232a-114">Указывает, что проект поддерживает ссылки на сборки (отличные от WinRTReferences).</span><span class="sxs-lookup"><span data-stu-id="f232a-114">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="f232a-115">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="f232a-115">DeclaredSourceItems</span></span> | <span data-ttu-id="f232a-116">Указывает, что проект является стандартным проектом MSBuild (не DNX), в том плане, что исходные элементы объявляются в самом проекте.</span><span class="sxs-lookup"><span data-stu-id="f232a-116">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="f232a-117">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="f232a-117">UserSourceItems</span></span>|<span data-ttu-id="f232a-118">Указывает, что пользователю разрешено добавлять произвольные файлы в проект.</span><span class="sxs-lookup"><span data-stu-id="f232a-118">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="f232a-119">Для систем проектов на основе CPS реализация возможностей проекта, которые описываются далее в этом разделе, уже произведена.</span><span class="sxs-lookup"><span data-stu-id="f232a-119">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="f232a-120">См. раздел, посвященный [объявлению возможностей проекта в проектах CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span><span class="sxs-lookup"><span data-stu-id="f232a-120">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="f232a-121">Реализация класса VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="f232a-121">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="f232a-122">Класс `VsProjectCapabilitiesPresenceChecker` должен реализовывать интерфейс `IVsBooleanSymbolPresenceChecker`, который определен следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f232a-122">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

```cs
public interface IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// Checks whether the symbols defined may have changed since the last time
    /// this method was called.
    /// </summary>
    /// <param name="versionObject">
    /// The response version object assigned at the last call.
    /// May be null to get the initial version.
    /// At the conclusion of this method call, the reference may be changed so that on a subsequent call
    /// we know what version was last observed. The caller should treat this value as an opaque object,
    /// and should not assume any significance from whether the pointer changed or not.
    /// </param>
    /// <returns>
    /// <c>true</c> if the symbols defined may have changed since the last call to this method
    /// or if <paramref name="versionObject"/> was <c>null</c> upon entering this method.
    /// <c>false</c> if the responses would all be the same.
    /// </returns>
    bool HasChangedSince(ref object versionObject);

    /// <summary>
    /// Checks for the presence of a given symbol.
    /// </summary>
    /// <param name="symbol">The symbol to check for.</param>
    /// <returns><c>true</c> if the symbol is present; <c>false</c> otherwise.</returns>
    bool IsSymbolPresent(string symbol);
}
```

<span data-ttu-id="f232a-123">Вот пример реализации этого интерфейса:</span><span class="sxs-lookup"><span data-stu-id="f232a-123">A sample implementation of this interface would then be:</span></span>

```cs
class VsProjectCapabilitiesPresenceChecker : IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// The set of capabilities this project system actually has.
    /// This should be kept current, and honestly reflect what the project can do.
    /// </summary>
    private static readonly HashSet<string> ActualProjectCapabilities = new HashSet<string>(StringComparer.OrdinalIgnoreCase)
        {
            "AssemblyReferences",
            "DeclaredSourceItems",
            "UserSourceItems",
        };

    public bool HasChangedSince(ref object versionObject)
    {
        // If your project capabilities do not change over time while the project is open,
        // you may simply `return false;` from your `HasChangedSince` method.
        return false;
    }

    public bool IsSymbolPresent(string symbol)
    {
        return ActualProjectCapabilities.Contains(symbol);
    }
}
```

<span data-ttu-id="f232a-124">Не забудьте добавить возможности в набор `ActualProjectCapabilities` или удалить их из него с учетом того, какие возможности фактически поддерживает ваша система проектов.</span><span class="sxs-lookup"><span data-stu-id="f232a-124">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="f232a-125">Подробное описание см. в [документации по возможностям проектов](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="f232a-125">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="f232a-126">Реагирование на запросы</span><span class="sxs-lookup"><span data-stu-id="f232a-126">Responding to queries</span></span>

<span data-ttu-id="f232a-127">Эта возможность объявляется в проекте путем поддержки свойства `VSHPROPID_ProjectCapabilitiesChecker` посредством `IVsHierarchy::GetProperty`.</span><span class="sxs-lookup"><span data-stu-id="f232a-127">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="f232a-128">Должен возвращаться экземпляр интерфейса `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, который определен в сборке `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll`.</span><span class="sxs-lookup"><span data-stu-id="f232a-128">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="f232a-129">Чтобы сослаться на эту сборку, установите [соответствующий пакет NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span><span class="sxs-lookup"><span data-stu-id="f232a-129">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="f232a-130">Например, можно добавить следующий оператор `case` в оператор `switch` метода `IVsHierarchy::GetProperty`:</span><span class="sxs-lookup"><span data-stu-id="f232a-130">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="f232a-131">Поддержка DTE</span><span class="sxs-lookup"><span data-stu-id="f232a-131">DTE Support</span></span>

<span data-ttu-id="f232a-132">NuGet позволяет системе проектов добавлять ссылки, элементы содержимого и импорты MSBuild, вызывая [среду средств разработки](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), которая представляет собой интерфейс автоматизации Visual Studio верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="f232a-132">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="f232a-133">Среда средств разработки — это набор COM-интерфейсов. Они могут быть уже реализованы.</span><span class="sxs-lookup"><span data-stu-id="f232a-133">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="f232a-134">Если тип проекта основан на CPS, среда средств разработки реализуется автоматически.</span><span class="sxs-lookup"><span data-stu-id="f232a-134">If your project type is based on CPS, DTE is implemented for you.</span></span>
