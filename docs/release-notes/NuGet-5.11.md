---
title: заметки о выпуске NuGet 5,11
description: заметки о выпуске для NuGet 5,11, включая новые функции, исправления ошибок и dcr.
author: erdembayar
ms.author: eryondon
ms.date: 8/10/2021
ms.topic: conceptual
ms.openlocfilehash: 97b59be0fa3da2bfb788e540fef795522d938ed4
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/23/2021
ms.locfileid: "122728425"
---
# <a name="nuget-511-release-notes"></a>заметки о выпуске NuGet 5,11

Средства распространения NuGet:

| Версия NuGet | Доступно в версии Visual Studio | Доступно в пакетах SDK для .NET |
|:---|:---|:---|
| [**5.11.0**](https://nuget.org/downloads) | [Visual Studio 2019 версии 16,11](https://visualstudio.microsoft.com/downloads/) | [5.0.400](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> установлен с Visual Studio 2019 с рабочей нагрузкой .net Core
  
> [!NOTE]
> для Visual Studio 16,11, MSBuild 16,11 и .net 5.0.400 + требуется NuGet.exe 5,11 или более поздней версии.

## <a name="summary-whats-new-in-511"></a>Сводка: новые возможности в 5,11

### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

**Появились**

* сервис-> параметры-> строка NuGet диспетчер пакетов усечена — [#10779](https://github.com/NuGet/Home/issues/10779)

* Зависает при срабатывании события Паккажесмиссингстатусчанжед. [#10854](https://github.com/NuGet/Home/issues/10854)

* клиент NuGet игнорирует параметр NO_PROXY — [#10902](https://github.com/NuGet/Home/issues/10902)

**[Список всех проблем, исправленных в этом выпуске — 5,11](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTk5MDE)**

**[Список фиксаций в этом выпуске — 5,11](https://github.com/NuGet/NuGet.Client/compare/5.10.0.7240...5.11.0.17)**

## <a name="feedback-welcome"></a>Добро пожаловать на отзыв

Ваши отзывы очень важны для нас.  если в этом выпуске возникли какие либо проблемы, ознакомьтесь с нашими [проблемами GitHub](https://github.com/NuGet/Home/issues) и [Visual Studio разработчика Community](https://developercommunity.visualstudio.com/) для существующих проблем.  при возникновении новых проблем в NuGet сообщите об [ошибке GitHub](https://github.com/NuGet/Home/issues/new).
для получения общих проблем NuGet обратитесь к нам с помощью параметра [сообщить о проблеме](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) в избранной среде IDE в разделе **справка > сообщить о проблеме**.
