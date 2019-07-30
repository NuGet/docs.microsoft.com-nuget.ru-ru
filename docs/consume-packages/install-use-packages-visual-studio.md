---
title: Установка пакетов NuGet и управление ими в Visual Studio
description: Инструкции по применению пользовательского интерфейса диспетчера пакетов NuGet в Visual Studio для работы с пакетами NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 7e4ea59b9954e787e7ab060adc964f3097a8240b
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419973"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a><span data-ttu-id="90192-103">Устанавливайте пакеты и управляйте ими непосредственно в Visual Studio с помощью диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="90192-103">Install and manage packages in Visual Studio using the NuGet Package Manager</span></span>

<span data-ttu-id="90192-104">С помощью пользовательского интерфейса диспетчера пакетов NuGet в Visual Studio вы можете легко устанавливать, удалять и обновлять пакеты NuGet в проектах и решениях в ОС Windows.</span><span class="sxs-lookup"><span data-stu-id="90192-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="90192-105">Если вы используете Visual Studio для Mac, см. руководство по [включению пакета NuGet в проект](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span><span class="sxs-lookup"><span data-stu-id="90192-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span></span> <span data-ttu-id="90192-106">Пользовательский интерфейс диспетчера пакетов не входит в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="90192-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="90192-107">Если у вас нет диспетчера пакетов NuGet в Visual Studio 2015, щелкните **Средства > Расширения и обновления** и найдите расширение *Диспетчер пакетов NuGet*.</span><span class="sxs-lookup"><span data-stu-id="90192-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="90192-108">Если вы не можете использовать установщик расширений в Visual Studio, скачайте расширение отсюда: [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="90192-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="90192-109">Начиная с Visual Studio 2017, NuGet и диспетчер пакетов NuGet автоматически устанавливаются с любыми рабочими нагрузками, связанными с .NET.</span><span class="sxs-lookup"><span data-stu-id="90192-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="90192-110">Установите его отдельно, щелкнув **Отдельные компоненты > Средства для работы с кодом > Диспетчер пакетов NuGet** в установщике Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="90192-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="90192-111">Поиск и установка пакета</span><span class="sxs-lookup"><span data-stu-id="90192-111">Find and install a package</span></span>

1. <span data-ttu-id="90192-112">В **обозревателе решений** щелкните правой кнопкой мыши **Ссылки** или сам проект и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="90192-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Пункт меню "Управление пакетами NuGet"](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="90192-114">На вкладке **Обзор** по популярности отображаются пакеты из выбранного в данный момент источника (см. подробнее об [источниках пакетов](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="90192-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="90192-115">Выполните поиск определенного пакета с помощью поля поиска в левом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="90192-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="90192-116">Выберите пакет в списке, чтобы отобразить сведения о нем. Это также активирует кнопку **Установить** и раскрывающийся список для выбора версии.</span><span class="sxs-lookup"><span data-stu-id="90192-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Вкладка "Обзор" в диалоговом окне "Управление пакетами NuGet"](media/Search.png)

1. <span data-ttu-id="90192-118">Выберите нужную версию в раскрывающемся списке и щелкните **Установить**.</span><span class="sxs-lookup"><span data-stu-id="90192-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="90192-119">Visual Studio установит пакет и его зависимости в проект.</span><span class="sxs-lookup"><span data-stu-id="90192-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="90192-120">Может появиться запрос на принятие условий лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="90192-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="90192-121">После завершения установки добавленные пакеты отобразятся на вкладке **Установленные**. Пакеты также перечислены в узле **Ссылки** обозревателя решений. Это значит, что их можно указывать в проекте с помощью инструкций `using`.</span><span class="sxs-lookup"><span data-stu-id="90192-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Ссылки в обозревателе решений](media/References.png)

> [!Tip]
> <span data-ttu-id="90192-123">Чтобы включить предварительные версии в поиск и сделать их доступными в раскрывающемся списке версий, щелкните **Включить предварительные версии**.</span><span class="sxs-lookup"><span data-stu-id="90192-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="90192-124">Удаление пакета</span><span class="sxs-lookup"><span data-stu-id="90192-124">Uninstall a package</span></span>

1. <span data-ttu-id="90192-125">В **обозревателе решений** щелкните правой кнопкой мыши **Ссылки** или сам проект и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="90192-125">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="90192-126">Откройте вкладку **Установленные**.</span><span class="sxs-lookup"><span data-stu-id="90192-126">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="90192-127">Выберите пакет для удаления (при необходимости используйте поиск, чтобы отфильтровать список) и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="90192-127">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Удаление пакета](media/UninstallPackage.png)

