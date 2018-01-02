---
title: "Объекты pack и restore NuGet в качестве целевых объектов MSBuild | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/3/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 86f7e724-2509-4d7d-aa8d-4a3fb913ded6
description: "Объекты pack и restore NuGet могут выступать непосредственно в качестве целевых объектов MSBuild в NuGet 4.0+."
keywords: "NuGet и MSBuild, целевой объект pack NuGet, целевой объект restore NuGet"
ms.reviewer: karann-msft
ms.openlocfilehash: def01380e5bc3bf878e72dd437f52cd033641ca5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="975c8-104">Объекты pack и restore NuGet в качестве целевых объектов MSBuild</span><span class="sxs-lookup"><span data-stu-id="975c8-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="975c8-105">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="975c8-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="975c8-106">NuGet 4.0+ может работать непосредственно с данными в файле `.csproj` без необходимости в отдельном файле `.nuspec` или `project.json`.</span><span class="sxs-lookup"><span data-stu-id="975c8-106">NuGet 4.0+ can work directly with the information in a `.csproj` file without requiring a separate `.nuspec` or `project.json` file.</span></span> <span data-ttu-id="975c8-107">Все метаданные, которые ранее хранились в этих файлах конфигурации, можно сохранить прямо в файле `.csproj`, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="975c8-107">All the metadata that was previously stored in those configuration files can be instead stored in the `.csproj` file directly, as described here.</span></span>

<span data-ttu-id="975c8-108">При использовании MSBuild 15.1+ NuGet также является привилегированным компонентом MSBuild с целевыми объектами `pack` и `restore`, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="975c8-108">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="975c8-109">Эти целевые объекты позволяют работать с NuGet, как с любой другой задачей или другим целевым объектом MSBuild.</span><span class="sxs-lookup"><span data-stu-id="975c8-109">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="975c8-110">(Для NuGet 3.x и более ранних версий можно использовать команды [pack](../tools/cli-ref-pack.md) и [restore](../tools/cli-ref-restore.md) в NuGet CLI.)</span><span class="sxs-lookup"><span data-stu-id="975c8-110">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

<span data-ttu-id="975c8-111">Содержание раздела</span><span class="sxs-lookup"><span data-stu-id="975c8-111">In this topic:</span></span>

