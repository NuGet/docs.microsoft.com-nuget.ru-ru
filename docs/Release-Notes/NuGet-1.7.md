---
title: "Заметки о выпуске NuGet 1.7 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске для NuGet 1.7, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 1.7 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7b16bea8c6bcc77f814dd32a43b895b5e656c95d
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="6ae5e-104">Заметки о выпуске 1.7 NuGet</span><span class="sxs-lookup"><span data-stu-id="6ae5e-104">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="6ae5e-105">[Заметки о выпуске NuGet 1.6](../release-notes/nuget-1.6.md) | [NuGet 1.8 заметки о выпуске](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="6ae5e-105">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="6ae5e-106">NuGet 1.7 был выпущен 4 апреля 2012 г.</span><span class="sxs-lookup"><span data-stu-id="6ae5e-106">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="6ae5e-107">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="6ae5e-107">Known Installation Issue</span></span>
<span data-ttu-id="6ae5e-108">Если вы используете VS 2010 с пакетом обновления 1, вы можете столкнуться ошибка установки при попытке обновить NuGet, если у вас установлена более ранняя версия.</span><span class="sxs-lookup"><span data-stu-id="6ae5e-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="6ae5e-109">Достаточно просто удалить NuGet, а затем установить его из библиотеки расширения VS.</span><span class="sxs-lookup"><span data-stu-id="6ae5e-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="6ae5e-110">Дополнительные сведения см. на странице по адресу [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).</span><span class="sxs-lookup"><span data-stu-id="6ae5e-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="6ae5e-111">Примечание: Если Visual Studio не позволяют удалить расширение (кнопка удаления отключена), скорее всего, необходимо перезапустить Visual Studio, используя «Запуск от имени администратора».</span><span class="sxs-lookup"><span data-stu-id="6ae5e-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="6ae5e-112">Функции</span><span class="sxs-lookup"><span data-stu-id="6ae5e-112">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="6ae5e-113">Поддерживается открытие файла readme.txt после установки</span><span class="sxs-lookup"><span data-stu-id="6ae5e-113">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="6ae5e-114">Новые возможности в 1.7, если пакет содержит `readme.txt` файл в корне пакета NuGet автоматически открыть этот файл, после завершения установки пакета.</span><span class="sxs-lookup"><span data-stu-id="6ae5e-114">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="6ae5e-115">Показать предварительные версии пакетов в диалоговом окне NuGet управление пакетами</span><span class="sxs-lookup"><span data-stu-id="6ae5e-115">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="6ae5e-116">Диалоговое окно Управление пакетами NuGet теперь содержит раскрывающийся список, который предоставляет параметр для отображения предварительные выпуски пакетов.</span><span class="sxs-lookup"><span data-stu-id="6ae5e-116">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Отображение предварительные версии пакетов](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="6ae5e-118">Показать кнопку восстановить пакет, если отсутствуют файлы пакета</span><span class="sxs-lookup"><span data-stu-id="6ae5e-118">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="6ae5e-119">После открытия консоли диспетчера пакетов или NuGet диспетчера пакетов диалогового окна, проверит, если текущее решение включен режим восстановление пакетов NuGet, и если отсутствуют файлы пакета, `packages` папки.</span><span class="sxs-lookup"><span data-stu-id="6ae5e-119">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="6ae5e-120">Если эти два условия выполняются, NuGet сообщит, а отображается удобный «восстановить».</span><span class="sxs-lookup"><span data-stu-id="6ae5e-120">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="6ae5e-121">При нажатии этой кнопки, запускающие восстановления отсутствующих пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="6ae5e-121">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Кнопка восстановления пакета в диалоговом окне](./media/packagerestore-dialog.png)

![Кнопка восстановления пакета в консоли](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="6ae5e-124">Добавьте файл packages.config уровня решения</span><span class="sxs-lookup"><span data-stu-id="6ae5e-124">Add solution-level packages.config file</span></span>
<span data-ttu-id="6ae5e-125">В предыдущих версиях NuGet, каждый проект имеет `packages.config` файл, который отслеживает какие пакеты NuGet устанавливаются в этом проекте.</span><span class="sxs-lookup"><span data-stu-id="6ae5e-125">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="6ae5e-126">Однако отсутствовал аналогичный файл на уровне решения для отслеживания решения на уровне пакетов.</span><span class="sxs-lookup"><span data-stu-id="6ae5e-126">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="6ae5e-127">В результате не было возможности восстановления решения на уровне пакетов.</span><span class="sxs-lookup"><span data-stu-id="6ae5e-127">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="6ae5e-128">Эта функция реализована в NuGet 1.7.</span><span class="sxs-lookup"><span data-stu-id="6ae5e-128">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="6ae5e-129">Решения уровня `packages.config` файл помещается в `.nuget` папку решения корневой и будет хранить пакеты только на уровне решения.</span><span class="sxs-lookup"><span data-stu-id="6ae5e-129">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="6ae5e-130">Удалить команду New-Package</span><span class="sxs-lookup"><span data-stu-id="6ae5e-130">Remove New-Package command</span></span>
<span data-ttu-id="6ae5e-131">Из-за низкой загрузке команду New-пакет был удален.</span><span class="sxs-lookup"><span data-stu-id="6ae5e-131">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="6ae5e-132">Разработчикам рекомендуется использовать для создания пакетов nuget.exe или удобным обозреватель пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="6ae5e-132">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="6ae5e-133">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="6ae5e-133">Bug Fixes</span></span>
<span data-ttu-id="6ae5e-134">NuGet 1.7 исправил множество ошибок вокруг восстановление пакетов рабочего процесса и сценарии сети или системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="6ae5e-134">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="6ae5e-135">Полный список рабочих элементов исправления в NuGet 1.7, представление [NuGet отслеживания проблем в этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="6ae5e-135">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
