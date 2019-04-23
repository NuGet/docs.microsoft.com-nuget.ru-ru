---
title: Объекты pack и restore NuGet в качестве целевых объектов MSBuild
description: Объекты pack и restore NuGet могут выступать непосредственно в качестве целевых объектов MSBuild в NuGet 4.0+.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 1e89aeb46f2538d46c013561a51a41702b2472d8
ms.sourcegitcommit: 6b71926f062ecddb8729ef8567baf67fd269642a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2019
ms.locfileid: "59932103"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="cf42b-103">Объекты pack и restore NuGet в качестве целевых объектов MSBuild</span><span class="sxs-lookup"><span data-stu-id="cf42b-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="cf42b-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="cf42b-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="cf42b-105">Благодаря формату PackageReference в NuGet 4.0 и более поздних версиях все метаданные манифеста могут храниться прямо в файле проекта, не требуя использования отдельного файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="cf42b-106">При использовании MSBuild 15.1+ NuGet также является привилегированным компонентом MSBuild с целевыми объектами `pack` и `restore`, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="cf42b-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="cf42b-107">Эти целевые объекты позволяют работать с NuGet, как с любой другой задачей или другим целевым объектом MSBuild.</span><span class="sxs-lookup"><span data-stu-id="cf42b-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="cf42b-108">(Для NuGet 3.x и более ранних версий можно использовать команды [pack](../tools/cli-ref-pack.md) и [restore](../tools/cli-ref-restore.md) в NuGet CLI.)</span><span class="sxs-lookup"><span data-stu-id="cf42b-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="cf42b-109">Порядок сборки целевого объекта</span><span class="sxs-lookup"><span data-stu-id="cf42b-109">Target build order</span></span>

<span data-ttu-id="cf42b-110">Так как `pack` и `restore` являются целевыми объектами MSBuild, вы можете обращаться к ним для улучшения рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="cf42b-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="cf42b-111">Например, предположим, что вам нужно скопировать пакет в общую сетевую папку после его упаковки.</span><span class="sxs-lookup"><span data-stu-id="cf42b-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="cf42b-112">Это можно сделать, добавив следующий код в файл проекта:</span><span class="sxs-lookup"><span data-stu-id="cf42b-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="cf42b-113">Аналогичным образом, вы можете создать задачу MSBuild и собственный целевой объект и использовать свойства NuGet в этой задаче MSBuild.</span><span class="sxs-lookup"><span data-stu-id="cf42b-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="cf42b-114">Целевой объект pack</span><span class="sxs-lookup"><span data-stu-id="cf42b-114">pack target</span></span>

