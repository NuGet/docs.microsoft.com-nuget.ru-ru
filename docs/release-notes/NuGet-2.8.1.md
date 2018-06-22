---
title: Заметки о выпуске NuGet 2.8.1
description: Заметки о выпуске для NuGet 2.8.1, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8787aee36d31ed5d8071b35a8c243823029d135f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820525"
---
# <a name="nuget-281-release-notes"></a>Заметки о выпуске NuGet 2.8.1

[Заметки о выпуске NuGet 2.8](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 заметки о выпуске](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 был выпущен 2 апреля 2014 г.

## <a name="notable-features-in-the-release"></a>Возможности в выпуске

### <a name="support-for-windows-phone-81-projects"></a>Поддержка проектов Windows Phone 8.1
Теперь этот выпуск поддерживает следующие новые моникеров целевой платформы которые могут использоваться в проекты, предназначенные для Windows Phone 8.1:

* WindowsPhone81 / WP81 (для проектов на базе Silverlight для Windows Phone)
* WindowsPhoneApp81 / WPA81 (для проектов на базе WinRT приложения Windows Phone)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Обновление расширения WebMatrix NuGet
Этот выпуск содержит обновления для клиента NuGet в WebMatrix для [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1, после чего он обладает например XDT преобразования. Что более важно, 2.6.1 core обновления позволяет клиенту WebMatrix установить пакеты NuGet, которые содержат более поздних версиях `.nuspec` схемы, в том числе пакеты ASP.NET NuGet.

Дополнительные сведения об обновлении расширения WebMatrix видит конкретных [заметки о выпуске](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Исправления ошибок
Помимо этих функций этого выпуска NuGet включает исправления других ошибок. Произошли 16 общее проблемы, описанные в выпуске. Полный список рабочих элементов исправления в NuGet 2.8.1, представление [NuGet отслеживания проблем в этом выпуске](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Reshipping вместе с Visual Studio «14» CTP-версия
В Visual Studio «14» CTP-версии выпустила 3 июня 2014 г NuGet 2.8.1 поставляется в коробке. Он поддерживает функции остаются в par с другими 2.8.1 VSIXes такой файл для Visual Studio 2013.
