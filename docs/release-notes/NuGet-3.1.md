---
title: Заметки о выпуске 3.1 NuGet
description: Заметки о выпуске для NuGet 3.1, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545351"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="374ea-103">Заметки о выпуске 3.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="374ea-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="374ea-104">[Заметки о выпуске NuGet 3.0](../release-notes/nuget-3.0.0.md) | [заметки о выпуске NuGet 3.1.1](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="374ea-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="374ea-105">NuGet 3.1 была выпущена 27 июля 2015 г. как расширение распространение для пакета SDK универсальной платформы Windows для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="374ea-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="374ea-106">Таким образом, чтобы процесс разработки для Windows можно использовать преимущество работы кросс платформенных NuGet, которая была запущена ранее доставлен этот выпуск с пакетом SDK для платформы Windows.</span><span class="sxs-lookup"><span data-stu-id="374ea-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="374ea-107">Эта версия расширения NuGet доступна только для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="374ea-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="374ea-108">Мы рекомендуем тех разработчиков, имеющих доступ к коллекции Visual Studio с обновлением до последней версии, доступен, как всегда, мы публикуем обновления, исправления ошибок и новые функции.</span><span class="sxs-lookup"><span data-stu-id="374ea-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="374ea-109">Расширение NuGet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="374ea-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="374ea-110">Проблемы и функции в этом выпуске помечены на сайте GitHub с [вехи «3.1 RTM UWP транзитивное поддержки»](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) в целом, мы закрытых 67 проблем в версии 3.1.</span><span class="sxs-lookup"><span data-stu-id="374ea-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="374ea-111">Новые функции</span><span class="sxs-lookup"><span data-stu-id="374ea-111">New Features</span></span>

* <span data-ttu-id="374ea-112">`project.json` поддерживает использование Windows UWP и ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="374ea-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="374ea-113">Транзитивное пакета установки</span><span class="sxs-lookup"><span data-stu-id="374ea-113">Transitive package installation</span></span>

<span data-ttu-id="374ea-114">Описания и определения этих функций можно найти в другом месте в документации.</span><span class="sxs-lookup"><span data-stu-id="374ea-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="374ea-115">Устарело</span><span class="sxs-lookup"><span data-stu-id="374ea-115">Deprecated</span></span>

<span data-ttu-id="374ea-116">Для Visual Studio 2015 больше не доступны следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="374ea-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="374ea-117">Больше нельзя устанавливать пакеты уровня решения</span><span class="sxs-lookup"><span data-stu-id="374ea-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="374ea-118">Следующие функции больше не доступны для Visual Studio 2015 и проекты, использующие `project.json` спецификации</span><span class="sxs-lookup"><span data-stu-id="374ea-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="374ea-119">`install.ps1` и `uninstall.ps1` -эти сценарии будут игнорироваться во время установки пакета, восстановление, обновления и удаления</span><span class="sxs-lookup"><span data-stu-id="374ea-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="374ea-120">Преобразования конфигурации будут пропущены</span><span class="sxs-lookup"><span data-stu-id="374ea-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="374ea-121">Содержимое будут перенесены, но не копируется в проект.</span><span class="sxs-lookup"><span data-stu-id="374ea-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="374ea-122">Повторно реализовать эту функцию, следите за обсуждениями и выполняться работает команда: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="374ea-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="374ea-123">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="374ea-123">Known Issues</span></span>

<span data-ttu-id="374ea-124">Обнаружены несколько известных проблем, присутствующие в этом выпуске.</span><span class="sxs-lookup"><span data-stu-id="374ea-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="374ea-125">Установки 3.1 версии с помощью пакета SDK для Windows 10 будет понизить любая версия расширения NuGet, который ранее был установлен</span><span class="sxs-lookup"><span data-stu-id="374ea-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="374ea-126">Командной строки NuGet</span><span class="sxs-lookup"><span data-stu-id="374ea-126">NuGet Command-line</span></span>

<span data-ttu-id="374ea-127">Исполняемый файл командной строки NuGet была обновлена и перемещен в новое расположение распространяемый таким образом, чтобы старые версии nuget.exe по-прежнему будут доступны.</span><span class="sxs-lookup"><span data-stu-id="374ea-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="374ea-128">3.1 бета-версии nuget.exe можно загрузить для Windows в: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="374ea-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="374ea-129">Новое расположение распространяемый находится на dist.nuget.org хост-компьютере и структуру папок, которая следует за этот шаблон:</span><span class="sxs-lookup"><span data-stu-id="374ea-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="374ea-130">Новые функции</span><span class="sxs-lookup"><span data-stu-id="374ea-130">New Features</span></span>

* <span data-ttu-id="374ea-131">NuGet.exe можно восстановить и установки пакетов в проекты, использующие `project.json` файл.</span><span class="sxs-lookup"><span data-stu-id="374ea-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="374ea-132">NuGet.exe может подключиться к и использовать протокол v3 NuGet на: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="374ea-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="374ea-133">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="374ea-133">Known Issues</span></span> ##

1.    <span data-ttu-id="374ea-134">Не удается выполнить пакет с `project.json` файл — [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="374ea-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="374ea-135">Не поддерживается в Mono — [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="374ea-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="374ea-136">Не локализован - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="374ea-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="374ea-137">Не имеет подписи, так же, как существующий http://nuget.org/nuget.exe  -  [бинарная](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="374ea-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
