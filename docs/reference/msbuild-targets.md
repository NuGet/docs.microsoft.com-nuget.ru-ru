---
title: Объекты pack и restore NuGet в качестве целевых объектов MSBuild
description: Объекты pack и restore NuGet могут выступать непосредственно в качестве целевых объектов MSBuild в NuGet 4.0+.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: d8d1b2ef0185381d16c1bb73035588fe90bcfd14
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959683"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="c879d-103">Объекты pack и restore NuGet в качестве целевых объектов MSBuild</span><span class="sxs-lookup"><span data-stu-id="c879d-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="c879d-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="c879d-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="c879d-105">В формате [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + может хранить все метаданные манифеста непосредственно в файле проекта вместо использования отдельного `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="c879d-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="c879d-106">При использовании MSBuild 15.1+ NuGet также является привилегированным компонентом MSBuild с целевыми объектами `pack` и `restore`, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="c879d-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="c879d-107">Эти целевые объекты позволяют работать с NuGet, как с любой другой задачей или другим целевым объектом MSBuild.</span><span class="sxs-lookup"><span data-stu-id="c879d-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="c879d-108">Инструкции по созданию пакета NuGet с помощью MSBuild см. в статье [Создание пакета NuGet с помощью MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="c879d-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="c879d-109">(Для NuGet 3.x и более ранних версий можно использовать команды [pack](../reference/cli-reference/cli-ref-pack.md) и [restore](../reference/cli-reference/cli-ref-restore.md) в NuGet CLI.)</span><span class="sxs-lookup"><span data-stu-id="c879d-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="c879d-110">Порядок сборки целевого объекта</span><span class="sxs-lookup"><span data-stu-id="c879d-110">Target build order</span></span>

<span data-ttu-id="c879d-111">Так как `pack` и `restore` являются целевыми объектами MSBuild, вы можете обращаться к ним для улучшения рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="c879d-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="c879d-112">Например, предположим, что вам нужно скопировать пакет в общую сетевую папку после его упаковки.</span><span class="sxs-lookup"><span data-stu-id="c879d-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="c879d-113">Это можно сделать, добавив следующий код в файл проекта:</span><span class="sxs-lookup"><span data-stu-id="c879d-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="c879d-114">Аналогичным образом, вы можете создать задачу MSBuild и собственный целевой объект и использовать свойства NuGet в этой задаче MSBuild.</span><span class="sxs-lookup"><span data-stu-id="c879d-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="c879d-115">`$(OutputPath)`является относительным и предполагает, что команда выполняется из корневого каталога проекта.</span><span class="sxs-lookup"><span data-stu-id="c879d-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="c879d-116">Целевой объект pack</span><span class="sxs-lookup"><span data-stu-id="c879d-116">pack target</span></span>

<span data-ttu-id="c879d-117">Для .NET Standard проектов, использующих формат PackageReference `msbuild -t:pack` , команда рисует входные данные из файла проекта для использования при создании пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="c879d-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="c879d-118">В следующей таблице описываются свойства MSBuild, которые можно добавить в файл проекта в первом узле `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="c879d-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="c879d-119">Эти изменения легко внести в Visual Studio 2017 и более поздней версии, щелкнув проект правой кнопкой мыши и выбрав пункт **Изменить {project_name}** .</span><span class="sxs-lookup"><span data-stu-id="c879d-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="c879d-120">Для удобства таблица упорядочена по эквивалентным свойствам в [файле `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="c879d-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="c879d-121">Обратите внимание, что свойства `Owners` и `Summary` из `.nuspec` не поддерживаются в MSBuild.</span><span class="sxs-lookup"><span data-stu-id="c879d-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="c879d-122">Значение атрибута или NuSpec</span><span class="sxs-lookup"><span data-stu-id="c879d-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="c879d-123">Свойство MSBuild</span><span class="sxs-lookup"><span data-stu-id="c879d-123">MSBuild Property</span></span> | <span data-ttu-id="c879d-124">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="c879d-124">Default</span></span> | <span data-ttu-id="c879d-125">Примечания</span><span class="sxs-lookup"><span data-stu-id="c879d-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="c879d-126">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="c879d-126">Id</span></span> | <span data-ttu-id="c879d-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="c879d-127">PackageId</span></span> | <span data-ttu-id="c879d-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="c879d-128">AssemblyName</span></span> | <span data-ttu-id="c879d-129">$(AssemblyName) из MSBuild</span><span class="sxs-lookup"><span data-stu-id="c879d-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="c879d-130">Версия</span><span class="sxs-lookup"><span data-stu-id="c879d-130">Version</span></span> | <span data-ttu-id="c879d-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="c879d-131">PackageVersion</span></span> | <span data-ttu-id="c879d-132">Версия</span><span class="sxs-lookup"><span data-stu-id="c879d-132">Version</span></span> | <span data-ttu-id="c879d-133">Это значение совместимо с SemVer, например "1.0.0", "1.0.0-beta" или "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="c879d-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="c879d-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="c879d-134">VersionPrefix</span></span> | <span data-ttu-id="c879d-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="c879d-135">PackageVersionPrefix</span></span> | <span data-ttu-id="c879d-136">пустой</span><span class="sxs-lookup"><span data-stu-id="c879d-136">empty</span></span> | <span data-ttu-id="c879d-137">Задав PackageVersion, вы перезапишите PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="c879d-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="c879d-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="c879d-138">VersionSuffix</span></span> | <span data-ttu-id="c879d-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="c879d-139">PackageVersionSuffix</span></span> | <span data-ttu-id="c879d-140">пустой</span><span class="sxs-lookup"><span data-stu-id="c879d-140">empty</span></span> | <span data-ttu-id="c879d-141">$(VersionSuffix) из MSBuild.</span><span class="sxs-lookup"><span data-stu-id="c879d-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="c879d-142">Задав PackageVersion, вы перезапишите PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="c879d-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="c879d-143">Authors</span><span class="sxs-lookup"><span data-stu-id="c879d-143">Authors</span></span> | <span data-ttu-id="c879d-144">Authors</span><span class="sxs-lookup"><span data-stu-id="c879d-144">Authors</span></span> | <span data-ttu-id="c879d-145">Имя текущего пользователя</span><span class="sxs-lookup"><span data-stu-id="c879d-145">Username of the current user</span></span> | |
| <span data-ttu-id="c879d-146">Владельцы</span><span class="sxs-lookup"><span data-stu-id="c879d-146">Owners</span></span> | <span data-ttu-id="c879d-147">Н/Д</span><span class="sxs-lookup"><span data-stu-id="c879d-147">N/A</span></span> | <span data-ttu-id="c879d-148">Не существует в NuSpec</span><span class="sxs-lookup"><span data-stu-id="c879d-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="c879d-149">Заголовок</span><span class="sxs-lookup"><span data-stu-id="c879d-149">Title</span></span> | <span data-ttu-id="c879d-150">Заголовок</span><span class="sxs-lookup"><span data-stu-id="c879d-150">Title</span></span> | <span data-ttu-id="c879d-151">Идентификатор пакета</span><span class="sxs-lookup"><span data-stu-id="c879d-151">The PackageId</span></span>| |
| <span data-ttu-id="c879d-152">Описание</span><span class="sxs-lookup"><span data-stu-id="c879d-152">Description</span></span> | <span data-ttu-id="c879d-153">Описание</span><span class="sxs-lookup"><span data-stu-id="c879d-153">Description</span></span> | <span data-ttu-id="c879d-154">"Описание пакета"</span><span class="sxs-lookup"><span data-stu-id="c879d-154">"Package Description"</span></span> | |
| <span data-ttu-id="c879d-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="c879d-155">Copyright</span></span> | <span data-ttu-id="c879d-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="c879d-156">Copyright</span></span> | <span data-ttu-id="c879d-157">пустой</span><span class="sxs-lookup"><span data-stu-id="c879d-157">empty</span></span> | |
| <span data-ttu-id="c879d-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="c879d-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="c879d-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="c879d-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="c879d-160">False</span><span class="sxs-lookup"><span data-stu-id="c879d-160">false</span></span> | |
| <span data-ttu-id="c879d-161">лицензии</span><span class="sxs-lookup"><span data-stu-id="c879d-161">license</span></span> | <span data-ttu-id="c879d-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="c879d-162">PackageLicenseExpression</span></span> | <span data-ttu-id="c879d-163">пустой</span><span class="sxs-lookup"><span data-stu-id="c879d-163">empty</span></span> | <span data-ttu-id="c879d-164">Соответствует`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="c879d-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="c879d-165">лицензии</span><span class="sxs-lookup"><span data-stu-id="c879d-165">license</span></span> | <span data-ttu-id="c879d-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="c879d-166">PackageLicenseFile</span></span> | <span data-ttu-id="c879d-167">пустой</span><span class="sxs-lookup"><span data-stu-id="c879d-167">empty</span></span> | <span data-ttu-id="c879d-168">Соответствует `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="c879d-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="c879d-169">Возможно, потребуется явно упаковать файл лицензии, на который указывает ссылка.</span><span class="sxs-lookup"><span data-stu-id="c879d-169">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="c879d-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="c879d-170">LicenseUrl</span></span> | <span data-ttu-id="c879d-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="c879d-171">PackageLicenseUrl</span></span> | <span data-ttu-id="c879d-172">пустой</span><span class="sxs-lookup"><span data-stu-id="c879d-172">empty</span></span> | <span data-ttu-id="c879d-173">`licenseUrl`является устаревшим, используйте свойство Паккажелиценсикспрессион или Паккажелиценсефиле.</span><span class="sxs-lookup"><span data-stu-id="c879d-173">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="c879d-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="c879d-174">ProjectUrl</span></span> | <span data-ttu-id="c879d-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="c879d-175">PackageProjectUrl</span></span> | <span data-ttu-id="c879d-176">пустой</span><span class="sxs-lookup"><span data-stu-id="c879d-176">empty</span></span> | |
| <span data-ttu-id="c879d-177">IconUrl</span><span class="sxs-lookup"><span data-stu-id="c879d-177">IconUrl</span></span> | <span data-ttu-id="c879d-178">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="c879d-178">PackageIconUrl</span></span> | <span data-ttu-id="c879d-179">пустой</span><span class="sxs-lookup"><span data-stu-id="c879d-179">empty</span></span> | |
| <span data-ttu-id="c879d-180">Теги</span><span class="sxs-lookup"><span data-stu-id="c879d-180">Tags</span></span> | <span data-ttu-id="c879d-181">PackageTags</span><span class="sxs-lookup"><span data-stu-id="c879d-181">PackageTags</span></span> | <span data-ttu-id="c879d-182">пустой</span><span class="sxs-lookup"><span data-stu-id="c879d-182">empty</span></span> | <span data-ttu-id="c879d-183">Теги разделяются точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="c879d-183">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="c879d-184">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="c879d-184">ReleaseNotes</span></span> | <span data-ttu-id="c879d-185">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="c879d-185">PackageReleaseNotes</span></span> | <span data-ttu-id="c879d-186">пустой</span><span class="sxs-lookup"><span data-stu-id="c879d-186">empty</span></span> | |
| <span data-ttu-id="c879d-187">Репозиторий/URL-адрес</span><span class="sxs-lookup"><span data-stu-id="c879d-187">Repository/Url</span></span> | <span data-ttu-id="c879d-188">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="c879d-188">RepositoryUrl</span></span> | <span data-ttu-id="c879d-189">пустой</span><span class="sxs-lookup"><span data-stu-id="c879d-189">empty</span></span> | <span data-ttu-id="c879d-190">URL-адрес репозитория, используемый для клонирования или извлечения исходного кода.</span><span class="sxs-lookup"><span data-stu-id="c879d-190">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="c879d-191">Например *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="c879d-191">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="c879d-192">Репозиторий или тип</span><span class="sxs-lookup"><span data-stu-id="c879d-192">Repository/Type</span></span> | <span data-ttu-id="c879d-193">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="c879d-193">RepositoryType</span></span> | <span data-ttu-id="c879d-194">пустой</span><span class="sxs-lookup"><span data-stu-id="c879d-194">empty</span></span> | <span data-ttu-id="c879d-195">Тип репозитория.</span><span class="sxs-lookup"><span data-stu-id="c879d-195">Repository type.</span></span> <span data-ttu-id="c879d-196">Примеры: *Git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="c879d-196">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="c879d-197">Репозиторий или ветвь</span><span class="sxs-lookup"><span data-stu-id="c879d-197">Repository/Branch</span></span> | <span data-ttu-id="c879d-198">репоситорибранч</span><span class="sxs-lookup"><span data-stu-id="c879d-198">RepositoryBranch</span></span> | <span data-ttu-id="c879d-199">пустой</span><span class="sxs-lookup"><span data-stu-id="c879d-199">empty</span></span> | <span data-ttu-id="c879d-200">Дополнительные сведения о ветви репозитория.</span><span class="sxs-lookup"><span data-stu-id="c879d-200">Optional repository branch information.</span></span> <span data-ttu-id="c879d-201">Для включения этого свойства также необходимо указать *репоситорюрл* .</span><span class="sxs-lookup"><span data-stu-id="c879d-201">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="c879d-202">Пример: *master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="c879d-202">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="c879d-203">Репозиторий/фиксация</span><span class="sxs-lookup"><span data-stu-id="c879d-203">Repository/Commit</span></span> | <span data-ttu-id="c879d-204">репоситорикоммит</span><span class="sxs-lookup"><span data-stu-id="c879d-204">RepositoryCommit</span></span> | <span data-ttu-id="c879d-205">пустой</span><span class="sxs-lookup"><span data-stu-id="c879d-205">empty</span></span> | <span data-ttu-id="c879d-206">Необязательная фиксация или набор изменений репозитория для указания источника, на основе которого был создан пакет.</span><span class="sxs-lookup"><span data-stu-id="c879d-206">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="c879d-207">Для включения этого свойства также необходимо указать *репоситорюрл* .</span><span class="sxs-lookup"><span data-stu-id="c879d-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="c879d-208">Пример *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="c879d-208">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="c879d-209">PackageType</span><span class="sxs-lookup"><span data-stu-id="c879d-209">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="c879d-210">Сводка</span><span class="sxs-lookup"><span data-stu-id="c879d-210">Summary</span></span> | <span data-ttu-id="c879d-211">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="c879d-211">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="c879d-212">Входные данные целевого объекта pack</span><span class="sxs-lookup"><span data-stu-id="c879d-212">pack target inputs</span></span>

- <span data-ttu-id="c879d-213">IsPackable</span><span class="sxs-lookup"><span data-stu-id="c879d-213">IsPackable</span></span>
- <span data-ttu-id="c879d-214">суппрессдепенденЦиесвхенпаккинг</span><span class="sxs-lookup"><span data-stu-id="c879d-214">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="c879d-215">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="c879d-215">PackageVersion</span></span>
- <span data-ttu-id="c879d-216">PackageId</span><span class="sxs-lookup"><span data-stu-id="c879d-216">PackageId</span></span>
- <span data-ttu-id="c879d-217">Authors</span><span class="sxs-lookup"><span data-stu-id="c879d-217">Authors</span></span>
- <span data-ttu-id="c879d-218">Описание</span><span class="sxs-lookup"><span data-stu-id="c879d-218">Description</span></span>
- <span data-ttu-id="c879d-219">Copyright</span><span class="sxs-lookup"><span data-stu-id="c879d-219">Copyright</span></span>
- <span data-ttu-id="c879d-220">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="c879d-220">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="c879d-221">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="c879d-221">DevelopmentDependency</span></span>
- <span data-ttu-id="c879d-222">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="c879d-222">PackageLicenseExpression</span></span>
- <span data-ttu-id="c879d-223">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="c879d-223">PackageLicenseFile</span></span>
- <span data-ttu-id="c879d-224">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="c879d-224">PackageLicenseUrl</span></span>
- <span data-ttu-id="c879d-225">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="c879d-225">PackageProjectUrl</span></span>
- <span data-ttu-id="c879d-226">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="c879d-226">PackageIconUrl</span></span>
- <span data-ttu-id="c879d-227">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="c879d-227">PackageReleaseNotes</span></span>
- <span data-ttu-id="c879d-228">PackageTags</span><span class="sxs-lookup"><span data-stu-id="c879d-228">PackageTags</span></span>
- <span data-ttu-id="c879d-229">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="c879d-229">PackageOutputPath</span></span>
- <span data-ttu-id="c879d-230">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="c879d-230">IncludeSymbols</span></span>
- <span data-ttu-id="c879d-231">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="c879d-231">IncludeSource</span></span>
- <span data-ttu-id="c879d-232">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="c879d-232">PackageTypes</span></span>
- <span data-ttu-id="c879d-233">IsTool</span><span class="sxs-lookup"><span data-stu-id="c879d-233">IsTool</span></span>
- <span data-ttu-id="c879d-234">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="c879d-234">RepositoryUrl</span></span>
- <span data-ttu-id="c879d-235">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="c879d-235">RepositoryType</span></span>
- <span data-ttu-id="c879d-236">репоситорибранч</span><span class="sxs-lookup"><span data-stu-id="c879d-236">RepositoryBranch</span></span>
- <span data-ttu-id="c879d-237">репоситорикоммит</span><span class="sxs-lookup"><span data-stu-id="c879d-237">RepositoryCommit</span></span>
- <span data-ttu-id="c879d-238">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="c879d-238">NoPackageAnalysis</span></span>
- <span data-ttu-id="c879d-239">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="c879d-239">MinClientVersion</span></span>
- <span data-ttu-id="c879d-240">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="c879d-240">IncludeBuildOutput</span></span>
- <span data-ttu-id="c879d-241">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="c879d-241">IncludeContentInPack</span></span>
- <span data-ttu-id="c879d-242">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="c879d-242">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="c879d-243">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="c879d-243">ContentTargetFolders</span></span>
- <span data-ttu-id="c879d-244">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="c879d-244">NuspecFile</span></span>
- <span data-ttu-id="c879d-245">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="c879d-245">NuspecBasePath</span></span>
- <span data-ttu-id="c879d-246">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="c879d-246">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="c879d-247">Сценарии использования pack</span><span class="sxs-lookup"><span data-stu-id="c879d-247">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="c879d-248">Подавлять зависимости</span><span class="sxs-lookup"><span data-stu-id="c879d-248">Suppress dependencies</span></span>

<span data-ttu-id="c879d-249">Чтобы исключить зависимости пакета из созданного пакета NuGet, `SuppressDependenciesWhenPacking` задайте `true` для значение, которое позволит пропустить все зависимости из созданного файла nupkg.</span><span class="sxs-lookup"><span data-stu-id="c879d-249">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="c879d-250">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="c879d-250">PackageIconUrl</span></span>

<span data-ttu-id="c879d-251">Как часть изменения для проблемы с [NuGet 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` в конечном итоге будет изменен на `PackageIconUri` и может быть относительным путем к файлу значка, который будет включен в корень полученного пакета.</span><span class="sxs-lookup"><span data-stu-id="c879d-251">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="c879d-252">Выходные сборки</span><span class="sxs-lookup"><span data-stu-id="c879d-252">Output assemblies</span></span>

<span data-ttu-id="c879d-253">`nuget pack` копирует выходные файлы с расширениями `.exe`, `.dll`, `.xml`, `.winmd`, `.json` и `.pri`.</span><span class="sxs-lookup"><span data-stu-id="c879d-253">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="c879d-254">Копируемые выходные файлы зависят от того, что MSBuild предоставляет из целевого объекта `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="c879d-254">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="c879d-255">Существует два свойства MSBuild, которые можно использовать в файле проекта или командной строке для управления местом назначения для выходных сборок:</span><span class="sxs-lookup"><span data-stu-id="c879d-255">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="c879d-256">`IncludeBuildOutput`: Логическое значение, определяющее, следует ли включать в пакет сборки выходных данных сборки.</span><span class="sxs-lookup"><span data-stu-id="c879d-256">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="c879d-257">`BuildOutputTargetFolder`: Указывает папку, в которой должны размещаться выходные сборки.</span><span class="sxs-lookup"><span data-stu-id="c879d-257">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="c879d-258">Выходные сборки (и другие выходные файлы) копируются в соответствующие папки платформы.</span><span class="sxs-lookup"><span data-stu-id="c879d-258">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="c879d-259">Ссылки на пакеты</span><span class="sxs-lookup"><span data-stu-id="c879d-259">Package references</span></span>

<span data-ttu-id="c879d-260">См. раздел [Ссылки на пакеты в файлах проекта](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="c879d-260">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="c879d-261">Перекрестные ссылки между проектами</span><span class="sxs-lookup"><span data-stu-id="c879d-261">Project to project references</span></span>

<span data-ttu-id="c879d-262">Перекрестные ссылки между проектами по умолчанию считаются ссылками на пакет NuGet, например:</span><span class="sxs-lookup"><span data-stu-id="c879d-262">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="c879d-263">Вы также можете добавить в ссылку на проект следующие метаданные:</span><span class="sxs-lookup"><span data-stu-id="c879d-263">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="c879d-264">Включение содержимого в пакет</span><span class="sxs-lookup"><span data-stu-id="c879d-264">Including content in a package</span></span>

<span data-ttu-id="c879d-265">Чтобы включить содержимое, добавьте дополнительные метаданные для существующего элемента `<Content>`.</span><span class="sxs-lookup"><span data-stu-id="c879d-265">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="c879d-266">По умолчанию все данные типа "Content" включаются в пакет, если только вы не переопределите такое поведение с помощью записей, аналогичных следующим:</span><span class="sxs-lookup"><span data-stu-id="c879d-266">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="c879d-267">По умолчанию все данные добавляются в корень папки `content` и `contentFiles\any\<target_framework>` в пакете и сохраняют относительную структуру папок, если только не указан путь к пакету:</span><span class="sxs-lookup"><span data-stu-id="c879d-267">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="c879d-268">Если требуется скопировать все содержимое только в определенные корневые папки (вместо `content` и `contentFiles`), можно использовать свойство MSBuild `ContentTargetFolders`, которое по умолчанию имеет значение "content;contentFiles", но может принимать любые другие имена папок.</span><span class="sxs-lookup"><span data-stu-id="c879d-268">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="c879d-269">Обратите внимание, если указать "contentFiles" в `ContentTargetFolders`, файлы помещаются в `contentFiles\any\<target_framework>` или `contentFiles\<language>\<target_framework>` в зависимости от `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="c879d-269">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="c879d-270">`PackagePath` может быть набором целевых путей, разделенных точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="c879d-270">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="c879d-271">Если указан пустой путь к пакету, файл добавляется в корневой каталог пакета.</span><span class="sxs-lookup"><span data-stu-id="c879d-271">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="c879d-272">Например, следующий код добавляет `libuv.txt` в `content\myfiles`, `content\samples` и корневой каталог пакета:</span><span class="sxs-lookup"><span data-stu-id="c879d-272">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="c879d-273">Имеется также свойство MSBuild `$(IncludeContentInPack)`, которое по умолчанию равно `true`.</span><span class="sxs-lookup"><span data-stu-id="c879d-273">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="c879d-274">Если оно имеет значение `false` для какого-либо проекта, то содержимое этого проекта не включается в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="c879d-274">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="c879d-275">Другие относящиеся к pack метаданные, которые можно задать для любого из указанных выше элементов, включают ```<PackageCopyToOutput>``` и ```<PackageFlatten>```, задающие значения ```CopyToOutput``` и ```Flatten``` для записи ```contentFiles``` в выходном файле NUSPEC.</span><span class="sxs-lookup"><span data-stu-id="c879d-275">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="c879d-276">Кроме элементов содержимого, метаданные `<Pack>` и `<PackagePath>` также можно задать для файлов с действием сборки Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource или None.</span><span class="sxs-lookup"><span data-stu-id="c879d-276">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="c879d-277">Чтобы объект pack добавил имя файла в путь к пакету при использовании стандартных масок, путь к пакету должен заканчиваться символом разделителя папок, в противном случае этот путь считается полным путем, включающим имя файла.</span><span class="sxs-lookup"><span data-stu-id="c879d-277">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="c879d-278">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="c879d-278">IncludeSymbols</span></span>

<span data-ttu-id="c879d-279">При использовании `MSBuild -t:pack -p:IncludeSymbols=true` соответствующие файлы `.pdb` копируются вместе с другими выходными файлами (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="c879d-279">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="c879d-280">Обратите внимание, что при задании `IncludeSymbols=true` создается обычный пакет *и* пакет символов.</span><span class="sxs-lookup"><span data-stu-id="c879d-280">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="c879d-281">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="c879d-281">IncludeSource</span></span>

<span data-ttu-id="c879d-282">Аналогично `IncludeSymbols`, только копирует исходные файлы вместе с файлами `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="c879d-282">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="c879d-283">Все файлы типа `Compile` копируются в `src\<ProjectName>\` с сохранением относительной структуры папок в итоговом пакете.</span><span class="sxs-lookup"><span data-stu-id="c879d-283">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="c879d-284">То же самое происходит с исходными файлами любого `ProjectReference`, у которого `TreatAsPackageReference` имеет значение `false`.</span><span class="sxs-lookup"><span data-stu-id="c879d-284">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="c879d-285">Если файл типа Compile находится вне папки проекта, он просто добавляется в `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="c879d-285">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="c879d-286">Упаковка выражения лицензии или файла лицензии</span><span class="sxs-lookup"><span data-stu-id="c879d-286">Packing a license expression or a license file</span></span>

<span data-ttu-id="c879d-287">При использовании выражения лицензии следует использовать свойство Паккажелиценсикспрессион.</span><span class="sxs-lookup"><span data-stu-id="c879d-287">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="c879d-288">[Пример выражения лицензии](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="c879d-288">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="c879d-289">Дополнительные [сведения о лицензионных выражениях и лицензиях, принимаемых NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="c879d-289">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="c879d-290">При упаковке файла лицензии необходимо использовать свойство Паккажелиценсефиле, чтобы указать путь к пакету относительно корня пакета.</span><span class="sxs-lookup"><span data-stu-id="c879d-290">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="c879d-291">Кроме того, необходимо убедиться, что файл включен в пакет.</span><span class="sxs-lookup"><span data-stu-id="c879d-291">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="c879d-292">Например:</span><span class="sxs-lookup"><span data-stu-id="c879d-292">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="c879d-293">[Пример файла лицензии](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="c879d-293">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="c879d-294">IsTool</span><span class="sxs-lookup"><span data-stu-id="c879d-294">IsTool</span></span>

<span data-ttu-id="c879d-295">При использовании `MSBuild -t:pack -p:IsTool=true` все выходные файлы, как указано в сценарии [Выходные сборки](#output-assemblies), копируются в папку `tools` вместо папки `lib`.</span><span class="sxs-lookup"><span data-stu-id="c879d-295">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="c879d-296">Обратите внимание, что это свойство отличается от `DotNetCliTool`, которое указывается путем задания `PackageType` в файле `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="c879d-296">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="c879d-297">Упаковка с помощью NUSPEC</span><span class="sxs-lookup"><span data-stu-id="c879d-297">Packing using a .nuspec</span></span>

<span data-ttu-id="c879d-298">Хотя рекомендуется включить в файл проекта [все свойства](../reference/msbuild-targets.md#pack-target) , которые обычно находятся в `.nuspec` файле, можно использовать `.nuspec` файл для упаковки проекта.</span><span class="sxs-lookup"><span data-stu-id="c879d-298">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="c879d-299">Для проекта в стиле, отличном от SDK, `PackageReference`который использует, необходимо `NuGet.Build.Tasks.Pack.targets` импортировать, чтобы можно было выполнить задачу «Pack».</span><span class="sxs-lookup"><span data-stu-id="c879d-299">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="c879d-300">Вам по-прежнему потребуется восстановить проект, чтобы можно было упаковать файл nuspec.</span><span class="sxs-lookup"><span data-stu-id="c879d-300">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="c879d-301">(Проект в стиле SDK включает целевые объекты Pack по умолчанию.)</span><span class="sxs-lookup"><span data-stu-id="c879d-301">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="c879d-302">Целевая платформа файла проекта несущественна и не используется при упаковке nuspec.</span><span class="sxs-lookup"><span data-stu-id="c879d-302">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="c879d-303">Следующие три свойства MSBuild связаны с упаковкой с помощью `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="c879d-303">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="c879d-304">`NuspecFile`: относительный или абсолютный путь к файлу `.nuspec`, используемому для упаковки.</span><span class="sxs-lookup"><span data-stu-id="c879d-304">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="c879d-305">`NuspecProperties`: список разделенных точками с запятой пар "ключ-значение".</span><span class="sxs-lookup"><span data-stu-id="c879d-305">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="c879d-306">Из-за особенностей работы анализа в командной строке MSBuild несколько свойств нужно указать следующим образом: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="c879d-306">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="c879d-307">`NuspecBasePath`: Базовый путь `.nuspec` к файлу.</span><span class="sxs-lookup"><span data-stu-id="c879d-307">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="c879d-308">Если вы используете `dotnet.exe` для упаковки проекта, воспользуйтесь командой, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="c879d-308">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="c879d-309">Если вы используете MSBuild для упаковки проекта, воспользуйтесь командой, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="c879d-309">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="c879d-310">Обратите внимание, что упаковка a nuspec с помощью DotNet. exe или MSBuild также ведет к построению проекта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c879d-310">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="c879d-311">Это можно избежать, передав ```--no-build``` свойство в файл DotNet. exe, эквивалентное параметру ```<NoBuild>true</NoBuild> ``` в файле проекта, а также задав параметр ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="c879d-311">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="c879d-312">Пример файла *. csproj* для упаковки файла nuspec:</span><span class="sxs-lookup"><span data-stu-id="c879d-312">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="c879d-313">Дополнительные точки расширения для создания настраиваемого пакета</span><span class="sxs-lookup"><span data-stu-id="c879d-313">Advanced extension points to create customized package</span></span>

<span data-ttu-id="c879d-314">`pack` Целевой объект предоставляет две точки расширения, которые выполняются во внутренней и целевой сборке конкретной платформы.</span><span class="sxs-lookup"><span data-stu-id="c879d-314">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="c879d-315">Поддержка точек расширения включает в пакет содержимое и сборки, относящиеся к целевой платформе.</span><span class="sxs-lookup"><span data-stu-id="c879d-315">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="c879d-316">`TargetsForTfmSpecificBuildOutput`мишень Используется для файлов в `lib` папке или в папке, заданной с помощью. `BuildOutputTargetFolder`</span><span class="sxs-lookup"><span data-stu-id="c879d-316">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="c879d-317">`TargetsForTfmSpecificContentInPackage`мишень Используется для файлов за пределами `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="c879d-317">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="c879d-318">таржетсфортфмспеЦификбуилдаутпут</span><span class="sxs-lookup"><span data-stu-id="c879d-318">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="c879d-319">Напишите настраиваемый целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificBuildOutput)` свойства.</span><span class="sxs-lookup"><span data-stu-id="c879d-319">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="c879d-320">Для файлов, которые необходимо `BuildOutputTargetFolder` переключать в (LIB по умолчанию), целевой объект должен записать эти файлы в ItemGroup `BuildOutputInPackage` и задать следующие два значения метаданных:</span><span class="sxs-lookup"><span data-stu-id="c879d-320">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="c879d-321">`FinalOutputPath`: Абсолютный путь к файлу; Если этот параметр не указан, для вычисления исходного пути используется удостоверение.</span><span class="sxs-lookup"><span data-stu-id="c879d-321">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="c879d-322">`TargetPath`:  Используемых Задается, когда файл необходимо переключиться во `lib\<TargetFramework>` вложенную папку в, например вспомогательные сборки, которые находятся в соответствующих папках языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="c879d-322">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="c879d-323">По умолчанию используется имя файла.</span><span class="sxs-lookup"><span data-stu-id="c879d-323">Defaults to the name of the file.</span></span>

<span data-ttu-id="c879d-324">Пример</span><span class="sxs-lookup"><span data-stu-id="c879d-324">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="c879d-325">таржетсфортфмспеЦификконтентинпаккаже</span><span class="sxs-lookup"><span data-stu-id="c879d-325">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="c879d-326">Напишите настраиваемый целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificContentInPackage)` свойства.</span><span class="sxs-lookup"><span data-stu-id="c879d-326">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="c879d-327">Для всех файлов, включаемых в пакет, целевой объект должен записать эти файлы в ItemGroup `TfmSpecificPackageFile` и задать следующие необязательные метаданные:</span><span class="sxs-lookup"><span data-stu-id="c879d-327">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="c879d-328">`PackagePath`: Путь, по которому файл должен быть выведен в пакете.</span><span class="sxs-lookup"><span data-stu-id="c879d-328">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="c879d-329">NuGet выдает предупреждение, если в один и тот же путь к пакету добавляется несколько файлов.</span><span class="sxs-lookup"><span data-stu-id="c879d-329">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="c879d-330">`BuildAction`: Действие сборки, присваиваемое файлу, требуется только в том случае, если путь к пакету `contentFiles` находится в папке.</span><span class="sxs-lookup"><span data-stu-id="c879d-330">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="c879d-331">По умолчанию используется значение "нет".</span><span class="sxs-lookup"><span data-stu-id="c879d-331">Defaults to "None".</span></span>

<span data-ttu-id="c879d-332">Пример:</span><span class="sxs-lookup"><span data-stu-id="c879d-332">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="c879d-333">Целевой объект restore</span><span class="sxs-lookup"><span data-stu-id="c879d-333">restore target</span></span>

<span data-ttu-id="c879d-334">`MSBuild -t:restore` (который `nuget restore` и `dotnet restore` используют с проектами .NET Core) восстанавливает пакеты, на которые ссылается файл проекта:</span><span class="sxs-lookup"><span data-stu-id="c879d-334">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="c879d-335">Чтение перекрестных ссылок между проектами.</span><span class="sxs-lookup"><span data-stu-id="c879d-335">Read all project to project references</span></span>
1. <span data-ttu-id="c879d-336">Чтение свойств проекта, чтобы найти промежуточную папку и целевые платформы.</span><span class="sxs-lookup"><span data-stu-id="c879d-336">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="c879d-337">Передача данных MSBuild в NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="c879d-337">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="c879d-338">Запуск восстановления.</span><span class="sxs-lookup"><span data-stu-id="c879d-338">Run restore</span></span>
1. <span data-ttu-id="c879d-339">Скачивание пакетов.</span><span class="sxs-lookup"><span data-stu-id="c879d-339">Download packages</span></span>
1. <span data-ttu-id="c879d-340">Запись файла ресурсов, целевых объектов и свойств.</span><span class="sxs-lookup"><span data-stu-id="c879d-340">Write assets file, targets, and props</span></span>

<span data-ttu-id="c879d-341">Целевой объект работает только для проектов, использующих формат PackageReference. `restore`</span><span class="sxs-lookup"><span data-stu-id="c879d-341">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="c879d-342">Он **не** работает для проектов, использующих этот `packages.config` формат; вместо этого используйте [Восстановление NuGet](../reference/cli-reference/cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="c879d-342">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="c879d-343">Свойства восстановления</span><span class="sxs-lookup"><span data-stu-id="c879d-343">Restore properties</span></span>

<span data-ttu-id="c879d-344">Дополнительные параметры восстановления могут поступать из свойств MSBuild в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="c879d-344">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="c879d-345">Значения также можно задать из командной строки с помощью параметра `-p:` (см. примеры ниже).</span><span class="sxs-lookup"><span data-stu-id="c879d-345">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="c879d-346">Свойство.</span><span class="sxs-lookup"><span data-stu-id="c879d-346">Property</span></span> | <span data-ttu-id="c879d-347">Описание</span><span class="sxs-lookup"><span data-stu-id="c879d-347">Description</span></span> |
|--------|--------|
| <span data-ttu-id="c879d-348">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="c879d-348">RestoreSources</span></span> | <span data-ttu-id="c879d-349">Разделенный точками с запятой список источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="c879d-349">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="c879d-350">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="c879d-350">RestorePackagesPath</span></span> | <span data-ttu-id="c879d-351">Путь к папке пакетов пользователя.</span><span class="sxs-lookup"><span data-stu-id="c879d-351">User packages folder path.</span></span> |
| <span data-ttu-id="c879d-352">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="c879d-352">RestoreDisableParallel</span></span> | <span data-ttu-id="c879d-353">Ограничение скачиваний до одного за раз.</span><span class="sxs-lookup"><span data-stu-id="c879d-353">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="c879d-354">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="c879d-354">RestoreConfigFile</span></span> | <span data-ttu-id="c879d-355">Путь к применяемому файлу `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="c879d-355">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="c879d-356">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="c879d-356">RestoreNoCache</span></span> | <span data-ttu-id="c879d-357">Значение true позволяет избежать использования кэшированных пакетов.</span><span class="sxs-lookup"><span data-stu-id="c879d-357">If true, avoids using cached packages.</span></span> <span data-ttu-id="c879d-358">См. раздел [Управление глобальными пакетами и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="c879d-358">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="c879d-359">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="c879d-359">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="c879d-360">Если значение равно true, нерабочие или отсутствующие источники пакетов игнорируются.</span><span class="sxs-lookup"><span data-stu-id="c879d-360">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="c879d-361">ресторефаллбаккфолдерс</span><span class="sxs-lookup"><span data-stu-id="c879d-361">RestoreFallbackFolders</span></span> | <span data-ttu-id="c879d-362">Резервные папки используются так же, как и папка User Packages.</span><span class="sxs-lookup"><span data-stu-id="c879d-362">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="c879d-363">рестореаддитионалпрожектсаурцес</span><span class="sxs-lookup"><span data-stu-id="c879d-363">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="c879d-364">Дополнительные источники, используемые во время восстановления.</span><span class="sxs-lookup"><span data-stu-id="c879d-364">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="c879d-365">рестореаддитионалпрожектфаллбаккфолдерс</span><span class="sxs-lookup"><span data-stu-id="c879d-365">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="c879d-366">Дополнительные резервные папки для использования во время восстановления.</span><span class="sxs-lookup"><span data-stu-id="c879d-366">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="c879d-367">рестореаддитионалпрожектфаллбаккфолдерсексклудес</span><span class="sxs-lookup"><span data-stu-id="c879d-367">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="c879d-368">Исключает резервные папки, указанные в`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="c879d-368">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="c879d-369">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="c879d-369">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="c879d-370">Путь к `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="c879d-370">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="c879d-371">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="c879d-371">RestoreGraphProjectInput</span></span> | <span data-ttu-id="c879d-372">Разделенный точками с запятой список проектов для восстановления, который должен содержать абсолютные пути.</span><span class="sxs-lookup"><span data-stu-id="c879d-372">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="c879d-373">рестореусескипнонексистенттаржетс</span><span class="sxs-lookup"><span data-stu-id="c879d-373">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="c879d-374">При сборе проектов с помощью MSBuild определяет, будут ли они собраны с `SkipNonexistentTargets` помощью оптимизации.</span><span class="sxs-lookup"><span data-stu-id="c879d-374">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="c879d-375">Если значение не задано, по `true`умолчанию используется значение.</span><span class="sxs-lookup"><span data-stu-id="c879d-375">When not set, defaults to `true`.</span></span> <span data-ttu-id="c879d-376">Следствием является быстрое поведение при сбое, если целевые объекты проекта не могут быть импортированы.</span><span class="sxs-lookup"><span data-stu-id="c879d-376">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="c879d-377">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="c879d-377">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="c879d-378">Папка Output, по умолчанию `BaseIntermediateOutputPath` — `obj` и папка.</span><span class="sxs-lookup"><span data-stu-id="c879d-378">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="c879d-379">Примеры</span><span class="sxs-lookup"><span data-stu-id="c879d-379">Examples</span></span>

<span data-ttu-id="c879d-380">Командная строка:</span><span class="sxs-lookup"><span data-stu-id="c879d-380">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="c879d-381">Файл проекта:</span><span class="sxs-lookup"><span data-stu-id="c879d-381">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="c879d-382">Выходные данные восстановления</span><span class="sxs-lookup"><span data-stu-id="c879d-382">Restore outputs</span></span>

<span data-ttu-id="c879d-383">Операция восстановления создает в папке сборки `obj` следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="c879d-383">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="c879d-384">Файл</span><span class="sxs-lookup"><span data-stu-id="c879d-384">File</span></span> | <span data-ttu-id="c879d-385">Описание</span><span class="sxs-lookup"><span data-stu-id="c879d-385">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="c879d-386">Содержит диаграмму зависимостей всех ссылок на пакеты.</span><span class="sxs-lookup"><span data-stu-id="c879d-386">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="c879d-387">Ссылки на свойства MSBuild, содержащиеся в пакетах.</span><span class="sxs-lookup"><span data-stu-id="c879d-387">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="c879d-388">Ссылки на целевые объекты MSBuild, содержащиеся в пакетах.</span><span class="sxs-lookup"><span data-stu-id="c879d-388">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="c879d-389">Восстановление и сборка с помощью одной команды MSBuild</span><span class="sxs-lookup"><span data-stu-id="c879d-389">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="c879d-390">Из-за того, что NuGet может восстанавливать пакеты, которые выводят цели и свойства MSBuild, оценки восстановления и сборки выполняются с разными глобальными свойствами.</span><span class="sxs-lookup"><span data-stu-id="c879d-390">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="c879d-391">Это означает, что следующие действия будут иметь непредсказуемое и неправильное поведение.</span><span class="sxs-lookup"><span data-stu-id="c879d-391">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="c879d-392">Вместо этого рекомендуемый подход:</span><span class="sxs-lookup"><span data-stu-id="c879d-392">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="c879d-393">Одна и та же логика применяется к другим `build`целевым объектам, аналогичным.</span><span class="sxs-lookup"><span data-stu-id="c879d-393">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="c879d-394">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="c879d-394">PackageTargetFallback</span></span>

<span data-ttu-id="c879d-395">Элемент `PackageTargetFallback` позволяет указать набор совместимых целевых объектов, которые следует использовать при восстановлении пакетов.</span><span class="sxs-lookup"><span data-stu-id="c879d-395">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="c879d-396">Он разрешает пакетам, использующим dotnet [TxM](../reference/target-frameworks.md), взаимодействовать с совместимыми пакетами, которые не объявляют dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="c879d-396">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="c879d-397">Таким образом, если в проекте используется dotnet TxM, все пакеты, от которых вы зависите, должны также содержать dotnet TxM. В противном случае нужно добавить `<PackageTargetFallback>` в проект, чтобы обеспечить совместимость с платформами, отличными от dotnet.</span><span class="sxs-lookup"><span data-stu-id="c879d-397">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="c879d-398">Например, если в проекте используется `netstandard1.6` TxM, а зависимый пакет содержит только `lib/net45/a.dll` и `lib/portable-net45+win81/a.dll`, то сборка проекта завершится со сбоем.</span><span class="sxs-lookup"><span data-stu-id="c879d-398">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="c879d-399">Если вы хотите использовать вторую библиотеку DLL, можете добавить `PackageTargetFallback` следующим образом, чтобы обозначить совместимость библиотеки DLL `portable-net45+win81`:</span><span class="sxs-lookup"><span data-stu-id="c879d-399">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="c879d-400">Чтобы объявить откат для всех целевых объектов в проекте, оставьте атрибут `Condition`.</span><span class="sxs-lookup"><span data-stu-id="c879d-400">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="c879d-401">Кроме того, можно расширить существующий `PackageTargetFallback`, включив `$(PackageTargetFallback)`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="c879d-401">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="c879d-402">Замена одной библиотеки из графа восстановления</span><span class="sxs-lookup"><span data-stu-id="c879d-402">Replacing one library from a restore graph</span></span>

<span data-ttu-id="c879d-403">Если операция восстановления предоставляет неправильную сборку, вы можете исключить значение по умолчанию для этого пакета, заменив его своим значением.</span><span class="sxs-lookup"><span data-stu-id="c879d-403">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="c879d-404">Первый с `PackageReference` верхнего уровня, исключите все ресурсы:</span><span class="sxs-lookup"><span data-stu-id="c879d-404">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="c879d-405">После этого добавьте собственную ссылку на соответствующую локальную копию библиотеки DLL:</span><span class="sxs-lookup"><span data-stu-id="c879d-405">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
