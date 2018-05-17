---
title: Объекты pack и restore NuGet в качестве целевых объектов MSBuild
description: Объекты pack и restore NuGet могут выступать непосредственно в качестве целевых объектов MSBuild в NuGet 4.0+.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 00d763bcfdd2f3db50378a1e7774eae7a2e1fcd1
ms.sourcegitcommit: 00c4c809c69c16fcf4d81012eb53ea22f0691d0b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="3eddb-103">Объекты pack и restore NuGet в качестве целевых объектов MSBuild</span><span class="sxs-lookup"><span data-stu-id="3eddb-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="3eddb-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="3eddb-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="3eddb-105">Благодаря формату PackageReference в NuGet 4.0 и более поздних версиях все метаданные манифеста могут храниться прямо в файле проекта, не требуя использования отдельного файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="3eddb-106">При использовании MSBuild 15.1+ NuGet также является привилегированным компонентом MSBuild с целевыми объектами `pack` и `restore`, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="3eddb-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="3eddb-107">Эти целевые объекты позволяют работать с NuGet, как с любой другой задачей или другим целевым объектом MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3eddb-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="3eddb-108">(Для NuGet 3.x и более ранних версий можно использовать команды [pack](../tools/cli-ref-pack.md) и [restore](../tools/cli-ref-restore.md) в NuGet CLI.)</span><span class="sxs-lookup"><span data-stu-id="3eddb-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="3eddb-109">Порядок сборки целевого объекта</span><span class="sxs-lookup"><span data-stu-id="3eddb-109">Target build order</span></span>

<span data-ttu-id="3eddb-110">Так как `pack` и `restore` являются целевыми объектами MSBuild, вы можете обращаться к ним для улучшения рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="3eddb-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="3eddb-111">Например, предположим, что вам нужно скопировать пакет в общую сетевую папку после его упаковки.</span><span class="sxs-lookup"><span data-stu-id="3eddb-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="3eddb-112">Это можно сделать, добавив следующий код в файл проекта:</span><span class="sxs-lookup"><span data-stu-id="3eddb-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="3eddb-113">Аналогичным образом, вы можете создать задачу MSBuild и собственный целевой объект и использовать свойства NuGet в этой задаче MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3eddb-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="3eddb-114">Целевой объект pack</span><span class="sxs-lookup"><span data-stu-id="3eddb-114">pack target</span></span>

