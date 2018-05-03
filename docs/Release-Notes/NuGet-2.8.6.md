---
title: Заметки о выпуске NuGet 2.8.6
description: Заметки о выпуске для NuGet 2.8.6, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ee801a0edfe22888d65506cea557fd9c79dcf7bd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="9ea4c-103">Заметки о выпуске NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="9ea4c-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="9ea4c-104">[Заметки о выпуске NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 заметки о выпуске](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="9ea4c-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="9ea4c-105">NuGet 2.8.6 был выпущен 20 июля 2015 г. как незначительное обновление для наших 2.8.5 VSIX с некоторыми целевой исправления и улучшения для поддержки пакетов, которые могут доставляться с поддержкой модели разработки Windows 10 UWP.</span><span class="sxs-lookup"><span data-stu-id="9ea4c-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="9ea4c-106">Эта версия расширения диспетчера пакетов NuGet обеспечивает поддержку только для Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="9ea4c-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="9ea4c-107">В этом выпуске диспетчер пакетов NuGet диалогового окна имел добавлена поддержка для:</span><span class="sxs-lookup"><span data-stu-id="9ea4c-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="9ea4c-108">Появился UAP моникер целевой платформы для разработки приложений Windows 10.</span><span class="sxs-lookup"><span data-stu-id="9ea4c-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="9ea4c-109">Протокол NuGet версии 3-конечные точки</span><span class="sxs-lookup"><span data-stu-id="9ea4c-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="9ea4c-110">Поддержка [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion атрибут источникам репозиториев.</span><span class="sxs-lookup"><span data-stu-id="9ea4c-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="9ea4c-111">Значение по умолчанию — «2»</span><span class="sxs-lookup"><span data-stu-id="9ea4c-111">Default value is "2"</span></span>
* <span data-ttu-id="9ea4c-112">Будет использоваться предыдущий удаленный репозиторий, если версия требуемый пакет недоступен в локальном кэше</span><span class="sxs-lookup"><span data-stu-id="9ea4c-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>