---
title: Заметки о выпуске NuGet 1,6
description: Заметки о выпуске NuGet 1,6, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2878d3809b2be4fb71f4e7b1a1e08e405ead44b9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384141"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="ce811-103">Заметки о выпуске NuGet 1,6</span><span class="sxs-lookup"><span data-stu-id="ce811-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="ce811-104">[Заметки о выпуске nuget 1,5](../release-notes/nuget-1.5.md) | [заметок о выпуске NuGet 1,7](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="ce811-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="ce811-105">Версия NuGet 1,6 была выпущена 13 декабря 2011 г.</span><span class="sxs-lookup"><span data-stu-id="ce811-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="ce811-106">Известная ошибка установки</span><span class="sxs-lookup"><span data-stu-id="ce811-106">Known Installation Issue</span></span>
<span data-ttu-id="ce811-107">Если вы используете VS 2010 с пакетом обновления 1 (SP1), при попытке обновить NuGet, если установлена более старая версия, может возникнуть ошибка установки.</span><span class="sxs-lookup"><span data-stu-id="ce811-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="ce811-108">Чтобы решить эту проблему, просто удалите NuGet, а затем установите его из коллекции расширений VS.</span><span class="sxs-lookup"><span data-stu-id="ce811-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="ce811-109">Дополнительные сведения см. в разделе <https://support.microsoft.com/kb/2581019>.</span><span class="sxs-lookup"><span data-stu-id="ce811-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="ce811-110">Примечание. Если Visual Studio не позволит удалить расширение (кнопка удаления отключена), скорее всего, потребуется перезапустить Visual Studio с помощью команды "Запуск от имени администратора".</span><span class="sxs-lookup"><span data-stu-id="ce811-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="ce811-111">Функции</span><span class="sxs-lookup"><span data-stu-id="ce811-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="ce811-112">Поддержка семантического управления версиями и предварительных пакетов</span><span class="sxs-lookup"><span data-stu-id="ce811-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="ce811-113">В NuGet 1,6 введена поддержка семантического управления версиями (SemVer).</span><span class="sxs-lookup"><span data-stu-id="ce811-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="ce811-114">Дополнительные сведения об использовании SemVer см. в [документации по системе управления версиями](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ce811-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="ce811-115">Использование NuGet без возврата пакетов (восстановление пакета)</span><span class="sxs-lookup"><span data-stu-id="ce811-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="ce811-116">NuGet 1,6 теперь обладает первой поддержкой класса для рабочего процесса, в котором пакеты NuGet не добавляются в систему управления версиями, а восстанавливаются во время сборки, если они отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="ce811-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="ce811-117">Дополнительные сведения см. в разделе [Использование NuGet без фиксации пакетов в системе управления версиями](../consume-packages/packages-and-source-control.md) .</span><span class="sxs-lookup"><span data-stu-id="ce811-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="ce811-118">Шаблоны элементов, устанавливающие пакеты NuGet</span><span class="sxs-lookup"><span data-stu-id="ce811-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="ce811-119">При построении на работе для поддержки предварительно установленного пакета NuGet в шаблонах проектов Visual Studio NuGet 1,6 также добавляет поддержку шаблонов элементов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ce811-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="ce811-120">Шаблоны элементов могут иметь связанные пакеты NuGet, которые устанавливаются при вызове шаблона.</span><span class="sxs-lookup"><span data-stu-id="ce811-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="ce811-121">Дополнительные сведения о том, как изменить шаблон проекта или элемента для установки пакетов NuGet, см. в разделе [пакеты в Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) .</span><span class="sxs-lookup"><span data-stu-id="ce811-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="ce811-122">Поддержка отключения источников пакетов</span><span class="sxs-lookup"><span data-stu-id="ce811-122">Support for disabling package sources</span></span>
<span data-ttu-id="ce811-123">Если настроено несколько источников пакетов, NuGet будет просматривать каждый из них для пакетов во время установки пакета и его зависимостей.</span><span class="sxs-lookup"><span data-stu-id="ce811-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="ce811-124">Источник пакета, который не работает по какой-либо причине, может значительно замедлить работу NuGet.</span><span class="sxs-lookup"><span data-stu-id="ce811-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="ce811-125">До NuGet 1,6 можно было удалить источник пакета, но затем необходимо запомнить сведения о том, когда нужно добавить его обратно.</span><span class="sxs-lookup"><span data-stu-id="ce811-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="ce811-126">NuGet 1,6 позволяет отменить проверку источника пакета, чтобы отключить его, но не учитывать его.</span><span class="sxs-lookup"><span data-stu-id="ce811-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Отключение пакета](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="ce811-128">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="ce811-128">Bug Fixes</span></span>
<span data-ttu-id="ce811-129">В NuGet 1,6 было исправлено всего 106 рабочих элементов.</span><span class="sxs-lookup"><span data-stu-id="ce811-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="ce811-130">95 из них были классифицированы как ошибки и 10 из них.</span><span class="sxs-lookup"><span data-stu-id="ce811-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="ce811-131">Полный список рабочих элементов, исправленных в NuGet 1,6, см. в [этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="ce811-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
