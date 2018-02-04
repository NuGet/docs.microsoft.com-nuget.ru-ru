---
title: "Заметки о выпуске NuGet 2.0 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске для NuGet 2.0, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 2.0 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: eaa3c8db1cce72ff93671a1df63698748cdfab70
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="600a8-104">Заметки о версии 2.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="600a8-104">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="600a8-105">[Заметки о выпуске NuGet 1.8](../release-notes/nuget-1.8.md) | [заметки о выпуске NuGet 2.1](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="600a8-105">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="600a8-106">NuGet 2.0 была выпущена 19 июня 2012 г.</span><span class="sxs-lookup"><span data-stu-id="600a8-106">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="600a8-107">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="600a8-107">Known Installation Issue</span></span>
<span data-ttu-id="600a8-108">Если вы используете VS 2010 с пакетом обновления 1, вы можете столкнуться ошибка установки при попытке обновить NuGet, если у вас установлена более ранняя версия.</span><span class="sxs-lookup"><span data-stu-id="600a8-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="600a8-109">Достаточно просто удалить NuGet, а затем установить его из библиотеки расширения VS.</span><span class="sxs-lookup"><span data-stu-id="600a8-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="600a8-110">В разделе [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) Дополнительные сведения или [перейдите непосредственно на исправление VS](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="600a8-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="600a8-111">Примечание: Если Visual Studio не позволяют удалить расширение (кнопка удаления отключена), скорее всего, необходимо перезапустить Visual Studio, используя «Запуск от имени администратора».</span><span class="sxs-lookup"><span data-stu-id="600a8-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="600a8-112">Сейчас активен согласия восстановления пакета</span><span class="sxs-lookup"><span data-stu-id="600a8-112">Package restore consent is now active</span></span>

<span data-ttu-id="600a8-113">Как описано в этом [разместить на согласия восстановления пакета](http://blog.nuget.org/20120518/package-restore-and-consent.html), теперь требуют NuGet 2.0 согласия присваивается включить восстановление пакета, чтобы подключиться к Интернету и загрузки пакетов.</span><span class="sxs-lookup"><span data-stu-id="600a8-113">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="600a8-114">Убедитесь, что вы предоставили согласие через диалоговое окно конфигурации диспетчера пакет или переменной среды EnableNuGetPackageRestore.</span><span class="sxs-lookup"><span data-stu-id="600a8-114">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="600a8-115">Группы зависимостей путем целевые платформы</span><span class="sxs-lookup"><span data-stu-id="600a8-115">Group dependencies by target frameworks</span></span>

<span data-ttu-id="600a8-116">Начиная с версии 2.0, пакет может отличаться в зависимости на основе профиле .NET framework целевого проекта.</span><span class="sxs-lookup"><span data-stu-id="600a8-116">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="600a8-117">Это достигается с помощью обновленной `.nuspec` схемы.</span><span class="sxs-lookup"><span data-stu-id="600a8-117">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="600a8-118">`<dependencies>` Элемент теперь может содержать набор `<group>` элементов.</span><span class="sxs-lookup"><span data-stu-id="600a8-118">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="600a8-119">Каждая группа содержит ноль или более `<dependency>` элементы и `targetFramework` атрибута.</span><span class="sxs-lookup"><span data-stu-id="600a8-119">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="600a8-120">Все зависимости внутри группы устанавливаются вместе, если требуемая версия .NET framework совместима с профиль целевой платформы проекта.</span><span class="sxs-lookup"><span data-stu-id="600a8-120">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="600a8-121">Пример:</span><span class="sxs-lookup"><span data-stu-id="600a8-121">For example:</span></span>

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

<span data-ttu-id="600a8-122">Обратите внимание, что группа может содержать **нуля** зависимости.</span><span class="sxs-lookup"><span data-stu-id="600a8-122">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="600a8-123">В приведенном выше примере Если пакет не установлен в проекте, ориентированном на Silverlight 3.0 или более поздней версии, зависимости не будут устанавливаться.</span><span class="sxs-lookup"><span data-stu-id="600a8-123">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="600a8-124">Если пакет установлен в проекте, ориентированном на .NET 4.0 или более поздней версии, двумя зависимостями, jQuery и WebActivator, будет установлен.</span><span class="sxs-lookup"><span data-stu-id="600a8-124">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="600a8-125">Если пакет установлен в проекте, ориентированном на ранней версией этих платформ 2 или любой другой платформе, будут устанавливаться RouteMagic 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="600a8-125">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="600a8-126">Нет без наследования между группами.</span><span class="sxs-lookup"><span data-stu-id="600a8-126">There is no inheritance between groups.</span></span> <span data-ttu-id="600a8-127">Если целевая платформа проекта соответствует `targetFramework` будет установлен атрибут группы, а только зависимости в пределах этой группы.</span><span class="sxs-lookup"><span data-stu-id="600a8-127">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="600a8-128">Пакет можно задать зависимости пакета в двух форматах: старый формат списка `<dependency>` элементов или групп.</span><span class="sxs-lookup"><span data-stu-id="600a8-128">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="600a8-129">Если `<group>` используется формат, пакет не установлен в версиях NuGet до версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="600a8-129">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="600a8-130">Обратите внимание, что нельзя совместно использовать два формата.</span><span class="sxs-lookup"><span data-stu-id="600a8-130">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="600a8-131">Например, следующий фрагмент кода является **недопустимый** и будут отклонены NuGet.</span><span class="sxs-lookup"><span data-stu-id="600a8-131">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="600a8-132">Группирование содержимого файлов и сценариев PowerShell, требуемая версия .NET framework</span><span class="sxs-lookup"><span data-stu-id="600a8-132">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="600a8-133">Помимо ссылки на сборки файлы содержимого и сценариев PowerShell можно также группировать по требуемой версии .NET framework.</span><span class="sxs-lookup"><span data-stu-id="600a8-133">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="600a8-134">Найти структуру папок в `lib` папку для указания целевой платформы теперь можно применять таким же образом, чтобы `content` и `tools` папки.</span><span class="sxs-lookup"><span data-stu-id="600a8-134">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="600a8-135">Пример:</span><span class="sxs-lookup"><span data-stu-id="600a8-135">For example:</span></span>

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

<span data-ttu-id="600a8-136">**Примечание**: поскольку `init.ps1` выполняется на уровне решения и является не зависят от любого отдельного проекта, он должен быть помещен непосредственно под `tools` папки.</span><span class="sxs-lookup"><span data-stu-id="600a8-136">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="600a8-137">Если поместить в папку отдельной платформы, он будет игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="600a8-137">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="600a8-138">Кроме того, новая функция в NuGet 2.0 — возможность, папки платформы *пустой*, в этом случае NuGet будет не добавлять ссылки на сборки, файлы содержимого или запускать скрипты PowerShell для версии конкретной платформы.</span><span class="sxs-lookup"><span data-stu-id="600a8-138">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="600a8-139">В примере выше папки `content\net40` пуст.</span><span class="sxs-lookup"><span data-stu-id="600a8-139">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="600a8-140">Улучшенная вкладку завершения производительности</span><span class="sxs-lookup"><span data-stu-id="600a8-140">Improved tab completion performance</span></span>
<span data-ttu-id="600a8-141">Функция завершения tab в консоли диспетчера пакетов NuGet теперь значительно повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="600a8-141">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="600a8-142">Будет гораздо меньше задержка между временем нажатии клавиши tab, пока не появится раскрывающийся список предложений.</span><span class="sxs-lookup"><span data-stu-id="600a8-142">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="600a8-143">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="600a8-143">Bug Fixes</span></span>
<span data-ttu-id="600a8-144">NuGet 2.0 включает множество исправлений ошибок с акцентом на пакет восстановления согласия и производительности.</span><span class="sxs-lookup"><span data-stu-id="600a8-144">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="600a8-145">Полный список рабочих элементов исправления в NuGet 2.0 представление [NuGet отслеживания проблем в этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="600a8-145">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
