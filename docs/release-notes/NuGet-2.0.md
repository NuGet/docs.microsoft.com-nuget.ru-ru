---
title: Заметки о выпуске 2.0 NuGet
description: Заметки о выпуске для NuGet 2.0, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547579"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="3647f-103">Заметки о выпуске 2.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="3647f-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="3647f-104">[Заметки о выпуске NuGet 1.8](../release-notes/nuget-1.8.md) | [заметки о выпуске NuGet 2.1](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="3647f-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="3647f-105">NuGet 2.0 было выпущено 19 июня 2012 г.</span><span class="sxs-lookup"><span data-stu-id="3647f-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="3647f-106">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="3647f-106">Known Installation Issue</span></span>
<span data-ttu-id="3647f-107">Если вы используете VS 2010 SP1, вы можете столкнуться ошибка установки при попытке обновить NuGet, если у вас установлена более ранняя версия.</span><span class="sxs-lookup"><span data-stu-id="3647f-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="3647f-108">Обойти это просто удалить диспетчер NuGet, а затем установить его из коллекции расширений VS.</span><span class="sxs-lookup"><span data-stu-id="3647f-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="3647f-109">См. в разделе [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Дополнительные сведения или [перейдите непосредственно на исправление VS](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="3647f-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="3647f-110">Примечание: Если Visual Studio не позволяют удалить расширение (кнопка "Удалить" отключена), скорее всего, потребуется перезапустить Visual Studio, используя «Запуск от имени администратора».</span><span class="sxs-lookup"><span data-stu-id="3647f-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="3647f-111">Теперь активен согласия восстановления пакета</span><span class="sxs-lookup"><span data-stu-id="3647f-111">Package restore consent is now active</span></span>

<span data-ttu-id="3647f-112">Как описано в этой [блоге согласия восстановления пакета](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 теперь будет требоваться, что согласие предоставить включите восстановление пакетов, чтобы подключиться к Интернету и скачать пакеты.</span><span class="sxs-lookup"><span data-stu-id="3647f-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="3647f-113">Убедитесь, что вы предоставили согласие через диалоговое окно настройки диспетчера пакетов или переменной среды EnableNuGetPackageRestore.</span><span class="sxs-lookup"><span data-stu-id="3647f-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="3647f-114">Зависимости группы по целевых платформ</span><span class="sxs-lookup"><span data-stu-id="3647f-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="3647f-115">Начиная с версии 2.0, пакет может варьироваться в зависимости на основе профилем платформы целевого проекта.</span><span class="sxs-lookup"><span data-stu-id="3647f-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="3647f-116">Это достигается с помощью обновленный `.nuspec` схемы.</span><span class="sxs-lookup"><span data-stu-id="3647f-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="3647f-117">`<dependencies>` Элемент теперь может содержать набор `<group>` элементов.</span><span class="sxs-lookup"><span data-stu-id="3647f-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="3647f-118">Каждая группа содержит ноль или более `<dependency>` элементов и `targetFramework` атрибута.</span><span class="sxs-lookup"><span data-stu-id="3647f-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="3647f-119">Все зависимости внутри группы устанавливаются вместе, если целевая платформа совместима с профиль целевой платформы проекта.</span><span class="sxs-lookup"><span data-stu-id="3647f-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="3647f-120">Пример:</span><span class="sxs-lookup"><span data-stu-id="3647f-120">For example:</span></span>

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

<span data-ttu-id="3647f-121">Обратите внимание, что каждая группа может содержать **ноль** зависимости.</span><span class="sxs-lookup"><span data-stu-id="3647f-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="3647f-122">В приведенном выше примере Если пакет установлен в проекте, ориентированном на Silverlight 3.0 или более поздней версии, зависимости не будут устанавливаться.</span><span class="sxs-lookup"><span data-stu-id="3647f-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="3647f-123">Если пакет будет установлен в проекте, ориентированном на .NET 4.0 или более поздней версии, две зависимости, jQuery и WebActivator, будут устанавливаться.</span><span class="sxs-lookup"><span data-stu-id="3647f-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="3647f-124">Если пакет устанавливается в проекте, ориентированном на версию системы эти 2 платформы, или любой другой платформы, будет устанавливаться RouteMagic 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="3647f-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="3647f-125">Нет не поддерживают наследование между группами.</span><span class="sxs-lookup"><span data-stu-id="3647f-125">There is no inheritance between groups.</span></span> <span data-ttu-id="3647f-126">Если целевая платформа проекта соответствует `targetFramework` устанавливается атрибут группы, а только зависимости в пределах этой группы.</span><span class="sxs-lookup"><span data-stu-id="3647f-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="3647f-127">Пакет можно указать зависимости пакетов в двух форматах: старый формат списка `<dependency>` элементов или групп.</span><span class="sxs-lookup"><span data-stu-id="3647f-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="3647f-128">Если `<group>` используется формат, не удается установить пакет, в версиях NuGet до 2.0.</span><span class="sxs-lookup"><span data-stu-id="3647f-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="3647f-129">Обратите внимание на то, что нельзя совместно использовать два формата.</span><span class="sxs-lookup"><span data-stu-id="3647f-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="3647f-130">Например, следующий фрагмент является **недопустимый** и будут отклонены NuGet.</span><span class="sxs-lookup"><span data-stu-id="3647f-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="3647f-131">Группирование содержимого файлов и сценариев PowerShell с требуемой версии .NET framework</span><span class="sxs-lookup"><span data-stu-id="3647f-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="3647f-132">Помимо ссылки на сборки файлы содержимого и скрипты PowerShell можно также группировать по целевой платформе.</span><span class="sxs-lookup"><span data-stu-id="3647f-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="3647f-133">Найти ту же структуру папок в `lib` папку для указания целевой платформы, теперь может применяться таким же образом, чтобы `content` и `tools` папки.</span><span class="sxs-lookup"><span data-stu-id="3647f-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="3647f-134">Пример:</span><span class="sxs-lookup"><span data-stu-id="3647f-134">For example:</span></span>

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

<span data-ttu-id="3647f-135">**Примечание**: поскольку `init.ps1` выполняется на уровне решения и находится не зависит от любого отдельного проекта, его необходимо поместить непосредственно под `tools` папки.</span><span class="sxs-lookup"><span data-stu-id="3647f-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="3647f-136">Если поместить в папку с платформой, он игнорируется.</span><span class="sxs-lookup"><span data-stu-id="3647f-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="3647f-137">Кроме того, новая функция в NuGet 2.0 — что может быть папка платформы *пустой*, в этом случае NuGet не добавлять ссылки на сборки, добавить файлы содержимого или запускать скрипты PowerShell для версии конкретной платформы.</span><span class="sxs-lookup"><span data-stu-id="3647f-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="3647f-138">В примере выше папке `content\net40` пуст.</span><span class="sxs-lookup"><span data-stu-id="3647f-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="3647f-139">Улучшенная вкладки завершения производительности</span><span class="sxs-lookup"><span data-stu-id="3647f-139">Improved tab completion performance</span></span>
<span data-ttu-id="3647f-140">Функция завершения вкладку в консоли диспетчера пакетов NuGet обновлен позволит значительно повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="3647f-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="3647f-141">Будет гораздо меньше задержка с момента нажатии клавиши tab, пока не появится раскрывающийся список предложений.</span><span class="sxs-lookup"><span data-stu-id="3647f-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="3647f-142">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="3647f-142">Bug Fixes</span></span>
<span data-ttu-id="3647f-143">NuGet 2.0 включает много исправлений ошибок, с акцентом на согласие восстановления пакета и производительности.</span><span class="sxs-lookup"><span data-stu-id="3647f-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="3647f-144">Полный список рабочих элементов исправленные в NuGet 2.0 обратитесь представление [Issue Tracker NuGet для этого выпуска](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="3647f-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
