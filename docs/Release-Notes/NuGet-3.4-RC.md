---
title: "Заметки о выпуске 3.4 RC NuGet | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 239d3d95-5a72-4fac-8389-b6deac27884d
description: "Заметки о выпуске для RC NuGet 3.4, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "Версия-Кандидат NuGet 3.4 заметки о выпуске, исправления ошибок, известные проблемы, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 86c37d516eede2ac5e6e5e842f687a8f3b17c0a4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="bd116-104">Заметки о выпуске 3.4 RC NuGet</span><span class="sxs-lookup"><span data-stu-id="bd116-104">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="bd116-105">[Заметки о выпуске NuGet 3.3](../release-notes/nuget-3.3.md) | [NuGet 3.4 заметки о выпуске](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="bd116-105">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="bd116-106">NuGet 3.4-RC была выпущена 3 марта 2016 г. параллельно с Visual Studio 2015 г. обновление 2 RC и был построен с несколько принципов в умы:</span><span class="sxs-lookup"><span data-stu-id="bd116-106">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

*  <span data-ttu-id="bd116-107">Кроссплатформенная поддержка</span><span class="sxs-lookup"><span data-stu-id="bd116-107">Cross-Platform support</span></span>
*  <span data-ttu-id="bd116-108">Улучшения производительности</span><span class="sxs-lookup"><span data-stu-id="bd116-108">Performance improvements</span></span>
*  <span data-ttu-id="bd116-109">Незначительные изменения пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="bd116-109">Minor UI improvements</span></span>

<span data-ttu-id="bd116-110">Следующие функции доступны в этой версии-Кандидата с более спланированных для 3,4 окончательной версии.</span><span class="sxs-lookup"><span data-stu-id="bd116-110">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="bd116-111">Новые функции</span><span class="sxs-lookup"><span data-stu-id="bd116-111">New Features</span></span>

* <span data-ttu-id="bd116-112">Клиенты NuGet теперь поддерживают gzip content-encoding из репозиториев</span><span class="sxs-lookup"><span data-stu-id="bd116-112">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="bd116-113">Поддержка PDB-файлы из пакетов в компилируемых проектах</span><span class="sxs-lookup"><span data-stu-id="bd116-113">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="bd116-114">Поддержка iOS и Android построения действий в элементе contentFiles</span><span class="sxs-lookup"><span data-stu-id="bd116-114">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="bd116-115">Поддержка моникеров netstandard и netstandardapp моникеров платформы</span><span class="sxs-lookup"><span data-stu-id="bd116-115">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="bd116-116">Новые функции пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="bd116-116">New User Interface Features</span></span>

* <span data-ttu-id="bd116-117">Значительное повышение производительности особенно на вкладках установки, обновления и Консолидация</span><span class="sxs-lookup"><span data-stu-id="bd116-117">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="bd116-118">Установки и обновления вкладки теперь отсортированы в алфавитном порядке</span><span class="sxs-lookup"><span data-stu-id="bd116-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="bd116-119">Добавить кнопку обновления, которая позволяет поиска для обновления</span><span class="sxs-lookup"><span data-stu-id="bd116-119">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="bd116-120">Обновления и улучшения</span><span class="sxs-lookup"><span data-stu-id="bd116-120">Updates and Improvements</span></span>

* <span data-ttu-id="bd116-121">Пакеты, на которые ссылается `project.json` , имеющих плавающей версии не будут обновлены для каждой сборки.</span><span class="sxs-lookup"><span data-stu-id="bd116-121">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="bd116-122">Вместо этого они будут обновлены только в том случае, когда принудительного восстановления, очистка, перестроение и изменение `project.json`.</span><span class="sxs-lookup"><span data-stu-id="bd116-122">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="bd116-123">источники NuGet.org репозитории нет необходимости в конфигурацию проекта при использовании NuGet конфигурации пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="bd116-123">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="bd116-124">NuGet больше не восстанавливает пакетов в общих проектов, а также записывает файл блокировки.</span><span class="sxs-lookup"><span data-stu-id="bd116-124">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="bd116-125">Мы улучшили сбой сети и повторите попытку обработки для серверов недоступен или медленно в ответ.</span><span class="sxs-lookup"><span data-stu-id="bd116-125">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="bd116-126">Клавиатура и мышь поведения улучшение в пользовательском Интерфейсе диспетчера пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bd116-126">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="bd116-127">Добавлена поддержка последней `project.json` схемы в DNX.</span><span class="sxs-lookup"><span data-stu-id="bd116-127">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="bd116-128">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="bd116-128">Known Issues</span></span>

<span data-ttu-id="bd116-129">Мы продолжаем отслеживания проблем на наш список проблем GitHub, которую можно найти в: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="bd116-129">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>