---
title: Заметки о выпуске NuGet 3.3 | Документы Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Заметки о выпуске для NuGet 3.3, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
keywords: NuGet 3.3 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ab5e1ca550297c608017cb56dff32f4bd4bbb885
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="e9f0e-104">Заметки о выпуске 3.3 NuGet</span><span class="sxs-lookup"><span data-stu-id="e9f0e-104">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="e9f0e-105">[Заметки о выпуске NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC замечания.](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="e9f0e-105">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="e9f0e-106">NuGet 3.3 был выпущен 30 ноября 2015 г. с значительное количество обновлении пользовательского интерфейса и функции командной строки, а также набором полезных исправлений на клиентах NuGet.</span><span class="sxs-lookup"><span data-stu-id="e9f0e-106">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="e9f0e-107">Новые возможности</span><span class="sxs-lookup"><span data-stu-id="e9f0e-107">New Features</span></span>

* <span data-ttu-id="e9f0e-108">Были введены поставщиков учетных данных, позволяющих NuGet командной строки клиентам возможность эффективно взаимодействовать с проверкой подлинности веб-канала.</span><span class="sxs-lookup"><span data-stu-id="e9f0e-108">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="e9f0e-109">[Инструкции по установке Visual Studio Team Services учетных данных поставщика ](../api/nuget-exe-credential-providers.md) и настройте NuGet-клиентов можно найти на NuGet Docs.</span><span class="sxs-lookup"><span data-stu-id="e9f0e-109">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="e9f0e-110">Новые функции пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="e9f0e-110">New User Interface Features</span></span>

* <span data-ttu-id="e9f0e-111">Отдельные вкладки обзора, установки и доступных обновлений</span><span class="sxs-lookup"><span data-stu-id="e9f0e-111">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="e9f0e-112">Обновления доступны эмблемы, указывающее количество пакетов с использованием доступных обновлений</span><span class="sxs-lookup"><span data-stu-id="e9f0e-112">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="e9f0e-113">Карточки в список пакетов, чтобы указать, если установлен пакет или доступно обновление пакета</span><span class="sxs-lookup"><span data-stu-id="e9f0e-113">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="e9f0e-114">Загрузите count и автор добавляется к списку пакетов</span><span class="sxs-lookup"><span data-stu-id="e9f0e-114">Download count and author added to the package list</span></span>
* <span data-ttu-id="e9f0e-115">Наибольший номер версии и номер текущей версии в списке пакетов</span><span class="sxs-lookup"><span data-stu-id="e9f0e-115">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="e9f0e-116">Действие кнопки, позволяющие Быстрая установка, обновление и удаление из списка пакетов</span><span class="sxs-lookup"><span data-stu-id="e9f0e-116">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="e9f0e-117">Четкое кнопок на панели сведений пакета</span><span class="sxs-lookup"><span data-stu-id="e9f0e-117">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="e9f0e-118">Пакет обновления на панели сведений пакета</span><span class="sxs-lookup"><span data-stu-id="e9f0e-118">Package update date on the package detail panel</span></span>
* <span data-ttu-id="e9f0e-119">Консолидация панель в представление решения</span><span class="sxs-lookup"><span data-stu-id="e9f0e-119">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="e9f0e-120">Сортируемый сетки проектов и номера версий установленных на представление решения</span><span class="sxs-lookup"><span data-stu-id="e9f0e-120">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="e9f0e-121">Новые возможности командной строки</span><span class="sxs-lookup"><span data-stu-id="e9f0e-121">New Command-line Features</span></span>

<span data-ttu-id="e9f0e-122">В этой версии мы представили `add` и `init` команды для инициализации хранилища для папки, как описано в [nuget.exe ссылка](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="e9f0e-122">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="e9f0e-123">Репозитории, создается и сохраняется с этой папкой структура будет [обеспечивают значительное преимущество в производительности](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) , описанной в нашем блоге.</span><span class="sxs-lookup"><span data-stu-id="e9f0e-123">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="e9f0e-124">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="e9f0e-124">ContentFiles</span></span>

<span data-ttu-id="e9f0e-125">Содержимое теперь поддерживается в `project.json` управляемых проектов при помощи новых `contentFiles` папки и `.nuspec` `contentFiles` элемент нотации.</span><span class="sxs-lookup"><span data-stu-id="e9f0e-125">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="e9f0e-126">Это содержимое можно указывать более непосредственно автором пакета для взаимодействия с системами проекта.</span><span class="sxs-lookup"><span data-stu-id="e9f0e-126">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="e9f0e-127">Дополнительные сведения о настройке contentFiles в `.nuspec` документ можно найти в [.nuspec ссылка](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="e9f0e-127">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="e9f0e-128">Локальные переменные NuGet кэша управления</span><span class="sxs-lookup"><span data-stu-id="e9f0e-128">NuGet Locals Cache Management</span></span>

<span data-ttu-id="e9f0e-129">NuGet командной строки был обновлен для включения сведений об управлении локальный кэш на рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="e9f0e-129">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="e9f0e-130">Дополнительные сведения о команде локальные переменные недоступны в [Справочник по командной строке NuGet](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="e9f0e-130">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="e9f0e-131">Исправленные ошибки</span><span class="sxs-lookup"><span data-stu-id="e9f0e-131">Fixed Issues</span></span>

<span data-ttu-id="e9f0e-132">**Важные моменты**</span><span class="sxs-lookup"><span data-stu-id="e9f0e-132">**Notable Issues**</span></span>

* <span data-ttu-id="e9f0e-133">Пакеты NuGet командной строки восстановленной поддержка восстановления с файлом решения на моно - [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="e9f0e-133">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="e9f0e-134">Полный список проблем, которые не были в выпуске 3.3 можно найти на GitHub под [3,3 вехи](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="e9f0e-134">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="e9f0e-135">Список проблем, исправленных в выпуске 3.3 командной строки записываются в [3,3 вехи командной строки](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="e9f0e-135">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="e9f0e-136">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="e9f0e-136">Known Issues</span></span>

<span data-ttu-id="e9f0e-137">Мы продолжаем отслеживания проблем на наш список проблем GitHub, которую можно найти в: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="e9f0e-137">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>