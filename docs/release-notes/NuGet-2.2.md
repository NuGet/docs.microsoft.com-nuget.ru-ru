---
title: Заметки о выпуске версии 2.2 NuGet
description: Заметки о выпуске для NuGet 2.2, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545996"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="41911-103">Заметки о выпуске версии 2.2 NuGet</span><span class="sxs-lookup"><span data-stu-id="41911-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="41911-104">[Заметки о выпуске NuGet 2.1](../release-notes/nuget-2.1.md) | [заметки о выпуске NuGet 2.2.1](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="41911-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="41911-105">NuGet 2.2 была выпущена 12 декабря 2012 г.</span><span class="sxs-lookup"><span data-stu-id="41911-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="41911-106">Быстрый запуск Visual Studio</span><span class="sxs-lookup"><span data-stu-id="41911-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="41911-107">Одна из новых функций, добавленных в Visual Studio 2012 был [диалоговое окно быстрого запуска](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="41911-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="41911-108">NuGet 2.2 расширяет это диалоговое окно, что позволяет инициализировать диалоговое окно диспетчера пакета с условиями поиска, введенные в панели быстрого запуска.</span><span class="sxs-lookup"><span data-stu-id="41911-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="41911-109">Например введя «jquery» на панели быстрого запуска теперь включает в себя параметр в результатах поиска пакетов NuGet по запросу «jquery».</span><span class="sxs-lookup"><span data-stu-id="41911-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![NuGet в Visual Studio быстрого запуска](./media/quick-launch.png)

<span data-ttu-id="41911-111">При выборе этого параметра приведет к запуску стандартный NuGet пакета диспетчера реализации возможностей поиска для термина «jquery».</span><span class="sxs-lookup"><span data-stu-id="41911-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Диалоговое окно диспетчера пакетов NuGet, предварительно заполненный](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="41911-113">Укажите всю папку для пакета содержимого</span><span class="sxs-lookup"><span data-stu-id="41911-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="41911-114">NuGet 2.2 теперь можно указать всю папку в `<file>` элемент `.nuspec` файл, чтобы включить все содержимое этой папки.</span><span class="sxs-lookup"><span data-stu-id="41911-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="41911-115">Например ниже приведет все скрипты в папке scripts пакета для добавления к папке contents\scripts при установке пакета в проект.</span><span class="sxs-lookup"><span data-stu-id="41911-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="41911-116">**Обновление 6/24/16: пустые папки в папке «content» учитываются при установке пакета.**</span><span class="sxs-lookup"><span data-stu-id="41911-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="41911-117">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="41911-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="41911-118">Установка пакета завершается сбоем для проектов F #, при использовании консоли диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="41911-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="41911-119">При попытке установить пакет NuGet в проекте F # с помощью консоли диспетчера пакетов, генерируется исключение InvalidOperationException.</span><span class="sxs-lookup"><span data-stu-id="41911-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="41911-120">Мы активно работаем с группой разработки F # для решения проблемы, но в то же время обходным путем является установка пакетов NuGet в проектах F # с помощью диалогового окна диспетчера пакетов NuGet, а не консоль.</span><span class="sxs-lookup"><span data-stu-id="41911-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="41911-121">[Дополнительные сведения можно найти на сайте CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="41911-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="41911-122">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="41911-122">Bug Fixes</span></span>
<span data-ttu-id="41911-123">NuGet 2.2 включает множество исправлений ошибок.</span><span class="sxs-lookup"><span data-stu-id="41911-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="41911-124">Полный список рабочих элементов исправленные в NuGet 2.2, пожалуйста представление [Issue Tracker NuGet для этого выпуска](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="41911-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
