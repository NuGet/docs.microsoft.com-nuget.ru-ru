---
title: "Восстановление пакетов NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Описание того, как NuGet восстанавливает пакеты, от которых зависит проект, включая отключение восстановления и ограничения версий."
keywords: "восстановление пакетов NuGet, установка пакетов NuGet, установка пакета, восстановление пакетов, версии зависимостей, отключение автоматического восстановления, ограничение версий пакетов"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4e819a2bb34bbe70f0f11d5adeed82b976a8cb65
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="package-restore"></a><span data-ttu-id="0a1d2-104">Восстановление пакетов</span><span class="sxs-lookup"><span data-stu-id="0a1d2-104">Package Restore</span></span>

<span data-ttu-id="0a1d2-105">Чтобы очистить среду разработки и уменьшить размер репозитория, **функция восстановления пакетов** NuGet устанавливает все указанные в ссылках пакеты перед сборкой проекта.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="0a1d2-106">Эта широко применяемая функция гарантирует доступность всех зависимостей в проекте без необходимости сохранения этих пакетов в системе управления исходным кодом (сведения о том, как настроить репозиторий, чтобы исключить двоичные файлы пакетов, см. в разделе [Пакеты и система управления версиями](../consume-packages/packages-and-source-control.md)).</span><span class="sxs-lookup"><span data-stu-id="0a1d2-106">This widely-used feature ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span>

