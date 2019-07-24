---
title: Объекты pack и restore NuGet в качестве целевых объектов MSBuild
description: Объекты pack и restore NuGet могут выступать непосредственно в качестве целевых объектов MSBuild в NuGet 4.0+.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 8e662194fffc031d0cfc0aa129a5a15b555a4231
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/23/2019
ms.locfileid: "68420013"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="6d271-103">Объекты pack и restore NuGet в качестве целевых объектов MSBuild</span><span class="sxs-lookup"><span data-stu-id="6d271-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="6d271-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="6d271-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="6d271-105">В формате [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + может хранить все метаданные манифеста непосредственно в файле проекта вместо использования отдельного `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="6d271-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="6d271-106">При использовании MSBuild 15.1+ NuGet также является привилегированным компонентом MSBuild с целевыми объектами `pack` и `restore`, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="6d271-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="6d271-107">Эти целевые объекты позволяют работать с NuGet, как с любой другой задачей или другим целевым объектом MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6d271-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="6d271-108">(Для NuGet 3.x и более ранних версий можно использовать команды [pack](../reference/cli-reference/cli-ref-pack.md) и [restore](../reference/cli-reference/cli-ref-restore.md) в NuGet CLI.)</span><span class="sxs-lookup"><span data-stu-id="6d271-108">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="6d271-109">Порядок сборки целевого объекта</span><span class="sxs-lookup"><span data-stu-id="6d271-109">Target build order</span></span>

<span data-ttu-id="6d271-110">Так как `pack` и `restore` являются целевыми объектами MSBuild, вы можете обращаться к ним для улучшения рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="6d271-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="6d271-111">Например, предположим, что вам нужно скопировать пакет в общую сетевую папку после его упаковки.</span><span class="sxs-lookup"><span data-stu-id="6d271-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="6d271-112">Это можно сделать, добавив следующий код в файл проекта:</span><span class="sxs-lookup"><span data-stu-id="6d271-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="6d271-113">Аналогичным образом, вы можете создать задачу MSBuild и собственный целевой объект и использовать свойства NuGet в этой задаче MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6d271-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="6d271-114">Целевой объект pack</span><span class="sxs-lookup"><span data-stu-id="6d271-114">pack target</span></span>

