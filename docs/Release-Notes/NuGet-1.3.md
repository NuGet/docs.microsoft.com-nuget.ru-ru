---
title: Заметки о выпуске 1,3 NuGet
description: Заметки о выпуске для NuGet 1.3, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c0284fe0afb11bf6465897132cccd160674ea3e1
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="a396e-103">Заметки о выпуске 1,3 NuGet</span><span class="sxs-lookup"><span data-stu-id="a396e-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="a396e-104">[Заметки о выпуске NuGet 1.2](../release-notes/nuget-1.2.md) | [заметки о выпуске NuGet 1.4](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="a396e-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="a396e-105">NuGet 1.3 был выпущен 25 апреля 2011 г.</span><span class="sxs-lookup"><span data-stu-id="a396e-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="a396e-106">Новые функции</span><span class="sxs-lookup"><span data-stu-id="a396e-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="a396e-107">Упрощенное создание пакета с помощью интеграции сервера символов</span><span class="sxs-lookup"><span data-stu-id="a396e-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="a396e-108">Команды NuGet, сотрудничающих с ребятами [SymbolSource.org](http://www.symbolsource.org/) предоставляет очень простой способ публикации источников и PDB-файла вместе с вашего пакета.</span><span class="sxs-lookup"><span data-stu-id="a396e-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="a396e-109">Это позволяет клиентам пакета шаг с заходом в исходный для пакета в отладчике.</span><span class="sxs-lookup"><span data-stu-id="a396e-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="a396e-110">Дополнительные сведения см. в статье [создания и публикации пакета символов](../create-packages/symbol-packages.md) легко публиковать пакеты NuGet с источниками.</span><span class="sxs-lookup"><span data-stu-id="a396e-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="a396e-111">Также можно просматривать динамическую демонстрацию этой функции как часть NuGet в глубину обращения во Mix11.</span><span class="sxs-lookup"><span data-stu-id="a396e-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="a396e-112">Эта функция полностью демонстрируется начиная с 20-минутное знаком видео.</span><span class="sxs-lookup"><span data-stu-id="a396e-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="a396e-113">`Open-PackagePage` Команда</span><span class="sxs-lookup"><span data-stu-id="a396e-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="a396e-114">Эта команда позволяет легко перейти на страницу проекта для пакета из консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="a396e-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="a396e-115">Он также предоставляет параметры, чтобы открыть URL-адрес лицензии и о нарушении страницы отчета для пакета.</span><span class="sxs-lookup"><span data-stu-id="a396e-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="a396e-116">Ниже приведен синтаксис для команды.</span><span class="sxs-lookup"><span data-stu-id="a396e-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="a396e-117">`-PassThru` Параметр используется для возврата значения из указанного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="a396e-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="a396e-118">Примеры</span><span class="sxs-lookup"><span data-stu-id="a396e-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="a396e-119">Открывает в браузере URL-адрес проекта, указанный в пакете Ninject.</span><span class="sxs-lookup"><span data-stu-id="a396e-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="a396e-120">Открывает в браузере URL-адрес лицензии, указанный в пакете Ninject.</span><span class="sxs-lookup"><span data-stu-id="a396e-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="a396e-121">Открывает в браузере URL-адрес текущего источника пакетов, используемый для сообщения о нарушении для указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="a396e-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="a396e-122">Назначает URL-адрес лицензии переменной $url, не открывая его в браузере.</span><span class="sxs-lookup"><span data-stu-id="a396e-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="a396e-123">Улучшения производительности</span><span class="sxs-lookup"><span data-stu-id="a396e-123">Performance Improvements</span></span>

<span data-ttu-id="a396e-124">NuGet 1.3 предоставляет много улучшений производительности.</span><span class="sxs-lookup"><span data-stu-id="a396e-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="a396e-125">NuGet 1.3 позволяет избежать загрузки несколько раз одну и ту же версию пакета, включая кэш локального пользователя.</span><span class="sxs-lookup"><span data-stu-id="a396e-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="a396e-126">Кэш может осуществлять доступ к очищен через диалоговое окно параметров диспетчера пакетов:</span><span class="sxs-lookup"><span data-stu-id="a396e-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Диалоговое окно параметров NuGet с параметрами кэша пакета](./media/nuget-options.png)

<span data-ttu-id="a396e-128">Другие усовершенствования производительности включают добавление поддержка сжатия HTTP и повышение скорости установки пакета в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a396e-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="a396e-129">Visual Studio и nuget.exe использует тот же список источников пакетов</span><span class="sxs-lookup"><span data-stu-id="a396e-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="a396e-130">До NuGet 1.3 список источников пакетов, используемых nuget.exe NuGet Visual Studio надстройка и не были сохранены в том же месте.</span><span class="sxs-lookup"><span data-stu-id="a396e-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="a396e-131">NuGet 1.3 теперь использует тот же список в обоих местах.</span><span class="sxs-lookup"><span data-stu-id="a396e-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="a396e-132">Список хранится в `NuGet.Config` и помещен в папку AppData.</span><span class="sxs-lookup"><span data-stu-id="a396e-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="a396e-133">NuGet.exe не учитывает файлы и папки, которые начинаются с "." по умолчанию</span><span class="sxs-lookup"><span data-stu-id="a396e-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="a396e-134">Для упрощения работы с системами управления версиями, таких как Subversion и Mercurial NuGet, nuget.exe не учитывает папки и файлы, которые начинаются с "." символов при создании пакетов.</span><span class="sxs-lookup"><span data-stu-id="a396e-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="a396e-135">Это может быть переопределено с помощью двух новых флаги:</span><span class="sxs-lookup"><span data-stu-id="a396e-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="a396e-136">__-NoDefaultExcludes__ используется для переопределения этого параметра и включает все файлы.</span><span class="sxs-lookup"><span data-stu-id="a396e-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="a396e-137">__-Исключить__ используется для добавления других файлов и папок для исключения с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="a396e-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="a396e-138">Например, чтобы исключить все файлы с расширением '.bak'</span><span class="sxs-lookup"><span data-stu-id="a396e-138">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="a396e-139">_Примечание: шаблон не является рекурсивным по умолчанию._</span><span class="sxs-lookup"><span data-stu-id="a396e-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="a396e-140">Поддержка проектов WiX и Micro .NET Framework</span><span class="sxs-lookup"><span data-stu-id="a396e-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="a396e-141">Благодаря материалы сообщества NuGet включает поддержку WiX типы проектов, а также Micro .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a396e-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="a396e-142">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="a396e-142">Bug Fixes</span></span>

<span data-ttu-id="a396e-143">Полный список исправлений ошибок, просмотреть [NuGet отслеживания проблем в этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="a396e-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="a396e-144">Исправления следует отметить</span><span class="sxs-lookup"><span data-stu-id="a396e-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="a396e-145">Пакеты с исходными файлами работать в двух веб-сайтов и проектов веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="a396e-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="a396e-146">Для веб-сайтов, исходные файлы копируются в `App_Code` папки</span><span class="sxs-lookup"><span data-stu-id="a396e-146">For Websites, source files are copied into the `App_Code` folder</span></span>
