---
title: Установка и управление пакетами NuGet в Visual Studio
description: Инструкции по использованию пользовательского интерфейса диспетчера пакетов NuGet в Visual Studio для работы с пакетами NuGet.
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 97e5de3f07199cd3c6a645749c8f2f1603ca630e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426238"
---
# <a name="install-and-manage-packages-in-visual-studio"></a><span data-ttu-id="10dc6-103">Установка пакетов и управления ими в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="10dc6-103">Install and manage packages in Visual Studio</span></span>

<span data-ttu-id="10dc6-104">Пользовательский Интерфейс диспетчера пакетов NuGet в Visual Studio в Windows позволяет легко установка, удаление и обновление пакетов NuGet в проектах и решениях.</span><span class="sxs-lookup"><span data-stu-id="10dc6-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="10dc6-105">Возможности в Visual Studio для Mac, см. в разделе [Включение пакета NuGet в проекте](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="10dc6-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="10dc6-106">Пользовательский Интерфейс диспетчера пакетов не входит в состав Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="10dc6-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="10dc6-107">Если вы пропустили диспетчер пакетов NuGet в Visual Studio 2015, проверьте **Сервис > расширения и обновления...**  и выполните поиск *диспетчер пакетов NuGet* расширения.</span><span class="sxs-lookup"><span data-stu-id="10dc6-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="10dc6-108">Если вы не удается использовать установщик расширений в Visual Studio, чтобы скачать расширение непосредственно из [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="10dc6-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="10dc6-109">Начиная с Visual Studio 2017, NuGet и диспетчер пакетов NuGet автоматически устанавливаются вместе с любой. Рабочие нагрузки, связанные с NET.</span><span class="sxs-lookup"><span data-stu-id="10dc6-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="10dc6-110">Установить по отдельности, выбрав **отдельные компоненты > средства кода > Диспетчер пакетов NuGet** параметр в установщике Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="10dc6-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="10dc6-111">Поиск и установка пакета</span><span class="sxs-lookup"><span data-stu-id="10dc6-111">Finding and installing a package</span></span>

1. <span data-ttu-id="10dc6-112">В **обозревателе решений**, щелкните правой кнопкой мыши либо **ссылки** или проект и выберите **управление пакетами NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="10dc6-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Управление пакетами NuGet пункт меню](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="10dc6-114">**Обзор** вкладке отображаются пакеты по популярности из выбранного источника (см. в разделе [источников пакетов](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="10dc6-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="10dc6-115">Поиск определенного пакета с помощью поля поиска в левом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="10dc6-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="10dc6-116">Выберите пакет из списка для отображения данных, который также позволяет **установить** кнопки, а также раскрывающийся список выбора версии.</span><span class="sxs-lookup"><span data-stu-id="10dc6-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Управление вкладку Обзор диалоговое окно пакетов NuGet](media/Search.png)

1. <span data-ttu-id="10dc6-118">Выберите нужную версию из раскрывающегося списка и выберите **установить**.</span><span class="sxs-lookup"><span data-stu-id="10dc6-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="10dc6-119">Visual Studio устанавливает пакет и его зависимости в проект.</span><span class="sxs-lookup"><span data-stu-id="10dc6-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="10dc6-120">Может быть предложено принять условия лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="10dc6-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="10dc6-121">По завершении установки добавлены пакеты отображаются на **установленные** вкладки. Пакеты также отображаются в **ссылки** узле обозревателя решений, указывающее, можно обратиться к ним в проекте с `using` инструкций.</span><span class="sxs-lookup"><span data-stu-id="10dc6-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Ссылки в обозревателе решений](media/References.png)

> [!Tip]
> <span data-ttu-id="10dc6-123">Для включения предварительных версий при поиске и чтобы сделать предварительные версии, доступной в версии раскрывающегося списка, выберите **включить предварительные выпуски** параметр.</span><span class="sxs-lookup"><span data-stu-id="10dc6-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="10dc6-124">Удаление пакета</span><span class="sxs-lookup"><span data-stu-id="10dc6-124">Uninstalling a package</span></span>