1. <span data-ttu-id="90192-129">Обратите внимание, что элементы управления **Включить предварительные версии** и **Источник пакета** не применяются при удалении пакетов.</span><span class="sxs-lookup"><span data-stu-id="90192-129">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="90192-130">Обновление пакета</span><span class="sxs-lookup"><span data-stu-id="90192-130">Update a package</span></span>

1. <span data-ttu-id="90192-131">В **обозревателе решений** щелкните правой кнопкой мыши **Ссылки** или сам проект и выберите **Управление пакетами NuGet**. (В проектах веб-сайтов щелкните правой кнопкой мыши папку **Bin**.)</span><span class="sxs-lookup"><span data-stu-id="90192-131">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="90192-132">Перейдите на вкладку **Обновления**, чтобы просмотреть пакеты, для которых доступны обновления из выбранных источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="90192-132">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="90192-133">Выберите **Включить предварительные версии**, чтобы включить предварительные версии пакетов в список обновлений.</span><span class="sxs-lookup"><span data-stu-id="90192-133">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="90192-134">Последовательно выберите пакет для обновления и нужную версию в раскрывающемся списке справа, а затем щелкните **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="90192-134">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Обновление пакета](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="90192-136">Для некоторых пакетов отключена кнопка **Обновить**. При этом появляется сообщение "На этот пакет неявно ссылается пакет SDK" (AutoReferenced).</span><span class="sxs-lookup"><span data-stu-id="90192-136">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="90192-137">Это сообщение означает, что пакет является частью более крупной платформы или пакета SDK и не должен обновляться отдельно.</span><span class="sxs-lookup"><span data-stu-id="90192-137">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="90192-138">(Такие пакеты отмечаются атрибутом `<IsImplicitlyDefined>True</IsImplicitlyDefined>`). Например, `Microsoft.NETCore.App` является частью пакета SDK для .NET Core, и версия пакета не совпадает с версией платформы среды выполнения, используемой приложением.</span><span class="sxs-lookup"><span data-stu-id="90192-138">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="90192-139">Необходимо [обновить установку .NET Core](https://aka.ms/dotnet-download), чтобы получить новые версии ASP.NET Core и среды выполнения .NET Core.</span><span class="sxs-lookup"><span data-stu-id="90192-139">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="90192-140">См. подробнее о [метапакетах и управлении версиями .NET Core](/dotnet/core/packages).</span><span class="sxs-lookup"><span data-stu-id="90192-140">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="90192-141">Это относится к следующим часто используемым пакетам:</span><span class="sxs-lookup"><span data-stu-id="90192-141">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="90192-142">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="90192-142">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="90192-143">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="90192-143">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="90192-144">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="90192-144">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="90192-145">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="90192-145">NETStandard.Library</span></span>

    ![Пример пакета, отмеченного как неявная ссылка или AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="90192-147">Чтобы обновить несколько пакетов до последних версий, выберите их в списке и нажмите кнопку **Обновить**, расположенную над списком.</span><span class="sxs-lookup"><span data-stu-id="90192-147">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="90192-148">Кроме того, можно обновить отдельный пакет на вкладке **Установленные**. В этом случае сведения о пакете будут содержать средство выбора версии (зависит от параметра **Включить предварительные версии**) и кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="90192-148">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="manage-packages-for-the-solution"></a><span data-ttu-id="90192-149">Управление пакетами для решения</span><span class="sxs-lookup"><span data-stu-id="90192-149">Manage packages for the solution</span></span>

<span data-ttu-id="90192-150">Управление пакетами для решения — это удобный способ одновременно работать с несколькими проектами.</span><span class="sxs-lookup"><span data-stu-id="90192-150">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="90192-151">Выберите команду меню **Средства > Диспетчер пакетов NuGet > Управление пакетами NuGet для решения** или щелкните правой кнопкой мыши решение и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="90192-151">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Управление пакетами NuGet для решения](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="90192-153">При управлении пакетами для решения пользовательский интерфейс позволяет выбрать проекты, затрагиваемые операциями.</span><span class="sxs-lookup"><span data-stu-id="90192-153">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Выбор проекта при управлении пакетами для решения](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="90192-155">Вкладка "Консолидация"</span><span class="sxs-lookup"><span data-stu-id="90192-155">Consolidate tab</span></span>

<span data-ttu-id="90192-156">Разработчики обычно предпочитают не использовать разные версии одного и того же пакета NuGet в разных проектах в одном решении.</span><span class="sxs-lookup"><span data-stu-id="90192-156">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="90192-157">Когда вы выбираете управление пакетами для решения, в пользовательском интерфейсе диспетчера пакетов появляется вкладка **Консолидация**, на которой вы можете отслеживать использование пакетов с разными номерами версий разными проектами в решении.</span><span class="sxs-lookup"><span data-stu-id="90192-157">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Вкладка "Консолидация" пользовательского интерфейса диспетчера пакетов](media/ConsolidateTab.png)

<span data-ttu-id="90192-159">В этом примере проект ClassLibrary1 использует EntityFramework 6.2.0, а ConsoleApp1 использует EntityFramework 6.1.0.</span><span class="sxs-lookup"><span data-stu-id="90192-159">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="90192-160">Для консолидации версий пакета сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="90192-160">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="90192-161">Выберите проекты для обновления в списке проектов.</span><span class="sxs-lookup"><span data-stu-id="90192-161">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="90192-162">Выберите версию, которая будет использоваться во всех проектах в элементе управления **Версия**, например EntityFramework 6.2.0.</span><span class="sxs-lookup"><span data-stu-id="90192-162">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="90192-163">Нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="90192-163">Select the **Install** button.</span></span>

<span data-ttu-id="90192-164">Диспетчер пакетов устанавливает выбранную версию пакета во все выбранные проекты. После этого пакет больше не будет отображаться на вкладке **Консолидация**.</span><span class="sxs-lookup"><span data-stu-id="90192-164">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="90192-165">Источники пакетов</span><span class="sxs-lookup"><span data-stu-id="90192-165">Package sources</span></span>

<span data-ttu-id="90192-166">Чтобы изменить источник, из которого Visual Studio получает пакеты, выберите его в средстве выбора источника.</span><span class="sxs-lookup"><span data-stu-id="90192-166">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Средство выбора источника пакетов в пользовательском интерфейсе диспетчера пакетов](media/PackageSourceDropDown.png)

<span data-ttu-id="90192-168">Для управления источниками пакетов сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="90192-168">To manage package sources:</span></span>

1. <span data-ttu-id="90192-169">Щелкните значок **Параметры** в пользовательском интерфейсе диспетчера пакетов, как показано ниже, или выберите **Средства > Параметры** и прокрутите до пункта **Диспетчер пакетов NuGet**.</span><span class="sxs-lookup"><span data-stu-id="90192-169">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Значок параметров пользовательского интерфейса диспетчера пакетов](media/PackageSourceSettings.png)

