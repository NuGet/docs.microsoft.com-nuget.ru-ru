---
title: Заметки о выпуске 2.8.6 NuGet
description: Заметки о выпуске NuGet 2.8.6, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776706"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="c6377-103">Заметки о выпуске 2.8.6 NuGet</span><span class="sxs-lookup"><span data-stu-id="c6377-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="c6377-104">[Заметки о](../release-notes/nuget-2.8.5.md)  |  выпуске 2.8.5 NuGet [Заметки о выпуске 2.8.7 NuGet](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="c6377-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="c6377-105">2.8.6 NuGet была выпущена 20 июля 2015 в качестве дополнительного обновления для нашего 2.8.5 VSIX с некоторыми целевыми исправлениями и улучшениями для поддержки пакетов, которые могут доставляться с поддержкой модели разработки Windows 10 UWP.</span><span class="sxs-lookup"><span data-stu-id="c6377-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="c6377-106">Эта версия расширения диспетчера пакетов NuGet обеспечивает поддержку только для Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="c6377-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="c6377-107">В этом выпуске в диалоговом окне диспетчера пакетов NuGet добавлена поддержка:</span><span class="sxs-lookup"><span data-stu-id="c6377-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="c6377-108">Введен моникер целевой платформы UAP для поддержки разработки приложений Windows 10.</span><span class="sxs-lookup"><span data-stu-id="c6377-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="c6377-109">Конечные точки протокола NuGet версии 3</span><span class="sxs-lookup"><span data-stu-id="c6377-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="c6377-110">Поддержка атрибута [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) протоколверсион в источниках репозитория.</span><span class="sxs-lookup"><span data-stu-id="c6377-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="c6377-111">Значение по умолчанию — 2.</span><span class="sxs-lookup"><span data-stu-id="c6377-111">Default value is "2"</span></span>
* <span data-ttu-id="c6377-112">Возврат к удаленному репозиторию, если требуемая версия пакета недоступна в локальном кэше</span><span class="sxs-lookup"><span data-stu-id="c6377-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>