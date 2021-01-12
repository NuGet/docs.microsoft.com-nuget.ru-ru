---
title: Установка пакетов NuGet и управление ими с помощью консоли в Visual Studio
description: Инструкции по использованию консоли диспетчера пакетов NuGet в Visual Studio для работы с пакетами.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 31fa51bc017eaaf9306d5f267e5d4b0d7a15ec9c
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699842"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="eb02e-103">Установка пакетов и управление ими с помощью консоли диспетчера пакетов в Visual Studio (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="eb02e-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="eb02e-104">Консоль диспетчера пакетов NuGet позволяет использовать [команды PowerShell NuGet](../reference/powershell-reference.md) для поиска, установки, удаления и обновления пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="eb02e-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../reference/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="eb02e-105">Это удобно, когда пользовательский интерфейс диспетчера пакетов не позволяет выполнять операции.</span><span class="sxs-lookup"><span data-stu-id="eb02e-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="eb02e-106">См. подробнее об [использовании CLI `nuget.exe` в консоли](#use-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="eb02e-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#use-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="eb02e-107">Консоль встроена в Visual Studio для Windows.</span><span class="sxs-lookup"><span data-stu-id="eb02e-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="eb02e-108">Она не включена в Visual Studio для Mac и Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="eb02e-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

> [!Important]
> <span data-ttu-id="eb02e-109">Перечисленные здесь команды относятся только к консоли диспетчера пакетов в Visual Studio и отличаются от [команд модуля "Управление пакетами"](/powershell/module/packagemanagement/), доступных в общей среде PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eb02e-109">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="eb02e-110">В частности, в каждой среде есть команды, недоступные в другой среде, а в командах с тем же именем могут отличаться некоторые аргументы.</span><span class="sxs-lookup"><span data-stu-id="eb02e-110">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="eb02e-111">При использовании консоли "Управление пакетами" в Visual Studio применяются команды и аргументы, описанные в этой статье.</span><span class="sxs-lookup"><span data-stu-id="eb02e-111">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="eb02e-112">Поиск и установка пакета</span><span class="sxs-lookup"><span data-stu-id="eb02e-112">Find and install a package</span></span>

<span data-ttu-id="eb02e-113">Для поиска и установки пакета необходимо выполнить три простых шага:</span><span class="sxs-lookup"><span data-stu-id="eb02e-113">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="eb02e-114">Откройте проект или решение в Visual Studio, а затем откройте консоль, щелкнув **Средства > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="eb02e-114">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="eb02e-115">Найдите пакет, который требуется установить.</span><span class="sxs-lookup"><span data-stu-id="eb02e-115">Find the package you want to install.</span></span> <span data-ttu-id="eb02e-116">Если вы уже знакомы с этим процессом, перейдите к шагу 3.</span><span class="sxs-lookup"><span data-stu-id="eb02e-116">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="eb02e-117">Выполните команду установки:</span><span class="sxs-lookup"><span data-stu-id="eb02e-117">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="eb02e-118">Все операции, доступные в консоли, также можно выполнить с помощью [CLI NuGet](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="eb02e-118">All operations that are available in the console can also be done with the [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="eb02e-119">Но команды консоли работают в контексте Visual Studio и сохраненного проекта или решения, и область их применения часто шире, чем у их эквивалентов в CLI.</span><span class="sxs-lookup"><span data-stu-id="eb02e-119">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="eb02e-120">Например, при установке пакета с помощью консоли добавляется ссылка на проект, а при использовании команды CLI этого не происходит.</span><span class="sxs-lookup"><span data-stu-id="eb02e-120">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="eb02e-121">По этой причине разработчики, работающие в Visual Studio, обычно предпочитают использовать консоль вместо CLI.</span><span class="sxs-lookup"><span data-stu-id="eb02e-121">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="eb02e-122">Многие операции консоли зависят от наличия решения, открытого в Visual Studio с использованием известного имени пути.</span><span class="sxs-lookup"><span data-stu-id="eb02e-122">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="eb02e-123">Если у вас нет решения или оно не сохранено, отобразится сообщение об ошибке "Решение не открыто или не сохранено.</span><span class="sxs-lookup"><span data-stu-id="eb02e-123">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="eb02e-124">Убедитесь, что вы открыли и сохранили решение".</span><span class="sxs-lookup"><span data-stu-id="eb02e-124">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="eb02e-125">Это означает, что консоль не может определить папку решения.</span><span class="sxs-lookup"><span data-stu-id="eb02e-125">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="eb02e-126">Эту ошибку можно исправить, сохранив несохраненное решение или создав и сохранив решение, если оно не открыто.</span><span class="sxs-lookup"><span data-stu-id="eb02e-126">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="eb02e-127">Открытие консоли и элементов управления консоли</span><span class="sxs-lookup"><span data-stu-id="eb02e-127">Opening the console and console controls</span></span>

1. <span data-ttu-id="eb02e-128">Откройте консоль в Visual Studio, щелкнув **Средства > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="eb02e-128">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="eb02e-129">Консоль — это окно Visual Studio, которое может быть упорядочено и размещено по вашему усмотрению (см. руководство по [настройке макетов окон в Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="eb02e-129">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="eb02e-130">По умолчанию команды консоли работают с конкретным источником пакета и проектом, как указано в элементе управления в верхней части окна.</span><span class="sxs-lookup"><span data-stu-id="eb02e-130">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Элементы управления консоли диспетчера пакетов для источника пакета и проекта](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="eb02e-132">Выбор другого источника пакета или проекта изменяет эти значения по умолчанию для последующих команд.</span><span class="sxs-lookup"><span data-stu-id="eb02e-132">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="eb02e-133">Чтобы переопределить эти настройки, не меняя значения по умолчанию, большинство команд поддерживают параметры `-Source` и `-ProjectName`.</span><span class="sxs-lookup"><span data-stu-id="eb02e-133">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="eb02e-134">Чтобы управлять источниками пакетов, щелкните значок шестеренки.</span><span class="sxs-lookup"><span data-stu-id="eb02e-134">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="eb02e-135">Это ярлык для диалогового окна **Средства > Параметры > Диспетчер пакетов NuGet > Источники пакетов**, как описано на странице, посвященной [пользовательскому интерфейсу диспетчера пакетов](install-use-packages-visual-studio.md#package-sources).</span><span class="sxs-lookup"><span data-stu-id="eb02e-135">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](install-use-packages-visual-studio.md#package-sources) page.</span></span> <span data-ttu-id="eb02e-136">Кроме того, элемент управления справа от средства выбора проектов очищает содержимое консоли.</span><span class="sxs-lookup"><span data-stu-id="eb02e-136">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Параметры консоли диспетчера пакетов и элементы очистки](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="eb02e-138">Крайняя правая кнопка прерывает команду, которая выполняется в течение долгого периода времени.</span><span class="sxs-lookup"><span data-stu-id="eb02e-138">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="eb02e-139">Например, выполнение `Get-Package -ListAvailable -PageSize 500` перечисляет первые 500 пакетов в источнике по умолчанию (например, nuget.org), что может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="eb02e-139">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Элемент управления для прерывания выполнения в консоли диспетчера пакетов](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a><span data-ttu-id="eb02e-141">Установка пакета</span><span class="sxs-lookup"><span data-stu-id="eb02e-141">Install a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="eb02e-142">См. подробнее об [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="eb02e-142">See [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span></span>

<span data-ttu-id="eb02e-143">При установке пакета в консоли выполняются те же действия, которые описаны в руководстве по [установке пакета NuGet](../concepts/package-installation-process.md), со следующими дополнениями:</span><span class="sxs-lookup"><span data-stu-id="eb02e-143">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="eb02e-144">Консоль отображает применимые условия лицензии в окне с соответствующим соглашением.</span><span class="sxs-lookup"><span data-stu-id="eb02e-144">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="eb02e-145">Если вы не согласны с условиями, следует сразу же удалить пакет.</span><span class="sxs-lookup"><span data-stu-id="eb02e-145">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="eb02e-146">Кроме того, ссылка на пакет добавляется в файл проекта и отображается в **обозревателе решений** в узле **Ссылки**. Сохраните проект, чтобы просмотреть изменения непосредственно в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="eb02e-146">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="eb02e-147">Удаление пакета</span><span class="sxs-lookup"><span data-stu-id="eb02e-147">Uninstall a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="eb02e-148">См. подробнее об [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="eb02e-148">See [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="eb02e-149">Если необходимо найти идентификатор, чтобы просмотреть все пакеты, установленные в проекте по умолчанию, используйте команду [Get-Package](../reference/ps-reference/ps-ref-get-package.md).</span><span class="sxs-lookup"><span data-stu-id="eb02e-149">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="eb02e-150">При удалении пакета выполняются следующие действия:</span><span class="sxs-lookup"><span data-stu-id="eb02e-150">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="eb02e-151">Удаляются ссылки на пакет из проекта (и любого используемого формата управления).</span><span class="sxs-lookup"><span data-stu-id="eb02e-151">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="eb02e-152">Ссылки больше не отображаются в **обозревателе решений**</span><span class="sxs-lookup"><span data-stu-id="eb02e-152">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="eb02e-153">(возможно, потребуется перестроить проект, чтобы он был удален из папки **Bin**).</span><span class="sxs-lookup"><span data-stu-id="eb02e-153">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="eb02e-154">Отменяются все изменения, внесенные в `app.config` или `web.config` при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="eb02e-154">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="eb02e-155">Удаляются ранее установленные зависимости, если остальные пакеты не используют эти зависимости.</span><span class="sxs-lookup"><span data-stu-id="eb02e-155">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="eb02e-156">Обновление пакета</span><span class="sxs-lookup"><span data-stu-id="eb02e-156">Update a package</span></span>

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

<span data-ttu-id="eb02e-157">См. подробнее о [Get-Package](../reference/ps-reference/ps-ref-get-package.md) и [Update-Package](../reference/ps-reference/ps-ref-update-package.md).</span><span class="sxs-lookup"><span data-stu-id="eb02e-157">See [Get-Package](../reference/ps-reference/ps-ref-get-package.md) and [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span></span>

## <a name="find-a-package"></a><span data-ttu-id="eb02e-158">Поиск пакета</span><span class="sxs-lookup"><span data-stu-id="eb02e-158">Find a package</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

<span data-ttu-id="eb02e-159">См. подробнее о [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="eb02e-159">See [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span></span> <span data-ttu-id="eb02e-160">В Visual Studio 2013 и более ранних версиях используйте команду [Get-Package](../reference/ps-reference/ps-ref-get-package.md).</span><span class="sxs-lookup"><span data-stu-id="eb02e-160">In Visual Studio 2013 and earlier, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="eb02e-161">Доступность консоли</span><span class="sxs-lookup"><span data-stu-id="eb02e-161">Availability of the console</span></span>

<span data-ttu-id="eb02e-162">Начиная с Visual Studio 2017, NuGet и диспетчер пакетов NuGet автоматически устанавливаются при выборе рабочей нагрузки, связанной с .NET. Вы также можете установить эти компоненты отдельно, щелкнув **Отдельные компоненты > Средства для работы с кодом > Диспетчер пакетов NuGet** в установщике Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eb02e-162">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="eb02e-163">Кроме того, если у вас нет диспетчера пакетов NuGet в Visual Studio 2015 и более ранних версиях, щелкните **Инструменты > Расширения и обновления** и найдите расширение диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="eb02e-163">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="eb02e-164">Если вы не можете использовать установщик расширений в Visual Studio, скачайте расширение отсюда: [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="eb02e-164">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="eb02e-165">Консоль диспетчера пакетов сейчас недоступна в Visual Studio для Mac.</span><span class="sxs-lookup"><span data-stu-id="eb02e-165">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="eb02e-166">Но аналогичные команды доступны через [CLI NuGet](../reference/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="eb02e-166">The equivalent commands, however, are available through the [NuGet CLI](../reference/nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="eb02e-167">В Visual Studio для Mac есть пользовательский интерфейс для управления пакетами NuGet.</span><span class="sxs-lookup"><span data-stu-id="eb02e-167">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="eb02e-168">См. подробнее о [включении пакета NuGet в проект](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="eb02e-168">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="eb02e-169">Консоль диспетчера пакетов не входит в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="eb02e-169">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extend-the-package-manager-console"></a><span data-ttu-id="eb02e-170">Расширение консоли диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="eb02e-170">Extend the Package Manager Console</span></span>

<span data-ttu-id="eb02e-171">Некоторые пакеты устанавливают новые команды для консоли.</span><span class="sxs-lookup"><span data-stu-id="eb02e-171">Some packages install new commands for the console.</span></span> <span data-ttu-id="eb02e-172">Например, `MvcScaffolding` создает команды, например команду `Scaffold` (см. ниже), которая, в свою очередь, создает контроллеры и представления ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="eb02e-172">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Установка и использование MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a><span data-ttu-id="eb02e-174">Настройка профиля PowerShell NuGet</span><span class="sxs-lookup"><span data-stu-id="eb02e-174">Set up a NuGet PowerShell profile</span></span>

<span data-ttu-id="eb02e-175">Профиль PowerShell позволяет сделать часто используемые команды доступными при использовании PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eb02e-175">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="eb02e-176">NuGet поддерживает профиль NuGet, который обычно находится в следующем расположении:</span><span class="sxs-lookup"><span data-stu-id="eb02e-176">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="eb02e-177">Чтобы найти профиль, в консоли введите `$profile`.</span><span class="sxs-lookup"><span data-stu-id="eb02e-177">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="eb02e-178">См. подробнее о [профилях Windows PowerShell](/previous-versions//bb613488(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="eb02e-178">For more details, refer to [Windows PowerShell Profiles](/previous-versions//bb613488(v=vs.85)).</span></span>

## <a name="use-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="eb02e-179">Использование CLI nuget.exe в консоли</span><span class="sxs-lookup"><span data-stu-id="eb02e-179">Use the nuget.exe CLI in the console</span></span>

<span data-ttu-id="eb02e-180">Чтобы добавить [CLI`nuget.exe`](../reference/nuget-exe-cli-reference.md) в консоль диспетчера пакетов, установите пакет [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) из консоли.</span><span class="sxs-lookup"><span data-stu-id="eb02e-180">To make the [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
