---
title: Установка и управление пакетами NuGet, использование консоли в Visual Studio
description: Инструкции по использованию консоли диспетчера пакетов NuGet в Visual Studio для работы с пакетами.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 91ab3859994e5ae738c6637219681ebbfc92d420
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842584"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="00dc3-103">Установка пакетов и управления ими с помощью консоли диспетчера пакетов в Visual Studio (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="00dc3-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="00dc3-104">Консоль диспетчера пакетов NuGet позволяет использовать [команд NuGet PowerShell](../tools/powershell-reference.md) для поиска, установка, удаление и обновление пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="00dc3-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="00dc3-105">С помощью консоли необходим в случаях, когда пользовательский Интерфейс диспетчера пакетов, не позволяют выполнить операцию.</span><span class="sxs-lookup"><span data-stu-id="00dc3-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="00dc3-106">Чтобы использовать `nuget.exe` команд интерфейса командной строки в консоли, см. в разделе [с помощью интерфейса командной строки nuget.exe в консоли](#using-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="00dc3-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="00dc3-107">Консоль встроена в Visual Studio в Windows.</span><span class="sxs-lookup"><span data-stu-id="00dc3-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="00dc3-108">Это не входит в состав Visual Studio для Mac или Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="00dc3-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="00dc3-109">Найти и установить пакет</span><span class="sxs-lookup"><span data-stu-id="00dc3-109">Find and install a package</span></span>

<span data-ttu-id="00dc3-110">Например поиск и установка пакета выполняется с помощью трех простых действий:</span><span class="sxs-lookup"><span data-stu-id="00dc3-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="00dc3-111">Откройте проект или решение в Visual Studio и откройте консоль, используя **Сервис > Диспетчер пакетов NuGet > консоль диспетчера пакетов** команды.</span><span class="sxs-lookup"><span data-stu-id="00dc3-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="00dc3-112">Найти пакет, который вы хотите установить.</span><span class="sxs-lookup"><span data-stu-id="00dc3-112">Find the package you want to install.</span></span> <span data-ttu-id="00dc3-113">Если вы уже знаете это, перейдите к шагу 3.</span><span class="sxs-lookup"><span data-stu-id="00dc3-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="00dc3-114">Выполните команды установки:</span><span class="sxs-lookup"><span data-stu-id="00dc3-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="00dc3-115">Все операции, которые доступны в консоли может также выполняться с помощью [интерфейса командной строки NuGet](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="00dc3-115">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="00dc3-116">Тем не менее консольные команды работают в контексте Visual Studio и сохраненные решения или проекта и часто выполнять больше, чем их эквивалентные команды интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="00dc3-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="00dc3-117">Например установка пакета через консоль добавляет ссылку в проект не поддерживает команду CLI.</span><span class="sxs-lookup"><span data-stu-id="00dc3-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="00dc3-118">По этой причине разработчики, работы в Visual Studio, обычно предпочитают использовать консоль для интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="00dc3-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="00dc3-119">Многие операции консоли зависит от наличия открыт в Visual Studio с использованием известных пути решения.</span><span class="sxs-lookup"><span data-stu-id="00dc3-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="00dc3-120">Если у вас есть несохраненное решение или решение отсутствует, может появится сообщение об ошибке, «решение не открывается или не сохраняется.</span><span class="sxs-lookup"><span data-stu-id="00dc3-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="00dc3-121">Убедитесь, что у вас есть решение открытым и сохраняется.»</span><span class="sxs-lookup"><span data-stu-id="00dc3-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="00dc3-122">Это означает, что консоль не может определить папку решения.</span><span class="sxs-lookup"><span data-stu-id="00dc3-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="00dc3-123">Сохранение несохраненное решение, или создать и сохранить решение, если у вас его открыть, следует исправить эту ошибку.</span><span class="sxs-lookup"><span data-stu-id="00dc3-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="00dc3-124">Открытие консоли и консоли управления</span><span class="sxs-lookup"><span data-stu-id="00dc3-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="00dc3-125">Откройте консоль в Visual Studio с помощью **Сервис > Диспетчер пакетов NuGet > консоль диспетчера пакетов** команды.</span><span class="sxs-lookup"><span data-stu-id="00dc3-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="00dc3-126">Консоль — это окно Visual Studio, в котором могут быть упорядочены и расположение, своему усмотрению (см. в разделе [Настройка макетов окон в Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="00dc3-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="00dc3-127">По умолчанию команды консоли работают от источника пакета и проекта задаваемое в элементе управления в верхней части окна:</span><span class="sxs-lookup"><span data-stu-id="00dc3-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Элементы управления консоли диспетчера пакетов для источника пакета и проекта](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="00dc3-129">При выборе другой пакет источника или проекта меняется эти значения по умолчанию для последующих команд.</span><span class="sxs-lookup"><span data-stu-id="00dc3-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="00dc3-130">Чтобы переопределен с помощью этих параметров, не изменяя значения по умолчанию, большинство команд поддерживают `-Source` и `-ProjectName` параметры.</span><span class="sxs-lookup"><span data-stu-id="00dc3-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="00dc3-131">Чтобы управлять источники пакетов, щелкните значок шестеренки.</span><span class="sxs-lookup"><span data-stu-id="00dc3-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="00dc3-132">Это ярлык для **Сервис > Параметры > Диспетчер пакетов NuGet > источники пакетов** диалоговое окно, как описано в разделе [пользовательский Интерфейс диспетчера пакетов](package-manager-ui.md#package-sources) страницы.</span><span class="sxs-lookup"><span data-stu-id="00dc3-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="00dc3-133">Кроме того элемент управления справа от Выбор проекта очищает содержимое консоли:</span><span class="sxs-lookup"><span data-stu-id="00dc3-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Параметры консоли диспетчера пакетов и очистить элементы управления](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="00dc3-135">Самую верхнюю кнопку прерывает долго выполняющуюся команду.</span><span class="sxs-lookup"><span data-stu-id="00dc3-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="00dc3-136">Например, на котором работают `Get-Package -ListAvailable -PageSize 500` перечислены первые 500 пакетов на источник по умолчанию (например, nuget.org), которая может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="00dc3-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Остановка управления консоли диспетчера пакетов](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="00dc3-138">Установка пакета</span><span class="sxs-lookup"><span data-stu-id="00dc3-138">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="00dc3-139">См. в разделе [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="00dc3-139">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="00dc3-140">Установка пакета в консоли выполняет те же действия, как описано в разделе [что происходит при установке пакета](../concepts/package-installation-process.md), со следующими дополнениями:</span><span class="sxs-lookup"><span data-stu-id="00dc3-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="00dc3-141">В консоли отображаются применимых условиях лицензии в своем окне неявные соглашения.</span><span class="sxs-lookup"><span data-stu-id="00dc3-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="00dc3-142">Если вы не согласны с условиями, следует удалить пакет немедленно.</span><span class="sxs-lookup"><span data-stu-id="00dc3-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="00dc3-143">Также добавляется к файлу проекта ссылку на пакет и отображается в **обозревателе решений** под **ссылки** узла, необходимо сохранить проект, чтобы увидеть изменения в файл проекта напрямую.</span><span class="sxs-lookup"><span data-stu-id="00dc3-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="00dc3-144">Удаление пакета</span><span class="sxs-lookup"><span data-stu-id="00dc3-144">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="00dc3-145">См. в разделе [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="00dc3-145">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="00dc3-146">Используйте [Get-Package](../tools/ps-ref-get-package.md) чтобы видеть все пакеты, установленные в проекте по умолчанию, если вам нужно найти идентификатор.</span><span class="sxs-lookup"><span data-stu-id="00dc3-146">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="00dc3-147">Удаление пакета выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="00dc3-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="00dc3-148">Удаляет ссылки на пакет из проекта (и любого привычного формата управления он используется).</span><span class="sxs-lookup"><span data-stu-id="00dc3-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="00dc3-149">Ссылки, больше не отображаются в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="00dc3-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="00dc3-150">(Может потребоваться перестроить проект, чтобы просмотреть его удалить **Bin** папки.)</span><span class="sxs-lookup"><span data-stu-id="00dc3-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="00dc3-151">Отменяет все изменения, внесенные в `app.config` или `web.config` во время установки пакета.</span><span class="sxs-lookup"><span data-stu-id="00dc3-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="00dc3-152">Удаляет ранее установленные зависимостей, если нет оставшиеся пакеты используют эти зависимости.</span><span class="sxs-lookup"><span data-stu-id="00dc3-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="00dc3-153">Обновление пакета</span><span class="sxs-lookup"><span data-stu-id="00dc3-153">Updating a package</span></span>

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

<span data-ttu-id="00dc3-154">См. в разделе [Get-Package](../tools/ps-ref-get-package.md) и [Update-Package](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="00dc3-154">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="00dc3-155">Поиск пакета</span><span class="sxs-lookup"><span data-stu-id="00dc3-155">Finding a package</span></span>

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

<span data-ttu-id="00dc3-156">См. в разделе [Find-Package](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="00dc3-156">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="00dc3-157">В Visual Studio 2013 и более ранних версий, используйте [Get-Package](../tools/ps-ref-get-package.md) вместо этого.</span><span class="sxs-lookup"><span data-stu-id="00dc3-157">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="00dc3-158">Доступность консоли</span><span class="sxs-lookup"><span data-stu-id="00dc3-158">Availability of the console</span></span>

<span data-ttu-id="00dc3-159">Начиная с Visual Studio 2017, NuGet и диспетчер пакетов NuGet автоматически устанавливаются при выборе любого. Рабочим нагрузкам, связанным с NET; Можно также установить его по отдельности, установив **отдельные компоненты > средства кода > Диспетчер пакетов NuGet** параметр в установщике Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="00dc3-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="00dc3-160">Кроме того, если вы пропустили диспетчер пакетов NuGet в Visual Studio 2015 и более ранних версий, проверьте **Сервис > расширения и обновления...**  и выполните поиск расширение диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="00dc3-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="00dc3-161">Если вы не удается использовать установщик расширений в Visual Studio, можно загрузить модуль непосредственно из [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="00dc3-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="00dc3-162">Консоль диспетчера пакетов недоступен в настоящее время с помощью Visual Studio для Mac.</span><span class="sxs-lookup"><span data-stu-id="00dc3-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="00dc3-163">Эквивалентные команды, тем не менее, доступны через [интерфейса командной строки NuGet](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="00dc3-163">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="00dc3-164">Visual Studio для Mac имеют пользовательский Интерфейс для управления пакетами NuGet.</span><span class="sxs-lookup"><span data-stu-id="00dc3-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="00dc3-165">См. в разделе [Включение пакета NuGet в проекте](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="00dc3-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="00dc3-166">Консоль диспетчера пакетов не входит в состав Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="00dc3-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="00dc3-167">Расширение консоли диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="00dc3-167">Extending the Package Manager Console</span></span>

<span data-ttu-id="00dc3-168">Некоторые пакеты устанавливают новые команды для консоли.</span><span class="sxs-lookup"><span data-stu-id="00dc3-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="00dc3-169">Например `MvcScaffolding` создает команд, таких как `Scaffold` показано ниже, служащего для контроллеров и представлений ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="00dc3-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Установка и использование MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="00dc3-171">Настройка профиля NuGet PowerShell</span><span class="sxs-lookup"><span data-stu-id="00dc3-171">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="00dc3-172">Профиль PowerShell позволяет сделать доступными часто используемые команды при любом использовании PowerShell.</span><span class="sxs-lookup"><span data-stu-id="00dc3-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="00dc3-173">NuGet поддерживает NuGet отдельный профиль, как правило, находятся в следующем расположении:</span><span class="sxs-lookup"><span data-stu-id="00dc3-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="00dc3-174">Чтобы найти профиль, введите `$profile` в консоли:</span><span class="sxs-lookup"><span data-stu-id="00dc3-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="00dc3-175">Дополнительные сведения см. в [профили Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="00dc3-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="00dc3-176">Используя интерфейс командной строки nuget.exe в консоли</span><span class="sxs-lookup"><span data-stu-id="00dc3-176">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="00dc3-177">Чтобы сделать [ `nuget.exe` CLI](nuget-exe-cli-reference.md) доступны в консоли диспетчера пакетов, установите [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) пакета из консоли:</span><span class="sxs-lookup"><span data-stu-id="00dc3-177">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
