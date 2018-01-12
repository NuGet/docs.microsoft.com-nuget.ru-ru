---
title: "Руководство по консоли диспетчера пакетов NuGet | Документы Microsoft"
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2b92b119-6861-406c-82af-9d739af230e4
f1_keywords: vs.nuget.packagemanager.console
description: "Инструкции по использованию консоли диспетчера пакетов NuGet в Visual Studio для работы с пакетами."
keywords: "Консоль диспетчера пакетов NuGet, powershell NuGet, управлять пакетами NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b8f1df23d1a43412868c14e508ee5221d48dcc7c
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/10/2018
---
# <a name="package-manager-console"></a><span data-ttu-id="2d940-104">Консоль диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="2d940-104">Package Manager Console</span></span>

<span data-ttu-id="2d940-105">Консоль диспетчера пакетов NuGet встроены в Visual Studio в Windows 2012 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="2d940-105">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="2d940-106">(Это не входят в состав Visual Studio для Mac или кода Visual Studio.)</span><span class="sxs-lookup"><span data-stu-id="2d940-106">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="2d940-107">Консоль дает возможность использовать [команд NuGet PowerShell](../tools/powershell-reference.md) для поиска, установки, удаления и обновить пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="2d940-107">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="2d940-108">С помощью консоли требуется в случаях, где пользовательский Интерфейс диспетчера пакетов не обеспечивает способ выполнения операции.</span><span class="sxs-lookup"><span data-stu-id="2d940-108">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span>

<span data-ttu-id="2d940-109">Например поиск и установка пакета выполняется с 3 простых шага:</span><span class="sxs-lookup"><span data-stu-id="2d940-109">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="2d940-110">Откройте проект или решение в Visual Studio, чтобы открыть консоль, используя **Сервис > Диспетчер пакетов NuGet > консоль диспетчера пакетов** команды.</span><span class="sxs-lookup"><span data-stu-id="2d940-110">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="2d940-111">Найти пакет, который вы хотите установить.</span><span class="sxs-lookup"><span data-stu-id="2d940-111">Find the package you want to install.</span></span> <span data-ttu-id="2d940-112">Если вы уже знаете это, перейдите к шагу 3.</span><span class="sxs-lookup"><span data-stu-id="2d940-112">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="2d940-113">Выполните команду установки:</span><span class="sxs-lookup"><span data-stu-id="2d940-113">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

<span data-ttu-id="2d940-114">В этом разделе.</span><span class="sxs-lookup"><span data-stu-id="2d940-114">In this topic:</span></span>

