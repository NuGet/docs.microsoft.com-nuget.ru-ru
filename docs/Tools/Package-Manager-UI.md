---
title: "Справочник по пользовательскому Интерфейсу диспетчера пакетов NuGet | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
description: "Инструкции по использованию пользовательского интерфейса диспетчера пакетов NuGet в Visual Studio для работы с пакетами NuGet."
keywords: "NuGet пользовательского интерфейса, диспетчер пакетов NuGet пользовательского интерфейса, NuGet в Visual Studio, управление пакетами NuGet, NuGet пользовательский интерфейс, диспетчер пакетов в Visual Studio"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 35bb856ccff43c77af7eac67da4614d83dcdc533
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/08/2018
---
# <a name="nuget-package-manager-ui"></a><span data-ttu-id="0d696-104">Пользовательский Интерфейс диспетчера пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="0d696-104">NuGet Package Manager UI</span></span>

<span data-ttu-id="0d696-105">Пользовательский Интерфейс диспетчера пакетов NuGet в Visual Studio в Windows позволяет легко устанавливать, удалять и обновить пакеты NuGet в проекты и решения.</span><span class="sxs-lookup"><span data-stu-id="0d696-105">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="0d696-106">Для работы в Visual Studio для Mac, в разделе [пакет NuGet, включая в проекте](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="0d696-106">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="0d696-107">Пользовательский Интерфейс диспетчера пакетов не включено с кодом Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0d696-107">The Package Manager UI is not included with Visual Studio Code.</span></span>

<span data-ttu-id="0d696-108">В этом разделе.</span><span class="sxs-lookup"><span data-stu-id="0d696-108">In this topic:</span></span>

- [<span data-ttu-id="0d696-109">Поиск и установка пакета (вкладка «Обзор»)</span><span class="sxs-lookup"><span data-stu-id="0d696-109">Finding and installing a package (Browse tab)</span></span>](#finding-and-installing-a-package)
- [<span data-ttu-id="0d696-110">При удалении пакета (вкладка «установлено»)</span><span class="sxs-lookup"><span data-stu-id="0d696-110">Uninstalling a package (Installed tab)</span></span>](#uninstalling-a-package)
- <span data-ttu-id="0d696-111">[Обновление пакета (вкладок установки и обновления)](#updating-a-package) (включает в себя [«Неявно ссылается пакет SDK» или «AutoReferenced» сообщения](#implicit_reference))</span><span class="sxs-lookup"><span data-stu-id="0d696-111">[Updating a package (Installed and Updates tabs)](#updating-a-package) (includes the ["Implicitly referenced by an SDK" or "AutoReferenced" message](#implicit_reference))</span></span>
- <span data-ttu-id="0d696-112">[Управление пакетами для решения](#managing-packages-for-the-solution) (Работа с несколькими проектами, в то же время).</span><span class="sxs-lookup"><span data-stu-id="0d696-112">[Managing packages for the solution](#managing-packages-for-the-solution) (working with multiple projects at the same time).</span></span>
- [<span data-ttu-id="0d696-113">Источники пакетов</span><span class="sxs-lookup"><span data-stu-id="0d696-113">Package sources</span></span>](#package-sources)
- [<span data-ttu-id="0d696-114">Параметры диспетчера пакета управления</span><span class="sxs-lookup"><span data-stu-id="0d696-114">Package manager Options control</span></span>](#package-manager-options-control)

> [!Note]
> <span data-ttu-id="0d696-115">Если вы пропустили диспетчер пакетов NuGet в Visual Studio 2015, проверьте **Сервис > расширения и обновления...**  и выполните поиск *диспетчера пакетов NuGet* расширения.</span><span class="sxs-lookup"><span data-stu-id="0d696-115">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="0d696-116">Если вы не удается использовать установщик расширения в Visual Studio, загрузите расширение непосредственно из [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="0d696-116">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="0d696-117">В Visual Studio 2017 г NuGet и диспетчер пакетов NuGet автоматически устанавливается вместе с любой. Рабочие нагрузки, связанные с NET.</span><span class="sxs-lookup"><span data-stu-id="0d696-117">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="0d696-118">Устанавливать по отдельности, выбрав **отдельные компоненты > кода Сервис > Диспетчер пакетов NuGet** в установщике Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="0d696-118">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="0d696-119">Поиск и установка пакета</span><span class="sxs-lookup"><span data-stu-id="0d696-119">Finding and installing a package</span></span>

1. <span data-ttu-id="0d696-120">В **обозревателе решений**, щелкните правой кнопкой мыши либо **ссылки** или проекта, так и выбрать **управление пакетами NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="0d696-120">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Управление пакетами NuGet пункта меню](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="0d696-122">**Обзор** вкладке отображаются популярности из выбранного источника пакетов (в разделе [пакета источников](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="0d696-122">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="0d696-123">Поиск определенного пакета с помощью поля поиска в левом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="0d696-123">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="0d696-124">Выбор пакета из списка для отображения данных, который также включает **установить** кнопку вместе с раскрывающимся списком выбора версии.</span><span class="sxs-lookup"><span data-stu-id="0d696-124">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Управление вкладку Обзор диалоговое окно пакетов NuGet](media/Search.png)

1. <span data-ttu-id="0d696-126">Выберите необходимую версию из раскрывающегося списка и выберите **установить**.</span><span class="sxs-lookup"><span data-stu-id="0d696-126">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="0d696-127">Visual Studio устанавливает пакет и его зависимости в проект.</span><span class="sxs-lookup"><span data-stu-id="0d696-127">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="0d696-128">Может появиться запрос, чтобы принять условия лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="0d696-128">You may be asked to accept license terms.</span></span> <span data-ttu-id="0d696-129">По завершении установки добавлены пакеты отображаются в **установленные** вкладки. Пакеты также перечислены в **ссылки** узел в обозревателе решений, указывающее, ссылаются на них в проект с `using` инструкции.</span><span class="sxs-lookup"><span data-stu-id="0d696-129">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Ссылки в обозревателе решений](media/References.png)

> [!Tip]
    > <span data-ttu-id="0d696-131">Для включения предварительные версии при поиске, а также для предоставления предварительных версий в версии раскрывающегося списка выберите **включить предварительный выпуск** параметр.</span><span class="sxs-lookup"><span data-stu-id="0d696-131">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="0d696-132">Удаление пакета</span><span class="sxs-lookup"><span data-stu-id="0d696-132">Uninstalling a package</span></span>

1. <span data-ttu-id="0d696-133">В **обозревателе решений**, щелкните правой кнопкой мыши либо **ссылки** или нужного проекта и выберите **управление пакетами NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="0d696-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="0d696-134">Выберите **установленные** вкладки.</span><span class="sxs-lookup"><span data-stu-id="0d696-134">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="0d696-135">Выберите пакет для удаления (с помощью поиска для фильтрации списка, при необходимости) и выберите **удаления**.</span><span class="sxs-lookup"><span data-stu-id="0d696-135">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Удаление пакета](media/UninstallPackage.png)

1. <span data-ttu-id="0d696-137">Обратите внимание, что **включить предварительный выпуск** и **источник пакета** элементов управления не действуют при удалении пакетов.</span><span class="sxs-lookup"><span data-stu-id="0d696-137">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="0d696-138">Обновление пакета</span><span class="sxs-lookup"><span data-stu-id="0d696-138">Updating a package</span></span>

1. <span data-ttu-id="0d696-139">В **обозревателе решений**, щелкните правой кнопкой мыши либо **ссылки** или нужного проекта и выберите **управление пакетами NuGet...** . (В проектах веб-сайт, щелкните правой кнопкой мыши **Bin** папки.)</span><span class="sxs-lookup"><span data-stu-id="0d696-139">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="0d696-140">Выберите **обновления** Чтобы просмотреть пакеты, доступные обновления в выбранный пакет источников.</span><span class="sxs-lookup"><span data-stu-id="0d696-140">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="0d696-141">Выберите **включить предварительный выпуск** включать предварительные версии пакетов в списке обновлений.</span><span class="sxs-lookup"><span data-stu-id="0d696-141">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="0d696-142">Выберите пакет для обновления, выберите необходимую версию из раскрывающегося списка справа и выберите **обновление**.</span><span class="sxs-lookup"><span data-stu-id="0d696-142">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Обновление пакета](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="0d696-144">Для некоторых пакетов **обновление** кнопка становится недоступной, и появляется сообщение о том, что он «неявно ссылается пакет SDK» (или «AutoReferenced»).</span><span class="sxs-lookup"><span data-stu-id="0d696-144">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="0d696-145">Данное сообщение указывает, что пакета, например Microsoft.NETCore.App или Microsoft.NETStandard.Library, является частью большего структуре или SDK и не должны обновляться независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="0d696-145">The message indicates that the package, such as Microsoft.NETCore.App or Microsoft.NETStandard.Library, is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="0d696-146">(Эти пакеты помечаются внутренне `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Чтобы обновить пакет, обновите пакет SDK, к которой он принадлежит.</span><span class="sxs-lookup"><span data-stu-id="0d696-146">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) To update the package, update the SDK to which it belongs.</span></span>

    ![Пример пакета пометку неявно ссылки или AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="0d696-148">Чтобы обновить несколько пакетов до их последние версии, выберите их в список и выберите **обновление** кнопку над списком.</span><span class="sxs-lookup"><span data-stu-id="0d696-148">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="0d696-149">Можно также обновить отдельного пакета из **установленные** вкладки. В этом случае данные для пакета включают селектора версии (предметом **включить предварительный выпуск** параметр) и **обновление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="0d696-149">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="0d696-150">Управление пакетами для решения</span><span class="sxs-lookup"><span data-stu-id="0d696-150">Managing packages for the solution</span></span>

<span data-ttu-id="0d696-151">Управление пакетами для решения является удобным средством для одновременно работать с несколькими проектами.</span><span class="sxs-lookup"><span data-stu-id="0d696-151">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="0d696-152">Выберите **Сервис > Диспетчер пакетов NuGet > Управление пакетами NuGet для решения...**  меню команды, или щелкните правой кнопкой мыши решение и выберите **управление пакетами NuGet...** :</span><span class="sxs-lookup"><span data-stu-id="0d696-152">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Управление пакетами NuGet для решения](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="0d696-154">При управлении пакетами для решения, пользовательский Интерфейс позволяет выбрать проекты, затрагиваемые операций:</span><span class="sxs-lookup"><span data-stu-id="0d696-154">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Выбор проекта при управлении пакетами для решения](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="0d696-156">Консолидация вкладки</span><span class="sxs-lookup"><span data-stu-id="0d696-156">Consolidate tab</span></span>

<span data-ttu-id="0d696-157">Разработчики обычно считают, что рекомендуется использовать разные версии того же пакета NuGet в различных проектах в одном решении.</span><span class="sxs-lookup"><span data-stu-id="0d696-157">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="0d696-158">При выборе для управления пакетами для решения, которое предоставляет пользовательский Интерфейс диспетчера пакетов **Консолидация** на которой можно легко увидеть где пакеты с номерами различных версий используются в разных проектах в решении:</span><span class="sxs-lookup"><span data-stu-id="0d696-158">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Вкладка консолидировать пользовательского интерфейса диспетчера пакетов](media/ConsolidateTab.png)

<span data-ttu-id="0d696-160">В этом примере проекта ClassLibrary1 с использованием EntityFramework, 6.2.0, тогда как ConsoleApp1 с использованием EntityFramework 6.1.0.</span><span class="sxs-lookup"><span data-stu-id="0d696-160">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="0d696-161">Чтобы консолидировать версии пакетов, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="0d696-161">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="0d696-162">Выберите проекты для обновления в списке проектов.</span><span class="sxs-lookup"><span data-stu-id="0d696-162">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="0d696-163">Выберите версию для использования в тех проектах, в **версии** элемента управления, например EntityFramework 6.2.0.</span><span class="sxs-lookup"><span data-stu-id="0d696-163">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="0d696-164">Выберите **установить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="0d696-164">Select the **Install** button.</span></span>

<span data-ttu-id="0d696-165">Диспетчер пакетов устанавливается версия выбранного пакета на все выбранные проекты, после чего пакета больше не отображается на **Консолидация** вкладки.</span><span class="sxs-lookup"><span data-stu-id="0d696-165">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="0d696-166">Источники пакетов</span><span class="sxs-lookup"><span data-stu-id="0d696-166">Package sources</span></span>

<span data-ttu-id="0d696-167">Чтобы изменить источник, из которого Visual Studio получает пакеты, выберите один из источника селектора.</span><span class="sxs-lookup"><span data-stu-id="0d696-167">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Селектор источника пакета в пользовательский Интерфейс диспетчера пакетов](media/PackageSourceDropDown.png)

<span data-ttu-id="0d696-169">Управление источниками пакета:</span><span class="sxs-lookup"><span data-stu-id="0d696-169">To manage package sources:</span></span>

1. <span data-ttu-id="0d696-170">Выберите **параметры** значок в пользовательском Интерфейсе диспетчера пакетов приведенным ниже, или использовать **Сервис > Параметры** команд и перейдите к пункту **диспетчера пакетов NuGet**:</span><span class="sxs-lookup"><span data-stu-id="0d696-170">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Значок параметров пользовательского интерфейса диспетчера пакетов](media/PackageSourceSettings.png)

1. <span data-ttu-id="0d696-172">Выберите **источники пакетов** узла:</span><span class="sxs-lookup"><span data-stu-id="0d696-172">Select the **Package Sources** node:</span></span>

    ![Параметры-источники пакетов](media/options.png)

1. <span data-ttu-id="0d696-174">Добавление источника, выберите  **+** , изменить имя, введите URL-адрес или путь в **источника** управления и выберите **обновление**.</span><span class="sxs-lookup"><span data-stu-id="0d696-174">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="0d696-175">Источник теперь отображается в селекторе раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="0d696-175">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="0d696-176">Чтобы изменить источник пакета, выберите его, внесите изменения в **имя** и **источника** поля, а затем выберите **обновление**.</span><span class="sxs-lookup"><span data-stu-id="0d696-176">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="0d696-177">Чтобы отключить источник пакета, снимите флажок слева от имени в списке.</span><span class="sxs-lookup"><span data-stu-id="0d696-177">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="0d696-178">Чтобы удалить источник пакета, выберите его, а затем выберите **X** кнопки.</span><span class="sxs-lookup"><span data-stu-id="0d696-178">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="0d696-179">Используйте вверх и Стрелка вниз, чтобы изменить порядок приоритета из источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="0d696-179">Use the up and down arrow buttons to change the priority order of the package sources.</span></span> <span data-ttu-id="0d696-180">Visual Studio осуществляет эти источники в порядке приоритета, когда восстановление пакетов для проекта.</span><span class="sxs-lookup"><span data-stu-id="0d696-180">Visual Studio searches these sources in the priority order when restoring packages for a project.</span></span> <span data-ttu-id="0d696-181">Дополнительные сведения см. в разделе [восстановление пакета](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="0d696-181">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="0d696-182">Если источник пакета снова появляется после удаления, могут быть указаны в уровне компьютера или уровня пользователя `NuGet.Config` файлов.</span><span class="sxs-lookup"><span data-stu-id="0d696-182">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="0d696-183">В разделе [NuGet Настройка поведения](../consume-packages/configuring-nuget-behavior.md) расположение этих файлов, удалите источник редактирования файлов вручную или с помощью [nuget источники команда](../tools/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="0d696-183">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="0d696-184">Параметры диспетчера пакета управления</span><span class="sxs-lookup"><span data-stu-id="0d696-184">Package manager Options control</span></span>

<span data-ttu-id="0d696-185">При выборе пакета, пользовательский Интерфейс диспетчера пакетов отображает небольшая, расширяемый **параметры** управления под селектор версии (показаны оба свернутое и развернутое).</span><span class="sxs-lookup"><span data-stu-id="0d696-185">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="0d696-186">Обратите внимание, что для некоторых проектов только для типов, **Показать окно предварительного просмотра** предоставить параметр.</span><span class="sxs-lookup"><span data-stu-id="0d696-186">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Параметры диспетчера пакетов](media/PackageManagerUIOptions.png)

<span data-ttu-id="0d696-188">В следующих разделах эти параметры.</span><span class="sxs-lookup"><span data-stu-id="0d696-188">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="0d696-189">Показать окно предварительного просмотра</span><span class="sxs-lookup"><span data-stu-id="0d696-189">Show preview window</span></span>

<span data-ttu-id="0d696-190">При выборе модальное окно отображает которой зависимости выбранного пакета перед установкой пакета:</span><span class="sxs-lookup"><span data-stu-id="0d696-190">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Пример этого окна предварительного просмотра](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="0d696-192">Параметры установки и обновления</span><span class="sxs-lookup"><span data-stu-id="0d696-192">Install and Update Options</span></span>

<span data-ttu-id="0d696-193">(Доступно не для всех типов проектов.)</span><span class="sxs-lookup"><span data-stu-id="0d696-193">(Not available for all project types.)</span></span>

<span data-ttu-id="0d696-194">**Поведение зависимостей** настраивает как NuGet решает, какие версии зависимых пакетов для установки:</span><span class="sxs-lookup"><span data-stu-id="0d696-194">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="0d696-195">*Пропуск зависимостей* пропускает установки все зависимости, которая обычно нарушает устанавливаемого пакета.</span><span class="sxs-lookup"><span data-stu-id="0d696-195">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="0d696-196">*Наименьший* [Default] устанавливает зависимость с номером версии минимальным требованиям первичного выбранного пакета.</span><span class="sxs-lookup"><span data-stu-id="0d696-196">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="0d696-197">*Исправление с наивысшим* устанавливает версию с одинаковые номера основной и вспомогательной версии, но с наибольшим числом исправления.</span><span class="sxs-lookup"><span data-stu-id="0d696-197">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="0d696-198">Например если указана версия 1.2.2 затем самую новую версию, которая начинается с 1.2 будет установлен</span><span class="sxs-lookup"><span data-stu-id="0d696-198">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="0d696-199">*Наибольший вспомогательные* устанавливает версию с тот же номер основной версии, но наивысший дополнительный номер и номер исправления.</span><span class="sxs-lookup"><span data-stu-id="0d696-199">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="0d696-200">Если указана версия 1.2.2, затем самую новую версию, которая начинается с 1 будет установлен</span><span class="sxs-lookup"><span data-stu-id="0d696-200">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="0d696-201">*Наибольший* устанавливает наибольший доступная версия пакета.</span><span class="sxs-lookup"><span data-stu-id="0d696-201">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="0d696-202">**Файл действия конфликт** указывает порядок обработки NuGet пакеты, которые уже существуют в проекте или на локальном компьютере:</span><span class="sxs-lookup"><span data-stu-id="0d696-202">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="0d696-203">*Запрос* предписывает NuGet спросить, следует ли оставить или заменить существующие пакеты.</span><span class="sxs-lookup"><span data-stu-id="0d696-203">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="0d696-204">*Пропустить все* предписывает NuGet, чтобы пропустить, перезаписывая все существующие пакеты.</span><span class="sxs-lookup"><span data-stu-id="0d696-204">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="0d696-205">*Перезаписать все* предписывает NuGet, чтобы перезаписать все существующие пакеты.</span><span class="sxs-lookup"><span data-stu-id="0d696-205">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="0d696-206">Удалить параметры</span><span class="sxs-lookup"><span data-stu-id="0d696-206">Uninstall Options</span></span>

<span data-ttu-id="0d696-207">(Доступно не для всех типов проектов.)</span><span class="sxs-lookup"><span data-stu-id="0d696-207">(Not available for all project types.)</span></span>

<span data-ttu-id="0d696-208">**Удалите зависимости**: при выборе удаляет все зависимые пакеты, если вы не обращается к ним в другом месте в проекте.</span><span class="sxs-lookup"><span data-stu-id="0d696-208">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="0d696-209">**Принудительно удалить, даже если есть зависимости от его**: при выборе удаляет пакет, даже если он будет по-прежнему, на которую ссылается проект.</span><span class="sxs-lookup"><span data-stu-id="0d696-209">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="0d696-210">Обычно используется в сочетании с **удаления зависимостей** для удаления пакета и любые зависимости он установлен.</span><span class="sxs-lookup"><span data-stu-id="0d696-210">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="0d696-211">При использовании этого параметра может тем не менее, привести к нарушенным ссылкам в проект.</span><span class="sxs-lookup"><span data-stu-id="0d696-211">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="0d696-212">В таких случаях может потребоваться [переустановить эти другие пакеты](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="0d696-212">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