<span data-ttu-id="3eddb-115">Для проектов .NET Standard в формате PackageReference, с помощью `msbuild /t:pack` рисует входные данные из файла проекта для создания пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="3eddb-115">For .NET Standard projects using the PackageReference format, using `msbuild /t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="3eddb-116">В следующей таблице описываются свойства MSBuild, которые можно добавить в файл проекта в первом узле `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="3eddb-117">Эти изменения легко внести в Visual Studio 2017 и более поздней версии, щелкнув проект правой кнопкой мыши и выбрав пункт **Изменить {project_name}**.</span><span class="sxs-lookup"><span data-stu-id="3eddb-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="3eddb-118">Для удобства таблица упорядочена по эквивалентным свойствам в [файле `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="3eddb-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="3eddb-119">Обратите внимание, что свойства `Owners` и `Summary` из `.nuspec` не поддерживаются в MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3eddb-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="3eddb-120">Значение атрибута или NuSpec</span><span class="sxs-lookup"><span data-stu-id="3eddb-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="3eddb-121">Свойство MSBuild</span><span class="sxs-lookup"><span data-stu-id="3eddb-121">MSBuild Property</span></span> | <span data-ttu-id="3eddb-122">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3eddb-122">Default</span></span> | <span data-ttu-id="3eddb-123">Примечания</span><span class="sxs-lookup"><span data-stu-id="3eddb-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="3eddb-124">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="3eddb-124">Id</span></span> | <span data-ttu-id="3eddb-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="3eddb-125">PackageId</span></span> | <span data-ttu-id="3eddb-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="3eddb-126">AssemblyName</span></span> | <span data-ttu-id="3eddb-127">$(AssemblyName) из MSBuild</span><span class="sxs-lookup"><span data-stu-id="3eddb-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="3eddb-128">Версия</span><span class="sxs-lookup"><span data-stu-id="3eddb-128">Version</span></span> | <span data-ttu-id="3eddb-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="3eddb-129">PackageVersion</span></span> | <span data-ttu-id="3eddb-130">Версия</span><span class="sxs-lookup"><span data-stu-id="3eddb-130">Version</span></span> | <span data-ttu-id="3eddb-131">Это значение совместимо с SemVer, например "1.0.0", "1.0.0-beta" или "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="3eddb-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="3eddb-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="3eddb-132">VersionPrefix</span></span> | <span data-ttu-id="3eddb-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="3eddb-133">PackageVersionPrefix</span></span> | <span data-ttu-id="3eddb-134">пустой</span><span class="sxs-lookup"><span data-stu-id="3eddb-134">empty</span></span> | <span data-ttu-id="3eddb-135">Задав PackageVersion, вы перезапишите PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="3eddb-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="3eddb-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="3eddb-136">VersionSuffix</span></span> | <span data-ttu-id="3eddb-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="3eddb-137">PackageVersionSuffix</span></span> | <span data-ttu-id="3eddb-138">пустой</span><span class="sxs-lookup"><span data-stu-id="3eddb-138">empty</span></span> | <span data-ttu-id="3eddb-139">$(VersionSuffix) из MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3eddb-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="3eddb-140">Задав PackageVersion, вы перезапишите PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="3eddb-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="3eddb-141">Authors</span><span class="sxs-lookup"><span data-stu-id="3eddb-141">Authors</span></span> | <span data-ttu-id="3eddb-142">Authors</span><span class="sxs-lookup"><span data-stu-id="3eddb-142">Authors</span></span> | <span data-ttu-id="3eddb-143">Имя текущего пользователя</span><span class="sxs-lookup"><span data-stu-id="3eddb-143">Username of the current user</span></span> | |
| <span data-ttu-id="3eddb-144">Владельцы</span><span class="sxs-lookup"><span data-stu-id="3eddb-144">Owners</span></span> | <span data-ttu-id="3eddb-145">Н/Д</span><span class="sxs-lookup"><span data-stu-id="3eddb-145">N/A</span></span> | <span data-ttu-id="3eddb-146">Не существует в NuSpec</span><span class="sxs-lookup"><span data-stu-id="3eddb-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="3eddb-147">Заголовок</span><span class="sxs-lookup"><span data-stu-id="3eddb-147">Title</span></span> | <span data-ttu-id="3eddb-148">Заголовок</span><span class="sxs-lookup"><span data-stu-id="3eddb-148">Title</span></span> | <span data-ttu-id="3eddb-149">Идентификатор пакета</span><span class="sxs-lookup"><span data-stu-id="3eddb-149">The PackageId</span></span>| |
| <span data-ttu-id="3eddb-150">Описание</span><span class="sxs-lookup"><span data-stu-id="3eddb-150">Description</span></span> | <span data-ttu-id="3eddb-151">Описание</span><span class="sxs-lookup"><span data-stu-id="3eddb-151">Description</span></span> | <span data-ttu-id="3eddb-152">"Описание пакета"</span><span class="sxs-lookup"><span data-stu-id="3eddb-152">"Package Description"</span></span> | |
| <span data-ttu-id="3eddb-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="3eddb-153">Copyright</span></span> | <span data-ttu-id="3eddb-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="3eddb-154">Copyright</span></span> | <span data-ttu-id="3eddb-155">пустой</span><span class="sxs-lookup"><span data-stu-id="3eddb-155">empty</span></span> | |
| <span data-ttu-id="3eddb-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3eddb-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="3eddb-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3eddb-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="3eddb-158">False</span><span class="sxs-lookup"><span data-stu-id="3eddb-158">false</span></span> | |
| <span data-ttu-id="3eddb-159">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3eddb-159">LicenseUrl</span></span> | <span data-ttu-id="3eddb-160">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3eddb-160">PackageLicenseUrl</span></span> | <span data-ttu-id="3eddb-161">пустой</span><span class="sxs-lookup"><span data-stu-id="3eddb-161">empty</span></span> | |
| <span data-ttu-id="3eddb-162">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3eddb-162">ProjectUrl</span></span> | <span data-ttu-id="3eddb-163">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3eddb-163">PackageProjectUrl</span></span> | <span data-ttu-id="3eddb-164">пустой</span><span class="sxs-lookup"><span data-stu-id="3eddb-164">empty</span></span> | |
| <span data-ttu-id="3eddb-165">IconUrl</span><span class="sxs-lookup"><span data-stu-id="3eddb-165">IconUrl</span></span> | <span data-ttu-id="3eddb-166">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="3eddb-166">PackageIconUrl</span></span> | <span data-ttu-id="3eddb-167">пустой</span><span class="sxs-lookup"><span data-stu-id="3eddb-167">empty</span></span> | |
| <span data-ttu-id="3eddb-168">Теги</span><span class="sxs-lookup"><span data-stu-id="3eddb-168">Tags</span></span> | <span data-ttu-id="3eddb-169">PackageTags</span><span class="sxs-lookup"><span data-stu-id="3eddb-169">PackageTags</span></span> | <span data-ttu-id="3eddb-170">пустой</span><span class="sxs-lookup"><span data-stu-id="3eddb-170">empty</span></span> | <span data-ttu-id="3eddb-171">Теги разделяются точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="3eddb-171">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="3eddb-172">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3eddb-172">ReleaseNotes</span></span> | <span data-ttu-id="3eddb-173">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3eddb-173">PackageReleaseNotes</span></span> | <span data-ttu-id="3eddb-174">пустой</span><span class="sxs-lookup"><span data-stu-id="3eddb-174">empty</span></span> | |
| <span data-ttu-id="3eddb-175">URL-адрес или репозитория</span><span class="sxs-lookup"><span data-stu-id="3eddb-175">Repository/Url</span></span> | <span data-ttu-id="3eddb-176">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="3eddb-176">RepositoryUrl</span></span> | <span data-ttu-id="3eddb-177">пустой</span><span class="sxs-lookup"><span data-stu-id="3eddb-177">empty</span></span> | <span data-ttu-id="3eddb-178">URL-адрес репозитория используется для клонирования или получения исходного кода.</span><span class="sxs-lookup"><span data-stu-id="3eddb-178">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="3eddb-179">Пример: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="3eddb-179">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="3eddb-180">Тип или репозитория</span><span class="sxs-lookup"><span data-stu-id="3eddb-180">Repository/Type</span></span> | <span data-ttu-id="3eddb-181">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="3eddb-181">RepositoryType</span></span> | <span data-ttu-id="3eddb-182">пустой</span><span class="sxs-lookup"><span data-stu-id="3eddb-182">empty</span></span> | <span data-ttu-id="3eddb-183">Тип репозитория.</span><span class="sxs-lookup"><span data-stu-id="3eddb-183">Repository type.</span></span> <span data-ttu-id="3eddb-184">Примеры: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="3eddb-184">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="3eddb-185">Репозиторий и ветвь</span><span class="sxs-lookup"><span data-stu-id="3eddb-185">Repository/Branch</span></span> | <span data-ttu-id="3eddb-186">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="3eddb-186">RepositoryBranch</span></span> | <span data-ttu-id="3eddb-187">пустой</span><span class="sxs-lookup"><span data-stu-id="3eddb-187">empty</span></span> | <span data-ttu-id="3eddb-188">Сведения о ветви необязательно репозитории.</span><span class="sxs-lookup"><span data-stu-id="3eddb-188">Optional repository branch information.</span></span> <span data-ttu-id="3eddb-189">*RepositoryUrl* также необходимо указать для этого свойства для включения.</span><span class="sxs-lookup"><span data-stu-id="3eddb-189">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="3eddb-190">Пример: *master* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="3eddb-190">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="3eddb-191">Репозитории/фиксации</span><span class="sxs-lookup"><span data-stu-id="3eddb-191">Repository/Commit</span></span> | <span data-ttu-id="3eddb-192">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="3eddb-192">RepositoryCommit</span></span> | <span data-ttu-id="3eddb-193">пустой</span><span class="sxs-lookup"><span data-stu-id="3eddb-193">empty</span></span> | <span data-ttu-id="3eddb-194">Необязательный репозитория commit или изменений, чтобы указать, что источник пакета было создано.</span><span class="sxs-lookup"><span data-stu-id="3eddb-194">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="3eddb-195">*RepositoryUrl* также необходимо указать для этого свойства для включения.</span><span class="sxs-lookup"><span data-stu-id="3eddb-195">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="3eddb-196">Пример: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="3eddb-196">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="3eddb-197">PackageType</span><span class="sxs-lookup"><span data-stu-id="3eddb-197">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="3eddb-198">Сводка</span><span class="sxs-lookup"><span data-stu-id="3eddb-198">Summary</span></span> | <span data-ttu-id="3eddb-199">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="3eddb-199">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="3eddb-200">Входные данные целевого объекта pack</span><span class="sxs-lookup"><span data-stu-id="3eddb-200">pack target inputs</span></span>