1. <span data-ttu-id="10dc6-125">В **обозревателе решений**, щелкните правой кнопкой мыши либо **ссылки** или нужный проект и выберите **управление пакетами NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="10dc6-125">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="10dc6-126">Выберите **установленные** вкладки.</span><span class="sxs-lookup"><span data-stu-id="10dc6-126">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="10dc6-127">Выберите пакет для удаления (с помощью поиска для фильтрации списка, при необходимости) и нажмите кнопку **удаления**.</span><span class="sxs-lookup"><span data-stu-id="10dc6-127">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Удаление пакета](media/UninstallPackage.png)

1. <span data-ttu-id="10dc6-129">Обратите внимание, что **включить предварительные выпуски** и **источник пакета** элементы управления не действуют при удалении пакетов.</span><span class="sxs-lookup"><span data-stu-id="10dc6-129">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="10dc6-130">Обновление пакета</span><span class="sxs-lookup"><span data-stu-id="10dc6-130">Updating a package</span></span>

1. <span data-ttu-id="10dc6-131">В **обозревателе решений**, щелкните правой кнопкой мыши либо **ссылки** или нужный проект и выберите **управление пакетами NuGet...** . (В проектах веб-сайт, щелкните правой кнопкой мыши **Bin** папки.)</span><span class="sxs-lookup"><span data-stu-id="10dc6-131">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="10dc6-132">Выберите **обновления** вкладку, чтобы увидеть пакеты, которые имеют доступные обновления из источников выбранного пакета.</span><span class="sxs-lookup"><span data-stu-id="10dc6-132">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="10dc6-133">Выберите **включить предварительные выпуски** содержать предварительные выпуски пакетов в списке обновлений.</span><span class="sxs-lookup"><span data-stu-id="10dc6-133">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="10dc6-134">Выберите пакет для обновления, выберите нужную версию из раскрывающегося списка справа и выберите **обновление**.</span><span class="sxs-lookup"><span data-stu-id="10dc6-134">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Обновление пакета](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="10dc6-136">Для некоторых пакетов **обновления** кнопка отключена, появится сообщение о том, что он является «неявно ссылается пакет SDK» (или «Автоссылками»).</span><span class="sxs-lookup"><span data-stu-id="10dc6-136">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="10dc6-137">Это сообщение означает, что пакет является частью большего размера платформа или пакет SDK и не должны обновляться независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="10dc6-137">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="10dc6-138">(Такие пакеты отмечены внутренне `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Например `Microsoft.NETCore.App` является частью пакета SDK для .NET Core, и версия пакета не соответствует версии платформы среды выполнения, используемые приложением.</span><span class="sxs-lookup"><span data-stu-id="10dc6-138">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="10dc6-139">Вам нужно [обновить установку .NET Core](https://aka.ms/dotnet-download) для получения новых версий среды выполнения ASP.NET Core и .NET Core.</span><span class="sxs-lookup"><span data-stu-id="10dc6-139">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="10dc6-140">[Дополнительные сведения см. в разделе о метапакеты .NET Core и управлении версиями](/dotnet/core/packages).</span><span class="sxs-lookup"><span data-stu-id="10dc6-140">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="10dc6-141">Это относится к следующим пакетам часто используемые:</span><span class="sxs-lookup"><span data-stu-id="10dc6-141">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="10dc6-142">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="10dc6-142">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="10dc6-143">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="10dc6-143">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="10dc6-144">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="10dc6-144">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="10dc6-145">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="10dc6-145">NETStandard.Library</span></span>

    ![Пример пакета помечен как неявно, ссылки или Автоссылками](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="10dc6-147">Чтобы обновить несколько пакетов до последней версии, выберите их в списке и выберите **обновление** кнопку над списком.</span><span class="sxs-lookup"><span data-stu-id="10dc6-147">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="10dc6-148">Вы также можете обновить отдельный пакет из **установленные** вкладки. В этом случае данные для пакета включают выбора версий (регулируются **включить предварительные выпуски** параметр) и **обновления** кнопки.</span><span class="sxs-lookup"><span data-stu-id="10dc6-148">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="10dc6-149">Управление пакетами для решения</span><span class="sxs-lookup"><span data-stu-id="10dc6-149">Managing packages for the solution</span></span>

<span data-ttu-id="10dc6-150">Управление пакетами для решения — это удобный способ для работы с несколькими проектами одновременно.</span><span class="sxs-lookup"><span data-stu-id="10dc6-150">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="10dc6-151">Выберите **Сервис > Диспетчер пакетов NuGet > Управление пакетами NuGet для решения...**  меню команды, или щелкните правой кнопкой мыши решение и выберите **управление пакетами NuGet...** :</span><span class="sxs-lookup"><span data-stu-id="10dc6-151">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Управление пакетами NuGet для решения](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="10dc6-153">При управлении пакетами для решения, пользовательский Интерфейс позволяет выбрать проекты, которые были затронуты операций:</span><span class="sxs-lookup"><span data-stu-id="10dc6-153">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Выбор проекта при управлении пакетами для решения](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="10dc6-155">Объединить вкладки</span><span class="sxs-lookup"><span data-stu-id="10dc6-155">Consolidate tab</span></span>

<span data-ttu-id="10dc6-156">Как правило, разработчикам рассматривать ее рекомендуется использовать различные версии одного пакета NuGet в различных проектах в одном решении.</span><span class="sxs-lookup"><span data-stu-id="10dc6-156">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="10dc6-157">При выборе для управления пакетами для решения, предоставляет пользовательский Интерфейс диспетчера пакетов **Консолидация** вкладки, на котором было видно где пакеты с номерами различных версий используются разные проекты в решении:</span><span class="sxs-lookup"><span data-stu-id="10dc6-157">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Вкладка консолидировать пользовательского интерфейса диспетчера пакетов](media/ConsolidateTab.png)

<span data-ttu-id="10dc6-159">В этом примере проект ClassLibrary1 с использованием EntityFramework, 6.2.0, тогда как ConsoleApp1 использует EntityFramework 6.1.0.</span><span class="sxs-lookup"><span data-stu-id="10dc6-159">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="10dc6-160">Чтобы консолидировать версии пакетов, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="10dc6-160">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="10dc6-161">Выберите проекты для обновления в списке проектов.</span><span class="sxs-lookup"><span data-stu-id="10dc6-161">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="10dc6-162">Выберите версию для использования этих проектов в **версии** элемента управления, например EntityFramework 6.2.0.</span><span class="sxs-lookup"><span data-stu-id="10dc6-162">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="10dc6-163">Выберите **установить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="10dc6-163">Select the **Install** button.</span></span>

<span data-ttu-id="10dc6-164">Диспетчер пакетов устанавливается версия выбранного пакета на все выбранные проекты, после чего пакета больше не отображается на **Консолидация** вкладки.</span><span class="sxs-lookup"><span data-stu-id="10dc6-164">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="10dc6-165">Источники пакетов</span><span class="sxs-lookup"><span data-stu-id="10dc6-165">Package sources</span></span>

<span data-ttu-id="10dc6-166">Чтобы изменить источник, из которой Visual Studio получает пакеты, выберите один из выбора источника:</span><span class="sxs-lookup"><span data-stu-id="10dc6-166">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Селектор источника пакета в пользовательского интерфейса диспетчера пакетов](media/PackageSourceDropDown.png)

<span data-ttu-id="10dc6-168">Для управления источники пакетов:</span><span class="sxs-lookup"><span data-stu-id="10dc6-168">To manage package sources:</span></span>

1. <span data-ttu-id="10dc6-169">Выберите **параметры** значок в пользовательском Интерфейсе диспетчера пакетов, описанные ниже, или использовать **Сервис > Параметры** команды и прокрутите экран до **диспетчер пакетов NuGet**:</span><span class="sxs-lookup"><span data-stu-id="10dc6-169">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Значок "Параметры" пользовательского интерфейса диспетчера пакетов](media/PackageSourceSettings.png)

1. <span data-ttu-id="10dc6-171">Выберите **источники пакетов** узла:</span><span class="sxs-lookup"><span data-stu-id="10dc6-171">Select the **Package Sources** node:</span></span>

    ![Параметры источников пакетов](media/options.png)

1. <span data-ttu-id="10dc6-173">Добавление источника, выберите **+** , измените имя, введите URL-адрес или путь в **источника** управления и выберите **обновления**.</span><span class="sxs-lookup"><span data-stu-id="10dc6-173">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="10dc6-174">Источник теперь отображается в раскрывающемся списке выбора.</span><span class="sxs-lookup"><span data-stu-id="10dc6-174">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="10dc6-175">Чтобы изменить источник пакета, выберите его, внесите изменения в **имя** и **источника** поля, а затем выберите **обновления**.</span><span class="sxs-lookup"><span data-stu-id="10dc6-175">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="10dc6-176">Чтобы отключить источник пакетов, снимите флажок слева от имени в списке.</span><span class="sxs-lookup"><span data-stu-id="10dc6-176">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="10dc6-177">Чтобы удалить источник пакета, выберите его, а затем выберите **X** кнопки.</span><span class="sxs-lookup"><span data-stu-id="10dc6-177">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="10dc6-178">С помощью вверх и Стрелка вниз кнопки не изменяет порядок источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="10dc6-178">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="10dc6-179">Visual Studio игнорирует порядок источников пакетов, используя пакет из любого источника, первым отвечать на запросы.</span><span class="sxs-lookup"><span data-stu-id="10dc6-179">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="10dc6-180">Дополнительные сведения см. в разделе [восстановление пакетов](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="10dc6-180">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="10dc6-181">Если источник пакета снова появится после его удаления, могут быть указаны на уровне компьютера или пользователя на уровне `NuGet.Config` файлов.</span><span class="sxs-lookup"><span data-stu-id="10dc6-181">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="10dc6-182">См. в разделе [NuGet распространенных конфигураций](../consume-packages/configuring-nuget-behavior.md) для расположения этих файлов, затем удалите исходную, изменив файлы вручную или с помощью [nuget источники команда](../tools/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="10dc6-182">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="10dc6-183">Управление параметрами диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="10dc6-183">Package manager Options control</span></span>

<span data-ttu-id="10dc6-184">При выборе пакета, пользовательский Интерфейс диспетчера пакетов отображается небольшой, расширяемый **параметры** управления под выбора версий (Здесь показаны оба сворачивать и разворачивать).</span><span class="sxs-lookup"><span data-stu-id="10dc6-184">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="10dc6-185">Обратите внимание, что для некоторых проекта только для типов, **Показать окно предварительного просмотра** параметр.</span><span class="sxs-lookup"><span data-stu-id="10dc6-185">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Параметры диспетчера пакетов](media/PackageManagerUIOptions.png)

<span data-ttu-id="10dc6-187">В следующих разделах эти параметры.</span><span class="sxs-lookup"><span data-stu-id="10dc6-187">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="10dc6-188">Показать окно предварительного просмотра</span><span class="sxs-lookup"><span data-stu-id="10dc6-188">Show preview window</span></span>

<span data-ttu-id="10dc6-189">При выборе модальное окно отображает которой зависимости выбранного пакета перед установкой пакета:</span><span class="sxs-lookup"><span data-stu-id="10dc6-189">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Диалоговое окно предварительного просмотра пример](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="10dc6-191">Установка и обновление параметров</span><span class="sxs-lookup"><span data-stu-id="10dc6-191">Install and Update Options</span></span>

<span data-ttu-id="10dc6-192">(Недоступно для всех типов проектов.)</span><span class="sxs-lookup"><span data-stu-id="10dc6-192">(Not available for all project types.)</span></span>

<span data-ttu-id="10dc6-193">**Поведение зависимостей** настраивает как NuGet определяет, какие версии зависимых пакетов для установки:</span><span class="sxs-lookup"><span data-stu-id="10dc6-193">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="10dc6-194">*Пропуск зависимостей* пропускает Установка всех зависимостей, которая обычно нарушает устанавливаемого пакета.</span><span class="sxs-lookup"><span data-stu-id="10dc6-194">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="10dc6-195">*Наименьшее* [Default] устанавливает зависимость с номер минимальной версии, отвечающий требованиям основного выбранного пакета.</span><span class="sxs-lookup"><span data-stu-id="10dc6-195">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="10dc6-196">*Самый высокий Patch* устанавливает версию с теми же номерами основного и дополнительного номеров версий, но наибольший номер исправления.</span><span class="sxs-lookup"><span data-stu-id="10dc6-196">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="10dc6-197">Например если указана версия 1.2.2 затем старшую версию, которая начинается с 1.2 устанавливается</span><span class="sxs-lookup"><span data-stu-id="10dc6-197">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="10dc6-198">*Самый высокий Minor* устанавливает версию с тем же основной номер версии, но наибольший номер, дополнительный номер и номера исправления.</span><span class="sxs-lookup"><span data-stu-id="10dc6-198">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="10dc6-199">Если указана версия 1.2.2, затем старшую версию, которая начинается с 1 устанавливается</span><span class="sxs-lookup"><span data-stu-id="10dc6-199">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="10dc6-200">*Самый высокий* устанавливает старшая доступная версия пакета.</span><span class="sxs-lookup"><span data-stu-id="10dc6-200">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="10dc6-201">**Файл действие конфликта** указывает, как NuGet должен обрабатывать пакеты, которые уже существуют в проекте или в локальном компьютере:</span><span class="sxs-lookup"><span data-stu-id="10dc6-201">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="10dc6-202">*Prompt* предписывает NuGet ли сохранить или перезаписать существующие пакеты.</span><span class="sxs-lookup"><span data-stu-id="10dc6-202">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="10dc6-203">*Пропустить все* предписывает NuGet пропустит, перезаписывая все существующие пакеты.</span><span class="sxs-lookup"><span data-stu-id="10dc6-203">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="10dc6-204">*Перезаписать все* предоставляет диспетчеру NuGet, чтобы перезаписать все существующие пакеты.</span><span class="sxs-lookup"><span data-stu-id="10dc6-204">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="10dc6-205">Удалить параметры</span><span class="sxs-lookup"><span data-stu-id="10dc6-205">Uninstall Options</span></span>

<span data-ttu-id="10dc6-206">(Недоступно для всех типов проектов.)</span><span class="sxs-lookup"><span data-stu-id="10dc6-206">(Not available for all project types.)</span></span>

<span data-ttu-id="10dc6-207">**Удаление зависимостей**: при выборе удаляет все зависимые пакеты, если они не есть ссылки на них в другом месте в проекте.</span><span class="sxs-lookup"><span data-stu-id="10dc6-207">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="10dc6-208">**Принудительное удаление, даже при наличии зависимости на нем**: при выборе удаляет пакет, даже если он по-прежнему приведена ссылка в проекте.</span><span class="sxs-lookup"><span data-stu-id="10dc6-208">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="10dc6-209">Обычно используется в сочетании с **удалить зависимости** удаляемый пакет и все зависимости, она установлена.</span><span class="sxs-lookup"><span data-stu-id="10dc6-209">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="10dc6-210">С помощью этого параметра может тем не менее, привести к нарушенным ссылкам в проект.</span><span class="sxs-lookup"><span data-stu-id="10dc6-210">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="10dc6-211">В таких случаях может потребоваться [переустановить эти другие пакеты](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="10dc6-211">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