- [<span data-ttu-id="975c8-112">Порядок сборки целевого объекта</span><span class="sxs-lookup"><span data-stu-id="975c8-112">Target build order</span></span>](#target-build-order)
- [<span data-ttu-id="975c8-113">Целевой объект pack</span><span class="sxs-lookup"><span data-stu-id="975c8-113">pack target</span></span>](#pack-target)
- [<span data-ttu-id="975c8-114">Сценарии использования pack</span><span class="sxs-lookup"><span data-stu-id="975c8-114">pack scenarios</span></span>](#pack-scenarios)
- [<span data-ttu-id="975c8-115">Целевой объект restore</span><span class="sxs-lookup"><span data-stu-id="975c8-115">restore target</span></span>](#restore-target)
- [<span data-ttu-id="975c8-116">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="975c8-116">PackageTargetFallback</span></span>](#packagetargetfallback)

## <a name="target-build-order"></a><span data-ttu-id="975c8-117">Порядок сборки целевого объекта</span><span class="sxs-lookup"><span data-stu-id="975c8-117">Target build order</span></span>

<span data-ttu-id="975c8-118">Так как `pack` и `restore` являются целевыми объектами MSBuild, вы можете обращаться к ним для улучшения рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="975c8-118">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="975c8-119">Например, предположим, что вам нужно скопировать пакет в общую сетевую папку после его упаковки.</span><span class="sxs-lookup"><span data-stu-id="975c8-119">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="975c8-120">Это можно сделать, добавив следующий код в файл проекта:</span><span class="sxs-lookup"><span data-stu-id="975c8-120">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="975c8-121">Аналогичным образом, вы можете создать задачу MSBuild и собственный целевой объект и использовать свойства NuGet в этой задаче MSBuild.</span><span class="sxs-lookup"><span data-stu-id="975c8-121">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="975c8-122">Целевой объект pack</span><span class="sxs-lookup"><span data-stu-id="975c8-122">pack target</span></span>

<span data-ttu-id="975c8-123">При использовании целевого объекта pack, то есть `msbuild /t:pack`, MSBuild получает входные данные из файла `.csproj`, а не файлов `project.json` или `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="975c8-123">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the `.csproj` file rather than `project.json` or `.nuspec` files.</span></span> <span data-ttu-id="975c8-124">Следующая таблица описывает свойства MSBuild, которые можно добавить в файл `.csproj` в первом узле `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="975c8-124">The table below describes the MSBuild properties that can be added to a `.csproj` file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="975c8-125">Эти изменения легко внести в Visual Studio 2017 и более поздней версии, щелкнув проект правой кнопкой мыши и выбрав пункт **Изменить {project_name}**.</span><span class="sxs-lookup"><span data-stu-id="975c8-125">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="975c8-126">Для удобства таблица упорядочена по эквивалентным свойствам в [файле `.nuspec`](../schema/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="975c8-126">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../schema/nuspec.md).</span></span>

<span data-ttu-id="975c8-127">Обратите внимание, что свойства `Owners` и `Summary` из `.nuspec` не поддерживаются в MSBuild.</span><span class="sxs-lookup"><span data-stu-id="975c8-127">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>


| <span data-ttu-id="975c8-128">Значение атрибута или NuSpec</span><span class="sxs-lookup"><span data-stu-id="975c8-128">Attribute/NuSpec Value</span></span> | <span data-ttu-id="975c8-129">Свойство MSBuild</span><span class="sxs-lookup"><span data-stu-id="975c8-129">MSBuild Property</span></span> | <span data-ttu-id="975c8-130">По умолчанию</span><span class="sxs-lookup"><span data-stu-id="975c8-130">Default</span></span> | <span data-ttu-id="975c8-131">Примечания</span><span class="sxs-lookup"><span data-stu-id="975c8-131">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="975c8-132">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="975c8-132">Id</span></span> | <span data-ttu-id="975c8-133">PackageId</span><span class="sxs-lookup"><span data-stu-id="975c8-133">PackageId</span></span> | <span data-ttu-id="975c8-134">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="975c8-134">AssemblyName</span></span> | <span data-ttu-id="975c8-135">$(AssemblyName) из MSBuild</span><span class="sxs-lookup"><span data-stu-id="975c8-135">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="975c8-136">Версия</span><span class="sxs-lookup"><span data-stu-id="975c8-136">Version</span></span> | <span data-ttu-id="975c8-137">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="975c8-137">PackageVersion</span></span> | <span data-ttu-id="975c8-138">Версия</span><span class="sxs-lookup"><span data-stu-id="975c8-138">Version</span></span> | <span data-ttu-id="975c8-139">Это значение совместимо с SemVer, например "1.0.0", "1.0.0-beta" или "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="975c8-139">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="975c8-140">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="975c8-140">VersionPrefix</span></span> | <span data-ttu-id="975c8-141">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="975c8-141">PackageVersionPrefix</span></span> | <span data-ttu-id="975c8-142">пустой</span><span class="sxs-lookup"><span data-stu-id="975c8-142">empty</span></span> | <span data-ttu-id="975c8-143">Задав PackageVersion, вы перезапишете PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="975c8-143">Setting PackageVersion will overwrite PackageVersionPrefix</span></span> |
| <span data-ttu-id="975c8-144">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="975c8-144">VersionSuffix</span></span> | <span data-ttu-id="975c8-145">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="975c8-145">PackageVersionSuffix</span></span> | <span data-ttu-id="975c8-146">пустой</span><span class="sxs-lookup"><span data-stu-id="975c8-146">empty</span></span> | <span data-ttu-id="975c8-147">$(VersionSuffix) из MSBuild.</span><span class="sxs-lookup"><span data-stu-id="975c8-147">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="975c8-148">Задав PackageVersion, вы перезапишете PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="975c8-148">Setting PackageVersion will overwrite PackageVersionSuffix</span></span> | 
| <span data-ttu-id="975c8-149">Authors</span><span class="sxs-lookup"><span data-stu-id="975c8-149">Authors</span></span> | <span data-ttu-id="975c8-150">Authors</span><span class="sxs-lookup"><span data-stu-id="975c8-150">Authors</span></span> | <span data-ttu-id="975c8-151">Имя текущего пользователя</span><span class="sxs-lookup"><span data-stu-id="975c8-151">Username of the current user</span></span> | |
| <span data-ttu-id="975c8-152">Владельцы</span><span class="sxs-lookup"><span data-stu-id="975c8-152">Owners</span></span> | <span data-ttu-id="975c8-153">Н/Д</span><span class="sxs-lookup"><span data-stu-id="975c8-153">N/A</span></span> | <span data-ttu-id="975c8-154">Не существует в NuSpec</span><span class="sxs-lookup"><span data-stu-id="975c8-154">Not present in NuSpec</span></span> | |
| <span data-ttu-id="975c8-155">Заголовок</span><span class="sxs-lookup"><span data-stu-id="975c8-155">Title</span></span> | <span data-ttu-id="975c8-156">Заголовок</span><span class="sxs-lookup"><span data-stu-id="975c8-156">Title</span></span> | <span data-ttu-id="975c8-157">Идентификатор пакета</span><span class="sxs-lookup"><span data-stu-id="975c8-157">The PackageId</span></span>| |
| <span data-ttu-id="975c8-158">Описание</span><span class="sxs-lookup"><span data-stu-id="975c8-158">Description</span></span> | <span data-ttu-id="975c8-159">Описание</span><span class="sxs-lookup"><span data-stu-id="975c8-159">Description</span></span> | <span data-ttu-id="975c8-160">"Описание пакета"</span><span class="sxs-lookup"><span data-stu-id="975c8-160">"Package Description"</span></span> | |
| <span data-ttu-id="975c8-161">Copyright</span><span class="sxs-lookup"><span data-stu-id="975c8-161">Copyright</span></span> | <span data-ttu-id="975c8-162">Copyright</span><span class="sxs-lookup"><span data-stu-id="975c8-162">Copyright</span></span> | <span data-ttu-id="975c8-163">пустой</span><span class="sxs-lookup"><span data-stu-id="975c8-163">empty</span></span> | |
| <span data-ttu-id="975c8-164">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="975c8-164">RequireLicenseAcceptance</span></span> | <span data-ttu-id="975c8-165">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="975c8-165">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="975c8-166">false</span><span class="sxs-lookup"><span data-stu-id="975c8-166">false</span></span> | |
| <span data-ttu-id="975c8-167">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="975c8-167">LicenseUrl</span></span> | <span data-ttu-id="975c8-168">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="975c8-168">PackageLicenseUrl</span></span> | <span data-ttu-id="975c8-169">пустой</span><span class="sxs-lookup"><span data-stu-id="975c8-169">empty</span></span> | |
| <span data-ttu-id="975c8-170">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="975c8-170">ProjectUrl</span></span> | <span data-ttu-id="975c8-171">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="975c8-171">PackageProjectUrl</span></span> | <span data-ttu-id="975c8-172">пустой</span><span class="sxs-lookup"><span data-stu-id="975c8-172">empty</span></span> | |
| <span data-ttu-id="975c8-173">IconUrl</span><span class="sxs-lookup"><span data-stu-id="975c8-173">IconUrl</span></span> | <span data-ttu-id="975c8-174">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="975c8-174">PackageIconUrl</span></span> | <span data-ttu-id="975c8-175">пустой</span><span class="sxs-lookup"><span data-stu-id="975c8-175">empty</span></span> | |
| <span data-ttu-id="975c8-176">Теги</span><span class="sxs-lookup"><span data-stu-id="975c8-176">Tags</span></span> | <span data-ttu-id="975c8-177">PackageTags</span><span class="sxs-lookup"><span data-stu-id="975c8-177">PackageTags</span></span> | <span data-ttu-id="975c8-178">пустой</span><span class="sxs-lookup"><span data-stu-id="975c8-178">empty</span></span> | <span data-ttu-id="975c8-179">Теги разделяются точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="975c8-179">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="975c8-180">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="975c8-180">ReleaseNotes</span></span> | <span data-ttu-id="975c8-181">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="975c8-181">PackageReleaseNotes</span></span> | <span data-ttu-id="975c8-182">пустой</span><span class="sxs-lookup"><span data-stu-id="975c8-182">empty</span></span> | |
| <span data-ttu-id="975c8-183">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="975c8-183">RepositoryUrl</span></span> | <span data-ttu-id="975c8-184">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="975c8-184">RepositoryUrl</span></span> | <span data-ttu-id="975c8-185">пустой</span><span class="sxs-lookup"><span data-stu-id="975c8-185">empty</span></span> | |
| <span data-ttu-id="975c8-186">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="975c8-186">RepositoryType</span></span> | <span data-ttu-id="975c8-187">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="975c8-187">RepositoryType</span></span> | <span data-ttu-id="975c8-188">пустой</span><span class="sxs-lookup"><span data-stu-id="975c8-188">empty</span></span> | |
| <span data-ttu-id="975c8-189">PackageType</span><span class="sxs-lookup"><span data-stu-id="975c8-189">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="975c8-190">Сводка</span><span class="sxs-lookup"><span data-stu-id="975c8-190">Summary</span></span> | <span data-ttu-id="975c8-191">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="975c8-191">Not supported</span></span> | | |


### <a name="pack-target-inputs"></a><span data-ttu-id="975c8-192">Входные данные целевого объекта pack</span><span class="sxs-lookup"><span data-stu-id="975c8-192">pack target inputs</span></span>

- <span data-ttu-id="975c8-193">IsPackable</span><span class="sxs-lookup"><span data-stu-id="975c8-193">IsPackable</span></span>
- <span data-ttu-id="975c8-194">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="975c8-194">PackageVersion</span></span>
- <span data-ttu-id="975c8-195">PackageId</span><span class="sxs-lookup"><span data-stu-id="975c8-195">PackageId</span></span>
- <span data-ttu-id="975c8-196">Authors</span><span class="sxs-lookup"><span data-stu-id="975c8-196">Authors</span></span>
- <span data-ttu-id="975c8-197">Описание</span><span class="sxs-lookup"><span data-stu-id="975c8-197">Description</span></span>
- <span data-ttu-id="975c8-198">Copyright</span><span class="sxs-lookup"><span data-stu-id="975c8-198">Copyright</span></span>
- <span data-ttu-id="975c8-199">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="975c8-199">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="975c8-200">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="975c8-200">DevelopmentDependency</span></span>
- <span data-ttu-id="975c8-201">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="975c8-201">PackageLicenseUrl</span></span>
- <span data-ttu-id="975c8-202">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="975c8-202">PackageProjectUrl</span></span>
- <span data-ttu-id="975c8-203">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="975c8-203">PackageIconUrl</span></span>
- <span data-ttu-id="975c8-204">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="975c8-204">PackageReleaseNotes</span></span>
- <span data-ttu-id="975c8-205">PackageTags</span><span class="sxs-lookup"><span data-stu-id="975c8-205">PackageTags</span></span>
- <span data-ttu-id="975c8-206">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="975c8-206">PackageOutputPath</span></span>
- <span data-ttu-id="975c8-207">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="975c8-207">IncludeSymbols</span></span>
- <span data-ttu-id="975c8-208">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="975c8-208">IncludeSource</span></span>
- <span data-ttu-id="975c8-209">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="975c8-209">PackageTypes</span></span>
- <span data-ttu-id="975c8-210">IsTool</span><span class="sxs-lookup"><span data-stu-id="975c8-210">IsTool</span></span>
- <span data-ttu-id="975c8-211">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="975c8-211">RepositoryUrl</span></span>
- <span data-ttu-id="975c8-212">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="975c8-212">RepositoryType</span></span>
- <span data-ttu-id="975c8-213">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="975c8-213">NoPackageAnalysis</span></span>
- <span data-ttu-id="975c8-214">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="975c8-214">MinClientVersion</span></span>
- <span data-ttu-id="975c8-215">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="975c8-215">IncludeBuildOutput</span></span>
- <span data-ttu-id="975c8-216">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="975c8-216">IncludeContentInPack</span></span>
- <span data-ttu-id="975c8-217">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="975c8-217">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="975c8-218">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="975c8-218">ContentTargetFolders</span></span>
- <span data-ttu-id="975c8-219">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="975c8-219">NuspecFile</span></span>
- <span data-ttu-id="975c8-220">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="975c8-220">NuspecBasePath</span></span>
- <span data-ttu-id="975c8-221">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="975c8-221">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="975c8-222">Сценарии использования pack</span><span class="sxs-lookup"><span data-stu-id="975c8-222">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="975c8-223">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="975c8-223">PackageIconUrl</span></span>

<span data-ttu-id="975c8-224">В процессе внесения изменения для [вопроса 2582 по NuGet](https://github.com/NuGet/Home/issues/2582) `PackageIconUrl` в конечном итоге будет изменен на `PackageIconUri` и может быть относительным путем к файлу значка, который будет включен в корень итогового пакета.</span><span class="sxs-lookup"><span data-stu-id="975c8-224">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="975c8-225">Выходные сборки</span><span class="sxs-lookup"><span data-stu-id="975c8-225">Output assemblies</span></span>

<span data-ttu-id="975c8-226">`nuget pack` копирует выходные файлы с расширениями `.exe`, `.dll`, `.xml`, `.winmd`, `.json` и `.pri`.</span><span class="sxs-lookup"><span data-stu-id="975c8-226">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="975c8-227">Копируемые выходные файлы зависят от того, что MSBuild предоставляет из целевого объекта `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="975c8-227">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="975c8-228">Существует два свойства MSBuild, которые можно использовать в файле проекта или командной строке для управления местом назначения для выходных сборок:</span><span class="sxs-lookup"><span data-stu-id="975c8-228">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="975c8-229">`IncludeBuildOutput`: логическое значение, определяющее, следует ли включать выходные сборки в пакете.</span><span class="sxs-lookup"><span data-stu-id="975c8-229">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="975c8-230">`BuildOutputTargetFolder`: указывает папку, куда следует помещать выходные сборки.</span><span class="sxs-lookup"><span data-stu-id="975c8-230">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="975c8-231">Выходные сборки (и другие выходные файлы) копируются в соответствующие папки платформы.</span><span class="sxs-lookup"><span data-stu-id="975c8-231">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="975c8-232">Ссылки на пакеты</span><span class="sxs-lookup"><span data-stu-id="975c8-232">Package references</span></span>

<span data-ttu-id="975c8-233">См. раздел [Ссылки на пакеты в файлах проекта](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="975c8-233">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="975c8-234">Перекрестные ссылки между проектами</span><span class="sxs-lookup"><span data-stu-id="975c8-234">Project to project references</span></span>

<span data-ttu-id="975c8-235">Перекрестные ссылки между проектами по умолчанию считаются ссылками на пакет NuGet, например:</span><span class="sxs-lookup"><span data-stu-id="975c8-235">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="975c8-236">Вы также можете добавить в ссылку на проект следующие метаданные:</span><span class="sxs-lookup"><span data-stu-id="975c8-236">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="975c8-237">Включение содержимого в пакет</span><span class="sxs-lookup"><span data-stu-id="975c8-237">Including content in a package</span></span>

<span data-ttu-id="975c8-238">Чтобы включить содержимое, добавьте дополнительные метаданные для существующего элемента `<Content>`.</span><span class="sxs-lookup"><span data-stu-id="975c8-238">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="975c8-239">По умолчанию все данные типа "Content" включаются в пакет, если только вы не переопределите такое поведение с помощью записей, аналогичных следующим:</span><span class="sxs-lookup"><span data-stu-id="975c8-239">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="975c8-240">По умолчанию все данные добавляются в корень папки `content` и `contentFiles\any\<target_framework>` в пакете и сохраняют относительную структуру папок, если только не указан путь к пакету:</span><span class="sxs-lookup"><span data-stu-id="975c8-240">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">        
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="975c8-241">Если требуется скопировать все содержимое только в определенные корневые папки (вместо `content` и `contentFiles`), можно использовать свойство MSBuild `ContentTargetFolders`, которое по умолчанию имеет значение "content;contentFiles", но может принимать любые другие имена папок.</span><span class="sxs-lookup"><span data-stu-id="975c8-241">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="975c8-242">Обратите внимание, если указать "contentFiles" в `ContentTargetFolders`, файлы помещаются в `contentFiles\any\<target_framework>` или `contentFiles\<language>\<target_framework>` в зависимости от `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="975c8-242">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="975c8-243">`PackagePath` может быть набором целевых путей, разделенных точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="975c8-243">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="975c8-244">Если указан пустой путь к пакету, файл добавляется в корневой каталог пакета.</span><span class="sxs-lookup"><span data-stu-id="975c8-244">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="975c8-245">Например, следующий код добавляет `libuv.txt` в `content\myfiles`, `content\samples` и корневой каталог пакета:</span><span class="sxs-lookup"><span data-stu-id="975c8-245">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="975c8-246">Имеется также свойство MSBuild `$(IncludeContentInPack)`, которое по умолчанию равно `true`.</span><span class="sxs-lookup"><span data-stu-id="975c8-246">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="975c8-247">Если оно имеет значение `false` для какого-либо проекта, то содержимое этого проекта не включается в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="975c8-247">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="975c8-248">Другие относящиеся к pack метаданные, которые можно задать для любого из указанных выше элементов, включают ```<PackageCopyToOutput>``` и ```<PackageFlatten>```, задающие значения ```CopyToOutput``` и ```Flatten``` для записи ```contentFiles``` в выходном файле NUSPEC.</span><span class="sxs-lookup"><span data-stu-id="975c8-248">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>


> [!Note]
> <span data-ttu-id="975c8-249">Кроме элементов содержимого, метаданные `<Pack>` и `<PackagePath>` также можно задать для файлов с действием сборки Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource или None.</span><span class="sxs-lookup"><span data-stu-id="975c8-249">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="975c8-250">Чтобы объект pack добавил имя файла в путь к пакету при использовании стандартных масок, путь к пакету должен заканчиваться символом разделителя папок, в противном случае этот путь считается полным путем, включающим имя файла.</span><span class="sxs-lookup"><span data-stu-id="975c8-250">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="975c8-251">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="975c8-251">IncludeSymbols</span></span>

<span data-ttu-id="975c8-252">При использовании `MSBuild /t:pack /p:IncludeSymbols=true` соответствующие файлы `.pdb` копируются вместе с другими выходными файлами (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="975c8-252">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="975c8-253">Обратите внимание, что при задании `IncludeSymbols=true` создается обычный пакет *и* пакет символов.</span><span class="sxs-lookup"><span data-stu-id="975c8-253">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="975c8-254">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="975c8-254">IncludeSource</span></span>

<span data-ttu-id="975c8-255">Аналогично `IncludeSymbols`, только копирует исходные файлы вместе с файлами `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="975c8-255">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="975c8-256">Все файлы типа `Compile` копируются в `src\<ProjectName>\` с сохранением относительной структуры папок в итоговом пакете.</span><span class="sxs-lookup"><span data-stu-id="975c8-256">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="975c8-257">То же самое происходит с исходными файлами любого `ProjectReference`, у которого `TreatAsPackageReference` имеет значение `false`.</span><span class="sxs-lookup"><span data-stu-id="975c8-257">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="975c8-258">Если файл типа "Compile" находится вне папки проекта, он добавляется только в `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="975c8-258">If a file of type Compile, is outside the project folder, then it is just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="975c8-259">IsTool</span><span class="sxs-lookup"><span data-stu-id="975c8-259">IsTool</span></span>

<span data-ttu-id="975c8-260">При использовании `MSBuild /t:pack /p:IsTool=true` все выходные файлы, как указано в сценарии [Выходные сборки](#output-assemblies), копируются в папку `tools` вместо папки `lib`.</span><span class="sxs-lookup"><span data-stu-id="975c8-260">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="975c8-261">Обратите внимание, что это свойство отличается от `DotNetCliTool`, которое указывается путем задания `PackageType` в файле `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="975c8-261">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="975c8-262">Упаковка с помощью NUSPEC</span><span class="sxs-lookup"><span data-stu-id="975c8-262">Packing using a .nuspec</span></span>

<span data-ttu-id="975c8-263">Вы можете использовать файл `.nuspec` для упаковки проекта при условии, что у вас есть файл проекта для импорта `NuGet.Build.Tasks.Pack.targets`, чтобы можно было выполнить задачу пакета.</span><span class="sxs-lookup"><span data-stu-id="975c8-263">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="975c8-264">Следующие три свойства MSBuild связаны с упаковкой с помощью `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="975c8-264">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="975c8-265">`NuspecFile`: относительный или абсолютный путь к файлу `.nuspec`, используемому для упаковки.</span><span class="sxs-lookup"><span data-stu-id="975c8-265">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="975c8-266">`NuspecProperties`: список разделенных точками с запятой пар "ключ-значение".</span><span class="sxs-lookup"><span data-stu-id="975c8-266">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="975c8-267">Из-за особенностей работы анализа в командной строке MSBuild несколько свойств нужно указать следующим образом: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="975c8-267">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="975c8-268">`NuspecBasePath`: базовый путь для файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="975c8-268">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="975c8-269">Если вы используете `dotnet.exe` для упаковки проекта, воспользуйтесь командой, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="975c8-269">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="975c8-270">Если вы используете MSBuild для упаковки проекта, воспользуйтесь командой, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="975c8-270">If using MSBuild to pack your project, use a command like the following:</span></span>

```
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="975c8-271">Целевой объект restore</span><span class="sxs-lookup"><span data-stu-id="975c8-271">restore target</span></span>

<span data-ttu-id="975c8-272">`MSBuild /t:restore` (который `nuget restore` и `dotnet restore` используют с проектами .NET Core) восстанавливает пакеты, на которые ссылается файл проекта:</span><span class="sxs-lookup"><span data-stu-id="975c8-272">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="975c8-273">Чтение перекрестных ссылок между проектами.</span><span class="sxs-lookup"><span data-stu-id="975c8-273">Read all project to project references</span></span>
1. <span data-ttu-id="975c8-274">Чтение свойств проекта, чтобы найти промежуточную папку и целевые платформы.</span><span class="sxs-lookup"><span data-stu-id="975c8-274">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="975c8-275">Передача данных MSBuild в NuGet.Build.Tasks.dll.</span><span class="sxs-lookup"><span data-stu-id="975c8-275">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="975c8-276">Запуск восстановления.</span><span class="sxs-lookup"><span data-stu-id="975c8-276">Run restore</span></span>
1. <span data-ttu-id="975c8-277">Скачивание пакетов.</span><span class="sxs-lookup"><span data-stu-id="975c8-277">Download packages</span></span>
1. <span data-ttu-id="975c8-278">Запись файла ресурсов, целевых объектов и свойств.</span><span class="sxs-lookup"><span data-stu-id="975c8-278">Write assets file, targets, and props</span></span>


### <a name="restore-properties"></a><span data-ttu-id="975c8-279">Свойства восстановления</span><span class="sxs-lookup"><span data-stu-id="975c8-279">Restore properties</span></span>

<span data-ttu-id="975c8-280">Дополнительные параметры восстановления могут поступать из свойств MSBuild в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="975c8-280">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="975c8-281">Значения также можно задать из командной строки с помощью параметра `/p:` (см. примеры ниже).</span><span class="sxs-lookup"><span data-stu-id="975c8-281">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="975c8-282">Свойство</span><span class="sxs-lookup"><span data-stu-id="975c8-282">Property</span></span> | <span data-ttu-id="975c8-283">Описание</span><span class="sxs-lookup"><span data-stu-id="975c8-283">Description</span></span> |
|--------|--------|
| <span data-ttu-id="975c8-284">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="975c8-284">RestoreSources</span></span> | <span data-ttu-id="975c8-285">Разделенный точками с запятой список источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="975c8-285">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="975c8-286">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="975c8-286">RestorePackagesPath</span></span> | <span data-ttu-id="975c8-287">Путь к папке пакетов пользователя.</span><span class="sxs-lookup"><span data-stu-id="975c8-287">User packages folder path.</span></span> |
| <span data-ttu-id="975c8-288">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="975c8-288">RestoreDisableParallel</span></span> | <span data-ttu-id="975c8-289">Ограничение скачиваний до одного за раз.</span><span class="sxs-lookup"><span data-stu-id="975c8-289">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="975c8-290">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="975c8-290">RestoreConfigFile</span></span> | <span data-ttu-id="975c8-291">Путь к применяемому файлу `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="975c8-291">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="975c8-292">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="975c8-292">RestoreNoCache</span></span> | <span data-ttu-id="975c8-293">Если значение равно true, веб-кэш по возможности не используется.</span><span class="sxs-lookup"><span data-stu-id="975c8-293">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="975c8-294">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="975c8-294">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="975c8-295">Если значение равно true, нерабочие или отсутствующие источники пакетов игнорируются.</span><span class="sxs-lookup"><span data-stu-id="975c8-295">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="975c8-296">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="975c8-296">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="975c8-297">Путь к `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="975c8-297">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="975c8-298">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="975c8-298">RestoreGraphProjectInput</span></span> | <span data-ttu-id="975c8-299">Разделенный точками с запятой список проектов для восстановления, который должен содержать абсолютные пути.</span><span class="sxs-lookup"><span data-stu-id="975c8-299">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="975c8-300">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="975c8-300">RestoreOutputPath</span></span> | <span data-ttu-id="975c8-301">Выходная папка, по умолчанию используется `obj`.</span><span class="sxs-lookup"><span data-stu-id="975c8-301">Output folder, defaulting to the `obj` folder.</span></span> |

<span data-ttu-id="975c8-302">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="975c8-302">**Examples**</span></span>

<span data-ttu-id="975c8-303">Командная строка:</span><span class="sxs-lookup"><span data-stu-id="975c8-303">Command line:</span></span>

```
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="975c8-304">Файл проекта:</span><span class="sxs-lookup"><span data-stu-id="975c8-304">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="975c8-305">Выходные данные восстановления</span><span class="sxs-lookup"><span data-stu-id="975c8-305">Restore outputs</span></span>

<span data-ttu-id="975c8-306">Операция восстановления создает в папке сборки `obj` следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="975c8-306">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="975c8-307">Файл</span><span class="sxs-lookup"><span data-stu-id="975c8-307">File</span></span> | <span data-ttu-id="975c8-308">Описание</span><span class="sxs-lookup"><span data-stu-id="975c8-308">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="975c8-309">Раньше назывался `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="975c8-309">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="975c8-310">Ссылки на свойства MSBuild, содержащиеся в пакетах.</span><span class="sxs-lookup"><span data-stu-id="975c8-310">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="975c8-311">Ссылки на целевые объекты MSBuild, содержащиеся в пакетах.</span><span class="sxs-lookup"><span data-stu-id="975c8-311">References to MSBuild targets contained in packages</span></span> |


### <a name="packagetargetfallback"></a><span data-ttu-id="975c8-312">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="975c8-312">PackageTargetFallback</span></span> 

<span data-ttu-id="975c8-313">Элемент `PackageTargetFallback` позволяет указать набор совместимых целевых объектов, которые следует использовать при восстановлении пакетов (эквивалент [`imports` в `project.json`](../schema/project-json.md#imports)).</span><span class="sxs-lookup"><span data-stu-id="975c8-313">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages (the equivalent of [`imports` in `project.json`](../schema/project-json.md#imports)).</span></span> <span data-ttu-id="975c8-314">Он разрешает пакетам, использующим dotnet [TxM](../schema/target-frameworks.md), взаимодействовать с совместимыми пакетами, которые не объявляют dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="975c8-314">It's designed to allow packages that use a dotnet [TxM](../schema/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="975c8-315">Таким образом, если в проекте используется dotnet TxM, все пакеты, от которых вы зависите, должны также содержать dotnet TxM. В противном случае нужно добавить `<PackageTargetFallback>` в проект, чтобы обеспечить совместимость с платформами, отличными от dotnet.</span><span class="sxs-lookup"><span data-stu-id="975c8-315">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span> 

<span data-ttu-id="975c8-316">Например, если в проекте используется `netstandard1.6` TxM, а зависимый пакет содержит только `lib/net45/a.dll` и `lib/portable-net45+win81/a.dll`, то сборка проекта завершится со сбоем.</span><span class="sxs-lookup"><span data-stu-id="975c8-316">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="975c8-317">Если вы хотите использовать вторую библиотеку DLL, можете добавить `PackageTargetFallback` следующим образом, чтобы обозначить совместимость библиотеки DLL `portable-net45+win81`:</span><span class="sxs-lookup"><span data-stu-id="975c8-317">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="975c8-318">Чтобы объявить откат для всех целевых объектов в проекте, оставьте атрибут `Condition`.</span><span class="sxs-lookup"><span data-stu-id="975c8-318">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="975c8-319">Кроме того, можно расширить существующий `PackageTargetFallback`, включив `$(PackageTargetFallback)`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="975c8-319">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```


### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="975c8-320">Замена одной библиотеки из графа восстановления</span><span class="sxs-lookup"><span data-stu-id="975c8-320">Replacing one library from a restore graph</span></span>

<span data-ttu-id="975c8-321">Если операция восстановления предоставляет неправильную сборку, можно исключить значение по умолчанию для этого пакета, заменив его своим значением.</span><span class="sxs-lookup"><span data-stu-id="975c8-321">If a restore is bringing the wrong assembly, it is possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="975c8-322">Первый с `PackageReference` верхнего уровня, исключите все ресурсы:</span><span class="sxs-lookup"><span data-stu-id="975c8-322">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="975c8-323">После этого добавьте собственную ссылку на соответствующую локальную копию библиотеки DLL:</span><span class="sxs-lookup"><span data-stu-id="975c8-323">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
