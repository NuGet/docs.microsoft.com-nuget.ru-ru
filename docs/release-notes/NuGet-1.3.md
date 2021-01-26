---
title: Заметки о выпуске NuGet 1,3
description: Заметки о выпуске NuGet 1,3, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 54eda149352810eacc1d6340ad16cec1b03194e3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777114"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="12b24-103">Заметки о выпуске NuGet 1,3</span><span class="sxs-lookup"><span data-stu-id="12b24-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="12b24-104">[Заметки о](../release-notes/nuget-1.2.md)  |  выпуске NuGet 1,2 [Заметки о выпуске NuGet 1,4](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="12b24-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="12b24-105">Версия NuGet 1,3 была выпущена 25 апреля 2011.</span><span class="sxs-lookup"><span data-stu-id="12b24-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="12b24-106">Новые возможности</span><span class="sxs-lookup"><span data-stu-id="12b24-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="12b24-107">Упрощенное создание пакетов с помощью интеграции с сервером символов</span><span class="sxs-lookup"><span data-stu-id="12b24-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="12b24-108">Группа NuGet, которая взаимодействует с сотрудниками в [SymbolSource.org](http://www.symbolsource.org/) , предлагает простой способ публикации источников и PDB вместе с пакетом.</span><span class="sxs-lookup"><span data-stu-id="12b24-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="12b24-109">Это позволяет пользователям пакета выполнять шаг с заходом в исходный код для пакета в отладчике.</span><span class="sxs-lookup"><span data-stu-id="12b24-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="12b24-110">Дополнительные сведения см. в статье [Создание и Публикация пакета символов](../create-packages/symbol-packages.md) с помощью простого способа публикации пакетов NuGet с источниками.</span><span class="sxs-lookup"><span data-stu-id="12b24-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="12b24-111">Вы также можете просмотреть динамическую демонстрацию этой функции в составе NuGet, подробно обсудим по адресу Mix11.</span><span class="sxs-lookup"><span data-stu-id="12b24-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="12b24-112">Эта функция полностью демонстрируется, начиная с 20-минутной метки видео.</span><span class="sxs-lookup"><span data-stu-id="12b24-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="12b24-113">`Open-PackagePage` Command</span><span class="sxs-lookup"><span data-stu-id="12b24-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="12b24-114">Эта команда позволяет легко перейти на страницу проекта пакета из консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="12b24-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="12b24-115">Он также предоставляет параметры для открытия URL-адреса лицензии и страницы «сообщение о нарушении» для пакета.</span><span class="sxs-lookup"><span data-stu-id="12b24-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="12b24-116">Синтаксис команды:</span><span class="sxs-lookup"><span data-stu-id="12b24-116">The syntax for the command is:</span></span>

```
Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]
```

<span data-ttu-id="12b24-117">`-PassThru`Параметр используется для получения значения указанного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="12b24-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="12b24-118">Примеры:</span><span class="sxs-lookup"><span data-stu-id="12b24-118">Examples:</span></span>

```
PM> Open-PackagePage Ninject
```

<span data-ttu-id="12b24-119">Открывает браузер по URL-адресу проекта, указанному в пакете Нинжект.</span><span class="sxs-lookup"><span data-stu-id="12b24-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

```
PM> Open-PackagePage Ninject -License
```

<span data-ttu-id="12b24-120">Открывает браузер с URL-адресом лицензии, указанным в пакете Нинжект.</span><span class="sxs-lookup"><span data-stu-id="12b24-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

```
PM> Open-PackagePage Ninject -ReportAbuse
```

<span data-ttu-id="12b24-121">Открывает браузер по URL-адресу в текущем источнике пакета, который используется для сообщения о нарушении для указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="12b24-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

```
PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru
```

<span data-ttu-id="12b24-122">Присваивает переменной URL-адрес лицензии $url, не открывая URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="12b24-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="12b24-123">Повышение производительности</span><span class="sxs-lookup"><span data-stu-id="12b24-123">Performance Improvements</span></span>

<span data-ttu-id="12b24-124">NuGet 1,3 вносит значительные улучшения в производительность.</span><span class="sxs-lookup"><span data-stu-id="12b24-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="12b24-125">NuGet 1,3 не позволяет загружать одну и ту же версию пакета несколько раз, включая локальный кэш для каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="12b24-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="12b24-126">Доступ к кэшу можно получить и очистить с помощью диалогового окна "Параметры диспетчера пакетов":</span><span class="sxs-lookup"><span data-stu-id="12b24-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Диалоговое окно параметров NuGet с параметрами кэша пакетов](./media/nuget-options.png)

<span data-ttu-id="12b24-128">К другим улучшениям производительности относятся добавление поддержки сжатия HTTP и повышение скорости установки пакета в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="12b24-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="12b24-129">Visual Studio и nuget.exe используют один и тот же список источников пакетов</span><span class="sxs-lookup"><span data-stu-id="12b24-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="12b24-130">До NuGet 1,3 список источников пакетов, используемых nuget.exe и NuGet Visual Studio Add-In, не хранился в одном месте.</span><span class="sxs-lookup"><span data-stu-id="12b24-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="12b24-131">NuGet 1,3 теперь использует один и тот же список в обоих местах.</span><span class="sxs-lookup"><span data-stu-id="12b24-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="12b24-132">Список хранится в `NuGet.Config` папке AppData и сохраняется в ней.</span><span class="sxs-lookup"><span data-stu-id="12b24-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="12b24-133">nuget.exe пропускает файлы и папки, которые начинаются с "." по умолчанию</span><span class="sxs-lookup"><span data-stu-id="12b24-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="12b24-134">Чтобы NuGet хорошо работала с системами управления версиями, такими как Subversion и Mercurial, nuget.exe игнорирует папки и файлы, начинающиеся с символа "." при создании пакетов.</span><span class="sxs-lookup"><span data-stu-id="12b24-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="12b24-135">Это можно переопределить с помощью двух новых флагов:</span><span class="sxs-lookup"><span data-stu-id="12b24-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="12b24-136">__-Нодефаултексклудес__ используется для переопределения этого параметра и включения всех файлов.</span><span class="sxs-lookup"><span data-stu-id="12b24-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="12b24-137">__-Exclude__ используется для добавления других файлов или папок, исключаемых с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="12b24-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="12b24-138">Например, чтобы исключить все файлы с расширением BAK</span><span class="sxs-lookup"><span data-stu-id="12b24-138">For example, to exclude all files with the '.bak' file extension</span></span>

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="12b24-139">_Примечание. по умолчанию шаблон не является рекурсивным._</span><span class="sxs-lookup"><span data-stu-id="12b24-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="12b24-140">Поддержка проектов WiX и .NET Micro Framework</span><span class="sxs-lookup"><span data-stu-id="12b24-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="12b24-141">Благодаря вкладам сообщества NuGet обеспечивает поддержку типов проектов WiX, а также .NET Micro Framework.</span><span class="sxs-lookup"><span data-stu-id="12b24-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="12b24-142">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="12b24-142">Bug Fixes</span></span>

<span data-ttu-id="12b24-143">Полный список исправлений ошибок см. в [этой версии средства регистрации проблем NuGet](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="12b24-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="12b24-144">Исправлены ошибки, которые следует отметить</span><span class="sxs-lookup"><span data-stu-id="12b24-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="12b24-145">Пакеты с исходными файлами работают как на веб-сайтах, так и в проектах веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="12b24-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="12b24-146">Исходные файлы для веб-сайтов копируются в `App_Code` папку</span><span class="sxs-lookup"><span data-stu-id="12b24-146">For Websites, source files are copied into the `App_Code` folder</span></span>
