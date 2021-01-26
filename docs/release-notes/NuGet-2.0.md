---
title: Заметки о выпуске NuGet 2,0
description: Заметки о выпуске NuGet 2,0, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6874cbf0404f18ab7007bec1e0f66089c790d08
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776988"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="aad6f-103">Заметки о выпуске NuGet 2,0</span><span class="sxs-lookup"><span data-stu-id="aad6f-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="aad6f-104">[Заметки о](../release-notes/nuget-1.8.md)  |  выпуске NuGet 1,8 [Заметки о выпуске NuGet 2,1](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="aad6f-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="aad6f-105">Версия NuGet 2,0 была выпущена 19 июня 2012 г.</span><span class="sxs-lookup"><span data-stu-id="aad6f-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="aad6f-106">Известная ошибка установки</span><span class="sxs-lookup"><span data-stu-id="aad6f-106">Known Installation Issue</span></span>
<span data-ttu-id="aad6f-107">Если вы используете VS 2010 с пакетом обновления 1 (SP1), при попытке обновить NuGet, если установлена более старая версия, может возникнуть ошибка установки.</span><span class="sxs-lookup"><span data-stu-id="aad6f-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="aad6f-108">Чтобы решить эту проблему, просто удалите NuGet, а затем установите его из коллекции расширений VS.</span><span class="sxs-lookup"><span data-stu-id="aad6f-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="aad6f-109"><https://support.microsoft.com/kb/2581019>Дополнительные сведения см. в разделе для получения дополнительных сведений или [непосредственно к исправлению VS](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="aad6f-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="aad6f-110">Примечание. Если Visual Studio не позволит удалить расширение (кнопка удаления отключена), скорее всего, потребуется перезапустить Visual Studio с помощью команды "Запуск от имени администратора".</span><span class="sxs-lookup"><span data-stu-id="aad6f-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="aad6f-111">Согласие на восстановление пакета теперь активно</span><span class="sxs-lookup"><span data-stu-id="aad6f-111">Package restore consent is now active</span></span>

<span data-ttu-id="aad6f-112">Как описано в этой [записи при получении согласия на восстановление пакета](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2,0 будет требовать предоставления этого согласия, чтобы включить восстановление пакетов для подключения к сети и загрузки пакетов.</span><span class="sxs-lookup"><span data-stu-id="aad6f-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="aad6f-113">Убедитесь, что вы указали согласие с помощью диалогового окна настройки диспетчера пакетов или переменной среды Енабленужетпаккажересторе.</span><span class="sxs-lookup"><span data-stu-id="aad6f-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="aad6f-114">Группирование зависимостей по целевым платформам</span><span class="sxs-lookup"><span data-stu-id="aad6f-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="aad6f-115">Начиная с версии 2,0 зависимости пакета могут различаться в зависимости от профиля платформы целевого проекта.</span><span class="sxs-lookup"><span data-stu-id="aad6f-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="aad6f-116">Это достигается с помощью обновленной `.nuspec` схемы.</span><span class="sxs-lookup"><span data-stu-id="aad6f-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="aad6f-117">`<dependencies>`Теперь элемент может содержать набор `<group>` элементов.</span><span class="sxs-lookup"><span data-stu-id="aad6f-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="aad6f-118">Каждая группа содержит ноль или более `<dependency>` элементов и `targetFramework` атрибут.</span><span class="sxs-lookup"><span data-stu-id="aad6f-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="aad6f-119">Все зависимости внутри группы устанавливаются вместе, если Целевая платформа совместима с целевым профилем конечной платформы проекта.</span><span class="sxs-lookup"><span data-stu-id="aad6f-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="aad6f-120">Пример:</span><span class="sxs-lookup"><span data-stu-id="aad6f-120">For example:</span></span>

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

<span data-ttu-id="aad6f-121">Обратите внимание, что группа может содержать **нулевые** зависимости.</span><span class="sxs-lookup"><span data-stu-id="aad6f-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="aad6f-122">В приведенном выше примере, если пакет установлен в проекте, ориентированном на Silverlight 3,0 или более поздней версии, зависимости не будут установлены.</span><span class="sxs-lookup"><span data-stu-id="aad6f-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="aad6f-123">Если пакет устанавливается в проект, предназначенный для .NET 4,0 или более поздней версии, будут установлены две зависимости, jQuery и активатор.</span><span class="sxs-lookup"><span data-stu-id="aad6f-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="aad6f-124">Если пакет устанавливается в проект, предназначенный для ранних версий этих двух платформ или для любой другой платформы, будет установлена Раутемагик 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="aad6f-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="aad6f-125">Между группами нет наследования.</span><span class="sxs-lookup"><span data-stu-id="aad6f-125">There is no inheritance between groups.</span></span> <span data-ttu-id="aad6f-126">Если целевая платформа проекта соответствует `targetFramework` атрибуту группы, будут установлены только зависимости внутри этой группы.</span><span class="sxs-lookup"><span data-stu-id="aad6f-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="aad6f-127">Пакет может задавать зависимости пакета в одном из двух форматов: старом формате неструктурированного списка `<dependency>` элементов или групп.</span><span class="sxs-lookup"><span data-stu-id="aad6f-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="aad6f-128">Если `<group>` используется формат, пакет не может быть установлен в версии NuGet более ранней, чем 2,0.</span><span class="sxs-lookup"><span data-stu-id="aad6f-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="aad6f-129">Обратите внимание, что смешивание двух форматов не допускается.</span><span class="sxs-lookup"><span data-stu-id="aad6f-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="aad6f-130">Например, следующий фрагмент кода является **недопустимым** и будет отклонен NuGet.</span><span class="sxs-lookup"><span data-stu-id="aad6f-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="aad6f-131">Группирование файлов содержимого и скриптов PowerShell по целевым платформам</span><span class="sxs-lookup"><span data-stu-id="aad6f-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="aad6f-132">Помимо ссылок на сборки, файлы содержимого и скрипты PowerShell также могут быть сгруппированы по целевой платформе.</span><span class="sxs-lookup"><span data-stu-id="aad6f-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="aad6f-133">Та же структура папок, которая находится в `lib` папке для указания целевой платформы, теперь может быть применена таким же образом, как `content` и `tools` папки и.</span><span class="sxs-lookup"><span data-stu-id="aad6f-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="aad6f-134">Пример:</span><span class="sxs-lookup"><span data-stu-id="aad6f-134">For example:</span></span>

```
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
```

<span data-ttu-id="aad6f-135">**Примечание**. Поскольку выполняется `init.ps1` на уровне решения и не зависит от отдельного проекта, его необходимо поместить непосредственно в `tools` папку.</span><span class="sxs-lookup"><span data-stu-id="aad6f-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="aad6f-136">При помещении в папку, зависящую от платформы, она будет проигнорирована.</span><span class="sxs-lookup"><span data-stu-id="aad6f-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="aad6f-137">Кроме того, Новая функция в NuGet 2,0 заключается в том, что папка Framework может быть *пустой*. в этом случае NuGet не будет добавлять ссылки на сборки, добавлять файлы содержимого или запускать скрипты PowerShell для конкретной версии платформы.</span><span class="sxs-lookup"><span data-stu-id="aad6f-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="aad6f-138">В приведенном выше примере папка `content\net40` пуста.</span><span class="sxs-lookup"><span data-stu-id="aad6f-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="aad6f-139">Улучшенная производительность заполнения нажатием клавиши TAB</span><span class="sxs-lookup"><span data-stu-id="aad6f-139">Improved tab completion performance</span></span>
<span data-ttu-id="aad6f-140">Функция заполнения нажатием клавиши TAB в консоли диспетчера пакетов NuGet была обновлена для значительного повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="aad6f-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="aad6f-141">При нажатии клавиши Tab будет значительно меньше задержки, пока не появится раскрывающийся список предложений.</span><span class="sxs-lookup"><span data-stu-id="aad6f-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="aad6f-142">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="aad6f-142">Bug Fixes</span></span>
<span data-ttu-id="aad6f-143">NuGet 2,0 включает множество исправлений ошибок с учетом согласия и производительности восстановления пакета.</span><span class="sxs-lookup"><span data-stu-id="aad6f-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="aad6f-144">Полный список рабочих элементов, исправленных в NuGet 2,0, см. в [этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="aad6f-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
