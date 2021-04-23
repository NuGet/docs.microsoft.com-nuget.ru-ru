---
title: NuGet упаковать и восстановить как MSBuild целевые объекты
description: NuGet пакет и восстановление могут работать непосредственно в качестве MSBuild целевых объектов с помощью 4.0 и более поздних версий NuGet .
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 0a10a6f1e4c71903232281c25a6c4b6bbc65fb34
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901490"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="4c5ad-103">NuGet упаковать и восстановить как MSBuild целевые объекты</span><span class="sxs-lookup"><span data-stu-id="4c5ad-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="4c5ad-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="4c5ad-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="4c5ad-105">В формате [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + может хранить все метаданные манифеста непосредственно в файле проекта вместо использования отдельного `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="4c5ad-106">С помощью MSBuild 15.1 + NuGet также является членом первого класса MSBuild с `pack` `restore` целевыми объектами и, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="4c5ad-107">Эти целевые объекты позволяют работать NuGet так же, как с любой другой MSBuild задачей или целевым объектом.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="4c5ad-108">Инструкции по созданию NuGet пакета с помощью см MSBuild . в разделе [Создание NuGet пакета MSBuild с помощью ](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="4c5ad-109">(Для NuGet 3. x и более ранних версиях вы используете команды [Pack](../reference/cli-reference/cli-ref-pack.md) и [RESTORE](../reference/cli-reference/cli-ref-restore.md) через интерфейс NuGet командной строки.)</span><span class="sxs-lookup"><span data-stu-id="4c5ad-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="4c5ad-110">Порядок сборки целевого объекта</span><span class="sxs-lookup"><span data-stu-id="4c5ad-110">Target build order</span></span>

<span data-ttu-id="4c5ad-111">Поскольку `pack` и `restore` являются  MSBuild целевыми объектами, к ним можно обращаться для улучшения рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="4c5ad-112">Например, предположим, что вы хотите скопировать пакет в сетевую папку после упаковки.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-112">For example, let's say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="4c5ad-113">Это можно сделать, добавив следующий код в файл проекта:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="4c5ad-114">Аналогичным образом можно написать MSBuild задачу, написать собственный целевой объект и использовать NuGet свойства в MSBuild задаче.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="4c5ad-115">`$(OutputPath)` является относительным и предполагает, что команда выполняется из корневого каталога проекта.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="4c5ad-116">Целевой объект pack</span><span class="sxs-lookup"><span data-stu-id="4c5ad-116">pack target</span></span>

<span data-ttu-id="4c5ad-117">Для проектов .NET, использующих `PackageReference` Формат, с помощью команды `msbuild -t:pack` рисует входные данные из файла проекта для использования при создании NuGet пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="4c5ad-118">В следующей таблице описаны MSBuild свойства, которые можно добавить в файл проекта в пределах первого `<PropertyGroup>` узла.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="4c5ad-119">Эти изменения легко внести в Visual Studio 2017 и более поздней версии, щелкнув проект правой кнопкой мыши и выбрав пункт **Изменить {project_name}**.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="4c5ad-120">Для удобства таблица упорядочивается по эквивалентному свойству в [ `.nuspec` файле](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4c5ad-121">`Owners``Summary`Свойства и из `.nuspec` не поддерживаются в MSBuild .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-121">`Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="4c5ad-122">Атрибут или nuspec значение</span><span class="sxs-lookup"><span data-stu-id="4c5ad-122">Attribute/nuspec Value</span></span> | <span data-ttu-id="4c5ad-123">СвойствоMSBuild .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-123">MSBuild Property</span></span> | <span data-ttu-id="4c5ad-124">По умолчанию</span><span class="sxs-lookup"><span data-stu-id="4c5ad-124">Default</span></span> | <span data-ttu-id="4c5ad-125">Примечания</span><span class="sxs-lookup"><span data-stu-id="4c5ad-125">Notes</span></span> |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | <span data-ttu-id="4c5ad-126">`$(AssemblyName)` из MSBuild</span><span class="sxs-lookup"><span data-stu-id="4c5ad-126">`$(AssemblyName)` from MSBuild</span></span> |
| `Version` | `PackageVersion` | <span data-ttu-id="4c5ad-127">Версия</span><span class="sxs-lookup"><span data-stu-id="4c5ad-127">Version</span></span> | <span data-ttu-id="4c5ad-128">Это semver совместимо, например, `1.0.0` `1.0.0-beta` или `1.0.0-beta-00345`</span><span class="sxs-lookup"><span data-stu-id="4c5ad-128">This is semver compatible, for example `1.0.0`, `1.0.0-beta`, or `1.0.0-beta-00345`</span></span> |
| `VersionPrefix` | `PackageVersionPrefix` | <span data-ttu-id="4c5ad-129">пустых</span><span class="sxs-lookup"><span data-stu-id="4c5ad-129">empty</span></span> | <span data-ttu-id="4c5ad-130">Настройка `PackageVersion` перезаписи `PackageVersionPrefix`</span><span class="sxs-lookup"><span data-stu-id="4c5ad-130">Setting `PackageVersion` overwrites `PackageVersionPrefix`</span></span> |
| `VersionSuffix` | `PackageVersionSuffix` | <span data-ttu-id="4c5ad-131">пустых</span><span class="sxs-lookup"><span data-stu-id="4c5ad-131">empty</span></span> | <span data-ttu-id="4c5ad-132">`$(VersionSuffix)` из MSBuild .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-132">`$(VersionSuffix)` from MSBuild.</span></span> <span data-ttu-id="4c5ad-133">Настройка `PackageVersion` перезаписи `PackageVersionSuffix`</span><span class="sxs-lookup"><span data-stu-id="4c5ad-133">Setting `PackageVersion` overwrites `PackageVersionSuffix`</span></span> |
| `Authors` | `Authors` | <span data-ttu-id="4c5ad-134">Имя текущего пользователя</span><span class="sxs-lookup"><span data-stu-id="4c5ad-134">Username of the current user</span></span> | <span data-ttu-id="4c5ad-135">Разделенный точками с запятой список авторов пакетов, соответствующих именам профилей в nuget.org. Они отображаются в NuGet коллекции NuGet.org и используются для перекрестных ссылок на пакеты с теми же авторами.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-135">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Owners` | <span data-ttu-id="4c5ad-136">Н/Д</span><span class="sxs-lookup"><span data-stu-id="4c5ad-136">N/A</span></span> | <span data-ttu-id="4c5ad-137">Отсутствует в nuspec</span><span class="sxs-lookup"><span data-stu-id="4c5ad-137">Not present in nuspec</span></span> | |
| `Title` | `Title` | <span data-ttu-id="4c5ad-138">Конструктор `PackageId`</span><span class="sxs-lookup"><span data-stu-id="4c5ad-138">The `PackageId`</span></span> | <span data-ttu-id="4c5ad-139">Понятный заголовок пакета, обычно используемый при отображении пользовательского интерфейса, как на сайте nuget.org и в диспетчере пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| `Description` | `Description` | <span data-ttu-id="4c5ad-140">"Описание пакета"</span><span class="sxs-lookup"><span data-stu-id="4c5ad-140">"Package Description"</span></span> | <span data-ttu-id="4c5ad-141">Подробное описание сборки.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-141">A long description for the assembly.</span></span> <span data-ttu-id="4c5ad-142">Если `PackageDescription` не указывать, это свойство также будет использоваться в качестве описания пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-142">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | `Copyright` | <span data-ttu-id="4c5ad-143">пустых</span><span class="sxs-lookup"><span data-stu-id="4c5ad-143">empty</span></span> | <span data-ttu-id="4c5ad-144">Сведения об авторских правах для пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-144">Copyright details for the package.</span></span> |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | <span data-ttu-id="4c5ad-145">Логическое значение, указывающее, должен ли клиент просить потребителя принять условия лицензии перед установкой пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-145">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| `license` | `PackageLicenseExpression` | <span data-ttu-id="4c5ad-146">пустых</span><span class="sxs-lookup"><span data-stu-id="4c5ad-146">empty</span></span> | <span data-ttu-id="4c5ad-147">Соответствует `<license type="expression">`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-147">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="4c5ad-148">См. раздел [Упаковка лицензионного выражения или файла лицензии](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-148">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `license` | `PackageLicenseFile` | <span data-ttu-id="4c5ad-149">пустых</span><span class="sxs-lookup"><span data-stu-id="4c5ad-149">empty</span></span> | <span data-ttu-id="4c5ad-150">Путь к файлу лицензии в пакете, если вы используете пользовательскую лицензию или лицензию, которой не назначен идентификатор СПДКС.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-150">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="4c5ad-151">Необходимо явно упаковать файл лицензии, на который указывает ссылка.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-151">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="4c5ad-152">Соответствует `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-152">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="4c5ad-153">См. раздел [Упаковка лицензионного выражения или файла лицензии](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-153">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `LicenseUrl` | `PackageLicenseUrl` | <span data-ttu-id="4c5ad-154">пустых</span><span class="sxs-lookup"><span data-stu-id="4c5ad-154">empty</span></span> | <span data-ttu-id="4c5ad-155">Параметр `PackageLicenseUrl` использовать не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-155">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="4c5ad-156">Вместо него следует использовать элементы `PackageLicenseExpression` или `PackageLicenseFile`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-156">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `ProjectUrl` | `PackageProjectUrl` | <span data-ttu-id="4c5ad-157">пустых</span><span class="sxs-lookup"><span data-stu-id="4c5ad-157">empty</span></span> | |
| `Icon` | `PackageIcon` | <span data-ttu-id="4c5ad-158">пустых</span><span class="sxs-lookup"><span data-stu-id="4c5ad-158">empty</span></span> | <span data-ttu-id="4c5ad-159">Путь к образу в пакете, используемому в качестве значка пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-159">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="4c5ad-160">Необходимо явно упаковать файл изображения значка, на который указывает ссылка.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-160">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="4c5ad-161">Дополнительные сведения см. в разделе Упаковка изображения и [ `icon` метаданных](./nuspec.md#icon) [значка](#packing-an-icon-image-file) .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-161">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](./nuspec.md#icon).</span></span> |
| `IconUrl` | `PackageIconUrl` | <span data-ttu-id="4c5ad-162">пустых</span><span class="sxs-lookup"><span data-stu-id="4c5ad-162">empty</span></span> | <span data-ttu-id="4c5ad-163">`PackageIconUrl` является нерекомендуемым в пользу `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-163">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="4c5ad-164">Однако для лучшей работы с предыдущими версиями необходимо указать `PackageIconUrl` в дополнение к `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-164">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| `Readme` | `PackageReadmeFile` | <span data-ttu-id="4c5ad-165">пустых</span><span class="sxs-lookup"><span data-stu-id="4c5ad-165">empty</span></span> | <span data-ttu-id="4c5ad-166">Необходимо явно упаковать файл сведений, на который указывает ссылка.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-166">You need to explicitly pack the referenced readme file.</span></span>|
| `Tags` | `PackageTags` | <span data-ttu-id="4c5ad-167">пустых</span><span class="sxs-lookup"><span data-stu-id="4c5ad-167">empty</span></span> | <span data-ttu-id="4c5ad-168">Разделенный точками с запятой список тегов, обозначающий пакет.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-168">A semicolon-delimited list of tags that designates the package.</span></span> |
| `ReleaseNotes` | `PackageReleaseNotes` | <span data-ttu-id="4c5ad-169">пустых</span><span class="sxs-lookup"><span data-stu-id="4c5ad-169">empty</span></span> | <span data-ttu-id="4c5ad-170">Заметки о выпуске для пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-170">Release notes for the package.</span></span> |
| `Repository/Url` | `RepositoryUrl` | <span data-ttu-id="4c5ad-171">пустых</span><span class="sxs-lookup"><span data-stu-id="4c5ad-171">empty</span></span> | <span data-ttu-id="4c5ad-172">URL-адрес репозитория, используемый для клонирования или извлечения исходного кода.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-172">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="4c5ad-173">Пример: *https://github.com/ NuGet / NuGet . Client. git*.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-173">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `Repository/Type` | `RepositoryType` | <span data-ttu-id="4c5ad-174">пустых</span><span class="sxs-lookup"><span data-stu-id="4c5ad-174">empty</span></span> | <span data-ttu-id="4c5ad-175">Тип репозитория.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-175">Repository type.</span></span> <span data-ttu-id="4c5ad-176">Примеры: `git` (по умолчанию), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-176">Examples: `git` (default), `tfs`.</span></span> |
| `Repository/Branch` | `RepositoryBranch` | <span data-ttu-id="4c5ad-177">пустых</span><span class="sxs-lookup"><span data-stu-id="4c5ad-177">empty</span></span> | <span data-ttu-id="4c5ad-178">Дополнительные сведения о ветви репозитория.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-178">Optional repository branch information.</span></span> <span data-ttu-id="4c5ad-179">Необходимо также указать `RepositoryUrl`, чтобы включить это свойство.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-179">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="4c5ad-180">Пример: *master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-180">Example: *master* (NuGet 4.7.0+).</span></span> |
| `Repository/Commit` | `RepositoryCommit` | <span data-ttu-id="4c5ad-181">пустых</span><span class="sxs-lookup"><span data-stu-id="4c5ad-181">empty</span></span> | <span data-ttu-id="4c5ad-182">Необязательная фиксация или набор изменений репозитория для указания источника, на основе которого был создан пакет.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-182">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="4c5ad-183">Необходимо также указать `RepositoryUrl`, чтобы включить это свойство.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-183">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="4c5ad-184">Пример: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-184">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | <span data-ttu-id="4c5ad-185">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="4c5ad-185">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="4c5ad-186">Входные данные целевого объекта pack</span><span class="sxs-lookup"><span data-stu-id="4c5ad-186">pack target inputs</span></span>

| <span data-ttu-id="4c5ad-187">Свойство</span><span class="sxs-lookup"><span data-stu-id="4c5ad-187">Property</span></span> | <span data-ttu-id="4c5ad-188">Описание</span><span class="sxs-lookup"><span data-stu-id="4c5ad-188">Description</span></span> |
| - | - |
| `IsPackable` | <span data-ttu-id="4c5ad-189">Логическое значение, которое указывает, можно ли упаковать проект.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-189">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="4c5ad-190">Значение по умолчанию — `true`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-190">The default value is `true`.</span></span> |
| `SuppressDependenciesWhenPacking` | <span data-ttu-id="4c5ad-191">Установите значение `true` , чтобы подавить зависимости пакета от созданного NuGet пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-191">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| `PackageVersion` | <span data-ttu-id="4c5ad-192">Указывает версию, которую будет иметь итоговый пакет.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-192">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="4c5ad-193">Принимает все формы NuGet строки версии.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-193">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="4c5ad-194">По умолчанию используется значение `$(Version)`, то есть значение свойства `Version` в проекте.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-194">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| `PackageId` | <span data-ttu-id="4c5ad-195">Указывает имя для итогового пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-195">Specifies the name for the resulting package.</span></span> <span data-ttu-id="4c5ad-196">Если значение не указано, операция `pack` по умолчанию использует в качестве имени пакета `AssemblyName` или имя каталога.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-196">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| `PackageDescription` | <span data-ttu-id="4c5ad-197">Подробное описание пакета для отображения пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-197">A long description of the package for UI display.</span></span> |
| `Authors` | <span data-ttu-id="4c5ad-198">Разделенный точками с запятой список авторов пакетов, соответствующих именам профилей в nuget.org. Они отображаются в NuGet коллекции NuGet.org и используются для перекрестных ссылок на пакеты с теми же авторами.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-198">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Description` | <span data-ttu-id="4c5ad-199">Подробное описание сборки.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-199">A long description for the assembly.</span></span> <span data-ttu-id="4c5ad-200">Если `PackageDescription` не указывать, это свойство также будет использоваться в качестве описания пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-200">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | <span data-ttu-id="4c5ad-201">Сведения об авторских правах для пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-201">Copyright details for the package.</span></span> |
| `PackageRequireLicenseAcceptance` | <span data-ttu-id="4c5ad-202">Логическое значение, указывающее, должен ли клиент просить потребителя принять условия лицензии перед установкой пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-202">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="4c5ad-203">Значение по умолчанию — `false`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-203">The default is `false`.</span></span> |
| `DevelopmentDependency` | <span data-ttu-id="4c5ad-204">Логическое значение, указывающее на то, помечен ли пакет как зависимость только для разработки, что позволяет запретить его включение в качестве зависимости в другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-204">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="4c5ad-205">В `PackageReference` ( NuGet 4.8 +) этот флаг также означает, что ресурсы времени компиляции исключаются из компиляции.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-205">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="4c5ad-206">Дополнительные сведения см. в статье [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) (Поддержка DevelopmentDependency для PackageReference).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-206">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| `PackageLicenseExpression` | <span data-ttu-id="4c5ad-207">Идентификатор или выражение [лицензии спдкс](https://spdx.org/licenses/) , например `Apache-2.0` .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-207">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="4c5ad-208">Дополнительные сведения см. в разделе Упаковка а. Лицензионное [выражение или файл лицензии](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-208">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `PackageLicenseFile` | <span data-ttu-id="4c5ad-209">Путь к файлу лицензии в пакете, если вы используете пользовательскую лицензию или лицензию, которой не назначен идентификатор СПДКС.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-209">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| `PackageLicenseUrl` | <span data-ttu-id="4c5ad-210">Параметр `PackageLicenseUrl` использовать не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-210">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="4c5ad-211">Вместо него следует использовать элементы `PackageLicenseExpression` или `PackageLicenseFile`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-211">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `PackageProjectUrl` | |
| `PackageIcon` | <span data-ttu-id="4c5ad-212">Указывает путь к значку пакета относительно корня пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-212">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="4c5ad-213">Дополнительные сведения см. в разделе [Упаковка файла изображения значка](#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-213">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| `PackageReleaseNotes` | <span data-ttu-id="4c5ad-214">Заметки о выпуске для пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-214">Release notes for the package.</span></span> |
| `PackageReadmeFile` | <span data-ttu-id="4c5ad-215">Файл сведений о пакете.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-215">Readme for the package.</span></span> |
| `PackageTags` | <span data-ttu-id="4c5ad-216">Разделенный точками с запятой список тегов, обозначающий пакет.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-216">A semicolon-delimited list of tags that designates the package.</span></span> |
| `PackageOutputPath` | <span data-ttu-id="4c5ad-217">Определяет выходной путь для размещения упакованного пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-217">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="4c5ad-218">Значение по умолчанию — `$(OutputPath)`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-218">Default is `$(OutputPath)`.</span></span> |
| `IncludeSymbols` | <span data-ttu-id="4c5ad-219">Это логическое значение указывает, должен ли пакет создавать дополнительный пакет символов при упаковке проекта.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-219">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="4c5ad-220">Форматом пакета символов управляет свойство `SymbolPackageFormat`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-220">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="4c5ad-221">Дополнительные сведения см. в разделе [инклудесимболс](#includesymbols).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-221">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| `IncludeSource` | <span data-ttu-id="4c5ad-222">Это логическое значение указывает, должен ли процесс упаковки создавать исходный пакет.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-222">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="4c5ad-223">Исходный пакет содержит библиотеку исходного кода, а также файлы PDB.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-223">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="4c5ad-224">Исходные файлы помещаются в каталог `src/ProjectName` итогового файла пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-224">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="4c5ad-225">Дополнительные сведения см. в разделе [инклудесаурце](#includesource).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-225">For more information, see [IncludeSource](#includesource).</span></span> |
| `PackageType` | |
| `IsTool` | <span data-ttu-id="4c5ad-226">Указывает, копируются ли все выходные файлы в папку *tools* вместо папки *lib*.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-226">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="4c5ad-227">Дополнительные сведения см. в разделе [Tool](#istool).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-227">For more information, see [IsTool](#istool).</span></span> |
| `RepositoryUrl` | <span data-ttu-id="4c5ad-228">URL-адрес репозитория, используемый для клонирования или извлечения исходного кода.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-228">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="4c5ad-229">Пример: *https://github.com/ NuGet / NuGet . Client. git*.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-229">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `RepositoryType` | <span data-ttu-id="4c5ad-230">Тип репозитория.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-230">Repository type.</span></span> <span data-ttu-id="4c5ad-231">Примеры: `git` (по умолчанию), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-231">Examples: `git` (default), `tfs`.</span></span> |
| `RepositoryBranch` | <span data-ttu-id="4c5ad-232">Дополнительные сведения о ветви репозитория.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-232">Optional repository branch information.</span></span> <span data-ttu-id="4c5ad-233">Необходимо также указать `RepositoryUrl`, чтобы включить это свойство.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-233">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="4c5ad-234">Пример: *master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-234">Example: *master* (NuGet 4.7.0+).</span></span> |
| `RepositoryCommit` | <span data-ttu-id="4c5ad-235">Необязательная фиксация или набор изменений репозитория для указания источника, на основе которого был создан пакет.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-235">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="4c5ad-236">Необходимо также указать `RepositoryUrl`, чтобы включить это свойство.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-236">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="4c5ad-237">Пример: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-237">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `SymbolPackageFormat` | <span data-ttu-id="4c5ad-238">Задает формат пакета символов.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-238">Specifies the format of the symbols package.</span></span> <span data-ttu-id="4c5ad-239">Если "Symbols. nupkg", пакет устаревших символов создается с расширением *. Symbols. nupkg* , содержащим PDB, DLL и другие выходные файлы.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-239">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="4c5ad-240">Если "снупкг", создается пакет символов снупкг, содержащий переносимые PDB-файлы.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-240">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="4c5ad-241">Значение по умолчанию — Symbols. nupkg.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-241">The default is "symbols.nupkg".</span></span> |
| `NoPackageAnalysis` | <span data-ttu-id="4c5ad-242">Указывает, что `pack` не следует выполнять анализ пакетов после сборки пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-242">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| `MinClientVersion` | <span data-ttu-id="4c5ad-243">Указывает минимальную версию NuGet клиента, который может установить этот пакет, принудительно с помощью nuget.exe и диспетчера пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-243">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| `IncludeBuildOutput` | <span data-ttu-id="4c5ad-244">Это логическое значение указывает, следует ли упаковывать выходные сборки в файл *NUPKG*.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-244">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| `IncludeContentInPack` | <span data-ttu-id="4c5ad-245">Это логическое значение указывает, будут ли все элементы, имеющие тип, `Content` включаться в итоговый пакет автоматически.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-245">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="4c5ad-246">Значение по умолчанию — `true`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-246">The default is `true`.</span></span> |
| `BuildOutputTargetFolder` | <span data-ttu-id="4c5ad-247">Указывает папку для размещения выходных сборок.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-247">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="4c5ad-248">Выходные сборки (и другие выходные файлы) копируются в соответствующие папки платформы.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-248">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="4c5ad-249">Дополнительные сведения см. в разделе [выходные сборки](#output-assemblies).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-249">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| `ContentTargetFolders` | <span data-ttu-id="4c5ad-250">Указывает расположение по умолчанию, по которому должны указываться все файлы содержимого, если `PackagePath` для них не задано значение.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-250">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="4c5ad-251">Значение по умолчанию — "content;contentFiles".</span><span class="sxs-lookup"><span data-stu-id="4c5ad-251">The default value is "content;contentFiles".</span></span> <span data-ttu-id="4c5ad-252">Дополнительные сведения см. в статье [Включение содержимого в пакет](#including-content-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-252">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| `NuspecFile` | <span data-ttu-id="4c5ad-253">Относительный или абсолютный путь к *.nuspec* файлу, используемому для упаковки.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-253">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="4c5ad-254">Если он указан, он используется **исключительно** для сведений о упаковке, а любые сведения в проектах не используются.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-254">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="4c5ad-255">Дополнительные сведения см. [в .nuspec разделе Упаковка с помощью ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-255">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecBasePath` | <span data-ttu-id="4c5ad-256">Базовый путь к *.nuspec* файлу.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-256">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="4c5ad-257">Дополнительные сведения см. [в .nuspec разделе Упаковка с помощью ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-257">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecProperties` | <span data-ttu-id="4c5ad-258">Список разделенных точками с запятой пар "ключ-значение".</span><span class="sxs-lookup"><span data-stu-id="4c5ad-258">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="4c5ad-259">Дополнительные сведения см. [в .nuspec разделе Упаковка с помощью ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-259">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="4c5ad-260">Сценарии использования pack</span><span class="sxs-lookup"><span data-stu-id="4c5ad-260">pack scenarios</span></span>

### <a name="suppressing-dependencies"></a><span data-ttu-id="4c5ad-261">Подавление зависимостей</span><span class="sxs-lookup"><span data-stu-id="4c5ad-261">Suppressing dependencies</span></span>

<span data-ttu-id="4c5ad-262">Чтобы исключить зависимости пакета из созданного NuGet пакета, задайте для значение, `SuppressDependenciesWhenPacking` `true` которое позволит пропустить все зависимости из созданного файла nupkg.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-262">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### `PackageIconUrl`

<span data-ttu-id="4c5ad-263">`PackageIconUrl` является нерекомендуемым в пользу [`PackageIcon`](#packageicon) Свойства.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-263">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="4c5ad-264">Начиная с NuGet 5,3 и Visual Studio 2019 версии 16,3, `pack` создает предупреждение [NU5048](./errors-and-warnings/nu5048.md) , если только метаданные пакета указывают только `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-264">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### `PackageIcon`

> [!Tip]
> <span data-ttu-id="4c5ad-265">Чтобы обеспечить обратную совместимость с клиентами и источниками, которые еще не поддерживаются `PackageIcon` , укажите `PackageIcon` и `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-265">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="4c5ad-266">Visual Studio поддерживает `PackageIcon` пакеты, поступающие из источника, основанного на папках.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-266">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="4c5ad-267">Упаковка файла изображения значка</span><span class="sxs-lookup"><span data-stu-id="4c5ad-267">Packing an icon image file</span></span>

<span data-ttu-id="4c5ad-268">При упаковке файла изображения значка используйте `PackageIcon` свойство, чтобы указать путь к файлу значка относительно корня пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-268">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="4c5ad-269">Кроме того, убедитесь, что файл включен в пакет.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-269">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="4c5ad-270">Размер файла изображения ограничен 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-270">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="4c5ad-271">Поддерживаются следующие форматы файлов: JPEG и PNG.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-271">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="4c5ad-272">Рекомендуется разрешение изображения 128x128.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-272">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="4c5ad-273">Пример:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-273">For example:</span></span>

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

<span data-ttu-id="4c5ad-274">[Пример значка пакета](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-274">[Package Icon sample](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span></span>

<span data-ttu-id="4c5ad-275">Для получения nuspec эквивалента просмотрите [ nuspec ссылку на значок](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-275">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="packagereadmefile"></a><span data-ttu-id="4c5ad-276">паккажереадмефиле</span><span class="sxs-lookup"><span data-stu-id="4c5ad-276">PackageReadmeFile</span></span>

<span data-ttu-id="4c5ad-277">*Поддерживается с **NuGet 5.10.0 Preview 2**  /  **.NET 5.0.3** и более поздних версий*</span><span class="sxs-lookup"><span data-stu-id="4c5ad-277">*Supported with **NuGet 5.10.0 preview 2** / **.NET 5.0.3** and above*</span></span>

<span data-ttu-id="4c5ad-278">При упаковке файла сведений необходимо использовать `PackageReadmeFile` свойство, чтобы указать путь к пакету относительно корня пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-278">When packing a readme file, you need to use the `PackageReadmeFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="4c5ad-279">Помимо этого, необходимо убедиться, что файл включен в пакет.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-279">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="4c5ad-280">Поддерживаемые форматы файлов включают только Markdown (*. md*).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-280">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="4c5ad-281">Пример:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-281">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageReadmeFile>readme.md</PackageReadmeFile>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="docs\readme.md" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="4c5ad-282">Для получения nuspec эквивалента ознакомьтесь со ссылкой на [ nuspec файл readme](nuspec.md#readme).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-282">For the nuspec equivalent, take a look at [nuspec reference for readme](nuspec.md#readme).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="4c5ad-283">Выходные сборки</span><span class="sxs-lookup"><span data-stu-id="4c5ad-283">Output assemblies</span></span>

<span data-ttu-id="4c5ad-284">`nuget pack` копирует выходные файлы с расширениями `.exe`, `.dll`, `.xml`, `.winmd`, `.json` и `.pri`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-284">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="4c5ad-285">Копируемые выходные файлы зависят от того, что MSBuild предоставлено из `BuiltOutputProjectGroup` целевого объекта.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-285">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="4c5ad-286">Существует два MSBuild  свойства, которые можно использовать в файле проекта или командной строке для управления размещением выходных сборок:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-286">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="4c5ad-287">`IncludeBuildOutput`: логическое значение, определяющее, следует ли включать выходные сборки в пакете.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-287">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="4c5ad-288">`BuildOutputTargetFolder`: указывает папку, куда следует помещать выходные сборки.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-288">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="4c5ad-289">Выходные сборки (и другие выходные файлы) копируются в соответствующие папки платформы.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-289">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="4c5ad-290">Ссылки на пакеты</span><span class="sxs-lookup"><span data-stu-id="4c5ad-290">Package references</span></span>

<span data-ttu-id="4c5ad-291">См. раздел [Ссылки на пакеты в файлах проекта](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-291">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="4c5ad-292">Перекрестные ссылки между проектами</span><span class="sxs-lookup"><span data-stu-id="4c5ad-292">Project to project references</span></span>

<span data-ttu-id="4c5ad-293">Ссылки между проектами по умолчанию считаются NuGet ссылками на пакеты.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-293">Project to project references are considered by default as NuGet package references.</span></span> <span data-ttu-id="4c5ad-294">Пример:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-294">For example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="4c5ad-295">Вы также можете добавить в ссылку на проект следующие метаданные:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-295">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="4c5ad-296">Включение содержимого в пакет</span><span class="sxs-lookup"><span data-stu-id="4c5ad-296">Including content in a package</span></span>

<span data-ttu-id="4c5ad-297">Чтобы включить содержимое, добавьте дополнительные метаданные для существующего элемента `<Content>`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-297">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="4c5ad-298">По умолчанию все данные типа "Content" включаются в пакет, если только вы не переопределите такое поведение с помощью записей, аналогичных следующим:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-298">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="4c5ad-299">По умолчанию все данные добавляются в корень папки `content` и `contentFiles\any\<target_framework>` в пакете и сохраняют относительную структуру папок, если только не указан путь к пакету:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-299">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="4c5ad-300">Если нужно скопировать все содержимое только в определенные корневые папки (а не `content` и на `contentFiles` оба), можно использовать MSBuild свойство `ContentTargetFolders` , которое по умолчанию имеет значение "Content; contentFiles", но можно задать любые другие имена папок.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-300">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="4c5ad-301">Обратите внимание, если указать "contentFiles" в `ContentTargetFolders`, файлы помещаются в `contentFiles\any\<target_framework>` или `contentFiles\<language>\<target_framework>` в зависимости от `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-301">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="4c5ad-302">`PackagePath` может быть набором целевых путей, разделенных точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-302">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="4c5ad-303">Если указан пустой путь к пакету, файл добавляется в корневой каталог пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-303">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="4c5ad-304">Например, следующий код добавляет `libuv.txt` в `content\myfiles`, `content\samples` и корневой каталог пакета:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-304">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="4c5ad-305">Существует также MSBuild свойство `$(IncludeContentInPack)` , по умолчанию — `true` .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-305">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="4c5ad-306">Если оно имеет значение `false` для какого-либо проекта, то содержимое этого проекта не включается в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-306">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="4c5ad-307">Другие метаданные, относящиеся к пакету, которые можно задать для любого из перечисленных выше элементов, включают ```<PackageCopyToOutput>``` и ```<PackageFlatten>``` наборы ```CopyToOutput``` и ```Flatten``` значения для ```contentFiles``` записи в выходных данных nuspec .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-307">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="4c5ad-308">Кроме элементов содержимого, метаданные `<Pack>` и `<PackagePath>` также можно задать для файлов с действием сборки Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource или None.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-308">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="4c5ad-309">Чтобы объект pack добавил имя файла в путь к пакету при использовании стандартных масок, путь к пакету должен заканчиваться символом разделителя папок, в противном случае этот путь считается полным путем, включающим имя файла.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-309">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="4c5ad-310">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="4c5ad-310">IncludeSymbols</span></span>

<span data-ttu-id="4c5ad-311">При использовании `MSBuild -t:pack -p:IncludeSymbols=true` соответствующие файлы `.pdb` копируются вместе с другими выходными файлами (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-311">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="4c5ad-312">Обратите внимание, что при задании `IncludeSymbols=true` создается обычный пакет *и* пакет символов.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-312">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="4c5ad-313">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="4c5ad-313">IncludeSource</span></span>

<span data-ttu-id="4c5ad-314">Аналогично `IncludeSymbols`, только копирует исходные файлы вместе с файлами `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-314">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="4c5ad-315">Все файлы типа `Compile` копируются в `src\<ProjectName>\` с сохранением относительной структуры папок в итоговом пакете.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-315">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="4c5ad-316">То же самое происходит с исходными файлами любого `ProjectReference`, у которого `TreatAsPackageReference` имеет значение `false`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-316">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="4c5ad-317">Если файл типа Compile находится вне папки проекта, он просто добавляется в `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-317">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="4c5ad-318">Упаковка выражения лицензии или файла лицензии</span><span class="sxs-lookup"><span data-stu-id="4c5ad-318">Packing a license expression or a license file</span></span>

<span data-ttu-id="4c5ad-319">При использовании выражения лицензии используйте `PackageLicenseExpression` свойство.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-319">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="4c5ad-320">Пример см. в разделе [пример выражения лицензии](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-320">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="4c5ad-321">Дополнительные сведения о лицензионных выражениях и лицензиях, принятых NuGet . org, см. в разделе [метаданные лицензии](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-321">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="4c5ad-322">При упаковке файла лицензии используйте свойство, `PackageLicenseFile` чтобы указать путь к пакету относительно корня пакета.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-322">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="4c5ad-323">Кроме того, убедитесь, что файл включен в пакет.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-323">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="4c5ad-324">Пример:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-324">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="4c5ad-325">Пример см. в разделе [Пример файла лицензии](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-325">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="4c5ad-326">`PackageLicenseExpression`Одновременно можно указать только один из, `PackageLicenseFile` и `PackageLicenseUrl` .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-326">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="4c5ad-327">Упаковка файла без расширения</span><span class="sxs-lookup"><span data-stu-id="4c5ad-327">Packing a file without an extension</span></span>

<span data-ttu-id="4c5ad-328">В некоторых сценариях, например при упаковке файла лицензии, может потребоваться включить файл без расширения.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-328">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="4c5ad-329">По историческим причинам следует NuGet  &  MSBuild рассматривать пути без расширения в качестве каталогов.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-329">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="4c5ad-330">[Файл без примера расширения](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-330">[File without an extension sample](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span></span>

### <a name="istool"></a><span data-ttu-id="4c5ad-331">IsTool</span><span class="sxs-lookup"><span data-stu-id="4c5ad-331">IsTool</span></span>

<span data-ttu-id="4c5ad-332">При использовании `MSBuild -t:pack -p:IsTool=true` все выходные файлы, как указано в сценарии [Выходные сборки](#output-assemblies), копируются в папку `tools` вместо папки `lib`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-332">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="4c5ad-333">Обратите внимание, что это свойство отличается от `DotNetCliTool`, которое указывается путем задания `PackageType` в файле `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-333">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec-file"></a><span data-ttu-id="4c5ad-334">Упаковка с помощью `.nuspec` файла</span><span class="sxs-lookup"><span data-stu-id="4c5ad-334">Packing using a `.nuspec` file</span></span>

<span data-ttu-id="4c5ad-335">Хотя рекомендуется включить в файл проекта [все свойства](../reference/msbuild-targets.md#pack-target) , которые обычно находятся в файле `.nuspec` , можно использовать `.nuspec` файл для упаковки проекта.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-335">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="4c5ad-336">Для проекта в стиле, отличном от SDK, который использует `PackageReference` , необходимо импортировать, `NuGet.Build.Tasks.Pack.targets` чтобы можно было выполнить задачу «Pack».</span><span class="sxs-lookup"><span data-stu-id="4c5ad-336">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="4c5ad-337">Вам по-прежнему потребуется восстановить проект, прежде чем можно будет упаковать nuspec файл.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-337">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="4c5ad-338">(Проект в стиле SDK включает целевые объекты Pack по умолчанию.)</span><span class="sxs-lookup"><span data-stu-id="4c5ad-338">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="4c5ad-339">Целевая платформа файла проекта несущественна и не используется при упаковке a nuspec .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-339">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="4c5ad-340">Следующие три MSBuild свойства важны для упаковки с помощью `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="4c5ad-340">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="4c5ad-341">`NuspecFile`: относительный или абсолютный путь к файлу `.nuspec`, используемому для упаковки.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-341">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="4c5ad-342">`NuspecProperties`: список разделенных точками с запятой пар "ключ-значение".</span><span class="sxs-lookup"><span data-stu-id="4c5ad-342">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="4c5ad-343">Из-за того MSBuild , как работает синтаксический анализ из командной строки, необходимо указать несколько свойств следующим образом: `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-343">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="4c5ad-344">`NuspecBasePath`: базовый путь для файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-344">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="4c5ad-345">Если вы используете `dotnet.exe` для упаковки проекта, воспользуйтесь командой, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-345">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="4c5ad-346">Если вы используете MSBuild для упаковки проекта, воспользуйтесь командой, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-346">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="4c5ad-347">Обратите внимание, что упаковка a nuspec с помощью dotnet.exe или MSBuild также ведет к построению проекта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-347">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="4c5ad-348">Это можно избежать, передав ```--no-build``` свойство в dotnet.exe, которое является аналогом параметра ```<NoBuild>true</NoBuild> ``` в файле проекта, а также параметром ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-348">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="4c5ad-349">Пример файла *. csproj* для упаковки nuspec файла:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-349">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="4c5ad-350">Улучшенные точки расширения для создания настраиваемого пакета</span><span class="sxs-lookup"><span data-stu-id="4c5ad-350">Advanced extension points to create customized package</span></span>

<span data-ttu-id="4c5ad-351">`pack`Целевой объект предоставляет две точки расширения, которые выполняются во внутренней и целевой сборке конкретной платформы.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-351">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="4c5ad-352">Поддержка точек расширения включает в пакет содержимое и сборки, относящиеся к целевой платформе.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-352">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="4c5ad-353">`TargetsForTfmSpecificBuildOutput` target: используйте для файлов в `lib` папке или в папке, указанной с помощью `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-353">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="4c5ad-354">`TargetsForTfmSpecificContentInPackage` target: используйте для файлов за пределами `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-354">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### `TargetsForTfmSpecificBuildOutput`

<span data-ttu-id="4c5ad-355">Напишите настраиваемый целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificBuildOutput)` Свойства.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-355">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="4c5ad-356">Для файлов, которые необходимо переключать в `BuildOutputTargetFolder` (LIB по умолчанию), целевой объект должен записать эти файлы в ItemGroup `BuildOutputInPackage` и задать следующие два значения метаданных:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-356">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="4c5ad-357">`FinalOutputPath`: Абсолютный путь к файлу; Если этот параметр не указан, для вычисления исходного пути используется удостоверение.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-357">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="4c5ad-358">`TargetPath`: (Необязательно) задайте, когда файл необходимо переключиться во вложенную папку в `lib\<TargetFramework>` , например вспомогательные сборки, которые находятся в соответствующих папках языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-358">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="4c5ad-359">По умолчанию используется имя файла.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-359">Defaults to the name of the file.</span></span>

<span data-ttu-id="4c5ad-360">Пример:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-360">Example:</span></span>

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

#### `TargetsForTfmSpecificContentInPackage`

<span data-ttu-id="4c5ad-361">Напишите настраиваемый целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificContentInPackage)` Свойства.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-361">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="4c5ad-362">Для всех файлов, включаемых в пакет, целевой объект должен записать эти файлы в ItemGroup `TfmSpecificPackageFile` и задать следующие необязательные метаданные:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-362">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="4c5ad-363">`PackagePath`: Путь, по которому файл должен быть выведен в пакете.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-363">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="4c5ad-364">NuGet выдает предупреждение, если в один и тот же путь к пакету добавляется несколько файлов.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-364">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="4c5ad-365">`BuildAction`: Действие сборки, присваиваемое файлу, требуется только в том случае, если путь к пакету находится в `contentFiles` папке.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-365">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="4c5ad-366">По умолчанию используется значение "нет".</span><span class="sxs-lookup"><span data-stu-id="4c5ad-366">Defaults to "None".</span></span>

<span data-ttu-id="4c5ad-367">Пример:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-367">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="4c5ad-368">Целевой объект restore</span><span class="sxs-lookup"><span data-stu-id="4c5ad-368">restore target</span></span>

<span data-ttu-id="4c5ad-369">`MSBuild -t:restore` (который `nuget restore` и `dotnet restore` используют с проектами .NET Core) восстанавливает пакеты, на которые ссылается файл проекта:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-369">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="4c5ad-370">Чтение перекрестных ссылок между проектами.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-370">Read all project to project references</span></span>
1. <span data-ttu-id="4c5ad-371">Чтение свойств проекта, чтобы найти промежуточную папку и целевые платформы.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-371">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="4c5ad-372">Передача MSBuild данных в NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="4c5ad-372">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="4c5ad-373">Запуск восстановления.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-373">Run restore</span></span>
1. <span data-ttu-id="4c5ad-374">Скачивание пакетов</span><span class="sxs-lookup"><span data-stu-id="4c5ad-374">Download packages</span></span>
1. <span data-ttu-id="4c5ad-375">Запись файла ресурсов, целевых объектов и свойств.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-375">Write assets file, targets, and props</span></span>

<span data-ttu-id="4c5ad-376">`restore`Целевой объект работает для проектов, использующих формат PackageReference.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-376">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="4c5ad-377">`MSBuild 16.5+` также имеет [поддержку согласия](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) для `packages.config` формата.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-377">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="4c5ad-378">`restore`Целевой объект [не должен выполняться](#restoring-and-building-with-one-msbuild-command) в сочетании с целевым объектом `build` .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-378">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="4c5ad-379">Свойства восстановления</span><span class="sxs-lookup"><span data-stu-id="4c5ad-379">Restore properties</span></span>

<span data-ttu-id="4c5ad-380">Дополнительные параметры восстановления могут поступать из MSBuild свойств в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-380">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="4c5ad-381">Значения также можно задать из командной строки с помощью параметра `-p:` (см. примеры ниже).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-381">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="4c5ad-382">Свойство</span><span class="sxs-lookup"><span data-stu-id="4c5ad-382">Property</span></span> | <span data-ttu-id="4c5ad-383">Описание</span><span class="sxs-lookup"><span data-stu-id="4c5ad-383">Description</span></span> |
|--------|--------|
| `RestoreSources` | <span data-ttu-id="4c5ad-384">Разделенный точками с запятой список источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-384">Semicolon-delimited list of package sources.</span></span> |
| `RestorePackagesPath` | <span data-ttu-id="4c5ad-385">Путь к папке пакетов пользователя.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-385">User packages folder path.</span></span> |
| `RestoreDisableParallel` | <span data-ttu-id="4c5ad-386">Ограничение скачиваний до одного за раз.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-386">Limit downloads to one at a time.</span></span> |
| `RestoreConfigFile` | <span data-ttu-id="4c5ad-387">Путь к применяемому файлу `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-387">Path to a `Nuget.Config` file to apply.</span></span> |
| `RestoreNoCache` | <span data-ttu-id="4c5ad-388">Значение true позволяет избежать использования кэшированных пакетов.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-388">If true, avoids using cached packages.</span></span> <span data-ttu-id="4c5ad-389">См. раздел [Управление глобальными пакетами и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-389">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| `RestoreIgnoreFailedSources` | <span data-ttu-id="4c5ad-390">Если значение равно true, нерабочие или отсутствующие источники пакетов игнорируются.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-390">If true, ignores failing or missing package sources.</span></span> |
| `RestoreFallbackFolders` | <span data-ttu-id="4c5ad-391">Резервные папки используются так же, как и папка User Packages.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-391">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| `RestoreAdditionalProjectSources` | <span data-ttu-id="4c5ad-392">Дополнительные источники, используемые во время восстановления.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-392">Additional sources to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFolders` | <span data-ttu-id="4c5ad-393">Дополнительные резервные папки для использования во время восстановления.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-393">Additional fallback folders to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | <span data-ttu-id="4c5ad-394">Исключает резервные папки, указанные в `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="4c5ad-394">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| `RestoreTaskAssemblyFile` | <span data-ttu-id="4c5ad-395">Путь к `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-395">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| `RestoreGraphProjectInput` | <span data-ttu-id="4c5ad-396">Разделенный точками с запятой список проектов для восстановления, который должен содержать абсолютные пути.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-396">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| `RestoreUseSkipNonexistentTargets`  | <span data-ttu-id="4c5ad-397">При сборе проекта с помощью MSBuild он определяет, будут ли они собраны с использованием `SkipNonexistentTargets` оптимизации.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-397">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="4c5ad-398">Если значение не задано, по умолчанию используется значение `true` .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-398">When not set, defaults to `true`.</span></span> <span data-ttu-id="4c5ad-399">Следствием является быстрое поведение при сбое, если целевые объекты проекта не могут быть импортированы.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-399">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| `MSBuildProjectExtensionsPath` | <span data-ttu-id="4c5ad-400">Папка Output, по умолчанию — `BaseIntermediateOutputPath` и `obj` Папка.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-400">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| `RestoreForce` | <span data-ttu-id="4c5ad-401">В проектах на основе PackageReference принудительно разрешаются все зависимости, даже если последнее восстановление прошло успешно.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-401">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="4c5ad-402">Установка этого флага аналогична удалению `project.assets.json` файла.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-402">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="4c5ad-403">Это не позволяет обходить HTTP-кэш.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-403">This does not bypass the http-cache.</span></span> |
| `RestorePackagesWithLockFile` | <span data-ttu-id="4c5ad-404">Разрешение использовать файл блокировки.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-404">Opts into the usage of a lock file.</span></span> |
| `RestoreLockedMode` | <span data-ttu-id="4c5ad-405">Запустите восстановление в заблокированном режиме.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-405">Run restore in locked mode.</span></span> <span data-ttu-id="4c5ad-406">Это означает, что восстановление не будет переоценивать зависимости.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-406">This means that restore will not reevaluate the dependencies.</span></span> |
| `NuGetLockFilePath` | <span data-ttu-id="4c5ad-407">Пользовательское расположение файла блокировки.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-407">A custom location for the lock file.</span></span> <span data-ttu-id="4c5ad-408">Расположение по умолчанию находится рядом с проектом и имеет имя `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-408">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| `RestoreForceEvaluate` | <span data-ttu-id="4c5ad-409">Принудительное восстановление для повторного расчета зависимостей и обновление файла блокировки без предупреждения.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-409">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| `RestorePackagesConfig` | <span data-ttu-id="4c5ad-410">Параметр согласия, который восстанавливает проекты с packages.config. Поддерживается `MSBuild -t:restore` только с.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-410">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| `RestoreUseStaticGraphEvaluation` | <span data-ttu-id="4c5ad-411">Параметр выбора для использования статической оценки графа MSBuild вместо стандартного вычисления.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-411">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="4c5ad-412">Статическая Оценка графа — это экспериментальная функция, которая значительно ускоряется для больших репозиториев и решений.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-412">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="4c5ad-413">Примеры</span><span class="sxs-lookup"><span data-stu-id="4c5ad-413">Examples</span></span>

<span data-ttu-id="4c5ad-414">Командная строка:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-414">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="4c5ad-415">Файл проекта:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-415">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="4c5ad-416">Выходные данные восстановления</span><span class="sxs-lookup"><span data-stu-id="4c5ad-416">Restore outputs</span></span>

<span data-ttu-id="4c5ad-417">Операция восстановления создает в папке сборки `obj` следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-417">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="4c5ad-418">Файл</span><span class="sxs-lookup"><span data-stu-id="4c5ad-418">File</span></span> | <span data-ttu-id="4c5ad-419">Описание</span><span class="sxs-lookup"><span data-stu-id="4c5ad-419">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="4c5ad-420">Содержит диаграмму зависимостей всех ссылок на пакеты.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-420">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="4c5ad-421">Ссылки на свойства MSBuild Props, содержащиеся в пакетах</span><span class="sxs-lookup"><span data-stu-id="4c5ad-421">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="4c5ad-422">Ссылки на MSBuild целевые объекты, содержащиеся в пакетах</span><span class="sxs-lookup"><span data-stu-id="4c5ad-422">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="4c5ad-423">Восстановление и сборка с помощью одной MSBuild команды</span><span class="sxs-lookup"><span data-stu-id="4c5ad-423">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="4c5ad-424">Из-за того факта, что NuGet можно восстановить пакеты, которые предоставляют MSBuild целевые объекты и свойства, оценки восстановления и сборки выполняются с разными глобальными свойствами.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-424">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="4c5ad-425">Это означает, что следующие действия будут иметь непредсказуемое и неправильное поведение.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-425">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="4c5ad-426">Вместо этого рекомендуемый подход:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-426">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="4c5ad-427">Одна и та же логика применяется к другим целевым объектам, аналогичным `build` .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-427">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a><span data-ttu-id="4c5ad-428">Восстановление проектов PackageReference и packages.config с помощью MSBuild</span><span class="sxs-lookup"><span data-stu-id="4c5ad-428">Restoring PackageReference and packages.config projects with MSBuild</span></span>

<span data-ttu-id="4c5ad-429">При использовании MSBuild 16.5 + packages.config также поддерживаются для `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-429">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="4c5ad-430">`packages.config` Restore доступен только в `MSBuild 16.5+` , а не в `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="4c5ad-430">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="4c5ad-431">Восстановление с помощью MSBuild статической оценки графа</span><span class="sxs-lookup"><span data-stu-id="4c5ad-431">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="4c5ad-432">В MSBuild 16.6 + NuGet Добавлена экспериментальная функция для использования статической оценки графа из командной строки, значительно повышающей время восстановления больших репозиториев.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-432">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="4c5ad-433">Кроме того, его можно включить, задав свойство в каталоге. Build. props.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-433">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="4c5ad-434">Начиная с Visual Studio 2019. x и NuGet 5. x, эта функция считается экспериментальной и явной.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-434">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="4c5ad-435">Чтобы получить подробные сведения о том, когда эта функция будет включена по умолчанию, следуйте указаниям в [ NuGet /Home # 9803](https://github.com/NuGet/Home/issues/9803) .</span><span class="sxs-lookup"><span data-stu-id="4c5ad-435">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="4c5ad-436">При восстановлении статического графа изменяется часть MSBuild, вычисление и чтение проекта, но не алгоритм восстановления.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-436">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="4c5ad-437">Алгоритм восстановления одинаков для всех NuGet средств ( NuGet exe, MSBuild exe, dotnet.exe и Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-437">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="4c5ad-438">В очень редких случаях восстановление статических графов может отличаться от текущего при восстановлении, а некоторые объявленные PackageReferences или ссылками могут отсутствовать.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-438">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="4c5ad-439">Для упрощения проверки при переходе к статическому восстановлению графа можно выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-439">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="4c5ad-440">NuGet*не* должны сообщать об изменениях.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-440">NuGet should *not* report any changes.</span></span> <span data-ttu-id="4c5ad-441">Если вы видите несоответствие, напишите вопрос по адресу [ NuGet /Home](https://github.com/nuget/home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="4c5ad-441">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="4c5ad-442">Замена одной библиотеки из графа восстановления</span><span class="sxs-lookup"><span data-stu-id="4c5ad-442">Replacing one library from a restore graph</span></span>

<span data-ttu-id="4c5ad-443">Если операция восстановления предоставляет неправильную сборку, вы можете исключить значение по умолчанию для этого пакета, заменив его своим значением.</span><span class="sxs-lookup"><span data-stu-id="4c5ad-443">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="4c5ad-444">Первый с `PackageReference` верхнего уровня, исключите все ресурсы:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-444">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="4c5ad-445">После этого добавьте собственную ссылку на соответствующую локальную копию библиотеки DLL:</span><span class="sxs-lookup"><span data-stu-id="4c5ad-445">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```