1. <span data-ttu-id="90192-171">Выберите узел **Источники пакетов**.</span><span class="sxs-lookup"><span data-stu-id="90192-171">Select the **Package Sources** node:</span></span>

    ![Параметры источников пакетов](media/options.png)

1. <span data-ttu-id="90192-173">Чтобы добавить источник, выберите **+**, измените имя, введите URL-адрес или путь в элементе управления **Источник** и щелкните **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="90192-173">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="90192-174">Источник отобразится в раскрывающемся списке для выбора.</span><span class="sxs-lookup"><span data-stu-id="90192-174">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="90192-175">Чтобы изменить источник пакета, выберите его, внесите изменения в поля **Имя** и **Источник** и щелкните **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="90192-175">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="90192-176">Чтобы отключить источник пакета, снимите флажок слева от имени в списке.</span><span class="sxs-lookup"><span data-stu-id="90192-176">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="90192-177">Чтобы удалить источник пакета, выберите его и нажмите кнопку **X**.</span><span class="sxs-lookup"><span data-stu-id="90192-177">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="90192-178">Использование кнопок со стрелками вверх и вниз не меняет приоритетный порядок источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="90192-178">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="90192-179">Visual Studio игнорирует порядок источников пакетов, используя пакет из любого источника, первым ответившего на запросы.</span><span class="sxs-lookup"><span data-stu-id="90192-179">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="90192-180">См. подробнее о [восстановлении пакетов](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="90192-180">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="90192-181">Если источник пакета появляется после удаления, он может быть указан в файлах `NuGet.Config` уровня компьютера или уровня пользователя.</span><span class="sxs-lookup"><span data-stu-id="90192-181">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="90192-182">Чтобы определить расположение этих файлов, см. описание [распространенных конфигураций NuGet](../consume-packages/configuring-nuget-behavior.md). Затем удалите источник, отредактировав файлы вручную или с помощью команды [nuget sources](../reference/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="90192-182">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../reference/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="90192-183">Элемент управления "Параметры" диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="90192-183">Package manager Options control</span></span>

<span data-ttu-id="90192-184">Если пакет выбран, пользовательский интерфейс диспетчера пакетов отображает небольшой развертываемый элемент управления **Параметры** под средством выбора версий (показан в свернутом и развернутом виде).</span><span class="sxs-lookup"><span data-stu-id="90192-184">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="90192-185">Обратите внимание, что для некоторых типов проектов предоставляется только параметр **Показать окно предварительного просмотра**.</span><span class="sxs-lookup"><span data-stu-id="90192-185">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Параметры диспетчера пакетов](media/PackageManagerUIOptions.png)

<span data-ttu-id="90192-187">Эти параметры объясняются в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="90192-187">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="90192-188">Показать окно предварительного просмотра</span><span class="sxs-lookup"><span data-stu-id="90192-188">Show preview window</span></span>

<span data-ttu-id="90192-189">При выборе этого параметра модальное окно отображает зависимости выбранного пакета перед его установкой.</span><span class="sxs-lookup"><span data-stu-id="90192-189">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Пример диалогового окна предварительного просмотра](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="90192-191">Параметры установки и обновления</span><span class="sxs-lookup"><span data-stu-id="90192-191">Install and Update Options</span></span>

<span data-ttu-id="90192-192">(доступно не для всех типов проектов)</span><span class="sxs-lookup"><span data-stu-id="90192-192">(Not available for all project types.)</span></span>

<span data-ttu-id="90192-193">**Поведение зависимости** — указывает способ определения устанавливаемых версий зависимых пакетов в NuGet.</span><span class="sxs-lookup"><span data-stu-id="90192-193">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="90192-194">*Игнорировать зависимости* — пропускает установку зависимостей, что обычно приводит к прерыванию установки пакета.</span><span class="sxs-lookup"><span data-stu-id="90192-194">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="90192-195">*Наименьший* [по умолчанию] — устанавливает зависимость с минимальным номером версии, соответствующим требованиям основного выбранного пакета.</span><span class="sxs-lookup"><span data-stu-id="90192-195">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="90192-196">*Наибольший номер исправления* — устанавливает версию с теми же основными и дополнительными номерами версий, но с самым большим номером исправления.</span><span class="sxs-lookup"><span data-stu-id="90192-196">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="90192-197">Например, если указана версия 1.2.2, будет установлена самая высокая версия, которая начинается с 1.2.</span><span class="sxs-lookup"><span data-stu-id="90192-197">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="90192-198">*Наибольший номер дополнительной версии* — устанавливает версию с тем же основным номером версии, но с самым большим номером дополнительной версии и номером исправления.</span><span class="sxs-lookup"><span data-stu-id="90192-198">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="90192-199">Если указана версия 1.2.2, будет установлена самая высокая версия, которая начинается с 1.</span><span class="sxs-lookup"><span data-stu-id="90192-199">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="90192-200">*Наибольший* — устанавливает самую высокую доступную версию пакета.</span><span class="sxs-lookup"><span data-stu-id="90192-200">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="90192-201">**Действие при конфликте файлов** — указывает, как в NuGet должны обрабатываться пакеты, которые уже существуют в проекте или на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="90192-201">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="90192-202">*По приглашению* — NuGet спрашивает, следует ли сохранять или перезаписывать существующие пакеты.</span><span class="sxs-lookup"><span data-stu-id="90192-202">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="90192-203">*Пропустить все* — NuGet пропускает перезапись существующих пакетов.</span><span class="sxs-lookup"><span data-stu-id="90192-203">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="90192-204">*Перезаписать все* — NuGet перезаписывает существующие пакеты.</span><span class="sxs-lookup"><span data-stu-id="90192-204">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="90192-205">Параметры удаления</span><span class="sxs-lookup"><span data-stu-id="90192-205">Uninstall Options</span></span>

<span data-ttu-id="90192-206">(доступно не для всех типов проектов)</span><span class="sxs-lookup"><span data-stu-id="90192-206">(Not available for all project types.)</span></span>

<span data-ttu-id="90192-207">**Удалить зависимости** — удаляются все зависимые пакеты, если на них нет ссылок в других местах проекта.</span><span class="sxs-lookup"><span data-stu-id="90192-207">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="90192-208">**Принудительно удалить, даже если есть зависимости от него** — пакет удаляется, даже если на него по-прежнему есть ссылка в проекте.</span><span class="sxs-lookup"><span data-stu-id="90192-208">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="90192-209">Обычно используется в сочетании с **удалением зависимостей** для удаления пакета и любых установленных зависимостей.</span><span class="sxs-lookup"><span data-stu-id="90192-209">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="90192-210">Но использование этого параметра может привести к нарушению ссылок в проекте.</span><span class="sxs-lookup"><span data-stu-id="90192-210">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="90192-211">В таких случаях может потребоваться [переустановить другие пакеты](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="90192-211">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
