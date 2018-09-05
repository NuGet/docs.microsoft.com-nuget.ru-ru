---
title: Заметки о выпуске NuGet 3.4.2
description: Заметки о выпуске для NuGet 3.4.2, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549155"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="810b2-103">Заметки о выпуске NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="810b2-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="810b2-104">[Заметки о выпуске NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [заметки о выпуске NuGet 3.4.3](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="810b2-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="810b2-105">NuGet 3.4.2 был выпущен 8 апреля 2016 г. решить некоторые проблемы, которые были определены в 3.4 и 3.4.1 выпуска.</span><span class="sxs-lookup"><span data-stu-id="810b2-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="810b2-106">версия-Кандидат NuGet.exe 3.4.2 доступна</span><span class="sxs-lookup"><span data-stu-id="810b2-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="810b2-107">Можно загрузить версию-кандидат nuget.exe 3.4.2 [здесь](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="810b2-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="810b2-108">Обновления и улучшения</span><span class="sxs-lookup"><span data-stu-id="810b2-108">Updates and Improvements</span></span>

* <span data-ttu-id="810b2-109">Мы значительно улучшили производительность обновления в конкретной ситуации, где обновлений для пакетов с помощью графов зависимостей глубокого занимает очень много времени и зависание Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="810b2-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="810b2-110">Восстановление NuGet без сетевого трафика — два с половиной раза — в 3 раза быстрее в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="810b2-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="810b2-111">Помимо этого изменения мы устранили проблему где мы попадание сети, дважды в том случае, когда получение обновления число в пользовательском Интерфейсе VS.</span><span class="sxs-lookup"><span data-stu-id="810b2-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="810b2-112">Частично это отвечал за некоторые клиенты проблемы времени ожидания, 3.4 или 3.4.1 опытом.</span><span class="sxs-lookup"><span data-stu-id="810b2-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="810b2-113">Добавлена поддержка параметра no_proxy</span><span class="sxs-lookup"><span data-stu-id="810b2-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="810b2-114">Исправления</span><span class="sxs-lookup"><span data-stu-id="810b2-114">Fixes</span></span>

* <span data-ttu-id="810b2-115">Устранена проблема, где nuget.org источник отсутствует в параметрах NuGet или конфигурации после обновления до 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="810b2-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="810b2-116">Устранена проблема, где изменение регистра FindPackagesById в 3.4.1 нарушает Artifactory.</span><span class="sxs-lookup"><span data-stu-id="810b2-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="810b2-117">Исправлена проблема с FIPS, вызвавшего сбоев с помощью функции восстановления NuGet с nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="810b2-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="810b2-118">Исправлена ошибка, когда Просмотр источников с помощью URL-адрес Недопустимый значок.</span><span class="sxs-lookup"><span data-stu-id="810b2-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="810b2-119">Устранены проблемы со средствами слияния версий и операции из «Все источники».</span><span class="sxs-lookup"><span data-stu-id="810b2-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="810b2-120">Известные проблемы в разделе 3.4.2 командной строки Windows x86 (RC)</span><span class="sxs-lookup"><span data-stu-id="810b2-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="810b2-121">Эти проблемы будут исправлены ранний следующей недели, прежде чем мы получаем RTM.</span><span class="sxs-lookup"><span data-stu-id="810b2-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="810b2-122">Выполнение восстановления nuget над решением, завершится ошибкой, если файл решения помещается в нижнем иерархии папок, чем файлы проекта.</span><span class="sxs-lookup"><span data-stu-id="810b2-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="810b2-123">Выполняется команда delete nuget пакета с помощью веб-канала версии 2 не удастся.</span><span class="sxs-lookup"><span data-stu-id="810b2-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="810b2-124">Вместо этого используйте V3 веб-канала.</span><span class="sxs-lookup"><span data-stu-id="810b2-124">Use V3 feed instead.</span></span>


<span data-ttu-id="810b2-125">Полный список исправлений и усовершенствований этого выпуска, ознакомьтесь со списком проблем [здесь](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="810b2-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>