<span data-ttu-id="0a1d2-107">В этом разделе.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-107">In this topic:</span></span>
- [<span data-ttu-id="0a1d2-108">Краткое руководство по восстановлению пакетов</span><span class="sxs-lookup"><span data-stu-id="0a1d2-108">Quick guide to package restore</span></span>](#quick-guide-to-package-restore)
- [<span data-ttu-id="0a1d2-109">Обзор восстановления пакетов</span><span class="sxs-lookup"><span data-stu-id="0a1d2-109">Package restore overview</span></span>](#package-restore-overview)
- [<span data-ttu-id="0a1d2-110">Включение и отключение восстановления пакетов</span><span class="sxs-lookup"><span data-stu-id="0a1d2-110">Enabling and disabling package restore</span></span>](#enabling-and-disabling-package-restore)
- [<span data-ttu-id="0a1d2-111">Ограничение версий пакетов при восстановлении</span><span class="sxs-lookup"><span data-stu-id="0a1d2-111">Constraining package versions with restore</span></span>](#constraining-package-versions-with-restore)
- <span data-ttu-id="0a1d2-112">[Восстановление из командной строки](#command-line-restore), для всех версий NuGet</span><span class="sxs-lookup"><span data-stu-id="0a1d2-112">[Command-line restore](#command-line-restore), for all versions of NuGet</span></span>
- <span data-ttu-id="0a1d2-113">[Автоматическое восстановление в Visual Studio](#automatic-restore-in-visual-studio), для NuGet 2.7 и более поздних версий</span><span class="sxs-lookup"><span data-stu-id="0a1d2-113">[Automatic restore in Visual Studio](#automatic-restore-in-visual-studio), for NuGet 2.7 and later.</span></span>
- <span data-ttu-id="0a1d2-114">[Встроенное в MSBuild восстановление в Visual Studio](#msbuild-integrated-restore), для NuGet 2.6 и более ранних версий</span><span class="sxs-lookup"><span data-stu-id="0a1d2-114">[MSBuild-integrated restore in Visual Studio](#msbuild-integrated-restore), for NuGet 2.6 and earlier.</span></span>
- [<span data-ttu-id="0a1d2-115">Восстановление пакетов с помощью сборки Team Foundation</span><span class="sxs-lookup"><span data-stu-id="0a1d2-115">Package restore with Team Foundation Build</span></span>](#package-restore-with-team-foundation-build)

<span data-ttu-id="0a1d2-116">Поведение при восстановлении зависит от версии. Чтобы узнать используемую версию NuGet, просто запустите `nuget.exe` в командной строке и посмотрите на первую строку выходных данных.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-116">Restore behavior does vary by version; to check your NuGet version, simply run `nuget.exe` on the command line and look at the first line of output.</span></span>

<span data-ttu-id="0a1d2-117">Дополнительные сведения о восстановлении пакетов на серверах сборки см. в разделе [Восстановление пакетов с помощью TFBuild](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="0a1d2-117">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

> [!Note]
> <span data-ttu-id="0a1d2-118">Проекты, настроенные для восстановления пакетов, работают с xbuild в Mono.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-118">Projects configured for package restore also work with xbuild on Mono.</span></span>

## <a name="quick-guide-to-package-restore"></a><span data-ttu-id="0a1d2-119">Краткое руководство по восстановлению пакетов</span><span class="sxs-lookup"><span data-stu-id="0a1d2-119">Quick guide to package restore</span></span>

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> <span data-ttu-id="0a1d2-120">Если отображается ошибка "Данный проект ссылается на пакеты NuGet, отсутствующие на этом компьютере" или "Необходимо восстановить один или несколько пакетов NuGet, однако это невозможно без вашего согласия", включите автоматическое восстановление, следуя инструкциям в разделе [Включение и отключение восстановления пакетов](#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="0a1d2-120">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="0a1d2-121">Обзор восстановления пакетов</span><span class="sxs-lookup"><span data-stu-id="0a1d2-121">Package restore overview</span></span>

<span data-ttu-id="0a1d2-122">Во-первых, в зависимости от типа проекта и версии NuGet ссылки на пакеты хранятся в одном из указанных ниже форматов управления пакетами.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-122">First, package references are maintained in one of the following package management formats, depending on project type and NuGet version.</span></span> <span data-ttu-id="0a1d2-123">(Обратите внимание, что NuGet 4 и MSBuild 15.1 устанавливаются вместе с Visual Studio 2017.)</span><span class="sxs-lookup"><span data-stu-id="0a1d2-123">(Note that NuGet 4 and MSBuild 15.1 are installed with Visual Studio 2017.)</span></span>

| <span data-ttu-id="0a1d2-124">Метод</span><span class="sxs-lookup"><span data-stu-id="0a1d2-124">Method</span></span> | <span data-ttu-id="0a1d2-125">Версия NuGet</span><span class="sxs-lookup"><span data-stu-id="0a1d2-125">NuGet Version</span></span> | <span data-ttu-id="0a1d2-126">Описание:</span><span class="sxs-lookup"><span data-stu-id="0a1d2-126">Description</span></span> | 
| --- | --- | --- |
| `packages.config` | <span data-ttu-id="0a1d2-127">2.x+</span><span class="sxs-lookup"><span data-stu-id="0a1d2-127">2.x+</span></span> | <span data-ttu-id="0a1d2-128">Указывает полный глубокий набор зависимостей.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-128">Lists the complete deep set of dependencies.</span></span> <span data-ttu-id="0a1d2-129">Пакеты, добавляемые в `packages.config`, также должны добавляться в файл проекта, как и целевые объекты и свойства.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-129">Packages added to `packages.config` must also be added to the project file, and Targets and Props must also be added to the project file.</span></span> <span data-ttu-id="0a1d2-130">Это базовый метод для всех версий NuGet, однако он имеет пониженную производительность по сравнению с другими вариантами.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-130">This is the baseline method for all versions of NuGet, but has slower performance compared with the other options.</span></span> <span data-ttu-id="0a1d2-131">(См. раздел [Схема packages.config](../schema/packages-config.md).)</span><span class="sxs-lookup"><span data-stu-id="0a1d2-131">(See [packages.config schema](../schema/packages-config.md).)</span></span> | 
| `project.json` | <span data-ttu-id="0a1d2-132">3.x+</span><span class="sxs-lookup"><span data-stu-id="0a1d2-132">3.x+</span></span> | <span data-ttu-id="0a1d2-133">Используется по умолчанию только с проектами UWP, но проекты можно преобразовать из `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-133">Used only by default with UWP projects, but projects can be converted from `packages.config`.</span></span> <span data-ttu-id="0a1d2-134">`project.json` указывает только высокоуровневые зависимости.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-134">`project.json` lists only top-level dependencies.</span></span> <span data-ttu-id="0a1d2-135">Ссылки, целевые объекты и свойства добавляются в проект динамически во время сборки, что обеспечивает более высокую производительность по сравнению с `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-135">References, Targets, and Props are added dynamically to the project during build, resulting in better performance compared with `packages.config`.</span></span> <span data-ttu-id="0a1d2-136">(См. раздел [Схема project.json](../schema/project-json.md).)</span><span class="sxs-lookup"><span data-stu-id="0a1d2-136">(See [project.json schema](../schema/project-json.md).)</span></span>|
| <span data-ttu-id="0a1d2-137">PackageReference</span><span class="sxs-lookup"><span data-stu-id="0a1d2-137">PackageReference</span></span> | <span data-ttu-id="0a1d2-138">4.x+</span><span class="sxs-lookup"><span data-stu-id="0a1d2-138">4.x+</span></span> | <span data-ttu-id="0a1d2-139">Указывает зависимости прямо в файле проекта в узле `<PackageReference>` вместе с `<Reference>` и `<ProjectReference>`.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-139">Lists dependencies directly in the project file in the `<PackageReference>` node, alongside `<Reference>` and `<ProjectReference>`.</span></span> <span data-ttu-id="0a1d2-140">Работает аналогично `project.json`; см. раздел [Ссылки на пакеты в файлах проекта](../Consume-Packages/Package-References-in-Project-Files.md).</span><span class="sxs-lookup"><span data-stu-id="0a1d2-140">Works similarly to `project.json`; see [Package references in project files](../Consume-Packages/Package-References-in-Project-Files.md).</span></span> |

<span data-ttu-id="0a1d2-141">Во-вторых, запустить восстановление с помощью списка ссылок можно разными способами:</span><span class="sxs-lookup"><span data-stu-id="0a1d2-141">Second, you start a restore using the reference list in a variety of ways:</span></span>

<span data-ttu-id="0a1d2-142">Из командной строки или [консоли диспетчера пакетов](../tools/Package-Manager-Console.md):</span><span class="sxs-lookup"><span data-stu-id="0a1d2-142">From the command line or [Package Manager Console](../tools/Package-Manager-Console.md):</span></span>

| <span data-ttu-id="0a1d2-143">Команда</span><span class="sxs-lookup"><span data-stu-id="0a1d2-143">Command</span></span> | <span data-ttu-id="0a1d2-144">Применимые сценарии</span><span class="sxs-lookup"><span data-stu-id="0a1d2-144">Applicable scenarios</span></span> |
| --- | --- | 
| `nuget restore` | <span data-ttu-id="0a1d2-145">Все версии NuGet и все типы ссылок.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-145">All versions of NuGet and all reference types.</span></span> <span data-ttu-id="0a1d2-146">См. раздел [Восстановление из командной строки](#command-line-restore) ниже.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-146">See [Command-line restore](#command-line-restore) below.</span></span> | 
| `dotnet restore` | <span data-ttu-id="0a1d2-147">То же, что и `nuget restore`, для проектов .NET Core.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-147">Same as `nuget restore` for .NET Core projects.</span></span> <span data-ttu-id="0a1d2-148">См. раздел [dotnet restore](/dotnet/articles/core/tools/dotnet-restore).</span><span class="sxs-lookup"><span data-stu-id="0a1d2-148">See [dotnet restore](/dotnet/articles/core/tools/dotnet-restore).</span></span> |
| `msbuild /t:restore` | <span data-ttu-id="0a1d2-149">Только Nuget 4.x+ и MSBuild 15.1+ со [ссылками на пакеты в файлах проекта](../Consume-Packages/Package-References-in-Project-Files.md).</span><span class="sxs-lookup"><span data-stu-id="0a1d2-149">Nuget 4.x+ and MSBuild 15.1+ with [package references in project files](../Consume-Packages/Package-References-in-Project-Files.md) only.</span></span> <span data-ttu-id="0a1d2-150">`nuget restore` и `dotnet restore` используют эту команду для подходящих проектов.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-150">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span> <span data-ttu-id="0a1d2-151">См. раздел [Объекты pack и restore NuGet в качестве целевых объектов MSBuild — целевой объект restore](../schema/msbuild-targets.md#restore-target).</span><span class="sxs-lookup"><span data-stu-id="0a1d2-151">See [NuGet pack and restore as MSBuild targets- restore target](../schema/msbuild-targets.md#restore-target).</span></span>|

<span data-ttu-id="0a1d2-152">В разное время среда Visual Studio также восстанавливает пакеты:</span><span class="sxs-lookup"><span data-stu-id="0a1d2-152">Visual Studio itself also restores packages at different times:</span></span>

| <span data-ttu-id="0a1d2-153">Тип</span><span class="sxs-lookup"><span data-stu-id="0a1d2-153">Type</span></span> | <span data-ttu-id="0a1d2-154">Когда происходит восстановление</span><span class="sxs-lookup"><span data-stu-id="0a1d2-154">When restore happens</span></span> |
| --- | --- |
| <span data-ttu-id="0a1d2-155">Восстановление шаблона</span><span class="sxs-lookup"><span data-stu-id="0a1d2-155">Template restore</span></span> | <span data-ttu-id="0a1d2-156">При создании проекта, так как некоторые шаблоны зависят от внешних пакетов.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-156">During creation of a new project, as some templates depend on external packages.</span></span> |
| <span data-ttu-id="0a1d2-157">Восстановление сборки</span><span class="sxs-lookup"><span data-stu-id="0a1d2-157">Build restore</span></span> | <span data-ttu-id="0a1d2-158">На первом шаге сборки.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-158">As the first step of a build.</span></span> |
| <span data-ttu-id="0a1d2-159">Восстановление решения</span><span class="sxs-lookup"><span data-stu-id="0a1d2-159">Solution restore</span></span> | <span data-ttu-id="0a1d2-160">Когда пользователь щелкает правой кнопкой мыши решение и выбирает пункт **Восстановить пакеты NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-160">When user right-clicks a solution and selects **Restore NuGet Packages**.</span></span> |
| <span data-ttu-id="0a1d2-161">Восстановление при изменении проекта</span><span class="sxs-lookup"><span data-stu-id="0a1d2-161">Restore on project change</span></span> | <span data-ttu-id="0a1d2-162">*(Только NuGet 4.x)* Когда используется проект на основе пакета SDK для .NET Core, включая изменение состояния проекта.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-162">*(NuGet 4.x only)* When a .NET Core SDK-based project is used, including when project state changes.</span></span> |

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="0a1d2-163">Включение и отключение восстановления пакетов</span><span class="sxs-lookup"><span data-stu-id="0a1d2-163">Enabling and disabling package restore</span></span>

<span data-ttu-id="0a1d2-164">Восстановление пакетов можно включить в меню **Сервис > Параметры > Диспетчер пакетов NuGet** в Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="0a1d2-164">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![Управление поведением восстановления пакетов с помощью параметров диспетчера пакетов NuGet](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="0a1d2-166">**Разрешить NuGet скачивать отсутствующие пакеты**: определяет все формы восстановления пакетов, изменяя `packageRestore/enabled` в файле `%AppData%\NuGet\NuGet.Config`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-166">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  <span data-ttu-id="0a1d2-167">Параметр `packageRestore/enabled` можно переопределить на глобальном уровне, задав для переменной среды с именем **EnableNuGetPackageRestore** значение TRUE или FALSE перед запуском Visual Studio или началом сборки.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-167">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>
    

- <span data-ttu-id="0a1d2-168">**Автоматически проверять отсутствие пакетов при сборке в Visual Studio**: управляет автоматическим восстановлением для NuGet 2.7 и более поздних версий, изменяя `packageRestore/automatic` в файле `%AppData%\NuGet\NuGet.Config`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-168">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore for NuGet 2.7 and later by changing the `packageRestore/automatic` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>
            
    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

<span data-ttu-id="0a1d2-169">Справочную информацию см. в разделе [Файл конфигурации NuGet — packageRestore](../Schema/nuget-config-file.md#packagerestore-section).</span><span class="sxs-lookup"><span data-stu-id="0a1d2-169">For reference, see the [NuGet config file - packageRestore section](../Schema/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="0a1d2-170">В некоторых случаях разработчику или организации может потребоваться включить или отключить восстановление пакетов на компьютере по умолчанию для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-170">In some cases, a developer or company might want to enable or disable package restore on a machine by default for all users.</span></span> <span data-ttu-id="0a1d2-171">Это можно сделать, добавив указанные выше параметры в файл глобальной конфигурации NuGet, находящийся в `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-171">This can be done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="0a1d2-172">После этого отдельные пользователи могут выборочно включить восстановление на уровне проекта по необходимости.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-172">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="0a1d2-173">Точные сведения о том, как NuGet устанавливает приоритеты для нескольких файлов конфигурации, см. в разделе [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span><span class="sxs-lookup"><span data-stu-id="0a1d2-173">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="0a1d2-174">Ограничение версий пакетов при восстановлении</span><span class="sxs-lookup"><span data-stu-id="0a1d2-174">Constraining package versions with restore</span></span>

<span data-ttu-id="0a1d2-175">Когда NuGet восстанавливает пакеты любым из методов, он учитывает все ограничения, указанные в `packages.config`, `project.json` или файле проекта:</span><span class="sxs-lookup"><span data-stu-id="0a1d2-175">When NuGet restores packages through any method, it will honor any constraints specified in `packages.config`, `project.json`, or the project file:</span></span>

- <span data-ttu-id="0a1d2-176">`packages.config`: укажите диапазон версий в свойстве `allowedVersion` зависимости.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-176">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="0a1d2-177">См. раздел [Повторная установка и обновление пакетов](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="0a1d2-177">See [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="0a1d2-178">Пример:</span><span class="sxs-lookup"><span data-stu-id="0a1d2-178">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="0a1d2-179">`project.json`: укажите диапазон версий непосредственно с номером версии зависимости.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-179">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="0a1d2-180">Пример:</span><span class="sxs-lookup"><span data-stu-id="0a1d2-180">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- <span data-ttu-id="0a1d2-181">Ссылки на пакеты в файлах проекта: укажите диапазон версий непосредственно с номером версии зависимости.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-181">Package references in project files: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="0a1d2-182">Пример:</span><span class="sxs-lookup"><span data-stu-id="0a1d2-182">For example:</span></span>
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

<span data-ttu-id="0a1d2-183">Во всех случаях используйте нотацию, описанную в статье [Управление версиями пакета](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="0a1d2-183">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="command-line-restore"></a><span data-ttu-id="0a1d2-184">Восстановление из командной строки</span><span class="sxs-lookup"><span data-stu-id="0a1d2-184">Command-line restore</span></span>

<span data-ttu-id="0a1d2-185">Для NuGet 2.7 и более поздних версий используйте команду [Восстановить](../tools/cli-ref-restore.md), чтобы восстановить все пакеты в решении (использует ли оно `packages.config`, `project.json` или ссылки на пакеты в файлах проекта).</span><span class="sxs-lookup"><span data-stu-id="0a1d2-185">For NuGet 2.7 and above, use the [Restore](../tools/cli-ref-restore.md) command to restore all packages in a solution (whether it uses `packages.config`, `project.json`, or package references in project files).</span></span> <span data-ttu-id="0a1d2-186">Для заданной папки проекта, например `c:\proj\app`, пакеты восстанавливает каждый из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="0a1d2-186">For a given project folder such as `c:\proj\app`, the common variations below each restore the packages:</span></span>

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

<span data-ttu-id="0a1d2-187">Для NuGet 4.0+ и MSBuild 15.1+ можно также использовать `MSBuild /t:restore`, как описано в разделе [Объекты pack и restore NuGet в качестве целевых объектов MSBuild](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="0a1d2-187">For NuGet 4.0+ and MSBuild 15.1+, you can also use `MSBuild /t:restore` as described on [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="build-time-restore-in-visual-studio"></a><span data-ttu-id="0a1d2-188">Восстановление во время сборки в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0a1d2-188">Build-time restore in Visual Studio</span></span>

<span data-ttu-id="0a1d2-189">Visual Studio автоматически восстанавливает отсутствующие пакеты по умолчанию в начале сборки.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-189">Visual Studio automatically restores missing packages by default at the beginning of a build.</span></span> <span data-ttu-id="0a1d2-190">Это поведение можно изменить, сняв флажок **Сервис > Параметры > Диспетчер пакетов NuGet > Общие > Автоматически проверять отсутствие пакетов при сборке в Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-190">This behavior can be changed by clearing **Tools > Options > NuGet Package Manager > General > Automatically check for missing packages during build in Visual Studio**.</span></span>

<span data-ttu-id="0a1d2-191">Когда автоматическое восстановление включено, оно работает следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0a1d2-191">When enabled, automatic restore works as follows:</span></span>

1. <span data-ttu-id="0a1d2-192">В начале сборки Visual Studio предписывает NuGet восстановить пакеты.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-192">When a build begins, Visual Studio instructs NuGet to restore packages.</span></span>
1. <span data-ttu-id="0a1d2-193">NuGet рекурсивно ищет все файлы `packages.config` в решении, выполняет поиск `project.json`, а также по файлу проекта.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-193">NuGet recursively looks for all `packages.config` files in the solution, looks for `project.json`, or looks in the project file.</span></span>
1. <span data-ttu-id="0a1d2-194">Для каждого из пакетов, указанных в файлах ссылок, NuGet проверяет, существует ли он в решении (в папке `packages`, `project.lock.json` или `project.assets.json` — в зависимости от того, использует ли проект `packages.config`, `project.json` или ссылки на пакеты в файлах проекта).</span><span class="sxs-lookup"><span data-stu-id="0a1d2-194">For each packages listed in the reference files, NuGet checks if it already exists in the solution (the `packages` folder, `project.lock.json`, or `project.assets.json` depending on whether the project is using `packages.config`, `project.json`, or package references in project files).</span></span>
1. <span data-ttu-id="0a1d2-195">Если пакет не найден, NuGet сначала пытается извлечь его из своего кэша (см. раздел [Управление кэшем NuGet](../consume-packages/managing-the-nuget-cache.md)).</span><span class="sxs-lookup"><span data-stu-id="0a1d2-195">If the package is not found, NuGet attempts to retrieve the package from its cache first (see [Managing the NuGet cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="0a1d2-196">Если пакета нет в кэше, NuGet пытается скачать его из включенных источников, как указано в меню **Сервис > Параметры > Диспетчер пакетов NuGet > Источники пакетов**, проверяя их в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-196">If the package is not in the cache, NuGet attempts to download the package from the enabled sources as listed in **Tools > Options > NuGet Package Manager > Package Sources**, in the order that the sources appear.</span></span> <span data-ttu-id="0a1d2-197">В этом случае NuGet не выдает ошибку поиска пакета, пока не проверит все источники, после чего выдает ошибку только для последнего источника в списке.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-197">In this case, NuGet does not indicate a failure to find the package until all the sources have been checked, at which time it reports the failure only for the last source in the list.</span></span> <span data-ttu-id="0a1d2-198">Неявно такая ошибка означает, что пакет отсутствовал и во всех других источниках, хотя отдельные ошибки для них не выдавались.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-198">By implication such an error also means that the package wasn't present on any of the other sources either, even though errors were not shown for those sources individually.</span></span>
1. <span data-ttu-id="0a1d2-199">В случае успешного скачивания NuGet кэширует пакет и устанавливает его в решении (опять же в папку `packages`, `project.lock.json` или `project.assets.json`); в противном случае происходит сбой NuGet и сборка завершается с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-199">If the download is successful, NuGet caches the package and installs it into the solution (again, into either the `packages` folder, `project.lock.json`, or `project.assets.json`); otherwise NuGet fails and the build fails.</span></span>

<span data-ttu-id="0a1d2-200">Во время этого процесса отображается диалоговое окно хода выполнения, где можно отменить восстановление пакетов.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-200">During this process, you see a progress dialog with the option to cancel package restore.</span></span>

## <a name="package-restore-with-team-foundation-build"></a><span data-ttu-id="0a1d2-201">Восстановление пакетов с помощью сборки Team Foundation</span><span class="sxs-lookup"><span data-stu-id="0a1d2-201">Package Restore with Team Foundation Build</span></span>

<span data-ttu-id="0a1d2-202">Восстановление пакетов обычно используется при сборке проектов на серверах сборки, например с помощью Team Foundation Server (TFS) и Visual Studio Team Services (а также других систем сборки, которые здесь не описаны).</span><span class="sxs-lookup"><span data-stu-id="0a1d2-202">Package restore is commonly used when building projects on build servers, as with Team Foundation Server (TFS) and Visual Studio Team Services (as well as other build systems, which are not covered here).</span></span>

### <a name="visual-studio-team-services"></a><span data-ttu-id="0a1d2-203">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="0a1d2-203">Visual Studio Team Services</span></span>

<span data-ttu-id="0a1d2-204">При создании определения сборки в Team Services просто включите в него задачу "Восстановить пакеты NuGet" до любой задачи сборки.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-204">When creating a build definition on Team Services, simply include the Restore NuGet Packages task in the definition before any build task.</span></span> <span data-ttu-id="0a1d2-205">Эта задача по умолчанию входит в несколько шаблонов сборки.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-205">This task is included by default in a number of build templates.</span></span>

![Задача восстановления пакетов NuGet в определении сборки Visual Studio Team Service](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a><span data-ttu-id="0a1d2-207">Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="0a1d2-207">Team Foundation Server</span></span>

<span data-ttu-id="0a1d2-208">В TFS 2013 и более поздних версий пакеты восстанавливаются автоматически по умолчанию во время сборки при условии, что вы используете шаблон командной сборки для Team Foundation Server 2013 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-208">With TFS 2013 and later, packages are automatically restored by default during build, provided that you're using a Team Build Template for Team Foundation Server 2013 or later.</span></span>

<span data-ttu-id="0a1d2-209">Если вы используете предыдущую версию шаблонов сборки (например, в проекте, который был перенесен из более ранних версий TFS), потребуется также выполнить миграцию этих шаблонов сборки в TFS 2013.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-209">If you're using a previous version of build templates (such as in a project that's been migrated from earlier versions of TFS), you'll need to also migrate those build templates to TFS 2013.</span></span> <span data-ttu-id="0a1d2-210">По существу это означает повторное создание пользовательских частей шаблонов сборки с помощью подходящего шаблона для вашей системы управления исходным кодом (TFVC или Git).</span><span class="sxs-lookup"><span data-stu-id="0a1d2-210">This essentially means recreating the custom parts of the Build Templates using the appropriate template for your source control (TFVC or Git).</span></span>

<span data-ttu-id="0a1d2-211">Для более ранней версии TFS можно просто включить шаг сборки, чтобы вызвать [восстановление из командной строки](#command-line-restore), как описано выше.</span><span class="sxs-lookup"><span data-stu-id="0a1d2-211">For earlier version of TFS, you can simply include a build step to invoke [command-line restore](#command-line-restore) as described earlier.</span></span>

<span data-ttu-id="0a1d2-212">Дополнительные сведения см. в разделе [Пошаговое руководство по восстановлению пакетов с помощью сборки Team Foundation](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="0a1d2-212">For more details see then [Walkthrough of Package Restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>    