- [<span data-ttu-id="2d940-115">Открытие консоли</span><span class="sxs-lookup"><span data-stu-id="2d940-115">Opening the console</span></span>](#opening-the-console-and-console-controls)
- [<span data-ttu-id="2d940-116">Установка пакета</span><span class="sxs-lookup"><span data-stu-id="2d940-116">Installing a package</span></span>](#installing-a-package)
- [<span data-ttu-id="2d940-117">Удаление пакета</span><span class="sxs-lookup"><span data-stu-id="2d940-117">Uninstalling a package</span></span>](#uninstalling-a-package)
- [<span data-ttu-id="2d940-118">Поиск пакета</span><span class="sxs-lookup"><span data-stu-id="2d940-118">Finding a package</span></span>](#finding-a-package)
- [<span data-ttu-id="2d940-119">Обновление пакета</span><span class="sxs-lookup"><span data-stu-id="2d940-119">Updating a package</span></span>](#updating-a-package)
- [<span data-ttu-id="2d940-120">Доступность консоли</span><span class="sxs-lookup"><span data-stu-id="2d940-120">Availability of the console</span></span>](#availability-of-the-console)
- [<span data-ttu-id="2d940-121">Расширение консоли диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="2d940-121">Extending the Package Manager Console</span></span>](#extending-the-package-manager-console)
- [<span data-ttu-id="2d940-122">Настройка профиля NuGet PowerShell</span><span class="sxs-lookup"><span data-stu-id="2d940-122">Setting up a NuGet PowerShell profile</span></span>](#setting-up-a-nuget-powershell-profile)

> [!Important]
> <span data-ttu-id="2d940-123">Все операции, которые доступны в консоли можно также с [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="2d940-123">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="2d940-124">Однако команды консоли работать в контексте Visual Studio и сохраненное решение или проект и часто выполнять больше, чем их эквивалентные команды CLI.</span><span class="sxs-lookup"><span data-stu-id="2d940-124">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="2d940-125">Например установка пакета через консоль добавляет ссылку на проект, тогда как команду CLI не делает.</span><span class="sxs-lookup"><span data-stu-id="2d940-125">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="2d940-126">По этой причине разработчики, работающие в Visual Studio обычно используется консоль, чтобы CLI.</span><span class="sxs-lookup"><span data-stu-id="2d940-126">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="2d940-127">Многие операции в консоли зависит от наличия решение открывается в Visual Studio с именем известному пути.</span><span class="sxs-lookup"><span data-stu-id="2d940-127">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="2d940-128">Если у вас есть несохраненное решение или ни одно решение, можно увидеть ошибку, «решение не открыто или не сохранено.</span><span class="sxs-lookup"><span data-stu-id="2d940-128">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="2d940-129">Убедитесь, что вы уже открыли и сохранили решение.»</span><span class="sxs-lookup"><span data-stu-id="2d940-129">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="2d940-130">Это означает, что консоль невозможно определить папку решения.</span><span class="sxs-lookup"><span data-stu-id="2d940-130">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="2d940-131">Сохранение несохраненное решение, или создание и сохранение решения в том случае, если у вас нет открыт, необходимо исправить ошибку.</span><span class="sxs-lookup"><span data-stu-id="2d940-131">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="2d940-132">Открытие консоли и консоли управления</span><span class="sxs-lookup"><span data-stu-id="2d940-132">Opening the console and console controls</span></span>

1. <span data-ttu-id="2d940-133">Откройте консоль в Visual Studio с помощью **Сервис > Диспетчер пакетов NuGet > консоль диспетчера пакетов** команды.</span><span class="sxs-lookup"><span data-stu-id="2d940-133">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="2d940-134">Консоль — это окно Visual Studio, в котором упорядочены и располагается, однако вам нравится (см. [Настройка макетов окон в Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="2d940-134">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="2d940-135">По умолчанию команды консоли работают от исходного пакета и проекта как набор в элементе управления в верхней части окна:</span><span class="sxs-lookup"><span data-stu-id="2d940-135">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Консоль диспетчера пакетов управления для источника пакета и проекта](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="2d940-137">При выборе источника другой пакет или проект изменения этих значений по умолчанию для последующих команд.</span><span class="sxs-lookup"><span data-stu-id="2d940-137">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="2d940-138">Переопределен эти параметры, не меняя значений по умолчанию, большинство команд поддержки `-Source` и `-ProjectName` параметры.</span><span class="sxs-lookup"><span data-stu-id="2d940-138">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="2d940-139">Чтобы управлять источников пакетов, щелкните значок шестеренки.</span><span class="sxs-lookup"><span data-stu-id="2d940-139">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="2d940-140">Ярлык для **Сервис > Параметры > Диспетчер пакетов NuGet > источники пакетов** диалоговое окно «», как описано в статье [пользовательского интерфейса диспетчера пакетов](Package-Manager-UI.md#package-sources) страницы.</span><span class="sxs-lookup"><span data-stu-id="2d940-140">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](Package-Manager-UI.md#package-sources) page.</span></span> <span data-ttu-id="2d940-141">Кроме того элемент управления справа от проекта селектор очищает содержимое консоли:</span><span class="sxs-lookup"><span data-stu-id="2d940-141">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Параметры консоли диспетчера пакетов и очистить элементы управления](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="2d940-143">Самую верхнюю кнопку прерывает долго выполняющуюся команду.</span><span class="sxs-lookup"><span data-stu-id="2d940-143">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="2d940-144">Например, на котором работают `Get-Package -ListAvailable -PageSize 500` перечисляет первые 500 пакетов на источник по умолчанию (например nuget.org), которая может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2d940-144">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Остановка управления консоли диспетчера пакетов](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="2d940-146">Установка пакета</span><span class="sxs-lookup"><span data-stu-id="2d940-146">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="2d940-147">В разделе [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="2d940-147">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="2d940-148">Установка пакета выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2d940-148">Installing a package performs the following actions:</span></span>

- <span data-ttu-id="2d940-149">Отображает применимые условия лицензионных соглашений в окне консоли с неявные соглашения.</span><span class="sxs-lookup"><span data-stu-id="2d940-149">Displays applicable license terms in the console window with implied agreement.</span></span> <span data-ttu-id="2d940-150">Если вы не согласны с условиями, следует удалить пакет немедленно.</span><span class="sxs-lookup"><span data-stu-id="2d940-150">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="2d940-151">Добавляет ссылку на проект в любой формат ссылки уже используется.</span><span class="sxs-lookup"><span data-stu-id="2d940-151">Adds a reference to the project in whatever reference format is in use.</span></span> <span data-ttu-id="2d940-152">В обозревателе решений и в нем применяется ссылка впоследствии отображаются ссылки.</span><span class="sxs-lookup"><span data-stu-id="2d940-152">References subsequently appear in Solution Explorer and the applicable reference format file.</span></span> <span data-ttu-id="2d940-153">Обратите внимание, что с PackageReference, необходимо сохранить проект, чтобы увидеть изменения в файл проекта напрямую.</span><span class="sxs-lookup"><span data-stu-id="2d940-153">Note, however, that with PackageReference, you need to save the project to see the changes in the project file directly.</span></span>
- <span data-ttu-id="2d940-154">Кэширует пакета:</span><span class="sxs-lookup"><span data-stu-id="2d940-154">Caches the package:</span></span>
    - <span data-ttu-id="2d940-155">PackageReference: пакет кэшируется в `%USERPROFILE%\.nuget\packages` и блокировки файлов, т. е. `project.assets.json` обновляется.</span><span class="sxs-lookup"><span data-stu-id="2d940-155">PackageReference:  package is cached at `%USERPROFILE%\.nuget\packages` and the lock file i.e. `project.assets.json` is updated.</span></span>
    - <span data-ttu-id="2d940-156">`packages.config`: создает `packages` перейдите в папку корень решения и копирует файлы пакетов в подпапку внутри него.</span><span class="sxs-lookup"><span data-stu-id="2d940-156">`packages.config`: creates a `packages` folder at the solution root and copies the package files into a subfolder within it.</span></span> <span data-ttu-id="2d940-157">`package.config` Обновить файл.</span><span class="sxs-lookup"><span data-stu-id="2d940-157">The `package.config` file is updated.</span></span>
- <span data-ttu-id="2d940-158">Обновления `app.config` и/или `web.config` Если пакет использует [источника и конфигурации файла преобразования](../create-packages/source-and-config-file-transformations.md).</span><span class="sxs-lookup"><span data-stu-id="2d940-158">Updates `app.config` and/or `web.config` if the package uses [source and config file transformations](../create-packages/source-and-config-file-transformations.md).</span></span>
- <span data-ttu-id="2d940-159">Устанавливает все зависимости, если он уже имеется в проекте.</span><span class="sxs-lookup"><span data-stu-id="2d940-159">Installs any dependencies if not already present in the project.</span></span> <span data-ttu-id="2d940-160">Это обновление версий пакета в процессе, как описано в [разрешении зависимостей](../consume-packages/dependency-resolution.md).</span><span class="sxs-lookup"><span data-stu-id="2d940-160">This might update package versions in the process, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span>
- <span data-ttu-id="2d940-161">Отображает файл readme пакета, если он доступен в окне Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d940-161">Displays the package's readme file, if available, in a Visual Studio window.</span></span>

> [!Tip]
> <span data-ttu-id="2d940-162">Одно из главных преимуществ установки пакетов с `Install-Package` является команды в консоли, добавляет ссылку на проект, как если бы вы использовали пользовательский Интерфейс диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="2d940-162">One of the primary advantages of installing packages with the `Install-Package` command in the console is that adds a reference to the project just as if you used the Package Manager UI.</span></span> <span data-ttu-id="2d940-163">Напротив `nuget install` команду CLI загружает пакет и автоматически не добавляются ссылки.</span><span class="sxs-lookup"><span data-stu-id="2d940-163">In contrast, the `nuget install` CLI command only downloads the package and does not automatically add a reference.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="2d940-164">Удаление пакета</span><span class="sxs-lookup"><span data-stu-id="2d940-164">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="2d940-165">В разделе [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="2d940-165">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="2d940-166">Используйте [Get-Package](../tools/ps-ref-get-package.md) чтобы видеть все пакеты, установленные в проекте по умолчанию, если требуется найти идентификатор.</span><span class="sxs-lookup"><span data-stu-id="2d940-166">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="2d940-167">При удалении пакет выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2d940-167">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="2d940-168">Удаляет ссылки на пакет из проекта (и используется формат ссылки на любые).</span><span class="sxs-lookup"><span data-stu-id="2d940-168">Removes references to the package from the project (and whatever reference format is in use).</span></span> <span data-ttu-id="2d940-169">Ссылки больше не отображаются в обозревателе решений.</span><span class="sxs-lookup"><span data-stu-id="2d940-169">References no longer appear in Solution Explorer.</span></span> <span data-ttu-id="2d940-170">(Может потребоваться перестроить проект, чтобы увидеть его удалить **Bin** папки.)</span><span class="sxs-lookup"><span data-stu-id="2d940-170">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="2d940-171">Отменяет все изменения, внесенные в `app.config` или `web.config` во время установки пакета.</span><span class="sxs-lookup"><span data-stu-id="2d940-171">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="2d940-172">Удаляет ранее установленные зависимости, если нет оставшиеся пакеты используют эти зависимости.</span><span class="sxs-lookup"><span data-stu-id="2d940-172">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

> [!Tip]
> <span data-ttu-id="2d940-173">Как `Install-Package`, `Uninstall-Package` команда имеет преимущество управление ссылками в проекте, в отличие от `nuget uninstall` команду CLI.</span><span class="sxs-lookup"><span data-stu-id="2d940-173">Like `Install-Package`, the `Uninstall-Package` command has the benefit of managing references in the project, unlike the `nuget uninstall` CLI command.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="2d940-174">Обновление пакета</span><span class="sxs-lookup"><span data-stu-id="2d940-174">Updating a package</span></span>

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

<span data-ttu-id="2d940-175">В разделе [Get-Package](../tools/ps-ref-get-package.md) и [пакета обновления](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="2d940-175">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="2d940-176">Поиск пакета</span><span class="sxs-lookup"><span data-stu-id="2d940-176">Finding a package</span></span>

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

<span data-ttu-id="2d940-177">В разделе [Find-Package](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="2d940-177">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="2d940-178">В Visual Studio 2013 и более ранних версий, используйте [Get-Package](../tools/ps-ref-get-package.md) вместо него.</span><span class="sxs-lookup"><span data-stu-id="2d940-178">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="2d940-179">Доступность консоли</span><span class="sxs-lookup"><span data-stu-id="2d940-179">Availability of the console</span></span>

<span data-ttu-id="2d940-180">В Visual Studio 2017 г NuGet и диспетчер пакетов NuGet устанавливаются автоматически при выборе любого. Рабочие нагрузки, связанные с NET; Можно также установить его по отдельности, проверив **отдельные компоненты > средства кода > Диспетчер пакетов NuGet** в установщике Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="2d940-180">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="2d940-181">Кроме того, если диспетчер пакетов NuGet в Visual Studio 2015 и более ранних версий, что отсутствует, проверьте **Сервис > расширения и обновления...**  и выполните поиск расширение диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="2d940-181">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="2d940-182">Если вы не удается использовать установщик расширения в Visual Studio, можно загрузить модуль непосредственно из [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="2d940-182">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="2d940-183">Консоль диспетчера пакетов недоступна в настоящее время Visual Studio для Mac.</span><span class="sxs-lookup"><span data-stu-id="2d940-183">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="2d940-184">Эквивалентные команды, однако доступны через [NuGet CLI](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="2d940-184">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="2d940-185">Visual Studio для Mac имеет пользовательский Интерфейс для управления пакетами NuGet.</span><span class="sxs-lookup"><span data-stu-id="2d940-185">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="2d940-186">В разделе [пакет NuGet, включая в проекте](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="2d940-186">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="2d940-187">Консоль диспетчера пакетов не включено с кодом Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d940-187">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="2d940-188">Расширение консоли диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="2d940-188">Extending the Package Manager Console</span></span>

<span data-ttu-id="2d940-189">Некоторые пакеты установки новых команд консоли.</span><span class="sxs-lookup"><span data-stu-id="2d940-189">Some packages install new commands for the console.</span></span> <span data-ttu-id="2d940-190">Например `MvcScaffolding` создает команды `Scaffold` показано ниже, который приводит к возникновению ошибки ASP.NET MVC контроллеры и представления:</span><span class="sxs-lookup"><span data-stu-id="2d940-190">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Установка и использование MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="2d940-192">Настройка профиля PowerShell NuGet</span><span class="sxs-lookup"><span data-stu-id="2d940-192">Setting up a NuGet PowerShell Profile</span></span>

<span data-ttu-id="2d940-193">Профиль PowerShell позволяет сделать доступными часто используемые команды при любом использовании PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2d940-193">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="2d940-194">NuGet поддерживает NuGet отдельный профиль, обычно находятся в следующем расположении:</span><span class="sxs-lookup"><span data-stu-id="2d940-194">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

```
%UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="2d940-195">Чтобы найти профиль, введите `$profile` в консоли:</span><span class="sxs-lookup"><span data-stu-id="2d940-195">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="2d940-196">Дополнительные сведения см. в [профили Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="2d940-196">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>
