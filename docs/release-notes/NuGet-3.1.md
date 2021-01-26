---
title: Заметки о выпуске NuGet 3,1
description: Заметки о выпуске NuGet 3,1, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776536"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="04c33-103">Заметки о выпуске NuGet 3,1</span><span class="sxs-lookup"><span data-stu-id="04c33-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="04c33-104">[Заметки о](../release-notes/nuget-3.0.0.md)  |  выпуске NuGet 3,0 [Заметки о выпуске 3.1.1 NuGet](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="04c33-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="04c33-105">Пакет NuGet 3,1 был выпущен 27 июля 2015 в качестве упакованного расширения для пакета SDK универсальная платформа Windows для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="04c33-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="04c33-106">Мы доставили этот выпуск с помощью пакета SDK для платформы Windows, чтобы опыт разработки Windows мог воспользоваться преимуществами межплатформенных операций NuGet, которые были ранее запущены.</span><span class="sxs-lookup"><span data-stu-id="04c33-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="04c33-107">Эта версия расширения NuGet доступна только для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="04c33-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="04c33-108">Рекомендуется, чтобы разработчики, у которых есть доступ к коллекции Visual Studio, могли перейти к последней доступной версии, так как мы всегда публикуем обновления с исправлениями ошибок и новыми функциями.</span><span class="sxs-lookup"><span data-stu-id="04c33-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="04c33-109">Расширение NuGet для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="04c33-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="04c33-110">Проблемы и функции в этом выпуске помечаются на сайте GitHub на этапе "промежуточная [Поддержка версии UWP в 3,1 RTM"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  . Мы закрыли 67 в выпуске 3,1.</span><span class="sxs-lookup"><span data-stu-id="04c33-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="04c33-111">Новые возможности</span><span class="sxs-lookup"><span data-stu-id="04c33-111">New Features</span></span>

* <span data-ttu-id="04c33-112">`project.json` Поддержка Windows UWP и поддержки ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="04c33-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="04c33-113">Установка транзитивных пакетов</span><span class="sxs-lookup"><span data-stu-id="04c33-113">Transitive package installation</span></span>

<span data-ttu-id="04c33-114">Описание и определение этих функций можно найти в другой части документации.</span><span class="sxs-lookup"><span data-stu-id="04c33-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="04c33-115">Не рекомендуется</span><span class="sxs-lookup"><span data-stu-id="04c33-115">Deprecated</span></span>

<span data-ttu-id="04c33-116">Следующие функции больше не доступны для Visual Studio 2015:</span><span class="sxs-lookup"><span data-stu-id="04c33-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="04c33-117">Пакеты уровня решения больше не могут быть установлены</span><span class="sxs-lookup"><span data-stu-id="04c33-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="04c33-118">Следующие функции больше не доступны для Visual Studio 2015 и проектов, использующих `project.json` спецификацию.</span><span class="sxs-lookup"><span data-stu-id="04c33-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="04c33-119">`install.ps1` и `uninstall.ps1` — эти скрипты будут игнорироваться во время установки, восстановления, обновления и удаления пакета</span><span class="sxs-lookup"><span data-stu-id="04c33-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="04c33-120">Преобразования конфигурации будут пропущены</span><span class="sxs-lookup"><span data-stu-id="04c33-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="04c33-121">Содержимое будет перенесено, но не скопировано в проект.</span><span class="sxs-lookup"><span data-stu-id="04c33-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="04c33-122">Рабочая группа работает над повторной реализацией этой функции, следуйте обсуждению и прогрессу в: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="04c33-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="04c33-123">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="04c33-123">Known Issues</span></span>

<span data-ttu-id="04c33-124">В этом выпуске было доставлено несколько известных проблем.</span><span class="sxs-lookup"><span data-stu-id="04c33-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="04c33-125">Установка выпуска 3,1 с пакетом SDK для Windows 10 приведет к понижению версии установленного ранее расширения NuGet.</span><span class="sxs-lookup"><span data-stu-id="04c33-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="04c33-126">Командная строка NuGet</span><span class="sxs-lookup"><span data-stu-id="04c33-126">NuGet Command-line</span></span>

<span data-ttu-id="04c33-127">Исполняемый файл командной строки NuGet был обновлен и перемещен в новое распространяемое расположение, чтобы предыдущие версии nuget.exe могли стать доступными.</span><span class="sxs-lookup"><span data-stu-id="04c33-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="04c33-128">Бета-версию 3,1 nuget.exe для Windows можно скачать по адресу: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="04c33-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="04c33-129">Новое распространяемое расположение находится на узле dist.nuget.org со структурой папок, следующей за этим шаблоном:</span><span class="sxs-lookup"><span data-stu-id="04c33-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a><span data-ttu-id="04c33-130">Новые возможности</span><span class="sxs-lookup"><span data-stu-id="04c33-130">New Features</span></span>

* <span data-ttu-id="04c33-131">nuget.exe может восстанавливать и устанавливать пакеты в проекты, использующие `project.json` файл.</span><span class="sxs-lookup"><span data-stu-id="04c33-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="04c33-132">nuget.exe можете подключиться к протоколу NuGet v3 и использовать его по адресу: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="04c33-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="04c33-133">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="04c33-133">Known Issues</span></span> ##

1.    <span data-ttu-id="04c33-134">Невозможно выполнить пакет для `project.json` файла — [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="04c33-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="04c33-135">Не поддерживается на Mono- [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="04c33-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="04c33-136">Не локализовано — [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="04c33-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="04c33-137">Не подписан, как и существующий http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="04c33-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
