---
title: Заметки о выпуске версии 1.3 NuGet
description: Заметки о выпуске для NuGet 1.3, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551355"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="9359d-103">Заметки о выпуске версии 1.3 NuGet</span><span class="sxs-lookup"><span data-stu-id="9359d-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="9359d-104">[Заметки о выпуске NuGet 1.2](../release-notes/nuget-1.2.md) | [заметки о выпуске NuGet 1.4](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="9359d-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="9359d-105">25 апреля 2011 г. был выпущен NuGet 1.3.</span><span class="sxs-lookup"><span data-stu-id="9359d-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="9359d-106">Новые функции</span><span class="sxs-lookup"><span data-stu-id="9359d-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="9359d-107">Упрощенное создание пакета с помощью интеграции сервера символов</span><span class="sxs-lookup"><span data-stu-id="9359d-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="9359d-108">Команда NuGet привлечена ребята из [SymbolSource.org](http://www.symbolsource.org/) предложить очень простой способ публикации источников и PDB-файла, а также пакет.</span><span class="sxs-lookup"><span data-stu-id="9359d-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="9359d-109">Это позволяет клиентам выполнять шаги с заходом источник для пакета в отладчике пакета.</span><span class="sxs-lookup"><span data-stu-id="9359d-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="9359d-110">Дополнительные сведения см. в статье [Создание и публикация пакета символов](../create-packages/symbol-packages.md) простой способ публикации пакетов NuGet с источниками.</span><span class="sxs-lookup"><span data-stu-id="9359d-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="9359d-111">Вы также можете посмотреть проведена Демонстрация эту функцию как часть NuGet подробно поговорим в Mix11.</span><span class="sxs-lookup"><span data-stu-id="9359d-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="9359d-112">Эта функция является полностью показан с отметки времени знак 20-минутное видео.</span><span class="sxs-lookup"><span data-stu-id="9359d-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="9359d-113">`Open-PackagePage` Команда</span><span class="sxs-lookup"><span data-stu-id="9359d-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="9359d-114">Эта команда позволяет легко получить доступ к странице проекта для обновления в консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="9359d-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="9359d-115">Он также предоставляет параметры, чтобы открыть URL-адрес лицензии и страницы отчета о нарушении для пакета.</span><span class="sxs-lookup"><span data-stu-id="9359d-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="9359d-116">Используется следующий синтаксис команды:</span><span class="sxs-lookup"><span data-stu-id="9359d-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="9359d-117">`-PassThru` Параметр используется для возврата значения из указанного URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="9359d-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="9359d-118">Примеры</span><span class="sxs-lookup"><span data-stu-id="9359d-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="9359d-119">Открывает в браузере URL-адрес проекта, указанный в пакете Ninject.</span><span class="sxs-lookup"><span data-stu-id="9359d-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="9359d-120">Открывает в браузере URL-адрес лицензии, указанный в пакете Ninject.</span><span class="sxs-lookup"><span data-stu-id="9359d-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="9359d-121">Открывает в браузере URL-адрес в текущем источнике пакета, используемый для сообщения о нарушении для указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="9359d-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="9359d-122">Назначает URL-адрес лицензии переменной $url, не открывая URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="9359d-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="9359d-123">Улучшения производительности</span><span class="sxs-lookup"><span data-stu-id="9359d-123">Performance Improvements</span></span>

<span data-ttu-id="9359d-124">NuGet 1.3 вызывает массу повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="9359d-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="9359d-125">NuGet 1.3 позволяет избежать загрузки несколько раз ту же версию пакета, включая кэш локального пользователя.</span><span class="sxs-lookup"><span data-stu-id="9359d-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="9359d-126">Кэш может быть доступно и очищены с помощью диалогового окна Параметры диспетчера пакетов:</span><span class="sxs-lookup"><span data-stu-id="9359d-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Диалоговое окно параметров NuGet с параметрами кэша пакета](./media/nuget-options.png)

<span data-ttu-id="9359d-128">Другие улучшения производительности включают добавление поддержки HTTP-сжатие и повышение скорости установки пакета в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9359d-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="9359d-129">Visual Studio и nuget.exe использует тот же список источников пакетов</span><span class="sxs-lookup"><span data-stu-id="9359d-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="9359d-130">До 1.3 NuGet список источников пакетов, используемых nuget.exe и NuGet Visual Studio надстройки не были сохранены в одном месте.</span><span class="sxs-lookup"><span data-stu-id="9359d-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="9359d-131">NuGet 1.3 теперь использует тот же список в обоих местах.</span><span class="sxs-lookup"><span data-stu-id="9359d-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="9359d-132">Список хранится в `NuGet.Config` и сохраняется в папку AppData.</span><span class="sxs-lookup"><span data-stu-id="9359d-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="9359d-133">NuGet.exe не обрабатывает файлы и папки, начинающиеся с "." по умолчанию</span><span class="sxs-lookup"><span data-stu-id="9359d-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="9359d-134">Чтобы сделать NuGet работы с системами управления версиями, такие Subversion и Mercurial, nuget.exe игнорирует папки и файлы, которые начинаются с "." символов при создании пакетов.</span><span class="sxs-lookup"><span data-stu-id="9359d-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="9359d-135">Это может быть переопределено с помощью двух новые флаги:</span><span class="sxs-lookup"><span data-stu-id="9359d-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="9359d-136">__-NoDefaultExcludes__ позволяет переопределить этот параметр и включение всех файлов.</span><span class="sxs-lookup"><span data-stu-id="9359d-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="9359d-137">__-Исключение__ используется для добавления других файлов и папок, чтобы исключить с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="9359d-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="9359d-138">Например, чтобы исключить все файлы с расширением файла '.bak'</span><span class="sxs-lookup"><span data-stu-id="9359d-138">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="9359d-139">_Примечание: шаблон не является рекурсивным по умолчанию._</span><span class="sxs-lookup"><span data-stu-id="9359d-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="9359d-140">Поддержка проекты WiX и управлением .NET Micro Framework</span><span class="sxs-lookup"><span data-stu-id="9359d-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="9359d-141">Благодаря предложения участников сообщества NuGet включает в себя поддержку для типов проектов WiX, а также .NET Micro Framework.</span><span class="sxs-lookup"><span data-stu-id="9359d-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="9359d-142">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="9359d-142">Bug Fixes</span></span>

<span data-ttu-id="9359d-143">Полный список исправлений ошибок, просмотр [Issue Tracker NuGet для этого выпуска](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="9359d-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="9359d-144">Исправления ошибок, следует отметить</span><span class="sxs-lookup"><span data-stu-id="9359d-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="9359d-145">Пакеты с исходными файлами работать в обоих веб-сайтов и проектов веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="9359d-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="9359d-146">Для веб-сайтов, исходные файлы копируются в `App_Code` папки</span><span class="sxs-lookup"><span data-stu-id="9359d-146">For Websites, source files are copied into the `App_Code` folder</span></span>
