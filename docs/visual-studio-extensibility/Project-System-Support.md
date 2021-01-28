---
title: Поддержка NuGet в системе проектов Visual Studio
description: Интеграция NuGet в систему проектов Visual Studio для сторонних типов проектов.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 7af330f88b47352666933598719d9c8f8cb66a78
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779405"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Поддержка NuGet в системе проектов Visual Studio

Для поддержки сторонних типов проектов в Visual Studio в NuGet 3.x и более поздних версиях поддерживается [общая система проектов (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md). Кроме того, в NuGet 3.2 и более поздних версиях поддерживаются системы проектов, отличные от CPS.

Для интеграции с NuGet в системе проектов должна быть заявлена поддержка всех возможностей, описываемых в этом разделе.

> [!Note]
> Чтобы пакеты можно было устанавливать в проекте, не объявляйте возможности, которых на самом деле нет в проекте. Многие компоненты Visual Studio и других расширений используют возможности проектов, которые не обеспечиваются клиентом NuGet. Неправильное объявление возможностей проекта может привести к тому, что эти компоненты не будут функционировать и у пользователей начнут возникать проблемы.

## <a name="advertise-project-capabilities"></a>Объявление возможностей проекта

Клиент NuGet определяет, какие пакеты совместимы с типом проекта, на основе [возможностей проекта](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), которые представлены в таблице ниже.

| Функция | Description |
| --- | --- |
| AssemblyReferences | Указывает, что проект поддерживает ссылки на сборки (отличные от WinRTReferences). |
| DeclaredSourceItems | Указывает, что проект является стандартным проектом MSBuild (не DNX), в том плане, что исходные элементы объявляются в самом проекте. |
| UserSourceItems|Указывает, что пользователю разрешено добавлять произвольные файлы в проект. |

Для систем проектов на основе CPS реализация возможностей проекта, которые описываются далее в этом разделе, уже произведена. См. раздел, посвященный [объявлению возможностей проекта в проектах CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>Реализация класса VsProjectCapabilitiesPresenceChecker

Класс `VsProjectCapabilitiesPresenceChecker` должен реализовывать интерфейс `IVsBooleanSymbolPresenceChecker`, который определен следующим образом:

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

Вот пример реализации этого интерфейса:

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

Не забудьте добавить возможности в набор `ActualProjectCapabilities` или удалить их из него с учетом того, какие возможности фактически поддерживает ваша система проектов. Подробное описание см. в [документации по возможностям проектов](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md).

## <a name="responding-to-queries"></a>Реагирование на запросы

Эта возможность объявляется в проекте путем поддержки свойства `VSHPROPID_ProjectCapabilitiesChecker` посредством `IVsHierarchy::GetProperty`. Должен возвращаться экземпляр интерфейса `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, который определен в сборке `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll`. Чтобы сослаться на эту сборку, установите [соответствующий пакет NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).

Например, можно добавить следующий оператор `case` в оператор `switch` метода `IVsHierarchy::GetProperty`:

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>Поддержка DTE

NuGet позволяет системе проектов добавлять ссылки, элементы содержимого и импорты MSBuild, вызывая [среду средств разработки](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), которая представляет собой интерфейс автоматизации Visual Studio верхнего уровня. Среда средств разработки — это набор COM-интерфейсов. Они могут быть уже реализованы.

Если тип проекта основан на CPS, среда средств разработки реализуется автоматически.
