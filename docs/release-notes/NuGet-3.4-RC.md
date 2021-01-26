---
title: NuGet 3,4 — заметки о выпуске RC
description: Заметки о выпуске для версии-КАНДИДАТа NuGet 3,4, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780234"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="ba4b5-103">NuGet 3,4 — заметки о выпуске RC</span><span class="sxs-lookup"><span data-stu-id="ba4b5-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="ba4b5-104">[Заметки о](../release-notes/nuget-3.3.md)  |  выпуске NuGet 3,3 [Заметки о выпуске NuGet 3,4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="ba4b5-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="ba4b5-105">NuGet 3,4-RC выпущен 3 марта 2016 вместе с версией-КАНДИДАТом Visual Studio 2015 с обновлением 2 и был построен с использованием нескольких принципов в умы:</span><span class="sxs-lookup"><span data-stu-id="ba4b5-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="ba4b5-106">Кросс-платформенная поддержка</span><span class="sxs-lookup"><span data-stu-id="ba4b5-106">Cross-Platform support</span></span>
* <span data-ttu-id="ba4b5-107">Улучшения производительности</span><span class="sxs-lookup"><span data-stu-id="ba4b5-107">Performance improvements</span></span>
* <span data-ttu-id="ba4b5-108">Незначительные улучшения пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="ba4b5-108">Minor UI improvements</span></span>

<span data-ttu-id="ba4b5-109">В этой версии-КАНДИДАТе доступны следующие функции с более плановым выпуском 3,4.</span><span class="sxs-lookup"><span data-stu-id="ba4b5-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="ba4b5-110">Новые возможности</span><span class="sxs-lookup"><span data-stu-id="ba4b5-110">New Features</span></span>

* <span data-ttu-id="ba4b5-111">Клиенты NuGet теперь поддерживают кодирование содержимого gzip из репозиториев</span><span class="sxs-lookup"><span data-stu-id="ba4b5-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="ba4b5-112">Поддержка PDB из пакетов в проектах xproj</span><span class="sxs-lookup"><span data-stu-id="ba4b5-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="ba4b5-113">Поддержка действий сборки iOS и Android в элементе contentFiles</span><span class="sxs-lookup"><span data-stu-id="ba4b5-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="ba4b5-114">Поддержка моникеров платформы netstandard и нетстандардапп</span><span class="sxs-lookup"><span data-stu-id="ba4b5-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="ba4b5-115">Новые функции пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="ba4b5-115">New User Interface Features</span></span>

* <span data-ttu-id="ba4b5-116">Значительные улучшения производительности, особенно на вкладках «установленные», «обновления» и «консолидация»</span><span class="sxs-lookup"><span data-stu-id="ba4b5-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="ba4b5-117">Вкладки установленные и обновленные теперь сортируются в алфавитном порядке</span><span class="sxs-lookup"><span data-stu-id="ba4b5-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="ba4b5-118">Добавлена кнопка Обновить, позволяющая обновлять Поиск.</span><span class="sxs-lookup"><span data-stu-id="ba4b5-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="ba4b5-119">Обновления и улучшения</span><span class="sxs-lookup"><span data-stu-id="ba4b5-119">Updates and Improvements</span></span>

* <span data-ttu-id="ba4b5-120">Пакеты, на `project.json` которые ссылается в, имеют плавающую версию, не будут обновляться при каждой сборке.</span><span class="sxs-lookup"><span data-stu-id="ba4b5-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="ba4b5-121">Вместо этого они будут обновляться только при принудительном восстановлении, очистке, перестроении или изменении `project.json` .</span><span class="sxs-lookup"><span data-stu-id="ba4b5-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="ba4b5-122">источники репозитория nuget.org больше не переносятся в конфигурацию проекта при использовании пользовательского интерфейса настройки NuGet.</span><span class="sxs-lookup"><span data-stu-id="ba4b5-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="ba4b5-123">NuGet больше не восстанавливает пакеты в общих проектах и не записывает файл блокировки.</span><span class="sxs-lookup"><span data-stu-id="ba4b5-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="ba4b5-124">Мы улучшили сетевые сбои и повторную обработку недостижимых или медленных серверов.</span><span class="sxs-lookup"><span data-stu-id="ba4b5-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="ba4b5-125">В пользовательском интерфейсе диспетчера пакетов Visual Studio улучшены режимы работы клавиатуры и мыши.</span><span class="sxs-lookup"><span data-stu-id="ba4b5-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="ba4b5-126">Теперь мы поддерживаем последнюю `project.json` схему в DNX.</span><span class="sxs-lookup"><span data-stu-id="ba4b5-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="ba4b5-127">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="ba4b5-127">Known Issues</span></span>

<span data-ttu-id="ba4b5-128">Мы продолжаем отслеживанием проблем в нашем списке проблем GitHub, который можно найти по адресу: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="ba4b5-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>