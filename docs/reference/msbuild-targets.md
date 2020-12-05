---
title: Объекты pack и restore NuGet в качестве целевых объектов MSBuild
description: Объекты pack и restore NuGet могут выступать непосредственно в качестве целевых объектов MSBuild в NuGet 4.0+.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 4a04c6dd7993fc47bcf7a6fe46236ed700a0d105
ms.sourcegitcommit: e39e5a5ddf68bf41e816617e7f0339308523bbb3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2020
ms.locfileid: "96738933"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="60a16-103">Объекты pack и restore NuGet в качестве целевых объектов MSBuild</span><span class="sxs-lookup"><span data-stu-id="60a16-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="60a16-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="60a16-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="60a16-105">В формате [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + может хранить все метаданные манифеста непосредственно в файле проекта вместо использования отдельного `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="60a16-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="60a16-106">При использовании MSBuild 15.1+ NuGet также является привилегированным компонентом MSBuild с целевыми объектами `pack` и `restore`, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="60a16-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="60a16-107">Эти целевые объекты позволяют работать с NuGet, как с любой другой задачей или другим целевым объектом MSBuild.</span><span class="sxs-lookup"><span data-stu-id="60a16-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="60a16-108">Инструкции по созданию пакета NuGet с помощью MSBuild см. в статье [Создание пакета NuGet с помощью MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="60a16-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="60a16-109">(Для NuGet 3.x и более ранних версий можно использовать команды [pack](../reference/cli-reference/cli-ref-pack.md) и [restore](../reference/cli-reference/cli-ref-restore.md) в NuGet CLI.)</span><span class="sxs-lookup"><span data-stu-id="60a16-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="60a16-110">Порядок сборки целевого объекта</span><span class="sxs-lookup"><span data-stu-id="60a16-110">Target build order</span></span>

<span data-ttu-id="60a16-111">Так как `pack` и `restore` являются целевыми объектами MSBuild, вы можете обращаться к ним для улучшения рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="60a16-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="60a16-112">Например, предположим, что вам нужно скопировать пакет в общую сетевую папку после его упаковки.</span><span class="sxs-lookup"><span data-stu-id="60a16-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="60a16-113">Это можно сделать, добавив следующий код в файл проекта:</span><span class="sxs-lookup"><span data-stu-id="60a16-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="60a16-114">Аналогичным образом, вы можете создать задачу MSBuild и собственный целевой объект и использовать свойства NuGet в этой задаче MSBuild.</span><span class="sxs-lookup"><span data-stu-id="60a16-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="60a16-115">`$(OutputPath)` является относительным и предполагает, что команда выполняется из корневого каталога проекта.</span><span class="sxs-lookup"><span data-stu-id="60a16-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="60a16-116">Целевой объект pack</span><span class="sxs-lookup"><span data-stu-id="60a16-116">pack target</span></span>

<span data-ttu-id="60a16-117">Для .NET Standard проектов, использующих формат PackageReference, команда `msbuild -t:pack` рисует входные данные из файла проекта для использования при создании пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="60a16-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="60a16-118">В следующей таблице описываются свойства MSBuild, которые можно добавить в файл проекта в первом узле `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="60a16-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="60a16-119">Эти изменения легко внести в Visual Studio 2017 и более поздней версии, щелкнув проект правой кнопкой мыши и выбрав пункт **Изменить {project_name}**.</span><span class="sxs-lookup"><span data-stu-id="60a16-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="60a16-120">Для удобства таблица упорядочивается по эквивалентному свойству в [ `.nuspec` файле](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="60a16-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="60a16-121">Обратите внимание, что свойства `Owners` и `Summary` из `.nuspec` не поддерживаются в MSBuild.</span><span class="sxs-lookup"><span data-stu-id="60a16-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="60a16-122">Значение атрибута или NuSpec</span><span class="sxs-lookup"><span data-stu-id="60a16-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="60a16-123">Свойство MSBuild</span><span class="sxs-lookup"><span data-stu-id="60a16-123">MSBuild Property</span></span> | <span data-ttu-id="60a16-124">По умолчанию</span><span class="sxs-lookup"><span data-stu-id="60a16-124">Default</span></span> | <span data-ttu-id="60a16-125">Примечания</span><span class="sxs-lookup"><span data-stu-id="60a16-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="60a16-126">Id</span><span class="sxs-lookup"><span data-stu-id="60a16-126">Id</span></span> | <span data-ttu-id="60a16-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="60a16-127">PackageId</span></span> | <span data-ttu-id="60a16-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="60a16-128">AssemblyName</span></span> | <span data-ttu-id="60a16-129">$(AssemblyName) из MSBuild</span><span class="sxs-lookup"><span data-stu-id="60a16-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="60a16-130">Версия</span><span class="sxs-lookup"><span data-stu-id="60a16-130">Version</span></span> | <span data-ttu-id="60a16-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="60a16-131">PackageVersion</span></span> | <span data-ttu-id="60a16-132">Версия</span><span class="sxs-lookup"><span data-stu-id="60a16-132">Version</span></span> | <span data-ttu-id="60a16-133">Это значение совместимо с SemVer, например "1.0.0", "1.0.0-beta" или "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="60a16-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="60a16-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="60a16-134">VersionPrefix</span></span> | <span data-ttu-id="60a16-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="60a16-135">PackageVersionPrefix</span></span> | <span data-ttu-id="60a16-136">пустых</span><span class="sxs-lookup"><span data-stu-id="60a16-136">empty</span></span> | <span data-ttu-id="60a16-137">Задав PackageVersion, вы перезапишите PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="60a16-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="60a16-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="60a16-138">VersionSuffix</span></span> | <span data-ttu-id="60a16-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="60a16-139">PackageVersionSuffix</span></span> | <span data-ttu-id="60a16-140">пустых</span><span class="sxs-lookup"><span data-stu-id="60a16-140">empty</span></span> | <span data-ttu-id="60a16-141">$(VersionSuffix) из MSBuild.</span><span class="sxs-lookup"><span data-stu-id="60a16-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="60a16-142">Задав PackageVersion, вы перезапишите PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="60a16-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="60a16-143">Авторы</span><span class="sxs-lookup"><span data-stu-id="60a16-143">Authors</span></span> | <span data-ttu-id="60a16-144">Авторы</span><span class="sxs-lookup"><span data-stu-id="60a16-144">Authors</span></span> | <span data-ttu-id="60a16-145">Имя текущего пользователя</span><span class="sxs-lookup"><span data-stu-id="60a16-145">Username of the current user</span></span> | |
| <span data-ttu-id="60a16-146">Владельцы</span><span class="sxs-lookup"><span data-stu-id="60a16-146">Owners</span></span> | <span data-ttu-id="60a16-147">Н/Д</span><span class="sxs-lookup"><span data-stu-id="60a16-147">N/A</span></span> | <span data-ttu-id="60a16-148">Не существует в NuSpec</span><span class="sxs-lookup"><span data-stu-id="60a16-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="60a16-149">Заголовок</span><span class="sxs-lookup"><span data-stu-id="60a16-149">Title</span></span> | <span data-ttu-id="60a16-150">Заголовок</span><span class="sxs-lookup"><span data-stu-id="60a16-150">Title</span></span> | <span data-ttu-id="60a16-151">Идентификатор пакета</span><span class="sxs-lookup"><span data-stu-id="60a16-151">The PackageId</span></span>| |
| <span data-ttu-id="60a16-152">Description</span><span class="sxs-lookup"><span data-stu-id="60a16-152">Description</span></span> | <span data-ttu-id="60a16-153">Описание</span><span class="sxs-lookup"><span data-stu-id="60a16-153">Description</span></span> | <span data-ttu-id="60a16-154">"Описание пакета"</span><span class="sxs-lookup"><span data-stu-id="60a16-154">"Package Description"</span></span> | |
| <span data-ttu-id="60a16-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="60a16-155">Copyright</span></span> | <span data-ttu-id="60a16-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="60a16-156">Copyright</span></span> | <span data-ttu-id="60a16-157">пустых</span><span class="sxs-lookup"><span data-stu-id="60a16-157">empty</span></span> | |
| <span data-ttu-id="60a16-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="60a16-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="60a16-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="60a16-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="60a16-160">false</span><span class="sxs-lookup"><span data-stu-id="60a16-160">false</span></span> | |
| <span data-ttu-id="60a16-161">license</span><span class="sxs-lookup"><span data-stu-id="60a16-161">license</span></span> | <span data-ttu-id="60a16-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="60a16-162">PackageLicenseExpression</span></span> | <span data-ttu-id="60a16-163">пустых</span><span class="sxs-lookup"><span data-stu-id="60a16-163">empty</span></span> | <span data-ttu-id="60a16-164">Соответствует `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="60a16-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="60a16-165">license</span><span class="sxs-lookup"><span data-stu-id="60a16-165">license</span></span> | <span data-ttu-id="60a16-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="60a16-166">PackageLicenseFile</span></span> | <span data-ttu-id="60a16-167">пустых</span><span class="sxs-lookup"><span data-stu-id="60a16-167">empty</span></span> | <span data-ttu-id="60a16-168">Соответствует `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="60a16-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="60a16-169">Необходимо явно упаковать файл лицензии, на который указывает ссылка.</span><span class="sxs-lookup"><span data-stu-id="60a16-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="60a16-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="60a16-170">LicenseUrl</span></span> | <span data-ttu-id="60a16-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="60a16-171">PackageLicenseUrl</span></span> | <span data-ttu-id="60a16-172">пустых</span><span class="sxs-lookup"><span data-stu-id="60a16-172">empty</span></span> | <span data-ttu-id="60a16-173">`PackageLicenseUrl` является устаревшим, используйте свойство Паккажелиценсикспрессион или Паккажелиценсефиле.</span><span class="sxs-lookup"><span data-stu-id="60a16-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="60a16-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="60a16-174">ProjectUrl</span></span> | <span data-ttu-id="60a16-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="60a16-175">PackageProjectUrl</span></span> | <span data-ttu-id="60a16-176">пустых</span><span class="sxs-lookup"><span data-stu-id="60a16-176">empty</span></span> | |
| <span data-ttu-id="60a16-177">Значок</span><span class="sxs-lookup"><span data-stu-id="60a16-177">Icon</span></span> | <span data-ttu-id="60a16-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="60a16-178">PackageIcon</span></span> | <span data-ttu-id="60a16-179">пустых</span><span class="sxs-lookup"><span data-stu-id="60a16-179">empty</span></span> | <span data-ttu-id="60a16-180">Необходимо явно упаковать файл изображения значка, на который указывает ссылка.</span><span class="sxs-lookup"><span data-stu-id="60a16-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="60a16-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="60a16-181">IconUrl</span></span> | <span data-ttu-id="60a16-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="60a16-182">PackageIconUrl</span></span> | <span data-ttu-id="60a16-183">пустых</span><span class="sxs-lookup"><span data-stu-id="60a16-183">empty</span></span> | <span data-ttu-id="60a16-184">Для лучшей работы с предыдущими версиями `PackageIconUrl` следует указать в дополнение к `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="60a16-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="60a16-185">Более длительное выражение `PackageIconUrl` будет считаться устаревшим.</span><span class="sxs-lookup"><span data-stu-id="60a16-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="60a16-186">Теги</span><span class="sxs-lookup"><span data-stu-id="60a16-186">Tags</span></span> | <span data-ttu-id="60a16-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="60a16-187">PackageTags</span></span> | <span data-ttu-id="60a16-188">пустых</span><span class="sxs-lookup"><span data-stu-id="60a16-188">empty</span></span> | <span data-ttu-id="60a16-189">Теги разделяются точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="60a16-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="60a16-190">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="60a16-190">ReleaseNotes</span></span> | <span data-ttu-id="60a16-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="60a16-191">PackageReleaseNotes</span></span> | <span data-ttu-id="60a16-192">пустых</span><span class="sxs-lookup"><span data-stu-id="60a16-192">empty</span></span> | |
| <span data-ttu-id="60a16-193">Репозиторий/URL-адрес</span><span class="sxs-lookup"><span data-stu-id="60a16-193">Repository/Url</span></span> | <span data-ttu-id="60a16-194">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="60a16-194">RepositoryUrl</span></span> | <span data-ttu-id="60a16-195">пустых</span><span class="sxs-lookup"><span data-stu-id="60a16-195">empty</span></span> | <span data-ttu-id="60a16-196">URL-адрес репозитория, используемый для клонирования или извлечения исходного кода.</span><span class="sxs-lookup"><span data-stu-id="60a16-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="60a16-197">Например *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="60a16-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="60a16-198">Репозиторий или тип</span><span class="sxs-lookup"><span data-stu-id="60a16-198">Repository/Type</span></span> | <span data-ttu-id="60a16-199">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="60a16-199">RepositoryType</span></span> | <span data-ttu-id="60a16-200">пустых</span><span class="sxs-lookup"><span data-stu-id="60a16-200">empty</span></span> | <span data-ttu-id="60a16-201">Тип репозитория.</span><span class="sxs-lookup"><span data-stu-id="60a16-201">Repository type.</span></span> <span data-ttu-id="60a16-202">Примеры: *Git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="60a16-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="60a16-203">Репозиторий или ветвь</span><span class="sxs-lookup"><span data-stu-id="60a16-203">Repository/Branch</span></span> | <span data-ttu-id="60a16-204">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="60a16-204">RepositoryBranch</span></span> | <span data-ttu-id="60a16-205">пустых</span><span class="sxs-lookup"><span data-stu-id="60a16-205">empty</span></span> | <span data-ttu-id="60a16-206">Дополнительные сведения о ветви репозитория.</span><span class="sxs-lookup"><span data-stu-id="60a16-206">Optional repository branch information.</span></span> <span data-ttu-id="60a16-207">Для включения этого свойства также необходимо указать *репоситорюрл* .</span><span class="sxs-lookup"><span data-stu-id="60a16-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="60a16-208">Пример: *master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="60a16-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="60a16-209">Репозиторий/фиксация</span><span class="sxs-lookup"><span data-stu-id="60a16-209">Repository/Commit</span></span> | <span data-ttu-id="60a16-210">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="60a16-210">RepositoryCommit</span></span> | <span data-ttu-id="60a16-211">пустых</span><span class="sxs-lookup"><span data-stu-id="60a16-211">empty</span></span> | <span data-ttu-id="60a16-212">Необязательная фиксация или набор изменений репозитория для указания источника, на основе которого был создан пакет.</span><span class="sxs-lookup"><span data-stu-id="60a16-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="60a16-213">Для включения этого свойства также необходимо указать *репоситорюрл* .</span><span class="sxs-lookup"><span data-stu-id="60a16-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="60a16-214">Пример: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="60a16-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="60a16-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="60a16-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="60a16-216">Сводка</span><span class="sxs-lookup"><span data-stu-id="60a16-216">Summary</span></span> | <span data-ttu-id="60a16-217">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="60a16-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="60a16-218">Входные данные целевого объекта pack</span><span class="sxs-lookup"><span data-stu-id="60a16-218">pack target inputs</span></span>

- <span data-ttu-id="60a16-219">IsPackable</span><span class="sxs-lookup"><span data-stu-id="60a16-219">IsPackable</span></span>
- <span data-ttu-id="60a16-220">суппрессдепенденЦиесвхенпаккинг</span><span class="sxs-lookup"><span data-stu-id="60a16-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="60a16-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="60a16-221">PackageVersion</span></span>
- <span data-ttu-id="60a16-222">PackageId</span><span class="sxs-lookup"><span data-stu-id="60a16-222">PackageId</span></span>
- <span data-ttu-id="60a16-223">Авторы</span><span class="sxs-lookup"><span data-stu-id="60a16-223">Authors</span></span>
- <span data-ttu-id="60a16-224">Описание</span><span class="sxs-lookup"><span data-stu-id="60a16-224">Description</span></span>
- <span data-ttu-id="60a16-225">Copyright</span><span class="sxs-lookup"><span data-stu-id="60a16-225">Copyright</span></span>
- <span data-ttu-id="60a16-226">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="60a16-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="60a16-227">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="60a16-227">DevelopmentDependency</span></span>
- <span data-ttu-id="60a16-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="60a16-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="60a16-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="60a16-229">PackageLicenseFile</span></span>
- <span data-ttu-id="60a16-230">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="60a16-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="60a16-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="60a16-231">PackageProjectUrl</span></span>
- <span data-ttu-id="60a16-232">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="60a16-232">PackageIconUrl</span></span>
- <span data-ttu-id="60a16-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="60a16-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="60a16-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="60a16-234">PackageTags</span></span>
- <span data-ttu-id="60a16-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="60a16-235">PackageOutputPath</span></span>
- <span data-ttu-id="60a16-236">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="60a16-236">IncludeSymbols</span></span>
- <span data-ttu-id="60a16-237">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="60a16-237">IncludeSource</span></span>
- <span data-ttu-id="60a16-238">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="60a16-238">PackageTypes</span></span>
- <span data-ttu-id="60a16-239">IsTool</span><span class="sxs-lookup"><span data-stu-id="60a16-239">IsTool</span></span>
- <span data-ttu-id="60a16-240">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="60a16-240">RepositoryUrl</span></span>
- <span data-ttu-id="60a16-241">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="60a16-241">RepositoryType</span></span>
- <span data-ttu-id="60a16-242">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="60a16-242">RepositoryBranch</span></span>
- <span data-ttu-id="60a16-243">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="60a16-243">RepositoryCommit</span></span>
- <span data-ttu-id="60a16-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="60a16-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="60a16-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="60a16-245">MinClientVersion</span></span>
- <span data-ttu-id="60a16-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="60a16-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="60a16-247">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="60a16-247">IncludeContentInPack</span></span>
- <span data-ttu-id="60a16-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="60a16-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="60a16-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="60a16-249">ContentTargetFolders</span></span>
- <span data-ttu-id="60a16-250">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="60a16-250">NuspecFile</span></span>
- <span data-ttu-id="60a16-251">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="60a16-251">NuspecBasePath</span></span>
- <span data-ttu-id="60a16-252">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="60a16-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="60a16-253">Сценарии использования pack</span><span class="sxs-lookup"><span data-stu-id="60a16-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="60a16-254">Подавлять зависимости</span><span class="sxs-lookup"><span data-stu-id="60a16-254">Suppress dependencies</span></span>

<span data-ttu-id="60a16-255">Чтобы исключить зависимости пакета из созданного пакета NuGet, задайте для значение, `SuppressDependenciesWhenPacking` `true` которое позволит пропустить все зависимости из созданного файла nupkg.</span><span class="sxs-lookup"><span data-stu-id="60a16-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="60a16-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="60a16-256">PackageIconUrl</span></span>

<span data-ttu-id="60a16-257">`PackageIconUrl` будет считаться устаревшим в пользу нового [`PackageIcon`](#packageicon) Свойства.</span><span class="sxs-lookup"><span data-stu-id="60a16-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="60a16-258">Начиная с NuGet 5,3 & Visual Studio 2019 версии 16,3, `pack` вызовет предупреждение [NU5048](./errors-and-warnings/nu5048.md) , если только метаданные пакета указывают только `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="60a16-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="60a16-259">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="60a16-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="60a16-260">`PackageIcon` `PackageIconUrl` Для обеспечения обратной совместимости с клиентами и источниками, которые еще не поддерживаются, необходимо указать и, и `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="60a16-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="60a16-261">Visual Studio будет поддерживать `PackageIcon` пакеты, поступающие из источника на основе папок в будущем выпуске.</span><span class="sxs-lookup"><span data-stu-id="60a16-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="60a16-262">Упаковка файла изображения значка</span><span class="sxs-lookup"><span data-stu-id="60a16-262">Packing an icon image file</span></span>

<span data-ttu-id="60a16-263">При упаковке файла изображения значка необходимо использовать `PackageIcon` свойство, чтобы указать путь к пакету относительно корня пакета.</span><span class="sxs-lookup"><span data-stu-id="60a16-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="60a16-264">Кроме того, необходимо убедиться, что файл включен в пакет.</span><span class="sxs-lookup"><span data-stu-id="60a16-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="60a16-265">Размер файла изображения ограничен 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="60a16-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="60a16-266">Поддерживаются следующие форматы файлов: JPEG и PNG.</span><span class="sxs-lookup"><span data-stu-id="60a16-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="60a16-267">Рекомендуется разрешение изображения 128x128.</span><span class="sxs-lookup"><span data-stu-id="60a16-267">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="60a16-268">Пример:</span><span class="sxs-lookup"><span data-stu-id="60a16-268">For example:</span></span>

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

<span data-ttu-id="60a16-269">[Пример значка пакета](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="60a16-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="60a16-270">Чтобы получить nuspec эквивалент, просмотрите [ссылку на nuspec для значка](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="60a16-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="60a16-271">Выходные сборки</span><span class="sxs-lookup"><span data-stu-id="60a16-271">Output assemblies</span></span>

<span data-ttu-id="60a16-272">`nuget pack` копирует выходные файлы с расширениями `.exe`, `.dll`, `.xml`, `.winmd`, `.json` и `.pri`.</span><span class="sxs-lookup"><span data-stu-id="60a16-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="60a16-273">Копируемые выходные файлы зависят от того, что MSBuild предоставляет из целевого объекта `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="60a16-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="60a16-274">Существует два свойства MSBuild, которые можно использовать в файле проекта или командной строке для управления местом назначения для выходных сборок:</span><span class="sxs-lookup"><span data-stu-id="60a16-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="60a16-275">`IncludeBuildOutput`: логическое значение, определяющее, следует ли включать выходные сборки в пакете.</span><span class="sxs-lookup"><span data-stu-id="60a16-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="60a16-276">`BuildOutputTargetFolder`: указывает папку, куда следует помещать выходные сборки.</span><span class="sxs-lookup"><span data-stu-id="60a16-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="60a16-277">Выходные сборки (и другие выходные файлы) копируются в соответствующие папки платформы.</span><span class="sxs-lookup"><span data-stu-id="60a16-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="60a16-278">Ссылки на пакеты</span><span class="sxs-lookup"><span data-stu-id="60a16-278">Package references</span></span>

<span data-ttu-id="60a16-279">См. раздел [Ссылки на пакеты в файлах проекта](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="60a16-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="60a16-280">Перекрестные ссылки между проектами</span><span class="sxs-lookup"><span data-stu-id="60a16-280">Project to project references</span></span>

<span data-ttu-id="60a16-281">Перекрестные ссылки между проектами по умолчанию считаются ссылками на пакет NuGet, например:</span><span class="sxs-lookup"><span data-stu-id="60a16-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="60a16-282">Вы также можете добавить в ссылку на проект следующие метаданные:</span><span class="sxs-lookup"><span data-stu-id="60a16-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="60a16-283">Включение содержимого в пакет</span><span class="sxs-lookup"><span data-stu-id="60a16-283">Including content in a package</span></span>

<span data-ttu-id="60a16-284">Чтобы включить содержимое, добавьте дополнительные метаданные для существующего элемента `<Content>`.</span><span class="sxs-lookup"><span data-stu-id="60a16-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="60a16-285">По умолчанию все данные типа "Content" включаются в пакет, если только вы не переопределите такое поведение с помощью записей, аналогичных следующим:</span><span class="sxs-lookup"><span data-stu-id="60a16-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="60a16-286">По умолчанию все данные добавляются в корень папки `content` и `contentFiles\any\<target_framework>` в пакете и сохраняют относительную структуру папок, если только не указан путь к пакету:</span><span class="sxs-lookup"><span data-stu-id="60a16-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="60a16-287">Если требуется скопировать все содержимое только в определенные корневые папки (вместо `content` и `contentFiles`), можно использовать свойство MSBuild `ContentTargetFolders`, которое по умолчанию имеет значение "content;contentFiles", но может принимать любые другие имена папок.</span><span class="sxs-lookup"><span data-stu-id="60a16-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="60a16-288">Обратите внимание, если указать "contentFiles" в `ContentTargetFolders`, файлы помещаются в `contentFiles\any\<target_framework>` или `contentFiles\<language>\<target_framework>` в зависимости от `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="60a16-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="60a16-289">`PackagePath` может быть набором целевых путей, разделенных точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="60a16-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="60a16-290">Если указан пустой путь к пакету, файл добавляется в корневой каталог пакета.</span><span class="sxs-lookup"><span data-stu-id="60a16-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="60a16-291">Например, следующий код добавляет `libuv.txt` в `content\myfiles`, `content\samples` и корневой каталог пакета:</span><span class="sxs-lookup"><span data-stu-id="60a16-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="60a16-292">Имеется также свойство MSBuild `$(IncludeContentInPack)`, которое по умолчанию равно `true`.</span><span class="sxs-lookup"><span data-stu-id="60a16-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="60a16-293">Если оно имеет значение `false` для какого-либо проекта, то содержимое этого проекта не включается в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="60a16-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="60a16-294">Другие относящиеся к pack метаданные, которые можно задать для любого из указанных выше элементов, включают ```<PackageCopyToOutput>``` и ```<PackageFlatten>```, задающие значения ```CopyToOutput``` и ```Flatten``` для записи ```contentFiles``` в выходном файле NUSPEC.</span><span class="sxs-lookup"><span data-stu-id="60a16-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="60a16-295">Кроме элементов содержимого, метаданные `<Pack>` и `<PackagePath>` также можно задать для файлов с действием сборки Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource или None.</span><span class="sxs-lookup"><span data-stu-id="60a16-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="60a16-296">Чтобы объект pack добавил имя файла в путь к пакету при использовании стандартных масок, путь к пакету должен заканчиваться символом разделителя папок, в противном случае этот путь считается полным путем, включающим имя файла.</span><span class="sxs-lookup"><span data-stu-id="60a16-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="60a16-297">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="60a16-297">IncludeSymbols</span></span>

<span data-ttu-id="60a16-298">При использовании `MSBuild -t:pack -p:IncludeSymbols=true` соответствующие файлы `.pdb` копируются вместе с другими выходными файлами (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="60a16-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="60a16-299">Обратите внимание, что при задании `IncludeSymbols=true` создается обычный пакет *и* пакет символов.</span><span class="sxs-lookup"><span data-stu-id="60a16-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="60a16-300">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="60a16-300">IncludeSource</span></span>

<span data-ttu-id="60a16-301">Аналогично `IncludeSymbols`, только копирует исходные файлы вместе с файлами `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="60a16-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="60a16-302">Все файлы типа `Compile` копируются в `src\<ProjectName>\` с сохранением относительной структуры папок в итоговом пакете.</span><span class="sxs-lookup"><span data-stu-id="60a16-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="60a16-303">То же самое происходит с исходными файлами любого `ProjectReference`, у которого `TreatAsPackageReference` имеет значение `false`.</span><span class="sxs-lookup"><span data-stu-id="60a16-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="60a16-304">Если файл типа Compile находится вне папки проекта, он просто добавляется в `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="60a16-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="60a16-305">Упаковка выражения лицензии или файла лицензии</span><span class="sxs-lookup"><span data-stu-id="60a16-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="60a16-306">При использовании выражения лицензии следует использовать свойство Паккажелиценсикспрессион.</span><span class="sxs-lookup"><span data-stu-id="60a16-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="60a16-307">[Пример выражения лицензии](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="60a16-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="60a16-308">Дополнительные [сведения о лицензионных выражениях и лицензиях, принимаемых NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="60a16-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="60a16-309">При упаковке файла лицензии необходимо использовать свойство Паккажелиценсефиле, чтобы указать путь к пакету относительно корня пакета.</span><span class="sxs-lookup"><span data-stu-id="60a16-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="60a16-310">Кроме того, необходимо убедиться, что файл включен в пакет.</span><span class="sxs-lookup"><span data-stu-id="60a16-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="60a16-311">Пример:</span><span class="sxs-lookup"><span data-stu-id="60a16-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="60a16-312">[Пример файла лицензии](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="60a16-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="60a16-313">IsTool</span><span class="sxs-lookup"><span data-stu-id="60a16-313">IsTool</span></span>

<span data-ttu-id="60a16-314">При использовании `MSBuild -t:pack -p:IsTool=true` все выходные файлы, как указано в сценарии [Выходные сборки](#output-assemblies), копируются в папку `tools` вместо папки `lib`.</span><span class="sxs-lookup"><span data-stu-id="60a16-314">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="60a16-315">Обратите внимание, что это свойство отличается от `DotNetCliTool`, которое указывается путем задания `PackageType` в файле `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="60a16-315">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="60a16-316">Упаковка с помощью NUSPEC</span><span class="sxs-lookup"><span data-stu-id="60a16-316">Packing using a .nuspec</span></span>

<span data-ttu-id="60a16-317">Хотя рекомендуется включить в файл проекта [все свойства](../reference/msbuild-targets.md#pack-target) , которые обычно находятся в файле `.nuspec` , можно использовать `.nuspec` файл для упаковки проекта.</span><span class="sxs-lookup"><span data-stu-id="60a16-317">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="60a16-318">Для проекта в стиле, отличном от SDK, который использует `PackageReference` , необходимо импортировать, `NuGet.Build.Tasks.Pack.targets` чтобы можно было выполнить задачу «Pack».</span><span class="sxs-lookup"><span data-stu-id="60a16-318">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="60a16-319">Вам по-прежнему потребуется восстановить проект, чтобы можно было упаковать файл nuspec.</span><span class="sxs-lookup"><span data-stu-id="60a16-319">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="60a16-320">(Проект в стиле SDK включает целевые объекты Pack по умолчанию.)</span><span class="sxs-lookup"><span data-stu-id="60a16-320">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="60a16-321">Целевая платформа файла проекта несущественна и не используется при упаковке nuspec.</span><span class="sxs-lookup"><span data-stu-id="60a16-321">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="60a16-322">Следующие три свойства MSBuild связаны с упаковкой с помощью `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="60a16-322">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="60a16-323">`NuspecFile`: относительный или абсолютный путь к файлу `.nuspec`, используемому для упаковки.</span><span class="sxs-lookup"><span data-stu-id="60a16-323">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="60a16-324">`NuspecProperties`: список разделенных точками с запятой пар "ключ-значение".</span><span class="sxs-lookup"><span data-stu-id="60a16-324">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="60a16-325">Из-за особенностей работы анализа в командной строке MSBuild несколько свойств нужно указать следующим образом: `-p:NuspecProperties="key1=value1;key2=value2"`.</span><span class="sxs-lookup"><span data-stu-id="60a16-325">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="60a16-326">`NuspecBasePath`: базовый путь для файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="60a16-326">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="60a16-327">Если вы используете `dotnet.exe` для упаковки проекта, воспользуйтесь командой, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="60a16-327">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="60a16-328">Если вы используете MSBuild для упаковки проекта, воспользуйтесь командой, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="60a16-328">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="60a16-329">Обратите внимание, что упаковка a nuspec с помощью dotnet.exe или MSBuild также ведет к построению проекта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="60a16-329">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="60a16-330">Это можно избежать, передав ```--no-build``` свойство в dotnet.exe, которое является аналогом параметра ```<NoBuild>true</NoBuild> ``` в файле проекта, а также параметром ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="60a16-330">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="60a16-331">Пример файла *. csproj* для упаковки файла nuspec:</span><span class="sxs-lookup"><span data-stu-id="60a16-331">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="60a16-332">Улучшенные точки расширения для создания настраиваемого пакета</span><span class="sxs-lookup"><span data-stu-id="60a16-332">Advanced extension points to create customized package</span></span>

<span data-ttu-id="60a16-333">`pack`Целевой объект предоставляет две точки расширения, которые выполняются во внутренней и целевой сборке конкретной платформы.</span><span class="sxs-lookup"><span data-stu-id="60a16-333">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="60a16-334">Поддержка точек расширения включает в пакет содержимое и сборки, относящиеся к целевой платформе.</span><span class="sxs-lookup"><span data-stu-id="60a16-334">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="60a16-335">`TargetsForTfmSpecificBuildOutput` target: используйте для файлов в `lib` папке или в папке, указанной с помощью `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="60a16-335">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="60a16-336">`TargetsForTfmSpecificContentInPackage` target: используйте для файлов за пределами `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="60a16-336">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="60a16-337">таржетсфортфмспеЦификбуилдаутпут</span><span class="sxs-lookup"><span data-stu-id="60a16-337">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="60a16-338">Напишите настраиваемый целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificBuildOutput)` Свойства.</span><span class="sxs-lookup"><span data-stu-id="60a16-338">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="60a16-339">Для файлов, которые необходимо переключать в `BuildOutputTargetFolder` (LIB по умолчанию), целевой объект должен записать эти файлы в ItemGroup `BuildOutputInPackage` и задать следующие два значения метаданных:</span><span class="sxs-lookup"><span data-stu-id="60a16-339">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="60a16-340">`FinalOutputPath`: Абсолютный путь к файлу; Если этот параметр не указан, для вычисления исходного пути используется удостоверение.</span><span class="sxs-lookup"><span data-stu-id="60a16-340">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="60a16-341">`TargetPath`: (Необязательно) задайте, когда файл необходимо переключиться во вложенную папку в `lib\<TargetFramework>` , например вспомогательные сборки, которые находятся в соответствующих папках языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="60a16-341">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="60a16-342">По умолчанию используется имя файла.</span><span class="sxs-lookup"><span data-stu-id="60a16-342">Defaults to the name of the file.</span></span>

<span data-ttu-id="60a16-343">Пример</span><span class="sxs-lookup"><span data-stu-id="60a16-343">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="60a16-344">таржетсфортфмспеЦификконтентинпаккаже</span><span class="sxs-lookup"><span data-stu-id="60a16-344">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="60a16-345">Напишите настраиваемый целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificContentInPackage)` Свойства.</span><span class="sxs-lookup"><span data-stu-id="60a16-345">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="60a16-346">Для всех файлов, включаемых в пакет, целевой объект должен записать эти файлы в ItemGroup `TfmSpecificPackageFile` и задать следующие необязательные метаданные:</span><span class="sxs-lookup"><span data-stu-id="60a16-346">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="60a16-347">`PackagePath`: Путь, по которому файл должен быть выведен в пакете.</span><span class="sxs-lookup"><span data-stu-id="60a16-347">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="60a16-348">NuGet выдает предупреждение, если в один и тот же путь к пакету добавляется несколько файлов.</span><span class="sxs-lookup"><span data-stu-id="60a16-348">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="60a16-349">`BuildAction`: Действие сборки, присваиваемое файлу, требуется только в том случае, если путь к пакету находится в `contentFiles` папке.</span><span class="sxs-lookup"><span data-stu-id="60a16-349">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="60a16-350">По умолчанию используется значение "нет".</span><span class="sxs-lookup"><span data-stu-id="60a16-350">Defaults to "None".</span></span>

<span data-ttu-id="60a16-351">Пример:</span><span class="sxs-lookup"><span data-stu-id="60a16-351">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="60a16-352">Целевой объект restore</span><span class="sxs-lookup"><span data-stu-id="60a16-352">restore target</span></span>

<span data-ttu-id="60a16-353">`MSBuild -t:restore` (который `nuget restore` и `dotnet restore` используют с проектами .NET Core) восстанавливает пакеты, на которые ссылается файл проекта:</span><span class="sxs-lookup"><span data-stu-id="60a16-353">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="60a16-354">Чтение перекрестных ссылок между проектами.</span><span class="sxs-lookup"><span data-stu-id="60a16-354">Read all project to project references</span></span>
1. <span data-ttu-id="60a16-355">Чтение свойств проекта, чтобы найти промежуточную папку и целевые платформы.</span><span class="sxs-lookup"><span data-stu-id="60a16-355">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="60a16-356">Передача данных MSBuild в NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="60a16-356">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="60a16-357">Запуск восстановления.</span><span class="sxs-lookup"><span data-stu-id="60a16-357">Run restore</span></span>
1. <span data-ttu-id="60a16-358">Скачивание пакетов</span><span class="sxs-lookup"><span data-stu-id="60a16-358">Download packages</span></span>
1. <span data-ttu-id="60a16-359">Запись файла ресурсов, целевых объектов и свойств.</span><span class="sxs-lookup"><span data-stu-id="60a16-359">Write assets file, targets, and props</span></span>

<span data-ttu-id="60a16-360">`restore`Целевой объект работает для проектов, использующих формат PackageReference.</span><span class="sxs-lookup"><span data-stu-id="60a16-360">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="60a16-361">`MSBuild 16.5+` также имеет [поддержку согласия](#restoring-packagereference-and-packages.config-with-msbuild) для `packages.config` формата.</span><span class="sxs-lookup"><span data-stu-id="60a16-361">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packages.config-with-msbuild) for the `packages.config` format.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="60a16-362">Свойства восстановления</span><span class="sxs-lookup"><span data-stu-id="60a16-362">Restore properties</span></span>

<span data-ttu-id="60a16-363">Дополнительные параметры восстановления могут поступать из свойств MSBuild в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="60a16-363">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="60a16-364">Значения также можно задать из командной строки с помощью параметра `-p:` (см. примеры ниже).</span><span class="sxs-lookup"><span data-stu-id="60a16-364">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="60a16-365">Свойство.</span><span class="sxs-lookup"><span data-stu-id="60a16-365">Property</span></span> | <span data-ttu-id="60a16-366">Описание</span><span class="sxs-lookup"><span data-stu-id="60a16-366">Description</span></span> |
|--------|--------|
| <span data-ttu-id="60a16-367">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="60a16-367">RestoreSources</span></span> | <span data-ttu-id="60a16-368">Разделенный точками с запятой список источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="60a16-368">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="60a16-369">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="60a16-369">RestorePackagesPath</span></span> | <span data-ttu-id="60a16-370">Путь к папке пакетов пользователя.</span><span class="sxs-lookup"><span data-stu-id="60a16-370">User packages folder path.</span></span> |
| <span data-ttu-id="60a16-371">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="60a16-371">RestoreDisableParallel</span></span> | <span data-ttu-id="60a16-372">Ограничение скачиваний до одного за раз.</span><span class="sxs-lookup"><span data-stu-id="60a16-372">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="60a16-373">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="60a16-373">RestoreConfigFile</span></span> | <span data-ttu-id="60a16-374">Путь к применяемому файлу `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="60a16-374">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="60a16-375">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="60a16-375">RestoreNoCache</span></span> | <span data-ttu-id="60a16-376">Значение true позволяет избежать использования кэшированных пакетов.</span><span class="sxs-lookup"><span data-stu-id="60a16-376">If true, avoids using cached packages.</span></span> <span data-ttu-id="60a16-377">См. раздел [Управление глобальными пакетами и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="60a16-377">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="60a16-378">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="60a16-378">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="60a16-379">Если значение равно true, нерабочие или отсутствующие источники пакетов игнорируются.</span><span class="sxs-lookup"><span data-stu-id="60a16-379">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="60a16-380">ресторефаллбаккфолдерс</span><span class="sxs-lookup"><span data-stu-id="60a16-380">RestoreFallbackFolders</span></span> | <span data-ttu-id="60a16-381">Резервные папки используются так же, как и папка User Packages.</span><span class="sxs-lookup"><span data-stu-id="60a16-381">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="60a16-382">рестореаддитионалпрожектсаурцес</span><span class="sxs-lookup"><span data-stu-id="60a16-382">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="60a16-383">Дополнительные источники, используемые во время восстановления.</span><span class="sxs-lookup"><span data-stu-id="60a16-383">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="60a16-384">рестореаддитионалпрожектфаллбаккфолдерс</span><span class="sxs-lookup"><span data-stu-id="60a16-384">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="60a16-385">Дополнительные резервные папки для использования во время восстановления.</span><span class="sxs-lookup"><span data-stu-id="60a16-385">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="60a16-386">рестореаддитионалпрожектфаллбаккфолдерсексклудес</span><span class="sxs-lookup"><span data-stu-id="60a16-386">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="60a16-387">Исключает резервные папки, указанные в `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="60a16-387">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="60a16-388">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="60a16-388">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="60a16-389">Путь к `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="60a16-389">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="60a16-390">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="60a16-390">RestoreGraphProjectInput</span></span> | <span data-ttu-id="60a16-391">Разделенный точками с запятой список проектов для восстановления, который должен содержать абсолютные пути.</span><span class="sxs-lookup"><span data-stu-id="60a16-391">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="60a16-392">рестореусескипнонексистенттаржетс</span><span class="sxs-lookup"><span data-stu-id="60a16-392">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="60a16-393">При сборе проектов с помощью MSBuild определяет, будут ли они собраны с помощью `SkipNonexistentTargets` оптимизации.</span><span class="sxs-lookup"><span data-stu-id="60a16-393">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="60a16-394">Если значение не задано, по умолчанию используется значение `true` .</span><span class="sxs-lookup"><span data-stu-id="60a16-394">When not set, defaults to `true`.</span></span> <span data-ttu-id="60a16-395">Следствием является быстрое поведение при сбое, если целевые объекты проекта не могут быть импортированы.</span><span class="sxs-lookup"><span data-stu-id="60a16-395">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="60a16-396">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="60a16-396">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="60a16-397">Папка Output, по умолчанию — `BaseIntermediateOutputPath` и `obj` Папка.</span><span class="sxs-lookup"><span data-stu-id="60a16-397">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="60a16-398">ресторефорце</span><span class="sxs-lookup"><span data-stu-id="60a16-398">RestoreForce</span></span> | <span data-ttu-id="60a16-399">В проектах на основе PackageReference принудительно разрешаются все зависимости, даже если последнее восстановление прошло успешно.</span><span class="sxs-lookup"><span data-stu-id="60a16-399">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="60a16-400">Установка этого флага аналогична удалению `project.assets.json` файла.</span><span class="sxs-lookup"><span data-stu-id="60a16-400">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="60a16-401">Это не позволяет обходить HTTP-кэш.</span><span class="sxs-lookup"><span data-stu-id="60a16-401">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="60a16-402">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="60a16-402">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="60a16-403">Разрешение использовать файл блокировки.</span><span class="sxs-lookup"><span data-stu-id="60a16-403">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="60a16-404">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="60a16-404">RestoreLockedMode</span></span> | <span data-ttu-id="60a16-405">Запустите восстановление в заблокированном режиме.</span><span class="sxs-lookup"><span data-stu-id="60a16-405">Run restore in locked mode.</span></span> <span data-ttu-id="60a16-406">Это означает, что восстановление не будет переоценивать зависимости.</span><span class="sxs-lookup"><span data-stu-id="60a16-406">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="60a16-407">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="60a16-407">NuGetLockFilePath</span></span> | <span data-ttu-id="60a16-408">Пользовательское расположение файла блокировки.</span><span class="sxs-lookup"><span data-stu-id="60a16-408">A custom location for the lock file.</span></span> <span data-ttu-id="60a16-409">Расположение по умолчанию находится рядом с проектом и имеет имя `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="60a16-409">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="60a16-410">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="60a16-410">RestoreForceEvaluate</span></span> | <span data-ttu-id="60a16-411">Принудительное восстановление для повторного расчета зависимостей и обновление файла блокировки без предупреждения.</span><span class="sxs-lookup"><span data-stu-id="60a16-411">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="60a16-412">ресторепаккажесконфиг</span><span class="sxs-lookup"><span data-stu-id="60a16-412">RestorePackagesConfig</span></span> | <span data-ttu-id="60a16-413">Переключатель opt, который восстанавливает проекты с packages.config. Поддерживается `MSBuild -t:restore` только с.</span><span class="sxs-lookup"><span data-stu-id="60a16-413">An opt in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |

#### <a name="examples"></a><span data-ttu-id="60a16-414">Примеры</span><span class="sxs-lookup"><span data-stu-id="60a16-414">Examples</span></span>

<span data-ttu-id="60a16-415">Командная строка:</span><span class="sxs-lookup"><span data-stu-id="60a16-415">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="60a16-416">Файл проекта:</span><span class="sxs-lookup"><span data-stu-id="60a16-416">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="60a16-417">Выходные данные восстановления</span><span class="sxs-lookup"><span data-stu-id="60a16-417">Restore outputs</span></span>

<span data-ttu-id="60a16-418">Операция восстановления создает в папке сборки `obj` следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="60a16-418">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="60a16-419">Файл</span><span class="sxs-lookup"><span data-stu-id="60a16-419">File</span></span> | <span data-ttu-id="60a16-420">Описание</span><span class="sxs-lookup"><span data-stu-id="60a16-420">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="60a16-421">Содержит диаграмму зависимостей всех ссылок на пакеты.</span><span class="sxs-lookup"><span data-stu-id="60a16-421">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="60a16-422">Ссылки на свойства MSBuild, содержащиеся в пакетах.</span><span class="sxs-lookup"><span data-stu-id="60a16-422">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="60a16-423">Ссылки на целевые объекты MSBuild, содержащиеся в пакетах.</span><span class="sxs-lookup"><span data-stu-id="60a16-423">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="60a16-424">Восстановление и сборка с помощью одной команды MSBuild</span><span class="sxs-lookup"><span data-stu-id="60a16-424">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="60a16-425">Из-за того, что NuGet может восстанавливать пакеты, которые выводят цели и свойства MSBuild, оценки восстановления и сборки выполняются с разными глобальными свойствами.</span><span class="sxs-lookup"><span data-stu-id="60a16-425">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="60a16-426">Это означает, что следующие действия будут иметь непредсказуемое и неправильное поведение.</span><span class="sxs-lookup"><span data-stu-id="60a16-426">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="60a16-427">Вместо этого рекомендуемый подход:</span><span class="sxs-lookup"><span data-stu-id="60a16-427">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="60a16-428">Одна и та же логика применяется к другим целевым объектам, аналогичным `build` .</span><span class="sxs-lookup"><span data-stu-id="60a16-428">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="60a16-429">Восстановление PackageReference и packages.config с помощью MSBuild</span><span class="sxs-lookup"><span data-stu-id="60a16-429">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="60a16-430">С помощью MSBuild 16.5 + packages.config также поддерживаются для `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="60a16-430">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="60a16-431">`packages.config` Restore доступен только в `MSBuild 16.5+` , а не в `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="60a16-431">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="60a16-432">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="60a16-432">PackageTargetFallback</span></span>

<span data-ttu-id="60a16-433">Элемент `PackageTargetFallback` позволяет указать набор совместимых целевых объектов, которые следует использовать при восстановлении пакетов.</span><span class="sxs-lookup"><span data-stu-id="60a16-433">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="60a16-434">Он разрешает пакетам, использующим dotnet [TxM](../reference/target-frameworks.md), взаимодействовать с совместимыми пакетами, которые не объявляют dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="60a16-434">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="60a16-435">Таким образом, если в проекте используется dotnet TxM, все пакеты, от которых вы зависите, должны также содержать dotnet TxM. В противном случае нужно добавить `<PackageTargetFallback>` в проект, чтобы обеспечить совместимость с платформами, отличными от dotnet.</span><span class="sxs-lookup"><span data-stu-id="60a16-435">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="60a16-436">Например, если в проекте используется `netstandard1.6` TxM, а зависимый пакет содержит только `lib/net45/a.dll` и `lib/portable-net45+win81/a.dll`, то сборка проекта завершится со сбоем.</span><span class="sxs-lookup"><span data-stu-id="60a16-436">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="60a16-437">Если вы хотите использовать вторую библиотеку DLL, можете добавить `PackageTargetFallback` следующим образом, чтобы обозначить совместимость библиотеки DLL `portable-net45+win81`:</span><span class="sxs-lookup"><span data-stu-id="60a16-437">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="60a16-438">Чтобы объявить откат для всех целевых объектов в проекте, оставьте атрибут `Condition`.</span><span class="sxs-lookup"><span data-stu-id="60a16-438">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="60a16-439">Кроме того, можно расширить существующий `PackageTargetFallback`, включив `$(PackageTargetFallback)`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="60a16-439">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="60a16-440">Замена одной библиотеки из графа восстановления</span><span class="sxs-lookup"><span data-stu-id="60a16-440">Replacing one library from a restore graph</span></span>

<span data-ttu-id="60a16-441">Если операция восстановления предоставляет неправильную сборку, вы можете исключить значение по умолчанию для этого пакета, заменив его своим значением.</span><span class="sxs-lookup"><span data-stu-id="60a16-441">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="60a16-442">Первый с `PackageReference` верхнего уровня, исключите все ресурсы:</span><span class="sxs-lookup"><span data-stu-id="60a16-442">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="60a16-443">После этого добавьте собственную ссылку на соответствующую локальную копию библиотеки DLL:</span><span class="sxs-lookup"><span data-stu-id="60a16-443">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
