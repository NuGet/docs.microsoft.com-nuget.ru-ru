---
title: Заметки о выпуске NuGet 3.4 RC выпуска
description: Заметки о выпуске для NuGet 3.4 RC, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546758"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="cdf50-103">Заметки о выпуске NuGet 3.4 RC выпуска</span><span class="sxs-lookup"><span data-stu-id="cdf50-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="cdf50-104">[Заметки о выпуске NuGet 3.3](../release-notes/nuget-3.3.md) | [заметки о выпуске NuGet 3.4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="cdf50-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="cdf50-105">3.4 версии-Кандидата NuGet была выпущена 3 марта 2016 г. вместе с Visual Studio 2015 Update 2 RC и был собран с параметром обсудим несколько принципов в умы:</span><span class="sxs-lookup"><span data-stu-id="cdf50-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="cdf50-106">Поддержка разных платформ</span><span class="sxs-lookup"><span data-stu-id="cdf50-106">Cross-Platform support</span></span>
* <span data-ttu-id="cdf50-107">Улучшения производительности</span><span class="sxs-lookup"><span data-stu-id="cdf50-107">Performance improvements</span></span>
* <span data-ttu-id="cdf50-108">Незначительные улучшения пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="cdf50-108">Minor UI improvements</span></span>

<span data-ttu-id="cdf50-109">Следующие функции доступны в этой версии-Кандидате, более запланировано 3,4 окончательной.</span><span class="sxs-lookup"><span data-stu-id="cdf50-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="cdf50-110">Новые функции</span><span class="sxs-lookup"><span data-stu-id="cdf50-110">New Features</span></span>

* <span data-ttu-id="cdf50-111">Клиенты NuGet теперь поддерживают содержимое с кодированием gzip из репозиториев</span><span class="sxs-lookup"><span data-stu-id="cdf50-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="cdf50-112">Поддержка PDB-файлов из пакетов в проектах xproj</span><span class="sxs-lookup"><span data-stu-id="cdf50-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="cdf50-113">Действия в элементе contentFiles при сборке поддержка iOS и Android</span><span class="sxs-lookup"><span data-stu-id="cdf50-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="cdf50-114">Поддержка моникеров netstandard и netstandardapp платформы</span><span class="sxs-lookup"><span data-stu-id="cdf50-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="cdf50-115">Новые возможности пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="cdf50-115">New User Interface Features</span></span>

* <span data-ttu-id="cdf50-116">Значительно большую производительность, особенно на вкладках установки, обновления и Консолидация</span><span class="sxs-lookup"><span data-stu-id="cdf50-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="cdf50-117">Установлен и вкладки обновлений теперь отсортированы в алфавитном порядке</span><span class="sxs-lookup"><span data-stu-id="cdf50-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="cdf50-118">Добавлена кнопка обновления, которая позволяет search для обновления</span><span class="sxs-lookup"><span data-stu-id="cdf50-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="cdf50-119">Обновления и улучшения</span><span class="sxs-lookup"><span data-stu-id="cdf50-119">Updates and Improvements</span></span>

* <span data-ttu-id="cdf50-120">Пакеты, на которые ссылается `project.json` , имеющих плавающей версии не будут обновляться для каждой сборки.</span><span class="sxs-lookup"><span data-stu-id="cdf50-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="cdf50-121">Вместо этого они будут обновлены только в том случае, когда вынужден восстановления, очистки, перестроения или изменить `project.json`.</span><span class="sxs-lookup"><span data-stu-id="cdf50-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="cdf50-122">источники репозиториев NuGet.org нет необходимости в конфигурацию проекта при использовании NuGet конфигурации пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="cdf50-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="cdf50-123">Больше не NuGet восстанавливает пакеты в общих проектов, а также записывает файл блокировки.</span><span class="sxs-lookup"><span data-stu-id="cdf50-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="cdf50-124">Мы улучшили сбой сети и повторите попытку обработки для серверов недоступным или медленно ответят.</span><span class="sxs-lookup"><span data-stu-id="cdf50-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="cdf50-125">Поведение клавиатуры и мыши улучшаются в пользовательском Интерфейсе диспетчера пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cdf50-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="cdf50-126">Добавлена поддержка последней версии `project.json` схемы в DNX.</span><span class="sxs-lookup"><span data-stu-id="cdf50-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="cdf50-127">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="cdf50-127">Known Issues</span></span>

<span data-ttu-id="cdf50-128">Мы продолжаем для отслеживания проблем в нашем списке проблемы GitHub, который можно найти в: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="cdf50-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>