---
title: Заметки о выпуске версии 2.2 NuGet
description: Заметки о выпуске для NuGet 2.2, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 21f212de53da5faf1ec0762f97a840968b615b19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="1a975-103">Заметки о выпуске версии 2.2 NuGet</span><span class="sxs-lookup"><span data-stu-id="1a975-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="1a975-104">[Заметки о выпуске NuGet 2.1](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 заметки о выпуске](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="1a975-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="1a975-105">12 декабря 2012 года была выпущена NuGet 2.2.</span><span class="sxs-lookup"><span data-stu-id="1a975-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="1a975-106">Быстрый запуск Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1a975-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="1a975-107">Одна из новых функций, добавленные в Visual Studio 2012 была [диалогового окна быстрого запуска](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="1a975-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="1a975-108">NuGet 2.2 расширяет это диалоговое окно, что позволяет инициализировать диалоговое окно диспетчера пакета с условиями поиска, введенных на панели быстрого запуска.</span><span class="sxs-lookup"><span data-stu-id="1a975-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="1a975-109">Например введите «jquery» на панели быстрого запуска теперь содержит параметр в результатах поиска соответствия «jquery» пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="1a975-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![NuGet в Visual Studio быстрого запуска](./media/quick-launch.png)

<span data-ttu-id="1a975-111">При выборе этого параметра приведет к запуску результатов поиска диспетчера пакета Стандартная NuGet для термина «jquery».</span><span class="sxs-lookup"><span data-stu-id="1a975-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Диалоговое окно диспетчера пакетов NuGet предварительно заполненных](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="1a975-113">Укажите всю папку для пакета содержимого</span><span class="sxs-lookup"><span data-stu-id="1a975-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="1a975-114">NuGet 2.2 теперь можно указать всю папку, в `<file>` элемент `.nuspec` файла следует включить все содержимое этой папки.</span><span class="sxs-lookup"><span data-stu-id="1a975-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="1a975-115">Например следующие приведет все скрипты в папке скриптов пакет добавляется в папку contents\scripts при установке пакета в проект.</span><span class="sxs-lookup"><span data-stu-id="1a975-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="1a975-116">**Обновить 24/6/16: пустые папки в папку «content» учитываются при установке пакета.**</span><span class="sxs-lookup"><span data-stu-id="1a975-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="1a975-117">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="1a975-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="1a975-118">При использовании консоли диспетчера пакетов для проектов F # сбой установки пакета</span><span class="sxs-lookup"><span data-stu-id="1a975-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="1a975-119">При попытке установить пакет NuGet в проекте F #, используя консоль диспетчера пакетов, выдается исключение InvalidOperationException.</span><span class="sxs-lookup"><span data-stu-id="1a975-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="1a975-120">Мы активно работаем команде F #, чтобы устранить проблему, но в то же время достаточно установить пакеты NuGet в проектов F # с помощью диалогового окна диспетчера пакетов NuGet, а не консоли.</span><span class="sxs-lookup"><span data-stu-id="1a975-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="1a975-121">[Дополнительные сведения можно найти на сайте CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="1a975-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="1a975-122">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="1a975-122">Bug Fixes</span></span>
<span data-ttu-id="1a975-123">NuGet 2.2 содержит много исправлений ошибок.</span><span class="sxs-lookup"><span data-stu-id="1a975-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="1a975-124">Полный список рабочих элементов исправления в NuGet 2.2, представление [NuGet отслеживания проблем в этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="1a975-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
