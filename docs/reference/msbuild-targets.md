---
title: Объекты pack и restore NuGet в качестве целевых объектов MSBuild
description: Объекты pack и restore NuGet могут выступать непосредственно в качестве целевых объектов MSBuild в NuGet 4.0+.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 7de3f0f1133a89848e9268d489751293fb3cbf25
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235702"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="52db6-103">Объекты pack и restore NuGet в качестве целевых объектов MSBuild</span><span class="sxs-lookup"><span data-stu-id="52db6-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="52db6-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="52db6-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="52db6-105">В формате [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + может хранить все метаданные манифеста непосредственно в файле проекта вместо использования отдельного `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="52db6-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="52db6-106">При использовании MSBuild 15.1+ NuGet также является привилегированным компонентом MSBuild с целевыми объектами `pack` и `restore`, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="52db6-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="52db6-107">Эти целевые объекты позволяют работать с NuGet, как с любой другой задачей или другим целевым объектом MSBuild.</span><span class="sxs-lookup"><span data-stu-id="52db6-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="52db6-108">Инструкции по созданию пакета NuGet с помощью MSBuild см. в статье [Создание пакета NuGet с помощью MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="52db6-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="52db6-109">(Для NuGet 3.x и более ранних версий можно использовать команды [pack](../reference/cli-reference/cli-ref-pack.md) и [restore](../reference/cli-reference/cli-ref-restore.md) в NuGet CLI.)</span><span class="sxs-lookup"><span data-stu-id="52db6-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="52db6-110">Порядок сборки целевого объекта</span><span class="sxs-lookup"><span data-stu-id="52db6-110">Target build order</span></span>

<span data-ttu-id="52db6-111">Так как `pack` и `restore` являются целевыми объектами MSBuild, вы можете обращаться к ним для улучшения рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="52db6-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="52db6-112">Например, предположим, что вам нужно скопировать пакет в общую сетевую папку после его упаковки.</span><span class="sxs-lookup"><span data-stu-id="52db6-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="52db6-113">Это можно сделать, добавив следующий код в файл проекта:</span><span class="sxs-lookup"><span data-stu-id="52db6-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="52db6-114">Аналогичным образом, вы можете создать задачу MSBuild и собственный целевой объект и использовать свойства NuGet в этой задаче MSBuild.</span><span class="sxs-lookup"><span data-stu-id="52db6-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="52db6-115">`$(OutputPath)` является относительным и предполагает, что команда выполняется из корневого каталога проекта.</span><span class="sxs-lookup"><span data-stu-id="52db6-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="52db6-116">Целевой объект pack</span><span class="sxs-lookup"><span data-stu-id="52db6-116">pack target</span></span>

<span data-ttu-id="52db6-117">Для .NET Standard проектов, использующих формат PackageReference, команда `msbuild -t:pack` рисует входные данные из файла проекта для использования при создании пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="52db6-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="52db6-118">В следующей таблице описываются свойства MSBuild, которые можно добавить в файл проекта в первом узле `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="52db6-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="52db6-119">Эти изменения легко внести в Visual Studio 2017 и более поздней версии, щелкнув проект правой кнопкой мыши и выбрав пункт **Изменить {project_name}**.</span><span class="sxs-lookup"><span data-stu-id="52db6-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="52db6-120">Для удобства таблица упорядочивается по эквивалентному свойству в [ `.nuspec` файле](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="52db6-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="52db6-121">Обратите внимание, что свойства `Owners` и `Summary` из `.nuspec` не поддерживаются в MSBuild.</span><span class="sxs-lookup"><span data-stu-id="52db6-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="52db6-122">Значение атрибута или NuSpec</span><span class="sxs-lookup"><span data-stu-id="52db6-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="52db6-123">Свойство MSBuild</span><span class="sxs-lookup"><span data-stu-id="52db6-123">MSBuild Property</span></span> | <span data-ttu-id="52db6-124">По умолчанию</span><span class="sxs-lookup"><span data-stu-id="52db6-124">Default</span></span> | <span data-ttu-id="52db6-125">Примечания</span><span class="sxs-lookup"><span data-stu-id="52db6-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="52db6-126">Id</span><span class="sxs-lookup"><span data-stu-id="52db6-126">Id</span></span> | <span data-ttu-id="52db6-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="52db6-127">PackageId</span></span> | <span data-ttu-id="52db6-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="52db6-128">AssemblyName</span></span> | <span data-ttu-id="52db6-129">$(AssemblyName) из MSBuild</span><span class="sxs-lookup"><span data-stu-id="52db6-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="52db6-130">Version</span><span class="sxs-lookup"><span data-stu-id="52db6-130">Version</span></span> | <span data-ttu-id="52db6-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="52db6-131">PackageVersion</span></span> | <span data-ttu-id="52db6-132">Version</span><span class="sxs-lookup"><span data-stu-id="52db6-132">Version</span></span> | <span data-ttu-id="52db6-133">Это значение совместимо с SemVer, например "1.0.0", "1.0.0-beta" или "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="52db6-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="52db6-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="52db6-134">VersionPrefix</span></span> | <span data-ttu-id="52db6-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="52db6-135">PackageVersionPrefix</span></span> | <span data-ttu-id="52db6-136">пустых</span><span class="sxs-lookup"><span data-stu-id="52db6-136">empty</span></span> | <span data-ttu-id="52db6-137">Задав PackageVersion, вы перезапишите PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="52db6-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="52db6-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="52db6-138">VersionSuffix</span></span> | <span data-ttu-id="52db6-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="52db6-139">PackageVersionSuffix</span></span> | <span data-ttu-id="52db6-140">пустых</span><span class="sxs-lookup"><span data-stu-id="52db6-140">empty</span></span> | <span data-ttu-id="52db6-141">$(VersionSuffix) из MSBuild.</span><span class="sxs-lookup"><span data-stu-id="52db6-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="52db6-142">Задав PackageVersion, вы перезапишите PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="52db6-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="52db6-143">Авторы</span><span class="sxs-lookup"><span data-stu-id="52db6-143">Authors</span></span> | <span data-ttu-id="52db6-144">Авторы</span><span class="sxs-lookup"><span data-stu-id="52db6-144">Authors</span></span> | <span data-ttu-id="52db6-145">Имя текущего пользователя</span><span class="sxs-lookup"><span data-stu-id="52db6-145">Username of the current user</span></span> | |
| <span data-ttu-id="52db6-146">Владельцы</span><span class="sxs-lookup"><span data-stu-id="52db6-146">Owners</span></span> | <span data-ttu-id="52db6-147">Недоступно</span><span class="sxs-lookup"><span data-stu-id="52db6-147">N/A</span></span> | <span data-ttu-id="52db6-148">Не существует в NuSpec</span><span class="sxs-lookup"><span data-stu-id="52db6-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="52db6-149">Заголовок</span><span class="sxs-lookup"><span data-stu-id="52db6-149">Title</span></span> | <span data-ttu-id="52db6-150">Заголовок</span><span class="sxs-lookup"><span data-stu-id="52db6-150">Title</span></span> | <span data-ttu-id="52db6-151">Идентификатор пакета</span><span class="sxs-lookup"><span data-stu-id="52db6-151">The PackageId</span></span>| |
| <span data-ttu-id="52db6-152">Description</span><span class="sxs-lookup"><span data-stu-id="52db6-152">Description</span></span> | <span data-ttu-id="52db6-153">Описание</span><span class="sxs-lookup"><span data-stu-id="52db6-153">Description</span></span> | <span data-ttu-id="52db6-154">"Описание пакета"</span><span class="sxs-lookup"><span data-stu-id="52db6-154">"Package Description"</span></span> | |
| <span data-ttu-id="52db6-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="52db6-155">Copyright</span></span> | <span data-ttu-id="52db6-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="52db6-156">Copyright</span></span> | <span data-ttu-id="52db6-157">пустых</span><span class="sxs-lookup"><span data-stu-id="52db6-157">empty</span></span> | |
| <span data-ttu-id="52db6-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="52db6-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="52db6-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="52db6-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="52db6-160">false</span><span class="sxs-lookup"><span data-stu-id="52db6-160">false</span></span> | |
| <span data-ttu-id="52db6-161">license</span><span class="sxs-lookup"><span data-stu-id="52db6-161">license</span></span> | <span data-ttu-id="52db6-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="52db6-162">PackageLicenseExpression</span></span> | <span data-ttu-id="52db6-163">пустых</span><span class="sxs-lookup"><span data-stu-id="52db6-163">empty</span></span> | <span data-ttu-id="52db6-164">Соответствует `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="52db6-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="52db6-165">license</span><span class="sxs-lookup"><span data-stu-id="52db6-165">license</span></span> | <span data-ttu-id="52db6-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="52db6-166">PackageLicenseFile</span></span> | <span data-ttu-id="52db6-167">пустых</span><span class="sxs-lookup"><span data-stu-id="52db6-167">empty</span></span> | <span data-ttu-id="52db6-168">Соответствует `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="52db6-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="52db6-169">Необходимо явно упаковать файл лицензии, на который указывает ссылка.</span><span class="sxs-lookup"><span data-stu-id="52db6-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="52db6-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="52db6-170">LicenseUrl</span></span> | <span data-ttu-id="52db6-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="52db6-171">PackageLicenseUrl</span></span> | <span data-ttu-id="52db6-172">пустых</span><span class="sxs-lookup"><span data-stu-id="52db6-172">empty</span></span> | <span data-ttu-id="52db6-173">`PackageLicenseUrl` является устаревшим, используйте свойство Паккажелиценсикспрессион или Паккажелиценсефиле.</span><span class="sxs-lookup"><span data-stu-id="52db6-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="52db6-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="52db6-174">ProjectUrl</span></span> | <span data-ttu-id="52db6-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="52db6-175">PackageProjectUrl</span></span> | <span data-ttu-id="52db6-176">пустых</span><span class="sxs-lookup"><span data-stu-id="52db6-176">empty</span></span> | |
| <span data-ttu-id="52db6-177">Значок</span><span class="sxs-lookup"><span data-stu-id="52db6-177">Icon</span></span> | <span data-ttu-id="52db6-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="52db6-178">PackageIcon</span></span> | <span data-ttu-id="52db6-179">пустых</span><span class="sxs-lookup"><span data-stu-id="52db6-179">empty</span></span> | <span data-ttu-id="52db6-180">Необходимо явно упаковать файл изображения значка, на который указывает ссылка.</span><span class="sxs-lookup"><span data-stu-id="52db6-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="52db6-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="52db6-181">IconUrl</span></span> | <span data-ttu-id="52db6-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="52db6-182">PackageIconUrl</span></span> | <span data-ttu-id="52db6-183">пустых</span><span class="sxs-lookup"><span data-stu-id="52db6-183">empty</span></span> | <span data-ttu-id="52db6-184">Для лучшей работы с предыдущими версиями `PackageIconUrl` следует указать в дополнение к `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="52db6-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="52db6-185">Более длительное выражение `PackageIconUrl` будет считаться устаревшим.</span><span class="sxs-lookup"><span data-stu-id="52db6-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="52db6-186">Теги</span><span class="sxs-lookup"><span data-stu-id="52db6-186">Tags</span></span> | <span data-ttu-id="52db6-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="52db6-187">PackageTags</span></span> | <span data-ttu-id="52db6-188">пустых</span><span class="sxs-lookup"><span data-stu-id="52db6-188">empty</span></span> | <span data-ttu-id="52db6-189">Теги разделяются точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="52db6-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="52db6-190">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="52db6-190">ReleaseNotes</span></span> | <span data-ttu-id="52db6-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="52db6-191">PackageReleaseNotes</span></span> | <span data-ttu-id="52db6-192">пустых</span><span class="sxs-lookup"><span data-stu-id="52db6-192">empty</span></span> | |
| <span data-ttu-id="52db6-193">Репозиторий/URL-адрес</span><span class="sxs-lookup"><span data-stu-id="52db6-193">Repository/Url</span></span> | <span data-ttu-id="52db6-194">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="52db6-194">RepositoryUrl</span></span> | <span data-ttu-id="52db6-195">пустых</span><span class="sxs-lookup"><span data-stu-id="52db6-195">empty</span></span> | <span data-ttu-id="52db6-196">URL-адрес репозитория, используемый для клонирования или извлечения исходного кода.</span><span class="sxs-lookup"><span data-stu-id="52db6-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="52db6-197">Например *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="52db6-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="52db6-198">Репозиторий или тип</span><span class="sxs-lookup"><span data-stu-id="52db6-198">Repository/Type</span></span> | <span data-ttu-id="52db6-199">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="52db6-199">RepositoryType</span></span> | <span data-ttu-id="52db6-200">пустых</span><span class="sxs-lookup"><span data-stu-id="52db6-200">empty</span></span> | <span data-ttu-id="52db6-201">Тип репозитория.</span><span class="sxs-lookup"><span data-stu-id="52db6-201">Repository type.</span></span> <span data-ttu-id="52db6-202">Примеры: *Git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="52db6-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="52db6-203">Репозиторий или ветвь</span><span class="sxs-lookup"><span data-stu-id="52db6-203">Repository/Branch</span></span> | <span data-ttu-id="52db6-204">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="52db6-204">RepositoryBranch</span></span> | <span data-ttu-id="52db6-205">пустых</span><span class="sxs-lookup"><span data-stu-id="52db6-205">empty</span></span> | <span data-ttu-id="52db6-206">Дополнительные сведения о ветви репозитория.</span><span class="sxs-lookup"><span data-stu-id="52db6-206">Optional repository branch information.</span></span> <span data-ttu-id="52db6-207">Для включения этого свойства также необходимо указать *репоситорюрл* .</span><span class="sxs-lookup"><span data-stu-id="52db6-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="52db6-208">Пример: *master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="52db6-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="52db6-209">Репозиторий/фиксация</span><span class="sxs-lookup"><span data-stu-id="52db6-209">Repository/Commit</span></span> | <span data-ttu-id="52db6-210">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="52db6-210">RepositoryCommit</span></span> | <span data-ttu-id="52db6-211">пустых</span><span class="sxs-lookup"><span data-stu-id="52db6-211">empty</span></span> | <span data-ttu-id="52db6-212">Необязательная фиксация или набор изменений репозитория для указания источника, на основе которого был создан пакет.</span><span class="sxs-lookup"><span data-stu-id="52db6-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="52db6-213">Для включения этого свойства также необходимо указать *репоситорюрл* .</span><span class="sxs-lookup"><span data-stu-id="52db6-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="52db6-214">Пример: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="52db6-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="52db6-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="52db6-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="52db6-216">Сводка</span><span class="sxs-lookup"><span data-stu-id="52db6-216">Summary</span></span> | <span data-ttu-id="52db6-217">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="52db6-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="52db6-218">Входные данные целевого объекта pack</span><span class="sxs-lookup"><span data-stu-id="52db6-218">pack target inputs</span></span>

- <span data-ttu-id="52db6-219">IsPackable</span><span class="sxs-lookup"><span data-stu-id="52db6-219">IsPackable</span></span>
- <span data-ttu-id="52db6-220">суппрессдепенденЦиесвхенпаккинг</span><span class="sxs-lookup"><span data-stu-id="52db6-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="52db6-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="52db6-221">PackageVersion</span></span>
- <span data-ttu-id="52db6-222">PackageId</span><span class="sxs-lookup"><span data-stu-id="52db6-222">PackageId</span></span>
- <span data-ttu-id="52db6-223">Авторы</span><span class="sxs-lookup"><span data-stu-id="52db6-223">Authors</span></span>
- <span data-ttu-id="52db6-224">Описание</span><span class="sxs-lookup"><span data-stu-id="52db6-224">Description</span></span>
- <span data-ttu-id="52db6-225">Copyright</span><span class="sxs-lookup"><span data-stu-id="52db6-225">Copyright</span></span>
- <span data-ttu-id="52db6-226">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="52db6-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="52db6-227">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="52db6-227">DevelopmentDependency</span></span>
- <span data-ttu-id="52db6-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="52db6-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="52db6-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="52db6-229">PackageLicenseFile</span></span>
- <span data-ttu-id="52db6-230">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="52db6-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="52db6-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="52db6-231">PackageProjectUrl</span></span>
- <span data-ttu-id="52db6-232">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="52db6-232">PackageIconUrl</span></span>
- <span data-ttu-id="52db6-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="52db6-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="52db6-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="52db6-234">PackageTags</span></span>
- <span data-ttu-id="52db6-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="52db6-235">PackageOutputPath</span></span>
- <span data-ttu-id="52db6-236">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="52db6-236">IncludeSymbols</span></span>
- <span data-ttu-id="52db6-237">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="52db6-237">IncludeSource</span></span>
- <span data-ttu-id="52db6-238">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="52db6-238">PackageTypes</span></span>
- <span data-ttu-id="52db6-239">IsTool</span><span class="sxs-lookup"><span data-stu-id="52db6-239">IsTool</span></span>
- <span data-ttu-id="52db6-240">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="52db6-240">RepositoryUrl</span></span>
- <span data-ttu-id="52db6-241">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="52db6-241">RepositoryType</span></span>
- <span data-ttu-id="52db6-242">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="52db6-242">RepositoryBranch</span></span>
- <span data-ttu-id="52db6-243">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="52db6-243">RepositoryCommit</span></span>
- <span data-ttu-id="52db6-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="52db6-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="52db6-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="52db6-245">MinClientVersion</span></span>
- <span data-ttu-id="52db6-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="52db6-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="52db6-247">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="52db6-247">IncludeContentInPack</span></span>
- <span data-ttu-id="52db6-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="52db6-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="52db6-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="52db6-249">ContentTargetFolders</span></span>
- <span data-ttu-id="52db6-250">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="52db6-250">NuspecFile</span></span>
- <span data-ttu-id="52db6-251">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="52db6-251">NuspecBasePath</span></span>
- <span data-ttu-id="52db6-252">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="52db6-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="52db6-253">Сценарии использования pack</span><span class="sxs-lookup"><span data-stu-id="52db6-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="52db6-254">Подавлять зависимости</span><span class="sxs-lookup"><span data-stu-id="52db6-254">Suppress dependencies</span></span>

<span data-ttu-id="52db6-255">Чтобы исключить зависимости пакета из созданного пакета NuGet, задайте для значение, `SuppressDependenciesWhenPacking` `true` которое позволит пропустить все зависимости из созданного файла nupkg.</span><span class="sxs-lookup"><span data-stu-id="52db6-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="52db6-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="52db6-256">PackageIconUrl</span></span>

<span data-ttu-id="52db6-257">`PackageIconUrl` будет считаться устаревшим в пользу нового [`PackageIcon`](#packageicon) Свойства.</span><span class="sxs-lookup"><span data-stu-id="52db6-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="52db6-258">Начиная с NuGet 5,3 & Visual Studio 2019 версии 16,3, `pack` вызовет предупреждение [NU5048](./errors-and-warnings/nu5048.md) , если только метаданные пакета указывают только `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="52db6-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="52db6-259">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="52db6-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="52db6-260">`PackageIcon` `PackageIconUrl` Для обеспечения обратной совместимости с клиентами и источниками, которые еще не поддерживаются, необходимо указать и, и `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="52db6-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="52db6-261">Visual Studio будет поддерживать `PackageIcon` пакеты, поступающие из источника на основе папок в будущем выпуске.</span><span class="sxs-lookup"><span data-stu-id="52db6-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="52db6-262">Упаковка файла изображения значка</span><span class="sxs-lookup"><span data-stu-id="52db6-262">Packing an icon image file</span></span>

<span data-ttu-id="52db6-263">При упаковке файла изображения значка необходимо использовать `PackageIcon` свойство, чтобы указать путь к пакету относительно корня пакета.</span><span class="sxs-lookup"><span data-stu-id="52db6-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="52db6-264">Кроме того, необходимо убедиться, что файл включен в пакет.</span><span class="sxs-lookup"><span data-stu-id="52db6-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="52db6-265">Размер файла изображения ограничен 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="52db6-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="52db6-266">Поддерживаются следующие форматы файлов: JPEG и PNG.</span><span class="sxs-lookup"><span data-stu-id="52db6-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="52db6-267">Рекомендуется разрешение изображения 128x128.</span><span class="sxs-lookup"><span data-stu-id="52db6-267">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="52db6-268">Например:</span><span class="sxs-lookup"><span data-stu-id="52db6-268">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="52db6-269">[Пример значка пакета](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="52db6-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="52db6-270">Чтобы получить nuspec эквивалент, просмотрите [ссылку на nuspec для значка](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="52db6-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="52db6-271">Выходные сборки</span><span class="sxs-lookup"><span data-stu-id="52db6-271">Output assemblies</span></span>

<span data-ttu-id="52db6-272">`nuget pack` копирует выходные файлы с расширениями `.exe`, `.dll`, `.xml`, `.winmd`, `.json` и `.pri`.</span><span class="sxs-lookup"><span data-stu-id="52db6-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="52db6-273">Копируемые выходные файлы зависят от того, что MSBuild предоставляет из целевого объекта `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="52db6-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="52db6-274">Существует два свойства MSBuild, которые можно использовать в файле проекта или командной строке для управления местом назначения для выходных сборок:</span><span class="sxs-lookup"><span data-stu-id="52db6-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="52db6-275">`IncludeBuildOutput`: логическое значение, определяющее, следует ли включать выходные сборки в пакете.</span><span class="sxs-lookup"><span data-stu-id="52db6-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="52db6-276">`BuildOutputTargetFolder`: указывает папку, куда следует помещать выходные сборки.</span><span class="sxs-lookup"><span data-stu-id="52db6-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="52db6-277">Выходные сборки (и другие выходные файлы) копируются в соответствующие папки платформы.</span><span class="sxs-lookup"><span data-stu-id="52db6-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="52db6-278">Ссылки на пакеты</span><span class="sxs-lookup"><span data-stu-id="52db6-278">Package references</span></span>

<span data-ttu-id="52db6-279">См. раздел [Ссылки на пакеты в файлах проекта](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="52db6-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="52db6-280">Перекрестные ссылки между проектами</span><span class="sxs-lookup"><span data-stu-id="52db6-280">Project to project references</span></span>

<span data-ttu-id="52db6-281">Перекрестные ссылки между проектами по умолчанию считаются ссылками на пакет NuGet, например:</span><span class="sxs-lookup"><span data-stu-id="52db6-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="52db6-282">Вы также можете добавить в ссылку на проект следующие метаданные:</span><span class="sxs-lookup"><span data-stu-id="52db6-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="52db6-283">Включение содержимого в пакет</span><span class="sxs-lookup"><span data-stu-id="52db6-283">Including content in a package</span></span>

<span data-ttu-id="52db6-284">Чтобы включить содержимое, добавьте дополнительные метаданные для существующего элемента `<Content>`.</span><span class="sxs-lookup"><span data-stu-id="52db6-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="52db6-285">По умолчанию все данные типа "Content" включаются в пакет, если только вы не переопределите такое поведение с помощью записей, аналогичных следующим:</span><span class="sxs-lookup"><span data-stu-id="52db6-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="52db6-286">По умолчанию все данные добавляются в корень папки `content` и `contentFiles\any\<target_framework>` в пакете и сохраняют относительную структуру папок, если только не указан путь к пакету:</span><span class="sxs-lookup"><span data-stu-id="52db6-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="52db6-287">Если требуется скопировать все содержимое только в определенные корневые папки (вместо `content` и `contentFiles`), можно использовать свойство MSBuild `ContentTargetFolders`, которое по умолчанию имеет значение "content;contentFiles", но может принимать любые другие имена папок.</span><span class="sxs-lookup"><span data-stu-id="52db6-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="52db6-288">Обратите внимание, если указать "contentFiles" в `ContentTargetFolders`, файлы помещаются в `contentFiles\any\<target_framework>` или `contentFiles\<language>\<target_framework>` в зависимости от `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="52db6-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="52db6-289">`PackagePath` может быть набором целевых путей, разделенных точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="52db6-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="52db6-290">Если указан пустой путь к пакету, файл добавляется в корневой каталог пакета.</span><span class="sxs-lookup"><span data-stu-id="52db6-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="52db6-291">Например, следующий код добавляет `libuv.txt` в `content\myfiles`, `content\samples` и корневой каталог пакета:</span><span class="sxs-lookup"><span data-stu-id="52db6-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="52db6-292">Имеется также свойство MSBuild `$(IncludeContentInPack)`, которое по умолчанию равно `true`.</span><span class="sxs-lookup"><span data-stu-id="52db6-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="52db6-293">Если оно имеет значение `false` для какого-либо проекта, то содержимое этого проекта не включается в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="52db6-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="52db6-294">Другие относящиеся к pack метаданные, которые можно задать для любого из указанных выше элементов, включают ```<PackageCopyToOutput>``` и ```<PackageFlatten>```, задающие значения ```CopyToOutput``` и ```Flatten``` для записи ```contentFiles``` в выходном файле NUSPEC.</span><span class="sxs-lookup"><span data-stu-id="52db6-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="52db6-295">Кроме элементов содержимого, метаданные `<Pack>` и `<PackagePath>` также можно задать для файлов с действием сборки Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource или None.</span><span class="sxs-lookup"><span data-stu-id="52db6-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="52db6-296">Чтобы объект pack добавил имя файла в путь к пакету при использовании стандартных масок, путь к пакету должен заканчиваться символом разделителя папок, в противном случае этот путь считается полным путем, включающим имя файла.</span><span class="sxs-lookup"><span data-stu-id="52db6-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="52db6-297">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="52db6-297">IncludeSymbols</span></span>

<span data-ttu-id="52db6-298">При использовании `MSBuild -t:pack -p:IncludeSymbols=true` соответствующие файлы `.pdb` копируются вместе с другими выходными файлами (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="52db6-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="52db6-299">Обратите внимание, что при задании `IncludeSymbols=true` создается обычный пакет *и* пакет символов.</span><span class="sxs-lookup"><span data-stu-id="52db6-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="52db6-300">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="52db6-300">IncludeSource</span></span>

<span data-ttu-id="52db6-301">Аналогично `IncludeSymbols`, только копирует исходные файлы вместе с файлами `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="52db6-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="52db6-302">Все файлы типа `Compile` копируются в `src\<ProjectName>\` с сохранением относительной структуры папок в итоговом пакете.</span><span class="sxs-lookup"><span data-stu-id="52db6-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="52db6-303">То же самое происходит с исходными файлами любого `ProjectReference`, у которого `TreatAsPackageReference` имеет значение `false`.</span><span class="sxs-lookup"><span data-stu-id="52db6-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="52db6-304">Если файл типа Compile находится вне папки проекта, он просто добавляется в `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="52db6-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="52db6-305">Упаковка выражения лицензии или файла лицензии</span><span class="sxs-lookup"><span data-stu-id="52db6-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="52db6-306">При использовании выражения лицензии следует использовать свойство Паккажелиценсикспрессион.</span><span class="sxs-lookup"><span data-stu-id="52db6-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="52db6-307">[Пример выражения лицензии](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="52db6-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="52db6-308">Дополнительные [сведения о лицензионных выражениях и лицензиях, принимаемых NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="52db6-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="52db6-309">При упаковке файла лицензии необходимо использовать свойство Паккажелиценсефиле, чтобы указать путь к пакету относительно корня пакета.</span><span class="sxs-lookup"><span data-stu-id="52db6-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="52db6-310">Кроме того, необходимо убедиться, что файл включен в пакет.</span><span class="sxs-lookup"><span data-stu-id="52db6-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="52db6-311">Например:</span><span class="sxs-lookup"><span data-stu-id="52db6-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="52db6-312">[Пример файла лицензии](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="52db6-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="52db6-313">Упаковка файла без расширения</span><span class="sxs-lookup"><span data-stu-id="52db6-313">Packing a file without an extension</span></span>

<span data-ttu-id="52db6-314">В некоторых сценариях, например при упаковке файла лицензии, может потребоваться включить файл без расширения.</span><span class="sxs-lookup"><span data-stu-id="52db6-314">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="52db6-315">По историческим причинам NuGet & MSBuild обрабатывает пути без расширения в качестве каталогов.</span><span class="sxs-lookup"><span data-stu-id="52db6-315">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="52db6-316">[Файл без примера расширения](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="52db6-316">[File without an extension sample](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span></span>
### <a name="istool"></a><span data-ttu-id="52db6-317">IsTool</span><span class="sxs-lookup"><span data-stu-id="52db6-317">IsTool</span></span>

<span data-ttu-id="52db6-318">При использовании `MSBuild -t:pack -p:IsTool=true` все выходные файлы, как указано в сценарии [Выходные сборки](#output-assemblies), копируются в папку `tools` вместо папки `lib`.</span><span class="sxs-lookup"><span data-stu-id="52db6-318">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="52db6-319">Обратите внимание, что это свойство отличается от `DotNetCliTool`, которое указывается путем задания `PackageType` в файле `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="52db6-319">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="52db6-320">Упаковка с помощью NUSPEC</span><span class="sxs-lookup"><span data-stu-id="52db6-320">Packing using a .nuspec</span></span>

<span data-ttu-id="52db6-321">Хотя рекомендуется включить в файл проекта [все свойства](../reference/msbuild-targets.md#pack-target) , которые обычно находятся в файле `.nuspec` , можно использовать `.nuspec` файл для упаковки проекта.</span><span class="sxs-lookup"><span data-stu-id="52db6-321">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="52db6-322">Для проекта в стиле, отличном от SDK, который использует `PackageReference` , необходимо импортировать, `NuGet.Build.Tasks.Pack.targets` чтобы можно было выполнить задачу «Pack».</span><span class="sxs-lookup"><span data-stu-id="52db6-322">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="52db6-323">Вам по-прежнему потребуется восстановить проект, чтобы можно было упаковать файл nuspec.</span><span class="sxs-lookup"><span data-stu-id="52db6-323">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="52db6-324">(Проект в стиле SDK включает целевые объекты Pack по умолчанию.)</span><span class="sxs-lookup"><span data-stu-id="52db6-324">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="52db6-325">Целевая платформа файла проекта несущественна и не используется при упаковке nuspec.</span><span class="sxs-lookup"><span data-stu-id="52db6-325">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="52db6-326">Следующие три свойства MSBuild связаны с упаковкой с помощью `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="52db6-326">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="52db6-327">`NuspecFile`: относительный или абсолютный путь к файлу `.nuspec`, используемому для упаковки.</span><span class="sxs-lookup"><span data-stu-id="52db6-327">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="52db6-328">`NuspecProperties`: список разделенных точками с запятой пар "ключ-значение".</span><span class="sxs-lookup"><span data-stu-id="52db6-328">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="52db6-329">Из-за особенностей работы анализа в командной строке MSBuild несколько свойств нужно указать следующим образом: `-p:NuspecProperties="key1=value1;key2=value2"`.</span><span class="sxs-lookup"><span data-stu-id="52db6-329">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="52db6-330">`NuspecBasePath`: базовый путь для файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="52db6-330">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="52db6-331">Если вы используете `dotnet.exe` для упаковки проекта, воспользуйтесь командой, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="52db6-331">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="52db6-332">Если вы используете MSBuild для упаковки проекта, воспользуйтесь командой, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="52db6-332">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="52db6-333">Обратите внимание, что упаковка a nuspec с помощью dotnet.exe или MSBuild также ведет к построению проекта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="52db6-333">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="52db6-334">Это можно избежать, передав ```--no-build``` свойство в dotnet.exe, которое является аналогом параметра ```<NoBuild>true</NoBuild> ``` в файле проекта, а также параметром ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="52db6-334">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="52db6-335">Пример файла *. csproj* для упаковки файла nuspec:</span><span class="sxs-lookup"><span data-stu-id="52db6-335">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="52db6-336">Улучшенные точки расширения для создания настраиваемого пакета</span><span class="sxs-lookup"><span data-stu-id="52db6-336">Advanced extension points to create customized package</span></span>

<span data-ttu-id="52db6-337">`pack`Целевой объект предоставляет две точки расширения, которые выполняются во внутренней и целевой сборке конкретной платформы.</span><span class="sxs-lookup"><span data-stu-id="52db6-337">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="52db6-338">Поддержка точек расширения включает в пакет содержимое и сборки, относящиеся к целевой платформе.</span><span class="sxs-lookup"><span data-stu-id="52db6-338">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="52db6-339">`TargetsForTfmSpecificBuildOutput` target: используйте для файлов в `lib` папке или в папке, указанной с помощью `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="52db6-339">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="52db6-340">`TargetsForTfmSpecificContentInPackage` target: используйте для файлов за пределами `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="52db6-340">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="52db6-341">таржетсфортфмспеЦификбуилдаутпут</span><span class="sxs-lookup"><span data-stu-id="52db6-341">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="52db6-342">Напишите настраиваемый целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificBuildOutput)` Свойства.</span><span class="sxs-lookup"><span data-stu-id="52db6-342">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="52db6-343">Для файлов, которые необходимо переключать в `BuildOutputTargetFolder` (LIB по умолчанию), целевой объект должен записать эти файлы в ItemGroup `BuildOutputInPackage` и задать следующие два значения метаданных:</span><span class="sxs-lookup"><span data-stu-id="52db6-343">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="52db6-344">`FinalOutputPath`: Абсолютный путь к файлу; Если этот параметр не указан, для вычисления исходного пути используется удостоверение.</span><span class="sxs-lookup"><span data-stu-id="52db6-344">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="52db6-345">`TargetPath`: (Необязательно) задайте, когда файл необходимо переключиться во вложенную папку в `lib\<TargetFramework>` , например вспомогательные сборки, которые находятся в соответствующих папках языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="52db6-345">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="52db6-346">По умолчанию используется имя файла.</span><span class="sxs-lookup"><span data-stu-id="52db6-346">Defaults to the name of the file.</span></span>

<span data-ttu-id="52db6-347">Пример</span><span class="sxs-lookup"><span data-stu-id="52db6-347">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="52db6-348">таржетсфортфмспеЦификконтентинпаккаже</span><span class="sxs-lookup"><span data-stu-id="52db6-348">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="52db6-349">Напишите настраиваемый целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificContentInPackage)` Свойства.</span><span class="sxs-lookup"><span data-stu-id="52db6-349">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="52db6-350">Для всех файлов, включаемых в пакет, целевой объект должен записать эти файлы в ItemGroup `TfmSpecificPackageFile` и задать следующие необязательные метаданные:</span><span class="sxs-lookup"><span data-stu-id="52db6-350">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="52db6-351">`PackagePath`: Путь, по которому файл должен быть выведен в пакете.</span><span class="sxs-lookup"><span data-stu-id="52db6-351">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="52db6-352">NuGet выдает предупреждение, если в один и тот же путь к пакету добавляется несколько файлов.</span><span class="sxs-lookup"><span data-stu-id="52db6-352">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="52db6-353">`BuildAction`: Действие сборки, присваиваемое файлу, требуется только в том случае, если путь к пакету находится в `contentFiles` папке.</span><span class="sxs-lookup"><span data-stu-id="52db6-353">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="52db6-354">По умолчанию используется значение "нет".</span><span class="sxs-lookup"><span data-stu-id="52db6-354">Defaults to "None".</span></span>

<span data-ttu-id="52db6-355">Пример:</span><span class="sxs-lookup"><span data-stu-id="52db6-355">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="52db6-356">Целевой объект restore</span><span class="sxs-lookup"><span data-stu-id="52db6-356">restore target</span></span>

<span data-ttu-id="52db6-357">`MSBuild -t:restore` (который `nuget restore` и `dotnet restore` используют с проектами .NET Core) восстанавливает пакеты, на которые ссылается файл проекта:</span><span class="sxs-lookup"><span data-stu-id="52db6-357">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="52db6-358">Чтение перекрестных ссылок между проектами.</span><span class="sxs-lookup"><span data-stu-id="52db6-358">Read all project to project references</span></span>
1. <span data-ttu-id="52db6-359">Чтение свойств проекта, чтобы найти промежуточную папку и целевые платформы.</span><span class="sxs-lookup"><span data-stu-id="52db6-359">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="52db6-360">Передача данных MSBuild в NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="52db6-360">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="52db6-361">Запуск восстановления.</span><span class="sxs-lookup"><span data-stu-id="52db6-361">Run restore</span></span>
1. <span data-ttu-id="52db6-362">Скачивание пакетов</span><span class="sxs-lookup"><span data-stu-id="52db6-362">Download packages</span></span>
1. <span data-ttu-id="52db6-363">Запись файла ресурсов, целевых объектов и свойств.</span><span class="sxs-lookup"><span data-stu-id="52db6-363">Write assets file, targets, and props</span></span>

<span data-ttu-id="52db6-364">`restore`Целевой объект работает для проектов, использующих формат PackageReference.</span><span class="sxs-lookup"><span data-stu-id="52db6-364">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="52db6-365">`MSBuild 16.5+` также имеет [поддержку согласия](#restoring-packagereference-and-packagesconfig-with-msbuild) для `packages.config` формата.</span><span class="sxs-lookup"><span data-stu-id="52db6-365">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="52db6-366">`restore`Целевой объект [не должен выполняться](#restoring-and-building-with-one-msbuild-command) в сочетании с целевым объектом `build` .</span><span class="sxs-lookup"><span data-stu-id="52db6-366">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="52db6-367">Свойства восстановления</span><span class="sxs-lookup"><span data-stu-id="52db6-367">Restore properties</span></span>

<span data-ttu-id="52db6-368">Дополнительные параметры восстановления могут поступать из свойств MSBuild в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="52db6-368">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="52db6-369">Значения также можно задать из командной строки с помощью параметра `-p:` (см. примеры ниже).</span><span class="sxs-lookup"><span data-stu-id="52db6-369">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="52db6-370">Свойство</span><span class="sxs-lookup"><span data-stu-id="52db6-370">Property</span></span> | <span data-ttu-id="52db6-371">Описание</span><span class="sxs-lookup"><span data-stu-id="52db6-371">Description</span></span> |
|--------|--------|
| <span data-ttu-id="52db6-372">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="52db6-372">RestoreSources</span></span> | <span data-ttu-id="52db6-373">Разделенный точками с запятой список источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="52db6-373">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="52db6-374">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="52db6-374">RestorePackagesPath</span></span> | <span data-ttu-id="52db6-375">Путь к папке пакетов пользователя.</span><span class="sxs-lookup"><span data-stu-id="52db6-375">User packages folder path.</span></span> |
| <span data-ttu-id="52db6-376">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="52db6-376">RestoreDisableParallel</span></span> | <span data-ttu-id="52db6-377">Ограничение скачиваний до одного за раз.</span><span class="sxs-lookup"><span data-stu-id="52db6-377">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="52db6-378">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="52db6-378">RestoreConfigFile</span></span> | <span data-ttu-id="52db6-379">Путь к применяемому файлу `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="52db6-379">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="52db6-380">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="52db6-380">RestoreNoCache</span></span> | <span data-ttu-id="52db6-381">Значение true позволяет избежать использования кэшированных пакетов.</span><span class="sxs-lookup"><span data-stu-id="52db6-381">If true, avoids using cached packages.</span></span> <span data-ttu-id="52db6-382">См. раздел [Управление глобальными пакетами и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="52db6-382">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="52db6-383">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="52db6-383">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="52db6-384">Если значение равно true, нерабочие или отсутствующие источники пакетов игнорируются.</span><span class="sxs-lookup"><span data-stu-id="52db6-384">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="52db6-385">ресторефаллбаккфолдерс</span><span class="sxs-lookup"><span data-stu-id="52db6-385">RestoreFallbackFolders</span></span> | <span data-ttu-id="52db6-386">Резервные папки используются так же, как и папка User Packages.</span><span class="sxs-lookup"><span data-stu-id="52db6-386">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="52db6-387">рестореаддитионалпрожектсаурцес</span><span class="sxs-lookup"><span data-stu-id="52db6-387">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="52db6-388">Дополнительные источники, используемые во время восстановления.</span><span class="sxs-lookup"><span data-stu-id="52db6-388">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="52db6-389">рестореаддитионалпрожектфаллбаккфолдерс</span><span class="sxs-lookup"><span data-stu-id="52db6-389">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="52db6-390">Дополнительные резервные папки для использования во время восстановления.</span><span class="sxs-lookup"><span data-stu-id="52db6-390">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="52db6-391">рестореаддитионалпрожектфаллбаккфолдерсексклудес</span><span class="sxs-lookup"><span data-stu-id="52db6-391">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="52db6-392">Исключает резервные папки, указанные в `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="52db6-392">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="52db6-393">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="52db6-393">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="52db6-394">Путь к `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="52db6-394">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="52db6-395">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="52db6-395">RestoreGraphProjectInput</span></span> | <span data-ttu-id="52db6-396">Разделенный точками с запятой список проектов для восстановления, который должен содержать абсолютные пути.</span><span class="sxs-lookup"><span data-stu-id="52db6-396">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="52db6-397">рестореусескипнонексистенттаржетс</span><span class="sxs-lookup"><span data-stu-id="52db6-397">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="52db6-398">При сборе проектов с помощью MSBuild определяет, будут ли они собраны с помощью `SkipNonexistentTargets` оптимизации.</span><span class="sxs-lookup"><span data-stu-id="52db6-398">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="52db6-399">Если значение не задано, по умолчанию используется значение `true` .</span><span class="sxs-lookup"><span data-stu-id="52db6-399">When not set, defaults to `true`.</span></span> <span data-ttu-id="52db6-400">Следствием является быстрое поведение при сбое, если целевые объекты проекта не могут быть импортированы.</span><span class="sxs-lookup"><span data-stu-id="52db6-400">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="52db6-401">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="52db6-401">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="52db6-402">Папка Output, по умолчанию — `BaseIntermediateOutputPath` и `obj` Папка.</span><span class="sxs-lookup"><span data-stu-id="52db6-402">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="52db6-403">ресторефорце</span><span class="sxs-lookup"><span data-stu-id="52db6-403">RestoreForce</span></span> | <span data-ttu-id="52db6-404">В проектах на основе PackageReference принудительно разрешаются все зависимости, даже если последнее восстановление прошло успешно.</span><span class="sxs-lookup"><span data-stu-id="52db6-404">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="52db6-405">Установка этого флага аналогична удалению `project.assets.json` файла.</span><span class="sxs-lookup"><span data-stu-id="52db6-405">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="52db6-406">Это не позволяет обходить HTTP-кэш.</span><span class="sxs-lookup"><span data-stu-id="52db6-406">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="52db6-407">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="52db6-407">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="52db6-408">Разрешение использовать файл блокировки.</span><span class="sxs-lookup"><span data-stu-id="52db6-408">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="52db6-409">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="52db6-409">RestoreLockedMode</span></span> | <span data-ttu-id="52db6-410">Запустите восстановление в заблокированном режиме.</span><span class="sxs-lookup"><span data-stu-id="52db6-410">Run restore in locked mode.</span></span> <span data-ttu-id="52db6-411">Это означает, что восстановление не будет переоценивать зависимости.</span><span class="sxs-lookup"><span data-stu-id="52db6-411">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="52db6-412">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="52db6-412">NuGetLockFilePath</span></span> | <span data-ttu-id="52db6-413">Пользовательское расположение файла блокировки.</span><span class="sxs-lookup"><span data-stu-id="52db6-413">A custom location for the lock file.</span></span> <span data-ttu-id="52db6-414">Расположение по умолчанию находится рядом с проектом и имеет имя `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="52db6-414">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="52db6-415">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="52db6-415">RestoreForceEvaluate</span></span> | <span data-ttu-id="52db6-416">Принудительное восстановление для повторного расчета зависимостей и обновление файла блокировки без предупреждения.</span><span class="sxs-lookup"><span data-stu-id="52db6-416">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="52db6-417">ресторепаккажесконфиг</span><span class="sxs-lookup"><span data-stu-id="52db6-417">RestorePackagesConfig</span></span> | <span data-ttu-id="52db6-418">Параметр согласия, который восстанавливает проекты с packages.config. Поддерживается `MSBuild -t:restore` только с.</span><span class="sxs-lookup"><span data-stu-id="52db6-418">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| <span data-ttu-id="52db6-419">рестореусестатикграфевалуатион</span><span class="sxs-lookup"><span data-stu-id="52db6-419">RestoreUseStaticGraphEvaluation</span></span> | <span data-ttu-id="52db6-420">Переключение на использование статического графа MSBuild вместо стандартного вычисления.</span><span class="sxs-lookup"><span data-stu-id="52db6-420">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="52db6-421">Статическая Оценка графа — это экспериментальная функция, которая значительно ускоряется для больших репозиториев и решений.</span><span class="sxs-lookup"><span data-stu-id="52db6-421">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="52db6-422">Примеры</span><span class="sxs-lookup"><span data-stu-id="52db6-422">Examples</span></span>

<span data-ttu-id="52db6-423">Командная строка:</span><span class="sxs-lookup"><span data-stu-id="52db6-423">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="52db6-424">Файл проекта:</span><span class="sxs-lookup"><span data-stu-id="52db6-424">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="52db6-425">Выходные данные восстановления</span><span class="sxs-lookup"><span data-stu-id="52db6-425">Restore outputs</span></span>

<span data-ttu-id="52db6-426">Операция восстановления создает в папке сборки `obj` следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="52db6-426">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="52db6-427">Файл</span><span class="sxs-lookup"><span data-stu-id="52db6-427">File</span></span> | <span data-ttu-id="52db6-428">Описание</span><span class="sxs-lookup"><span data-stu-id="52db6-428">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="52db6-429">Содержит диаграмму зависимостей всех ссылок на пакеты.</span><span class="sxs-lookup"><span data-stu-id="52db6-429">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="52db6-430">Ссылки на свойства MSBuild, содержащиеся в пакетах.</span><span class="sxs-lookup"><span data-stu-id="52db6-430">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="52db6-431">Ссылки на целевые объекты MSBuild, содержащиеся в пакетах.</span><span class="sxs-lookup"><span data-stu-id="52db6-431">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="52db6-432">Восстановление и сборка с помощью одной команды MSBuild</span><span class="sxs-lookup"><span data-stu-id="52db6-432">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="52db6-433">Из-за того, что NuGet может восстанавливать пакеты, которые выводят цели и свойства MSBuild, оценки восстановления и сборки выполняются с разными глобальными свойствами.</span><span class="sxs-lookup"><span data-stu-id="52db6-433">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="52db6-434">Это означает, что следующие действия будут иметь непредсказуемое и неправильное поведение.</span><span class="sxs-lookup"><span data-stu-id="52db6-434">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="52db6-435">Вместо этого рекомендуемый подход:</span><span class="sxs-lookup"><span data-stu-id="52db6-435">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="52db6-436">Одна и та же логика применяется к другим целевым объектам, аналогичным `build` .</span><span class="sxs-lookup"><span data-stu-id="52db6-436">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="52db6-437">Восстановление PackageReference и packages.config с помощью MSBuild</span><span class="sxs-lookup"><span data-stu-id="52db6-437">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="52db6-438">С помощью MSBuild 16.5 + packages.config также поддерживаются для `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="52db6-438">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="52db6-439">`packages.config` Restore доступен только в `MSBuild 16.5+` , а не в `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="52db6-439">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="52db6-440">Восстановление со статической оценкой графа MSBuild</span><span class="sxs-lookup"><span data-stu-id="52db6-440">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="52db6-441">С помощью MSBuild 16.6 + NuGet добавил экспериментальную функцию для использования статической оценки графа из командной строки, значительно повышающей время восстановления для больших репозиториев.</span><span class="sxs-lookup"><span data-stu-id="52db6-441">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="52db6-442">Кроме того, его можно включить, задав свойство в каталоге. Build. props.</span><span class="sxs-lookup"><span data-stu-id="52db6-442">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="52db6-443">Начиная с Visual Studio 2019. x и NuGet 5. x, эта функция считается экспериментальной и явной.</span><span class="sxs-lookup"><span data-stu-id="52db6-443">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="52db6-444">Дополнительные сведения о том, когда эта функция будет включена по умолчанию, см. в [под9803е NuGet/Home #](https://github.com/NuGet/Home/issues/9803) .</span><span class="sxs-lookup"><span data-stu-id="52db6-444">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="52db6-445">При восстановлении статического графа изменяется часть MSBuild, вычисление и чтение проекта, но не алгоритм восстановления.</span><span class="sxs-lookup"><span data-stu-id="52db6-445">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="52db6-446">Алгоритм восстановления одинаков во всех инструментах NuGet (NuGet.exe, MSBuild.exe, dotnet.exe и Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="52db6-446">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="52db6-447">В очень редких случаях восстановление статических графов может отличаться от текущего при восстановлении, а некоторые объявленные PackageReferences или ссылками могут отсутствовать.</span><span class="sxs-lookup"><span data-stu-id="52db6-447">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="52db6-448">Для упрощения проверки при переходе к статическому восстановлению графа можно выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="52db6-448">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="52db6-449">NuGet *не* должен сообщать об изменениях.</span><span class="sxs-lookup"><span data-stu-id="52db6-449">NuGet should *not* report any changes.</span></span> <span data-ttu-id="52db6-450">Если вы видите несоответствие, напишите вопрос в [NuGet/Home](https://github.com/nuget/home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="52db6-450">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="52db6-451">Замена одной библиотеки из графа восстановления</span><span class="sxs-lookup"><span data-stu-id="52db6-451">Replacing one library from a restore graph</span></span>

<span data-ttu-id="52db6-452">Если операция восстановления предоставляет неправильную сборку, вы можете исключить значение по умолчанию для этого пакета, заменив его своим значением.</span><span class="sxs-lookup"><span data-stu-id="52db6-452">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="52db6-453">Первый с `PackageReference` верхнего уровня, исключите все ресурсы:</span><span class="sxs-lookup"><span data-stu-id="52db6-453">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="52db6-454">После этого добавьте собственную ссылку на соответствующую локальную копию библиотеки DLL:</span><span class="sxs-lookup"><span data-stu-id="52db6-454">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
