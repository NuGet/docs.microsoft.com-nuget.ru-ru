---
title: Устарелый формат project.json NuGet
description: Различные части содержимого с project.json удалены из других разделов документации по NuGet.
author: karann-msft
ms.author: karann
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: aa5cd1a2f3e3a6707a9d68204306db85651b0a18
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545204"
---
# <a name="projectjson-archive"></a><span data-ttu-id="4fba7-103">Устарелый формат project.json</span><span class="sxs-lookup"><span data-stu-id="4fba7-103">project.json archive</span></span>

<span data-ttu-id="4fba7-104">Формат управления `project.json` впервые появился в NuGet версии 3.x и использовался с определенными типами проектов.</span><span class="sxs-lookup"><span data-stu-id="4fba7-104">The `project.json` management format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="4fba7-105">Он был объявлен устаревшим с появлением формата PackageReference, в котором зависимости перечислены непосредственно в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="4fba7-105">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="4fba7-106">См. также:</span><span class="sxs-lookup"><span data-stu-id="4fba7-106">Also see:</span></span>

- [<span data-ttu-id="4fba7-107">Справочник по файлу project.json</span><span class="sxs-lookup"><span data-stu-id="4fba7-107">project.json schema</span></span>](project-json.md)
- <span data-ttu-id="4fba7-108">[Impact of project.json when creating packages](project-json-impact.md) (Влияние project.json при создании пакетов)</span><span class="sxs-lookup"><span data-stu-id="4fba7-108">[project.json impact on package authors](project-json-impact.md)</span></span>
- [<span data-ttu-id="4fba7-109">project.json и универсальная платформа Windows</span><span class="sxs-lookup"><span data-stu-id="4fba7-109">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a><span data-ttu-id="4fba7-110">Формат управления project.json</span><span class="sxs-lookup"><span data-stu-id="4fba7-110">project.json management format</span></span>

<span data-ttu-id="4fba7-111">*Полное описание см. в статье о [восстановлении пакетов](../what-is-nuget.md).*</span><span class="sxs-lookup"><span data-stu-id="4fba7-111">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="4fba7-112">В списке форматов управления:</span><span class="sxs-lookup"><span data-stu-id="4fba7-112">In the list of management formats:</span></span>

- <span data-ttu-id="4fba7-113">[`project.json`](project-json.md): *(объявлен устаревшим)* JSON-файл, содержащий список зависимостей проекта, при этом общая схема пакета приведена в связанном файле `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="4fba7-113">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="4fba7-114">Этот формат объявлен устаревшим в связи с появлением PackageReference.</span><span class="sxs-lookup"><span data-stu-id="4fba7-114">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="4fba7-115">Восстановление NuGet в Mono</span><span class="sxs-lookup"><span data-stu-id="4fba7-115">nuget restore on Mono</span></span>

<span data-ttu-id="4fba7-116">*Полное описание см. в статье об [установке клиентских средств NuGet](../install-nuget-client-tools.md).*</span><span class="sxs-lookup"><span data-stu-id="4fba7-116">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="4fba7-117">Работает с `project.json`.</span><span class="sxs-lookup"><span data-stu-id="4fba7-117">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="4fba7-118">Ограничение версий пакетов при восстановлении</span><span class="sxs-lookup"><span data-stu-id="4fba7-118">Constraining package versions with restore</span></span>

<span data-ttu-id="4fba7-119">*Полное описание см. в статье о [восстановлении пакетов](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span><span class="sxs-lookup"><span data-stu-id="4fba7-119">*Originally in [Package restore](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span></span>

- <span data-ttu-id="4fba7-120">`project.json`: укажите диапазон версий непосредственно с номером версии зависимости.</span><span class="sxs-lookup"><span data-stu-id="4fba7-120">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="4fba7-121">Пример:</span><span class="sxs-lookup"><span data-stu-id="4fba7-121">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="4fba7-122">Команды интерфейса командной строки NuGet</span><span class="sxs-lookup"><span data-stu-id="4fba7-122">NuGet CLI commands</span></span>

- <span data-ttu-id="4fba7-123">`nuget install` не работает с `project.json`.</span><span class="sxs-lookup"><span data-stu-id="4fba7-123">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="4fba7-124">`nuget restore`: при применении в проектах, использующих `project.json`, создается файл `project.lock.json` и (если необходимо) `<project>.nuget.props`.</span><span class="sxs-lookup"><span data-stu-id="4fba7-124">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="4fba7-125">(Оба эти файла можно опустить в системе управления версиями.) Аргумент `<projectPath>` может указывать на файл `project.json`. При этом поведение аналогично, как при указании на файл `packages.config` или файл проекта.</span><span class="sxs-lookup"><span data-stu-id="4fba7-125">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="4fba7-126">В порядке приоритета для папок пакета перед использованием `project.json` выполняется поиск в `%userprofile%\.nuget\packages`.</span><span class="sxs-lookup"><span data-stu-id="4fba7-126">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="4fba7-127">`nuget update`: в Mono эта команда не работает с проектами, использующими `project.json`.</span><span class="sxs-lookup"><span data-stu-id="4fba7-127">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="4fba7-128">Разрешение зависимостей при использовании PackageReference</span><span class="sxs-lookup"><span data-stu-id="4fba7-128">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="4fba7-129">*Полное описание см. в разделе о [разрешении зависимостей](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span><span class="sxs-lookup"><span data-stu-id="4fba7-129">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="4fba7-130">Поведение PackageReference также применяется к файлу `project.json`.</span><span class="sxs-lookup"><span data-stu-id="4fba7-130">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="4fba7-131">Команда восстановления NuGet записывает схему зависимостей в файл с именем `project.lock.json`, а также `project.json`.</span><span class="sxs-lookup"><span data-stu-id="4fba7-131">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="4fba7-132">Управление ресурсами зависимостей</span><span class="sxs-lookup"><span data-stu-id="4fba7-132">Managing dependency assets</span></span>

<span data-ttu-id="4fba7-133">*Полное описание см. в разделе о [разрешении зависимостей](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span><span class="sxs-lookup"><span data-stu-id="4fba7-133">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="4fba7-134">При использовании формата `project.json` вы можете управлять тем, какие ресурсы из зависимостей переходят в проект верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="4fba7-134">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="4fba7-135">Дополнительные сведения см. в [справочнике по файлу project.json](project-json.md).</span><span class="sxs-lookup"><span data-stu-id="4fba7-135">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="4fba7-136">Исключение ссылок</span><span class="sxs-lookup"><span data-stu-id="4fba7-136">Excluding references</span></span>

<span data-ttu-id="4fba7-137">*Полное описание см. в разделе о [разрешении зависимостей](../consume-packages/dependency-resolution.md#excluding-references).*</span><span class="sxs-lookup"><span data-stu-id="4fba7-137">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="4fba7-138">`project.json`: добавьте `"exclude" : "all"` в зависимость для пакета PackageC:</span><span class="sxs-lookup"><span data-stu-id="4fba7-138">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="4fba7-139">Устранение ошибок с несовместимостью пакетов</span><span class="sxs-lookup"><span data-stu-id="4fba7-139">Resolving incompatible package errors</span></span>

<span data-ttu-id="4fba7-140">*Полное описание см. в разделе о [разрешении зависимостей](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span><span class="sxs-lookup"><span data-stu-id="4fba7-140">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="4fba7-141">Добавленный метод устранения ошибок:</span><span class="sxs-lookup"><span data-stu-id="4fba7-141">An added means of resolving errors:</span></span>

- <span data-ttu-id="4fba7-142">**Не рекомендуется**: в качестве временной меры, пока вы сотрудничаете с автором пакетов, проекты, ориентированные на `netcore`, `netstandard` и `netcoreapp`, могут обозначать другие платформы как совместимые, тем самым позволяя использовать пакеты, ориентированные на эти платформы.</span><span class="sxs-lookup"><span data-stu-id="4fba7-142">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="4fba7-143">См. разделы [Оператор imports в project.json](project-json.md#imports) и [Целевой объект restore MSBuild в PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span><span class="sxs-lookup"><span data-stu-id="4fba7-143">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="4fba7-144">Это может привести к непредвиденному поведению, поэтому повторим, что лучше всего устранить проблемы совместимости путем сотрудничества с автором пакетов.</span><span class="sxs-lookup"><span data-stu-id="4fba7-144">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="4fba7-145">Требуемые версии .NET Framework</span><span class="sxs-lookup"><span data-stu-id="4fba7-145">Target frameworks</span></span>

<span data-ttu-id="4fba7-146">*Полное описание см. в статье о [требуемых версиях .NET Framework](../reference/target-frameworks.md).*</span><span class="sxs-lookup"><span data-stu-id="4fba7-146">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="4fba7-147">[project.json](project-json.md). Узел `frameworks` задает версии платформы, для которых может быть скомпилирован пакет.</span><span class="sxs-lookup"><span data-stu-id="4fba7-147">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="4fba7-148">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="4fba7-148">Creating a package</span></span>

<span data-ttu-id="4fba7-149">*Полное описание см. в статье о [создании пакета](../create-packages/creating-a-package.md).*</span><span class="sxs-lookup"><span data-stu-id="4fba7-149">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="4fba7-150">Указание типа пакета</span><span class="sxs-lookup"><span data-stu-id="4fba7-150">Setting a package type</span></span>

<span data-ttu-id="4fba7-151">С .NET Core 1.x при установке пакета DotnetCliTool среда Visual Studio помещает его в узел `project.json` `tools`, а не `dependencies`.</span><span class="sxs-lookup"><span data-stu-id="4fba7-151">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="4fba7-152">Типы пакетов заданы в файле `project.json`.</span><span class="sxs-lookup"><span data-stu-id="4fba7-152">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="4fba7-153">`project.json`: укажите тип пакета в свойстве `packOptions.packageType` файла JSON:</span><span class="sxs-lookup"><span data-stu-id="4fba7-153">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="4fba7-154">Добавление целевых объектов и свойств MSBuild</span><span class="sxs-lookup"><span data-stu-id="4fba7-154">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="4fba7-155">*Полное описание см. в статье о [создании пакетов NuGet для платформы .NET Standard с помощью Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span><span class="sxs-lookup"><span data-stu-id="4fba7-155">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="4fba7-156">При использовании `project.json` целевые платформы не добавляются в проект, а предоставляются через файл `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="4fba7-156">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="4fba7-157">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="4fba7-157">Package versioning</span></span>

<span data-ttu-id="4fba7-158">*Полное описание см. в статье об [управлении версиями пакета](../reference/package-versioning.md).*</span><span class="sxs-lookup"><span data-stu-id="4fba7-158">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="4fba7-159">При использовании формата `project.json` NuGet также поддерживает применение нотации с использованием подстановочного знака \* для суффикса номера основной, дополнительной, предварительной версии и версии с исправлением.</span><span class="sxs-lookup"><span data-stu-id="4fba7-159">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="4fba7-160">Справочник по NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="4fba7-160">NuGet.Config reference</span></span>

<span data-ttu-id="4fba7-161">*Полное описание см. в [справочнике по NuGet.Config](../reference/nuget-config-file.md).*</span><span class="sxs-lookup"><span data-stu-id="4fba7-161">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="4fba7-162">`globalPackagesFolder` применяется только к `project.json`.</span><span class="sxs-lookup"><span data-stu-id="4fba7-162">`globalPackagesFolder` applies only to `project.json`.</span></span> <span data-ttu-id="4fba7-163">(Применяется к формату PackageReference.)</span><span class="sxs-lookup"><span data-stu-id="4fba7-163">(Added note: also applies to PackageReference.)</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="4fba7-164">Справка по NUSPEC-файлу</span><span class="sxs-lookup"><span data-stu-id="4fba7-164">nuspec file reference</span></span>

<span data-ttu-id="4fba7-165">*Полное описание см. в [справочнике по NUSPEC-файлу](../reference/nuspec.md).*</span><span class="sxs-lookup"><span data-stu-id="4fba7-165">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="4fba7-166">Элемент `<contentFiles>` используется вместо `<files>` с файлом `project.json`.</span><span class="sxs-lookup"><span data-stu-id="4fba7-166">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="4fba7-167">Управление параметрами диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="4fba7-167">Package manager options control</span></span>

<span data-ttu-id="4fba7-168">*Полное описание см. в [справочнике по пользовательскому интерфейсу диспетчера пакетов](../tools/package-manager-ui.md).*</span><span class="sxs-lookup"><span data-stu-id="4fba7-168">*Originally in [Package Manager UI reference](../tools/package-manager-ui.md).*</span></span>

<span data-ttu-id="4fba7-169">В проектах, использующих формат управления `project.json`, отображается только параметр **Показать окно предварительного просмотра**.</span><span class="sxs-lookup"><span data-stu-id="4fba7-169">Projects using `project.json` management format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="4fba7-170">Шаблоны Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4fba7-170">Visual Studio Templates</span></span>

<span data-ttu-id="4fba7-171">*Полное описание см. в статье о [пакетах NuGet в шаблонах Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*</span><span class="sxs-lookup"><span data-stu-id="4fba7-171">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="4fba7-172">Шаблоны не содержат файл `project.json` и не включают в себя ссылки или содержимое, которое следует добавить при установке пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="4fba7-172">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>