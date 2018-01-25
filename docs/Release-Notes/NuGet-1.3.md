---
title: "Заметки о выпуске NuGet 1.3 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске для NuGet 1.3, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 1.3 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 59169be5b39ba4436e13e0935a0ad6efa724e08e
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="05aca-104">Заметки о выпуске 1,3 NuGet</span><span class="sxs-lookup"><span data-stu-id="05aca-104">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="05aca-105">[Заметки о выпуске NuGet 1.2](../release-notes/nuget-1.2.md) | [заметки о выпуске NuGet 1.4](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="05aca-105">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="05aca-106">NuGet 1.3 был выпущен 25 апреля 2011 г.</span><span class="sxs-lookup"><span data-stu-id="05aca-106">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="05aca-107">Новые функции</span><span class="sxs-lookup"><span data-stu-id="05aca-107">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="05aca-108">Упрощенное создание пакета с помощью интеграции сервера символов</span><span class="sxs-lookup"><span data-stu-id="05aca-108">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="05aca-109">Команды NuGet, сотрудничающих с ребятами [SymbolSource.org](http://www.symbolsource.org/) предоставляет очень простой способ публикации источников и PDB-файла вместе с вашего пакета.</span><span class="sxs-lookup"><span data-stu-id="05aca-109">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="05aca-110">Это позволяет клиентам пакета шаг с заходом в исходный для пакета в отладчике.</span><span class="sxs-lookup"><span data-stu-id="05aca-110">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="05aca-111">Дополнительные сведения см. в статье [создания и публикации пакета символов](../create-packages/symbol-packages.md) легко публиковать пакеты NuGet с источниками.</span><span class="sxs-lookup"><span data-stu-id="05aca-111">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="05aca-112">Также можно просматривать динамическую демонстрацию этой функции как часть NuGet в глубину обращения во Mix11.</span><span class="sxs-lookup"><span data-stu-id="05aca-112">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="05aca-113">Эта функция полностью демонстрируется начиная с 20-минутное знаком видео.</span><span class="sxs-lookup"><span data-stu-id="05aca-113">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="05aca-114">`Open-PackagePage`Команда</span><span class="sxs-lookup"><span data-stu-id="05aca-114">`Open-PackagePage` Command</span></span>

<span data-ttu-id="05aca-115">Эта команда позволяет легко перейти на страницу проекта для пакета из консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="05aca-115">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="05aca-116">Он также предоставляет параметры, чтобы открыть URL-адрес лицензии и о нарушении страницы отчета для пакета.</span><span class="sxs-lookup"><span data-stu-id="05aca-116">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="05aca-117">Ниже приведен синтаксис для команды.</span><span class="sxs-lookup"><span data-stu-id="05aca-117">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="05aca-118">`-PassThru` Параметр используется для возврата значения из указанного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="05aca-118">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="05aca-119">Примеры</span><span class="sxs-lookup"><span data-stu-id="05aca-119">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="05aca-120">Открывает в браузере URL-адрес проекта, указанный в пакете Ninject.</span><span class="sxs-lookup"><span data-stu-id="05aca-120">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="05aca-121">Открывает в браузере URL-адрес лицензии, указанный в пакете Ninject.</span><span class="sxs-lookup"><span data-stu-id="05aca-121">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="05aca-122">Открывает в браузере URL-адрес текущего источника пакетов, используемый для сообщения о нарушении для указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="05aca-122">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="05aca-123">Назначает URL-адрес лицензии переменной $url, не открывая его в браузере.</span><span class="sxs-lookup"><span data-stu-id="05aca-123">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="05aca-124">Улучшения производительности</span><span class="sxs-lookup"><span data-stu-id="05aca-124">Performance Improvements</span></span>

<span data-ttu-id="05aca-125">NuGet 1.3 предоставляет много улучшений производительности.</span><span class="sxs-lookup"><span data-stu-id="05aca-125">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="05aca-126">NuGet 1.3 позволяет избежать загрузки несколько раз одну и ту же версию пакета, включая кэш локального пользователя.</span><span class="sxs-lookup"><span data-stu-id="05aca-126">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="05aca-127">Кэш может осуществлять доступ к очищен через диалоговое окно параметров диспетчера пакетов:</span><span class="sxs-lookup"><span data-stu-id="05aca-127">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Диалоговое окно параметров NuGet с параметрами кэша пакета](./media/nuget-options.png)

<span data-ttu-id="05aca-129">Другие усовершенствования производительности включают добавление поддержка сжатия HTTP и повышение скорости установки пакета в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="05aca-129">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="05aca-130">Visual Studio и nuget.exe использует тот же список источников пакетов</span><span class="sxs-lookup"><span data-stu-id="05aca-130">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="05aca-131">До NuGet 1.3 список источников пакетов, используемых nuget.exe NuGet Visual Studio надстройка и не были сохранены в том же месте.</span><span class="sxs-lookup"><span data-stu-id="05aca-131">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="05aca-132">NuGet 1.3 теперь использует тот же список в обоих местах.</span><span class="sxs-lookup"><span data-stu-id="05aca-132">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="05aca-133">Список хранится в `NuGet.Config` и помещен в папку AppData.</span><span class="sxs-lookup"><span data-stu-id="05aca-133">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="05aca-134">NuGet.exe не учитывает файлы и папки, которые начинаются с "." по умолчанию</span><span class="sxs-lookup"><span data-stu-id="05aca-134">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="05aca-135">Для упрощения работы с системами управления версиями, таких как Subversion и Mercurial NuGet, nuget.exe не учитывает папки и файлы, которые начинаются с "." символов при создании пакетов.</span><span class="sxs-lookup"><span data-stu-id="05aca-135">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="05aca-136">Это может быть переопределено с помощью двух новых флаги:</span><span class="sxs-lookup"><span data-stu-id="05aca-136">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="05aca-137">__-NoDefaultExcludes__ используется для переопределения этого параметра и включает все файлы.</span><span class="sxs-lookup"><span data-stu-id="05aca-137">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="05aca-138">__-Исключить__ используется для добавления других файлов и папок для исключения с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="05aca-138">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="05aca-139">Например, чтобы исключить все файлы с расширением '.bak'</span><span class="sxs-lookup"><span data-stu-id="05aca-139">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="05aca-140">_Примечание: шаблон не является рекурсивным по умолчанию._</span><span class="sxs-lookup"><span data-stu-id="05aca-140">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="05aca-141">Поддержка проектов WiX и Micro .NET Framework</span><span class="sxs-lookup"><span data-stu-id="05aca-141">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="05aca-142">Благодаря материалы сообщества NuGet включает поддержку WiX типы проектов, а также Micro .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="05aca-142">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="05aca-143">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="05aca-143">Bug Fixes</span></span>

<span data-ttu-id="05aca-144">Полный список исправлений ошибок, просмотреть [NuGet отслеживания проблем в этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="05aca-144">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="05aca-145">Исправления следует отметить</span><span class="sxs-lookup"><span data-stu-id="05aca-145">Bug fixes worth noting</span></span>

* <span data-ttu-id="05aca-146">Пакеты с исходными файлами работать в двух веб-сайтов и проектов веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="05aca-146">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="05aca-147">Для веб-сайтов, исходные файлы копируются в `App_Code` папки</span><span class="sxs-lookup"><span data-stu-id="05aca-147">For Websites, source files are copied into the `App_Code` folder</span></span>