<span data-ttu-id="6d271-115">Для .NET Standard проектов, использующих формат PackageReference `msbuild -t:pack` , команда рисует входные данные из файла проекта для использования при создании пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="6d271-115">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="6d271-116">В следующей таблице описываются свойства MSBuild, которые можно добавить в файл проекта в первом узле `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="6d271-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="6d271-117">Эти изменения легко внести в Visual Studio 2017 и более поздней версии, щелкнув проект правой кнопкой мыши и выбрав пункт **Изменить {project_name}** .</span><span class="sxs-lookup"><span data-stu-id="6d271-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="6d271-118">Для удобства таблица упорядочена по эквивалентным свойствам в [файле `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="6d271-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="6d271-119">Обратите внимание, что свойства `Owners` и `Summary` из `.nuspec` не поддерживаются в MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6d271-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="6d271-120">Значение атрибута или NuSpec</span><span class="sxs-lookup"><span data-stu-id="6d271-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="6d271-121">Свойство MSBuild</span><span class="sxs-lookup"><span data-stu-id="6d271-121">MSBuild Property</span></span> | <span data-ttu-id="6d271-122">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="6d271-122">Default</span></span> | <span data-ttu-id="6d271-123">Примечания</span><span class="sxs-lookup"><span data-stu-id="6d271-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="6d271-124">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="6d271-124">Id</span></span> | <span data-ttu-id="6d271-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="6d271-125">PackageId</span></span> | <span data-ttu-id="6d271-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="6d271-126">AssemblyName</span></span> | <span data-ttu-id="6d271-127">$(AssemblyName) из MSBuild</span><span class="sxs-lookup"><span data-stu-id="6d271-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="6d271-128">Версия</span><span class="sxs-lookup"><span data-stu-id="6d271-128">Version</span></span> | <span data-ttu-id="6d271-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="6d271-129">PackageVersion</span></span> | <span data-ttu-id="6d271-130">Версия</span><span class="sxs-lookup"><span data-stu-id="6d271-130">Version</span></span> | <span data-ttu-id="6d271-131">Это значение совместимо с SemVer, например "1.0.0", "1.0.0-beta" или "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="6d271-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="6d271-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="6d271-132">VersionPrefix</span></span> | <span data-ttu-id="6d271-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="6d271-133">PackageVersionPrefix</span></span> | <span data-ttu-id="6d271-134">пустой</span><span class="sxs-lookup"><span data-stu-id="6d271-134">empty</span></span> | <span data-ttu-id="6d271-135">Задав PackageVersion, вы перезапишите PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="6d271-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="6d271-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="6d271-136">VersionSuffix</span></span> | <span data-ttu-id="6d271-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="6d271-137">PackageVersionSuffix</span></span> | <span data-ttu-id="6d271-138">пустой</span><span class="sxs-lookup"><span data-stu-id="6d271-138">empty</span></span> | <span data-ttu-id="6d271-139">$(VersionSuffix) из MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6d271-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="6d271-140">Задав PackageVersion, вы перезапишите PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="6d271-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="6d271-141">Authors</span><span class="sxs-lookup"><span data-stu-id="6d271-141">Authors</span></span> | <span data-ttu-id="6d271-142">Authors</span><span class="sxs-lookup"><span data-stu-id="6d271-142">Authors</span></span> | <span data-ttu-id="6d271-143">Имя текущего пользователя</span><span class="sxs-lookup"><span data-stu-id="6d271-143">Username of the current user</span></span> | |
| <span data-ttu-id="6d271-144">Владельцы</span><span class="sxs-lookup"><span data-stu-id="6d271-144">Owners</span></span> | <span data-ttu-id="6d271-145">Н/Д</span><span class="sxs-lookup"><span data-stu-id="6d271-145">N/A</span></span> | <span data-ttu-id="6d271-146">Не существует в NuSpec</span><span class="sxs-lookup"><span data-stu-id="6d271-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="6d271-147">Заголовок</span><span class="sxs-lookup"><span data-stu-id="6d271-147">Title</span></span> | <span data-ttu-id="6d271-148">Заголовок</span><span class="sxs-lookup"><span data-stu-id="6d271-148">Title</span></span> | <span data-ttu-id="6d271-149">Идентификатор пакета</span><span class="sxs-lookup"><span data-stu-id="6d271-149">The PackageId</span></span>| |
| <span data-ttu-id="6d271-150">Описание</span><span class="sxs-lookup"><span data-stu-id="6d271-150">Description</span></span> | <span data-ttu-id="6d271-151">Описание</span><span class="sxs-lookup"><span data-stu-id="6d271-151">Description</span></span> | <span data-ttu-id="6d271-152">"Описание пакета"</span><span class="sxs-lookup"><span data-stu-id="6d271-152">"Package Description"</span></span> | |
| <span data-ttu-id="6d271-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="6d271-153">Copyright</span></span> | <span data-ttu-id="6d271-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="6d271-154">Copyright</span></span> | <span data-ttu-id="6d271-155">пустой</span><span class="sxs-lookup"><span data-stu-id="6d271-155">empty</span></span> | |
| <span data-ttu-id="6d271-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="6d271-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="6d271-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="6d271-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="6d271-158">False</span><span class="sxs-lookup"><span data-stu-id="6d271-158">false</span></span> | |
| <span data-ttu-id="6d271-159">Лицензии</span><span class="sxs-lookup"><span data-stu-id="6d271-159">license</span></span> | <span data-ttu-id="6d271-160">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="6d271-160">PackageLicenseExpression</span></span> | <span data-ttu-id="6d271-161">пустой</span><span class="sxs-lookup"><span data-stu-id="6d271-161">empty</span></span> | <span data-ttu-id="6d271-162">Соответствует`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="6d271-162">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="6d271-163">Лицензии</span><span class="sxs-lookup"><span data-stu-id="6d271-163">license</span></span> | <span data-ttu-id="6d271-164">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="6d271-164">PackageLicenseFile</span></span> | <span data-ttu-id="6d271-165">пустой</span><span class="sxs-lookup"><span data-stu-id="6d271-165">empty</span></span> | <span data-ttu-id="6d271-166">Соответствует `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="6d271-166">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="6d271-167">Возможно, потребуется явно упаковать файл лицензии, на который указывает ссылка.</span><span class="sxs-lookup"><span data-stu-id="6d271-167">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="6d271-168">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="6d271-168">LicenseUrl</span></span> | <span data-ttu-id="6d271-169">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="6d271-169">PackageLicenseUrl</span></span> | <span data-ttu-id="6d271-170">пустой</span><span class="sxs-lookup"><span data-stu-id="6d271-170">empty</span></span> | <span data-ttu-id="6d271-171">`licenseUrl`является устаревшим, используйте свойство Паккажелиценсикспрессион или Паккажелиценсефиле.</span><span class="sxs-lookup"><span data-stu-id="6d271-171">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="6d271-172">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="6d271-172">ProjectUrl</span></span> | <span data-ttu-id="6d271-173">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="6d271-173">PackageProjectUrl</span></span> | <span data-ttu-id="6d271-174">пустой</span><span class="sxs-lookup"><span data-stu-id="6d271-174">empty</span></span> | |
| <span data-ttu-id="6d271-175">IconUrl</span><span class="sxs-lookup"><span data-stu-id="6d271-175">IconUrl</span></span> | <span data-ttu-id="6d271-176">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="6d271-176">PackageIconUrl</span></span> | <span data-ttu-id="6d271-177">пустой</span><span class="sxs-lookup"><span data-stu-id="6d271-177">empty</span></span> | |
| <span data-ttu-id="6d271-178">Теги</span><span class="sxs-lookup"><span data-stu-id="6d271-178">Tags</span></span> | <span data-ttu-id="6d271-179">PackageTags</span><span class="sxs-lookup"><span data-stu-id="6d271-179">PackageTags</span></span> | <span data-ttu-id="6d271-180">пустой</span><span class="sxs-lookup"><span data-stu-id="6d271-180">empty</span></span> | <span data-ttu-id="6d271-181">Теги разделяются точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="6d271-181">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="6d271-182">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="6d271-182">ReleaseNotes</span></span> | <span data-ttu-id="6d271-183">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="6d271-183">PackageReleaseNotes</span></span> | <span data-ttu-id="6d271-184">пустой</span><span class="sxs-lookup"><span data-stu-id="6d271-184">empty</span></span> | |
| <span data-ttu-id="6d271-185">Репозиторий/URL-адрес</span><span class="sxs-lookup"><span data-stu-id="6d271-185">Repository/Url</span></span> | <span data-ttu-id="6d271-186">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="6d271-186">RepositoryUrl</span></span> | <span data-ttu-id="6d271-187">пустой</span><span class="sxs-lookup"><span data-stu-id="6d271-187">empty</span></span> | <span data-ttu-id="6d271-188">URL-адрес репозитория, используемый для клонирования или извлечения исходного кода.</span><span class="sxs-lookup"><span data-stu-id="6d271-188">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="6d271-189">Например *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="6d271-189">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="6d271-190">Репозиторий или тип</span><span class="sxs-lookup"><span data-stu-id="6d271-190">Repository/Type</span></span> | <span data-ttu-id="6d271-191">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="6d271-191">RepositoryType</span></span> | <span data-ttu-id="6d271-192">пустой</span><span class="sxs-lookup"><span data-stu-id="6d271-192">empty</span></span> | <span data-ttu-id="6d271-193">Тип репозитория.</span><span class="sxs-lookup"><span data-stu-id="6d271-193">Repository type.</span></span> <span data-ttu-id="6d271-194">Примеры: *Git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="6d271-194">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="6d271-195">Репозиторий или ветвь</span><span class="sxs-lookup"><span data-stu-id="6d271-195">Repository/Branch</span></span> | <span data-ttu-id="6d271-196">репоситорибранч</span><span class="sxs-lookup"><span data-stu-id="6d271-196">RepositoryBranch</span></span> | <span data-ttu-id="6d271-197">пустой</span><span class="sxs-lookup"><span data-stu-id="6d271-197">empty</span></span> | <span data-ttu-id="6d271-198">Дополнительные сведения о ветви репозитория.</span><span class="sxs-lookup"><span data-stu-id="6d271-198">Optional repository branch information.</span></span> <span data-ttu-id="6d271-199">Для включения этого свойства также необходимо указать *репоситорюрл* .</span><span class="sxs-lookup"><span data-stu-id="6d271-199">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="6d271-200">Пример: *master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="6d271-200">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="6d271-201">Репозиторий/фиксация</span><span class="sxs-lookup"><span data-stu-id="6d271-201">Repository/Commit</span></span> | <span data-ttu-id="6d271-202">репоситорикоммит</span><span class="sxs-lookup"><span data-stu-id="6d271-202">RepositoryCommit</span></span> | <span data-ttu-id="6d271-203">пустой</span><span class="sxs-lookup"><span data-stu-id="6d271-203">empty</span></span> | <span data-ttu-id="6d271-204">Необязательная фиксация или набор изменений репозитория для указания источника, на основе которого был создан пакет.</span><span class="sxs-lookup"><span data-stu-id="6d271-204">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="6d271-205">Для включения этого свойства также необходимо указать *репоситорюрл* .</span><span class="sxs-lookup"><span data-stu-id="6d271-205">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="6d271-206">Пример *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="6d271-206">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="6d271-207">PackageType</span><span class="sxs-lookup"><span data-stu-id="6d271-207">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="6d271-208">Сводка</span><span class="sxs-lookup"><span data-stu-id="6d271-208">Summary</span></span> | <span data-ttu-id="6d271-209">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="6d271-209">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="6d271-210">Входные данные целевого объекта pack</span><span class="sxs-lookup"><span data-stu-id="6d271-210">pack target inputs</span></span>

