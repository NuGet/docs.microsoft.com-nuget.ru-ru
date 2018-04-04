---
title: Миграция с package.config в форматы PackageReference | Документы Microsoft
author: karann-msft
ms.author: karann
manager: unniravindranathan
ms.date: 03/27/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Сведения о миграции проекта из формата управления package.config PackageReference с поддержкой NuGet 4.0 + и VS2017 и .NET Core 2.0
keywords: NuGet migrator миграции, пакет ссылки, проект packages.config файлы PackageReference, VS2017, Visual Studio 2017 г., NuGet 4, .NET Core 2.0
ms.reviewer:
- karann
- unnir
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 10bd2fe95a6af11806a7edd7a43eaa497486fd80
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/03/2018
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="081c3-104">Миграция с packages.config на PackageReference</span><span class="sxs-lookup"><span data-stu-id="081c3-104">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="081c3-105">Visual Studio 2017 г. версия 15,7 предварительной версии 3 и более поздние версии поддерживают при переносе проекта из [packages.config](./packages-config.md) формат управления [PackageReference](../consume-packages/Package-References-in-Project-Files.md) формат.</span><span class="sxs-lookup"><span data-stu-id="081c3-105">Visual Studio 2017 Version 15.7 Preview 3 and later supports migrating a project from the [packages.config](./packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="081c3-106">Преимущества использования PackageReference</span><span class="sxs-lookup"><span data-stu-id="081c3-106">Benefits of using PackageReference</span></span>

* <span data-ttu-id="081c3-107">**Управление всех зависимостей проекта в одном месте**: так же, как ссылки проекта на проект и ссылки на сборки, ссылается на пакет NuGet (с помощью `PackageReference` узла) управляются непосредственно в файлах проекта, а не использовать отдельный файл Packages.config.</span><span class="sxs-lookup"><span data-stu-id="081c3-107">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="081c3-108">**Загромождать представление верхнего уровня зависимостей**: в отличие от packages.config, PackageReference список пакетов NuGet, непосредственно установленные в проекте.</span><span class="sxs-lookup"><span data-stu-id="081c3-108">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="081c3-109">В результате пользовательский Интерфейс диспетчера пакетов NuGet и файл проекта не загроможденными при наличии множества зависимостей низкого уровня.</span><span class="sxs-lookup"><span data-stu-id="081c3-109">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="081c3-110">**Повышение производительности**: при использовании PackageReference, пакеты сохраняются в *глобального пакеты* папку (как описано в статье [управление глобального пакетами и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md) а не в `packages` папки в рамках решения.</span><span class="sxs-lookup"><span data-stu-id="081c3-110">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="081c3-111">В результате PackageReference выполняется быстрее и требует меньше места на диске.</span><span class="sxs-lookup"><span data-stu-id="081c3-111">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="081c3-112">**Точный контроль над зависимости, так и поток содержимого**: с помощью существующих функций MSBuild позволяет [условно ссылаются на пакет NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) и выберите пакет будет ссылаться на целевой платформы, конфигурации, платформы или других аспектов.</span><span class="sxs-lookup"><span data-stu-id="081c3-112">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="081c3-113">**PackageReference находится в активной разработке**: в разделе [PackageReference выдает на GitHub](https://aka.ms/nuget-pr-improvements).</span><span class="sxs-lookup"><span data-stu-id="081c3-113">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="081c3-114">Packages.config больше не находится в активной разработке.</span><span class="sxs-lookup"><span data-stu-id="081c3-114">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="081c3-115">Ограничения</span><span class="sxs-lookup"><span data-stu-id="081c3-115">Limitations</span></span>

* <span data-ttu-id="081c3-116">NuGet PackageReference не доступны в Visual Studio 2015 и более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="081c3-116">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="081c3-117">Перенесенные проекты можно открыть только в Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="081c3-117">Migrated projects can be opened only in Visual Studio 2017.</span></span>
* <span data-ttu-id="081c3-118">Миграция не выполняется в настоящее время доступны для проектов C++ и ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="081c3-118">Migration is not currently available for C++ and ASP.NET project.</span></span>
* <span data-ttu-id="081c3-119">Возможно, некоторые пакеты не полностью совместим с PackageReference.</span><span class="sxs-lookup"><span data-stu-id="081c3-119">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="081c3-120">Дополнительные сведения см. в разделе [проблемы совместимости пакетов](#package-compatibility-issues).</span><span class="sxs-lookup"><span data-stu-id="081c3-120">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

## <a name="migration-steps"></a><span data-ttu-id="081c3-121">Действия миграции</span><span class="sxs-lookup"><span data-stu-id="081c3-121">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="081c3-122">Перед началом миграции, Visual Studio создает резервную копию проекта, чтобы можно было [выполните откат до packages.config](#how-to-roll-back-to-packagesconfig) при необходимости.</span><span class="sxs-lookup"><span data-stu-id="081c3-122">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="081c3-123">Откройте решение, содержащее проект с помощью `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="081c3-123">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="081c3-124">В **обозревателе решений**, щелкните правой кнопкой мыши **ссылки** узел или `packages.config` файла и выберите **перенести packages.config PackageReference...** .</span><span class="sxs-lookup"><span data-stu-id="081c3-124">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="081c3-125">Migrator анализирует ссылки на пакет NuGet для проекта и предпринимается попытка классифицировать их в **верхнего уровня зависимости** (NuGet пакетов этот каталог вы установили) и **транзитивное зависимости**(пакетов, которые были установлены в качестве зависимости пакетов верхнего уровня).</span><span class="sxs-lookup"><span data-stu-id="081c3-125">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directory) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="081c3-126">PackageReference поддерживает восстановление транзитивное пакета и разрешает зависимости динамически, это означает, что транзитивное зависимости не требуется установка явным образом.</span><span class="sxs-lookup"><span data-stu-id="081c3-126">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="081c3-127">(Необязательно) Вы можете обрабатывать пакет NuGet, которые классифицируются как транзитивное зависимостей как зависимость верхнего уровня, выбрав **верхнего уровня** параметр для пакета.</span><span class="sxs-lookup"><span data-stu-id="081c3-127">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="081c3-128">Этот параметр автоматически принимает значение пакеты, содержащие ресурсы, которые не проходят транзитивно (в `build`, `buildCrossTargeting`, `contentFiles`, или `analyzers` папок) и тех, помеченные как зависимость разработки (`developmentDependency = "true"`).</span><span class="sxs-lookup"><span data-stu-id="081c3-128">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="081c3-129">Просмотреть все [проблемы совместимости пакетов](#package-compatibility-issues).</span><span class="sxs-lookup"><span data-stu-id="081c3-129">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="081c3-130">Выберите **ОК** начать миграцию.</span><span class="sxs-lookup"><span data-stu-id="081c3-130">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="081c3-131">В конце миграции Visual Studio предоставляет отчет с путем резервного копирования, список установленных пакетов (верхнего уровня зависимости), список пакетов в ссылках как транзитивное зависимости и список проблем совместимости, описанных в начале Миграция.</span><span class="sxs-lookup"><span data-stu-id="081c3-131">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="081c3-132">Отчет сохраняется в папку резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="081c3-132">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="081c3-133">Проверьте, сборка и запуск решения.</span><span class="sxs-lookup"><span data-stu-id="081c3-133">Validate that the solution builds and runs.</span></span> <span data-ttu-id="081c3-134">Если возникли проблемы, [файлов проблемы на GitHub](https://github.com/NuGet/Home/issues/).</span><span class="sxs-lookup"><span data-stu-id="081c3-134">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="081c3-135">Как откатить к packages.config</span><span class="sxs-lookup"><span data-stu-id="081c3-135">How to roll back to packages.config</span></span>

1. <span data-ttu-id="081c3-136">Закройте перенесенного проекта.</span><span class="sxs-lookup"><span data-stu-id="081c3-136">Close the migrated project.</span></span>

1. <span data-ttu-id="081c3-137">Скопируйте файл проекта и `packages.config` из резервной копии (обычно `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) в папку проекта.</span><span class="sxs-lookup"><span data-stu-id="081c3-137">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span>

1. <span data-ttu-id="081c3-138">Откройте проект.</span><span class="sxs-lookup"><span data-stu-id="081c3-138">Open the project.</span></span>

1. <span data-ttu-id="081c3-139">Откройте консоль диспетчера пакетов с помощью **Сервис > Диспетчер пакетов NuGet > консоль диспетчера пакетов** команду меню.</span><span class="sxs-lookup"><span data-stu-id="081c3-139">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="081c3-140">В консоли выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="081c3-140">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a><span data-ttu-id="081c3-141">Проблемы совместимости пакета</span><span class="sxs-lookup"><span data-stu-id="081c3-141">Package compatibility issues</span></span>

<span data-ttu-id="081c3-142">Некоторые аспекты, которые поддерживались в файле packages.config в PackageReference не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="081c3-142">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="081c3-143">Migrator анализирует и обнаруживает такие проблемы.</span><span class="sxs-lookup"><span data-stu-id="081c3-143">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="081c3-144">Любой пакет, имеет один или несколько из следующих проблем могут работать не так, как ожидалось после миграции.</span><span class="sxs-lookup"><span data-stu-id="081c3-144">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="081c3-145">сценарии «install.ps1» учитываются при установке пакета после миграции</span><span class="sxs-lookup"><span data-stu-id="081c3-145">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="081c3-146">**Описание**</span><span class="sxs-lookup"><span data-stu-id="081c3-146">**Description**</span></span> | <span data-ttu-id="081c3-147">С PackageReference install.ps1 и uninstall.ps1 скрипты PowerShell не выполняются при установке или удалении пакета.</span><span class="sxs-lookup"><span data-stu-id="081c3-147">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="081c3-148">**Потенциальное воздействие**</span><span class="sxs-lookup"><span data-stu-id="081c3-148">**Potential impact**</span></span> | <span data-ttu-id="081c3-149">Пакеты, которые зависят от эти сценарии, чтобы настроить поведение некоторых в проекте назначения может не работать должным образом.</span><span class="sxs-lookup"><span data-stu-id="081c3-149">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="081c3-150">активы «content» недоступны при установке пакета после миграции</span><span class="sxs-lookup"><span data-stu-id="081c3-150">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="081c3-151">**Описание**</span><span class="sxs-lookup"><span data-stu-id="081c3-151">**Description**</span></span> | <span data-ttu-id="081c3-152">Ресурсы в пакете `content` папки с PackageReference не поддерживаются и пропускаются.</span><span class="sxs-lookup"><span data-stu-id="081c3-152">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="081c3-153">PackageReference добавляет поддержку `contentFiles` лучшей транзитивное поддержки и общего содержимого.</span><span class="sxs-lookup"><span data-stu-id="081c3-153">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="081c3-154">**Потенциальное воздействие**</span><span class="sxs-lookup"><span data-stu-id="081c3-154">**Potential impact**</span></span> | <span data-ttu-id="081c3-155">Ресурсы в `content` не копируются в проект и проект кода, который зависит от наличия этих средств требуется рефакторинга.</span><span class="sxs-lookup"><span data-stu-id="081c3-155">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="081c3-156">XDT преобразования не применяются при установке пакета после обновления</span><span class="sxs-lookup"><span data-stu-id="081c3-156">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="081c3-157">**Описание**</span><span class="sxs-lookup"><span data-stu-id="081c3-157">**Description**</span></span> | <span data-ttu-id="081c3-158">XDT преобразования не поддерживаются с PackageReference и `.xdt` файлы пропускаются при установке или удалении пакета.</span><span class="sxs-lookup"><span data-stu-id="081c3-158">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="081c3-159">**Потенциальное воздействие**</span><span class="sxs-lookup"><span data-stu-id="081c3-159">**Potential impact**</span></span> | <span data-ttu-id="081c3-160">XDT преобразования не применяются к XML-файлы в любой проект, наиболее часто `web.config.install.xdt` и `web.config.uninstall.xdt`, означающее проекта` web.config` файл не обновляется при установке или удалении пакета.</span><span class="sxs-lookup"><span data-stu-id="081c3-160">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="081c3-161">Сборки в корне lib учитываются при установке пакета после миграции</span><span class="sxs-lookup"><span data-stu-id="081c3-161">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="081c3-162">**Описание**</span><span class="sxs-lookup"><span data-stu-id="081c3-162">**Description**</span></span> | <span data-ttu-id="081c3-163">Используя PackageReference, представить сборок в корне `lib` папку без целевого определенные вложенные папки платформы учитываются.</span><span class="sxs-lookup"><span data-stu-id="081c3-163">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="081c3-164">NuGet ищет вложенной папки, соответствующие target framework моникером соответствующий целевой платформы проекта и устанавливает соответствующие сборки в проект.</span><span class="sxs-lookup"><span data-stu-id="081c3-164">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="081c3-165">**Потенциальное воздействие**</span><span class="sxs-lookup"><span data-stu-id="081c3-165">**Potential impact**</span></span> | <span data-ttu-id="081c3-166">Пакеты, которые не имеют вложенную папку сопоставления target framework моникером соответствующий целевой платформы проекта может не работать, как ожидалось после перехода или сбой установки во время миграции</span><span class="sxs-lookup"><span data-stu-id="081c3-166">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="081c3-167">Обнаружена проблема?</span><span class="sxs-lookup"><span data-stu-id="081c3-167">Found an issue?</span></span> <span data-ttu-id="081c3-168">Сообщите об этом!</span><span class="sxs-lookup"><span data-stu-id="081c3-168">Report it!</span></span>

<span data-ttu-id="081c3-169">Если возникли проблемы с взаимодействием миграции [файл проблему в репозитории NuGet GitHub](https://github.com/NuGet/Home/issues/).</span><span class="sxs-lookup"><span data-stu-id="081c3-169">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
