---
title: "Объекты pack и restore NuGet в качестве целевых объектов MSBuild | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Объекты pack и restore NuGet могут выступать непосредственно в качестве целевых объектов MSBuild в NuGet 4.0+."
keywords: "NuGet и MSBuild, целевой объект pack NuGet, целевой объект restore NuGet"
ms.reviewer:
- karann-msft
ms.openlocfilehash: bb0ade1b0f5f81d7c8822d3c2b2f9dd45745fb8d
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="45b4e-104">Объекты pack и restore NuGet в качестве целевых объектов MSBuild</span><span class="sxs-lookup"><span data-stu-id="45b4e-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="45b4e-105">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="45b4e-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="45b4e-106">Благодаря формату PackageReference в NuGet 4.0 и более поздних версиях все метаданные манифеста могут храниться прямо в файле проекта, не требуя использования отдельного файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="45b4e-107">При использовании MSBuild 15.1+ NuGet также является привилегированным компонентом MSBuild с целевыми объектами `pack` и `restore`, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="45b4e-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="45b4e-108">Эти целевые объекты позволяют работать с NuGet, как с любой другой задачей или другим целевым объектом MSBuild.</span><span class="sxs-lookup"><span data-stu-id="45b4e-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="45b4e-109">(Для NuGet 3.x и более ранних версий можно использовать команды [pack](../tools/cli-ref-pack.md) и [restore](../tools/cli-ref-restore.md) в NuGet CLI.)</span><span class="sxs-lookup"><span data-stu-id="45b4e-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="45b4e-110">Порядок сборки целевого объекта</span><span class="sxs-lookup"><span data-stu-id="45b4e-110">Target build order</span></span>

<span data-ttu-id="45b4e-111">Так как `pack` и `restore` являются целевыми объектами MSBuild, вы можете обращаться к ним для улучшения рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="45b4e-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="45b4e-112">Например, предположим, что вам нужно скопировать пакет в общую сетевую папку после его упаковки.</span><span class="sxs-lookup"><span data-stu-id="45b4e-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="45b4e-113">Это можно сделать, добавив следующий код в файл проекта:</span><span class="sxs-lookup"><span data-stu-id="45b4e-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="45b4e-114">Аналогичным образом, вы можете создать задачу MSBuild и собственный целевой объект и использовать свойства NuGet в этой задаче MSBuild.</span><span class="sxs-lookup"><span data-stu-id="45b4e-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="45b4e-115">Целевой объект pack</span><span class="sxs-lookup"><span data-stu-id="45b4e-115">pack target</span></span>