- <span data-ttu-id="6d271-211">IsPackable</span><span class="sxs-lookup"><span data-stu-id="6d271-211">IsPackable</span></span>
- <span data-ttu-id="6d271-212">суппрессдепенденЦиесвхенпаккинг</span><span class="sxs-lookup"><span data-stu-id="6d271-212">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="6d271-213">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="6d271-213">PackageVersion</span></span>
- <span data-ttu-id="6d271-214">PackageId</span><span class="sxs-lookup"><span data-stu-id="6d271-214">PackageId</span></span>
- <span data-ttu-id="6d271-215">Authors</span><span class="sxs-lookup"><span data-stu-id="6d271-215">Authors</span></span>
- <span data-ttu-id="6d271-216">Описание</span><span class="sxs-lookup"><span data-stu-id="6d271-216">Description</span></span>
- <span data-ttu-id="6d271-217">Copyright</span><span class="sxs-lookup"><span data-stu-id="6d271-217">Copyright</span></span>
- <span data-ttu-id="6d271-218">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="6d271-218">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="6d271-219">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="6d271-219">DevelopmentDependency</span></span>
- <span data-ttu-id="6d271-220">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="6d271-220">PackageLicenseExpression</span></span>
- <span data-ttu-id="6d271-221">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="6d271-221">PackageLicenseFile</span></span>
- <span data-ttu-id="6d271-222">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="6d271-222">PackageLicenseUrl</span></span>
- <span data-ttu-id="6d271-223">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="6d271-223">PackageProjectUrl</span></span>
- <span data-ttu-id="6d271-224">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="6d271-224">PackageIconUrl</span></span>
- <span data-ttu-id="6d271-225">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="6d271-225">PackageReleaseNotes</span></span>
- <span data-ttu-id="6d271-226">PackageTags</span><span class="sxs-lookup"><span data-stu-id="6d271-226">PackageTags</span></span>
- <span data-ttu-id="6d271-227">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="6d271-227">PackageOutputPath</span></span>
- <span data-ttu-id="6d271-228">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="6d271-228">IncludeSymbols</span></span>
- <span data-ttu-id="6d271-229">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="6d271-229">IncludeSource</span></span>
- <span data-ttu-id="6d271-230">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="6d271-230">PackageTypes</span></span>
- <span data-ttu-id="6d271-231">IsTool</span><span class="sxs-lookup"><span data-stu-id="6d271-231">IsTool</span></span>
- <span data-ttu-id="6d271-232">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="6d271-232">RepositoryUrl</span></span>
- <span data-ttu-id="6d271-233">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="6d271-233">RepositoryType</span></span>
- <span data-ttu-id="6d271-234">репоситорибранч</span><span class="sxs-lookup"><span data-stu-id="6d271-234">RepositoryBranch</span></span>
- <span data-ttu-id="6d271-235">репоситорикоммит</span><span class="sxs-lookup"><span data-stu-id="6d271-235">RepositoryCommit</span></span>
- <span data-ttu-id="6d271-236">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="6d271-236">NoPackageAnalysis</span></span>
- <span data-ttu-id="6d271-237">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="6d271-237">MinClientVersion</span></span>
- <span data-ttu-id="6d271-238">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="6d271-238">IncludeBuildOutput</span></span>
- <span data-ttu-id="6d271-239">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="6d271-239">IncludeContentInPack</span></span>
- <span data-ttu-id="6d271-240">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="6d271-240">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="6d271-241">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="6d271-241">ContentTargetFolders</span></span>
- <span data-ttu-id="6d271-242">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="6d271-242">NuspecFile</span></span>
- <span data-ttu-id="6d271-243">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="6d271-243">NuspecBasePath</span></span>
- <span data-ttu-id="6d271-244">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="6d271-244">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="6d271-245">Сценарии использования pack</span><span class="sxs-lookup"><span data-stu-id="6d271-245">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="6d271-246">Подавлять зависимости</span><span class="sxs-lookup"><span data-stu-id="6d271-246">Suppress dependencies</span></span>

