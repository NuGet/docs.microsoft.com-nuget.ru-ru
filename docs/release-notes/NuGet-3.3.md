---
title: Заметки о выпуске NuGet 3,3
description: Заметки о выпуске NuGet 3,3, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa8290c80cc500b59d1779bf76662c07382fd277
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813784"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="c4fe3-103">Заметки о выпуске NuGet 3,3</span><span class="sxs-lookup"><span data-stu-id="c4fe3-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="c4fe3-104">[Заметки о выпуске NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3,4 — заметки о ВЫпуске RC](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="c4fe3-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="c4fe3-105">Версия NuGet 3,3 была выпущена 30 ноября 2015 с существенным числом обновлений пользовательского интерфейса и функций командной строки, а также набором полезных исправлений для клиентов NuGet.</span><span class="sxs-lookup"><span data-stu-id="c4fe3-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="c4fe3-106">Новые функции</span><span class="sxs-lookup"><span data-stu-id="c4fe3-106">New Features</span></span>

* <span data-ttu-id="c4fe3-107">Были введены поставщики учетных данных, позволяющие клиентам командной строки NuGet легко работать с аутентифицированным каналом.</span><span class="sxs-lookup"><span data-stu-id="c4fe3-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="c4fe3-108">[Инструкции по установке поставщика учетных данных Visual Studio Team Services](../reference/extensibility/nuget-exe-credential-providers.md) и настройке клиентов NuGet для их использования доступны в документации по NuGet.</span><span class="sxs-lookup"><span data-stu-id="c4fe3-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../reference/extensibility/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="c4fe3-109">Новые функции пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="c4fe3-109">New User Interface Features</span></span>

* <span data-ttu-id="c4fe3-110">Отдельные вкладки, доступные для просмотра, установки и обновления</span><span class="sxs-lookup"><span data-stu-id="c4fe3-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="c4fe3-111">Значок "доступные обновления", указывающий число пакетов с доступными обновлениями</span><span class="sxs-lookup"><span data-stu-id="c4fe3-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="c4fe3-112">Эмблемы пакета в списке пакетов, указывающие, установлен ли пакет или имеется доступное обновление</span><span class="sxs-lookup"><span data-stu-id="c4fe3-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="c4fe3-113">Число Скачиваний и автор, добавленные в список пакетов</span><span class="sxs-lookup"><span data-stu-id="c4fe3-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="c4fe3-114">Максимальный доступный номер версии и текущий установленный номер версии в списке пакетов</span><span class="sxs-lookup"><span data-stu-id="c4fe3-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="c4fe3-115">Кнопки действий, позволяющие выполнять быструю установку, обновление и удаление из списка пакетов.</span><span class="sxs-lookup"><span data-stu-id="c4fe3-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="c4fe3-116">Кнопки более четкого действия на панели сведений о пакете</span><span class="sxs-lookup"><span data-stu-id="c4fe3-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="c4fe3-117">Дата обновления пакета на панели сведений о пакете</span><span class="sxs-lookup"><span data-stu-id="c4fe3-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="c4fe3-118">Панель консолидации в представлении решения</span><span class="sxs-lookup"><span data-stu-id="c4fe3-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="c4fe3-119">Упорядоченная сетка проектов и номеров установленных версий в представлении решения</span><span class="sxs-lookup"><span data-stu-id="c4fe3-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="c4fe3-120">Новые возможности командной строки</span><span class="sxs-lookup"><span data-stu-id="c4fe3-120">New Command-line Features</span></span>

<span data-ttu-id="c4fe3-121">В этой версии мы предоставили команды `add` и `init` для инициализации репозиториев на основе папок, как описано в [справочнике по NuGet. exe](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="c4fe3-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="c4fe3-122">Репозитории, созданные и поддерживаемые этой структурой папок, [обеспечивают значительные преимущества для повышения производительности](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) , как описано в нашем блоге.</span><span class="sxs-lookup"><span data-stu-id="c4fe3-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="c4fe3-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="c4fe3-123">ContentFiles</span></span>

<span data-ttu-id="c4fe3-124">Теперь содержимое поддерживается в `project.json` управляемых проектах с помощью новой папки `contentFiles` и `.nuspec` `contentFiles` элемента.</span><span class="sxs-lookup"><span data-stu-id="c4fe3-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="c4fe3-125">Это содержимое может быть более непосредственно задано автором пакета для взаимодействия с системами проектов.</span><span class="sxs-lookup"><span data-stu-id="c4fe3-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="c4fe3-126">Дополнительные сведения о настройке contentFiles в документе `.nuspec` можно найти в [справочнике по nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="c4fe3-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="c4fe3-127">Управление кэшем локальных переменных NuGet</span><span class="sxs-lookup"><span data-stu-id="c4fe3-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="c4fe3-128">Командная строка NuGet была обновлена и содержит сведения об управлении локальными кэшами на рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="c4fe3-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="c4fe3-129">Дополнительные сведения о команде Locals см. в [справочнике по командной строке NuGet](../reference/cli-reference/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="c4fe3-129">More information about the locals command is available in the [NuGet command-line reference](../reference/cli-reference/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="c4fe3-130">Исправленные проблемы</span><span class="sxs-lookup"><span data-stu-id="c4fe3-130">Fixed Issues</span></span>

<span data-ttu-id="c4fe3-131">**Важные проблемы**</span><span class="sxs-lookup"><span data-stu-id="c4fe3-131">**Notable Issues**</span></span>

* <span data-ttu-id="c4fe3-132">Восстановлена поддержка командной строки NuGet для восстановления пакетов с файлом решения на моно- [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="c4fe3-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="c4fe3-133">Полный список проблем, которые были устранены в выпуске 3,3, можно найти на сайте GitHub в рамках [вехи 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="c4fe3-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="c4fe3-134">Список проблем, исправленных в выпуске командной строки 3,3, записывается в [веху командной строки 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="c4fe3-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="c4fe3-135">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="c4fe3-135">Known Issues</span></span>

<span data-ttu-id="c4fe3-136">Мы продолжаем отслеживанием проблем в нашем списке проблем GitHub, который можно найти по адресу: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="c4fe3-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>