<span data-ttu-id="45b4e-116">Для проектов .NET Standard в формате PackageReference, с помощью `msbuild /t:pack` рисует входные данные из файла проекта для создания пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="45b4e-116">For .NET Standard projects using the PackageReference format, using `msbuild /t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="45b4e-117">В следующей таблице описываются свойства MSBuild, которые можно добавить в файл проекта в первом узле `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="45b4e-118">Эти изменения легко внести в Visual Studio 2017 и более поздней версии, щелкнув проект правой кнопкой мыши и выбрав пункт **Изменить {project_name}**.</span><span class="sxs-lookup"><span data-stu-id="45b4e-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="45b4e-119">Для удобства таблица упорядочена по эквивалентным свойствам в [файле `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="45b4e-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="45b4e-120">Обратите внимание, что свойства `Owners` и `Summary` из `.nuspec` не поддерживаются в MSBuild.</span><span class="sxs-lookup"><span data-stu-id="45b4e-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="45b4e-121">Значение атрибута или NuSpec</span><span class="sxs-lookup"><span data-stu-id="45b4e-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="45b4e-122">Свойство MSBuild</span><span class="sxs-lookup"><span data-stu-id="45b4e-122">MSBuild Property</span></span> | <span data-ttu-id="45b4e-123">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="45b4e-123">Default</span></span> | <span data-ttu-id="45b4e-124">Примечания</span><span class="sxs-lookup"><span data-stu-id="45b4e-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="45b4e-125">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="45b4e-125">Id</span></span> | <span data-ttu-id="45b4e-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="45b4e-126">PackageId</span></span> | <span data-ttu-id="45b4e-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="45b4e-127">AssemblyName</span></span> | <span data-ttu-id="45b4e-128">$(AssemblyName) из MSBuild</span><span class="sxs-lookup"><span data-stu-id="45b4e-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="45b4e-129">Версия</span><span class="sxs-lookup"><span data-stu-id="45b4e-129">Version</span></span> | <span data-ttu-id="45b4e-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="45b4e-130">PackageVersion</span></span> | <span data-ttu-id="45b4e-131">Версия</span><span class="sxs-lookup"><span data-stu-id="45b4e-131">Version</span></span> | <span data-ttu-id="45b4e-132">Это значение совместимо с SemVer, например "1.0.0", "1.0.0-beta" или "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="45b4e-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="45b4e-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="45b4e-133">VersionPrefix</span></span> | <span data-ttu-id="45b4e-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="45b4e-134">PackageVersionPrefix</span></span> | <span data-ttu-id="45b4e-135">пустой</span><span class="sxs-lookup"><span data-stu-id="45b4e-135">empty</span></span> | <span data-ttu-id="45b4e-136">Задав PackageVersion, вы перезапишите PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="45b4e-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="45b4e-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="45b4e-137">VersionSuffix</span></span> | <span data-ttu-id="45b4e-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="45b4e-138">PackageVersionSuffix</span></span> | <span data-ttu-id="45b4e-139">пустой</span><span class="sxs-lookup"><span data-stu-id="45b4e-139">empty</span></span> | <span data-ttu-id="45b4e-140">$(VersionSuffix) из MSBuild.</span><span class="sxs-lookup"><span data-stu-id="45b4e-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="45b4e-141">Задав PackageVersion, вы перезапишите PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="45b4e-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="45b4e-142">Authors</span><span class="sxs-lookup"><span data-stu-id="45b4e-142">Authors</span></span> | <span data-ttu-id="45b4e-143">Authors</span><span class="sxs-lookup"><span data-stu-id="45b4e-143">Authors</span></span> | <span data-ttu-id="45b4e-144">Имя текущего пользователя</span><span class="sxs-lookup"><span data-stu-id="45b4e-144">Username of the current user</span></span> | |
| <span data-ttu-id="45b4e-145">Владельцы</span><span class="sxs-lookup"><span data-stu-id="45b4e-145">Owners</span></span> | <span data-ttu-id="45b4e-146">Н/Д</span><span class="sxs-lookup"><span data-stu-id="45b4e-146">N/A</span></span> | <span data-ttu-id="45b4e-147">Не существует в NuSpec</span><span class="sxs-lookup"><span data-stu-id="45b4e-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="45b4e-148">Заголовок</span><span class="sxs-lookup"><span data-stu-id="45b4e-148">Title</span></span> | <span data-ttu-id="45b4e-149">Заголовок</span><span class="sxs-lookup"><span data-stu-id="45b4e-149">Title</span></span> | <span data-ttu-id="45b4e-150">Идентификатор пакета</span><span class="sxs-lookup"><span data-stu-id="45b4e-150">The PackageId</span></span>| |
| <span data-ttu-id="45b4e-151">Описание:</span><span class="sxs-lookup"><span data-stu-id="45b4e-151">Description</span></span> | <span data-ttu-id="45b4e-152">PackageDescription</span><span class="sxs-lookup"><span data-stu-id="45b4e-152">PackageDescription</span></span> | <span data-ttu-id="45b4e-153">"Описание пакета"</span><span class="sxs-lookup"><span data-stu-id="45b4e-153">"Package Description"</span></span> | |
| <span data-ttu-id="45b4e-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="45b4e-154">Copyright</span></span> | <span data-ttu-id="45b4e-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="45b4e-155">Copyright</span></span> | <span data-ttu-id="45b4e-156">пустой</span><span class="sxs-lookup"><span data-stu-id="45b4e-156">empty</span></span> | |
| <span data-ttu-id="45b4e-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="45b4e-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="45b4e-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="45b4e-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="45b4e-159">False</span><span class="sxs-lookup"><span data-stu-id="45b4e-159">false</span></span> | |
| <span data-ttu-id="45b4e-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="45b4e-160">LicenseUrl</span></span> | <span data-ttu-id="45b4e-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="45b4e-161">PackageLicenseUrl</span></span> | <span data-ttu-id="45b4e-162">пустой</span><span class="sxs-lookup"><span data-stu-id="45b4e-162">empty</span></span> | |
| <span data-ttu-id="45b4e-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="45b4e-163">ProjectUrl</span></span> | <span data-ttu-id="45b4e-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="45b4e-164">PackageProjectUrl</span></span> | <span data-ttu-id="45b4e-165">пустой</span><span class="sxs-lookup"><span data-stu-id="45b4e-165">empty</span></span> | |
| <span data-ttu-id="45b4e-166">IconUrl</span><span class="sxs-lookup"><span data-stu-id="45b4e-166">IconUrl</span></span> | <span data-ttu-id="45b4e-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="45b4e-167">PackageIconUrl</span></span> | <span data-ttu-id="45b4e-168">пустой</span><span class="sxs-lookup"><span data-stu-id="45b4e-168">empty</span></span> | |
| <span data-ttu-id="45b4e-169">Теги</span><span class="sxs-lookup"><span data-stu-id="45b4e-169">Tags</span></span> | <span data-ttu-id="45b4e-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="45b4e-170">PackageTags</span></span> | <span data-ttu-id="45b4e-171">пустой</span><span class="sxs-lookup"><span data-stu-id="45b4e-171">empty</span></span> | <span data-ttu-id="45b4e-172">Теги разделяются точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="45b4e-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="45b4e-173">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="45b4e-173">ReleaseNotes</span></span> | <span data-ttu-id="45b4e-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="45b4e-174">PackageReleaseNotes</span></span> | <span data-ttu-id="45b4e-175">пустой</span><span class="sxs-lookup"><span data-stu-id="45b4e-175">empty</span></span> | |
| <span data-ttu-id="45b4e-176">URL-адрес или репозитория</span><span class="sxs-lookup"><span data-stu-id="45b4e-176">Repository/Url</span></span> | <span data-ttu-id="45b4e-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="45b4e-177">RepositoryUrl</span></span> | <span data-ttu-id="45b4e-178">пустой</span><span class="sxs-lookup"><span data-stu-id="45b4e-178">empty</span></span> | <span data-ttu-id="45b4e-179">URL-адрес репозитория используется для клонирования или получения исходного кода.</span><span class="sxs-lookup"><span data-stu-id="45b4e-179">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="45b4e-180">Пример: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="45b4e-180">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="45b4e-181">Тип или репозитория</span><span class="sxs-lookup"><span data-stu-id="45b4e-181">Repository/Type</span></span> | <span data-ttu-id="45b4e-182">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="45b4e-182">RepositoryType</span></span> | <span data-ttu-id="45b4e-183">пустой</span><span class="sxs-lookup"><span data-stu-id="45b4e-183">empty</span></span> | <span data-ttu-id="45b4e-184">Тип репозитория.</span><span class="sxs-lookup"><span data-stu-id="45b4e-184">Repository type.</span></span> <span data-ttu-id="45b4e-185">Примеры: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="45b4e-185">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="45b4e-186">Репозиторий и ветвь</span><span class="sxs-lookup"><span data-stu-id="45b4e-186">Repository/Branch</span></span> | <span data-ttu-id="45b4e-187">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="45b4e-187">RepositoryBranch</span></span> | <span data-ttu-id="45b4e-188">пустой</span><span class="sxs-lookup"><span data-stu-id="45b4e-188">empty</span></span> | <span data-ttu-id="45b4e-189">Сведения о ветви необязательно репозитории.</span><span class="sxs-lookup"><span data-stu-id="45b4e-189">Optional repository branch information.</span></span> <span data-ttu-id="45b4e-190">*RepositoryUrl* также необходимо указать для этого свойства для включения.</span><span class="sxs-lookup"><span data-stu-id="45b4e-190">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="45b4e-191">Пример: *master* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="45b4e-191">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="45b4e-192">Репозитории/фиксации</span><span class="sxs-lookup"><span data-stu-id="45b4e-192">Repository/Commit</span></span> | <span data-ttu-id="45b4e-193">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="45b4e-193">RepositoryCommit</span></span> | <span data-ttu-id="45b4e-194">пустой</span><span class="sxs-lookup"><span data-stu-id="45b4e-194">empty</span></span> | <span data-ttu-id="45b4e-195">Необязательный репозитория commit или изменений, чтобы указать, что источник пакета было создано.</span><span class="sxs-lookup"><span data-stu-id="45b4e-195">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="45b4e-196">*RepositoryUrl* также необходимо указать для этого свойства для включения.</span><span class="sxs-lookup"><span data-stu-id="45b4e-196">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="45b4e-197">Пример: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="45b4e-197">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="45b4e-198">PackageType</span><span class="sxs-lookup"><span data-stu-id="45b4e-198">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="45b4e-199">Сводка</span><span class="sxs-lookup"><span data-stu-id="45b4e-199">Summary</span></span> | <span data-ttu-id="45b4e-200">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="45b4e-200">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="45b4e-201">Входные данные целевого объекта pack</span><span class="sxs-lookup"><span data-stu-id="45b4e-201">pack target inputs</span></span>

