---
title: Заметки о выпуске 3,4 NuGet
description: Заметки о выпуске для NuGet 3.4, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f2a945b628022bdcc6e69a7a4b1be6c53b65626
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="ffc5d-103">Заметки о выпуске 3,4 NuGet</span><span class="sxs-lookup"><span data-stu-id="ffc5d-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="ffc5d-104">[Заметки о выпуске 3.4 RC NuGet](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 заметки о выпуске](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="ffc5d-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="ffc5d-105">NuGet 3.4 был выпущен 30 марта 2016 г. как часть Visual Studio 2015 с обновлением 2 и предварительной версии Visual Studio 15 и был построен с несколько принципов в умы:</span><span class="sxs-lookup"><span data-stu-id="ffc5d-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="ffc5d-106">Кроссплатформенная поддержка</span><span class="sxs-lookup"><span data-stu-id="ffc5d-106">Cross-Platform support</span></span>
* <span data-ttu-id="ffc5d-107">Улучшения производительности</span><span class="sxs-lookup"><span data-stu-id="ffc5d-107">Performance improvements</span></span>
* <span data-ttu-id="ffc5d-108">Незначительные изменения пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="ffc5d-108">Minor UI improvements</span></span>

<span data-ttu-id="ffc5d-109">Следующие функции были ранее добавлены в RC и были обновлены или завершения 3,4 выпуска:</span><span class="sxs-lookup"><span data-stu-id="ffc5d-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="ffc5d-110">Новые функции</span><span class="sxs-lookup"><span data-stu-id="ffc5d-110">New Features</span></span>

* <span data-ttu-id="ffc5d-111">Клиенты NuGet теперь поддерживают gzip content-encoding из репозиториев</span><span class="sxs-lookup"><span data-stu-id="ffc5d-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="ffc5d-112">Поддержка PDB-файлы из пакетов в компилируемых проектах</span><span class="sxs-lookup"><span data-stu-id="ffc5d-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="ffc5d-113">Поддержка iOS и Android построения действий в элементе contentFiles</span><span class="sxs-lookup"><span data-stu-id="ffc5d-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="ffc5d-114">Поддержка моникеров netstandard и netstandardapp моникеров платформы</span><span class="sxs-lookup"><span data-stu-id="ffc5d-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="ffc5d-115">Новые функции пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="ffc5d-115">New User Interface Features</span></span>

* <span data-ttu-id="ffc5d-116">Значительное повышение производительности особенно на вкладках установки, обновления и Консолидация</span><span class="sxs-lookup"><span data-stu-id="ffc5d-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="ffc5d-117">Совокупное «Все источники пакетов» источник доступен при объединении результатов поиска правильной</span><span class="sxs-lookup"><span data-stu-id="ffc5d-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="ffc5d-118">Установки и обновления вкладки теперь отсортированы в алфавитном порядке</span><span class="sxs-lookup"><span data-stu-id="ffc5d-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="ffc5d-119">Добавить кнопку обновления, которая позволяет поиска для обновления</span><span class="sxs-lookup"><span data-stu-id="ffc5d-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="ffc5d-120">Последние параметры сборки в верхней части списка версия</span><span class="sxs-lookup"><span data-stu-id="ffc5d-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="ffc5d-121">Обновления и улучшения</span><span class="sxs-lookup"><span data-stu-id="ffc5d-121">Updates and Improvements</span></span>

* <span data-ttu-id="ffc5d-122">Пакеты, на которые ссылается `project.json` , имеющих плавающей версии не будут обновлены для каждой сборки.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="ffc5d-123">Вместо этого они будут обновлены только в том случае, когда принудительного восстановления, очистка, перестроение и изменение `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="ffc5d-124">источники NuGet.org репозитории нет необходимости в конфигурацию проекта при использовании NuGet конфигурации пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="ffc5d-125">NuGet больше не восстанавливает пакетов в общих проектов, а также записывает файл блокировки.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="ffc5d-126">Мы улучшили сбой сети и повторите попытку обработки для серверов недоступен или медленно в ответ.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="ffc5d-127">Клавиатура и мышь поведения улучшение в пользовательском Интерфейсе диспетчера пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="ffc5d-128">Добавлена поддержка последней `project.json` схемы в DNX.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="ffc5d-129">Критические изменения</span><span class="sxs-lookup"><span data-stu-id="ffc5d-129">Breaking Changes</span></span>

* <span data-ttu-id="ffc5d-130">Номера версий пакета теперь нормализуются в формат *основных*. *дополнительный номер*. *исправление*-*предварительной* каждой основной и вспомогательной и исправления, обрабатываются как целые числа и удалите все нули в начале.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="ffc5d-131">Предварительные сведения рассматривается как строка и изменения не применяются к нему.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="ffc5d-132">Эти номера используются в запросах, клиенты NuGet и поиска, предоставленный службой nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="ffc5d-133">Дополнительные сведения можно найти в NuGet Docs под [предварительной версии](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ffc5d-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="ffc5d-134">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="ffc5d-134">Known Issues</span></span>

* <span data-ttu-id="ffc5d-135">**Проблема:** v1511 пользователи Windows 10 могут возникнуть проблемы или даже Visual Studio сбоя с помощью Powershell в Visual Studio в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="ffc5d-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="ffc5d-136">Установка и удаление пакетов, которые имеют install.ps1 / uninstall.ps1 сценариев</span><span class="sxs-lookup"><span data-stu-id="ffc5d-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="ffc5d-137">Загрузка проектов, имеющих сценарий init.ps1 (например, EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="ffc5d-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="ffc5d-138">Публикация веб-содержимого</span><span class="sxs-lookup"><span data-stu-id="ffc5d-138">Publishing web content</span></span>

* <span data-ttu-id="ffc5d-139">**Обходной путь:** убедитесь, что ваша установка Windows 10 имеет применены последние исправления, expecially январь 2016 г. (KB 3124263) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="ffc5d-140">Дополнительные сведения доступны на [вопрос GitHub #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="ffc5d-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="ffc5d-141">**Проблема.** Перенаправление протокола NuGet 2 не работает.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="ffc5d-142">Пользовательские репозитории NuGet, которые перенаправляют запросы на другой узел, не учитывают запрос перенаправления.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="ffc5d-143">**Обходной путь:** Чтобы обойти эту проблему, настройте URI репозитория пакетов в параметрах, чтобы он указывал на расположение перенаправляемого сервера.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="ffc5d-144">Дополнительные сведения см. в разделе [GitHub запросу #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="ffc5d-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="ffc5d-145">Мы продолжаем отслеживания проблем на наш список проблем GitHub, которую можно найти в: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="ffc5d-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>