- <span data-ttu-id="3eddb-201">IsPackable</span><span class="sxs-lookup"><span data-stu-id="3eddb-201">IsPackable</span></span>
- <span data-ttu-id="3eddb-202">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="3eddb-202">PackageVersion</span></span>
- <span data-ttu-id="3eddb-203">PackageId</span><span class="sxs-lookup"><span data-stu-id="3eddb-203">PackageId</span></span>
- <span data-ttu-id="3eddb-204">Authors</span><span class="sxs-lookup"><span data-stu-id="3eddb-204">Authors</span></span>
- <span data-ttu-id="3eddb-205">Описание</span><span class="sxs-lookup"><span data-stu-id="3eddb-205">Description</span></span>
- <span data-ttu-id="3eddb-206">Copyright</span><span class="sxs-lookup"><span data-stu-id="3eddb-206">Copyright</span></span>
- <span data-ttu-id="3eddb-207">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3eddb-207">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="3eddb-208">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="3eddb-208">DevelopmentDependency</span></span>
- <span data-ttu-id="3eddb-209">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3eddb-209">PackageLicenseUrl</span></span>
- <span data-ttu-id="3eddb-210">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3eddb-210">PackageProjectUrl</span></span>
- <span data-ttu-id="3eddb-211">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="3eddb-211">PackageIconUrl</span></span>
- <span data-ttu-id="3eddb-212">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3eddb-212">PackageReleaseNotes</span></span>
- <span data-ttu-id="3eddb-213">PackageTags</span><span class="sxs-lookup"><span data-stu-id="3eddb-213">PackageTags</span></span>
- <span data-ttu-id="3eddb-214">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="3eddb-214">PackageOutputPath</span></span>
- <span data-ttu-id="3eddb-215">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="3eddb-215">IncludeSymbols</span></span>
- <span data-ttu-id="3eddb-216">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="3eddb-216">IncludeSource</span></span>
- <span data-ttu-id="3eddb-217">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="3eddb-217">PackageTypes</span></span>
- <span data-ttu-id="3eddb-218">IsTool</span><span class="sxs-lookup"><span data-stu-id="3eddb-218">IsTool</span></span>
- <span data-ttu-id="3eddb-219">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="3eddb-219">RepositoryUrl</span></span>
- <span data-ttu-id="3eddb-220">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="3eddb-220">RepositoryType</span></span>
- <span data-ttu-id="3eddb-221">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="3eddb-221">RepositoryBranch</span></span>
- <span data-ttu-id="3eddb-222">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="3eddb-222">RepositoryCommit</span></span>
- <span data-ttu-id="3eddb-223">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="3eddb-223">NoPackageAnalysis</span></span>
- <span data-ttu-id="3eddb-224">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="3eddb-224">MinClientVersion</span></span>
- <span data-ttu-id="3eddb-225">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="3eddb-225">IncludeBuildOutput</span></span>
- <span data-ttu-id="3eddb-226">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="3eddb-226">IncludeContentInPack</span></span>
- <span data-ttu-id="3eddb-227">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="3eddb-227">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="3eddb-228">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="3eddb-228">ContentTargetFolders</span></span>
- <span data-ttu-id="3eddb-229">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="3eddb-229">NuspecFile</span></span>
- <span data-ttu-id="3eddb-230">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="3eddb-230">NuspecBasePath</span></span>
- <span data-ttu-id="3eddb-231">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="3eddb-231">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="3eddb-232">Сценарии использования pack</span><span class="sxs-lookup"><span data-stu-id="3eddb-232">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="3eddb-233">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="3eddb-233">PackageIconUrl</span></span>

