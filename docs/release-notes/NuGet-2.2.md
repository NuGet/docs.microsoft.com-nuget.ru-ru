---
title: Заметки о выпуске NuGet 2,2
description: Заметки о выпуске NuGet 2,2, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780437"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="d9064-103">Заметки о выпуске NuGet 2,2</span><span class="sxs-lookup"><span data-stu-id="d9064-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="d9064-104">[Заметки о](../release-notes/nuget-2.1.md)  |  выпуске NuGet 2,1 [Заметки о выпуске NuGet 2.2.1](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="d9064-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="d9064-105">Версия NuGet 2,2 была выпущена 12 декабря 2012 г.</span><span class="sxs-lookup"><span data-stu-id="d9064-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="d9064-106">Быстрый запуск Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d9064-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="d9064-107">Одной из новых функций, добавленных в Visual Studio 2012, было [диалоговое окно быстрого запуска](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="d9064-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="d9064-108">NuGet 2,2 расширяет это диалоговое окно, позволяя ему инициализировать диалоговое окно диспетчера пакетов с помощью условий поиска, вводимых в области Быстрый запуск.</span><span class="sxs-lookup"><span data-stu-id="d9064-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="d9064-109">Например, если ввести "jQuery" в быстрый запуск, в результатах поиска можно искать пакеты NuGet, соответствующие "jQuery".</span><span class="sxs-lookup"><span data-stu-id="d9064-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![Быстрый запуск NuGet в Visual Studio](./media/quick-launch.png)

<span data-ttu-id="d9064-111">При выборе этого параметра будет запущен стандартный интерфейс поиска диспетчера пакетов NuGet для термина jQuery.</span><span class="sxs-lookup"><span data-stu-id="d9064-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Диалоговое окно диспетчера пакетов NuGet предварительно заполнено](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="d9064-113">Указать всю папку для содержимого пакета</span><span class="sxs-lookup"><span data-stu-id="d9064-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="d9064-114">NuGet 2,2 теперь позволяет указать всю папку в `<file>` элементе `.nuspec` файла, чтобы включить все содержимое этой папки.</span><span class="sxs-lookup"><span data-stu-id="d9064-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="d9064-115">Например, следующий сценарий приведет к добавлению всех скриптов в папке Scripts пакета в папку контентс\скриптс при установке пакета в проект.</span><span class="sxs-lookup"><span data-stu-id="d9064-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="d9064-116">**Обновление 6/24/16: при установке пакета пустые папки в папке "содержимое" игнорируются.**</span><span class="sxs-lookup"><span data-stu-id="d9064-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="d9064-117">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="d9064-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="d9064-118">Сбой установки пакета для проектов F # при использовании консоли диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="d9064-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="d9064-119">При попытке установить пакет NuGet в проект F # с помощью консоли диспетчера пакетов создается исключение InvalidOperationException.</span><span class="sxs-lookup"><span data-stu-id="d9064-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="d9064-120">Мы активно работаем с командой F # для устранения проблемы, но в то же время обходной путь заключается в установке пакетов NuGet в проекты F # с помощью диалогового окна диспетчера пакетов NuGet, а не консоли.</span><span class="sxs-lookup"><span data-stu-id="d9064-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="d9064-121">[Дополнительные сведения можно найти на сайте CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="d9064-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="d9064-122">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="d9064-122">Bug Fixes</span></span>
<span data-ttu-id="d9064-123">NuGet 2,2 включает множество исправлений ошибок.</span><span class="sxs-lookup"><span data-stu-id="d9064-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="d9064-124">Полный список рабочих элементов, исправленных в NuGet 2,2, см. в [этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="d9064-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