<span data-ttu-id="cf42b-115">Для проектов .NET Standard с помощью формата PackageReference, `msbuild -t:pack` рисует входные данные из файла проекта для использования при создании пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="cf42b-115">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="cf42b-116">В следующей таблице описываются свойства MSBuild, которые можно добавить в файл проекта в первом узле `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="cf42b-117">Эти изменения легко внести в Visual Studio 2017 и более поздней версии, щелкнув проект правой кнопкой мыши и выбрав пункт **Изменить {project_name}**.</span><span class="sxs-lookup"><span data-stu-id="cf42b-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="cf42b-118">Для удобства таблица упорядочена по эквивалентным свойствам в [файле `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="cf42b-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="cf42b-119">Обратите внимание, что свойства `Owners` и `Summary` из `.nuspec` не поддерживаются в MSBuild.</span><span class="sxs-lookup"><span data-stu-id="cf42b-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="cf42b-120">Значение атрибута или NuSpec</span><span class="sxs-lookup"><span data-stu-id="cf42b-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="cf42b-121">Свойство MSBuild</span><span class="sxs-lookup"><span data-stu-id="cf42b-121">MSBuild Property</span></span> | <span data-ttu-id="cf42b-122">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="cf42b-122">Default</span></span> | <span data-ttu-id="cf42b-123">Примечания</span><span class="sxs-lookup"><span data-stu-id="cf42b-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="cf42b-124">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="cf42b-124">Id</span></span> | <span data-ttu-id="cf42b-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="cf42b-125">PackageId</span></span> | <span data-ttu-id="cf42b-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="cf42b-126">AssemblyName</span></span> | <span data-ttu-id="cf42b-127">$(AssemblyName) из MSBuild</span><span class="sxs-lookup"><span data-stu-id="cf42b-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="cf42b-128">Версия</span><span class="sxs-lookup"><span data-stu-id="cf42b-128">Version</span></span> | <span data-ttu-id="cf42b-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="cf42b-129">PackageVersion</span></span> | <span data-ttu-id="cf42b-130">Версия</span><span class="sxs-lookup"><span data-stu-id="cf42b-130">Version</span></span> | <span data-ttu-id="cf42b-131">Это значение совместимо с SemVer, например "1.0.0", "1.0.0-beta" или "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="cf42b-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="cf42b-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="cf42b-132">VersionPrefix</span></span> | <span data-ttu-id="cf42b-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="cf42b-133">PackageVersionPrefix</span></span> | <span data-ttu-id="cf42b-134">пустой</span><span class="sxs-lookup"><span data-stu-id="cf42b-134">empty</span></span> | <span data-ttu-id="cf42b-135">Задав PackageVersion, вы перезапишите PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="cf42b-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="cf42b-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="cf42b-136">VersionSuffix</span></span> | <span data-ttu-id="cf42b-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="cf42b-137">PackageVersionSuffix</span></span> | <span data-ttu-id="cf42b-138">пустой</span><span class="sxs-lookup"><span data-stu-id="cf42b-138">empty</span></span> | <span data-ttu-id="cf42b-139">$(VersionSuffix) из MSBuild.</span><span class="sxs-lookup"><span data-stu-id="cf42b-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="cf42b-140">Задав PackageVersion, вы перезапишите PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="cf42b-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="cf42b-141">Authors</span><span class="sxs-lookup"><span data-stu-id="cf42b-141">Authors</span></span> | <span data-ttu-id="cf42b-142">Authors</span><span class="sxs-lookup"><span data-stu-id="cf42b-142">Authors</span></span> | <span data-ttu-id="cf42b-143">Имя текущего пользователя</span><span class="sxs-lookup"><span data-stu-id="cf42b-143">Username of the current user</span></span> | |
| <span data-ttu-id="cf42b-144">Владельцы</span><span class="sxs-lookup"><span data-stu-id="cf42b-144">Owners</span></span> | <span data-ttu-id="cf42b-145">Н/Д</span><span class="sxs-lookup"><span data-stu-id="cf42b-145">N/A</span></span> | <span data-ttu-id="cf42b-146">Не существует в NuSpec</span><span class="sxs-lookup"><span data-stu-id="cf42b-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="cf42b-147">Заголовок</span><span class="sxs-lookup"><span data-stu-id="cf42b-147">Title</span></span> | <span data-ttu-id="cf42b-148">Заголовок</span><span class="sxs-lookup"><span data-stu-id="cf42b-148">Title</span></span> | <span data-ttu-id="cf42b-149">Идентификатор пакета</span><span class="sxs-lookup"><span data-stu-id="cf42b-149">The PackageId</span></span>| |
| <span data-ttu-id="cf42b-150">Описание</span><span class="sxs-lookup"><span data-stu-id="cf42b-150">Description</span></span> | <span data-ttu-id="cf42b-151">Описание</span><span class="sxs-lookup"><span data-stu-id="cf42b-151">Description</span></span> | <span data-ttu-id="cf42b-152">"Описание пакета"</span><span class="sxs-lookup"><span data-stu-id="cf42b-152">"Package Description"</span></span> | |
| <span data-ttu-id="cf42b-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="cf42b-153">Copyright</span></span> | <span data-ttu-id="cf42b-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="cf42b-154">Copyright</span></span> | <span data-ttu-id="cf42b-155">пустой</span><span class="sxs-lookup"><span data-stu-id="cf42b-155">empty</span></span> | |
| <span data-ttu-id="cf42b-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="cf42b-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="cf42b-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="cf42b-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="cf42b-158">False</span><span class="sxs-lookup"><span data-stu-id="cf42b-158">false</span></span> | |
| <span data-ttu-id="cf42b-159">лицензии</span><span class="sxs-lookup"><span data-stu-id="cf42b-159">license</span></span> | <span data-ttu-id="cf42b-160">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="cf42b-160">PackageLicenseExpression</span></span> | <span data-ttu-id="cf42b-161">пустой</span><span class="sxs-lookup"><span data-stu-id="cf42b-161">empty</span></span> | <span data-ttu-id="cf42b-162">Соответствует `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="cf42b-162">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="cf42b-163">лицензии</span><span class="sxs-lookup"><span data-stu-id="cf42b-163">license</span></span> | <span data-ttu-id="cf42b-164">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="cf42b-164">PackageLicenseFile</span></span> | <span data-ttu-id="cf42b-165">пустой</span><span class="sxs-lookup"><span data-stu-id="cf42b-165">empty</span></span> | <span data-ttu-id="cf42b-166">Соответствует `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-166">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="cf42b-167">Может потребоваться явно пакета файл лицензии, на которую указывает ссылка.</span><span class="sxs-lookup"><span data-stu-id="cf42b-167">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="cf42b-168">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="cf42b-168">LicenseUrl</span></span> | <span data-ttu-id="cf42b-169">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="cf42b-169">PackageLicenseUrl</span></span> | <span data-ttu-id="cf42b-170">пустой</span><span class="sxs-lookup"><span data-stu-id="cf42b-170">empty</span></span> | <span data-ttu-id="cf42b-171">`licenseUrl` является устаревшим, используйте свойство PackageLicenseExpression или PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="cf42b-171">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="cf42b-172">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="cf42b-172">ProjectUrl</span></span> | <span data-ttu-id="cf42b-173">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="cf42b-173">PackageProjectUrl</span></span> | <span data-ttu-id="cf42b-174">пустой</span><span class="sxs-lookup"><span data-stu-id="cf42b-174">empty</span></span> | |
| <span data-ttu-id="cf42b-175">IconUrl</span><span class="sxs-lookup"><span data-stu-id="cf42b-175">IconUrl</span></span> | <span data-ttu-id="cf42b-176">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="cf42b-176">PackageIconUrl</span></span> | <span data-ttu-id="cf42b-177">пустой</span><span class="sxs-lookup"><span data-stu-id="cf42b-177">empty</span></span> | |
| <span data-ttu-id="cf42b-178">Теги</span><span class="sxs-lookup"><span data-stu-id="cf42b-178">Tags</span></span> | <span data-ttu-id="cf42b-179">PackageTags</span><span class="sxs-lookup"><span data-stu-id="cf42b-179">PackageTags</span></span> | <span data-ttu-id="cf42b-180">пустой</span><span class="sxs-lookup"><span data-stu-id="cf42b-180">empty</span></span> | <span data-ttu-id="cf42b-181">Теги разделяются точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="cf42b-181">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="cf42b-182">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="cf42b-182">ReleaseNotes</span></span> | <span data-ttu-id="cf42b-183">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="cf42b-183">PackageReleaseNotes</span></span> | <span data-ttu-id="cf42b-184">пустой</span><span class="sxs-lookup"><span data-stu-id="cf42b-184">empty</span></span> | |
| <span data-ttu-id="cf42b-185">URL-адрес репозитория /</span><span class="sxs-lookup"><span data-stu-id="cf42b-185">Repository/Url</span></span> | <span data-ttu-id="cf42b-186">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="cf42b-186">RepositoryUrl</span></span> | <span data-ttu-id="cf42b-187">пустой</span><span class="sxs-lookup"><span data-stu-id="cf42b-187">empty</span></span> | <span data-ttu-id="cf42b-188">URL-адрес репозитория можно клонировать или загрузить исходный код.</span><span class="sxs-lookup"><span data-stu-id="cf42b-188">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="cf42b-189">Пример: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="cf42b-189">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="cf42b-190">/ Тип репозитория</span><span class="sxs-lookup"><span data-stu-id="cf42b-190">Repository/Type</span></span> | <span data-ttu-id="cf42b-191">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="cf42b-191">RepositoryType</span></span> | <span data-ttu-id="cf42b-192">пустой</span><span class="sxs-lookup"><span data-stu-id="cf42b-192">empty</span></span> | <span data-ttu-id="cf42b-193">Тип репозитория.</span><span class="sxs-lookup"><span data-stu-id="cf42b-193">Repository type.</span></span> <span data-ttu-id="cf42b-194">Примеры: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="cf42b-194">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="cf42b-195">Репозитория или ветви</span><span class="sxs-lookup"><span data-stu-id="cf42b-195">Repository/Branch</span></span> | <span data-ttu-id="cf42b-196">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="cf42b-196">RepositoryBranch</span></span> | <span data-ttu-id="cf42b-197">пустой</span><span class="sxs-lookup"><span data-stu-id="cf42b-197">empty</span></span> | <span data-ttu-id="cf42b-198">Сведения о ветви необязательно репозитории.</span><span class="sxs-lookup"><span data-stu-id="cf42b-198">Optional repository branch information.</span></span> <span data-ttu-id="cf42b-199">*RepositoryUrl* также должен быть указан для этого свойства для включения.</span><span class="sxs-lookup"><span data-stu-id="cf42b-199">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="cf42b-200">Пример: *master* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="cf42b-200">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="cf42b-201">Репозиторий и фиксации</span><span class="sxs-lookup"><span data-stu-id="cf42b-201">Repository/Commit</span></span> | <span data-ttu-id="cf42b-202">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="cf42b-202">RepositoryCommit</span></span> | <span data-ttu-id="cf42b-203">пустой</span><span class="sxs-lookup"><span data-stu-id="cf42b-203">empty</span></span> | <span data-ttu-id="cf42b-204">Необязательный репозитория фиксацию или набор изменений, чтобы указать, что источник пакета было выполнено построение.</span><span class="sxs-lookup"><span data-stu-id="cf42b-204">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="cf42b-205">*RepositoryUrl* также должен быть указан для этого свойства для включения.</span><span class="sxs-lookup"><span data-stu-id="cf42b-205">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="cf42b-206">Пример *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="cf42b-206">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="cf42b-207">PackageType</span><span class="sxs-lookup"><span data-stu-id="cf42b-207">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="cf42b-208">Сводка</span><span class="sxs-lookup"><span data-stu-id="cf42b-208">Summary</span></span> | <span data-ttu-id="cf42b-209">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="cf42b-209">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="cf42b-210">Входные данные целевого объекта pack</span><span class="sxs-lookup"><span data-stu-id="cf42b-210">pack target inputs</span></span>

