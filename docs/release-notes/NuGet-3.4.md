---
title: Заметки о выпуске NuGet 3,4
description: Заметки о выпуске NuGet 3,4, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776423"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="93af6-103">Заметки о выпуске NuGet 3,4</span><span class="sxs-lookup"><span data-stu-id="93af6-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="93af6-104">[NuGet 3,4 — заметки о](../release-notes/nuget-3.4-RC.md)  |  ВЫпуске RC [Заметки о выпуске 3.4.1 NuGet](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="93af6-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="93af6-105">Версия NuGet 3,4 была выпущена 30 марта 2016 в составе Visual Studio 2015 с обновлением 2 и Visual Studio 15 Preview и была разработана с использованием нескольких принципов в умы:</span><span class="sxs-lookup"><span data-stu-id="93af6-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="93af6-106">Кросс-платформенная поддержка</span><span class="sxs-lookup"><span data-stu-id="93af6-106">Cross-Platform support</span></span>
* <span data-ttu-id="93af6-107">Улучшения производительности</span><span class="sxs-lookup"><span data-stu-id="93af6-107">Performance improvements</span></span>
* <span data-ttu-id="93af6-108">Незначительные улучшения пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="93af6-108">Minor UI improvements</span></span>

<span data-ttu-id="93af6-109">Следующие функции ранее были добавлены в версию-кандидат и были обновлены или завершены для выпуска 3,4:</span><span class="sxs-lookup"><span data-stu-id="93af6-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="93af6-110">Новые возможности</span><span class="sxs-lookup"><span data-stu-id="93af6-110">New Features</span></span>

* <span data-ttu-id="93af6-111">Клиенты NuGet теперь поддерживают кодирование содержимого gzip из репозиториев</span><span class="sxs-lookup"><span data-stu-id="93af6-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="93af6-112">Поддержка PDB из пакетов в проектах xproj</span><span class="sxs-lookup"><span data-stu-id="93af6-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="93af6-113">Поддержка действий сборки iOS и Android в элементе contentFiles</span><span class="sxs-lookup"><span data-stu-id="93af6-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="93af6-114">Поддержка моникеров платформы netstandard и нетстандардапп</span><span class="sxs-lookup"><span data-stu-id="93af6-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="93af6-115">Новые функции пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="93af6-115">New User Interface Features</span></span>

* <span data-ttu-id="93af6-116">Значительные улучшения производительности, особенно на вкладках «установленные», «обновления» и «консолидация»</span><span class="sxs-lookup"><span data-stu-id="93af6-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="93af6-117">Доступен общий источник "все источники пакетов" с соответствующим слиянием результатов поиска</span><span class="sxs-lookup"><span data-stu-id="93af6-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="93af6-118">Вкладки установленные и обновленные теперь сортируются в алфавитном порядке</span><span class="sxs-lookup"><span data-stu-id="93af6-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="93af6-119">Добавлена кнопка Обновить, позволяющая обновлять Поиск.</span><span class="sxs-lookup"><span data-stu-id="93af6-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="93af6-120">Последние параметры сборки в верхней части списка версий</span><span class="sxs-lookup"><span data-stu-id="93af6-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="93af6-121">Обновления и улучшения</span><span class="sxs-lookup"><span data-stu-id="93af6-121">Updates and Improvements</span></span>

* <span data-ttu-id="93af6-122">Пакеты, на `project.json` которые ссылается в, имеют плавающую версию, не будут обновляться при каждой сборке.</span><span class="sxs-lookup"><span data-stu-id="93af6-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="93af6-123">Вместо этого они будут обновляться только при принудительном восстановлении, очистке, перестроении или изменении `project.json` .</span><span class="sxs-lookup"><span data-stu-id="93af6-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="93af6-124">источники репозитория nuget.org больше не переносятся в конфигурацию проекта при использовании пользовательского интерфейса настройки NuGet.</span><span class="sxs-lookup"><span data-stu-id="93af6-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="93af6-125">NuGet больше не восстанавливает пакеты в общих проектах и не записывает файл блокировки.</span><span class="sxs-lookup"><span data-stu-id="93af6-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="93af6-126">Мы улучшили сетевые сбои и повторную обработку недостижимых или медленных серверов.</span><span class="sxs-lookup"><span data-stu-id="93af6-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="93af6-127">В пользовательском интерфейсе диспетчера пакетов Visual Studio улучшены режимы работы клавиатуры и мыши.</span><span class="sxs-lookup"><span data-stu-id="93af6-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="93af6-128">Теперь мы поддерживаем последнюю `project.json` схему в DNX.</span><span class="sxs-lookup"><span data-stu-id="93af6-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="93af6-129">Критические изменения</span><span class="sxs-lookup"><span data-stu-id="93af6-129">Breaking Changes</span></span>

* <span data-ttu-id="93af6-130">Номера версий пакета теперь нормализованы до формата " *основной*". *дополнительный номер*. *исправление* - *Предварительный выпуск*   Каждое из основных, дополнительных и исправлений обрабатывается как целые числа и удаляет начальные нули.</span><span class="sxs-lookup"><span data-stu-id="93af6-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="93af6-131">Сведения о предварительном выпуске обрабатываются как строка, и к ней не применяются никакие изменения.</span><span class="sxs-lookup"><span data-stu-id="93af6-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="93af6-132">Эти числа используются в запросах клиентов NuGet и в поиске, предоставляемом службой nuget.org.</span><span class="sxs-lookup"><span data-stu-id="93af6-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="93af6-133">Дополнительные сведения можно найти в документах NuGet в разделе [предварительные версии](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="93af6-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="93af6-134">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="93af6-134">Known Issues</span></span>

* <span data-ttu-id="93af6-135">**Вопрос.** Пользователи Windows 10 клиенте v1511 установлен могут столкнуться с проблемами или даже с аварийным завершением Visual Studio с помощью PowerShell в Visual Studio в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="93af6-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="93af6-136">Установка и удаление пакетов, в которых есть скрипты install.ps1 и uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="93af6-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="93af6-137">Загрузка проектов, имеющих скрипт init.ps1 (например, EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="93af6-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="93af6-138">Публикация веб-содержимого</span><span class="sxs-lookup"><span data-stu-id="93af6-138">Publishing web content</span></span>

* <span data-ttu-id="93af6-139">**Обходной путь:** Убедитесь, что на установку Windows 10 установлены последние исправления, експеЦиалли 2016 января (KB 3124263) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="93af6-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="93af6-140">Дополнительные сведения см. в [#1638 проблемы GitHub](http://github.com/nuget/home/issues/1638) .</span><span class="sxs-lookup"><span data-stu-id="93af6-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="93af6-141">**Проблема.** Перенаправление протокола NuGet 2 не работает.</span><span class="sxs-lookup"><span data-stu-id="93af6-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="93af6-142">Пользовательские репозитории NuGet, которые перенаправляют запросы на другой узел, не учитывают запрос перенаправления.</span><span class="sxs-lookup"><span data-stu-id="93af6-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="93af6-143">**Обходной путь:**  Чтобы обойти эту ошибку, настройте URI репозитория пакетов в параметрах, чтобы указать расположение перенаправленного сервера.</span><span class="sxs-lookup"><span data-stu-id="93af6-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="93af6-144">Дополнительные сведения см. в разделе [#387 запроса на вытягивание GitHub](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="93af6-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="93af6-145">Мы продолжаем отслеживанием проблем в нашем списке проблем GitHub, который можно найти по адресу: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="93af6-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>