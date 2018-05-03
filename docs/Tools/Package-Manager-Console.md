---
title: Руководство по консоли диспетчера пакетов NuGet
description: Инструкции по использованию консоли диспетчера пакетов NuGet в Visual Studio для работы с пакетами.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 64912f0dc32a492d9c23a02f45b4303c69faf340
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="package-manager-console"></a><span data-ttu-id="013cf-103">Консоль диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="013cf-103">Package Manager Console</span></span>

<span data-ttu-id="013cf-104">Консоль диспетчера пакетов NuGet встроены в Visual Studio в Windows 2012 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="013cf-104">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="013cf-105">(Это не входят в состав Visual Studio для Mac или кода Visual Studio.)</span><span class="sxs-lookup"><span data-stu-id="013cf-105">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="013cf-106">Консоль дает возможность использовать [команд NuGet PowerShell](../tools/powershell-reference.md) для поиска, установки, удаления и обновить пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="013cf-106">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="013cf-107">С помощью консоли требуется в случаях, где пользовательский Интерфейс диспетчера пакетов не обеспечивает способ выполнения операции.</span><span class="sxs-lookup"><span data-stu-id="013cf-107">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="013cf-108">Для использования `nuget.exe` команд в консоли в разделе [nuget.exe CLI в консоли с помощью](#using-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="013cf-108">To use `nuget.exe` commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="013cf-109">Например поиск и установка пакета выполняется с 3 простых шага:</span><span class="sxs-lookup"><span data-stu-id="013cf-109">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="013cf-110">Откройте проект или решение в Visual Studio, чтобы открыть консоль, используя **Сервис > Диспетчер пакетов NuGet > консоль диспетчера пакетов** команды.</span><span class="sxs-lookup"><span data-stu-id="013cf-110">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="013cf-111">Найти пакет, который вы хотите установить.</span><span class="sxs-lookup"><span data-stu-id="013cf-111">Find the package you want to install.</span></span> <span data-ttu-id="013cf-112">Если вы уже знаете это, перейдите к шагу 3.</span><span class="sxs-lookup"><span data-stu-id="013cf-112">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="013cf-113">Выполните команду установки:</span><span class="sxs-lookup"><span data-stu-id="013cf-113">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="013cf-114">Все операции, которые доступны в консоли можно также с [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="013cf-114">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="013cf-115">Однако команды консоли работать в контексте Visual Studio и сохраненное решение или проект и часто выполнять больше, чем их эквивалентные команды CLI.</span><span class="sxs-lookup"><span data-stu-id="013cf-115">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="013cf-116">Например установка пакета через консоль добавляет ссылку на проект, тогда как команду CLI не делает.</span><span class="sxs-lookup"><span data-stu-id="013cf-116">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="013cf-117">По этой причине разработчики, работающие в Visual Studio обычно используется консоль, чтобы CLI.</span><span class="sxs-lookup"><span data-stu-id="013cf-117">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="013cf-118">Многие операции в консоли зависит от наличия решение открывается в Visual Studio с именем известному пути.</span><span class="sxs-lookup"><span data-stu-id="013cf-118">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="013cf-119">Если у вас есть несохраненное решение или ни одно решение, можно увидеть ошибку, «решение не открыто или не сохранено.</span><span class="sxs-lookup"><span data-stu-id="013cf-119">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="013cf-120">Убедитесь, что вы уже открыли и сохранили решение.»</span><span class="sxs-lookup"><span data-stu-id="013cf-120">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="013cf-121">Это означает, что консоль невозможно определить папку решения.</span><span class="sxs-lookup"><span data-stu-id="013cf-121">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="013cf-122">Сохранение несохраненное решение, или создание и сохранение решения в том случае, если у вас нет открыт, необходимо исправить ошибку.</span><span class="sxs-lookup"><span data-stu-id="013cf-122">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="013cf-123">Открытие консоли и консоли управления</span><span class="sxs-lookup"><span data-stu-id="013cf-123">Opening the console and console controls</span></span>

1. <span data-ttu-id="013cf-124">Откройте консоль в Visual Studio с помощью **Сервис > Диспетчер пакетов NuGet > консоль диспетчера пакетов** команды.</span><span class="sxs-lookup"><span data-stu-id="013cf-124">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="013cf-125">Консоль — это окно Visual Studio, в котором упорядочены и располагается, однако вам нравится (см. [Настройка макетов окон в Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="013cf-125">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="013cf-126">По умолчанию команды консоли работают от исходного пакета и проекта как набор в элементе управления в верхней части окна:</span><span class="sxs-lookup"><span data-stu-id="013cf-126">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Консоль диспетчера пакетов управления для источника пакета и проекта](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="013cf-128">При выборе источника другой пакет или проект изменения этих значений по умолчанию для последующих команд.</span><span class="sxs-lookup"><span data-stu-id="013cf-128">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="013cf-129">Переопределен эти параметры, не меняя значений по умолчанию, большинство команд поддержки `-Source` и `-ProjectName` параметры.</span><span class="sxs-lookup"><span data-stu-id="013cf-129">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="013cf-130">Чтобы управлять источников пакетов, щелкните значок шестеренки.</span><span class="sxs-lookup"><span data-stu-id="013cf-130">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="013cf-131">Ярлык для **Сервис > Параметры > Диспетчер пакетов NuGet > источники пакетов** диалоговое окно «», как описано в статье [пользовательского интерфейса диспетчера пакетов](package-manager-ui.md#package-sources) страницы.</span><span class="sxs-lookup"><span data-stu-id="013cf-131">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="013cf-132">Кроме того элемент управления справа от проекта селектор очищает содержимое консоли:</span><span class="sxs-lookup"><span data-stu-id="013cf-132">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Параметры консоли диспетчера пакетов и очистить элементы управления](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="013cf-134">Самую верхнюю кнопку прерывает долго выполняющуюся команду.</span><span class="sxs-lookup"><span data-stu-id="013cf-134">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="013cf-135">Например, на котором работают `Get-Package -ListAvailable -PageSize 500` перечисляет первые 500 пакетов на источник по умолчанию (например nuget.org), которая может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="013cf-135">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Остановка управления консоли диспетчера пакетов](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="013cf-137">Установка пакета</span><span class="sxs-lookup"><span data-stu-id="013cf-137">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="013cf-138">В разделе [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="013cf-138">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="013cf-139">Установка пакета в консоли выполняет те же действия, как описано в статье [что происходит при установке пакета](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), с учетом следующих отличий:</span><span class="sxs-lookup"><span data-stu-id="013cf-139">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), with the following additions:</span></span>

- <span data-ttu-id="013cf-140">В консоли отображаются применимые условия лицензионных соглашений в своем окне неявные соглашения.</span><span class="sxs-lookup"><span data-stu-id="013cf-140">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="013cf-141">Если вы не согласны с условиями, следует удалить пакет немедленно.</span><span class="sxs-lookup"><span data-stu-id="013cf-141">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="013cf-142">Также ссылку на пакет добавляется в файл проекта и отображается в **обозревателе решений** под **ссылки** узла, необходимо сохранить проект, чтобы увидеть изменения в файл проекта напрямую.</span><span class="sxs-lookup"><span data-stu-id="013cf-142">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="013cf-143">Удаление пакета</span><span class="sxs-lookup"><span data-stu-id="013cf-143">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="013cf-144">В разделе [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="013cf-144">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="013cf-145">Используйте [Get-Package](../tools/ps-ref-get-package.md) чтобы видеть все пакеты, установленные в проекте по умолчанию, если требуется найти идентификатор.</span><span class="sxs-lookup"><span data-stu-id="013cf-145">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="013cf-146">При удалении пакет выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="013cf-146">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="013cf-147">Удаляет ссылки на пакет из проекта (и формату управления он используется).</span><span class="sxs-lookup"><span data-stu-id="013cf-147">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="013cf-148">Ссылки больше не отображались в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="013cf-148">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="013cf-149">(Может потребоваться перестроить проект, чтобы увидеть его удалить **Bin** папки.)</span><span class="sxs-lookup"><span data-stu-id="013cf-149">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="013cf-150">Отменяет все изменения, внесенные в `app.config` или `web.config` во время установки пакета.</span><span class="sxs-lookup"><span data-stu-id="013cf-150">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="013cf-151">Удаляет ранее установленные зависимости, если нет оставшиеся пакеты используют эти зависимости.</span><span class="sxs-lookup"><span data-stu-id="013cf-151">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="013cf-152">Обновление пакета</span><span class="sxs-lookup"><span data-stu-id="013cf-152">Updating a package</span></span>

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

<span data-ttu-id="013cf-153">В разделе [Get-Package](../tools/ps-ref-get-package.md) и [пакета обновления](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="013cf-153">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="013cf-154">Поиск пакета</span><span class="sxs-lookup"><span data-stu-id="013cf-154">Finding a package</span></span>

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

<span data-ttu-id="013cf-155">В разделе [Find-Package](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="013cf-155">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="013cf-156">В Visual Studio 2013 и более ранних версий, используйте [Get-Package](../tools/ps-ref-get-package.md) вместо него.</span><span class="sxs-lookup"><span data-stu-id="013cf-156">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="013cf-157">Доступность консоли</span><span class="sxs-lookup"><span data-stu-id="013cf-157">Availability of the console</span></span>

<span data-ttu-id="013cf-158">В Visual Studio 2017 г NuGet и диспетчер пакетов NuGet устанавливаются автоматически при выборе любого. Рабочие нагрузки, связанные с NET; Можно также установить его по отдельности, проверив **отдельные компоненты > средства кода > Диспетчер пакетов NuGet** в установщике Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="013cf-158">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="013cf-159">Кроме того, если диспетчер пакетов NuGet в Visual Studio 2015 и более ранних версий, что отсутствует, проверьте **Сервис > расширения и обновления...**  и выполните поиск расширение диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="013cf-159">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="013cf-160">Если вы не удается использовать установщик расширения в Visual Studio, можно загрузить модуль непосредственно из [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="013cf-160">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="013cf-161">Консоль диспетчера пакетов недоступна в настоящее время Visual Studio для Mac.</span><span class="sxs-lookup"><span data-stu-id="013cf-161">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="013cf-162">Эквивалентные команды, однако доступны через [NuGet CLI](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="013cf-162">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="013cf-163">Visual Studio для Mac имеет пользовательский Интерфейс для управления пакетами NuGet.</span><span class="sxs-lookup"><span data-stu-id="013cf-163">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="013cf-164">В разделе [пакет NuGet, включая в проекте](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="013cf-164">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="013cf-165">Консоль диспетчера пакетов не включено с кодом Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="013cf-165">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="013cf-166">Расширение консоли диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="013cf-166">Extending the Package Manager Console</span></span>

<span data-ttu-id="013cf-167">Некоторые пакеты установки новых команд консоли.</span><span class="sxs-lookup"><span data-stu-id="013cf-167">Some packages install new commands for the console.</span></span> <span data-ttu-id="013cf-168">Например `MvcScaffolding` создает команды `Scaffold` показано ниже, который приводит к возникновению ошибки ASP.NET MVC контроллеры и представления:</span><span class="sxs-lookup"><span data-stu-id="013cf-168">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Установка и использование MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="013cf-170">Настройка профиля NuGet PowerShell</span><span class="sxs-lookup"><span data-stu-id="013cf-170">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="013cf-171">Профиль PowerShell позволяет сделать доступными часто используемые команды при любом использовании PowerShell.</span><span class="sxs-lookup"><span data-stu-id="013cf-171">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="013cf-172">NuGet поддерживает NuGet отдельный профиль, обычно находятся в следующем расположении:</span><span class="sxs-lookup"><span data-stu-id="013cf-172">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="013cf-173">Чтобы найти профиль, введите `$profile` в консоли:</span><span class="sxs-lookup"><span data-stu-id="013cf-173">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="013cf-174">Дополнительные сведения см. в [профили Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="013cf-174">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="013cf-175">С помощью nuget.exe CLI в консоли</span><span class="sxs-lookup"><span data-stu-id="013cf-175">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="013cf-176">Чтобы сделать [ `nuget.exe` CLI](nuget-exe-cli-reference.md) доступны в консоли диспетчера пакетов установки [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) пакета с помощью консоли:</span><span class="sxs-lookup"><span data-stu-id="013cf-176">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