- <span data-ttu-id="cf42b-211">IsPackable</span><span class="sxs-lookup"><span data-stu-id="cf42b-211">IsPackable</span></span>
- <span data-ttu-id="cf42b-212">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="cf42b-212">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="cf42b-213">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="cf42b-213">PackageVersion</span></span>
- <span data-ttu-id="cf42b-214">PackageId</span><span class="sxs-lookup"><span data-stu-id="cf42b-214">PackageId</span></span>
- <span data-ttu-id="cf42b-215">Authors</span><span class="sxs-lookup"><span data-stu-id="cf42b-215">Authors</span></span>
- <span data-ttu-id="cf42b-216">Описание</span><span class="sxs-lookup"><span data-stu-id="cf42b-216">Description</span></span>
- <span data-ttu-id="cf42b-217">Copyright</span><span class="sxs-lookup"><span data-stu-id="cf42b-217">Copyright</span></span>
- <span data-ttu-id="cf42b-218">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="cf42b-218">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="cf42b-219">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="cf42b-219">DevelopmentDependency</span></span>
- <span data-ttu-id="cf42b-220">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="cf42b-220">PackageLicenseExpression</span></span>
- <span data-ttu-id="cf42b-221">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="cf42b-221">PackageLicenseFile</span></span>
- <span data-ttu-id="cf42b-222">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="cf42b-222">PackageLicenseUrl</span></span>
- <span data-ttu-id="cf42b-223">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="cf42b-223">PackageProjectUrl</span></span>
- <span data-ttu-id="cf42b-224">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="cf42b-224">PackageIconUrl</span></span>
- <span data-ttu-id="cf42b-225">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="cf42b-225">PackageReleaseNotes</span></span>
- <span data-ttu-id="cf42b-226">PackageTags</span><span class="sxs-lookup"><span data-stu-id="cf42b-226">PackageTags</span></span>
- <span data-ttu-id="cf42b-227">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="cf42b-227">PackageOutputPath</span></span>
- <span data-ttu-id="cf42b-228">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="cf42b-228">IncludeSymbols</span></span>
- <span data-ttu-id="cf42b-229">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="cf42b-229">IncludeSource</span></span>
- <span data-ttu-id="cf42b-230">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="cf42b-230">PackageTypes</span></span>
- <span data-ttu-id="cf42b-231">IsTool</span><span class="sxs-lookup"><span data-stu-id="cf42b-231">IsTool</span></span>
- <span data-ttu-id="cf42b-232">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="cf42b-232">RepositoryUrl</span></span>
- <span data-ttu-id="cf42b-233">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="cf42b-233">RepositoryType</span></span>
- <span data-ttu-id="cf42b-234">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="cf42b-234">RepositoryBranch</span></span>
- <span data-ttu-id="cf42b-235">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="cf42b-235">RepositoryCommit</span></span>
- <span data-ttu-id="cf42b-236">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="cf42b-236">NoPackageAnalysis</span></span>
- <span data-ttu-id="cf42b-237">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="cf42b-237">MinClientVersion</span></span>
- <span data-ttu-id="cf42b-238">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="cf42b-238">IncludeBuildOutput</span></span>
- <span data-ttu-id="cf42b-239">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="cf42b-239">IncludeContentInPack</span></span>
- <span data-ttu-id="cf42b-240">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="cf42b-240">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="cf42b-241">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="cf42b-241">ContentTargetFolders</span></span>
- <span data-ttu-id="cf42b-242">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="cf42b-242">NuspecFile</span></span>
- <span data-ttu-id="cf42b-243">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="cf42b-243">NuspecBasePath</span></span>
- <span data-ttu-id="cf42b-244">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="cf42b-244">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="cf42b-245">Сценарии использования pack</span><span class="sxs-lookup"><span data-stu-id="cf42b-245">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="cf42b-246">Подавлять зависимостей</span><span class="sxs-lookup"><span data-stu-id="cf42b-246">Suppress dependencies</span></span>

