---
title: Заметки о выпуске 3.4.2 NuGet
description: Заметки о выпуске NuGet 3.4.2, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780249"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="c16f2-103">Заметки о выпуске 3.4.2 NuGet</span><span class="sxs-lookup"><span data-stu-id="c16f2-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="c16f2-104">[Заметки о](../release-notes/nuget-3.4.1.md)  |  выпуске 3.4.1 NuGet [Заметки о выпуске 3.4.3 NuGet](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="c16f2-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="c16f2-105">3.4.2 NuGet выпущен 8 апреля 2016 для устранения нескольких проблем, обнаруженных в выпуске 3,4 и 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="c16f2-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="c16f2-106">nuget.exe версия-кандидат 3.4.2 теперь доступна</span><span class="sxs-lookup"><span data-stu-id="c16f2-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="c16f2-107">Версию-кандидат nuget.exe 3.4.2 можно скачать [здесь](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="c16f2-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="c16f2-108">Обновления и улучшения</span><span class="sxs-lookup"><span data-stu-id="c16f2-108">Updates and Improvements</span></span>

* <span data-ttu-id="c16f2-109">Мы значительно улучшили производительность обновлений в определенном сценарии, где обновления для пакетов со схемами с глубокими зависимостями заняли много времени и зависы в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c16f2-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="c16f2-110">Восстановление NuGet без сетевого трафика составляет 2,5 x – 3 раза быстрее в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c16f2-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="c16f2-111">В дополнение к этому изменению мы устранили проблемы, при которых в пользовательском интерфейсе VS для выборки числа обновлений был выбран параметр сеть дважды.</span><span class="sxs-lookup"><span data-stu-id="c16f2-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="c16f2-112">Это было частично ответственным за некоторые проблемы с временем ожидания, возникшие у клиентов в 3.4/3.4.1.</span><span class="sxs-lookup"><span data-stu-id="c16f2-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="c16f2-113">Добавлена поддержка параметра no_proxy</span><span class="sxs-lookup"><span data-stu-id="c16f2-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="c16f2-114">Исправления</span><span class="sxs-lookup"><span data-stu-id="c16f2-114">Fixes</span></span>

* <span data-ttu-id="c16f2-115">Исправлена проблема, при которой источник nuget.org отсутствовал в параметрах NuGet или config после обновления до 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="c16f2-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="c16f2-116">Исправлена проблема, из-за которой изменение регистра в Финдпаккажесбид в 3.4.1 нарушает артефакт.</span><span class="sxs-lookup"><span data-stu-id="c16f2-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="c16f2-117">Исправлена проблема с FIPS, которая привела к сбоям при восстановлении NuGet с nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="c16f2-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="c16f2-118">Исправлена ошибка при просмотре источников с недопустимым URL-адресом значка.</span><span class="sxs-lookup"><span data-stu-id="c16f2-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="c16f2-119">Исправлены проблемы с слиянием версий и записей из "все источники".</span><span class="sxs-lookup"><span data-stu-id="c16f2-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="c16f2-120">Известные проблемы в 3.4.2 Windows x86 commandline (RC)</span><span class="sxs-lookup"><span data-stu-id="c16f2-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="c16f2-121">Эти проблемы будут устранены на следующей неделе до того, как будет достигнута RTM.</span><span class="sxs-lookup"><span data-stu-id="c16f2-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="c16f2-122">Выполнение восстановления NuGet в решении завершится ошибкой, если файл решения помещается в иерархию папок меньшего уровня, чем файлы проекта.</span><span class="sxs-lookup"><span data-stu-id="c16f2-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="c16f2-123">Выполнение команды NuGet DELETE для пакета с помощью веб-канала версии 2 завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="c16f2-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="c16f2-124">Вместо этого используйте канал версии 3.</span><span class="sxs-lookup"><span data-stu-id="c16f2-124">Use V3 feed instead.</span></span>


<span data-ttu-id="c16f2-125">Полный список исправлений и улучшений в этом выпуске см. [здесь](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="c16f2-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>