<span data-ttu-id="3eddb-234">В процессе изменения для [NuGet проблема 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` в конечном итоге будет изменено на `PackageIconUri` и может быть относительный путь к файлу значка, который будет включен в корне полученный пакет.</span><span class="sxs-lookup"><span data-stu-id="3eddb-234">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="3eddb-235">Выходные сборки</span><span class="sxs-lookup"><span data-stu-id="3eddb-235">Output assemblies</span></span>

<span data-ttu-id="3eddb-236">`nuget pack` копирует выходные файлы с расширениями `.exe`, `.dll`, `.xml`, `.winmd`, `.json` и `.pri`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-236">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="3eddb-237">Копируемые выходные файлы зависят от того, что MSBuild предоставляет из целевого объекта `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-237">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="3eddb-238">Существует два свойства MSBuild, которые можно использовать в файле проекта или командной строке для управления местом назначения для выходных сборок:</span><span class="sxs-lookup"><span data-stu-id="3eddb-238">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="3eddb-239">`IncludeBuildOutput`: логическое значение, определяющее, следует ли включать выходные сборки в пакете.</span><span class="sxs-lookup"><span data-stu-id="3eddb-239">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="3eddb-240">`BuildOutputTargetFolder`: указывает папку, куда следует помещать выходные сборки.</span><span class="sxs-lookup"><span data-stu-id="3eddb-240">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="3eddb-241">Выходные сборки (и другие выходные файлы) копируются в соответствующие папки платформы.</span><span class="sxs-lookup"><span data-stu-id="3eddb-241">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="3eddb-242">Ссылки на пакеты</span><span class="sxs-lookup"><span data-stu-id="3eddb-242">Package references</span></span>

<span data-ttu-id="3eddb-243">См. раздел [Ссылки на пакеты в файлах проекта](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="3eddb-243">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="3eddb-244">Перекрестные ссылки между проектами</span><span class="sxs-lookup"><span data-stu-id="3eddb-244">Project to project references</span></span>

<span data-ttu-id="3eddb-245">Перекрестные ссылки между проектами по умолчанию считаются ссылками на пакет NuGet, например:</span><span class="sxs-lookup"><span data-stu-id="3eddb-245">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="3eddb-246">Вы также можете добавить в ссылку на проект следующие метаданные:</span><span class="sxs-lookup"><span data-stu-id="3eddb-246">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="3eddb-247">Включение содержимого в пакет</span><span class="sxs-lookup"><span data-stu-id="3eddb-247">Including content in a package</span></span>

<span data-ttu-id="3eddb-248">Чтобы включить содержимое, добавьте дополнительные метаданные для существующего элемента `<Content>`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-248">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="3eddb-249">По умолчанию все данные типа "Content" включаются в пакет, если только вы не переопределите такое поведение с помощью записей, аналогичных следующим:</span><span class="sxs-lookup"><span data-stu-id="3eddb-249">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="3eddb-250">По умолчанию все данные добавляются в корень папки `content` и `contentFiles\any\<target_framework>` в пакете и сохраняют относительную структуру папок, если только не указан путь к пакету:</span><span class="sxs-lookup"><span data-stu-id="3eddb-250">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="3eddb-251">Если требуется скопировать все содержимое только в определенные корневые папки (вместо `content` и `contentFiles`), можно использовать свойство MSBuild `ContentTargetFolders`, которое по умолчанию имеет значение "content;contentFiles", но может принимать любые другие имена папок.</span><span class="sxs-lookup"><span data-stu-id="3eddb-251">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="3eddb-252">Обратите внимание, если указать "contentFiles" в `ContentTargetFolders`, файлы помещаются в `contentFiles\any\<target_framework>` или `contentFiles\<language>\<target_framework>` в зависимости от `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-252">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="3eddb-253">`PackagePath` может быть набором целевых путей, разделенных точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="3eddb-253">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="3eddb-254">Если указан пустой путь к пакету, файл добавляется в корневой каталог пакета.</span><span class="sxs-lookup"><span data-stu-id="3eddb-254">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="3eddb-255">Например, следующий код добавляет `libuv.txt` в `content\myfiles`, `content\samples` и корневой каталог пакета:</span><span class="sxs-lookup"><span data-stu-id="3eddb-255">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="3eddb-256">Имеется также свойство MSBuild `$(IncludeContentInPack)`, которое по умолчанию равно `true`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-256">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="3eddb-257">Если оно имеет значение `false` для какого-либо проекта, то содержимое этого проекта не включается в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="3eddb-257">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="3eddb-258">Другие относящиеся к pack метаданные, которые можно задать для любого из указанных выше элементов, включают ```<PackageCopyToOutput>``` и ```<PackageFlatten>```, задающие значения ```CopyToOutput``` и ```Flatten``` для записи ```contentFiles``` в выходном файле NUSPEC.</span><span class="sxs-lookup"><span data-stu-id="3eddb-258">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="3eddb-259">Кроме элементов содержимого, метаданные `<Pack>` и `<PackagePath>` также можно задать для файлов с действием сборки Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource или None.</span><span class="sxs-lookup"><span data-stu-id="3eddb-259">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="3eddb-260">Чтобы объект pack добавил имя файла в путь к пакету при использовании стандартных масок, путь к пакету должен заканчиваться символом разделителя папок, в противном случае этот путь считается полным путем, включающим имя файла.</span><span class="sxs-lookup"><span data-stu-id="3eddb-260">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="3eddb-261">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="3eddb-261">IncludeSymbols</span></span>

<span data-ttu-id="3eddb-262">При использовании `MSBuild /t:pack /p:IncludeSymbols=true` соответствующие файлы `.pdb` копируются вместе с другими выходными файлами (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="3eddb-262">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="3eddb-263">Обратите внимание, что при задании `IncludeSymbols=true` создается обычный пакет *и* пакет символов.</span><span class="sxs-lookup"><span data-stu-id="3eddb-263">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="3eddb-264">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="3eddb-264">IncludeSource</span></span>

<span data-ttu-id="3eddb-265">Аналогично `IncludeSymbols`, только копирует исходные файлы вместе с файлами `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-265">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="3eddb-266">Все файлы типа `Compile` копируются в `src\<ProjectName>\` с сохранением относительной структуры папок в итоговом пакете.</span><span class="sxs-lookup"><span data-stu-id="3eddb-266">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="3eddb-267">То же самое происходит с исходными файлами любого `ProjectReference`, у которого `TreatAsPackageReference` имеет значение `false`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-267">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="3eddb-268">Если файл типа Compile находится вне папки проекта, он просто добавляется в `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-268">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="3eddb-269">IsTool</span><span class="sxs-lookup"><span data-stu-id="3eddb-269">IsTool</span></span>

<span data-ttu-id="3eddb-270">При использовании `MSBuild /t:pack /p:IsTool=true` все выходные файлы, как указано в сценарии [Выходные сборки](#output-assemblies), копируются в папку `tools` вместо папки `lib`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-270">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="3eddb-271">Обратите внимание, что это свойство отличается от `DotNetCliTool`, которое указывается путем задания `PackageType` в файле `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-271">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="3eddb-272">Упаковка с помощью NUSPEC</span><span class="sxs-lookup"><span data-stu-id="3eddb-272">Packing using a .nuspec</span></span>

<span data-ttu-id="3eddb-273">Можно использовать `.nuspec` пакет проекта, при условии, что у вас есть файл проекта SDK для импорта файла `NuGet.Build.Tasks.Pack.targets` , чтобы задача пакета могут быть выполнены.</span><span class="sxs-lookup"><span data-stu-id="3eddb-273">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="3eddb-274">По-прежнему необходимо восстановить проект, прежде чем можно упаковать nuspec-файла.</span><span class="sxs-lookup"><span data-stu-id="3eddb-274">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="3eddb-275">Требуемая версия .NET framework в файл проекта не имеет значения и не используется, когда при помощи nuspec.</span><span class="sxs-lookup"><span data-stu-id="3eddb-275">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="3eddb-276">Следующие три свойства MSBuild связаны с упаковкой с помощью `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="3eddb-276">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="3eddb-277">`NuspecFile`: относительный или абсолютный путь к файлу `.nuspec`, используемому для упаковки.</span><span class="sxs-lookup"><span data-stu-id="3eddb-277">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="3eddb-278">`NuspecProperties`: список разделенных точками с запятой пар "ключ-значение".</span><span class="sxs-lookup"><span data-stu-id="3eddb-278">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="3eddb-279">Из-за особенностей работы анализа в командной строке MSBuild несколько свойств нужно указать следующим образом: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-279">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="3eddb-280">`NuspecBasePath`: базовый путь для файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-280">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="3eddb-281">Если вы используете `dotnet.exe` для упаковки проекта, воспользуйтесь командой, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="3eddb-281">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="3eddb-282">Если вы используете MSBuild для упаковки проекта, воспользуйтесь командой, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="3eddb-282">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="3eddb-283">Обратите внимание на то, что упаковки nuspec с помощью dotnet.exe или msbuild также приводит к сборке проекта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3eddb-283">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="3eddb-284">Этого можно избежать путем передачи ```--no-build``` свойства dotnet.exe, что равносильно параметр ```<NoBuild>true</NoBuild> ``` в файле проекта, а также параметр ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` в файле проекта</span><span class="sxs-lookup"><span data-stu-id="3eddb-284">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="3eddb-285">Является примером csproj-файле для упаковки nuspec-файла:</span><span class="sxs-lookup"><span data-stu-id="3eddb-285">An example of a csproj file to pack a nuspec file is:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="3eddb-286">Дополнительные точки расширения для создания настраиваемого пакета</span><span class="sxs-lookup"><span data-stu-id="3eddb-286">Advanced extension points to create customized package</span></span>

<span data-ttu-id="3eddb-287">`pack` Целевой предоставляет две точки расширения, которые выполняются в конкретную сборку внутреннего, target framework.</span><span class="sxs-lookup"><span data-stu-id="3eddb-287">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="3eddb-288">Включая target framework конкретного содержимого и сборки в пакет поддержки точек расширения:</span><span class="sxs-lookup"><span data-stu-id="3eddb-288">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="3eddb-289">`TargetsForTfmSpecificBuildOutput` целевой: использование для файлов внутри `lib` или папки, заданные с помощью `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-289">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="3eddb-290">`TargetsForTfmSpecificContentInPackage` целевой: использование для файлов за пределами `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-290">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="3eddb-291">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="3eddb-291">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="3eddb-292">Запишите пользовательский целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificBuildOutput)` свойство.</span><span class="sxs-lookup"><span data-stu-id="3eddb-292">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="3eddb-293">Для всех файлов, которые необходимо перевести в `BuildOutputTargetFolder` (по умолчанию lib), целевой объект должен записывать эти файлы в ItemGroup `BuildOutputInPackage` и задайте следующие значения метаданных:</span><span class="sxs-lookup"><span data-stu-id="3eddb-293">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="3eddb-294">`FinalOutputPath`: Абсолютный путь файла. Если не указано, удостоверение используется для оценки исходный путь.</span><span class="sxs-lookup"><span data-stu-id="3eddb-294">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="3eddb-295">`TargetPath`: (Необязательно) задайте когда этот файл необходимо перейти в подпапку в `lib\<TargetFramework>` , например вспомогательные сборки, который выходит в своих папках соответствующего языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="3eddb-295">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="3eddb-296">По умолчанию используется имя файла.</span><span class="sxs-lookup"><span data-stu-id="3eddb-296">Defaults to the name of the file.</span></span>

<span data-ttu-id="3eddb-297">Пример</span><span class="sxs-lookup"><span data-stu-id="3eddb-297">Example:</span></span>

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="3eddb-298">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="3eddb-298">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="3eddb-299">Запишите пользовательский целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificContentInPackage)` свойство.</span><span class="sxs-lookup"><span data-stu-id="3eddb-299">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="3eddb-300">Для всех файлов для включения в пакет целевой объект должен записывать эти файлы в ItemGroup `TfmSpecificPackageFile` и задайте следующие необязательные метаданные:</span><span class="sxs-lookup"><span data-stu-id="3eddb-300">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="3eddb-301">`PackagePath`: Путь, где должен находиться файл выходных данных в пакете.</span><span class="sxs-lookup"><span data-stu-id="3eddb-301">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="3eddb-302">NuGet выдает предупреждение, если более одного файла добавляется один и тот же путь пакета.</span><span class="sxs-lookup"><span data-stu-id="3eddb-302">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="3eddb-303">`BuildAction`: Действие построения файла является обязательным, только если задан допустимый путь в `contentFiles` папки.</span><span class="sxs-lookup"><span data-stu-id="3eddb-303">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="3eddb-304">По умолчанию на «Нет».</span><span class="sxs-lookup"><span data-stu-id="3eddb-304">Defaults to "None".</span></span>

<span data-ttu-id="3eddb-305">Пример:</span><span class="sxs-lookup"><span data-stu-id="3eddb-305">An example:</span></span>
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name=""CustomContentTarget"">
  <ItemGroup>
    <TfmSpecificPackageFile Include=""abc.txt"">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include=""Extensions/ext.txt"" Condition=""'$(TargetFramework)' == 'net46'"">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a><span data-ttu-id="3eddb-306">Целевой объект restore</span><span class="sxs-lookup"><span data-stu-id="3eddb-306">restore target</span></span>

<span data-ttu-id="3eddb-307">`MSBuild /t:restore` (который `nuget restore` и `dotnet restore` используют с проектами .NET Core) восстанавливает пакеты, на которые ссылается файл проекта:</span><span class="sxs-lookup"><span data-stu-id="3eddb-307">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="3eddb-308">Чтение перекрестных ссылок между проектами.</span><span class="sxs-lookup"><span data-stu-id="3eddb-308">Read all project to project references</span></span>
1. <span data-ttu-id="3eddb-309">Чтение свойств проекта, чтобы найти промежуточную папку и целевые платформы.</span><span class="sxs-lookup"><span data-stu-id="3eddb-309">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="3eddb-310">Передача данных MSBuild в NuGet.Build.Tasks.dll.</span><span class="sxs-lookup"><span data-stu-id="3eddb-310">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="3eddb-311">Запуск восстановления.</span><span class="sxs-lookup"><span data-stu-id="3eddb-311">Run restore</span></span>
1. <span data-ttu-id="3eddb-312">Скачивание пакетов.</span><span class="sxs-lookup"><span data-stu-id="3eddb-312">Download packages</span></span>
1. <span data-ttu-id="3eddb-313">Запись файла ресурсов, целевых объектов и свойств.</span><span class="sxs-lookup"><span data-stu-id="3eddb-313">Write assets file, targets, and props</span></span>

<span data-ttu-id="3eddb-314">`restore` Целевой works **только** для проектов, в формате PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3eddb-314">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="3eddb-315">Это осуществляется **не** подходит для проектов с помощью `packages.config` форматирования; используйте [восстановление nuget](../tools/cli-ref-restore.md) вместо.</span><span class="sxs-lookup"><span data-stu-id="3eddb-315">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="3eddb-316">Свойства восстановления</span><span class="sxs-lookup"><span data-stu-id="3eddb-316">Restore properties</span></span>

<span data-ttu-id="3eddb-317">Дополнительные параметры восстановления могут поступать из свойств MSBuild в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="3eddb-317">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="3eddb-318">Значения также можно задать из командной строки с помощью параметра `/p:` (см. примеры ниже).</span><span class="sxs-lookup"><span data-stu-id="3eddb-318">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="3eddb-319">Свойство.</span><span class="sxs-lookup"><span data-stu-id="3eddb-319">Property</span></span> | <span data-ttu-id="3eddb-320">Описание</span><span class="sxs-lookup"><span data-stu-id="3eddb-320">Description</span></span> |
|--------|--------|
| <span data-ttu-id="3eddb-321">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="3eddb-321">RestoreSources</span></span> | <span data-ttu-id="3eddb-322">Разделенный точками с запятой список источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="3eddb-322">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="3eddb-323">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="3eddb-323">RestorePackagesPath</span></span> | <span data-ttu-id="3eddb-324">Путь к папке пакетов пользователя.</span><span class="sxs-lookup"><span data-stu-id="3eddb-324">User packages folder path.</span></span> |
| <span data-ttu-id="3eddb-325">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="3eddb-325">RestoreDisableParallel</span></span> | <span data-ttu-id="3eddb-326">Ограничение скачиваний до одного за раз.</span><span class="sxs-lookup"><span data-stu-id="3eddb-326">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="3eddb-327">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="3eddb-327">RestoreConfigFile</span></span> | <span data-ttu-id="3eddb-328">Путь к применяемому файлу `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-328">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="3eddb-329">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="3eddb-329">RestoreNoCache</span></span> | <span data-ttu-id="3eddb-330">Если значение равно true, позволяет избежать использования кэшированных пакетов.</span><span class="sxs-lookup"><span data-stu-id="3eddb-330">If true, avoids using cached packages.</span></span> <span data-ttu-id="3eddb-331">В разделе [управление глобального пакетами и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="3eddb-331">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="3eddb-332">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="3eddb-332">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="3eddb-333">Если значение равно true, нерабочие или отсутствующие источники пакетов игнорируются.</span><span class="sxs-lookup"><span data-stu-id="3eddb-333">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="3eddb-334">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="3eddb-334">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="3eddb-335">Путь к `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-335">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="3eddb-336">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="3eddb-336">RestoreGraphProjectInput</span></span> | <span data-ttu-id="3eddb-337">Разделенный точками с запятой список проектов для восстановления, который должен содержать абсолютные пути.</span><span class="sxs-lookup"><span data-stu-id="3eddb-337">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="3eddb-338">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="3eddb-338">RestoreOutputPath</span></span> | <span data-ttu-id="3eddb-339">Выходная папка, по умолчанию используется `obj`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-339">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="3eddb-340">Примеры</span><span class="sxs-lookup"><span data-stu-id="3eddb-340">Examples</span></span>

<span data-ttu-id="3eddb-341">Командная строка:</span><span class="sxs-lookup"><span data-stu-id="3eddb-341">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="3eddb-342">Файл проекта:</span><span class="sxs-lookup"><span data-stu-id="3eddb-342">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="3eddb-343">Выходные данные восстановления</span><span class="sxs-lookup"><span data-stu-id="3eddb-343">Restore outputs</span></span>

<span data-ttu-id="3eddb-344">Операция восстановления создает в папке сборки `obj` следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="3eddb-344">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="3eddb-345">Файл</span><span class="sxs-lookup"><span data-stu-id="3eddb-345">File</span></span> | <span data-ttu-id="3eddb-346">Описание</span><span class="sxs-lookup"><span data-stu-id="3eddb-346">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="3eddb-347">Содержит граф зависимостей все ссылки на пакет.</span><span class="sxs-lookup"><span data-stu-id="3eddb-347">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="3eddb-348">Ссылки на свойства MSBuild, содержащиеся в пакетах.</span><span class="sxs-lookup"><span data-stu-id="3eddb-348">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="3eddb-349">Ссылки на целевые объекты MSBuild, содержащиеся в пакетах.</span><span class="sxs-lookup"><span data-stu-id="3eddb-349">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="3eddb-350">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="3eddb-350">PackageTargetFallback</span></span>

<span data-ttu-id="3eddb-351">Элемент `PackageTargetFallback` позволяет указать набор совместимых целевых объектов, которые следует использовать при восстановлении пакетов.</span><span class="sxs-lookup"><span data-stu-id="3eddb-351">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="3eddb-352">Он разрешает пакетам, использующим dotnet [TxM](../reference/target-frameworks.md), взаимодействовать с совместимыми пакетами, которые не объявляют dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="3eddb-352">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="3eddb-353">Таким образом, если в проекте используется dotnet TxM, все пакеты, от которых вы зависите, должны также содержать dotnet TxM. В противном случае нужно добавить `<PackageTargetFallback>` в проект, чтобы обеспечить совместимость с платформами, отличными от dotnet.</span><span class="sxs-lookup"><span data-stu-id="3eddb-353">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="3eddb-354">Например, если в проекте используется `netstandard1.6` TxM, а зависимый пакет содержит только `lib/net45/a.dll` и `lib/portable-net45+win81/a.dll`, то сборка проекта завершится со сбоем.</span><span class="sxs-lookup"><span data-stu-id="3eddb-354">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="3eddb-355">Если вы хотите использовать вторую библиотеку DLL, можете добавить `PackageTargetFallback` следующим образом, чтобы обозначить совместимость библиотеки DLL `portable-net45+win81`:</span><span class="sxs-lookup"><span data-stu-id="3eddb-355">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="3eddb-356">Чтобы объявить откат для всех целевых объектов в проекте, оставьте атрибут `Condition`.</span><span class="sxs-lookup"><span data-stu-id="3eddb-356">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="3eddb-357">Кроме того, можно расширить существующий `PackageTargetFallback`, включив `$(PackageTargetFallback)`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="3eddb-357">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="3eddb-358">Замена одной библиотеки из графа восстановления</span><span class="sxs-lookup"><span data-stu-id="3eddb-358">Replacing one library from a restore graph</span></span>

<span data-ttu-id="3eddb-359">Если операция восстановления предоставляет неправильную сборку, вы можете исключить значение по умолчанию для этого пакета, заменив его своим значением.</span><span class="sxs-lookup"><span data-stu-id="3eddb-359">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="3eddb-360">Первый с `PackageReference` верхнего уровня, исключите все ресурсы:</span><span class="sxs-lookup"><span data-stu-id="3eddb-360">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="3eddb-361">После этого добавьте собственную ссылку на соответствующую локальную копию библиотеки DLL:</span><span class="sxs-lookup"><span data-stu-id="3eddb-361">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
