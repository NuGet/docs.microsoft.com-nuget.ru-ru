---
title: Заметки о выпуске NuGet 3,3
description: Заметки о выпуске NuGet 3,3, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cd3f8c9c4586c608d41e7b8bfc413acfc6aff497
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776507"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="a796f-103">Заметки о выпуске NuGet 3,3</span><span class="sxs-lookup"><span data-stu-id="a796f-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="a796f-104">[Заметки о](../release-notes/nuget-3.2.1.md)  |  выпуске NuGet 3.2.1 [NuGet 3,4 — заметки о выпуске RC](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="a796f-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="a796f-105">Версия NuGet 3,3 была выпущена 30 ноября 2015 с существенным числом обновлений пользовательского интерфейса и функций командной строки, а также набором полезных исправлений для клиентов NuGet.</span><span class="sxs-lookup"><span data-stu-id="a796f-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="a796f-106">Новые возможности</span><span class="sxs-lookup"><span data-stu-id="a796f-106">New Features</span></span>

* <span data-ttu-id="a796f-107">Были введены поставщики учетных данных, позволяющие клиентам командной строки NuGet легко работать с аутентифицированным каналом.</span><span class="sxs-lookup"><span data-stu-id="a796f-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="a796f-108">[Инструкции по установке поставщика учетных данных Visual Studio Team Services ](../reference/extensibility/nuget-exe-credential-providers.md) и настройке клиентов NuGet для их использования доступны в документации по NuGet.</span><span class="sxs-lookup"><span data-stu-id="a796f-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../reference/extensibility/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="a796f-109">Новые функции пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="a796f-109">New User Interface Features</span></span>

* <span data-ttu-id="a796f-110">Отдельные вкладки, доступные для просмотра, установки и обновления</span><span class="sxs-lookup"><span data-stu-id="a796f-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="a796f-111">Значок "доступные обновления", указывающий число пакетов с доступными обновлениями</span><span class="sxs-lookup"><span data-stu-id="a796f-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="a796f-112">Эмблемы пакета в списке пакетов, указывающие, установлен ли пакет или имеется доступное обновление</span><span class="sxs-lookup"><span data-stu-id="a796f-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="a796f-113">Число Скачиваний и автор, добавленные в список пакетов</span><span class="sxs-lookup"><span data-stu-id="a796f-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="a796f-114">Максимальный доступный номер версии и текущий установленный номер версии в списке пакетов</span><span class="sxs-lookup"><span data-stu-id="a796f-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="a796f-115">Кнопки действий, позволяющие выполнять быструю установку, обновление и удаление из списка пакетов.</span><span class="sxs-lookup"><span data-stu-id="a796f-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="a796f-116">Кнопки более четкого действия на панели сведений о пакете</span><span class="sxs-lookup"><span data-stu-id="a796f-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="a796f-117">Дата обновления пакета на панели сведений о пакете</span><span class="sxs-lookup"><span data-stu-id="a796f-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="a796f-118">Панель консолидации в представлении решения</span><span class="sxs-lookup"><span data-stu-id="a796f-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="a796f-119">Упорядоченная сетка проектов и номеров установленных версий в представлении решения</span><span class="sxs-lookup"><span data-stu-id="a796f-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="a796f-120">Новые возможности командной строки</span><span class="sxs-lookup"><span data-stu-id="a796f-120">New Command-line Features</span></span>

<span data-ttu-id="a796f-121">В этой версии мы предоставили `add` `init` команды и для инициализации репозиториев на основе папок, как описано в [ справочнике поnuget.exe](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="a796f-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="a796f-122">Репозитории, созданные и поддерживаемые этой структурой папок, [обеспечивают значительные преимущества для повышения производительности](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) , как описано в нашем блоге.</span><span class="sxs-lookup"><span data-stu-id="a796f-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="a796f-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="a796f-123">ContentFiles</span></span>

<span data-ttu-id="a796f-124">Теперь содержимое поддерживается в `project.json` управляемых проектах с помощью новой `contentFiles` папки и `.nuspec` `contentFiles` нотации элементов.</span><span class="sxs-lookup"><span data-stu-id="a796f-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="a796f-125">Это содержимое может быть более непосредственно задано автором пакета для взаимодействия с системами проектов.</span><span class="sxs-lookup"><span data-stu-id="a796f-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="a796f-126">Дополнительные сведения о настройке contentFiles в `.nuspec` документе можно найти в [справочнике по nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="a796f-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="a796f-127">Управление кэшем локальных переменных NuGet</span><span class="sxs-lookup"><span data-stu-id="a796f-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="a796f-128">Командная строка NuGet была обновлена и содержит сведения об управлении локальными кэшами на рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="a796f-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="a796f-129">Дополнительные сведения о команде Locals см. в [справочнике по командной строке NuGet](../reference/cli-reference/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="a796f-129">More information about the locals command is available in the [NuGet command-line reference](../reference/cli-reference/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="a796f-130">Исправленные проблемы</span><span class="sxs-lookup"><span data-stu-id="a796f-130">Fixed Issues</span></span>

<span data-ttu-id="a796f-131">**Важные проблемы**</span><span class="sxs-lookup"><span data-stu-id="a796f-131">**Notable Issues**</span></span>

* <span data-ttu-id="a796f-132">Восстановлена поддержка командной строки NuGet для восстановления пакетов с файлом решения на моно- [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="a796f-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="a796f-133">Полный список проблем, которые были устранены в выпуске 3,3, можно найти на сайте GitHub в рамках [вехи 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="a796f-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="a796f-134">Список проблем, исправленных в выпуске командной строки 3,3, записывается в [контрольной точке 3,3 Command-Line](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="a796f-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="a796f-135">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="a796f-135">Known Issues</span></span>

<span data-ttu-id="a796f-136">Мы продолжаем отслеживанием проблем в нашем списке проблем GitHub, который можно найти по адресу: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="a796f-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>