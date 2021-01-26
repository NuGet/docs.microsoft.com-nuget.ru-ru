---
title: Заметки о выпуске 2.8.1 NuGet
description: Заметки о выпуске NuGet 2.8.1, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776769"
---
# <a name="nuget-281-release-notes"></a>Заметки о выпуске 2.8.1 NuGet

[Заметки о](../release-notes/nuget-2.8.md)  |  выпуске NuGet 2,8 [Заметки о выпуске 2.8.2 NuGet](../release-notes/nuget-2.8.2.md)

2.8.1 NuGet выпущен 2 апреля 2014 г.

## <a name="notable-features-in-the-release"></a>Важные функции в выпуске

### <a name="support-for-windows-phone-81-projects"></a>Поддержка проектов Windows Phone 8,1
Этот выпуск теперь поддерживает следующие новые моникеры целевой платформы, которые можно использовать для назначения проектов Windows Phone 8,1:

* WindowsPhone81/WP81 (для проектов Windows Phone на основе Silverlight)
* WindowsPhoneApp81/WPA81 (для проектов приложений на основе WinRT Windows Phone)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Обновление расширения WebMatrix для NuGet
Этот выпуск обновляет клиент NuGet, находящийся в WebMatrix, в [NuGet. Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 и включает в себя такие функции, как преобразование xdt. Что более важно, обновление 2.6.1 Core позволяет клиенту WebMatrix устанавливать пакеты NuGet, содержащие более новые версии `.nuspec` схемы, включая пакеты nuget ASP.NET.

Дополнительные сведения об обновлении расширения WebMatrix см. в соответствующих [заметках о выпуске](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Исправления ошибок
Помимо этих функций, в этом выпуске NuGet имеются другие исправления ошибок. В выпуске было решено 16 общих проблем. Полный список рабочих элементов, исправленных в NuGet 2.8.1, см. в [этом выпуске](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Перепоставка с помощью Visual Studio "14" CTP
В Visual Studio «14» CTP-версии, выпущенной 3 июня 2014, в поле поставляются пакеты NuGet 2.8.1. Функции, которые он поддерживает, остаются в неизменном виде с другими 2.8.1 VSIX, такими как для Visual Studio 2013.
