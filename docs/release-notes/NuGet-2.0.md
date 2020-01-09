---
title: Заметки о выпуске NuGet 2,0
description: Заметки о выпуске NuGet 2,0, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 01fdbfafcaea009cf119dfa880b2b16539c9b088
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383071"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="ffe1a-103">Заметки о выпуске NuGet 2,0</span><span class="sxs-lookup"><span data-stu-id="ffe1a-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="ffe1a-104">[Заметки о выпуске nuget 1,8](../release-notes/nuget-1.8.md) | [заметок о выпуске NuGet 2,1](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="ffe1a-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="ffe1a-105">Версия NuGet 2,0 была выпущена 19 июня 2012 г.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="ffe1a-106">Известная ошибка установки</span><span class="sxs-lookup"><span data-stu-id="ffe1a-106">Known Installation Issue</span></span>
<span data-ttu-id="ffe1a-107">Если вы используете VS 2010 с пакетом обновления 1 (SP1), при попытке обновить NuGet, если установлена более старая версия, может возникнуть ошибка установки.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="ffe1a-108">Чтобы решить эту проблему, просто удалите NuGet, а затем установите его из коллекции расширений VS.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="ffe1a-109">Дополнительные сведения см. в разделе <https://support.microsoft.com/kb/2581019> или [непосредственно в исправление VS](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="ffe1a-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="ffe1a-110">Примечание. Если Visual Studio не позволит удалить расширение (кнопка удаления отключена), скорее всего, потребуется перезапустить Visual Studio с помощью команды "Запуск от имени администратора".</span><span class="sxs-lookup"><span data-stu-id="ffe1a-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="ffe1a-111">Согласие на восстановление пакета теперь активно</span><span class="sxs-lookup"><span data-stu-id="ffe1a-111">Package restore consent is now active</span></span>

<span data-ttu-id="ffe1a-112">Как описано в этой [записи при получении согласия на восстановление пакета](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2,0 будет требовать предоставления этого согласия, чтобы включить восстановление пакетов для подключения к сети и загрузки пакетов.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="ffe1a-113">Убедитесь, что вы указали согласие с помощью диалогового окна настройки диспетчера пакетов или переменной среды Енабленужетпаккажересторе.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="ffe1a-114">Группирование зависимостей по целевым платформам</span><span class="sxs-lookup"><span data-stu-id="ffe1a-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="ffe1a-115">Начиная с версии 2,0 зависимости пакета могут различаться в зависимости от профиля платформы целевого проекта.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="ffe1a-116">Это достигается с помощью обновленной схемы `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="ffe1a-117">Элемент `<dependencies>` теперь может содержать набор элементов `<group>`.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="ffe1a-118">Каждая группа содержит ноль или более `<dependency>` элементов и атрибут `targetFramework`.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="ffe1a-119">Все зависимости внутри группы устанавливаются вместе, если Целевая платформа совместима с целевым профилем конечной платформы проекта.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="ffe1a-120">Например:</span><span class="sxs-lookup"><span data-stu-id="ffe1a-120">For example:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<span data-ttu-id="ffe1a-121">Обратите внимание, что группа может содержать **нулевые** зависимости.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="ffe1a-122">В приведенном выше примере, если пакет установлен в проекте, ориентированном на Silverlight 3,0 или более поздней версии, зависимости не будут установлены.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="ffe1a-123">Если пакет устанавливается в проект, предназначенный для .NET 4,0 или более поздней версии, будут установлены две зависимости, jQuery и активатор.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="ffe1a-124">Если пакет устанавливается в проект, предназначенный для ранних версий этих двух платформ или для любой другой платформы, будет установлена Раутемагик 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="ffe1a-125">Между группами нет наследования.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-125">There is no inheritance between groups.</span></span> <span data-ttu-id="ffe1a-126">Если целевая платформа проекта соответствует атрибуту `targetFramework` группы, будут установлены только зависимости внутри этой группы.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="ffe1a-127">Пакет может задавать зависимости пакетов в одном из двух форматов: старый формат неструктурированного списка `<dependency>` элементов или групп.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="ffe1a-128">Если используется формат `<group>`, пакет нельзя установить в версии NuGet более ранней, чем 2,0.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="ffe1a-129">Обратите внимание, что смешивание двух форматов не допускается.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="ffe1a-130">Например, следующий фрагмент кода является **недопустимым** и будет отклонен NuGet.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="ffe1a-131">Группирование файлов содержимого и скриптов PowerShell по целевым платформам</span><span class="sxs-lookup"><span data-stu-id="ffe1a-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="ffe1a-132">Помимо ссылок на сборки, файлы содержимого и скрипты PowerShell также могут быть сгруппированы по целевой платформе.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="ffe1a-133">Та же структура папок, которая находится в папке `lib` для указания целевой платформы, теперь может быть применена таким же образом, как и к папкам `content` и `tools`.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="ffe1a-134">Например:</span><span class="sxs-lookup"><span data-stu-id="ffe1a-134">For example:</span></span>

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

<span data-ttu-id="ffe1a-135">**Примечание**. Поскольку `init.ps1` выполняется на уровне решения и не зависит от отдельного проекта, его необходимо поместить непосредственно в папку `tools`.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="ffe1a-136">При помещении в папку, зависящую от платформы, она будет проигнорирована.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="ffe1a-137">Кроме того, Новая функция в NuGet 2,0 заключается в том, что папка Framework может быть *пустой*. в этом случае NuGet не будет добавлять ссылки на сборки, добавлять файлы содержимого или запускать скрипты PowerShell для конкретной версии платформы.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="ffe1a-138">В приведенном выше примере папка `content\net40` пуста.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="ffe1a-139">Улучшенная производительность заполнения нажатием клавиши TAB</span><span class="sxs-lookup"><span data-stu-id="ffe1a-139">Improved tab completion performance</span></span>
<span data-ttu-id="ffe1a-140">Функция заполнения нажатием клавиши TAB в консоли диспетчера пакетов NuGet была обновлена для значительного повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="ffe1a-141">При нажатии клавиши Tab будет значительно меньше задержки, пока не появится раскрывающийся список предложений.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="ffe1a-142">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="ffe1a-142">Bug Fixes</span></span>
<span data-ttu-id="ffe1a-143">NuGet 2,0 включает множество исправлений ошибок с учетом согласия и производительности восстановления пакета.</span><span class="sxs-lookup"><span data-stu-id="ffe1a-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="ffe1a-144">Полный список рабочих элементов, исправленных в NuGet 2,0, см. в [этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="ffe1a-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