- <span data-ttu-id="45b4e-202">IsPackable</span><span class="sxs-lookup"><span data-stu-id="45b4e-202">IsPackable</span></span>
- <span data-ttu-id="45b4e-203">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="45b4e-203">PackageVersion</span></span>
- <span data-ttu-id="45b4e-204">PackageId</span><span class="sxs-lookup"><span data-stu-id="45b4e-204">PackageId</span></span>
- <span data-ttu-id="45b4e-205">Authors</span><span class="sxs-lookup"><span data-stu-id="45b4e-205">Authors</span></span>
- <span data-ttu-id="45b4e-206">Описание:</span><span class="sxs-lookup"><span data-stu-id="45b4e-206">Description</span></span>
- <span data-ttu-id="45b4e-207">Copyright</span><span class="sxs-lookup"><span data-stu-id="45b4e-207">Copyright</span></span>
- <span data-ttu-id="45b4e-208">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="45b4e-208">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="45b4e-209">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="45b4e-209">DevelopmentDependency</span></span>
- <span data-ttu-id="45b4e-210">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="45b4e-210">PackageLicenseUrl</span></span>
- <span data-ttu-id="45b4e-211">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="45b4e-211">PackageProjectUrl</span></span>
- <span data-ttu-id="45b4e-212">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="45b4e-212">PackageIconUrl</span></span>
- <span data-ttu-id="45b4e-213">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="45b4e-213">PackageReleaseNotes</span></span>
- <span data-ttu-id="45b4e-214">PackageTags</span><span class="sxs-lookup"><span data-stu-id="45b4e-214">PackageTags</span></span>
- <span data-ttu-id="45b4e-215">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="45b4e-215">PackageOutputPath</span></span>
- <span data-ttu-id="45b4e-216">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="45b4e-216">IncludeSymbols</span></span>
- <span data-ttu-id="45b4e-217">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="45b4e-217">IncludeSource</span></span>
- <span data-ttu-id="45b4e-218">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="45b4e-218">PackageTypes</span></span>
- <span data-ttu-id="45b4e-219">IsTool</span><span class="sxs-lookup"><span data-stu-id="45b4e-219">IsTool</span></span>
- <span data-ttu-id="45b4e-220">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="45b4e-220">RepositoryUrl</span></span>
- <span data-ttu-id="45b4e-221">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="45b4e-221">RepositoryType</span></span>
- <span data-ttu-id="45b4e-222">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="45b4e-222">RepositoryBranch</span></span>
- <span data-ttu-id="45b4e-223">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="45b4e-223">RepositoryCommit</span></span>
- <span data-ttu-id="45b4e-224">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="45b4e-224">NoPackageAnalysis</span></span>
- <span data-ttu-id="45b4e-225">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="45b4e-225">MinClientVersion</span></span>
- <span data-ttu-id="45b4e-226">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="45b4e-226">IncludeBuildOutput</span></span>
- <span data-ttu-id="45b4e-227">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="45b4e-227">IncludeContentInPack</span></span>
- <span data-ttu-id="45b4e-228">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="45b4e-228">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="45b4e-229">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="45b4e-229">ContentTargetFolders</span></span>
- <span data-ttu-id="45b4e-230">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="45b4e-230">NuspecFile</span></span>
- <span data-ttu-id="45b4e-231">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="45b4e-231">NuspecBasePath</span></span>
- <span data-ttu-id="45b4e-232">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="45b4e-232">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="45b4e-233">Сценарии использования pack</span><span class="sxs-lookup"><span data-stu-id="45b4e-233">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="45b4e-234">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="45b4e-234">PackageIconUrl</span></span>