<span data-ttu-id="6d271-247">Чтобы исключить зависимости пакета из созданного пакета NuGet, `SuppressDependenciesWhenPacking` задайте `true` для значение, которое позволит пропустить все зависимости из созданного файла nupkg.</span><span class="sxs-lookup"><span data-stu-id="6d271-247">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="6d271-248">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="6d271-248">PackageIconUrl</span></span>

<span data-ttu-id="6d271-249">Как часть изменения для проблемы с [NuGet 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` в конечном итоге будет изменен на `PackageIconUri` и может быть относительным путем к файлу значка, который будет включен в корень полученного пакета.</span><span class="sxs-lookup"><span data-stu-id="6d271-249">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="6d271-250">Выходные сборки</span><span class="sxs-lookup"><span data-stu-id="6d271-250">Output assemblies</span></span>

<span data-ttu-id="6d271-251">`nuget pack` копирует выходные файлы с расширениями `.exe`, `.dll`, `.xml`, `.winmd`, `.json` и `.pri`.</span><span class="sxs-lookup"><span data-stu-id="6d271-251">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="6d271-252">Копируемые выходные файлы зависят от того, что MSBuild предоставляет из целевого объекта `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="6d271-252">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="6d271-253">Существует два свойства MSBuild, которые можно использовать в файле проекта или командной строке для управления местом назначения для выходных сборок:</span><span class="sxs-lookup"><span data-stu-id="6d271-253">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="6d271-254">`IncludeBuildOutput`: Логическое значение, определяющее, следует ли включать в пакет сборки выходных данных сборки.</span><span class="sxs-lookup"><span data-stu-id="6d271-254">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="6d271-255">`BuildOutputTargetFolder`: Указывает папку, в которой должны размещаться выходные сборки.</span><span class="sxs-lookup"><span data-stu-id="6d271-255">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="6d271-256">Выходные сборки (и другие выходные файлы) копируются в соответствующие папки платформы.</span><span class="sxs-lookup"><span data-stu-id="6d271-256">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="6d271-257">Ссылки на пакеты</span><span class="sxs-lookup"><span data-stu-id="6d271-257">Package references</span></span>

<span data-ttu-id="6d271-258">См. раздел [Ссылки на пакеты в файлах проекта](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="6d271-258">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="6d271-259">Перекрестные ссылки между проектами</span><span class="sxs-lookup"><span data-stu-id="6d271-259">Project to project references</span></span>

<span data-ttu-id="6d271-260">Перекрестные ссылки между проектами по умолчанию считаются ссылками на пакет NuGet, например:</span><span class="sxs-lookup"><span data-stu-id="6d271-260">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="6d271-261">Вы также можете добавить в ссылку на проект следующие метаданные:</span><span class="sxs-lookup"><span data-stu-id="6d271-261">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="6d271-262">Включение содержимого в пакет</span><span class="sxs-lookup"><span data-stu-id="6d271-262">Including content in a package</span></span>

<span data-ttu-id="6d271-263">Чтобы включить содержимое, добавьте дополнительные метаданные для существующего элемента `<Content>`.</span><span class="sxs-lookup"><span data-stu-id="6d271-263">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="6d271-264">По умолчанию все данные типа "Content" включаются в пакет, если только вы не переопределите такое поведение с помощью записей, аналогичных следующим:</span><span class="sxs-lookup"><span data-stu-id="6d271-264">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="6d271-265">По умолчанию все данные добавляются в корень папки `content` и `contentFiles\any\<target_framework>` в пакете и сохраняют относительную структуру папок, если только не указан путь к пакету:</span><span class="sxs-lookup"><span data-stu-id="6d271-265">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="6d271-266">Если требуется скопировать все содержимое только в определенные корневые папки (вместо `content` и `contentFiles`), можно использовать свойство MSBuild `ContentTargetFolders`, которое по умолчанию имеет значение "content;contentFiles", но может принимать любые другие имена папок.</span><span class="sxs-lookup"><span data-stu-id="6d271-266">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="6d271-267">Обратите внимание, если указать "contentFiles" в `ContentTargetFolders`, файлы помещаются в `contentFiles\any\<target_framework>` или `contentFiles\<language>\<target_framework>` в зависимости от `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="6d271-267">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="6d271-268">`PackagePath` может быть набором целевых путей, разделенных точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="6d271-268">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="6d271-269">Если указан пустой путь к пакету, файл добавляется в корневой каталог пакета.</span><span class="sxs-lookup"><span data-stu-id="6d271-269">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="6d271-270">Например, следующий код добавляет `libuv.txt` в `content\myfiles`, `content\samples` и корневой каталог пакета:</span><span class="sxs-lookup"><span data-stu-id="6d271-270">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="6d271-271">Имеется также свойство MSBuild `$(IncludeContentInPack)`, которое по умолчанию равно `true`.</span><span class="sxs-lookup"><span data-stu-id="6d271-271">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="6d271-272">Если оно имеет значение `false` для какого-либо проекта, то содержимое этого проекта не включается в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="6d271-272">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="6d271-273">Другие относящиеся к pack метаданные, которые можно задать для любого из указанных выше элементов, включают ```<PackageCopyToOutput>``` и ```<PackageFlatten>```, задающие значения ```CopyToOutput``` и ```Flatten``` для записи ```contentFiles``` в выходном файле NUSPEC.</span><span class="sxs-lookup"><span data-stu-id="6d271-273">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="6d271-274">Кроме элементов содержимого, метаданные `<Pack>` и `<PackagePath>` также можно задать для файлов с действием сборки Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource или None.</span><span class="sxs-lookup"><span data-stu-id="6d271-274">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="6d271-275">Чтобы объект pack добавил имя файла в путь к пакету при использовании стандартных масок, путь к пакету должен заканчиваться символом разделителя папок, в противном случае этот путь считается полным путем, включающим имя файла.</span><span class="sxs-lookup"><span data-stu-id="6d271-275">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="6d271-276">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="6d271-276">IncludeSymbols</span></span>

<span data-ttu-id="6d271-277">При использовании `MSBuild -t:pack -p:IncludeSymbols=true` соответствующие файлы `.pdb` копируются вместе с другими выходными файлами (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="6d271-277">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="6d271-278">Обратите внимание, что при задании `IncludeSymbols=true` создается обычный пакет *и* пакет символов.</span><span class="sxs-lookup"><span data-stu-id="6d271-278">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="6d271-279">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="6d271-279">IncludeSource</span></span>

<span data-ttu-id="6d271-280">Аналогично `IncludeSymbols`, только копирует исходные файлы вместе с файлами `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="6d271-280">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="6d271-281">Все файлы типа `Compile` копируются в `src\<ProjectName>\` с сохранением относительной структуры папок в итоговом пакете.</span><span class="sxs-lookup"><span data-stu-id="6d271-281">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="6d271-282">То же самое происходит с исходными файлами любого `ProjectReference`, у которого `TreatAsPackageReference` имеет значение `false`.</span><span class="sxs-lookup"><span data-stu-id="6d271-282">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="6d271-283">Если файл типа Compile находится вне папки проекта, он просто добавляется в `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="6d271-283">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="6d271-284">Упаковка выражения лицензии или файла лицензии</span><span class="sxs-lookup"><span data-stu-id="6d271-284">Packing a license expression or a license file</span></span>

<span data-ttu-id="6d271-285">При использовании выражения лицензии следует использовать свойство Паккажелиценсикспрессион.</span><span class="sxs-lookup"><span data-stu-id="6d271-285">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="6d271-286">[Пример выражения лицензии](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="6d271-286">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="6d271-287">Дополнительные [сведения о лицензионных выражениях и лицензиях, принимаемых NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="6d271-287">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="6d271-288">При упаковке файла лицензии необходимо использовать свойство Паккажелиценсефиле, чтобы указать путь к пакету относительно корня пакета.</span><span class="sxs-lookup"><span data-stu-id="6d271-288">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="6d271-289">Кроме того, необходимо убедиться, что файл включен в пакет.</span><span class="sxs-lookup"><span data-stu-id="6d271-289">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="6d271-290">Например:</span><span class="sxs-lookup"><span data-stu-id="6d271-290">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="6d271-291">[Пример файла лицензии](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="6d271-291">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="6d271-292">IsTool</span><span class="sxs-lookup"><span data-stu-id="6d271-292">IsTool</span></span>

<span data-ttu-id="6d271-293">При использовании `MSBuild -t:pack -p:IsTool=true` все выходные файлы, как указано в сценарии [Выходные сборки](#output-assemblies), копируются в папку `tools` вместо папки `lib`.</span><span class="sxs-lookup"><span data-stu-id="6d271-293">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="6d271-294">Обратите внимание, что это свойство отличается от `DotNetCliTool`, которое указывается путем задания `PackageType` в файле `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="6d271-294">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="6d271-295">Упаковка с помощью NUSPEC</span><span class="sxs-lookup"><span data-stu-id="6d271-295">Packing using a .nuspec</span></span>

<span data-ttu-id="6d271-296">Хотя рекомендуется включить в файл проекта [все свойства](../reference/msbuild-targets.md#pack-target) , которые обычно находятся в `.nuspec` файле, можно использовать `.nuspec` файл для упаковки проекта.</span><span class="sxs-lookup"><span data-stu-id="6d271-296">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="6d271-297">Для проекта в стиле, отличном от SDK, `PackageReference`который использует, необходимо `NuGet.Build.Tasks.Pack.targets` импортировать, чтобы можно было выполнить задачу «Pack».</span><span class="sxs-lookup"><span data-stu-id="6d271-297">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="6d271-298">Вам по-прежнему потребуется восстановить проект, чтобы можно было упаковать файл nuspec.</span><span class="sxs-lookup"><span data-stu-id="6d271-298">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="6d271-299">(Проект в стиле SDK включает целевые объекты Pack по умолчанию.)</span><span class="sxs-lookup"><span data-stu-id="6d271-299">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="6d271-300">Целевая платформа файла проекта несущественна и не используется при упаковке nuspec.</span><span class="sxs-lookup"><span data-stu-id="6d271-300">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="6d271-301">Следующие три свойства MSBuild связаны с упаковкой с помощью `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="6d271-301">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="6d271-302">`NuspecFile`: относительный или абсолютный путь к файлу `.nuspec`, используемому для упаковки.</span><span class="sxs-lookup"><span data-stu-id="6d271-302">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="6d271-303">`NuspecProperties`: список разделенных точками с запятой пар "ключ-значение".</span><span class="sxs-lookup"><span data-stu-id="6d271-303">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="6d271-304">Из-за особенностей работы анализа в командной строке MSBuild несколько свойств нужно указать следующим образом: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="6d271-304">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="6d271-305">`NuspecBasePath`: Базовый путь `.nuspec` к файлу.</span><span class="sxs-lookup"><span data-stu-id="6d271-305">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="6d271-306">Если вы используете `dotnet.exe` для упаковки проекта, воспользуйтесь командой, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="6d271-306">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="6d271-307">Если вы используете MSBuild для упаковки проекта, воспользуйтесь командой, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="6d271-307">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="6d271-308">Обратите внимание, что упаковка a nuspec с помощью DotNet. exe или MSBuild также ведет к построению проекта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6d271-308">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="6d271-309">Это можно избежать, передав ```--no-build``` свойство в файл DotNet. exe, эквивалентное параметру ```<NoBuild>true</NoBuild> ``` в файле проекта, а также задав параметр ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="6d271-309">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="6d271-310">Пример файла *. csproj* для упаковки файла nuspec:</span><span class="sxs-lookup"><span data-stu-id="6d271-310">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="6d271-311">Дополнительные точки расширения для создания настраиваемого пакета</span><span class="sxs-lookup"><span data-stu-id="6d271-311">Advanced extension points to create customized package</span></span>

<span data-ttu-id="6d271-312">`pack` Целевой объект предоставляет две точки расширения, которые выполняются во внутренней и целевой сборке конкретной платформы.</span><span class="sxs-lookup"><span data-stu-id="6d271-312">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="6d271-313">Поддержка точек расширения включает в пакет содержимое и сборки, относящиеся к целевой платформе.</span><span class="sxs-lookup"><span data-stu-id="6d271-313">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="6d271-314">`TargetsForTfmSpecificBuildOutput`мишень Используется для файлов в `lib` папке или в папке, заданной с помощью. `BuildOutputTargetFolder`</span><span class="sxs-lookup"><span data-stu-id="6d271-314">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="6d271-315">`TargetsForTfmSpecificContentInPackage`мишень Используется для файлов за пределами `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="6d271-315">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="6d271-316">таржетсфортфмспеЦификбуилдаутпут</span><span class="sxs-lookup"><span data-stu-id="6d271-316">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="6d271-317">Напишите настраиваемый целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificBuildOutput)` свойства.</span><span class="sxs-lookup"><span data-stu-id="6d271-317">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="6d271-318">Для файлов, которые необходимо `BuildOutputTargetFolder` переключать в (LIB по умолчанию), целевой объект должен записать эти файлы в ItemGroup `BuildOutputInPackage` и задать следующие два значения метаданных:</span><span class="sxs-lookup"><span data-stu-id="6d271-318">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="6d271-319">`FinalOutputPath`: Абсолютный путь к файлу; Если этот параметр не указан, для вычисления исходного пути используется удостоверение.</span><span class="sxs-lookup"><span data-stu-id="6d271-319">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="6d271-320">`TargetPath`:  Используемых Задается, когда файл необходимо переключиться во `lib\<TargetFramework>` вложенную папку в, например вспомогательные сборки, которые находятся в соответствующих папках языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="6d271-320">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="6d271-321">По умолчанию используется имя файла.</span><span class="sxs-lookup"><span data-stu-id="6d271-321">Defaults to the name of the file.</span></span>

<span data-ttu-id="6d271-322">Пример</span><span class="sxs-lookup"><span data-stu-id="6d271-322">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="6d271-323">таржетсфортфмспеЦификконтентинпаккаже</span><span class="sxs-lookup"><span data-stu-id="6d271-323">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="6d271-324">Напишите настраиваемый целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificContentInPackage)` свойства.</span><span class="sxs-lookup"><span data-stu-id="6d271-324">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="6d271-325">Для всех файлов, включаемых в пакет, целевой объект должен записать эти файлы в ItemGroup `TfmSpecificPackageFile` и задать следующие необязательные метаданные:</span><span class="sxs-lookup"><span data-stu-id="6d271-325">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="6d271-326">`PackagePath`: Путь, по которому файл должен быть выведен в пакете.</span><span class="sxs-lookup"><span data-stu-id="6d271-326">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="6d271-327">NuGet выдает предупреждение, если в один и тот же путь к пакету добавляется несколько файлов.</span><span class="sxs-lookup"><span data-stu-id="6d271-327">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="6d271-328">`BuildAction`: Действие сборки, присваиваемое файлу, требуется только в том случае, если путь к пакету `contentFiles` находится в папке.</span><span class="sxs-lookup"><span data-stu-id="6d271-328">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="6d271-329">По умолчанию используется значение "нет".</span><span class="sxs-lookup"><span data-stu-id="6d271-329">Defaults to "None".</span></span>

<span data-ttu-id="6d271-330">Пример:</span><span class="sxs-lookup"><span data-stu-id="6d271-330">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="6d271-331">Целевой объект restore</span><span class="sxs-lookup"><span data-stu-id="6d271-331">restore target</span></span>

<span data-ttu-id="6d271-332">`MSBuild -t:restore` (который `nuget restore` и `dotnet restore` используют с проектами .NET Core) восстанавливает пакеты, на которые ссылается файл проекта:</span><span class="sxs-lookup"><span data-stu-id="6d271-332">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="6d271-333">Чтение перекрестных ссылок между проектами.</span><span class="sxs-lookup"><span data-stu-id="6d271-333">Read all project to project references</span></span>
1. <span data-ttu-id="6d271-334">Чтение свойств проекта, чтобы найти промежуточную папку и целевые платформы.</span><span class="sxs-lookup"><span data-stu-id="6d271-334">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="6d271-335">Передача данных MSBuild в NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="6d271-335">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="6d271-336">Запуск восстановления.</span><span class="sxs-lookup"><span data-stu-id="6d271-336">Run restore</span></span>
1. <span data-ttu-id="6d271-337">Скачивание пакетов.</span><span class="sxs-lookup"><span data-stu-id="6d271-337">Download packages</span></span>
1. <span data-ttu-id="6d271-338">Запись файла ресурсов, целевых объектов и свойств.</span><span class="sxs-lookup"><span data-stu-id="6d271-338">Write assets file, targets, and props</span></span>

<span data-ttu-id="6d271-339">Целевой объект работает только для проектов, использующих формат PackageReference.  `restore`</span><span class="sxs-lookup"><span data-stu-id="6d271-339">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="6d271-340">Он **не** работает для проектов, использующих этот `packages.config` формат; вместо этого используйте [Восстановление NuGet](../reference/cli-reference/cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="6d271-340">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="6d271-341">Свойства восстановления</span><span class="sxs-lookup"><span data-stu-id="6d271-341">Restore properties</span></span>

<span data-ttu-id="6d271-342">Дополнительные параметры восстановления могут поступать из свойств MSBuild в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="6d271-342">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="6d271-343">Значения также можно задать из командной строки с помощью параметра `-p:` (см. примеры ниже).</span><span class="sxs-lookup"><span data-stu-id="6d271-343">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="6d271-344">Свойство.</span><span class="sxs-lookup"><span data-stu-id="6d271-344">Property</span></span> | <span data-ttu-id="6d271-345">Описание</span><span class="sxs-lookup"><span data-stu-id="6d271-345">Description</span></span> |
|--------|--------|
| <span data-ttu-id="6d271-346">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="6d271-346">RestoreSources</span></span> | <span data-ttu-id="6d271-347">Разделенный точками с запятой список источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="6d271-347">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="6d271-348">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="6d271-348">RestorePackagesPath</span></span> | <span data-ttu-id="6d271-349">Путь к папке пакетов пользователя.</span><span class="sxs-lookup"><span data-stu-id="6d271-349">User packages folder path.</span></span> |
| <span data-ttu-id="6d271-350">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="6d271-350">RestoreDisableParallel</span></span> | <span data-ttu-id="6d271-351">Ограничение скачиваний до одного за раз.</span><span class="sxs-lookup"><span data-stu-id="6d271-351">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="6d271-352">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="6d271-352">RestoreConfigFile</span></span> | <span data-ttu-id="6d271-353">Путь к применяемому файлу `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="6d271-353">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="6d271-354">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="6d271-354">RestoreNoCache</span></span> | <span data-ttu-id="6d271-355">Значение true позволяет избежать использования кэшированных пакетов.</span><span class="sxs-lookup"><span data-stu-id="6d271-355">If true, avoids using cached packages.</span></span> <span data-ttu-id="6d271-356">См. раздел [Управление глобальными пакетами и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="6d271-356">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="6d271-357">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="6d271-357">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="6d271-358">Если значение равно true, нерабочие или отсутствующие источники пакетов игнорируются.</span><span class="sxs-lookup"><span data-stu-id="6d271-358">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="6d271-359">ресторефаллбаккфолдерс</span><span class="sxs-lookup"><span data-stu-id="6d271-359">RestoreFallbackFolders</span></span> | <span data-ttu-id="6d271-360">Резервные папки используются так же, как и папка User Packages.</span><span class="sxs-lookup"><span data-stu-id="6d271-360">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="6d271-361">рестореаддитионалпрожектсаурцес</span><span class="sxs-lookup"><span data-stu-id="6d271-361">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="6d271-362">Дополнительные источники, используемые во время восстановления.</span><span class="sxs-lookup"><span data-stu-id="6d271-362">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="6d271-363">рестореаддитионалпрожектфаллбаккфолдерс</span><span class="sxs-lookup"><span data-stu-id="6d271-363">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="6d271-364">Дополнительные резервные папки для использования во время восстановления.</span><span class="sxs-lookup"><span data-stu-id="6d271-364">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="6d271-365">рестореаддитионалпрожектфаллбаккфолдерсексклудес</span><span class="sxs-lookup"><span data-stu-id="6d271-365">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="6d271-366">Исключает резервные папки, указанные в`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="6d271-366">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="6d271-367">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="6d271-367">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="6d271-368">Путь к `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="6d271-368">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="6d271-369">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="6d271-369">RestoreGraphProjectInput</span></span> | <span data-ttu-id="6d271-370">Разделенный точками с запятой список проектов для восстановления, который должен содержать абсолютные пути.</span><span class="sxs-lookup"><span data-stu-id="6d271-370">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="6d271-371">рестореусескипнонексистенттаржетс</span><span class="sxs-lookup"><span data-stu-id="6d271-371">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="6d271-372">При сборе проектов с помощью MSBuild определяет, будут ли они собраны с `SkipNonexistentTargets` помощью оптимизации.</span><span class="sxs-lookup"><span data-stu-id="6d271-372">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="6d271-373">Если значение не задано, по `true`умолчанию используется значение.</span><span class="sxs-lookup"><span data-stu-id="6d271-373">When not set, defaults to `true`.</span></span> <span data-ttu-id="6d271-374">Следствием является быстрое поведение при сбое, если целевые объекты проекта не могут быть импортированы.</span><span class="sxs-lookup"><span data-stu-id="6d271-374">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="6d271-375">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="6d271-375">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="6d271-376">Папка Output, по умолчанию `BaseIntermediateOutputPath` — `obj` и папка.</span><span class="sxs-lookup"><span data-stu-id="6d271-376">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="6d271-377">Примеры</span><span class="sxs-lookup"><span data-stu-id="6d271-377">Examples</span></span>

<span data-ttu-id="6d271-378">Командная строка:</span><span class="sxs-lookup"><span data-stu-id="6d271-378">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="6d271-379">Файл проекта:</span><span class="sxs-lookup"><span data-stu-id="6d271-379">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="6d271-380">Выходные данные восстановления</span><span class="sxs-lookup"><span data-stu-id="6d271-380">Restore outputs</span></span>

<span data-ttu-id="6d271-381">Операция восстановления создает в папке сборки `obj` следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="6d271-381">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="6d271-382">Файл</span><span class="sxs-lookup"><span data-stu-id="6d271-382">File</span></span> | <span data-ttu-id="6d271-383">Описание</span><span class="sxs-lookup"><span data-stu-id="6d271-383">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="6d271-384">Содержит диаграмму зависимостей всех ссылок на пакеты.</span><span class="sxs-lookup"><span data-stu-id="6d271-384">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="6d271-385">Ссылки на свойства MSBuild, содержащиеся в пакетах.</span><span class="sxs-lookup"><span data-stu-id="6d271-385">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="6d271-386">Ссылки на целевые объекты MSBuild, содержащиеся в пакетах.</span><span class="sxs-lookup"><span data-stu-id="6d271-386">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="6d271-387">Восстановление и сборка с помощью одной команды MSBuild</span><span class="sxs-lookup"><span data-stu-id="6d271-387">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="6d271-388">Из-за того, что NuGet может восстанавливать пакеты, которые выводят цели и свойства MSBuild, оценки восстановления и сборки выполняются с разными глобальными свойствами.</span><span class="sxs-lookup"><span data-stu-id="6d271-388">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="6d271-389">Это означает, что следующие действия будут иметь непредсказуемое и неправильное поведение.</span><span class="sxs-lookup"><span data-stu-id="6d271-389">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="6d271-390">Вместо этого рекомендуемый подход:</span><span class="sxs-lookup"><span data-stu-id="6d271-390">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="6d271-391">Одна и та же логика применяется к другим `build`целевым объектам, аналогичным.</span><span class="sxs-lookup"><span data-stu-id="6d271-391">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="6d271-392">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="6d271-392">PackageTargetFallback</span></span>

<span data-ttu-id="6d271-393">Элемент `PackageTargetFallback` позволяет указать набор совместимых целевых объектов, которые следует использовать при восстановлении пакетов.</span><span class="sxs-lookup"><span data-stu-id="6d271-393">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="6d271-394">Он разрешает пакетам, использующим dotnet [TxM](../reference/target-frameworks.md), взаимодействовать с совместимыми пакетами, которые не объявляют dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="6d271-394">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="6d271-395">Таким образом, если в проекте используется dotnet TxM, все пакеты, от которых вы зависите, должны также содержать dotnet TxM. В противном случае нужно добавить `<PackageTargetFallback>` в проект, чтобы обеспечить совместимость с платформами, отличными от dotnet.</span><span class="sxs-lookup"><span data-stu-id="6d271-395">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="6d271-396">Например, если в проекте используется `netstandard1.6` TxM, а зависимый пакет содержит только `lib/net45/a.dll` и `lib/portable-net45+win81/a.dll`, то сборка проекта завершится со сбоем.</span><span class="sxs-lookup"><span data-stu-id="6d271-396">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="6d271-397">Если вы хотите использовать вторую библиотеку DLL, можете добавить `PackageTargetFallback` следующим образом, чтобы обозначить совместимость библиотеки DLL `portable-net45+win81`:</span><span class="sxs-lookup"><span data-stu-id="6d271-397">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="6d271-398">Чтобы объявить откат для всех целевых объектов в проекте, оставьте атрибут `Condition`.</span><span class="sxs-lookup"><span data-stu-id="6d271-398">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="6d271-399">Кроме того, можно расширить существующий `PackageTargetFallback`, включив `$(PackageTargetFallback)`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="6d271-399">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="6d271-400">Замена одной библиотеки из графа восстановления</span><span class="sxs-lookup"><span data-stu-id="6d271-400">Replacing one library from a restore graph</span></span>

<span data-ttu-id="6d271-401">Если операция восстановления предоставляет неправильную сборку, вы можете исключить значение по умолчанию для этого пакета, заменив его своим значением.</span><span class="sxs-lookup"><span data-stu-id="6d271-401">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="6d271-402">Первый с `PackageReference` верхнего уровня, исключите все ресурсы:</span><span class="sxs-lookup"><span data-stu-id="6d271-402">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="6d271-403">После этого добавьте собственную ссылку на соответствующую локальную копию библиотеки DLL:</span><span class="sxs-lookup"><span data-stu-id="6d271-403">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
