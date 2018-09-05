---
title: Заметки о выпуске NuGet 3.3 выпуска
description: Заметки о выпуске для NuGet 3.3, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546651"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="de463-103">Заметки о выпуске NuGet 3.3 выпуска</span><span class="sxs-lookup"><span data-stu-id="de463-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="de463-104">[Заметки о выпуске NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC заметки.](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="de463-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="de463-105">NuGet 3.3 был выпущен 30 ноября 2015 г. с значительное количество обновлении пользовательского интерфейса и функции командной строки, а также набор исправлений, полезные для клиентов NuGet.</span><span class="sxs-lookup"><span data-stu-id="de463-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="de463-106">Новые функции</span><span class="sxs-lookup"><span data-stu-id="de463-106">New Features</span></span>

* <span data-ttu-id="de463-107">Были введены поставщиков учетных данных, которые позволяют клиентам командной строки NuGet иметь возможность прозрачно совмещаются с собой прошедшего проверку подлинности веб-канал.</span><span class="sxs-lookup"><span data-stu-id="de463-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="de463-108">[Инструкции по установке Visual Studio Team Services учетных данных поставщик ](../api/nuget-exe-credential-providers.md) и настроить NuGet клиентов для его использования доступны в документации NuGet.</span><span class="sxs-lookup"><span data-stu-id="de463-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="de463-109">Новые возможности пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="de463-109">New User Interface Features</span></span>

* <span data-ttu-id="de463-110">Отдельные вкладки обзора, установленные и доступные обновления</span><span class="sxs-lookup"><span data-stu-id="de463-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="de463-111">Обновления доступны эмблемы, указывающее количество пакетов с помощью доступных обновлений</span><span class="sxs-lookup"><span data-stu-id="de463-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="de463-112">Индикаторы событий пакетов в списке пакетов, чтобы указать, если установлен пакет, или доступно обновление</span><span class="sxs-lookup"><span data-stu-id="de463-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="de463-113">Скачайте count и автор, добавляемый в список пакетов</span><span class="sxs-lookup"><span data-stu-id="de463-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="de463-114">Наибольший номер версии и номер текущей версии в списке пакетов</span><span class="sxs-lookup"><span data-stu-id="de463-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="de463-115">Действие кнопки, позволяющие быстро установить обновления, а в списке пакетов</span><span class="sxs-lookup"><span data-stu-id="de463-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="de463-116">Яснее кнопки действий на панель подробных сведений о пакете</span><span class="sxs-lookup"><span data-stu-id="de463-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="de463-117">Дата обновления пакета на панель подробных сведений о пакете</span><span class="sxs-lookup"><span data-stu-id="de463-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="de463-118">Объединить панели в представлении решения</span><span class="sxs-lookup"><span data-stu-id="de463-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="de463-119">Сортируемый сетки проектов и номеров установленных версий в представлении решения</span><span class="sxs-lookup"><span data-stu-id="de463-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="de463-120">Новые возможности командной строки</span><span class="sxs-lookup"><span data-stu-id="de463-120">New Command-line Features</span></span>

<span data-ttu-id="de463-121">В этой версии мы представили `add` и `init` команды, чтобы инициализировать репозиториев на основе папок, как описано в [nuget.exe ссылку](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="de463-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="de463-122">Репозитории, создан и сохранен вместе с этой папке структуры будет [обеспечить значительные преимущества в производительности](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) как описано в нашем блоге.</span><span class="sxs-lookup"><span data-stu-id="de463-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="de463-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="de463-123">ContentFiles</span></span>

<span data-ttu-id="de463-124">Содержимое теперь поддерживается в `project.json` управляемых проектов посредством нового `contentFiles` папки и `.nuspec` `contentFiles` элемент нотации.</span><span class="sxs-lookup"><span data-stu-id="de463-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="de463-125">Это содержимое можно напрямую указать автором пакета для взаимодействия с системы проектов.</span><span class="sxs-lookup"><span data-stu-id="de463-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="de463-126">Дополнительные сведения о настройке contentFiles в `.nuspec` документ можно найти в [Справочник по файлу nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="de463-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="de463-127">NuGet Locals кэшировать управления</span><span class="sxs-lookup"><span data-stu-id="de463-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="de463-128">Командной строки NuGet обновлен для включения сведений об управлении локальных кэшах на рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="de463-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="de463-129">Дополнительные сведения о команде "Локальные" можно найти в [Справочник по командной строке NuGet](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="de463-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="de463-130">Исправленные проблемы</span><span class="sxs-lookup"><span data-stu-id="de463-130">Fixed Issues</span></span>

<span data-ttu-id="de463-131">**Важные события**</span><span class="sxs-lookup"><span data-stu-id="de463-131">**Notable Issues**</span></span>

* <span data-ttu-id="de463-132">Поддержка восстановленной командной строки NuGet для восстановления пакетов с файлом решения в Mono — [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="de463-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="de463-133">Полный список проблем, которые были исправлены в версии 3.3 можно найти на сайте GitHub в разделе [3.3 вехи](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="de463-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="de463-134">Список проблем, исправленных в выпуске 3.3 командной строки записываются в [3.3 командной строки вехи](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="de463-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="de463-135">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="de463-135">Known Issues</span></span>

<span data-ttu-id="de463-136">Мы продолжаем для отслеживания проблем в нашем списке проблемы GitHub, который можно найти в: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="de463-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>