<span data-ttu-id="45b4e-235">В процессе внесения изменения для [вопроса 2582 по NuGet](https://github.com/NuGet/Home/issues/2582) `PackageIconUrl` в конечном итоге будет изменен на `PackageIconUri` и может быть относительным путем к файлу значка, который будет включен в корень итогового пакета.</span><span class="sxs-lookup"><span data-stu-id="45b4e-235">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="45b4e-236">Выходные сборки</span><span class="sxs-lookup"><span data-stu-id="45b4e-236">Output assemblies</span></span>

<span data-ttu-id="45b4e-237">`nuget pack` копирует выходные файлы с расширениями `.exe`, `.dll`, `.xml`, `.winmd`, `.json` и `.pri`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-237">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="45b4e-238">Копируемые выходные файлы зависят от того, что MSBuild предоставляет из целевого объекта `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-238">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="45b4e-239">Существует два свойства MSBuild, которые можно использовать в файле проекта или командной строке для управления местом назначения для выходных сборок:</span><span class="sxs-lookup"><span data-stu-id="45b4e-239">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="45b4e-240">`IncludeBuildOutput`: логическое значение, определяющее, следует ли включать выходные сборки в пакете.</span><span class="sxs-lookup"><span data-stu-id="45b4e-240">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="45b4e-241">`BuildOutputTargetFolder`: указывает папку, куда следует помещать выходные сборки.</span><span class="sxs-lookup"><span data-stu-id="45b4e-241">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="45b4e-242">Выходные сборки (и другие выходные файлы) копируются в соответствующие папки платформы.</span><span class="sxs-lookup"><span data-stu-id="45b4e-242">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="45b4e-243">Ссылки на пакеты</span><span class="sxs-lookup"><span data-stu-id="45b4e-243">Package references</span></span>

<span data-ttu-id="45b4e-244">См. раздел [Ссылки на пакеты в файлах проекта](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="45b4e-244">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="45b4e-245">Перекрестные ссылки между проектами</span><span class="sxs-lookup"><span data-stu-id="45b4e-245">Project to project references</span></span>

<span data-ttu-id="45b4e-246">Перекрестные ссылки между проектами по умолчанию считаются ссылками на пакет NuGet, например:</span><span class="sxs-lookup"><span data-stu-id="45b4e-246">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="45b4e-247">Вы также можете добавить в ссылку на проект следующие метаданные:</span><span class="sxs-lookup"><span data-stu-id="45b4e-247">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="45b4e-248">Включение содержимого в пакет</span><span class="sxs-lookup"><span data-stu-id="45b4e-248">Including content in a package</span></span>

<span data-ttu-id="45b4e-249">Чтобы включить содержимое, добавьте дополнительные метаданные для существующего элемента `<Content>`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-249">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="45b4e-250">По умолчанию все данные типа "Content" включаются в пакет, если только вы не переопределите такое поведение с помощью записей, аналогичных следующим:</span><span class="sxs-lookup"><span data-stu-id="45b4e-250">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="45b4e-251">По умолчанию все данные добавляются в корень папки `content` и `contentFiles\any\<target_framework>` в пакете и сохраняют относительную структуру папок, если только не указан путь к пакету:</span><span class="sxs-lookup"><span data-stu-id="45b4e-251">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="45b4e-252">Если требуется скопировать все содержимое только в определенные корневые папки (вместо `content` и `contentFiles`), можно использовать свойство MSBuild `ContentTargetFolders`, которое по умолчанию имеет значение "content;contentFiles", но может принимать любые другие имена папок.</span><span class="sxs-lookup"><span data-stu-id="45b4e-252">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="45b4e-253">Обратите внимание, если указать "contentFiles" в `ContentTargetFolders`, файлы помещаются в `contentFiles\any\<target_framework>` или `contentFiles\<language>\<target_framework>` в зависимости от `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-253">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="45b4e-254">`PackagePath` может быть набором целевых путей, разделенных точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="45b4e-254">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="45b4e-255">Если указан пустой путь к пакету, файл добавляется в корневой каталог пакета.</span><span class="sxs-lookup"><span data-stu-id="45b4e-255">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="45b4e-256">Например, следующий код добавляет `libuv.txt` в `content\myfiles`, `content\samples` и корневой каталог пакета:</span><span class="sxs-lookup"><span data-stu-id="45b4e-256">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="45b4e-257">Имеется также свойство MSBuild `$(IncludeContentInPack)`, которое по умолчанию равно `true`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-257">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="45b4e-258">Если оно имеет значение `false` для какого-либо проекта, то содержимое этого проекта не включается в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="45b4e-258">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="45b4e-259">Другие относящиеся к pack метаданные, которые можно задать для любого из указанных выше элементов, включают ```<PackageCopyToOutput>``` и ```<PackageFlatten>```, задающие значения ```CopyToOutput``` и ```Flatten``` для записи ```contentFiles``` в выходном файле NUSPEC.</span><span class="sxs-lookup"><span data-stu-id="45b4e-259">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="45b4e-260">Кроме элементов содержимого, метаданные `<Pack>` и `<PackagePath>` также можно задать для файлов с действием сборки Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource или None.</span><span class="sxs-lookup"><span data-stu-id="45b4e-260">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="45b4e-261">Чтобы объект pack добавил имя файла в путь к пакету при использовании стандартных масок, путь к пакету должен заканчиваться символом разделителя папок, в противном случае этот путь считается полным путем, включающим имя файла.</span><span class="sxs-lookup"><span data-stu-id="45b4e-261">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="45b4e-262">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="45b4e-262">IncludeSymbols</span></span>

<span data-ttu-id="45b4e-263">При использовании `MSBuild /t:pack /p:IncludeSymbols=true` соответствующие файлы `.pdb` копируются вместе с другими выходными файлами (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="45b4e-263">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="45b4e-264">Обратите внимание, что при задании `IncludeSymbols=true` создается обычный пакет *и* пакет символов.</span><span class="sxs-lookup"><span data-stu-id="45b4e-264">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="45b4e-265">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="45b4e-265">IncludeSource</span></span>

<span data-ttu-id="45b4e-266">Аналогично `IncludeSymbols`, только копирует исходные файлы вместе с файлами `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-266">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="45b4e-267">Все файлы типа `Compile` копируются в `src\<ProjectName>\` с сохранением относительной структуры папок в итоговом пакете.</span><span class="sxs-lookup"><span data-stu-id="45b4e-267">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="45b4e-268">То же самое происходит с исходными файлами любого `ProjectReference`, у которого `TreatAsPackageReference` имеет значение `false`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-268">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="45b4e-269">Если файл типа Compile находится вне папки проекта, он просто добавляется в `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-269">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="45b4e-270">IsTool</span><span class="sxs-lookup"><span data-stu-id="45b4e-270">IsTool</span></span>

<span data-ttu-id="45b4e-271">При использовании `MSBuild /t:pack /p:IsTool=true` все выходные файлы, как указано в сценарии [Выходные сборки](#output-assemblies), копируются в папку `tools` вместо папки `lib`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-271">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="45b4e-272">Обратите внимание, что это свойство отличается от `DotNetCliTool`, которое указывается путем задания `PackageType` в файле `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-272">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="45b4e-273">Упаковка с помощью NUSPEC</span><span class="sxs-lookup"><span data-stu-id="45b4e-273">Packing using a .nuspec</span></span>

<span data-ttu-id="45b4e-274">Можно использовать `.nuspec` пакет проекта, при условии, что у вас есть файл проекта SDK для импорта файла `NuGet.Build.Tasks.Pack.targets` , чтобы задача пакета могут быть выполнены.</span><span class="sxs-lookup"><span data-stu-id="45b4e-274">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="45b4e-275">По-прежнему необходимо восстановить проект, прежде чем можно упаковать nuspec-файла.</span><span class="sxs-lookup"><span data-stu-id="45b4e-275">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="45b4e-276">Требуемая версия .NET framework в файл проекта не имеет значения и не используется, когда при помощи nuspec.</span><span class="sxs-lookup"><span data-stu-id="45b4e-276">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="45b4e-277">Следующие три свойства MSBuild связаны с упаковкой с помощью `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="45b4e-277">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="45b4e-278">`NuspecFile`: относительный или абсолютный путь к файлу `.nuspec`, используемому для упаковки.</span><span class="sxs-lookup"><span data-stu-id="45b4e-278">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="45b4e-279">`NuspecProperties`: список разделенных точками с запятой пар "ключ-значение".</span><span class="sxs-lookup"><span data-stu-id="45b4e-279">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="45b4e-280">Из-за особенностей работы анализа в командной строке MSBuild несколько свойств нужно указать следующим образом: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-280">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="45b4e-281">`NuspecBasePath`: базовый путь для файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-281">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="45b4e-282">Если вы используете `dotnet.exe` для упаковки проекта, воспользуйтесь командой, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="45b4e-282">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="45b4e-283">Если вы используете MSBuild для упаковки проекта, воспользуйтесь командой, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="45b4e-283">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="45b4e-284">Обратите внимание на то, что упаковки nuspec с помощью dotnet.exe или msbuild также приводит к сборке проекта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="45b4e-284">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="45b4e-285">Этого можно избежать путем передачи ```--no-build``` свойства dotnet.exe, что равносильно параметр ```<NoBuild>true</NoBuild> ``` в файле проекта, а также параметр ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` в файле проекта</span><span class="sxs-lookup"><span data-stu-id="45b4e-285">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="45b4e-286">Является примером csproj-файле для упаковки nuspec-файла:</span><span class="sxs-lookup"><span data-stu-id="45b4e-286">An example of a csproj file to pack a nuspec file is:</span></span>

```
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

## <a name="restore-target"></a><span data-ttu-id="45b4e-287">Целевой объект restore</span><span class="sxs-lookup"><span data-stu-id="45b4e-287">restore target</span></span>

<span data-ttu-id="45b4e-288">`MSBuild /t:restore` (который `nuget restore` и `dotnet restore` используют с проектами .NET Core) восстанавливает пакеты, на которые ссылается файл проекта:</span><span class="sxs-lookup"><span data-stu-id="45b4e-288">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="45b4e-289">Чтение перекрестных ссылок между проектами.</span><span class="sxs-lookup"><span data-stu-id="45b4e-289">Read all project to project references</span></span>
1. <span data-ttu-id="45b4e-290">Чтение свойств проекта, чтобы найти промежуточную папку и целевые платформы.</span><span class="sxs-lookup"><span data-stu-id="45b4e-290">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="45b4e-291">Передача данных MSBuild в NuGet.Build.Tasks.dll.</span><span class="sxs-lookup"><span data-stu-id="45b4e-291">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="45b4e-292">Запуск восстановления.</span><span class="sxs-lookup"><span data-stu-id="45b4e-292">Run restore</span></span>
1. <span data-ttu-id="45b4e-293">Скачивание пакетов.</span><span class="sxs-lookup"><span data-stu-id="45b4e-293">Download packages</span></span>
1. <span data-ttu-id="45b4e-294">Запись файла ресурсов, целевых объектов и свойств.</span><span class="sxs-lookup"><span data-stu-id="45b4e-294">Write assets file, targets, and props</span></span>

<span data-ttu-id="45b4e-295">`restore` Целевой works **только** для проектов, в формате PackageReference.</span><span class="sxs-lookup"><span data-stu-id="45b4e-295">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="45b4e-296">Это осуществляется **не** подходит для проектов с помощью `packages.config` форматирования; используйте [восстановление nuget](../tools/cli-ref-restore.md) вместо.</span><span class="sxs-lookup"><span data-stu-id="45b4e-296">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="45b4e-297">Свойства восстановления</span><span class="sxs-lookup"><span data-stu-id="45b4e-297">Restore properties</span></span>

<span data-ttu-id="45b4e-298">Дополнительные параметры восстановления могут поступать из свойств MSBuild в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="45b4e-298">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="45b4e-299">Значения также можно задать из командной строки с помощью параметра `/p:` (см. примеры ниже).</span><span class="sxs-lookup"><span data-stu-id="45b4e-299">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="45b4e-300">Свойство.</span><span class="sxs-lookup"><span data-stu-id="45b4e-300">Property</span></span> | <span data-ttu-id="45b4e-301">Описание:</span><span class="sxs-lookup"><span data-stu-id="45b4e-301">Description</span></span> |
|--------|--------|
| <span data-ttu-id="45b4e-302">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="45b4e-302">RestoreSources</span></span> | <span data-ttu-id="45b4e-303">Разделенный точками с запятой список источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="45b4e-303">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="45b4e-304">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="45b4e-304">RestorePackagesPath</span></span> | <span data-ttu-id="45b4e-305">Путь к папке пакетов пользователя.</span><span class="sxs-lookup"><span data-stu-id="45b4e-305">User packages folder path.</span></span> |
| <span data-ttu-id="45b4e-306">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="45b4e-306">RestoreDisableParallel</span></span> | <span data-ttu-id="45b4e-307">Ограничение скачиваний до одного за раз.</span><span class="sxs-lookup"><span data-stu-id="45b4e-307">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="45b4e-308">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="45b4e-308">RestoreConfigFile</span></span> | <span data-ttu-id="45b4e-309">Путь к применяемому файлу `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-309">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="45b4e-310">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="45b4e-310">RestoreNoCache</span></span> | <span data-ttu-id="45b4e-311">Если значение равно true, веб-кэш по возможности не используется.</span><span class="sxs-lookup"><span data-stu-id="45b4e-311">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="45b4e-312">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="45b4e-312">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="45b4e-313">Если значение равно true, нерабочие или отсутствующие источники пакетов игнорируются.</span><span class="sxs-lookup"><span data-stu-id="45b4e-313">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="45b4e-314">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="45b4e-314">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="45b4e-315">Путь к `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-315">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="45b4e-316">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="45b4e-316">RestoreGraphProjectInput</span></span> | <span data-ttu-id="45b4e-317">Разделенный точками с запятой список проектов для восстановления, который должен содержать абсолютные пути.</span><span class="sxs-lookup"><span data-stu-id="45b4e-317">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="45b4e-318">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="45b4e-318">RestoreOutputPath</span></span> | <span data-ttu-id="45b4e-319">Выходная папка, по умолчанию используется `obj`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-319">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="45b4e-320">Примеры</span><span class="sxs-lookup"><span data-stu-id="45b4e-320">Examples</span></span>

<span data-ttu-id="45b4e-321">Командная строка:</span><span class="sxs-lookup"><span data-stu-id="45b4e-321">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="45b4e-322">Файл проекта:</span><span class="sxs-lookup"><span data-stu-id="45b4e-322">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="45b4e-323">Выходные данные восстановления</span><span class="sxs-lookup"><span data-stu-id="45b4e-323">Restore outputs</span></span>

<span data-ttu-id="45b4e-324">Операция восстановления создает в папке сборки `obj` следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="45b4e-324">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="45b4e-325">Файл</span><span class="sxs-lookup"><span data-stu-id="45b4e-325">File</span></span> | <span data-ttu-id="45b4e-326">Описание:</span><span class="sxs-lookup"><span data-stu-id="45b4e-326">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="45b4e-327">Раньше назывался `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-327">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="45b4e-328">Ссылки на свойства MSBuild, содержащиеся в пакетах.</span><span class="sxs-lookup"><span data-stu-id="45b4e-328">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="45b4e-329">Ссылки на целевые объекты MSBuild, содержащиеся в пакетах.</span><span class="sxs-lookup"><span data-stu-id="45b4e-329">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="45b4e-330">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="45b4e-330">PackageTargetFallback</span></span>

<span data-ttu-id="45b4e-331">Элемент `PackageTargetFallback` позволяет указать набор совместимых целевых объектов, которые следует использовать при восстановлении пакетов.</span><span class="sxs-lookup"><span data-stu-id="45b4e-331">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="45b4e-332">Он разрешает пакетам, использующим dotnet [TxM](../reference/target-frameworks.md), взаимодействовать с совместимыми пакетами, которые не объявляют dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="45b4e-332">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="45b4e-333">Таким образом, если в проекте используется dotnet TxM, все пакеты, от которых вы зависите, должны также содержать dotnet TxM. В противном случае нужно добавить `<PackageTargetFallback>` в проект, чтобы обеспечить совместимость с платформами, отличными от dotnet.</span><span class="sxs-lookup"><span data-stu-id="45b4e-333">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="45b4e-334">Например, если в проекте используется `netstandard1.6` TxM, а зависимый пакет содержит только `lib/net45/a.dll` и `lib/portable-net45+win81/a.dll`, то сборка проекта завершится со сбоем.</span><span class="sxs-lookup"><span data-stu-id="45b4e-334">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="45b4e-335">Если вы хотите использовать вторую библиотеку DLL, можете добавить `PackageTargetFallback` следующим образом, чтобы обозначить совместимость библиотеки DLL `portable-net45+win81`:</span><span class="sxs-lookup"><span data-stu-id="45b4e-335">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="45b4e-336">Чтобы объявить откат для всех целевых объектов в проекте, оставьте атрибут `Condition`.</span><span class="sxs-lookup"><span data-stu-id="45b4e-336">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="45b4e-337">Кроме того, можно расширить существующий `PackageTargetFallback`, включив `$(PackageTargetFallback)`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="45b4e-337">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="45b4e-338">Замена одной библиотеки из графа восстановления</span><span class="sxs-lookup"><span data-stu-id="45b4e-338">Replacing one library from a restore graph</span></span>

<span data-ttu-id="45b4e-339">Если операция восстановления предоставляет неправильную сборку, вы можете исключить значение по умолчанию для этого пакета, заменив его своим значением.</span><span class="sxs-lookup"><span data-stu-id="45b4e-339">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="45b4e-340">Первый с `PackageReference` верхнего уровня, исключите все ресурсы:</span><span class="sxs-lookup"><span data-stu-id="45b4e-340">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="45b4e-341">После этого добавьте собственную ссылку на соответствующую локальную копию библиотеки DLL:</span><span class="sxs-lookup"><span data-stu-id="45b4e-341">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
