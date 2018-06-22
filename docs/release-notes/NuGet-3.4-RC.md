---
title: Заметки о выпуске 3.4 RC NuGet
description: Заметки о выпуске для RC NuGet 3.4, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e40d685a5256fdfee818f0cc1f1bc352c698f3c2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820824"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="6e5a3-103">Заметки о выпуске 3.4 RC NuGet</span><span class="sxs-lookup"><span data-stu-id="6e5a3-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="6e5a3-104">[Заметки о выпуске NuGet 3.3](../release-notes/nuget-3.3.md) | [NuGet 3.4 заметки о выпуске](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="6e5a3-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="6e5a3-105">NuGet 3.4-RC была выпущена 3 марта 2016 г. параллельно с Visual Studio 2015 г. обновление 2 RC и был построен с несколько принципов в умы:</span><span class="sxs-lookup"><span data-stu-id="6e5a3-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="6e5a3-106">Кроссплатформенная поддержка</span><span class="sxs-lookup"><span data-stu-id="6e5a3-106">Cross-Platform support</span></span>
* <span data-ttu-id="6e5a3-107">Улучшения производительности</span><span class="sxs-lookup"><span data-stu-id="6e5a3-107">Performance improvements</span></span>
* <span data-ttu-id="6e5a3-108">Незначительные изменения пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="6e5a3-108">Minor UI improvements</span></span>

<span data-ttu-id="6e5a3-109">Следующие функции доступны в этой версии-Кандидата с более спланированных для 3,4 окончательной версии.</span><span class="sxs-lookup"><span data-stu-id="6e5a3-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="6e5a3-110">Новые функции</span><span class="sxs-lookup"><span data-stu-id="6e5a3-110">New Features</span></span>

* <span data-ttu-id="6e5a3-111">Клиенты NuGet теперь поддерживают gzip content-encoding из репозиториев</span><span class="sxs-lookup"><span data-stu-id="6e5a3-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="6e5a3-112">Поддержка PDB-файлы из пакетов в компилируемых проектах</span><span class="sxs-lookup"><span data-stu-id="6e5a3-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="6e5a3-113">Поддержка iOS и Android построения действий в элементе contentFiles</span><span class="sxs-lookup"><span data-stu-id="6e5a3-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="6e5a3-114">Поддержка моникеров netstandard и netstandardapp моникеров платформы</span><span class="sxs-lookup"><span data-stu-id="6e5a3-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="6e5a3-115">Новые функции пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="6e5a3-115">New User Interface Features</span></span>

* <span data-ttu-id="6e5a3-116">Значительное повышение производительности особенно на вкладках установки, обновления и Консолидация</span><span class="sxs-lookup"><span data-stu-id="6e5a3-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="6e5a3-117">Установки и обновления вкладки теперь отсортированы в алфавитном порядке</span><span class="sxs-lookup"><span data-stu-id="6e5a3-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="6e5a3-118">Добавить кнопку обновления, которая позволяет поиска для обновления</span><span class="sxs-lookup"><span data-stu-id="6e5a3-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="6e5a3-119">Обновления и улучшения</span><span class="sxs-lookup"><span data-stu-id="6e5a3-119">Updates and Improvements</span></span>

* <span data-ttu-id="6e5a3-120">Пакеты, на которые ссылается `project.json` , имеющих плавающей версии не будут обновлены для каждой сборки.</span><span class="sxs-lookup"><span data-stu-id="6e5a3-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="6e5a3-121">Вместо этого они будут обновлены только в том случае, когда принудительного восстановления, очистка, перестроение и изменение `project.json`.</span><span class="sxs-lookup"><span data-stu-id="6e5a3-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="6e5a3-122">источники NuGet.org репозитории нет необходимости в конфигурацию проекта при использовании NuGet конфигурации пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="6e5a3-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="6e5a3-123">NuGet больше не восстанавливает пакетов в общих проектов, а также записывает файл блокировки.</span><span class="sxs-lookup"><span data-stu-id="6e5a3-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="6e5a3-124">Мы улучшили сбой сети и повторите попытку обработки для серверов недоступен или медленно в ответ.</span><span class="sxs-lookup"><span data-stu-id="6e5a3-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="6e5a3-125">Клавиатура и мышь поведения улучшение в пользовательском Интерфейсе диспетчера пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6e5a3-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="6e5a3-126">Добавлена поддержка последней `project.json` схемы в DNX.</span><span class="sxs-lookup"><span data-stu-id="6e5a3-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="6e5a3-127">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="6e5a3-127">Known Issues</span></span>

<span data-ttu-id="6e5a3-128">Мы продолжаем отслеживания проблем на наш список проблем GitHub, которую можно найти в: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="6e5a3-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>