<span data-ttu-id="cf42b-247">Чтобы отключить зависимости пакетов из созданного пакета NuGet, присвойте параметру `SuppressDependenciesWhenPacking` для `true` которых пропускает все зависимости из файла созданного nupkg.</span><span class="sxs-lookup"><span data-stu-id="cf42b-247">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="cf42b-248">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="cf42b-248">PackageIconUrl</span></span>

<span data-ttu-id="cf42b-249">В процессе изменения для [352 проблема NuGet](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` со временем изменяется `PackageIconUri` и может быть относительным путем к файлу значка, который будет включен в корень итогового пакета.</span><span class="sxs-lookup"><span data-stu-id="cf42b-249">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="cf42b-250">Выходные сборки</span><span class="sxs-lookup"><span data-stu-id="cf42b-250">Output assemblies</span></span>

<span data-ttu-id="cf42b-251">`nuget pack` копирует выходные файлы с расширениями `.exe`, `.dll`, `.xml`, `.winmd`, `.json` и `.pri`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-251">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="cf42b-252">Копируемые выходные файлы зависят от того, что MSBuild предоставляет из целевого объекта `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-252">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="cf42b-253">Существует два свойства MSBuild, которые можно использовать в файле проекта или командной строке для управления местом назначения для выходных сборок:</span><span class="sxs-lookup"><span data-stu-id="cf42b-253">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="cf42b-254">`IncludeBuildOutput`: Логическое значение, определяющее, следует ли включать выходные сборки в пакете.</span><span class="sxs-lookup"><span data-stu-id="cf42b-254">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="cf42b-255">`BuildOutputTargetFolder`: Указывает папку, в котором должны размещаться выходные сборки.</span><span class="sxs-lookup"><span data-stu-id="cf42b-255">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="cf42b-256">Выходные сборки (и другие выходные файлы) копируются в соответствующие папки платформы.</span><span class="sxs-lookup"><span data-stu-id="cf42b-256">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="cf42b-257">Ссылки на пакеты</span><span class="sxs-lookup"><span data-stu-id="cf42b-257">Package references</span></span>

<span data-ttu-id="cf42b-258">См. раздел [Ссылки на пакеты в файлах проекта](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="cf42b-258">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="cf42b-259">Перекрестные ссылки между проектами</span><span class="sxs-lookup"><span data-stu-id="cf42b-259">Project to project references</span></span>

<span data-ttu-id="cf42b-260">Перекрестные ссылки между проектами по умолчанию считаются ссылками на пакет NuGet, например:</span><span class="sxs-lookup"><span data-stu-id="cf42b-260">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="cf42b-261">Вы также можете добавить в ссылку на проект следующие метаданные:</span><span class="sxs-lookup"><span data-stu-id="cf42b-261">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="cf42b-262">Включение содержимого в пакет</span><span class="sxs-lookup"><span data-stu-id="cf42b-262">Including content in a package</span></span>

<span data-ttu-id="cf42b-263">Чтобы включить содержимое, добавьте дополнительные метаданные для существующего элемента `<Content>`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-263">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="cf42b-264">По умолчанию все данные типа "Content" включаются в пакет, если только вы не переопределите такое поведение с помощью записей, аналогичных следующим:</span><span class="sxs-lookup"><span data-stu-id="cf42b-264">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="cf42b-265">По умолчанию все данные добавляются в корень папки `content` и `contentFiles\any\<target_framework>` в пакете и сохраняют относительную структуру папок, если только не указан путь к пакету:</span><span class="sxs-lookup"><span data-stu-id="cf42b-265">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="cf42b-266">Если требуется скопировать все содержимое только в определенные корневые папки (вместо `content` и `contentFiles`), можно использовать свойство MSBuild `ContentTargetFolders`, которое по умолчанию имеет значение "content;contentFiles", но может принимать любые другие имена папок.</span><span class="sxs-lookup"><span data-stu-id="cf42b-266">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="cf42b-267">Обратите внимание, если указать "contentFiles" в `ContentTargetFolders`, файлы помещаются в `contentFiles\any\<target_framework>` или `contentFiles\<language>\<target_framework>` в зависимости от `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-267">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="cf42b-268">`PackagePath` может быть набором целевых путей, разделенных точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="cf42b-268">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="cf42b-269">Если указан пустой путь к пакету, файл добавляется в корневой каталог пакета.</span><span class="sxs-lookup"><span data-stu-id="cf42b-269">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="cf42b-270">Например, следующий код добавляет `libuv.txt` в `content\myfiles`, `content\samples` и корневой каталог пакета:</span><span class="sxs-lookup"><span data-stu-id="cf42b-270">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="cf42b-271">Имеется также свойство MSBuild `$(IncludeContentInPack)`, которое по умолчанию равно `true`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-271">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="cf42b-272">Если оно имеет значение `false` для какого-либо проекта, то содержимое этого проекта не включается в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="cf42b-272">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="cf42b-273">Другие относящиеся к pack метаданные, которые можно задать для любого из указанных выше элементов, включают ```<PackageCopyToOutput>``` и ```<PackageFlatten>```, задающие значения ```CopyToOutput``` и ```Flatten``` для записи ```contentFiles``` в выходном файле NUSPEC.</span><span class="sxs-lookup"><span data-stu-id="cf42b-273">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="cf42b-274">Кроме элементов содержимого, метаданные `<Pack>` и `<PackagePath>` также можно задать для файлов с действием сборки Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource или None.</span><span class="sxs-lookup"><span data-stu-id="cf42b-274">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="cf42b-275">Чтобы объект pack добавил имя файла в путь к пакету при использовании стандартных масок, путь к пакету должен заканчиваться символом разделителя папок, в противном случае этот путь считается полным путем, включающим имя файла.</span><span class="sxs-lookup"><span data-stu-id="cf42b-275">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="cf42b-276">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="cf42b-276">IncludeSymbols</span></span>

<span data-ttu-id="cf42b-277">При использовании `MSBuild -t:pack -p:IncludeSymbols=true` соответствующие файлы `.pdb` копируются вместе с другими выходными файлами (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="cf42b-277">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="cf42b-278">Обратите внимание, что при задании `IncludeSymbols=true` создается обычный пакет *и* пакет символов.</span><span class="sxs-lookup"><span data-stu-id="cf42b-278">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="cf42b-279">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="cf42b-279">IncludeSource</span></span>

<span data-ttu-id="cf42b-280">Аналогично `IncludeSymbols`, только копирует исходные файлы вместе с файлами `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-280">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="cf42b-281">Все файлы типа `Compile` копируются в `src\<ProjectName>\` с сохранением относительной структуры папок в итоговом пакете.</span><span class="sxs-lookup"><span data-stu-id="cf42b-281">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="cf42b-282">То же самое происходит с исходными файлами любого `ProjectReference`, у которого `TreatAsPackageReference` имеет значение `false`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-282">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="cf42b-283">Если файл типа Compile находится вне папки проекта, он просто добавляется в `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-283">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="cf42b-284">Упаковка выражении лицензии или файл лицензии</span><span class="sxs-lookup"><span data-stu-id="cf42b-284">Packing a license expression or a license file</span></span>

<span data-ttu-id="cf42b-285">При использовании выражения лицензии, следует использовать свойство PackageLicenseExpression.</span><span class="sxs-lookup"><span data-stu-id="cf42b-285">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="cf42b-286">[Пример выражения лицензии](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="cf42b-286">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="cf42b-287">[Дополнительные сведения о выражениях лицензии и лицензии, которые может принимать NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="cf42b-287">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="cf42b-288">При упаковке файл лицензии, необходимо использовать свойство PackageLicenseFile чтобы указать путь к пакету, относительно корня пакета.</span><span class="sxs-lookup"><span data-stu-id="cf42b-288">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="cf42b-289">Кроме того необходимо убедиться, что файл включается в пакет.</span><span class="sxs-lookup"><span data-stu-id="cf42b-289">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="cf42b-290">Пример:</span><span class="sxs-lookup"><span data-stu-id="cf42b-290">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="cf42b-291">[Образец файла лицензии](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="cf42b-291">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="cf42b-292">IsTool</span><span class="sxs-lookup"><span data-stu-id="cf42b-292">IsTool</span></span>

<span data-ttu-id="cf42b-293">При использовании `MSBuild -t:pack -p:IsTool=true` все выходные файлы, как указано в сценарии [Выходные сборки](#output-assemblies), копируются в папку `tools` вместо папки `lib`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-293">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="cf42b-294">Обратите внимание, что это свойство отличается от `DotNetCliTool`, которое указывается путем задания `PackageType` в файле `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-294">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="cf42b-295">Упаковка с помощью NUSPEC</span><span class="sxs-lookup"><span data-stu-id="cf42b-295">Packing using a .nuspec</span></span>

<span data-ttu-id="cf42b-296">Можно использовать `.nuspec` файл для упаковки проекта, при условии, что у вас есть файл проекта SDK для импорта `NuGet.Build.Tasks.Pack.targets` , чтобы можно было выполнить задачу пакета.</span><span class="sxs-lookup"><span data-stu-id="cf42b-296">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="cf42b-297">По-прежнему необходимо восстановить проект, прежде чем можно упаковать в файл nuspec.</span><span class="sxs-lookup"><span data-stu-id="cf42b-297">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="cf42b-298">Требуемая версия .NET framework файл проекта не имеет значения и не использовались при упаковке nuspec.</span><span class="sxs-lookup"><span data-stu-id="cf42b-298">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="cf42b-299">Следующие три свойства MSBuild связаны с упаковкой с помощью `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="cf42b-299">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="cf42b-300">`NuspecFile`: относительный или абсолютный путь к файлу `.nuspec`, используемому для упаковки.</span><span class="sxs-lookup"><span data-stu-id="cf42b-300">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="cf42b-301">`NuspecProperties`: список разделенных точками с запятой пар "ключ-значение".</span><span class="sxs-lookup"><span data-stu-id="cf42b-301">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="cf42b-302">Из-за особенностей работы анализа в командной строке MSBuild несколько свойств нужно указать следующим образом: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-302">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="cf42b-303">`NuspecBasePath`: Базовый путь для `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="cf42b-303">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="cf42b-304">Если вы используете `dotnet.exe` для упаковки проекта, воспользуйтесь командой, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="cf42b-304">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="cf42b-305">Если вы используете MSBuild для упаковки проекта, воспользуйтесь командой, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="cf42b-305">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="cf42b-306">Обратите внимание на то, что упаковки nuspec использование dotnet.exe или msbuild также приводит к сборке проекта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cf42b-306">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="cf42b-307">Этого можно избежать путем передачи ```--no-build``` dotnet.exe, это эквивалентно заданию свойства ```<NoBuild>true</NoBuild> ``` в файле проекта, а также параметр ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` в файле проекта</span><span class="sxs-lookup"><span data-stu-id="cf42b-307">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="cf42b-308">Приведен пример файла csproj, упаковать в файл nuspec.</span><span class="sxs-lookup"><span data-stu-id="cf42b-308">An example of a csproj file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="cf42b-309">Дополнительные точки расширения, чтобы создать настроенный пакет</span><span class="sxs-lookup"><span data-stu-id="cf42b-309">Advanced extension points to create customized package</span></span>

<span data-ttu-id="cf42b-310">`pack` Целевой предоставляет две точки расширения, которые работают в определенной сборки внутренний целевой платформы.</span><span class="sxs-lookup"><span data-stu-id="cf42b-310">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="cf42b-311">Точки расширения поддерживают определенное содержимое целевой платформы и сборки в пакет:</span><span class="sxs-lookup"><span data-stu-id="cf42b-311">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="cf42b-312">`TargetsForTfmSpecificBuildOutput` целевой объект: Используйте для файлов в `lib` папка или папка, заданные с помощью `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-312">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="cf42b-313">`TargetsForTfmSpecificContentInPackage` целевой объект: Используйте для файлов за пределами `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-313">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="cf42b-314">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="cf42b-314">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="cf42b-315">Запишите пользовательский целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificBuildOutput)` свойство.</span><span class="sxs-lookup"><span data-stu-id="cf42b-315">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="cf42b-316">Для всех файлов, которые необходимо перевести в `BuildOutputTargetFolder` (по умолчанию), lib целевой объект должен записывать файлы в ItemGroup `BuildOutputInPackage` и задайте следующие два значения метаданных:</span><span class="sxs-lookup"><span data-stu-id="cf42b-316">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="cf42b-317">`FinalOutputPath`: Абсолютный путь к файлу; Если не указано, удостоверение используется для оценки исходный путь.</span><span class="sxs-lookup"><span data-stu-id="cf42b-317">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="cf42b-318">`TargetPath`:  (Необязательно) Значение, когда файл должен располагаться в подпапке в `lib\<TargetFramework>` , такие как вспомогательные сборки, учитываемых в своих папках соответствующего языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="cf42b-318">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="cf42b-319">По умолчанию указывается имя файла.</span><span class="sxs-lookup"><span data-stu-id="cf42b-319">Defaults to the name of the file.</span></span>

<span data-ttu-id="cf42b-320">Пример</span><span class="sxs-lookup"><span data-stu-id="cf42b-320">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="cf42b-321">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="cf42b-321">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="cf42b-322">Запишите пользовательский целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificContentInPackage)` свойство.</span><span class="sxs-lookup"><span data-stu-id="cf42b-322">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="cf42b-323">Для всех файлов, включаемых в пакет, целевой объект должен записывать файлы в ItemGroup `TfmSpecificPackageFile` и задайте следующие необязательные метаданные:</span><span class="sxs-lookup"><span data-stu-id="cf42b-323">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="cf42b-324">`PackagePath`: Путь, где этот файл должен быть выходные данные в пакете.</span><span class="sxs-lookup"><span data-stu-id="cf42b-324">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="cf42b-325">NuGet выдает предупреждение, если же путь к пакету добавляется более одного файла.</span><span class="sxs-lookup"><span data-stu-id="cf42b-325">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="cf42b-326">`BuildAction`: Действие построения файла, требуется только путь к пакету в `contentFiles` папку.</span><span class="sxs-lookup"><span data-stu-id="cf42b-326">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="cf42b-327">По умолчанию — «None».</span><span class="sxs-lookup"><span data-stu-id="cf42b-327">Defaults to "None".</span></span>

<span data-ttu-id="cf42b-328">Пример:</span><span class="sxs-lookup"><span data-stu-id="cf42b-328">An example:</span></span>
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a><span data-ttu-id="cf42b-329">Целевой объект restore</span><span class="sxs-lookup"><span data-stu-id="cf42b-329">restore target</span></span>

<span data-ttu-id="cf42b-330">`MSBuild -t:restore` (который `nuget restore` и `dotnet restore` используют с проектами .NET Core) восстанавливает пакеты, на которые ссылается файл проекта:</span><span class="sxs-lookup"><span data-stu-id="cf42b-330">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="cf42b-331">Чтение перекрестных ссылок между проектами.</span><span class="sxs-lookup"><span data-stu-id="cf42b-331">Read all project to project references</span></span>
1. <span data-ttu-id="cf42b-332">Чтение свойств проекта, чтобы найти промежуточную папку и целевые платформы.</span><span class="sxs-lookup"><span data-stu-id="cf42b-332">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="cf42b-333">Передача данных MSBuild в NuGet.Build.Tasks.dll.</span><span class="sxs-lookup"><span data-stu-id="cf42b-333">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="cf42b-334">Запуск восстановления.</span><span class="sxs-lookup"><span data-stu-id="cf42b-334">Run restore</span></span>
1. <span data-ttu-id="cf42b-335">Скачивание пакетов.</span><span class="sxs-lookup"><span data-stu-id="cf42b-335">Download packages</span></span>
1. <span data-ttu-id="cf42b-336">Запись файла ресурсов, целевых объектов и свойств.</span><span class="sxs-lookup"><span data-stu-id="cf42b-336">Write assets file, targets, and props</span></span>

<span data-ttu-id="cf42b-337">`restore` Целевой works **только** для проектов, использующих формат PackageReference.</span><span class="sxs-lookup"><span data-stu-id="cf42b-337">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="cf42b-338">Да **не** работают для проектов с помощью `packages.config` форматирования; используйте [восстановление nuget](../tools/cli-ref-restore.md) вместо этого.</span><span class="sxs-lookup"><span data-stu-id="cf42b-338">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="cf42b-339">Свойства восстановления</span><span class="sxs-lookup"><span data-stu-id="cf42b-339">Restore properties</span></span>

<span data-ttu-id="cf42b-340">Дополнительные параметры восстановления могут поступать из свойств MSBuild в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="cf42b-340">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="cf42b-341">Значения также можно задать из командной строки с помощью параметра `-p:` (см. примеры ниже).</span><span class="sxs-lookup"><span data-stu-id="cf42b-341">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="cf42b-342">Свойство</span><span class="sxs-lookup"><span data-stu-id="cf42b-342">Property</span></span> | <span data-ttu-id="cf42b-343">Описание</span><span class="sxs-lookup"><span data-stu-id="cf42b-343">Description</span></span> |
|--------|--------|
| <span data-ttu-id="cf42b-344">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="cf42b-344">RestoreSources</span></span> | <span data-ttu-id="cf42b-345">Разделенный точками с запятой список источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="cf42b-345">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="cf42b-346">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="cf42b-346">RestorePackagesPath</span></span> | <span data-ttu-id="cf42b-347">Путь к папке пакетов пользователя.</span><span class="sxs-lookup"><span data-stu-id="cf42b-347">User packages folder path.</span></span> |
| <span data-ttu-id="cf42b-348">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="cf42b-348">RestoreDisableParallel</span></span> | <span data-ttu-id="cf42b-349">Ограничение скачиваний до одного за раз.</span><span class="sxs-lookup"><span data-stu-id="cf42b-349">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="cf42b-350">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="cf42b-350">RestoreConfigFile</span></span> | <span data-ttu-id="cf42b-351">Путь к применяемому файлу `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-351">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="cf42b-352">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="cf42b-352">RestoreNoCache</span></span> | <span data-ttu-id="cf42b-353">Если значение равно true, позволяет избежать использования кэшированные пакеты.</span><span class="sxs-lookup"><span data-stu-id="cf42b-353">If true, avoids using cached packages.</span></span> <span data-ttu-id="cf42b-354">См. в разделе [управление папкой установки глобальных пакетов и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="cf42b-354">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="cf42b-355">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="cf42b-355">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="cf42b-356">Если значение равно true, нерабочие или отсутствующие источники пакетов игнорируются.</span><span class="sxs-lookup"><span data-stu-id="cf42b-356">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="cf42b-357">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="cf42b-357">RestoreFallbackFolders</span></span> | <span data-ttu-id="cf42b-358">Резервные папки используется таким же образом пользователя пакеты, которые будет использоваться папка.</span><span class="sxs-lookup"><span data-stu-id="cf42b-358">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="cf42b-359">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="cf42b-359">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="cf42b-360">Дополнительные источники, которые используются во время восстановления.</span><span class="sxs-lookup"><span data-stu-id="cf42b-360">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="cf42b-361">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="cf42b-361">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="cf42b-362">Дополнительные резервные папки для использования во время восстановления.</span><span class="sxs-lookup"><span data-stu-id="cf42b-362">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="cf42b-363">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="cf42b-363">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="cf42b-364">Исключает резервной папки, указанные в `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="cf42b-364">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="cf42b-365">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="cf42b-365">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="cf42b-366">Путь к `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-366">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="cf42b-367">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="cf42b-367">RestoreGraphProjectInput</span></span> | <span data-ttu-id="cf42b-368">Разделенный точками с запятой список проектов для восстановления, который должен содержать абсолютные пути.</span><span class="sxs-lookup"><span data-stu-id="cf42b-368">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="cf42b-369">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="cf42b-369">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="cf42b-370">Если проекты собираются с помощью MSBuild, он определяет, является ли они собираются с помощью `SkipNonexistentTargets` оптимизации.</span><span class="sxs-lookup"><span data-stu-id="cf42b-370">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="cf42b-371">Если значение не задано, по умолчанию используется `true`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-371">When not set, defaults to `true`.</span></span> <span data-ttu-id="cf42b-372">Результат при поведение высокопроизводительную целевыми платформами проекта не может быть импортирован.</span><span class="sxs-lookup"><span data-stu-id="cf42b-372">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="cf42b-373">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="cf42b-373">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="cf42b-374">Выходная папка по умолчанию принимается `BaseIntermediateOutputPath` и `obj` папки.</span><span class="sxs-lookup"><span data-stu-id="cf42b-374">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="cf42b-375">Примеры</span><span class="sxs-lookup"><span data-stu-id="cf42b-375">Examples</span></span>

<span data-ttu-id="cf42b-376">Командная строка:</span><span class="sxs-lookup"><span data-stu-id="cf42b-376">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="cf42b-377">Файл проекта:</span><span class="sxs-lookup"><span data-stu-id="cf42b-377">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="cf42b-378">Выходные данные восстановления</span><span class="sxs-lookup"><span data-stu-id="cf42b-378">Restore outputs</span></span>

<span data-ttu-id="cf42b-379">Операция восстановления создает в папке сборки `obj` следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="cf42b-379">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="cf42b-380">Файл</span><span class="sxs-lookup"><span data-stu-id="cf42b-380">File</span></span> | <span data-ttu-id="cf42b-381">Описание</span><span class="sxs-lookup"><span data-stu-id="cf42b-381">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="cf42b-382">Содержит все ссылки на пакеты в графе зависимостей.</span><span class="sxs-lookup"><span data-stu-id="cf42b-382">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="cf42b-383">Ссылки на свойства MSBuild, содержащиеся в пакетах.</span><span class="sxs-lookup"><span data-stu-id="cf42b-383">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="cf42b-384">Ссылки на целевые объекты MSBuild, содержащиеся в пакетах.</span><span class="sxs-lookup"><span data-stu-id="cf42b-384">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="cf42b-385">Восстановление и построение с помощью одной команды MSBuild</span><span class="sxs-lookup"><span data-stu-id="cf42b-385">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="cf42b-386">Тем, что NuGet можно восстановить пакеты, обеспечивающие работу целевых объектов MSBuild и свойств, восстановления и ознакомительные версии сборки выполняются с другими глобальными свойствами.</span><span class="sxs-lookup"><span data-stu-id="cf42b-386">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="cf42b-387">Это означает, что ниже будут непредсказуемыми и часто неправильное поведение.</span><span class="sxs-lookup"><span data-stu-id="cf42b-387">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="cf42b-388">Вместо этого рекомендуется:</span><span class="sxs-lookup"><span data-stu-id="cf42b-388">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="cf42b-389">Эта же логика применяется к другим целевым объектам, аналогичную `build`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-389">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="cf42b-390">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="cf42b-390">PackageTargetFallback</span></span>

<span data-ttu-id="cf42b-391">Элемент `PackageTargetFallback` позволяет указать набор совместимых целевых объектов, которые следует использовать при восстановлении пакетов.</span><span class="sxs-lookup"><span data-stu-id="cf42b-391">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="cf42b-392">Он разрешает пакетам, использующим dotnet [TxM](../reference/target-frameworks.md), взаимодействовать с совместимыми пакетами, которые не объявляют dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="cf42b-392">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="cf42b-393">Таким образом, если в проекте используется dotnet TxM, все пакеты, от которых вы зависите, должны также содержать dotnet TxM. В противном случае нужно добавить `<PackageTargetFallback>` в проект, чтобы обеспечить совместимость с платформами, отличными от dotnet.</span><span class="sxs-lookup"><span data-stu-id="cf42b-393">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="cf42b-394">Например, если в проекте используется `netstandard1.6` TxM, а зависимый пакет содержит только `lib/net45/a.dll` и `lib/portable-net45+win81/a.dll`, то сборка проекта завершится со сбоем.</span><span class="sxs-lookup"><span data-stu-id="cf42b-394">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="cf42b-395">Если вы хотите использовать вторую библиотеку DLL, можете добавить `PackageTargetFallback` следующим образом, чтобы обозначить совместимость библиотеки DLL `portable-net45+win81`:</span><span class="sxs-lookup"><span data-stu-id="cf42b-395">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="cf42b-396">Чтобы объявить откат для всех целевых объектов в проекте, оставьте атрибут `Condition`.</span><span class="sxs-lookup"><span data-stu-id="cf42b-396">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="cf42b-397">Кроме того, можно расширить существующий `PackageTargetFallback`, включив `$(PackageTargetFallback)`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="cf42b-397">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="cf42b-398">Замена одной библиотеки из графа восстановления</span><span class="sxs-lookup"><span data-stu-id="cf42b-398">Replacing one library from a restore graph</span></span>

<span data-ttu-id="cf42b-399">Если операция восстановления предоставляет неправильную сборку, вы можете исключить значение по умолчанию для этого пакета, заменив его своим значением.</span><span class="sxs-lookup"><span data-stu-id="cf42b-399">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="cf42b-400">Первый с `PackageReference` верхнего уровня, исключите все ресурсы:</span><span class="sxs-lookup"><span data-stu-id="cf42b-400">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="cf42b-401">После этого добавьте собственную ссылку на соответствующую локальную копию библиотеки DLL:</span><span class="sxs-lookup"><span data-stu-id="cf42b-401">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
