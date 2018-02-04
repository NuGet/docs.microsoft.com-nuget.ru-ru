---
title: "Заметки о выпуске NuGet 3.1 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске для NuGet 3.1, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 3.1 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a7aa43b8701b3bbef8f6ebce9a5d636ee1bc6abe
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="43afe-104">Заметки о выпуске 3.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="43afe-104">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="43afe-105">[Заметки о выпуске NuGet 3.0](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 заметки о выпуске](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="43afe-105">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="43afe-106">NuGet 3.1 был выпущен 27 июля 2015 г. как расширение распространение для универсальных Windows Platform SDK для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="43afe-106">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="43afe-107">Мы доставлено этой версии с Windows Platform SDK, чтобы процесс разработки Windows может использовать преимущества работы кросс платформенных NuGet, которая ранее была запущена.</span><span class="sxs-lookup"><span data-stu-id="43afe-107">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="43afe-108">Эта версия расширения NuGet доступна только для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="43afe-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="43afe-109">Мы рекомендуем разработчиков, которые имеют доступ к коллекции Visual Studio обновление до последней версии, которая доступна, как мы всегда выполняется публикация обновлений с помощью исправления и новые функции.</span><span class="sxs-lookup"><span data-stu-id="43afe-109">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="43afe-110">Расширение NuGet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="43afe-110">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="43afe-111">Проблемы и функций в этом выпуске помечены в GitHub с [вехи «3.1 RTM UWP транзитивное поддержки»](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) всего, мы закрытых 67 проблем в версии 3.1.</span><span class="sxs-lookup"><span data-stu-id="43afe-111">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="43afe-112">Новые функции</span><span class="sxs-lookup"><span data-stu-id="43afe-112">New Features</span></span>

* <span data-ttu-id="43afe-113">`project.json`Поддержка для поддержки Windows UWP и ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="43afe-113">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="43afe-114">Транзитивное пакета установки</span><span class="sxs-lookup"><span data-stu-id="43afe-114">Transitive package installation</span></span>

<span data-ttu-id="43afe-115">Описание и определение этих возможностей можно найти в другом месте в документации.</span><span class="sxs-lookup"><span data-stu-id="43afe-115">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="43afe-116">Рекомендуется использовать</span><span class="sxs-lookup"><span data-stu-id="43afe-116">Deprecated</span></span>

<span data-ttu-id="43afe-117">Для Visual Studio 2015 больше недоступны следующие функции:</span><span class="sxs-lookup"><span data-stu-id="43afe-117">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="43afe-118">Больше нельзя устанавливать пакеты уровня решения</span><span class="sxs-lookup"><span data-stu-id="43afe-118">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="43afe-119">Следующие функции недоступны для Visual Studio 2015 и проектов, использующих `project.json` спецификации</span><span class="sxs-lookup"><span data-stu-id="43afe-119">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="43afe-120">`install.ps1`и `uninstall.ps1` -эти сценарии будут пропущены во время установки пакета, восстановление, обновление и удаление</span><span class="sxs-lookup"><span data-stu-id="43afe-120">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="43afe-121">Конфигурация преобразования будет игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="43afe-121">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="43afe-122">Содержимое будет выполнена, но не копируется в проект.</span><span class="sxs-lookup"><span data-stu-id="43afe-122">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="43afe-123">Повторно реализовать эту функцию, обсуждения и инструкциями хода выполнения, в которой работает команда: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="43afe-123">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="43afe-124">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="43afe-124">Known Issues</span></span>

<span data-ttu-id="43afe-125">Обнаружены несколько известных проблем, присутствующие в этом выпуске.</span><span class="sxs-lookup"><span data-stu-id="43afe-125">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="43afe-126">3.1 выпуска с помощью пакета SDK Windows 10 будет произведено изменение настроек любой версии расширение NuGet, который был ранее установлен</span><span class="sxs-lookup"><span data-stu-id="43afe-126">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="43afe-127">NuGet командной строки</span><span class="sxs-lookup"><span data-stu-id="43afe-127">NuGet Command-line</span></span>

<span data-ttu-id="43afe-128">Исполняемый файл командной строки NuGet была обновлена и перемещен в новое расположение распространяемый, что исторические версии nuget.exe продолжения должны быть доступны.</span><span class="sxs-lookup"><span data-stu-id="43afe-128">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="43afe-129">Вы можете скачать 3.1 бета-версии nuget.exe для Windows, посетите: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="43afe-129">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="43afe-130">Новое расположение распространяемый находится на узле dist.nuget.org со структурой папок, соответствует этому шаблону.</span><span class="sxs-lookup"><span data-stu-id="43afe-130">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="43afe-131">Новые функции</span><span class="sxs-lookup"><span data-stu-id="43afe-131">New Features</span></span>

* <span data-ttu-id="43afe-132">можно восстановить и установить пакеты в проекты, использующие NuGet.exe `project.json` файл.</span><span class="sxs-lookup"><span data-stu-id="43afe-132">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="43afe-133">можно подключиться и использовать протокол v3 NuGet на NuGet.exe: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="43afe-133">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="43afe-134">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="43afe-134">Known Issues</span></span> ##

1.    <span data-ttu-id="43afe-135">Не удается выполнить пакет с `project.json` файл - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="43afe-135">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="43afe-136">Не поддерживается в моно - [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="43afe-136">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="43afe-137">Не локализован - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="43afe-137">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="43afe-138">Не имеет подписи, так же, как существующие http://nuget.org/nuget.exe - [бинарная](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="43afe-138">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
