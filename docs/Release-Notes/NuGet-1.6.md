---
title: "Заметки о выпуске NuGet 1.6 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске для NuGet 1.6, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 1.6 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 114b03cede24dee520ace1d8aa920a648ad16af1
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2018
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="0714c-104">Заметки о выпуске 1,6 NuGet</span><span class="sxs-lookup"><span data-stu-id="0714c-104">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="0714c-105">[Заметки о выпуске NuGet 1.5](../release-notes/nuget-1.5.md) | [NuGet 1.7 заметки о выпуске](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="0714c-105">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="0714c-106">13 декабря 2011 года была выпущена NuGet 1.6.</span><span class="sxs-lookup"><span data-stu-id="0714c-106">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="0714c-107">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="0714c-107">Known Installation Issue</span></span>
<span data-ttu-id="0714c-108">Если вы используете VS 2010 с пакетом обновления 1, вы можете столкнуться ошибка установки при попытке обновить NuGet, если у вас установлена более ранняя версия.</span><span class="sxs-lookup"><span data-stu-id="0714c-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="0714c-109">Достаточно просто удалить NuGet, а затем установить его из библиотеки расширения VS.</span><span class="sxs-lookup"><span data-stu-id="0714c-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="0714c-110">Дополнительные сведения см. на странице по адресу [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).</span><span class="sxs-lookup"><span data-stu-id="0714c-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="0714c-111">Примечание: Если Visual Studio не позволяют удалить расширение (кнопка удаления отключена), скорее всего, необходимо перезапустить Visual Studio, используя «Запуск от имени администратора».</span><span class="sxs-lookup"><span data-stu-id="0714c-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="0714c-112">Функции</span><span class="sxs-lookup"><span data-stu-id="0714c-112">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="0714c-113">Поддержка семантического управления версиями и предварительные версии пакетов</span><span class="sxs-lookup"><span data-stu-id="0714c-113">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="0714c-114">NuGet 1.6 появилась поддержка семантического управления версиями (SemVer).</span><span class="sxs-lookup"><span data-stu-id="0714c-114">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="0714c-115">Дополнительные сведения об использовании SemVer чтения [управление версиями документации](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="0714c-115">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="0714c-116">С помощью NuGet без проверки в пакетах (восстановление пакета)</span><span class="sxs-lookup"><span data-stu-id="0714c-116">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="0714c-117">NuGet 1.6 теперь полностью поддерживает для рабочего процесса, в какие NuGet пакеты не добавляются в систему управления версиями, но вместо этого будут восстановлены во время построения, если отсутствует.</span><span class="sxs-lookup"><span data-stu-id="0714c-117">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="0714c-118">Дополнительные сведения см. в статье [с помощью NuGet без фиксации пакетов в систему управления версиями](../consume-packages/packages-and-source-control.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="0714c-118">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="0714c-119">Шаблоны элементов, установить пакеты NuGet</span><span class="sxs-lookup"><span data-stu-id="0714c-119">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="0714c-120">Основываясь на работает для поддержки предварительно установленного пакета NuGet для шаблонов проектов Visual Studio, NuGet 1.6 также добавляет поддержку для шаблонов элементов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0714c-120">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="0714c-121">Шаблоны элементов могут иметь связанные пакеты NuGet, которые устанавливаются при вызове шаблона.</span><span class="sxs-lookup"><span data-stu-id="0714c-121">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="0714c-122">Дополнительные сведения о способах изменения шаблона проекта или элемента для установки пакетов NuGet читать [пакетов в Visual Studio шаблоны](../visual-studio-extensibility/visual-studio-templates.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="0714c-122">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="0714c-123">Поддержка отключения источники пакетов</span><span class="sxs-lookup"><span data-stu-id="0714c-123">Support for disabling package sources</span></span>
<span data-ttu-id="0714c-124">При настройке нескольких источников пакета NuGet будет выглядеть в каждом из них для пакетов во время установки пакета и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="0714c-124">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="0714c-125">Источник пакета, не работает для какой-либо причине может значительно замедлить NuGet.</span><span class="sxs-lookup"><span data-stu-id="0714c-125">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="0714c-126">До NuGet 1.6 источника пакета можно удалить, но вам придется запоминать подробности при необходимости добавьте его обратно в.</span><span class="sxs-lookup"><span data-stu-id="0714c-126">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="0714c-127">NuGet 1.6 позволяет источнику пакета, чтобы отключить его, но сохранить его вокруг сняв флажок.</span><span class="sxs-lookup"><span data-stu-id="0714c-127">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Отключение пакета](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="0714c-129">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="0714c-129">Bug Fixes</span></span>
<span data-ttu-id="0714c-130">NuGet 1.6 было всего 106 рабочие элементы фиксированной.</span><span class="sxs-lookup"><span data-stu-id="0714c-130">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="0714c-131">95 те из них были классифицируются как ошибки и 10 из них были функции.</span><span class="sxs-lookup"><span data-stu-id="0714c-131">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="0714c-132">Полный список рабочих элементов исправления в NuGet версии 1.6, представление [NuGet отслеживания проблем в этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="0714c-132">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
