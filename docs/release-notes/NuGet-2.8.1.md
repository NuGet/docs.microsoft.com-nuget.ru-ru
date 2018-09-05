---
title: Заметки о выпуске NuGet 2.8.1
description: Заметки о выпуске для NuGet 2.8.1, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545243"
---
# <a name="nuget-281-release-notes"></a>Заметки о выпуске NuGet 2.8.1

[Заметки о выпуске NuGet 2.8](../release-notes/nuget-2.8.md) | [заметки о выпуске NuGet 2.8.2](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 был выпущен 2 апреля 2014 г.

## <a name="notable-features-in-the-release"></a>Важные возможности в выпуске

### <a name="support-for-windows-phone-81-projects"></a>Поддержка проектов Windows Phone 8.1
Теперь этот выпуск поддерживает следующие новые моникеров целевой платформы которых может использоваться для проектов, предназначенные для Windows Phone 8.1:

* WindowsPhone81 / WP81 (для проектов на базе Silverlight Windows Phone)
* WindowsPhoneApp81 / WPA81 (для проектов на базе WinRT приложения Windows Phone)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Обновление расширения WebMatrix NuGet
Этот выпуск обновляет в WebMatrix для клиента NuGet [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 и с его такие функции преобразования XDT. Что более важно, 2.6.1 core обновления позволяет клиенту WebMatrix установки пакетов NuGet, которые содержат более поздних версиях `.nuspec` схемы, в том числе пакеты ASP.NET NuGet.

Дополнительные сведения об обновлении расширения WebMatrix см. в разделе их [заметки о выпуске](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Исправления ошибок
Помимо этих функций в этот выпуск NuGet включает другие исправления ошибок. Возникали 16 общее проблемы, описанной в выпуске. Полный список рабочих элементов исправленные в NuGet 2.8.1, пожалуйста представление [Issue Tracker NuGet для этого выпуска](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Reshipping с помощью Visual Studio «14» CTP-версии
В Visual Studio «14» CTP, выпущенную 3 июня 2014 года NuGet 2.8.1 поставляется в поле. Он поддерживает функции остаются в одном уровне с другими 2.8.1 VSIXes, например в каталог для Visual Studio 2013.
