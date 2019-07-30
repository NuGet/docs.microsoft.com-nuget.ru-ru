---
title: Управление пакетами NuGet с использованием CLI nuget.exe
description: Инструкции по использованию CLI nuget.exe для работы с пакетами NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 9eefed6f2c1a362f27c4a5d33d07645d743379fa
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317748"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="ef387-103">Управление пакетами с использованием CLI nuget.exe</span><span class="sxs-lookup"><span data-stu-id="ef387-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="ef387-104">С помощью средства CLI вы можете легко восстанавливать пакеты NuGet в проектах и решениях.</span><span class="sxs-lookup"><span data-stu-id="ef387-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="ef387-105">Это средство обеспечивает все функциональные возможности NuGet в Windows и большинство функций, выполняемых в рамках проекта Mono на компьютере Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="ef387-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="ef387-106">Средство CLI `nuget.exe` предназначено для работы с проектом .NET Framework и проектами не на основе пакетов SDK (например, для проектов, нацеленных на библиотеки .NET Standard).</span><span class="sxs-lookup"><span data-stu-id="ef387-106">The `nuget.exe` CLI is for your .NET Framework project and non-SDK-style projects (for example, a non-SDK style project that targets .NET Standard libraries).</span></span> <span data-ttu-id="ef387-107">Если вы используете проект не на основе пакета SDK, который перенесен в `PackageReference`, используйте CLI `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="ef387-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the `dotnet` CLI instead.</span></span> <span data-ttu-id="ef387-108">Чтобы указывать ссылки на пакеты, в CLI `nuget.exe` используется файл [packages.config](../reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="ef387-108">The `nuget.exe` CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="ef387-109">В большинстве сценариев рекомендуется [переносить проекты не на основе пакетов SDK](../reference/migrate-packages-config-to-package-reference.md), в которых используется файл `packages.config`, в PackageReference. В таких случаях можно использовать CLI `dotnet` вместо CLI `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="ef387-109">In most scenarios, we recommend [migrating non-SDK-style projects](../reference/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the `dotnet` CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="ef387-110">На данный момент не поддерживается миграция для проектов C++ и ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ef387-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="ef387-111">В этой статье описываются общие принципы использования некоторых распространенных команд CLI `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="ef387-111">This article shows you basic usage for a few of the most common `nuget.exe` CLI commands.</span></span> <span data-ttu-id="ef387-112">Для большинства из этих команд средство CLI ищет файл проекта в текущем каталоге, кроме случаев, когда файл проекта задан в самой команде.</span><span class="sxs-lookup"><span data-stu-id="ef387-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="ef387-113">Полный список доступных команд и аргументов см. в статье [Справочник по интерфейсу командной строки nuget.exe](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="ef387-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef387-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ef387-114">Prerequisites</span></span>

- <span data-ttu-id="ef387-115">Установите интерфейс командной строки `nuget.exe`, скачав его на сайте [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), и сохраните этот файл `.exe` в подходящую папку. Добавьте эту папку в переменную среды PATH.</span><span class="sxs-lookup"><span data-stu-id="ef387-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="ef387-116">Установка пакета</span><span class="sxs-lookup"><span data-stu-id="ef387-116">Install a package</span></span>

<span data-ttu-id="ef387-117">Команда [install](../reference/cli-reference/cli-ref-install.md) позволяет скачать и установить пакет в проект с использованием заданных источников пакетов. По умолчанию для этого используется текущая папка.</span><span class="sxs-lookup"><span data-stu-id="ef387-117">The [install](../reference/cli-reference/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="ef387-118">Установите новые пакеты в папку *packages* в корневом каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="ef387-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef387-119">Команда `install` не вносит изменения в файл проекта или файл *packages.config*. В этом она похожа на команду `restore`, которая также только добавляет пакеты на диск, не изменяя при этом зависимые компоненты проекта.</span><span class="sxs-lookup"><span data-stu-id="ef387-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="ef387-120">Чтобы добавить зависимый компонент, добавьте пакет с помощью пользовательского интерфейса диспетчера пакетов или консоли в Visual Studio, либо измените файл *packages.config* и затем выполните команду `install` или `restore`.</span><span class="sxs-lookup"><span data-stu-id="ef387-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="ef387-121">Откройте командную строку и перейдите в каталог, в котором находится файл проекта.</span><span class="sxs-lookup"><span data-stu-id="ef387-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="ef387-122">Выполните следующую команду для установки пакета NuGet в папку *packages*.</span><span class="sxs-lookup"><span data-stu-id="ef387-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="ef387-123">Например, чтобы установить пакет `Newtonsoft.json` в папку *packages*, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ef387-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="ef387-124">Также вы можете использовать следующую команду, чтобы установить пакет NuGet с помощью существующего файла `packages.config` в папку *packages*.</span><span class="sxs-lookup"><span data-stu-id="ef387-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="ef387-125">При этом пакет устанавливается локально и не добавляется в список зависимых компонентов проекта.</span><span class="sxs-lookup"><span data-stu-id="ef387-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="ef387-126">Установка определенной версии пакета</span><span class="sxs-lookup"><span data-stu-id="ef387-126">Install a specific version of a package</span></span>

<span data-ttu-id="ef387-127">Если при использовании команды [install](../reference/cli-reference/cli-ref-install.md) версия пакета не указана, NuGet установит его последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="ef387-127">If the version is not specified when you use the [install](../reference/cli-reference/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="ef387-128">Вы также можете установить определенную версию пакета Nuget.</span><span class="sxs-lookup"><span data-stu-id="ef387-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="ef387-129">Например, чтобы добавить версию 12.0.1 пакета `Newtonsoft.json`, воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="ef387-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="ef387-130">Дополнительные сведения об ограничениях и поведении команды `install` см. в статье [Установка пакета](#install-a-package).</span><span class="sxs-lookup"><span data-stu-id="ef387-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="ef387-131">Удаление пакета</span><span class="sxs-lookup"><span data-stu-id="ef387-131">Remove a package</span></span>

<span data-ttu-id="ef387-132">Если возникает необходимость, пакеты следует удалять из папки *packages*.</span><span class="sxs-lookup"><span data-stu-id="ef387-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="ef387-133">Чтобы переустановить пакеты, используйте команды `restore` или `install`.</span><span class="sxs-lookup"><span data-stu-id="ef387-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="ef387-134">Вывод списка пакетов</span><span class="sxs-lookup"><span data-stu-id="ef387-134">List packages</span></span>

<span data-ttu-id="ef387-135">Чтобы просмотреть список пакетов из заданного источника, выполните команду [list](../reference/cli-reference/cli-ref-list.md).</span><span class="sxs-lookup"><span data-stu-id="ef387-135">You can display a list of packages from a given source using the [list](../reference/cli-reference/cli-ref-list.md) command.</span></span> <span data-ttu-id="ef387-136">Чтобы ограничить область поиска, используйте параметр `-Source`.</span><span class="sxs-lookup"><span data-stu-id="ef387-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="ef387-137">Например, можно вывести список пакетов в папке *packages*.</span><span class="sxs-lookup"><span data-stu-id="ef387-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="ef387-138">Если вы указываете условие поиска, в результаты будут включены названия пакетов, теги и описания пакетов.</span><span class="sxs-lookup"><span data-stu-id="ef387-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="ef387-139">Обновление отдельного пакета</span><span class="sxs-lookup"><span data-stu-id="ef387-139">Update an individual package</span></span>

<span data-ttu-id="ef387-140">При выполнении команды `install` NuGet устанавливает последнюю версию пакета, кроме случаев, когда версия задается с помощью соответствующего параметра.</span><span class="sxs-lookup"><span data-stu-id="ef387-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="ef387-141">Обновление всех пакетов</span><span class="sxs-lookup"><span data-stu-id="ef387-141">Update all packages</span></span>

<span data-ttu-id="ef387-142">Чтобы обновить все пакеты, воспользуйтесь командой [update](../reference/cli-reference/cli-ref-update.md).</span><span class="sxs-lookup"><span data-stu-id="ef387-142">Use the [update](../reference/cli-reference/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="ef387-143">При этом все пакеты в проекте, использующем файл `packages.config`, обновляются до последней доступной версии.</span><span class="sxs-lookup"><span data-stu-id="ef387-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="ef387-144">Рекомендуется выполнить команду `restore` перед использованием команды `update`.</span><span class="sxs-lookup"><span data-stu-id="ef387-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="ef387-145">Восстановление пакетов</span><span class="sxs-lookup"><span data-stu-id="ef387-145">Restore packages</span></span>

<span data-ttu-id="ef387-146">Используйте команду [restore](../reference/cli-reference/cli-ref-restore.md), которая скачивает и устанавливает любые отсутствующие пакеты из папки *packages*.</span><span class="sxs-lookup"><span data-stu-id="ef387-146">Use the [restore](../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="ef387-147">Команда `restore` добавляет пакеты на диск, но не изменяет список зависимых компонентов проекта.</span><span class="sxs-lookup"><span data-stu-id="ef387-147">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="ef387-148">Чтобы восстановить зависимые компоненты пакета, измените файл `packages.config` и затем выполните команду `restore`.</span><span class="sxs-lookup"><span data-stu-id="ef387-148">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="ef387-149">Как и с другими командами CLI `nuget.exe`, откройте командную строку и перейдите к каталогу, в котором находится файл проекта.</span><span class="sxs-lookup"><span data-stu-id="ef387-149">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="ef387-150">Восстановление пакета с помощью `restore`.</span><span class="sxs-lookup"><span data-stu-id="ef387-150">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```