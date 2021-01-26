---
title: Заметки о выпуске NuGet 1,7
description: Заметки о выпуске NuGet 1,7, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777065"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="39415-103">Заметки о выпуске NuGet 1,7</span><span class="sxs-lookup"><span data-stu-id="39415-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="39415-104">[Заметки о](../release-notes/nuget-1.6.md)  |  выпуске NuGet 1,6 [Заметки о выпуске NuGet 1,8](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="39415-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="39415-105">Версия NuGet 1,7 была выпущена 4 апреля 2012 г.</span><span class="sxs-lookup"><span data-stu-id="39415-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="39415-106">Известная ошибка установки</span><span class="sxs-lookup"><span data-stu-id="39415-106">Known Installation Issue</span></span>
<span data-ttu-id="39415-107">Если вы используете VS 2010 с пакетом обновления 1 (SP1), при попытке обновить NuGet, если установлена более старая версия, может возникнуть ошибка установки.</span><span class="sxs-lookup"><span data-stu-id="39415-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="39415-108">Чтобы решить эту проблему, просто удалите NuGet, а затем установите его из коллекции расширений VS.</span><span class="sxs-lookup"><span data-stu-id="39415-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="39415-109">Дополнительные сведения см. в разделе <https://support.microsoft.com/kb/2581019>.</span><span class="sxs-lookup"><span data-stu-id="39415-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="39415-110">Примечание. Если Visual Studio не позволит удалить расширение (кнопка удаления отключена), скорее всего, потребуется перезапустить Visual Studio с помощью команды "Запуск от имени администратора".</span><span class="sxs-lookup"><span data-stu-id="39415-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="39415-111">Компоненты</span><span class="sxs-lookup"><span data-stu-id="39415-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="39415-112">Поддержка открытия файла readme.txt после установки</span><span class="sxs-lookup"><span data-stu-id="39415-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="39415-113">Новое в 1,7. Если пакет содержит `readme.txt` файл в корне пакета, то NuGet автоматически откроет этот файл после завершения установки пакета.</span><span class="sxs-lookup"><span data-stu-id="39415-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="39415-114">Показывать пакеты предварительной версии в диалоговом окне "Управление пакетами NuGet"</span><span class="sxs-lookup"><span data-stu-id="39415-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="39415-115">Диалоговое окно Управление пакетами NuGet теперь включает в себя раскрывающийся список, который предоставляет параметр для отображения предварительных пакетов.</span><span class="sxs-lookup"><span data-stu-id="39415-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Отображение предварительных пакетов](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="39415-117">Показывать кнопку восстановления пакета при отсутствии файлов пакета</span><span class="sxs-lookup"><span data-stu-id="39415-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="39415-118">При открытии консоли диспетчера пакетов или диалогового окна Диспетчер пакетов NuGet, NuGet проверяет, включен ли в текущем решении режим восстановления пакета, и если в папке отсутствуют файлы пакета `packages` .</span><span class="sxs-lookup"><span data-stu-id="39415-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="39415-119">Если эти два условия выполнены, NuGet уведомляет вас и покажет удобную кнопку восстановления.</span><span class="sxs-lookup"><span data-stu-id="39415-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="39415-120">Нажатие этой кнопки приведет к активации NuGet для восстановления всех отсутствующих пакетов.</span><span class="sxs-lookup"><span data-stu-id="39415-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Кнопка восстановления пакета в диалоговом окне](./media/packagerestore-dialog.png)

![Кнопка восстановления пакета в консоли](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="39415-123">Добавить файл packages.config уровня решения</span><span class="sxs-lookup"><span data-stu-id="39415-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="39415-124">В предыдущих версиях NuGet каждый проект имеет `packages.config` файл, который отслеживает, какие пакеты NuGet установлены в этом проекте.</span><span class="sxs-lookup"><span data-stu-id="39415-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="39415-125">Однако на уровне решения не существовало похожего файла для наблюдения за пакетами уровня решения.</span><span class="sxs-lookup"><span data-stu-id="39415-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="39415-126">В результате не существовало способа восстановить пакеты уровня решения.</span><span class="sxs-lookup"><span data-stu-id="39415-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="39415-127">Теперь эта функция реализована в NuGet 1,7.</span><span class="sxs-lookup"><span data-stu-id="39415-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="39415-128">Файл уровня решения `packages.config` помещается в папку в `.nuget` корневом каталоге решения и будет хранить только пакеты уровня решения.</span><span class="sxs-lookup"><span data-stu-id="39415-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="39415-129">Команда удаления New-Package</span><span class="sxs-lookup"><span data-stu-id="39415-129">Remove New-Package command</span></span>
<span data-ttu-id="39415-130">Из-за низкого уровня использования команда New-Package была удалена.</span><span class="sxs-lookup"><span data-stu-id="39415-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="39415-131">Разработчики рекомендуют использовать nuget.exe или удобный обозреватель пакетов NuGet для создания пакетов.</span><span class="sxs-lookup"><span data-stu-id="39415-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="39415-132">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="39415-132">Bug Fixes</span></span>
<span data-ttu-id="39415-133">В NuGet 1,7 устранено много ошибок, связанных с рабочим процессом восстановления пакетов и сценариями управления сетями и источниками.</span><span class="sxs-lookup"><span data-stu-id="39415-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="39415-134">Полный список рабочих элементов, исправленных в NuGet 1,7, см. в [этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="39415-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
