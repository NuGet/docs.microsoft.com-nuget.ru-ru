---
title: Заметки о выпуске NuGet 2.8.6
description: Заметки о выпуске для NuGet 2.8.6, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546495"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="1382f-103">Заметки о выпуске NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="1382f-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="1382f-104">[Заметки о выпуске NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [заметки о выпуске NuGet 2.8.7](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="1382f-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="1382f-105">NuGet 2.8.6 был выпущен 20 июля 2015 г. как незначительное обновление для наших 2.8.5 VSIX с некоторыми целевые исправления и улучшения для поддержки пакетов, которые затем могут доставляться с поддержкой модели разработки Windows 10 UWP.</span><span class="sxs-lookup"><span data-stu-id="1382f-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="1382f-106">Эта версия расширения диспетчера пакетов NuGet обеспечивает поддержку только для Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="1382f-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="1382f-107">В этом выпуске диалоговое окно диспетчера пакетов NuGet была добавлена поддержка для:</span><span class="sxs-lookup"><span data-stu-id="1382f-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="1382f-108">Появился UAP моникер целевой платформы для поддержки разработки приложений для Windows 10.</span><span class="sxs-lookup"><span data-stu-id="1382f-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="1382f-109">Конечные точки для версии 3 протокола NuGet</span><span class="sxs-lookup"><span data-stu-id="1382f-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="1382f-110">Поддержка [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion атрибут источники репозиториев.</span><span class="sxs-lookup"><span data-stu-id="1382f-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="1382f-111">Значение по умолчанию — «2»</span><span class="sxs-lookup"><span data-stu-id="1382f-111">Default value is "2"</span></span>
* <span data-ttu-id="1382f-112">Откат к удаленному репозиторию Если необходимый пакет версия недоступна в локальном кэше</span><span class="sxs-lookup"><span data-stu-id="1382f-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>