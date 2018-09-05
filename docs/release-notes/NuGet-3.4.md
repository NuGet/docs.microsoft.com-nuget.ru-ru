---
title: Заметки о выпуске NuGet 3.4 выпуска
description: Заметки о выпуске для NuGet 3.4, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551195"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="03e18-103">Заметки о выпуске NuGet 3.4 выпуска</span><span class="sxs-lookup"><span data-stu-id="03e18-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="03e18-104">[Заметки о выпуске NuGet 3.4 RC выпуска](../release-notes/nuget-3.4-RC.md) | [заметки о выпуске NuGet 3.4.1](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="03e18-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="03e18-105">NuGet 3.4 был выпущен 30 марта 2016 г. как часть Visual Studio 2015 с обновлением 2 и Visual Studio 15 предварительной версии и было создано с обсудим несколько принципов в умы:</span><span class="sxs-lookup"><span data-stu-id="03e18-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="03e18-106">Поддержка разных платформ</span><span class="sxs-lookup"><span data-stu-id="03e18-106">Cross-Platform support</span></span>
* <span data-ttu-id="03e18-107">Улучшения производительности</span><span class="sxs-lookup"><span data-stu-id="03e18-107">Performance improvements</span></span>
* <span data-ttu-id="03e18-108">Незначительные улучшения пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="03e18-108">Minor UI improvements</span></span>

<span data-ttu-id="03e18-109">Следующие функции ранее были добавлены в версию-Кандидат и были обновлены или завершения для 3,4 выпуска:</span><span class="sxs-lookup"><span data-stu-id="03e18-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="03e18-110">Новые функции</span><span class="sxs-lookup"><span data-stu-id="03e18-110">New Features</span></span>

* <span data-ttu-id="03e18-111">Клиенты NuGet теперь поддерживают содержимое с кодированием gzip из репозиториев</span><span class="sxs-lookup"><span data-stu-id="03e18-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="03e18-112">Поддержка PDB-файлов из пакетов в проектах xproj</span><span class="sxs-lookup"><span data-stu-id="03e18-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="03e18-113">Действия в элементе contentFiles при сборке поддержка iOS и Android</span><span class="sxs-lookup"><span data-stu-id="03e18-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="03e18-114">Поддержка моникеров netstandard и netstandardapp платформы</span><span class="sxs-lookup"><span data-stu-id="03e18-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="03e18-115">Новые возможности пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="03e18-115">New User Interface Features</span></span>

* <span data-ttu-id="03e18-116">Значительно большую производительность, особенно на вкладках установки, обновления и Консолидация</span><span class="sxs-lookup"><span data-stu-id="03e18-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="03e18-117">Источником «Все источники пакетов» входит в состав правильного поиска результат слияния</span><span class="sxs-lookup"><span data-stu-id="03e18-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="03e18-118">Установлен и вкладки обновлений теперь отсортированы в алфавитном порядке</span><span class="sxs-lookup"><span data-stu-id="03e18-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="03e18-119">Добавлена кнопка обновления, которая позволяет search для обновления</span><span class="sxs-lookup"><span data-stu-id="03e18-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="03e18-120">Последние параметры сборки в верхней части списка версия</span><span class="sxs-lookup"><span data-stu-id="03e18-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="03e18-121">Обновления и улучшения</span><span class="sxs-lookup"><span data-stu-id="03e18-121">Updates and Improvements</span></span>

* <span data-ttu-id="03e18-122">Пакеты, на которые ссылается `project.json` , имеющих плавающей версии не будут обновляться для каждой сборки.</span><span class="sxs-lookup"><span data-stu-id="03e18-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="03e18-123">Вместо этого они будут обновлены только в том случае, когда вынужден восстановления, очистки, перестроения или изменить `project.json`.</span><span class="sxs-lookup"><span data-stu-id="03e18-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="03e18-124">источники репозиториев NuGet.org нет необходимости в конфигурацию проекта при использовании NuGet конфигурации пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="03e18-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="03e18-125">Больше не NuGet восстанавливает пакеты в общих проектов, а также записывает файл блокировки.</span><span class="sxs-lookup"><span data-stu-id="03e18-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="03e18-126">Мы улучшили сбой сети и повторите попытку обработки для серверов недоступным или медленно ответят.</span><span class="sxs-lookup"><span data-stu-id="03e18-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="03e18-127">Поведение клавиатуры и мыши улучшаются в пользовательском Интерфейсе диспетчера пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="03e18-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="03e18-128">Добавлена поддержка последней версии `project.json` схемы в DNX.</span><span class="sxs-lookup"><span data-stu-id="03e18-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="03e18-129">Критические изменения</span><span class="sxs-lookup"><span data-stu-id="03e18-129">Breaking Changes</span></span>

* <span data-ttu-id="03e18-130">Номера версий пакета теперь нормализуются в формат *основных*. *дополнительный номер*. *исправление*-*предварительной* каждого из основной и вспомогательной и исправления, обрабатываются как целые числа и удалите все начальные нули.</span><span class="sxs-lookup"><span data-stu-id="03e18-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="03e18-131">Информацию о предварительных рассматривается как строка и изменения не применяются к нему.</span><span class="sxs-lookup"><span data-stu-id="03e18-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="03e18-132">Эти числа используются в запросах клиенты NuGet и поиска, предоставляемых службой nuget.org.</span><span class="sxs-lookup"><span data-stu-id="03e18-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="03e18-133">Дополнительные сведения можно найти в документации по NuGet в разделе [предварительной версии](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="03e18-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="03e18-134">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="03e18-134">Known Issues</span></span>

* <span data-ttu-id="03e18-135">**Проблема:** Windows 10 v1511 установлен у пользователей проблемы или даже Visual Studio сбой с помощью Powershell в Visual Studio в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="03e18-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="03e18-136">Установка / удаление пакетов, которые имеют install.ps1 / сценарии uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="03e18-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="03e18-137">Загрузка проектов, содержащих скрипт init.ps1, возникает (например, EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="03e18-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="03e18-138">Публикация веб-содержимого</span><span class="sxs-lookup"><span data-stu-id="03e18-138">Publishing web content</span></span>

* <span data-ttu-id="03e18-139">**Инструкции по решению:** убедитесь в наличии файлов установки Windows 10 последние исправления применены, специально января 2016 г. (базы Знаний 3124263) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="03e18-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="03e18-140">Дополнительные сведения доступны на [#1638 на сайте github](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="03e18-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="03e18-141">**Проблема.** Перенаправление протокола NuGet 2 не работает.</span><span class="sxs-lookup"><span data-stu-id="03e18-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="03e18-142">Пользовательские репозитории NuGet, которые перенаправляют запросы на другой узел, не учитывают запрос перенаправления.</span><span class="sxs-lookup"><span data-stu-id="03e18-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="03e18-143">**Инструкции по решению:** Чтобы обойти эту проблему, настройте URI репозитория пакетов в параметрах, чтобы он указывал на расположение перенаправляемого сервера.</span><span class="sxs-lookup"><span data-stu-id="03e18-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="03e18-144">Дополнительные сведения см. в разделе [запроса на включение внесенных изменений GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="03e18-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="03e18-145">Мы продолжаем для отслеживания проблем в нашем списке проблемы GitHub, который можно найти в: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="03e18-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>