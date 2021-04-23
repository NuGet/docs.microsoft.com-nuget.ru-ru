---
title: Ссылка на файл. nuspec для NuGet
description: Файл с расширением .nuspec содержит метаданные пакета, которые используются при построении пакета и предоставляют дополнительную информацию для его потребителей.
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: ed865aad6f72752adcf3e3921287a20b961c4a8a
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901815"
---
# <a name="nuspec-reference"></a><span data-ttu-id="c6470-103">Справочник по файлу NUSPEC</span><span class="sxs-lookup"><span data-stu-id="c6470-103">.nuspec reference</span></span>

<span data-ttu-id="c6470-104">Файл `.nuspec` представляет собой манифест в формате XML и содержит метаданные пакета.</span><span class="sxs-lookup"><span data-stu-id="c6470-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="c6470-105">Этот манифест используется при построении пакета и содержит дополнительные сведения для его потребителей.</span><span class="sxs-lookup"><span data-stu-id="c6470-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="c6470-106">Манифест всегда включается в пакет.</span><span class="sxs-lookup"><span data-stu-id="c6470-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="c6470-107">В этом разделе.</span><span class="sxs-lookup"><span data-stu-id="c6470-107">In this topic:</span></span>

- [<span data-ttu-id="c6470-108">Общая форма и схема</span><span class="sxs-lookup"><span data-stu-id="c6470-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="c6470-109">[Замена маркеров](#replacement-tokens) (при использовании с проектом Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="c6470-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="c6470-110">Зависимости</span><span class="sxs-lookup"><span data-stu-id="c6470-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="c6470-111">Явные ссылки на сборку</span><span class="sxs-lookup"><span data-stu-id="c6470-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="c6470-112">Ссылки на сборку платформы</span><span class="sxs-lookup"><span data-stu-id="c6470-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="c6470-113">Включение файлов сборки</span><span class="sxs-lookup"><span data-stu-id="c6470-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="c6470-114">Включение файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="c6470-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="c6470-115">Пример файлов nuspec</span><span class="sxs-lookup"><span data-stu-id="c6470-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="c6470-116">Совместимость типов проектов</span><span class="sxs-lookup"><span data-stu-id="c6470-116">Project type compatibility</span></span>

- <span data-ttu-id="c6470-117">Используйте `.nuspec` с `nuget.exe pack` для проектов в стиле, не являющихся SDK, которые используют `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="c6470-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="c6470-118">`.nuspec`Файл не требуется для создания пакетов для проектов в [стиле SDK](../resources/check-project-format.md) (обычно это проекты .net Core и .NET Standard, использующие [атрибут SDK](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="c6470-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="c6470-119">(Обратите внимание, что `.nuspec` создается при создании пакета.)</span><span class="sxs-lookup"><span data-stu-id="c6470-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="c6470-120">При создании пакета с помощью `dotnet.exe pack` или `msbuild pack target` рекомендуется включить в файл проекта [все свойства](../reference/msbuild-targets.md#pack-target) , которые обычно находятся в `.nuspec` файле.</span><span class="sxs-lookup"><span data-stu-id="c6470-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="c6470-121">Однако вместо этого можно [использовать `.nuspec` файл для упаковки с помощью `dotnet.exe` или `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="c6470-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec-file).</span></span>

- <span data-ttu-id="c6470-122">Для проектов, перенесенных из `packages.config` в [PackageReference](../consume-packages/package-references-in-project-files.md), `.nuspec` для создания пакета не требуется файл.</span><span class="sxs-lookup"><span data-stu-id="c6470-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="c6470-123">Вместо этого используйте [MSBuild-т:ПАКК](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="c6470-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="c6470-124">Общая форма и схема</span><span class="sxs-lookup"><span data-stu-id="c6470-124">General form and schema</span></span>

<span data-ttu-id="c6470-125">Текущий файл схемы `nuspec.xsd` представлен в [репозитории GitHub для NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="c6470-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="c6470-126">В рамках этой схемы файл `.nuspec` имеет следующую общую форму:</span><span class="sxs-lookup"><span data-stu-id="c6470-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

<span data-ttu-id="c6470-127">Чтобы получить наглядное представление схемы, откройте файл в режиме конструктора Visual Studio и щелкните ссылку **Обозреватель схемы XML**.</span><span class="sxs-lookup"><span data-stu-id="c6470-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="c6470-128">Также можно открыть этот файл в виде кода. Для этого щелкните правой кнопкой мыши в редакторе и выберите команду **Показать в обозревателе схемы XML**.</span><span class="sxs-lookup"><span data-stu-id="c6470-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="c6470-129">В любом случае при развертывании большинства узлов схема будет иметь примерно следующий вид:</span><span class="sxs-lookup"><span data-stu-id="c6470-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Обозреватель схемы Visual Studio с открытым файлом nuspec.xsd](media/SchemaExplorer.png)

<span data-ttu-id="c6470-131">Все имена XML-элементов в nuspec-файле чувствительны к регистру, как и в случае с XML в целом.</span><span class="sxs-lookup"><span data-stu-id="c6470-131">All XML element names in the .nuspec file are case-sensitive, as is the case for XML in general.</span></span> <span data-ttu-id="c6470-132">Например, использование элемента metadata `<description>` является правильным и `<Description>` неправильным.</span><span class="sxs-lookup"><span data-stu-id="c6470-132">For example, using the metadata element `<description>` is correct and `<Description>` is not correct.</span></span> <span data-ttu-id="c6470-133">Ниже описан правильный регистр для каждого имени элемента.</span><span class="sxs-lookup"><span data-stu-id="c6470-133">The proper casing for each element name is documented below.</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="c6470-134">Обязательные элементы метаданных</span><span class="sxs-lookup"><span data-stu-id="c6470-134">Required metadata elements</span></span>

<span data-ttu-id="c6470-135">Следующие элементы являются минимальным требованием для пакета, однако, несмотря на это, рекомендуется добавить [дополнительные элементы метаданных](#optional-metadata-elements), чтобы оптимизировать работу с вашим пакетом для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="c6470-135">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="c6470-136">Эти элементы должны использоваться внутри элемента `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="c6470-136">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="c6470-137">идентификатор</span><span class="sxs-lookup"><span data-stu-id="c6470-137">id</span></span> 
<span data-ttu-id="c6470-138">Идентификатор пакета без учета регистра, который должен быть уникальным в пределах сайта nuget.org или иной коллекции, в которой находится пакет.</span><span class="sxs-lookup"><span data-stu-id="c6470-138">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="c6470-139">Идентификаторы не должны содержать пробелов или символов, которые недопустимы в URL-адресах, и в них должны соблюдаться общие правила касательно пространств имен .NET.</span><span class="sxs-lookup"><span data-stu-id="c6470-139">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="c6470-140">Инструкции см. в разделе [Выбор уникального идентификатора пакета](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="c6470-140">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>

<span data-ttu-id="c6470-141">При отправке пакета в nuget.org `id` поле ограничено 128 символами.</span><span class="sxs-lookup"><span data-stu-id="c6470-141">When uploading a package to nuget.org, the `id` field is limited to 128 characters.</span></span>

#### <a name="version"></a><span data-ttu-id="c6470-142">version</span><span class="sxs-lookup"><span data-stu-id="c6470-142">version</span></span>
<span data-ttu-id="c6470-143">Версия пакета, указываемая согласно шаблону *основной_номер.дополнительный_номер.исправление*.</span><span class="sxs-lookup"><span data-stu-id="c6470-143">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="c6470-144">Номер версии может включать в себя суффикс предварительной версии, как описано в разделе [Управление версиями пакета](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="c6470-144">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 

<span data-ttu-id="c6470-145">При отправке пакета в nuget.org `version` поле ограничено 64 символами.</span><span class="sxs-lookup"><span data-stu-id="c6470-145">When uploading a package to nuget.org, the `version` field is limited to 64 characters.</span></span>

#### <a name="description"></a><span data-ttu-id="c6470-146">description</span><span class="sxs-lookup"><span data-stu-id="c6470-146">description</span></span>
<span data-ttu-id="c6470-147">Описание пакета для вывода пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c6470-147">A description of the package for UI display.</span></span>

<span data-ttu-id="c6470-148">При отправке пакета в nuget.org `description` поле ограничено 4000 символами.</span><span class="sxs-lookup"><span data-stu-id="c6470-148">When uploading a package to nuget.org, the `description` field is limited to 4000 characters.</span></span>

#### <a name="authors"></a><span data-ttu-id="c6470-149">authors</span><span class="sxs-lookup"><span data-stu-id="c6470-149">authors</span></span>
<span data-ttu-id="c6470-150">Разделенный запятыми список авторов пакетов, соответствующих именам профилей в nuget.org. Они отображаются в коллекции NuGet в nuget.org и используются для перекрестных ссылок на пакеты с теми же авторами.</span><span class="sxs-lookup"><span data-stu-id="c6470-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

<span data-ttu-id="c6470-151">При отправке пакета в nuget.org `authors` поле ограничено 4000 символами.</span><span class="sxs-lookup"><span data-stu-id="c6470-151">When uploading a package to nuget.org, the `authors` field is limited to 4000 characters.</span></span>

### <a name="optional-metadata-elements"></a><span data-ttu-id="c6470-152">Необязательные элементы метаданных</span><span class="sxs-lookup"><span data-stu-id="c6470-152">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="c6470-153">owners</span><span class="sxs-lookup"><span data-stu-id="c6470-153">owners</span></span>
> [!Important]
> <span data-ttu-id="c6470-154">владельцы являются устаревшими.</span><span class="sxs-lookup"><span data-stu-id="c6470-154">owners is deprecated.</span></span> <span data-ttu-id="c6470-155">Вместо этого используйте авторов.</span><span class="sxs-lookup"><span data-stu-id="c6470-155">Use authors instead.</span></span>

<span data-ttu-id="c6470-156">Разделенный запятыми список авторов пакетов, использующих имена профилей в nuget.org. Часто это тот же список, что `authors` и в, и игнорируется при отправке пакета в NuGet.org. См. раздел [Управление владельцами пакетов в NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="c6470-156">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="c6470-157">projectUrl</span><span class="sxs-lookup"><span data-stu-id="c6470-157">projectUrl</span></span>
<span data-ttu-id="c6470-158">URL-адрес для домашней страницы пакета, часто указываемый при отображении пользовательского интерфейса, также как и nuget.org.</span><span class="sxs-lookup"><span data-stu-id="c6470-158">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

<span data-ttu-id="c6470-159">При отправке пакета в nuget.org `projectUrl` поле ограничено 4000 символами.</span><span class="sxs-lookup"><span data-stu-id="c6470-159">When uploading a package to nuget.org, the `projectUrl` field is limited to 4000 characters.</span></span>

#### <a name="licenseurl"></a><span data-ttu-id="c6470-160">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="c6470-160">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="c6470-161">licenseUrl является устаревшим.</span><span class="sxs-lookup"><span data-stu-id="c6470-161">licenseUrl is deprecated.</span></span> <span data-ttu-id="c6470-162">Используйте вместо этого лицензию.</span><span class="sxs-lookup"><span data-stu-id="c6470-162">Use license instead.</span></span>

<span data-ttu-id="c6470-163">URL-адрес для лицензии пакета, часто показанный в пользовательских интерфейсах, таких как nuget.org.</span><span class="sxs-lookup"><span data-stu-id="c6470-163">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

<span data-ttu-id="c6470-164">При отправке пакета в nuget.org `licenseUrl` поле ограничено 4000 символами.</span><span class="sxs-lookup"><span data-stu-id="c6470-164">When uploading a package to nuget.org, the `licenseUrl` field is limited to 4000 characters.</span></span>

#### <a name="license"></a><span data-ttu-id="c6470-165">license</span><span class="sxs-lookup"><span data-stu-id="c6470-165">license</span></span>

<span data-ttu-id="c6470-166">*Поддерживается для **NuGet 4.9.0** и более поздних версий*</span><span class="sxs-lookup"><span data-stu-id="c6470-166">*Supported with **NuGet 4.9.0** and above*</span></span>

<span data-ttu-id="c6470-167">Выражение лицензии СПДКС или путь к файлу лицензии в пакете, который часто отображается в пользовательских интерфейсах, например nuget.org. Если вы намерены лицензирование пакета с помощью обычной лицензии, например MIT или BSD-2-предложения, используйте соответствующий [идентификатор лицензии спдкс](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="c6470-167">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="c6470-168">Пример:</span><span class="sxs-lookup"><span data-stu-id="c6470-168">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="c6470-169">NuGet.org принимает только те лицензионные выражения, которые утверждены инициативой Open Source или Free Software Foundation.</span><span class="sxs-lookup"><span data-stu-id="c6470-169">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="c6470-170">Если пакет лицензирован в нескольких распространенных лицензиях, можно указать составную лицензию с помощью [синтаксиса выражений спдкс версии 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="c6470-170">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="c6470-171">Пример:</span><span class="sxs-lookup"><span data-stu-id="c6470-171">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="c6470-172">При использовании пользовательской лицензии, которая не поддерживается в выражениях лицензий, можно упаковать `.txt` `.md` файл или с текстом лицензии.</span><span class="sxs-lookup"><span data-stu-id="c6470-172">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="c6470-173">Пример:</span><span class="sxs-lookup"><span data-stu-id="c6470-173">For example:</span></span>

```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

<span data-ttu-id="c6470-174">Для эквивалента MSBuild ознакомьтесь с [упаковкой лицензионного выражения или файла лицензии](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="c6470-174">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="c6470-175">Точный синтаксис выражений лицензии NuGet описывается ниже в [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="c6470-175">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>

```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a><span data-ttu-id="c6470-176">iconUrl</span><span class="sxs-lookup"><span data-stu-id="c6470-176">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="c6470-177">Иконурл является устаревшим.</span><span class="sxs-lookup"><span data-stu-id="c6470-177">iconUrl is deprecated.</span></span> <span data-ttu-id="c6470-178">Вместо этого используйте значок.</span><span class="sxs-lookup"><span data-stu-id="c6470-178">Use icon instead.</span></span>

<span data-ttu-id="c6470-179">URL-адрес для изображения 128x128 с фоном прозрачности для использования в качестве значка для пакета в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="c6470-179">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="c6470-180">Убедитесь, что этот элемент содержит *прямой URL-адрес изображения*, а не URL-адрес веб-страницы, на которой содержится изображение.</span><span class="sxs-lookup"><span data-stu-id="c6470-180">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="c6470-181">Например, чтобы использовать изображение из GitHub, используйте URL-адрес необработанного файла, например <em> https://github.com/ \<username\> / \<repository\> /рав/ \<branch\> / \<logo.png\> </em>.</span><span class="sxs-lookup"><span data-stu-id="c6470-181">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

<span data-ttu-id="c6470-182">При отправке пакета в nuget.org `iconUrl` поле ограничено 4000 символами.</span><span class="sxs-lookup"><span data-stu-id="c6470-182">When uploading a package to nuget.org, the `iconUrl` field is limited to 4000 characters.</span></span>

#### <a name="icon"></a><span data-ttu-id="c6470-183">icon</span><span class="sxs-lookup"><span data-stu-id="c6470-183">icon</span></span>

<span data-ttu-id="c6470-184">*Поддерживается для **NuGet 5.3.0** и более поздних версий*</span><span class="sxs-lookup"><span data-stu-id="c6470-184">*Supported with **NuGet 5.3.0** and above*</span></span>

<span data-ttu-id="c6470-185">Это путь к файлу изображения в пакете, который часто отображается в пользовательских интерфейсах, таких как nuget.org, как значок пакета.</span><span class="sxs-lookup"><span data-stu-id="c6470-185">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="c6470-186">Размер файла изображения ограничен 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="c6470-186">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="c6470-187">Поддерживаются следующие форматы файлов: JPEG и PNG.</span><span class="sxs-lookup"><span data-stu-id="c6470-187">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="c6470-188">Рекомендуется разрешение изображения 128x128.</span><span class="sxs-lookup"><span data-stu-id="c6470-188">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="c6470-189">Например, при создании пакета с помощью nuget.exe необходимо добавить следующий объект в nuspec:</span><span class="sxs-lookup"><span data-stu-id="c6470-189">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

```xml
<package>
  <metadata>
    ...
    <icon>images\icon.png</icon>
    ...
  </metadata>
  <files>
    ...
    <file src="..\icon.png" target="images\" />
    ...
  </files>
</package>
```

[<span data-ttu-id="c6470-190">Значок пакета nuspec Sample.</span><span class="sxs-lookup"><span data-stu-id="c6470-190">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/main/PackageIconNuspecExample)

<span data-ttu-id="c6470-191">Чтобы получить эквивалент MSBuild, Взгляните на [упаковку файла изображения значка](msbuild-targets.md#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="c6470-191">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="c6470-192">Можно указать `icon` и, и `iconUrl` для обеспечения обратной совместимости с источниками, которые не поддерживаются `icon` .</span><span class="sxs-lookup"><span data-stu-id="c6470-192">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="c6470-193">Visual Studio будет поддерживать `icon` пакеты, поступающие из источника на основе папок в будущем выпуске.</span><span class="sxs-lookup"><span data-stu-id="c6470-193">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="readme"></a><span data-ttu-id="c6470-194">Файл сведений</span><span class="sxs-lookup"><span data-stu-id="c6470-194">readme</span></span>

<span data-ttu-id="c6470-195">*Поддерживается с **NuGet 5.10.0 Preview 2** и более поздних версий*</span><span class="sxs-lookup"><span data-stu-id="c6470-195">*Supported with **NuGet 5.10.0 preview 2** and above*</span></span>

<span data-ttu-id="c6470-196">При упаковке файла сведений необходимо использовать `readme` элемент, чтобы указать путь к пакету относительно корня пакета.</span><span class="sxs-lookup"><span data-stu-id="c6470-196">When packing a readme file, you need to use the `readme` element to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="c6470-197">Помимо этого, необходимо убедиться, что файл включен в пакет.</span><span class="sxs-lookup"><span data-stu-id="c6470-197">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="c6470-198">Поддерживаемые форматы файлов включают только Markdown (*. md*).</span><span class="sxs-lookup"><span data-stu-id="c6470-198">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="c6470-199">Например, добавьте следующий объект в nuspec, чтобы упаковать файл сведений в свой проект:</span><span class="sxs-lookup"><span data-stu-id="c6470-199">For example, you would add the following to your nuspec in order to pack a readme file with your project:</span></span>

```xml
<package>
  <metadata>
    ...
    <readme>docs\readme.md</readme>
    ...
  </metadata>
  <files>
    ...
    <file src="..\readme.md" target="docs\" />
    ...
  </files>
</package>
```

<span data-ttu-id="c6470-200">Для эквивалента MSBuild ознакомьтесь с [упаковкой файла сведений](msbuild-targets.md#packagereadmefile).</span><span class="sxs-lookup"><span data-stu-id="c6470-200">For the MSBuild equivalent, take a look at [Packing a readme file](msbuild-targets.md#packagereadmefile).</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="c6470-201">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="c6470-201">requireLicenseAcceptance</span></span>
<span data-ttu-id="c6470-202">Логическое значение, указывающее, должен ли клиент просить потребителя принять условия лицензии перед установкой пакета.</span><span class="sxs-lookup"><span data-stu-id="c6470-202">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="c6470-203">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="c6470-203">developmentDependency</span></span>
<span data-ttu-id="c6470-204">*(Версия 2.8 и более поздние)* Логическое значение, указывающее, помечен ли пакет как зависимость только для разработки, что позволяет запретить его включение в качестве зависимости в другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="c6470-204">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="c6470-205">При использовании PackageReference (NuGet 4.8+) этот флажок также указывает на исключение ресурсов времени компиляции из компиляции.</span><span class="sxs-lookup"><span data-stu-id="c6470-205">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="c6470-206">См. раздел [Поддержка DevelopmentDependency для PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) .</span><span class="sxs-lookup"><span data-stu-id="c6470-206">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="c6470-207">Итоги</span><span class="sxs-lookup"><span data-stu-id="c6470-207">summary</span></span>
> [!Important]
> <span data-ttu-id="c6470-208">`summary` является устаревшим.</span><span class="sxs-lookup"><span data-stu-id="c6470-208">`summary` is being deprecated.</span></span> <span data-ttu-id="c6470-209">Используйте вместо этого `description`.</span><span class="sxs-lookup"><span data-stu-id="c6470-209">Use `description` instead.</span></span>

<span data-ttu-id="c6470-210">Краткое описание пакета для отображения пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c6470-210">A short description of the package for UI display.</span></span> <span data-ttu-id="c6470-211">Если этот элемент опущен, используется сокращенная версия элемента `description`.</span><span class="sxs-lookup"><span data-stu-id="c6470-211">If omitted, a truncated version of `description` is used.</span></span>

<span data-ttu-id="c6470-212">При отправке пакета в nuget.org `summary` поле ограничено 4000 символами.</span><span class="sxs-lookup"><span data-stu-id="c6470-212">When uploading a package to nuget.org, the `summary` field is limited to 4000 characters.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="c6470-213">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="c6470-213">releaseNotes</span></span>
<span data-ttu-id="c6470-214">*(Версия 1.5 и более поздние)* Описание изменений, внесенных в этом выпуске пакета NuGet; часто используется в пользовательском интерфейсе как вкладка **Обновления** диспетчера пакетов Visual Studio вместо описания пакета.</span><span class="sxs-lookup"><span data-stu-id="c6470-214">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

<span data-ttu-id="c6470-215">При отправке пакета в nuget.org `releaseNotes` поле ограничено 35 000 символами.</span><span class="sxs-lookup"><span data-stu-id="c6470-215">When uploading a package to nuget.org, the `releaseNotes` field is limited to 35,000 characters.</span></span>

#### <a name="copyright"></a><span data-ttu-id="c6470-216">авторские права</span><span class="sxs-lookup"><span data-stu-id="c6470-216">copyright</span></span>
<span data-ttu-id="c6470-217">*(Версия 1.5 и более поздние)* Сведения об авторских правах для пакета.</span><span class="sxs-lookup"><span data-stu-id="c6470-217">*(1.5+)* Copyright details for the package.</span></span>

<span data-ttu-id="c6470-218">При отправке пакета в nuget.org `copyright` поле ограничено 4000 символами.</span><span class="sxs-lookup"><span data-stu-id="c6470-218">When uploading a package to nuget.org, the `copyright` field is limited to 4000 characters.</span></span>

#### <a name="language"></a><span data-ttu-id="c6470-219">Язык</span><span class="sxs-lookup"><span data-stu-id="c6470-219">language</span></span>
<span data-ttu-id="c6470-220">Идентификатор языкового стандарта для пакета.</span><span class="sxs-lookup"><span data-stu-id="c6470-220">The locale ID for the package.</span></span> <span data-ttu-id="c6470-221">См. раздел [Создание локализованных пакетов](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="c6470-221">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="c6470-222">tags</span><span class="sxs-lookup"><span data-stu-id="c6470-222">tags</span></span>
<span data-ttu-id="c6470-223">Список разделенных пробелами тегов и ключевых слов, описывающих пакет NuGet и помогающих находить пакеты NuGet с помощью функций поиска и фильтрации.</span><span class="sxs-lookup"><span data-stu-id="c6470-223">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

<span data-ttu-id="c6470-224">При отправке пакета в nuget.org `tags` поле ограничено 4000 символами.</span><span class="sxs-lookup"><span data-stu-id="c6470-224">When uploading a package to nuget.org, the `tags` field is limited to 4000 characters.</span></span>

#### <a name="serviceable"></a><span data-ttu-id="c6470-225">serviceable</span><span class="sxs-lookup"><span data-stu-id="c6470-225">serviceable</span></span> 
<span data-ttu-id="c6470-226">*(Версия 3.3 и более поздние)* Только для внутреннего использования в NuGet.</span><span class="sxs-lookup"><span data-stu-id="c6470-226">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="c6470-227">repository</span><span class="sxs-lookup"><span data-stu-id="c6470-227">repository</span></span>
<span data-ttu-id="c6470-228">Метаданные репозитория, состоящие из четырех необязательных атрибутов: `type` и `url` *(4.0 +)* и `branch` и `commit` *(4.6 +)*.</span><span class="sxs-lookup"><span data-stu-id="c6470-228">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="c6470-229">Эти атрибуты позволяют сопоставлять объект `.nupkg` с репозиторием, в котором он построен, с возможностью получения таких сведений, как имя отдельной ветви и/или фиксация ХЭША SHA-1, который создал пакет.</span><span class="sxs-lookup"><span data-stu-id="c6470-229">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="c6470-230">Это должен быть общедоступный URL-адрес, который может вызываться непосредственно программным обеспечением управления версиями.</span><span class="sxs-lookup"><span data-stu-id="c6470-230">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="c6470-231">Это не должна быть HTML-страница, так как она предназначена для компьютера.</span><span class="sxs-lookup"><span data-stu-id="c6470-231">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="c6470-232">Для ссылки на страницу проекта используйте `projectUrl` вместо этого поле.</span><span class="sxs-lookup"><span data-stu-id="c6470-232">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="c6470-233">Пример:</span><span class="sxs-lookup"><span data-stu-id="c6470-233">For example:</span></span>
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

<span data-ttu-id="c6470-234">При отправке пакета в nuget.org `type` Длина атрибута ограничена 100 символами, а `url` Длина атрибута ограничена 4000 символами.</span><span class="sxs-lookup"><span data-stu-id="c6470-234">When uploading a package to nuget.org, the `type` attribute is limited to 100 characters and the `url` attribute is limited to 4000 characters.</span></span>

#### <a name="title"></a><span data-ttu-id="c6470-235">title</span><span class="sxs-lookup"><span data-stu-id="c6470-235">title</span></span>
<span data-ttu-id="c6470-236">Удобное для человека название пакета, которое может использоваться в некоторых интерфейсах пользователя.</span><span class="sxs-lookup"><span data-stu-id="c6470-236">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="c6470-237">(nuget.org и диспетчер пакетов в Visual Studio не отображают заголовок)</span><span class="sxs-lookup"><span data-stu-id="c6470-237">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

<span data-ttu-id="c6470-238">При отправке пакета в nuget.org `title` поле ограничено 256 символами, но не используется в целях вывода.</span><span class="sxs-lookup"><span data-stu-id="c6470-238">When uploading a package to nuget.org, the `title` field is limited to 256 characters but is not used for any display purposes.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="c6470-239">Элементы коллекции</span><span class="sxs-lookup"><span data-stu-id="c6470-239">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="c6470-240">packageTypes</span><span class="sxs-lookup"><span data-stu-id="c6470-240">packageTypes</span></span>
<span data-ttu-id="c6470-241">*(Версия 3.5 и более поздние)* Пустая коллекция или без нескольких элементов `<packageType>`, определяющих тип пакета, если он отличается от обычного пакета зависимостей.</span><span class="sxs-lookup"><span data-stu-id="c6470-241">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="c6470-242">Каждый элемент packageType имеет атрибуты *name* и *version*.</span><span class="sxs-lookup"><span data-stu-id="c6470-242">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="c6470-243">См. раздел [Указание типа пакета](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="c6470-243">See [Setting a package type](../create-packages/set-package-type.md).</span></span>

#### <a name="dependencies"></a><span data-ttu-id="c6470-244">зависимости</span><span class="sxs-lookup"><span data-stu-id="c6470-244">dependencies</span></span>
<span data-ttu-id="c6470-245">Коллекция из нуля или более элементов `<dependency>`, задающих зависимости для пакета.</span><span class="sxs-lookup"><span data-stu-id="c6470-245">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="c6470-246">Каждый элемент dependency имеет атрибуты *id*, *version*, *include* (версия 3.x и более поздние) и *exclude* (версия 3.x и более поздние).</span><span class="sxs-lookup"><span data-stu-id="c6470-246">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="c6470-247">См. раздел [Зависимости](#dependencies-element) далее.</span><span class="sxs-lookup"><span data-stu-id="c6470-247">See [Dependencies](#dependencies-element) below.</span></span>

#### <a name="frameworkassemblies"></a><span data-ttu-id="c6470-248">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="c6470-248">frameworkAssemblies</span></span>
<span data-ttu-id="c6470-249">*(Версия 1.2 и более поздние)* Коллекция из одного или более элементов `<frameworkAssembly>`, идентифицирующих ссылки на сборки .NET Framework, необходимые для этого пакета, что гарантирует добавление ссылок в проекты, использующие пакет.</span><span class="sxs-lookup"><span data-stu-id="c6470-249">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="c6470-250">Каждый элемент frameworkAssembly имеет атрибуты *assemblyName* и *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="c6470-250">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="c6470-251">См. раздел [Указание ссылок на сборки платформы в глобальном кэше сборок ](#specifying-framework-assembly-references-gac) ниже.</span><span class="sxs-lookup"><span data-stu-id="c6470-251">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>

#### <a name="references"></a><span data-ttu-id="c6470-252">Ссылки</span><span class="sxs-lookup"><span data-stu-id="c6470-252">references</span></span>
<span data-ttu-id="c6470-253">*(Версия 1.5 и более поздние)* Коллекция из нуля или более элементов `<reference>`, задающие имена сборок в папке `lib` пакета, которые добавляются в качестве ссылок проекта.</span><span class="sxs-lookup"><span data-stu-id="c6470-253">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="c6470-254">Каждый элемент reference имеет атрибут *file*.</span><span class="sxs-lookup"><span data-stu-id="c6470-254">Each reference has a *file* attribute.</span></span> <span data-ttu-id="c6470-255">Коллекция `<references>` также может содержать элемент `<group>` с атрибутом *targetFramework*, который, в свою очередь, содержит элементы `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="c6470-255">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="c6470-256">Если этот элемент опущен, включаются все ссылки в папке `lib`.</span><span class="sxs-lookup"><span data-stu-id="c6470-256">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="c6470-257">См. раздел [Указание явных ссылок на сборки](#specifying-explicit-assembly-references) ниже.</span><span class="sxs-lookup"><span data-stu-id="c6470-257">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>

#### <a name="contentfiles"></a><span data-ttu-id="c6470-258">contentFiles</span><span class="sxs-lookup"><span data-stu-id="c6470-258">contentFiles</span></span>
<span data-ttu-id="c6470-259">*(Версия 3.3 и более поздние)* Коллекция элементов `<files>`, которые идентифицируют файлы содержимого, включаемые в потребляющий проект.</span><span class="sxs-lookup"><span data-stu-id="c6470-259">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="c6470-260">Эти файлы задаются с набором атрибутов, который описывает их использование в системе проекта.</span><span class="sxs-lookup"><span data-stu-id="c6470-260">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="c6470-261">См. раздел [Указание включаемых в пакет файлов](#specifying-files-to-include-in-the-package) ниже.</span><span class="sxs-lookup"><span data-stu-id="c6470-261">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>

#### <a name="files"></a><span data-ttu-id="c6470-262">files</span><span class="sxs-lookup"><span data-stu-id="c6470-262">files</span></span> 
<span data-ttu-id="c6470-263">`<package>`Узел может содержать узел в `<files>` качестве одноуровневого элемента для `<metadata>` и `<contentFiles>` дочерний элемент в `<metadata>` , чтобы указать, какие файлы сборки и содержимого следует включить в пакет.</span><span class="sxs-lookup"><span data-stu-id="c6470-263">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="c6470-264">Дополнительные сведения см. далее в разделах [Включение файлов сборки](#including-assembly-files) и [Включение файлов содержимого](#including-content-files) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="c6470-264">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="c6470-265">атрибуты метаданных</span><span class="sxs-lookup"><span data-stu-id="c6470-265">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="c6470-266">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="c6470-266">minClientVersion</span></span>
<span data-ttu-id="c6470-267">Указывает минимальную версию клиента NuGet, который может установить этот пакет с использованием nuget.exe и диспетчера пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6470-267">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="c6470-268">Используется во всех случаях, когда пакет зависит от конкретных функций в файле `.nuspec`, которые были добавлены в определенной версии клиента NuGet.</span><span class="sxs-lookup"><span data-stu-id="c6470-268">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="c6470-269">Например, для пакета, использующего атрибут `developmentDependency`, атрибуту `minClientVersion` необходимо присвоить значение "2.8".</span><span class="sxs-lookup"><span data-stu-id="c6470-269">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="c6470-270">Аналогичным образом, для пакета, использующего элемент `contentFiles` (см. следующий раздел), атрибуту `minClientVersion` необходимо присвоить значение "3.3".</span><span class="sxs-lookup"><span data-stu-id="c6470-270">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="c6470-271">Также обратите внимание, что клиенты NuGet версий, предшествующих 2.5, не распознают этот флаг и поэтому *всегда* отклоняют установку пакета независимо от значения атрибута `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="c6470-271">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata minClientVersion="100.0.0.1">
        <id>dasdas</id>
        <version>2.0.0</version>
        <title />
        <authors>dsadas</authors>
        <owners />
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>My package description.</description>
    </metadata>
    <files>
        <file src="content\one.txt" target="content\one.txt" />
    </files>
</package>
```

## <a name="replacement-tokens"></a><span data-ttu-id="c6470-272">Замена маркеров</span><span class="sxs-lookup"><span data-stu-id="c6470-272">Replacement tokens</span></span>

<span data-ttu-id="c6470-273">При создании пакета [ `nuget pack` команда](../reference/cli-reference/cli-ref-pack.md) заменяет маркеры с разделителями $ в `.nuspec` `<metadata>` узле файла значениями, поступающими из файла проекта или `pack` `-properties` переключателя команды.</span><span class="sxs-lookup"><span data-stu-id="c6470-273">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="c6470-274">Маркеры задаются в командной строке следующим образом: `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="c6470-274">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="c6470-275">Например, вы можете использовать маркер, такой как `$owners$` и `$desc$`, в файле `.nuspec` и предоставить значения во время упаковки следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c6470-275">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="c6470-276">Чтобы использовать значения из проекта, укажите маркеры, описываемые в следующей таблице (AssemblyInfo ссылается на файл в `Properties`, например `AssemblyInfo.cs` или `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="c6470-276">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="c6470-277">Чтобы использовать эти маркеры, выполните команду `nuget pack` с файлом проекта, а не просто с файлом `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="c6470-277">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="c6470-278">Например, при использовании следующей команды маркеры `$id$` и `$version$` в файле `.nuspec` заменяются значениями проекта `AssemblyName` и `AssemblyVersion`:</span><span class="sxs-lookup"><span data-stu-id="c6470-278">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="c6470-279">Как правило, при наличии проекта вы изначально создаете файл `.nuspec` с использованием команды `nuget spec MyProject.csproj`, которая автоматически включает некоторые из этих стандартных маркеров.</span><span class="sxs-lookup"><span data-stu-id="c6470-279">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="c6470-280">Тем не менее, если в проекте отсутствуют значения для обязательных элементов `.nuspec`, команда `nuget pack` завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="c6470-280">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="c6470-281">Кроме того, при изменении значений проекта необходимо выполнить перестроение до создания пакета. Это можно легко сделать с помощью параметра `build` команды pack.</span><span class="sxs-lookup"><span data-stu-id="c6470-281">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="c6470-282">За исключением элемента `$configuration$`, значения в проекте используются в приоритетном порядке относительно любых значений, назначенных тому же маркеру в командной строке.</span><span class="sxs-lookup"><span data-stu-id="c6470-282">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="c6470-283">Токен</span><span class="sxs-lookup"><span data-stu-id="c6470-283">Token</span></span> | <span data-ttu-id="c6470-284">Источник значения</span><span class="sxs-lookup"><span data-stu-id="c6470-284">Value source</span></span> | <span data-ttu-id="c6470-285">Значение</span><span class="sxs-lookup"><span data-stu-id="c6470-285">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="c6470-286">**$id $**</span><span class="sxs-lookup"><span data-stu-id="c6470-286">**$id$**</span></span> | <span data-ttu-id="c6470-287">Файл проекта</span><span class="sxs-lookup"><span data-stu-id="c6470-287">Project file</span></span> | <span data-ttu-id="c6470-288">AssemblyName (Title) из файла проекта</span><span class="sxs-lookup"><span data-stu-id="c6470-288">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="c6470-289">**$version $**</span><span class="sxs-lookup"><span data-stu-id="c6470-289">**$version$**</span></span> | <span data-ttu-id="c6470-290">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="c6470-290">AssemblyInfo</span></span> | <span data-ttu-id="c6470-291">AssemblyInformationalVersion, если присутствует, в противном случае AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="c6470-291">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="c6470-292">**$author $**</span><span class="sxs-lookup"><span data-stu-id="c6470-292">**$author$**</span></span> | <span data-ttu-id="c6470-293">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="c6470-293">AssemblyInfo</span></span> | <span data-ttu-id="c6470-294">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="c6470-294">AssemblyCompany</span></span> |
| <span data-ttu-id="c6470-295">**$title $**</span><span class="sxs-lookup"><span data-stu-id="c6470-295">**$title$**</span></span> | <span data-ttu-id="c6470-296">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="c6470-296">AssemblyInfo</span></span> | <span data-ttu-id="c6470-297">ассемблититле</span><span class="sxs-lookup"><span data-stu-id="c6470-297">AssemblyTitle</span></span> |
| <span data-ttu-id="c6470-298">**$description $**</span><span class="sxs-lookup"><span data-stu-id="c6470-298">**$description$**</span></span> | <span data-ttu-id="c6470-299">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="c6470-299">AssemblyInfo</span></span> | <span data-ttu-id="c6470-300">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="c6470-300">AssemblyDescription</span></span> |
| <span data-ttu-id="c6470-301">**$copyright $**</span><span class="sxs-lookup"><span data-stu-id="c6470-301">**$copyright$**</span></span> | <span data-ttu-id="c6470-302">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="c6470-302">AssemblyInfo</span></span> | <span data-ttu-id="c6470-303">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="c6470-303">AssemblyCopyright</span></span> |
| <span data-ttu-id="c6470-304">**$configuration $**</span><span class="sxs-lookup"><span data-stu-id="c6470-304">**$configuration$**</span></span> | <span data-ttu-id="c6470-305">DLL-файл сборки</span><span class="sxs-lookup"><span data-stu-id="c6470-305">Assembly DLL</span></span> | <span data-ttu-id="c6470-306">Конфигурация, используемая для построения сборки, по умолчанию используется тип отладки.</span><span class="sxs-lookup"><span data-stu-id="c6470-306">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="c6470-307">Обратите внимание, что для создания пакета с помощью конфигурации выпуска в командной строке всегда используется параметр `-properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="c6470-307">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="c6470-308">Маркеры также можно использовать для разрешения путей при включении [файлов сборок](#including-assembly-files) и [файлов содержимого](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="c6470-308">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="c6470-309">Маркеры имеют те же имена, что и свойства MSBuild, что позволяет выбирать файлы для включения в зависимости в текущей конфигурации построения.</span><span class="sxs-lookup"><span data-stu-id="c6470-309">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="c6470-310">Например, если вы используете следующие маркеры в файле `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="c6470-310">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="c6470-311">И выполняете построение сборки, для которой `AssemblyName` имеет значение `LoggingLibrary` с конфигурацией `Release` в MSBuild, в файле `.nuspec` в пакете будут присутствовать следующие строки:</span><span class="sxs-lookup"><span data-stu-id="c6470-311">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="c6470-312">DEPENDENCIES, элемент</span><span class="sxs-lookup"><span data-stu-id="c6470-312">Dependencies element</span></span>

<span data-ttu-id="c6470-313">Элемент `<dependencies>` внутри элемента `<metadata>` содержит любое число элементов `<dependency>`, идентифицирующих другие пакеты, от которых зависит пакет верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="c6470-313">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="c6470-314">Ниже перечислены атрибуты каждого элемента `<dependency>`:</span><span class="sxs-lookup"><span data-stu-id="c6470-314">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="c6470-315">attribute</span><span class="sxs-lookup"><span data-stu-id="c6470-315">Attribute</span></span> | <span data-ttu-id="c6470-316">Описание</span><span class="sxs-lookup"><span data-stu-id="c6470-316">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="c6470-317">Идентификатор пакета зависимости, например EntityFramework и NUnit, являющийся именем пакета nuget.org, показан на странице пакета (обязательно).</span><span class="sxs-lookup"><span data-stu-id="c6470-317">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="c6470-318">Диапазон версий, которые допустимы в качестве зависимости (обязательно).</span><span class="sxs-lookup"><span data-stu-id="c6470-318">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="c6470-319">Точный синтаксис см. в разделе [Управление версиями пакета](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="c6470-319">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="c6470-320">Плавающие версии не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="c6470-320">Floating versions are not supported.</span></span> |
| <span data-ttu-id="c6470-321">include</span><span class="sxs-lookup"><span data-stu-id="c6470-321">include</span></span> | <span data-ttu-id="c6470-322">Разделенный запятыми список тегов включения или исключения (см. ниже), определяющий зависимости, включаемые в конечный пакет.</span><span class="sxs-lookup"><span data-stu-id="c6470-322">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="c6470-323">Значение по умолчанию — `all`.</span><span class="sxs-lookup"><span data-stu-id="c6470-323">The default value is `all`.</span></span> |
| <span data-ttu-id="c6470-324">исключение</span><span class="sxs-lookup"><span data-stu-id="c6470-324">exclude</span></span> | <span data-ttu-id="c6470-325">Разделенный запятыми список тегов включения или исключения (см. ниже), определяющий зависимости, исключаемые из конечного пакета.</span><span class="sxs-lookup"><span data-stu-id="c6470-325">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="c6470-326">Значение по умолчанию, `build,analyzers` которое может быть перезаписано.</span><span class="sxs-lookup"><span data-stu-id="c6470-326">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="c6470-327">Но `content/ ContentFiles` также неявно исключаются в окончательном пакете, который не может быть перезаписан.</span><span class="sxs-lookup"><span data-stu-id="c6470-327">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="c6470-328">Теги в свойстве `exclude` имеют приоритет перед тегами в свойстве `include`.</span><span class="sxs-lookup"><span data-stu-id="c6470-328">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="c6470-329">Например, `include="runtime, compile" exclude="compile"` равносильно `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="c6470-329">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

<span data-ttu-id="c6470-330">При отправке пакета в nuget.org длина `id` атрибута зависимости ограничена 128 символами, а `version` Длина атрибута ограничена 256 символами.</span><span class="sxs-lookup"><span data-stu-id="c6470-330">When uploading a package to nuget.org, each dependency's `id` attribute is limited to 128 characters and the `version` attribute is limited to 256 characters.</span></span>

| <span data-ttu-id="c6470-331">Тег включения или исключения</span><span class="sxs-lookup"><span data-stu-id="c6470-331">Include/Exclude tag</span></span> | <span data-ttu-id="c6470-332">Затрагиваемые папки пакета</span><span class="sxs-lookup"><span data-stu-id="c6470-332">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="c6470-333">contentFiles</span><span class="sxs-lookup"><span data-stu-id="c6470-333">contentFiles</span></span> | <span data-ttu-id="c6470-334">Содержимое</span><span class="sxs-lookup"><span data-stu-id="c6470-334">Content</span></span> |
| <span data-ttu-id="c6470-335">среда выполнения</span><span class="sxs-lookup"><span data-stu-id="c6470-335">runtime</span></span> | <span data-ttu-id="c6470-336">Runtime, Resources и FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="c6470-336">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="c6470-337">compile</span><span class="sxs-lookup"><span data-stu-id="c6470-337">compile</span></span> | <span data-ttu-id="c6470-338">lib</span><span class="sxs-lookup"><span data-stu-id="c6470-338">lib</span></span> |
| <span data-ttu-id="c6470-339">build;</span><span class="sxs-lookup"><span data-stu-id="c6470-339">build</span></span> | <span data-ttu-id="c6470-340">build (свойства и цели MSBuild)</span><span class="sxs-lookup"><span data-stu-id="c6470-340">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="c6470-341">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="c6470-341">native</span></span> | <span data-ttu-id="c6470-342">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="c6470-342">native</span></span> |
| <span data-ttu-id="c6470-343">нет</span><span class="sxs-lookup"><span data-stu-id="c6470-343">none</span></span> | <span data-ttu-id="c6470-344">Нет</span><span class="sxs-lookup"><span data-stu-id="c6470-344">No folders</span></span> |
| <span data-ttu-id="c6470-345">все</span><span class="sxs-lookup"><span data-stu-id="c6470-345">all</span></span> | <span data-ttu-id="c6470-346">Все папки</span><span class="sxs-lookup"><span data-stu-id="c6470-346">All folders</span></span> |

<span data-ttu-id="c6470-347">Например, следующие строки указывают зависимости от `PackageA` версии 1.1.0 или более поздней и `PackageB` версии 1.x.</span><span class="sxs-lookup"><span data-stu-id="c6470-347">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="c6470-348">Следующие строки указывают зависимости от тех же пакетов и включают папки `contentFiles` и `build` для `PackageA`, а также все папки, кроме `native` и `compile`, для `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="c6470-348">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="c6470-349">При создании `.nuspec` из проекта с помощью `nuget spec` , зависимости, существующие в этом проекте, не включаются автоматически в результирующий `.nuspec` файл.</span><span class="sxs-lookup"><span data-stu-id="c6470-349">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="c6470-350">Вместо этого используйте `nuget pack myproject.csproj` и получите файл с *расширением nuspec* в созданном *nupkgном* файле.</span><span class="sxs-lookup"><span data-stu-id="c6470-350">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="c6470-351">Этот *nuspec* содержит зависимости.</span><span class="sxs-lookup"><span data-stu-id="c6470-351">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="c6470-352">Группы зависимостей</span><span class="sxs-lookup"><span data-stu-id="c6470-352">Dependency groups</span></span>

<span data-ttu-id="c6470-353">*Версия 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="c6470-353">*Version 2.0+*</span></span>

<span data-ttu-id="c6470-354">В качестве альтернативы простому неструктурированному списку зависимости могут задаваться в соответствии с профилем платформы целевого проекта с использованием элементов `<group>` в элементе `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="c6470-354">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="c6470-355">Каждый элемент group имеет атрибут `targetFramework` и содержит ноль или более элементов `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="c6470-355">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="c6470-356">Эти зависимости устанавливаются вместе в том случае, если целевая платформа совместима с профилем платформы проекта.</span><span class="sxs-lookup"><span data-stu-id="c6470-356">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="c6470-357">Элемент `<group>` без атрибута `targetFramework` используется в качестве установленного по умолчанию или резервного списка зависимостей.</span><span class="sxs-lookup"><span data-stu-id="c6470-357">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="c6470-358">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="c6470-358">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="c6470-359">Формат группы не может смешиваться с неструктурированным списком.</span><span class="sxs-lookup"><span data-stu-id="c6470-359">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="c6470-360">Формат [моникера целевой платформы (TFM)](../reference/target-frameworks.md) , используемый в `lib/ref` папке, отличается по сравнению с TFM, используемым в `dependency groups` .</span><span class="sxs-lookup"><span data-stu-id="c6470-360">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="c6470-361">Если целевые платформы, объявленные в `dependencies group` и в `lib/ref` папке `.nuspec` файла, не имеют точных совпадений, `pack` команда вызовет вызов [предупреждения NuGet NU5128](../reference/errors-and-warnings/nu5128.md).</span><span class="sxs-lookup"><span data-stu-id="c6470-361">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="c6470-362">В следующем примере приводятся различные варианты элемента `<group>`:</span><span class="sxs-lookup"><span data-stu-id="c6470-362">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework=".NETFramework4.7.2">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="netcoreapp3.1">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="c6470-363">Явные ссылки на сборку</span><span class="sxs-lookup"><span data-stu-id="c6470-363">Explicit assembly references</span></span>

<span data-ttu-id="c6470-364">`<references>`Элемент используется проектами с `packages.config` целью явного указания сборок, на которые должен ссылаться целевой проект при использовании пакета.</span><span class="sxs-lookup"><span data-stu-id="c6470-364">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="c6470-365">Явные ссылки обычно применяются для сборок, используемых только во время разработки.</span><span class="sxs-lookup"><span data-stu-id="c6470-365">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="c6470-366">Дополнительные сведения см. на странице [Выбор сборок, на которые ссылаются проекты](../create-packages/select-assemblies-referenced-by-projects.md) .</span><span class="sxs-lookup"><span data-stu-id="c6470-366">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="c6470-367">Например, следующий элемент `<references>` указывает NuGet на необходимость добавлять ссылки только на сборки `xunit.dll` и `xunit.extensions.dll`, даже если в пакете есть другие сборки:</span><span class="sxs-lookup"><span data-stu-id="c6470-367">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="c6470-368">Группы ссылок</span><span class="sxs-lookup"><span data-stu-id="c6470-368">Reference groups</span></span>

<span data-ttu-id="c6470-369">В качестве альтернативы простому неструктурированному списку ссылки могут задаваться в соответствии с профилем платформы целевого проекта с использованием элементов `<group>` в элементе `<references>`.</span><span class="sxs-lookup"><span data-stu-id="c6470-369">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="c6470-370">Каждый элемент group имеет атрибут `targetFramework` и содержит ноль или более элементов `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="c6470-370">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="c6470-371">Эти ссылки добавляются в проект в том случае, если целевая платформа совместима с профилем платформы проекта.</span><span class="sxs-lookup"><span data-stu-id="c6470-371">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="c6470-372">Элемент `<group>` без атрибута `targetFramework` используется в качестве установленного по умолчанию или резервного списка ссылок.</span><span class="sxs-lookup"><span data-stu-id="c6470-372">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="c6470-373">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="c6470-373">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="c6470-374">Формат группы не может смешиваться с неструктурированным списком.</span><span class="sxs-lookup"><span data-stu-id="c6470-374">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="c6470-375">В следующем примере приводятся различные варианты элемента `<group>`:</span><span class="sxs-lookup"><span data-stu-id="c6470-375">The following example shows different variations of the `<group>` element:</span></span>

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a><span data-ttu-id="c6470-376">Ссылки на сборку платформы</span><span class="sxs-lookup"><span data-stu-id="c6470-376">Framework assembly references</span></span>

<span data-ttu-id="c6470-377">Сборки платформы входят в состав .NET Framework и должны находиться в глобальном кэше сборок любого заданного компьютера.</span><span class="sxs-lookup"><span data-stu-id="c6470-377">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="c6470-378">Идентифицируя такие сборки с помощью элемента `<frameworkAssemblies>`, пакет может гарантировать, что ссылки, отсутствующие в проекте, будут при необходимости добавлены в него.</span><span class="sxs-lookup"><span data-stu-id="c6470-378">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="c6470-379">Естественно, напрямую в пакет такие сборки не включаются.</span><span class="sxs-lookup"><span data-stu-id="c6470-379">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="c6470-380">Элемент `<frameworkAssemblies>` содержит ноль или более элементов `<frameworkAssembly>`, каждый из которых задает следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="c6470-380">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="c6470-381">attribute</span><span class="sxs-lookup"><span data-stu-id="c6470-381">Attribute</span></span> | <span data-ttu-id="c6470-382">Описание</span><span class="sxs-lookup"><span data-stu-id="c6470-382">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c6470-383">**имя_сборки**</span><span class="sxs-lookup"><span data-stu-id="c6470-383">**assemblyName**</span></span> | <span data-ttu-id="c6470-384">Полное имя сборки (обязательно).</span><span class="sxs-lookup"><span data-stu-id="c6470-384">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="c6470-385">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="c6470-385">**targetFramework**</span></span> | <span data-ttu-id="c6470-386">Указывает целевую платформу, к которой применяется эта ссылка (необязательно).</span><span class="sxs-lookup"><span data-stu-id="c6470-386">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="c6470-387">Если этот атрибут опущен, указывает, что ссылка применяется ко всем платформам.</span><span class="sxs-lookup"><span data-stu-id="c6470-387">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="c6470-388">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="c6470-388">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="c6470-389">В следующем примере показаны ссылка на `System.Net` для всех целевых платформ и ссылка на `System.ServiceModel` только для платформы .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="c6470-389">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="c6470-390">Включение файлов сборки</span><span class="sxs-lookup"><span data-stu-id="c6470-390">Including assembly files</span></span>

<span data-ttu-id="c6470-391">Если вы придерживаетесь соглашений, описываемых в разделе [Создание пакета](../create-packages/creating-a-package.md), вам не нужно явно задавать список файлов в файле `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="c6470-391">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="c6470-392">Команда `nuget pack` автоматически выбирает необходимые файлы.</span><span class="sxs-lookup"><span data-stu-id="c6470-392">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="c6470-393">Когда пакет устанавливается в проекте, NuGet автоматически добавляет ссылки на библиотеки DLL сборок в пакете, *кроме* тех из них, в именах которых есть `.resources.dll`, так как они считаются локализованными вспомогательными сборками.</span><span class="sxs-lookup"><span data-stu-id="c6470-393">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="c6470-394">По этой причине следует избегать использования `.resources.dll` в именах файлов пакета, которые содержат важный код.</span><span class="sxs-lookup"><span data-stu-id="c6470-394">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="c6470-395">Чтобы обойти такое автоматическое поведение и явно управлять включением сборок в пакет, поместите элемент `<files>` в качестве дочернего для `<package>` (на одном уровне с `<metadata>`), указывая каждый файл с помощью элемента `<file>`.</span><span class="sxs-lookup"><span data-stu-id="c6470-395">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="c6470-396">Пример:</span><span class="sxs-lookup"><span data-stu-id="c6470-396">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="c6470-397">В NuGet версии 2.x и более ранних в проектах, использующих `packages.config`, элемент `<files>` также используется для включения неизменяемых файлов содержимого при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="c6470-397">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="c6470-398">В NuGet версии 3.3 и более поздних и проектах PackageReference используется элемент `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="c6470-398">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="c6470-399">Дополнительные сведения см. в разделе [Включение файлов содержимого](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="c6470-399">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="c6470-400">Атрибуты элементов файла</span><span class="sxs-lookup"><span data-stu-id="c6470-400">File element attributes</span></span>

<span data-ttu-id="c6470-401">Каждый элемент `<file>` задает указанные ниже атрибуты:</span><span class="sxs-lookup"><span data-stu-id="c6470-401">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="c6470-402">attribute</span><span class="sxs-lookup"><span data-stu-id="c6470-402">Attribute</span></span> | <span data-ttu-id="c6470-403">Описание</span><span class="sxs-lookup"><span data-stu-id="c6470-403">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c6470-404">**src**</span><span class="sxs-lookup"><span data-stu-id="c6470-404">**src**</span></span> | <span data-ttu-id="c6470-405">Расположение файла или файлов, которые требуется включить, с учетом исключений, задаваемых атрибутом `exclude`.</span><span class="sxs-lookup"><span data-stu-id="c6470-405">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="c6470-406">Если не указан абсолютный путь, этот путь задается относительно файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="c6470-406">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="c6470-407">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="c6470-407">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="c6470-408">**target**</span><span class="sxs-lookup"><span data-stu-id="c6470-408">**target**</span></span> | <span data-ttu-id="c6470-409">Относительный путь к папке в пакете, куда помещаются файлы исходного кода. Должен начинаться с `lib`, `content`, `build` или `tools`.</span><span class="sxs-lookup"><span data-stu-id="c6470-409">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="c6470-410">См. раздел [Создание файла NUSPEC на основе рабочего каталога, соответствующего соглашениям](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="c6470-410">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="c6470-411">**запрет**</span><span class="sxs-lookup"><span data-stu-id="c6470-411">**exclude**</span></span> | <span data-ttu-id="c6470-412">Разделенный точками с запятой список файлов или шаблонов файлов, которые исключаются из расположения `src`.</span><span class="sxs-lookup"><span data-stu-id="c6470-412">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="c6470-413">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="c6470-413">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="c6470-414">Примеры</span><span class="sxs-lookup"><span data-stu-id="c6470-414">Examples</span></span>

<span data-ttu-id="c6470-415">**Одна сборка**</span><span class="sxs-lookup"><span data-stu-id="c6470-415">**Single assembly**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="library.dll" target="lib" />

Packaged result:
    lib\library.dll
```

<span data-ttu-id="c6470-416">**Одна сборка, относящаяся к целевой платформе**</span><span class="sxs-lookup"><span data-stu-id="c6470-416">**Single assembly specific to a target framework**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="assemblies\net40\library.dll" target="lib\net40" />

Packaged result:
    lib\net40\library.dll
```

<span data-ttu-id="c6470-417">**Набор DLL-файлов с использованием подстановочного знака**</span><span class="sxs-lookup"><span data-stu-id="c6470-417">**Set of DLLs using a wildcard**</span></span>

```
Source files:
    bin\release\libraryA.dll
    bin\release\libraryB.dll

.nuspec entry:
    <file src="bin\release\*.dll" target="lib" />

Packaged result:
    lib\libraryA.dll
    lib\libraryB.dll
```

<span data-ttu-id="c6470-418">**DLL-файлы для разных платформ**</span><span class="sxs-lookup"><span data-stu-id="c6470-418">**DLLs for different frameworks**</span></span>

```
Source files:
    lib\net40\library.dll
    lib\net20\library.dll

.nuspec entry (using ** recursive search):
    <file src="lib\**" target="lib" />

Packaged result:
    lib\net40\library.dll
    lib\net20\library.dll
```

<span data-ttu-id="c6470-419">**Исключение файлов**</span><span class="sxs-lookup"><span data-stu-id="c6470-419">**Excluding files**</span></span>

```
Source files:
    \tools\fileA.bak
    \tools\fileB.bak
    \tools\fileA.log
    \tools\build\fileB.log

.nuspec entries:
    <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
    <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

Package result:
    (no files)
```

## <a name="including-content-files"></a><span data-ttu-id="c6470-420">Включение файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="c6470-420">Including content files</span></span>

<span data-ttu-id="c6470-421">Файлы содержимого — это неизменяемые файлы, которые пакету необходимо включить в проект.</span><span class="sxs-lookup"><span data-stu-id="c6470-421">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="c6470-422">Такие файлы не подлежат изменению проектом, который потребляет их.</span><span class="sxs-lookup"><span data-stu-id="c6470-422">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="c6470-423">Примеры файлов содержимого:</span><span class="sxs-lookup"><span data-stu-id="c6470-423">Example content files include:</span></span>

- <span data-ttu-id="c6470-424">Изображения, внедряемые в качестве ресурсов</span><span class="sxs-lookup"><span data-stu-id="c6470-424">Images that are embedded as resources</span></span>
- <span data-ttu-id="c6470-425">Файлы исходного кода, которые уже были скомпилированы</span><span class="sxs-lookup"><span data-stu-id="c6470-425">Source files that are already compiled</span></span>
- <span data-ttu-id="c6470-426">Скрипты, которые необходимо включить в выходные данные построения проекта</span><span class="sxs-lookup"><span data-stu-id="c6470-426">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="c6470-427">Файлы конфигурации для пакета, которые необходимо включить в проект, но не требуется изменять в рамках отдельного проекта</span><span class="sxs-lookup"><span data-stu-id="c6470-427">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="c6470-428">Файлы содержимого включаются в проект с помощью элемента `<files>`, задающего папку `content` в атрибуте `target`.</span><span class="sxs-lookup"><span data-stu-id="c6470-428">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="c6470-429">Тем не менее такие файлы игнорируются при установке пакета в проект с использованием PackageReference, в которых вместо этого используется элемент `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="c6470-429">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="c6470-430">Чтобы обеспечить максимальную совместимость с потребляющими проектами, в идеальном случае файлы содержимого следует задавать в проекте с использованием обоих элементов.</span><span class="sxs-lookup"><span data-stu-id="c6470-430">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="c6470-431">Использование элемента files для файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="c6470-431">Using the files element for content files</span></span>

<span data-ttu-id="c6470-432">Для файлов содержимого следует использовать тот же формат, что и для файлов сборки, однако необходимо указать в качестве базовой сборки `content` в атрибуте `target`, как показано в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="c6470-432">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="c6470-433">**Базовые файлы содержимого**</span><span class="sxs-lookup"><span data-stu-id="c6470-433">**Basic content files**</span></span>

```
Source files:
    css\mobile\style1.css
    css\mobile\style2.css

.nuspec entry:
    <file src="css\mobile\*.css" target="content\css\mobile" />

Packaged result:
    content\css\mobile\style1.css
    content\css\mobile\style2.css
```

<span data-ttu-id="c6470-434">**Файлы содержимого со структурой каталогов**</span><span class="sxs-lookup"><span data-stu-id="c6470-434">**Content files with directory structure**</span></span>

```
Source files:
    css\mobile\style.css
    css\mobile\wp7\style.css
    css\browser\style.css

.nuspec entry:
    <file src="css\**\*.css" target="content\css" />

Packaged result:
    content\css\mobile\style.css
    content\css\mobile\wp7\style.css
    content\css\browser\style.css
```

<span data-ttu-id="c6470-435">**Файлы содержимого, относящиеся к целевой платформе**</span><span class="sxs-lookup"><span data-stu-id="c6470-435">**Content file specific to a target framework**</span></span>

```
Source file:
    css\cool\style.css

.nuspec entry
    <file src="css\cool\style.css" target="Content" />

Packaged result:
    content\style.css
```

<span data-ttu-id="c6470-436">**Файлы содержимого, копируемые в папку с точкой в имени**</span><span class="sxs-lookup"><span data-stu-id="c6470-436">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="c6470-437">В этом случае NuGet определяет, что расширение в атрибуте `target` не соответствует расширению в `src` и обрабатывает такую часть имени в атрибуте `target` как папку:</span><span class="sxs-lookup"><span data-stu-id="c6470-437">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

```
Source file:
    images\picture.png

.nuspec entry:
    <file src="images\picture.png" target="Content\images\package.icons" />

Packaged result:
    content\images\package.icons\picture.png
```

<span data-ttu-id="c6470-438">**Файлы содержимого без расширений**</span><span class="sxs-lookup"><span data-stu-id="c6470-438">**Content files without extensions**</span></span>

<span data-ttu-id="c6470-439">Чтобы включить файлы без расширения, используйте подстановочные знаки `*` или `**`:</span><span class="sxs-lookup"><span data-stu-id="c6470-439">To include files without an extension, use the `*` or `**` wildcards:</span></span>

```
Source file:
    flags\installed

.nuspec entry:
    <file src="flags\**" target="flags" />

Packaged result:
    flags\installed
```

<span data-ttu-id="c6470-440">**Файлы содержимого с глубоким путем и глубоким целевым объектом**</span><span class="sxs-lookup"><span data-stu-id="c6470-440">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="c6470-441">В этом случае из-за совпадения расширений файлов для исходного и целевого объектов NuGet предполагает, что целевой объект задает имя файла, а не папки:</span><span class="sxs-lookup"><span data-stu-id="c6470-441">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

```
Source file:
    css\cool\style.css

.nuspec entry:
    <file src="css\cool\style.css" target="Content\css\cool" />
    or:
    <file src="css\cool\style.css" target="Content\css\cool\style.css" />

Packaged result:
    content\css\cool\style.css
```

<span data-ttu-id="c6470-442">**Переименование файла содержимого в пакете**</span><span class="sxs-lookup"><span data-stu-id="c6470-442">**Renaming a content file in the package**</span></span>

```
Source file:
    ie\css\style.css

.nuspec entry:
    <file src="ie\css\style.css" target="Content\css\ie.css" />

Packaged result:
    content\css\ie.css
```

<span data-ttu-id="c6470-443">**Исключение файлов**</span><span class="sxs-lookup"><span data-stu-id="c6470-443">**Excluding files**</span></span>

```
Source file:
    docs\*.txt (multiple files)

.nuspec entry:
    <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
    or
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

Packaged result:
    All .txt files from docs except admin.txt (first example)
    All .txt files from docs except admin.txt and log.txt (second example)
```

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="c6470-444">Использование элемента contentFiles для файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="c6470-444">Using the contentFiles element for content files</span></span>

<span data-ttu-id="c6470-445">*NuGet 4.0 и более поздней версии с PackageReference*</span><span class="sxs-lookup"><span data-stu-id="c6470-445">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="c6470-446">По умолчанию пакет помещает содержимое в папку `contentFiles` (см. ниже), а команда `nuget pack` включает все файлы в этой папке с использованием установленных по умолчанию атрибутов.</span><span class="sxs-lookup"><span data-stu-id="c6470-446">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="c6470-447">В этом случае включать узел `contentFiles` в файл `.nuspec` не требуется.</span><span class="sxs-lookup"><span data-stu-id="c6470-447">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="c6470-448">Чтобы управлять включаемыми файлами, элемент `<contentFiles>` задает коллекцию элементов `<files>`, которая точно определяет включаемые файлы.</span><span class="sxs-lookup"><span data-stu-id="c6470-448">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="c6470-449">Эти файлы задаются с набором атрибутов, который описывает их использование в системе проекта:</span><span class="sxs-lookup"><span data-stu-id="c6470-449">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="c6470-450">attribute</span><span class="sxs-lookup"><span data-stu-id="c6470-450">Attribute</span></span> | <span data-ttu-id="c6470-451">Описание</span><span class="sxs-lookup"><span data-stu-id="c6470-451">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c6470-452">**относится**</span><span class="sxs-lookup"><span data-stu-id="c6470-452">**include**</span></span> | <span data-ttu-id="c6470-453">Расположение файла или файлов, которые требуется включить, с учетом исключений, задаваемых атрибутом `exclude` (обязательно).</span><span class="sxs-lookup"><span data-stu-id="c6470-453">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="c6470-454">Путь задается относительно `contentFiles` папки, если не указан абсолютный путь.</span><span class="sxs-lookup"><span data-stu-id="c6470-454">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="c6470-455">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="c6470-455">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="c6470-456">**запрет**</span><span class="sxs-lookup"><span data-stu-id="c6470-456">**exclude**</span></span> | <span data-ttu-id="c6470-457">Разделенный точками с запятой список файлов или шаблонов файлов, которые исключаются из расположения `src`.</span><span class="sxs-lookup"><span data-stu-id="c6470-457">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="c6470-458">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="c6470-458">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="c6470-459">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="c6470-459">**buildAction**</span></span> | <span data-ttu-id="c6470-460">Действие сборки, присваиваемое элементу содержимого для MSBuild, например,, `Content` , `None` `Embedded Resource` `Compile` и т. д. Значение по умолчанию — `Compile` .</span><span class="sxs-lookup"><span data-stu-id="c6470-460">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="c6470-461">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="c6470-461">**copyToOutput**</span></span> | <span data-ttu-id="c6470-462">Логическое значение, указывающее, следует ли копировать элементы содержимого в выходную папку сборки (или публикации).</span><span class="sxs-lookup"><span data-stu-id="c6470-462">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="c6470-463">Значение по умолчанию – false.</span><span class="sxs-lookup"><span data-stu-id="c6470-463">The default is false.</span></span> |
| <span data-ttu-id="c6470-464">**flatten**</span><span class="sxs-lookup"><span data-stu-id="c6470-464">**flatten**</span></span> | <span data-ttu-id="c6470-465">Логическое значение, указывающее на необходимость копировать элементы содержимого в одну папку в выходных данных построения (true) или сохранить структуру папок пакета (false).</span><span class="sxs-lookup"><span data-stu-id="c6470-465">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="c6470-466">Этот параметр применяется, только если для параметра copyToOutput установлено значение true.</span><span class="sxs-lookup"><span data-stu-id="c6470-466">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="c6470-467">Значение по умолчанию – false.</span><span class="sxs-lookup"><span data-stu-id="c6470-467">The default is false.</span></span> |

<span data-ttu-id="c6470-468">При установке пакета NuGet применяет дочерние элементы `<contentFiles>` в порядке сверху вниз.</span><span class="sxs-lookup"><span data-stu-id="c6470-468">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="c6470-469">Если одному файлу соответствует несколько записей, применяются все записи.</span><span class="sxs-lookup"><span data-stu-id="c6470-469">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="c6470-470">При обнаружении конфликтов для одного атрибута запись верхнего уровня переопределяет записи на нижних уровнях.</span><span class="sxs-lookup"><span data-stu-id="c6470-470">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="c6470-471">Структура папки пакета</span><span class="sxs-lookup"><span data-stu-id="c6470-471">Package folder structure</span></span>

<span data-ttu-id="c6470-472">Структурирование содержимого в проекте пакета осуществляется по следующему шаблону:</span><span class="sxs-lookup"><span data-stu-id="c6470-472">The package project should structure content using the following pattern:</span></span>

```
/contentFiles/{codeLanguage}/{TxM}/{any?}
```

- <span data-ttu-id="c6470-473">Элемент `codeLanguages` может иметь значение `cs`, `vb`, `fs`, `any` или любой другой эквивалент заданного `$(ProjectLanguage)` в нижнем регистре</span><span class="sxs-lookup"><span data-stu-id="c6470-473">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="c6470-474">Элемент `TxM` представляет любой допустимый моникер целевой платформы, поддерживаемой NuGet (см. раздел [Целевые платформы](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="c6470-474">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="c6470-475">В конце этого синтаксиса может добавляться любая структура папок.</span><span class="sxs-lookup"><span data-stu-id="c6470-475">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="c6470-476">Пример:</span><span class="sxs-lookup"><span data-stu-id="c6470-476">For example:</span></span>

```
Language- and framework-agnostic:
    /contentFiles/any/any/config.xml

net45 content for all languages
    /contentFiles/any/net45/config.xml

C#-specific content for net45 and up
    /contentFiles/cs/net45/sample.cs
```

<span data-ttu-id="c6470-477">Для пустых папок можно использовать `.`, чтобы отказаться от предоставления содержимого для определенных комбинаций языка и моникера целевой платформы, например:</span><span class="sxs-lookup"><span data-stu-id="c6470-477">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

```
/contentFiles/vb/any/code.vb
/contentFiles/cs/any/.
```

#### <a name="example-contentfiles-section"></a><span data-ttu-id="c6470-478">Пример раздела contentFiles</span><span class="sxs-lookup"><span data-stu-id="c6470-478">Example contentFiles section</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <contentFiles>
            <!-- Embed image resources -->
            <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
            <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

            <!-- Embed all image resources under contentFiles/cs/ -->
            <files include="cs/**/*.png" buildAction="EmbeddedResource" />

            <!-- Copy config.xml to the root of the output folder -->
            <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

            <!-- Copy run.cmd to the output folder and keep the directory structure -->
            <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

            <!-- Include everything in the scripts folder except exe files -->
            <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
        </contentFiles>
        </metadata>
</package>
```

## <a name="framework-reference-groups"></a><span data-ttu-id="c6470-479">Эталонные группы платформы</span><span class="sxs-lookup"><span data-stu-id="c6470-479">Framework reference groups</span></span>

<span data-ttu-id="c6470-480">*Только версия 5.1 и вих PackageReference*</span><span class="sxs-lookup"><span data-stu-id="c6470-480">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="c6470-481">Ссылки на платформы — это концепция .NET Core, представляющая общие платформы, такие как WPF или Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="c6470-481">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="c6470-482">Если указать общую платформу, пакет гарантирует, что все его зависимости Framework будут включены в ссылающийся проект.</span><span class="sxs-lookup"><span data-stu-id="c6470-482">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="c6470-483">Каждому `<group>` элементу требуется `targetFramework` атрибут и ноль или более `<frameworkReference>` элементов.</span><span class="sxs-lookup"><span data-stu-id="c6470-483">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="c6470-484">В следующем примере показан nuspec, созданный для проекта .NET Core WPF.</span><span class="sxs-lookup"><span data-stu-id="c6470-484">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="c6470-485">Обратите внимание, что создание нуспекс, содержащих ссылки на платформы, не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="c6470-485">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="c6470-486">Вместо этого рекомендуется использовать [целевой](msbuild-targets.md) пакет, который автоматически определит их в проекте.</span><span class="sxs-lookup"><span data-stu-id="c6470-486">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

```xml
<package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
  <metadata>
    <dependencies>
      <group targetFramework=".NETCoreApp3.1" />
    </dependencies>
    <frameworkReferences>
      <group targetFramework=".NETCoreApp3.1">
        <frameworkReference name="Microsoft.WindowsDesktop.App.WPF" />
      </group>
    </frameworkReferences>
  </metadata>
</package>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="c6470-487">Пример файлов nuspec</span><span class="sxs-lookup"><span data-stu-id="c6470-487">Example nuspec files</span></span>

<span data-ttu-id="c6470-488">**Простой файл `.nuspec`, в котором не задаются зависимости или файлы**</span><span class="sxs-lookup"><span data-stu-id="c6470-488">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

<span data-ttu-id="c6470-489">**Файл `.nuspec` с зависимостями**</span><span class="sxs-lookup"><span data-stu-id="c6470-489">**A `.nuspec` with dependencies**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

<span data-ttu-id="c6470-490">**Файл `.nuspec` с файлами**</span><span class="sxs-lookup"><span data-stu-id="c6470-490">**A `.nuspec` with files**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

<span data-ttu-id="c6470-491">**Файл `.nuspec` со сборками платформы**</span><span class="sxs-lookup"><span data-stu-id="c6470-491">**A `.nuspec` with framework assemblies**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

<span data-ttu-id="c6470-492">В этом примере для целевых объектов проекта устанавливаются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="c6470-492">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="c6470-493">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="c6470-493">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="c6470-494">Клиентский профиль .NET4 -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="c6470-494">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="c6470-495">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="c6470-495">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="c6470-496">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="c6470-496">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
