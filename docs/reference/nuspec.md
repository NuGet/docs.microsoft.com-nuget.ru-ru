---
title: Справочник по файлу nuspec для NuGet
description: Файл с расширением .nuspec содержит метаданные пакета, которые используются при построении пакета и предоставляют дополнительную информацию для его потребителей.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: fd6ecab05a392a2a0b4ddf1ac15eb108f2653703
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842414"
---
# <a name="nuspec-reference"></a><span data-ttu-id="182ab-103">Справочник по файлу NUSPEC</span><span class="sxs-lookup"><span data-stu-id="182ab-103">.nuspec reference</span></span>

<span data-ttu-id="182ab-104">Файл `.nuspec` представляет собой манифест в формате XML и содержит метаданные пакета.</span><span class="sxs-lookup"><span data-stu-id="182ab-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="182ab-105">Этот манифест используется при построении пакета и содержит дополнительные сведения для его потребителей.</span><span class="sxs-lookup"><span data-stu-id="182ab-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="182ab-106">Манифест всегда включается в пакет.</span><span class="sxs-lookup"><span data-stu-id="182ab-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="182ab-107">В этом разделе.</span><span class="sxs-lookup"><span data-stu-id="182ab-107">In this topic:</span></span>

- [<span data-ttu-id="182ab-108">Общая форма и схема</span><span class="sxs-lookup"><span data-stu-id="182ab-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="182ab-109">[Замена маркеров](#replacement-tokens) (при использовании с проектом Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="182ab-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="182ab-110">Зависимости</span><span class="sxs-lookup"><span data-stu-id="182ab-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="182ab-111">Явные ссылки на сборку</span><span class="sxs-lookup"><span data-stu-id="182ab-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="182ab-112">Ссылки на сборку платформы</span><span class="sxs-lookup"><span data-stu-id="182ab-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="182ab-113">Включение файлов сборки</span><span class="sxs-lookup"><span data-stu-id="182ab-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="182ab-114">Включение файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="182ab-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="182ab-115">Примеры файлов nuspec</span><span class="sxs-lookup"><span data-stu-id="182ab-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="182ab-116">Совместимость типов проектов</span><span class="sxs-lookup"><span data-stu-id="182ab-116">Project type compatibility</span></span>

- <span data-ttu-id="182ab-117">Используйте `.nuspec` с `nuget.exe pack` для не SDK-style проекты, использующие `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="182ab-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="182ab-118">Объект `.nuspec` файл не требуется для создания пакетов для [стиле пакетов SDK для проектов](../resources/check-project-format.md) (как правило, .NET Core и .NET Standard проекты, использующие [атрибута пакета SDK для](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="182ab-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="182ab-119">(Обратите внимание, что `.nuspec` создается при создании пакета.)</span><span class="sxs-lookup"><span data-stu-id="182ab-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="182ab-120">При создании пакета с помощью `dotnet.exe pack` или `msbuild pack target`, мы рекомендуем вам [включающей все свойства](../reference/msbuild-targets.md#pack-target) , которые обычно в `.nuspec` вместо этого файла в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="182ab-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="182ab-121">Тем не менее, вместо этого можно [использовать `.nuspec` файл пакета с помощью `dotnet.exe` или `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="182ab-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="182ab-122">Для проектов, перенесенных из `packages.config` для [PackageReference](../consume-packages/package-references-in-project-files.md), `.nuspec` файл не требуется для создания пакета.</span><span class="sxs-lookup"><span data-stu-id="182ab-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="182ab-123">Вместо этого используйте [пакета msbuild](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="182ab-123">Instead, use [msbuild pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="182ab-124">Общая форма и схема</span><span class="sxs-lookup"><span data-stu-id="182ab-124">General form and schema</span></span>

<span data-ttu-id="182ab-125">Текущий файл схемы `nuspec.xsd` представлен в [репозитории GitHub для NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="182ab-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="182ab-126">В рамках этой схемы файл `.nuspec` имеет следующую общую форму:</span><span class="sxs-lookup"><span data-stu-id="182ab-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="182ab-127">Чтобы получить наглядное представление схемы, откройте файл в режиме конструктора Visual Studio и щелкните ссылку **Обозреватель схемы XML**.</span><span class="sxs-lookup"><span data-stu-id="182ab-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="182ab-128">Также можно открыть этот файл в виде кода. Для этого щелкните правой кнопкой мыши в редакторе и выберите команду **Показать в обозревателе схемы XML**.</span><span class="sxs-lookup"><span data-stu-id="182ab-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="182ab-129">В любом случае при развертывании большинства узлов схема будет иметь примерно следующий вид:</span><span class="sxs-lookup"><span data-stu-id="182ab-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Обозреватель схемы Visual Studio с открытым файлом nuspec.xsd](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="182ab-131">Обязательные элементы метаданных</span><span class="sxs-lookup"><span data-stu-id="182ab-131">Required metadata elements</span></span>

<span data-ttu-id="182ab-132">Следующие элементы являются минимальным требованием для пакета, однако, несмотря на это, рекомендуется добавить [дополнительные элементы метаданных](#optional-metadata-elements), чтобы оптимизировать работу с вашим пакетом для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="182ab-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="182ab-133">Эти элементы должны использоваться внутри элемента `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="182ab-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="182ab-134">id</span><span class="sxs-lookup"><span data-stu-id="182ab-134">id</span></span> 
<span data-ttu-id="182ab-135">Идентификатор пакета без учета регистра, который должен быть уникальным в пределах сайта nuget.org или иной коллекции, в которой находится пакет.</span><span class="sxs-lookup"><span data-stu-id="182ab-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="182ab-136">Идентификаторы не должны содержать пробелов или символов, которые недопустимы в URL-адресах, и в них должны соблюдаться общие правила касательно пространств имен .NET.</span><span class="sxs-lookup"><span data-stu-id="182ab-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="182ab-137">Инструкции см. в разделе [Выбор уникального идентификатора пакета](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="182ab-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="182ab-138">version</span><span class="sxs-lookup"><span data-stu-id="182ab-138">version</span></span>
<span data-ttu-id="182ab-139">Версия пакета, указываемая согласно шаблону *основной_номер.дополнительный_номер.исправление*.</span><span class="sxs-lookup"><span data-stu-id="182ab-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="182ab-140">Номер версии может включать в себя суффикс предварительной версии, как описано в разделе [Управление версиями пакета](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="182ab-140">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="182ab-141">Описание</span><span class="sxs-lookup"><span data-stu-id="182ab-141">description</span></span>
<span data-ttu-id="182ab-142">Подробное описание пакета для отображения пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="182ab-142">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="182ab-143">authors</span><span class="sxs-lookup"><span data-stu-id="182ab-143">authors</span></span>
<span data-ttu-id="182ab-144">Разделенный запятыми список авторов пакетов, совпадающих с именами профилей на сайте nuget.org. Они отображаются в коллекции NuGet на сайте nuget.org и используются для перекрестных ссылок на пакеты тех же авторов.</span><span class="sxs-lookup"><span data-stu-id="182ab-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="182ab-145">Необязательные элементы метаданных</span><span class="sxs-lookup"><span data-stu-id="182ab-145">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="182ab-146">owners</span><span class="sxs-lookup"><span data-stu-id="182ab-146">owners</span></span>
<span data-ttu-id="182ab-147">Разделенный запятыми список создателей пакета, совпадающих с именами профилей на сайте nuget.org. Часто совпадает со списком в элементе `authors` и игнорируется при загрузке пакета на веб-сайт nuget.org. См. раздел [Управление владельцами пакетов на веб-сайте nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="182ab-147">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="182ab-148">projectUrl</span><span class="sxs-lookup"><span data-stu-id="182ab-148">projectUrl</span></span>
<span data-ttu-id="182ab-149">URL-адрес для домашней страницы пакета, часто указываемый при отображении пользовательского интерфейса, также как и nuget.org.</span><span class="sxs-lookup"><span data-stu-id="182ab-149">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

#### <a name="licenseurl"></a><span data-ttu-id="182ab-150">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="182ab-150">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="182ab-151">licenseUrl устарел.</span><span class="sxs-lookup"><span data-stu-id="182ab-151">licenseUrl is being deprecated.</span></span> <span data-ttu-id="182ab-152">Вместо этого используйте лицензию.</span><span class="sxs-lookup"><span data-stu-id="182ab-152">Use license instead.</span></span>

<span data-ttu-id="182ab-153">URL-адрес для лицензии пакета, часто отображающийся в интерфейсах пользователя как nuget.org.</span><span class="sxs-lookup"><span data-stu-id="182ab-153">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

#### <a name="license"></a><span data-ttu-id="182ab-154">лицензии</span><span class="sxs-lookup"><span data-stu-id="182ab-154">license</span></span>
<span data-ttu-id="182ab-155">Выражение SPDX лицензии или путь к файлу лицензии внутри пакета, часто отображающийся в интерфейсах пользователя как nuget.org. Если пакет по common лицензии, например MIT или BSD-2-предложение лицензируется использовать связанное [идентификатор лицензии SPDX](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="182ab-155">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="182ab-156">Например:</span><span class="sxs-lookup"><span data-stu-id="182ab-156">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="182ab-157">NuGet.org принимает только выражения лицензии утвержденные Open Source Initiative или бесплатная Software Foundation.</span><span class="sxs-lookup"><span data-stu-id="182ab-157">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="182ab-158">Если ваш пакет лицензируется распространенных сразу несколько лицензий, можно указать составного лицензии с помощью [SPDX выражение синтаксис версии 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="182ab-158">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="182ab-159">Например:</span><span class="sxs-lookup"><span data-stu-id="182ab-159">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="182ab-160">Если вы используете пользовательские лицензии, не поддерживаемый выражения лицензии, вы можете упаковать `.txt` или `.md` файл с текстом лицензии.</span><span class="sxs-lookup"><span data-stu-id="182ab-160">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="182ab-161">Например:</span><span class="sxs-lookup"><span data-stu-id="182ab-161">For example:</span></span>

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

<span data-ttu-id="182ab-162">Для эквивалентных MSBuild, взгляните на [упаковки выражении лицензии или файл лицензии](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="182ab-162">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="182ab-163">Точный синтаксис выражений лицензии NuGet описан ниже в [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="182ab-163">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="182ab-164">iconUrl</span><span class="sxs-lookup"><span data-stu-id="182ab-164">iconUrl</span></span>
<span data-ttu-id="182ab-165">URL-адрес для изображения размером 64x64 с прозрачным фоном, используемого в качестве значка для пакета при отображении пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="182ab-165">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="182ab-166">Убедитесь, что этот элемент содержит *прямой URL-адрес изображения*, а не URL-адрес веб-страницы, на которой содержится изображение.</span><span class="sxs-lookup"><span data-stu-id="182ab-166">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="182ab-167">Например, чтобы использовать изображение из GitHub, используйте необработанного файла, URL-адрес, например <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="182ab-167">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="182ab-168">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="182ab-168">requireLicenseAcceptance</span></span>
<span data-ttu-id="182ab-169">Логическое значение, указывающее, должен ли клиент просить потребителя принять условия лицензии перед установкой пакета.</span><span class="sxs-lookup"><span data-stu-id="182ab-169">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="182ab-170">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="182ab-170">developmentDependency</span></span>
<span data-ttu-id="182ab-171">*(Версия 2.8 и более поздние)* Логическое значение, указывающее, помечен ли пакет как зависимость только для разработки, что позволяет запретить его включение в качестве зависимости в другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="182ab-171">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="182ab-172">С помощью PackageReference (NuGet 4.8 +) этот флаг также означает, что исключает средств компиляции от компиляции.</span><span class="sxs-lookup"><span data-stu-id="182ab-172">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="182ab-173">См. в разделе [DevelopmentDependency поддержка формата PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="182ab-173">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="182ab-174">сводка</span><span class="sxs-lookup"><span data-stu-id="182ab-174">summary</span></span>
<span data-ttu-id="182ab-175">Краткое описание пакета для отображения пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="182ab-175">A short description of the package for UI display.</span></span> <span data-ttu-id="182ab-176">Если этот элемент опущен, используется сокращенная версия элемента `description`.</span><span class="sxs-lookup"><span data-stu-id="182ab-176">If omitted, a truncated version of `description` is used.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="182ab-177">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="182ab-177">releaseNotes</span></span>
<span data-ttu-id="182ab-178">*(Версия 1.5 и более поздние)* Описание изменений, внесенных в этом выпуске пакета NuGet; часто используется в пользовательском интерфейсе как вкладка **Обновления** диспетчера пакетов Visual Studio вместо описания пакета.</span><span class="sxs-lookup"><span data-stu-id="182ab-178">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

#### <a name="copyright"></a><span data-ttu-id="182ab-179">авторские права</span><span class="sxs-lookup"><span data-stu-id="182ab-179">copyright</span></span>
<span data-ttu-id="182ab-180">*(Версия 1.5 и более поздние)* Сведения об авторских правах для пакета.</span><span class="sxs-lookup"><span data-stu-id="182ab-180">*(1.5+)* Copyright details for the package.</span></span>

#### <a name="language"></a><span data-ttu-id="182ab-181">язык</span><span class="sxs-lookup"><span data-stu-id="182ab-181">language</span></span>
<span data-ttu-id="182ab-182">Идентификатор языкового стандарта для пакета.</span><span class="sxs-lookup"><span data-stu-id="182ab-182">The locale ID for the package.</span></span> <span data-ttu-id="182ab-183">См. раздел [Создание локализованных пакетов](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="182ab-183">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="182ab-184">теги</span><span class="sxs-lookup"><span data-stu-id="182ab-184">tags</span></span>
<span data-ttu-id="182ab-185">Список разделенных пробелами тегов и ключевых слов, описывающих пакет NuGet и помогающих находить пакеты NuGet с помощью функций поиска и фильтрации.</span><span class="sxs-lookup"><span data-stu-id="182ab-185">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

#### <a name="serviceable"></a><span data-ttu-id="182ab-186">обслуживанию</span><span class="sxs-lookup"><span data-stu-id="182ab-186">serviceable</span></span> 
<span data-ttu-id="182ab-187">*(Версия 3.3 и более поздние)* Только для внутреннего использования в NuGet.</span><span class="sxs-lookup"><span data-stu-id="182ab-187">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="182ab-188">репозиторий</span><span class="sxs-lookup"><span data-stu-id="182ab-188">repository</span></span>
<span data-ttu-id="182ab-189">Репозиторий метаданных, состоящий из четыре необязательных атрибута: *тип* и *URL-адрес* *(4.0 или более поздней)* , и *ветви* и  *фиксации* *(4.6 или более поздней)* .</span><span class="sxs-lookup"><span data-stu-id="182ab-189">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="182ab-190">Эти атрибуты позволяют сопоставлять файла nupkg в репозиторий, построении, с потенциально могут стать как описано, как отдельные ветви или фиксации, который создан пакет.</span><span class="sxs-lookup"><span data-stu-id="182ab-190">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="182ab-191">Это должен быть общедоступным URL-адрес, который может вызываться напрямую по для управления версиями.</span><span class="sxs-lookup"><span data-stu-id="182ab-191">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="182ab-192">Он не должно быть HTML-страницы, как это предназначено для компьютера.</span><span class="sxs-lookup"><span data-stu-id="182ab-192">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="182ab-193">Для связывания страницу проекта, используйте `projectUrl` , вместо этого поле.</span><span class="sxs-lookup"><span data-stu-id="182ab-193">For linking to project page, use the `projectUrl` field, instead.</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="182ab-194">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="182ab-194">minClientVersion</span></span>
<span data-ttu-id="182ab-195">Указывает минимальную версию клиента NuGet, который может установить этот пакет с использованием nuget.exe и диспетчера пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="182ab-195">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="182ab-196">Используется во всех случаях, когда пакет зависит от конкретных функций в файле `.nuspec`, которые были добавлены в определенной версии клиента NuGet.</span><span class="sxs-lookup"><span data-stu-id="182ab-196">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="182ab-197">Например, для пакета, использующего атрибут `developmentDependency`, атрибуту `minClientVersion` необходимо присвоить значение "2.8".</span><span class="sxs-lookup"><span data-stu-id="182ab-197">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="182ab-198">Аналогичным образом, для пакета, использующего элемент `contentFiles` (см. следующий раздел), атрибуту `minClientVersion` необходимо присвоить значение "3.3".</span><span class="sxs-lookup"><span data-stu-id="182ab-198">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="182ab-199">Также обратите внимание, что клиенты NuGet версий, предшествующих 2.5, не распознают этот флаг и поэтому *всегда* отклоняют установку пакета независимо от значения атрибута `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="182ab-199">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="title"></a><span data-ttu-id="182ab-200">заголовок</span><span class="sxs-lookup"><span data-stu-id="182ab-200">title</span></span>
<span data-ttu-id="182ab-201">Отображает понятный заголовок пакета, который может использоваться в пользовательский Интерфейс.</span><span class="sxs-lookup"><span data-stu-id="182ab-201">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="182ab-202">(nuget.org и диспетчера пакетов в Visual Studio больше не показывать заголовок)</span><span class="sxs-lookup"><span data-stu-id="182ab-202">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="182ab-203">Элементы коллекции</span><span class="sxs-lookup"><span data-stu-id="182ab-203">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="182ab-204">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="182ab-204">packageTypes</span></span>
<span data-ttu-id="182ab-205">*(Версия 3.5 и более поздние)* Пустая коллекция или без нескольких элементов `<packageType>`, определяющих тип пакета, если он отличается от обычного пакета зависимостей.</span><span class="sxs-lookup"><span data-stu-id="182ab-205">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="182ab-206">Каждый элемент packageType имеет атрибуты *name* и *version*.</span><span class="sxs-lookup"><span data-stu-id="182ab-206">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="182ab-207">См. раздел [Указание типа пакета](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="182ab-207">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="182ab-208">зависимости</span><span class="sxs-lookup"><span data-stu-id="182ab-208">dependencies</span></span>
<span data-ttu-id="182ab-209">Коллекция из нуля или более элементов `<dependency>`, задающих зависимости для пакета.</span><span class="sxs-lookup"><span data-stu-id="182ab-209">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="182ab-210">Каждый элемент dependency имеет атрибуты *id*, *version*, *include* (версия 3.x и более поздние) и *exclude* (версия 3.x и более поздние).</span><span class="sxs-lookup"><span data-stu-id="182ab-210">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="182ab-211">См. раздел [Зависимости](#dependencies-element) далее.</span><span class="sxs-lookup"><span data-stu-id="182ab-211">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="182ab-212">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="182ab-212">frameworkAssemblies</span></span>
<span data-ttu-id="182ab-213">*(Версия 1.2 и более поздние)* Коллекция из одного или более элементов `<frameworkAssembly>`, идентифицирующих ссылки на сборки .NET Framework, необходимые для этого пакета, что гарантирует добавление ссылок в проекты, использующие пакет.</span><span class="sxs-lookup"><span data-stu-id="182ab-213">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="182ab-214">Каждый элемент frameworkAssembly имеет атрибуты *assemblyName* и *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="182ab-214">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="182ab-215">См. раздел [Указание ссылок на сборки платформы в глобальном кэше сборок ](#specifying-framework-assembly-references-gac) ниже.</span><span class="sxs-lookup"><span data-stu-id="182ab-215">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="182ab-216">ссылки</span><span class="sxs-lookup"><span data-stu-id="182ab-216">references</span></span>
<span data-ttu-id="182ab-217">*(Версия 1.5 и более поздние)* Коллекция из нуля или более элементов `<reference>`, задающие имена сборок в папке `lib` пакета, которые добавляются в качестве ссылок проекта.</span><span class="sxs-lookup"><span data-stu-id="182ab-217">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="182ab-218">Каждый элемент reference имеет атрибут *file*.</span><span class="sxs-lookup"><span data-stu-id="182ab-218">Each reference has a *file* attribute.</span></span> <span data-ttu-id="182ab-219">Коллекция `<references>` также может содержать элемент `<group>` с атрибутом *targetFramework*, который, в свою очередь, содержит элементы `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="182ab-219">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="182ab-220">Если этот элемент опущен, включаются все ссылки в папке `lib`.</span><span class="sxs-lookup"><span data-stu-id="182ab-220">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="182ab-221">См. раздел [Указание явных ссылок на сборки](#specifying-explicit-assembly-references) ниже.</span><span class="sxs-lookup"><span data-stu-id="182ab-221">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="182ab-222">contentFiles</span><span class="sxs-lookup"><span data-stu-id="182ab-222">contentFiles</span></span>
<span data-ttu-id="182ab-223">*(Версия 3.3 и более поздние)* Коллекция элементов `<files>`, которые идентифицируют файлы содержимого, включаемые в потребляющий проект.</span><span class="sxs-lookup"><span data-stu-id="182ab-223">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="182ab-224">Эти файлы задаются с набором атрибутов, который описывает их использование в системе проекта.</span><span class="sxs-lookup"><span data-stu-id="182ab-224">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="182ab-225">См. раздел [Указание включаемых в пакет файлов](#specifying-files-to-include-in-the-package) ниже.</span><span class="sxs-lookup"><span data-stu-id="182ab-225">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="182ab-226">файлы</span><span class="sxs-lookup"><span data-stu-id="182ab-226">files</span></span> 
<span data-ttu-id="182ab-227">`<package>` Узел может содержать `<files>` узел как одноуровневый элемент `<metadata>`и `<contentFiles>` дочерний элемент в `<metadata>`, чтобы указать, какие файлы сборки и содержимого, следует включить в пакет.</span><span class="sxs-lookup"><span data-stu-id="182ab-227">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="182ab-228">Дополнительные сведения см. далее в разделах [Включение файлов сборки](#including-assembly-files) и [Включение файлов содержимого](#including-content-files) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="182ab-228">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="182ab-229">Замена маркеров</span><span class="sxs-lookup"><span data-stu-id="182ab-229">Replacement tokens</span></span>

<span data-ttu-id="182ab-230">При создании пакета [команда `nuget pack`](../tools/cli-ref-pack.md) заменяет маркеры с разделителями $ в узле `<metadata>` файла `.nuspec` значениями из файла проекта или параметра `-properties` команды `pack`.</span><span class="sxs-lookup"><span data-stu-id="182ab-230">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="182ab-231">Маркеры задаются в командной строке следующим образом: `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="182ab-231">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="182ab-232">Например, вы можете использовать маркер, такой как `$owners$` и `$desc$`, в файле `.nuspec` и предоставить значения во время упаковки следующим образом:</span><span class="sxs-lookup"><span data-stu-id="182ab-232">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="182ab-233">Чтобы использовать значения из проекта, укажите маркеры, описываемые в следующей таблице (AssemblyInfo ссылается на файл в `Properties`, например `AssemblyInfo.cs` или `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="182ab-233">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="182ab-234">Чтобы использовать эти маркеры, выполните команду `nuget pack` с файлом проекта, а не просто с файлом `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="182ab-234">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="182ab-235">Например, при использовании следующей команды маркеры `$id$` и `$version$` в файле `.nuspec` заменяются значениями проекта `AssemblyName` и `AssemblyVersion`:</span><span class="sxs-lookup"><span data-stu-id="182ab-235">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="182ab-236">Как правило, при наличии проекта вы изначально создаете файл `.nuspec` с использованием команды `nuget spec MyProject.csproj`, которая автоматически включает некоторые из этих стандартных маркеров.</span><span class="sxs-lookup"><span data-stu-id="182ab-236">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="182ab-237">Тем не менее, если в проекте отсутствуют значения для обязательных элементов `.nuspec`, команда `nuget pack` завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="182ab-237">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="182ab-238">Кроме того, при изменении значений проекта необходимо выполнить перестроение до создания пакета. Это можно легко сделать с помощью параметра `build` команды pack.</span><span class="sxs-lookup"><span data-stu-id="182ab-238">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="182ab-239">За исключением элемента `$configuration$`, значения в проекте используются в приоритетном порядке относительно любых значений, назначенных тому же маркеру в командной строке.</span><span class="sxs-lookup"><span data-stu-id="182ab-239">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="182ab-240">Токен</span><span class="sxs-lookup"><span data-stu-id="182ab-240">Token</span></span> | <span data-ttu-id="182ab-241">Источник значения</span><span class="sxs-lookup"><span data-stu-id="182ab-241">Value source</span></span> | <span data-ttu-id="182ab-242">Значение</span><span class="sxs-lookup"><span data-stu-id="182ab-242">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="182ab-243">**$id$**</span><span class="sxs-lookup"><span data-stu-id="182ab-243">**$id$**</span></span> | <span data-ttu-id="182ab-244">Файл проекта</span><span class="sxs-lookup"><span data-stu-id="182ab-244">Project file</span></span> | <span data-ttu-id="182ab-245">AssemblyName (заголовок) из файла проекта</span><span class="sxs-lookup"><span data-stu-id="182ab-245">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="182ab-246">**$version$**</span><span class="sxs-lookup"><span data-stu-id="182ab-246">**$version$**</span></span> | <span data-ttu-id="182ab-247">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="182ab-247">AssemblyInfo</span></span> | <span data-ttu-id="182ab-248">AssemblyInformationalVersion, если присутствует, в противном случае AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="182ab-248">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="182ab-249">**$author$**</span><span class="sxs-lookup"><span data-stu-id="182ab-249">**$author$**</span></span> | <span data-ttu-id="182ab-250">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="182ab-250">AssemblyInfo</span></span> | <span data-ttu-id="182ab-251">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="182ab-251">AssemblyCompany</span></span> |
| <span data-ttu-id="182ab-252">**$title$**</span><span class="sxs-lookup"><span data-stu-id="182ab-252">**$title$**</span></span> | <span data-ttu-id="182ab-253">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="182ab-253">AssemblyInfo</span></span> | <span data-ttu-id="182ab-254">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="182ab-254">AssemblyTitle</span></span> |
| <span data-ttu-id="182ab-255">**$description$**</span><span class="sxs-lookup"><span data-stu-id="182ab-255">**$description$**</span></span> | <span data-ttu-id="182ab-256">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="182ab-256">AssemblyInfo</span></span> | <span data-ttu-id="182ab-257">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="182ab-257">AssemblyDescription</span></span> |
| <span data-ttu-id="182ab-258">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="182ab-258">**$copyright$**</span></span> | <span data-ttu-id="182ab-259">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="182ab-259">AssemblyInfo</span></span> | <span data-ttu-id="182ab-260">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="182ab-260">AssemblyCopyright</span></span> |
| <span data-ttu-id="182ab-261">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="182ab-261">**$configuration$**</span></span> | <span data-ttu-id="182ab-262">DLL-файл сборки</span><span class="sxs-lookup"><span data-stu-id="182ab-262">Assembly DLL</span></span> | <span data-ttu-id="182ab-263">Конфигурация, используемая для построения сборки, по умолчанию используется тип отладки.</span><span class="sxs-lookup"><span data-stu-id="182ab-263">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="182ab-264">Обратите внимание, что для создания пакета с помощью конфигурации выпуска в командной строке всегда используется параметр `-properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="182ab-264">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="182ab-265">Маркеры также можно использовать для разрешения путей при включении [файлов сборок](#including-assembly-files) и [файлов содержимого](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="182ab-265">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="182ab-266">Маркеры имеют те же имена, что и свойства MSBuild, что позволяет выбирать файлы для включения в зависимости в текущей конфигурации построения.</span><span class="sxs-lookup"><span data-stu-id="182ab-266">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="182ab-267">Например, если вы используете следующие маркеры в файле `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="182ab-267">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="182ab-268">И выполняете построение сборки, для которой `AssemblyName` имеет значение `LoggingLibrary` с конфигурацией `Release` в MSBuild, в файле `.nuspec` в пакете будут присутствовать следующие строки:</span><span class="sxs-lookup"><span data-stu-id="182ab-268">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="182ab-269">Dependencies-элемент</span><span class="sxs-lookup"><span data-stu-id="182ab-269">Dependencies element</span></span>

<span data-ttu-id="182ab-270">Элемент `<dependencies>` внутри элемента `<metadata>` содержит любое число элементов `<dependency>`, идентифицирующих другие пакеты, от которых зависит пакет верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="182ab-270">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="182ab-271">Ниже перечислены атрибуты каждого элемента `<dependency>`:</span><span class="sxs-lookup"><span data-stu-id="182ab-271">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="182ab-272">Атрибут</span><span class="sxs-lookup"><span data-stu-id="182ab-272">Attribute</span></span> | <span data-ttu-id="182ab-273">Описание</span><span class="sxs-lookup"><span data-stu-id="182ab-273">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="182ab-274">Идентификатор пакета зависимости, например EntityFramework и NUnit, являющийся именем пакета nuget.org, показан на странице пакета (обязательно).</span><span class="sxs-lookup"><span data-stu-id="182ab-274">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="182ab-275">Диапазон версий, которые допустимы в качестве зависимости (обязательно).</span><span class="sxs-lookup"><span data-stu-id="182ab-275">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="182ab-276">Точный синтаксис см. в разделе [Управление версиями пакета](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="182ab-276">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="182ab-277">include</span><span class="sxs-lookup"><span data-stu-id="182ab-277">include</span></span> | <span data-ttu-id="182ab-278">Разделенный запятыми список тегов включения или исключения (см. ниже), определяющий зависимости, включаемые в конечный пакет.</span><span class="sxs-lookup"><span data-stu-id="182ab-278">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="182ab-279">Значение по умолчанию — `all`.</span><span class="sxs-lookup"><span data-stu-id="182ab-279">The default value is `all`.</span></span> |
| <span data-ttu-id="182ab-280">exclude</span><span class="sxs-lookup"><span data-stu-id="182ab-280">exclude</span></span> | <span data-ttu-id="182ab-281">Разделенный запятыми список тегов включения или исключения (см. ниже), определяющий зависимости, исключаемые из конечного пакета.</span><span class="sxs-lookup"><span data-stu-id="182ab-281">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="182ab-282">Значение по умолчанию — `build,analyzers` которого может быть возможна перезапись.</span><span class="sxs-lookup"><span data-stu-id="182ab-282">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="182ab-283">Но `content/ ContentFiles` исключаются также неявно в окончательный пакет, который не может быть возможна перезапись.</span><span class="sxs-lookup"><span data-stu-id="182ab-283">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="182ab-284">Теги в свойстве `exclude` имеют приоритет перед тегами в свойстве `include`.</span><span class="sxs-lookup"><span data-stu-id="182ab-284">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="182ab-285">Например, `include="runtime, compile" exclude="compile"` равносильно `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="182ab-285">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="182ab-286">Тег включения или исключения</span><span class="sxs-lookup"><span data-stu-id="182ab-286">Include/Exclude tag</span></span> | <span data-ttu-id="182ab-287">Затрагиваемые папки пакета</span><span class="sxs-lookup"><span data-stu-id="182ab-287">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="182ab-288">contentFiles</span><span class="sxs-lookup"><span data-stu-id="182ab-288">contentFiles</span></span> | <span data-ttu-id="182ab-289">Content</span><span class="sxs-lookup"><span data-stu-id="182ab-289">Content</span></span> |
| <span data-ttu-id="182ab-290">исполняющая среда</span><span class="sxs-lookup"><span data-stu-id="182ab-290">runtime</span></span> | <span data-ttu-id="182ab-291">Runtime, Resources и FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="182ab-291">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="182ab-292">compile</span><span class="sxs-lookup"><span data-stu-id="182ab-292">compile</span></span> | <span data-ttu-id="182ab-293">lib</span><span class="sxs-lookup"><span data-stu-id="182ab-293">lib</span></span> |
| <span data-ttu-id="182ab-294">выполнить сборку</span><span class="sxs-lookup"><span data-stu-id="182ab-294">build</span></span> | <span data-ttu-id="182ab-295">build (свойства и цели MSBuild)</span><span class="sxs-lookup"><span data-stu-id="182ab-295">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="182ab-296">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="182ab-296">native</span></span> | <span data-ttu-id="182ab-297">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="182ab-297">native</span></span> |
| <span data-ttu-id="182ab-298">none</span><span class="sxs-lookup"><span data-stu-id="182ab-298">none</span></span> | <span data-ttu-id="182ab-299">Нет</span><span class="sxs-lookup"><span data-stu-id="182ab-299">No folders</span></span> |
| <span data-ttu-id="182ab-300">все</span><span class="sxs-lookup"><span data-stu-id="182ab-300">all</span></span> | <span data-ttu-id="182ab-301">Все папки</span><span class="sxs-lookup"><span data-stu-id="182ab-301">All folders</span></span> |

<span data-ttu-id="182ab-302">Например, следующие строки указывают зависимости от `PackageA` версии 1.1.0 или более поздней и `PackageB` версии 1.x.</span><span class="sxs-lookup"><span data-stu-id="182ab-302">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="182ab-303">Следующие строки указывают зависимости от тех же пакетов и включают папки `contentFiles` и `build` для `PackageA`, а также все папки, кроме `native` и `compile`, для `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="182ab-303">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="182ab-304">Примечание. При создании `.nuspec` из проекта с помощью `nuget spec`, зависимости, существующие в проекте автоматически включаются в итоговый `.nuspec` файл.</span><span class="sxs-lookup"><span data-stu-id="182ab-304">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="182ab-305">Группы зависимостей</span><span class="sxs-lookup"><span data-stu-id="182ab-305">Dependency groups</span></span>

<span data-ttu-id="182ab-306">*Версия 2.0 и более поздние*</span><span class="sxs-lookup"><span data-stu-id="182ab-306">*Version 2.0+*</span></span>

<span data-ttu-id="182ab-307">В качестве альтернативы простому неструктурированному списку зависимости могут задаваться в соответствии с профилем платформы целевого проекта с использованием элементов `<group>` в элементе `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="182ab-307">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="182ab-308">Каждый элемент group имеет атрибут `targetFramework` и содержит ноль или более элементов `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="182ab-308">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="182ab-309">Эти зависимости устанавливаются вместе в том случае, если целевая платформа совместима с профилем платформы проекта.</span><span class="sxs-lookup"><span data-stu-id="182ab-309">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="182ab-310">Элемент `<group>` без атрибута `targetFramework` используется в качестве установленного по умолчанию или резервного списка зависимостей.</span><span class="sxs-lookup"><span data-stu-id="182ab-310">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="182ab-311">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="182ab-311">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="182ab-312">Формат группы не может смешиваться с неструктурированным списком.</span><span class="sxs-lookup"><span data-stu-id="182ab-312">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="182ab-313">В следующем примере приводятся различные варианты элемента `<group>`:</span><span class="sxs-lookup"><span data-stu-id="182ab-313">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="182ab-314">Явные ссылки на сборку</span><span class="sxs-lookup"><span data-stu-id="182ab-314">Explicit assembly references</span></span>

<span data-ttu-id="182ab-315">`<references>` Элемент используется проекты, использующие `packages.config` для явного указания сборок, которые целевой проект должен ссылаться при использовании пакета.</span><span class="sxs-lookup"><span data-stu-id="182ab-315">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="182ab-316">Явные ссылки обычно применяются для сборок, используемых только во время разработки.</span><span class="sxs-lookup"><span data-stu-id="182ab-316">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="182ab-317">Дополнительные сведения см. на странице на [Выбор сборок, указанных в проектах](../create-packages/select-assemblies-referenced-by-projects.md) Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="182ab-317">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="182ab-318">Например, следующий элемент `<references>` указывает NuGet на необходимость добавлять ссылки только на сборки `xunit.dll` и `xunit.extensions.dll`, даже если в пакете есть другие сборки:</span><span class="sxs-lookup"><span data-stu-id="182ab-318">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="182ab-319">Группы ссылок</span><span class="sxs-lookup"><span data-stu-id="182ab-319">Reference groups</span></span>

<span data-ttu-id="182ab-320">В качестве альтернативы простому неструктурированному списку ссылки могут задаваться в соответствии с профилем платформы целевого проекта с использованием элементов `<group>` в элементе `<references>`.</span><span class="sxs-lookup"><span data-stu-id="182ab-320">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="182ab-321">Каждый элемент group имеет атрибут `targetFramework` и содержит ноль или более элементов `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="182ab-321">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="182ab-322">Эти ссылки добавляются в проект в том случае, если целевая платформа совместима с профилем платформы проекта.</span><span class="sxs-lookup"><span data-stu-id="182ab-322">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="182ab-323">Элемент `<group>` без атрибута `targetFramework` используется в качестве установленного по умолчанию или резервного списка ссылок.</span><span class="sxs-lookup"><span data-stu-id="182ab-323">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="182ab-324">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="182ab-324">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="182ab-325">Формат группы не может смешиваться с неструктурированным списком.</span><span class="sxs-lookup"><span data-stu-id="182ab-325">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="182ab-326">В следующем примере приводятся различные варианты элемента `<group>`:</span><span class="sxs-lookup"><span data-stu-id="182ab-326">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="182ab-327">Ссылки на сборку платформы</span><span class="sxs-lookup"><span data-stu-id="182ab-327">Framework assembly references</span></span>

<span data-ttu-id="182ab-328">Сборки платформы входят в состав .NET Framework и должны находиться в глобальном кэше сборок любого заданного компьютера.</span><span class="sxs-lookup"><span data-stu-id="182ab-328">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="182ab-329">Идентифицируя такие сборки с помощью элемента `<frameworkAssemblies>`, пакет может гарантировать, что ссылки, отсутствующие в проекте, будут при необходимости добавлены в него.</span><span class="sxs-lookup"><span data-stu-id="182ab-329">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="182ab-330">Естественно, напрямую в пакет такие сборки не включаются.</span><span class="sxs-lookup"><span data-stu-id="182ab-330">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="182ab-331">Элемент `<frameworkAssemblies>` содержит ноль или более элементов `<frameworkAssembly>`, каждый из которых задает следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="182ab-331">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="182ab-332">Атрибут</span><span class="sxs-lookup"><span data-stu-id="182ab-332">Attribute</span></span> | <span data-ttu-id="182ab-333">Описание</span><span class="sxs-lookup"><span data-stu-id="182ab-333">Description</span></span> |
| --- | --- |
| <span data-ttu-id="182ab-334">**имя_сборки**</span><span class="sxs-lookup"><span data-stu-id="182ab-334">**assemblyName**</span></span> | <span data-ttu-id="182ab-335">Полное имя сборки (обязательно).</span><span class="sxs-lookup"><span data-stu-id="182ab-335">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="182ab-336">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="182ab-336">**targetFramework**</span></span> | <span data-ttu-id="182ab-337">Указывает целевую платформу, к которой применяется эта ссылка (необязательно).</span><span class="sxs-lookup"><span data-stu-id="182ab-337">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="182ab-338">Если этот атрибут опущен, указывает, что ссылка применяется ко всем платформам.</span><span class="sxs-lookup"><span data-stu-id="182ab-338">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="182ab-339">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="182ab-339">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="182ab-340">В следующем примере показаны ссылка на `System.Net` для всех целевых платформ и ссылка на `System.ServiceModel` только для платформы .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="182ab-340">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="182ab-341">Включение файлов сборки</span><span class="sxs-lookup"><span data-stu-id="182ab-341">Including assembly files</span></span>

<span data-ttu-id="182ab-342">Если вы придерживаетесь соглашений, описываемых в разделе [Создание пакета](../create-packages/creating-a-package.md), вам не нужно явно задавать список файлов в файле `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="182ab-342">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="182ab-343">Команда `nuget pack` автоматически выбирает необходимые файлы.</span><span class="sxs-lookup"><span data-stu-id="182ab-343">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="182ab-344">Когда пакет устанавливается в проекте, NuGet автоматически добавляет ссылки на библиотеки DLL сборок в пакете, *кроме* тех из них, в именах которых есть `.resources.dll`, так как они считаются локализованными вспомогательными сборками.</span><span class="sxs-lookup"><span data-stu-id="182ab-344">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="182ab-345">По этой причине следует избегать использования `.resources.dll` в именах файлов пакета, которые содержат важный код.</span><span class="sxs-lookup"><span data-stu-id="182ab-345">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="182ab-346">Чтобы обойти такое автоматическое поведение и явно управлять включением сборок в пакет, поместите элемент `<files>` в качестве дочернего для `<package>` (на одном уровне с `<metadata>`), указывая каждый файл с помощью элемента `<file>`.</span><span class="sxs-lookup"><span data-stu-id="182ab-346">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="182ab-347">Например:</span><span class="sxs-lookup"><span data-stu-id="182ab-347">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="182ab-348">В NuGet версии 2.x и более ранних в проектах, использующих `packages.config`, элемент `<files>` также используется для включения неизменяемых файлов содержимого при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="182ab-348">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="182ab-349">В NuGet версии 3.3 и более поздних и проектах PackageReference используется элемент `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="182ab-349">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="182ab-350">Дополнительные сведения см. в разделе [Включение файлов содержимого](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="182ab-350">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="182ab-351">Атрибуты элементов файла</span><span class="sxs-lookup"><span data-stu-id="182ab-351">File element attributes</span></span>

<span data-ttu-id="182ab-352">Каждый элемент `<file>` задает указанные ниже атрибуты:</span><span class="sxs-lookup"><span data-stu-id="182ab-352">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="182ab-353">Атрибут</span><span class="sxs-lookup"><span data-stu-id="182ab-353">Attribute</span></span> | <span data-ttu-id="182ab-354">Описание</span><span class="sxs-lookup"><span data-stu-id="182ab-354">Description</span></span> |
| --- | --- |
| <span data-ttu-id="182ab-355">**src**</span><span class="sxs-lookup"><span data-stu-id="182ab-355">**src**</span></span> | <span data-ttu-id="182ab-356">Расположение файла или файлов, которые требуется включить, с учетом исключений, задаваемых атрибутом `exclude`.</span><span class="sxs-lookup"><span data-stu-id="182ab-356">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="182ab-357">Если не указан абсолютный путь, этот путь задается относительно файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="182ab-357">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="182ab-358">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="182ab-358">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="182ab-359">**target**</span><span class="sxs-lookup"><span data-stu-id="182ab-359">**target**</span></span> | <span data-ttu-id="182ab-360">Относительный путь к папке в пакете, куда помещаются файлы исходного кода. Должен начинаться с `lib`, `content`, `build` или `tools`.</span><span class="sxs-lookup"><span data-stu-id="182ab-360">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="182ab-361">См. раздел [Создание файла NUSPEC на основе рабочего каталога, соответствующего соглашениям](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="182ab-361">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="182ab-362">**exclude**</span><span class="sxs-lookup"><span data-stu-id="182ab-362">**exclude**</span></span> | <span data-ttu-id="182ab-363">Разделенный точками с запятой список файлов или шаблонов файлов, которые исключаются из расположения `src`.</span><span class="sxs-lookup"><span data-stu-id="182ab-363">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="182ab-364">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="182ab-364">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="182ab-365">Примеры</span><span class="sxs-lookup"><span data-stu-id="182ab-365">Examples</span></span>

<span data-ttu-id="182ab-366">**Одна сборка**</span><span class="sxs-lookup"><span data-stu-id="182ab-366">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="182ab-367">**Одна сборка, относящаяся к целевой платформе**</span><span class="sxs-lookup"><span data-stu-id="182ab-367">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="182ab-368">**Набор DLL-файлов с использованием подстановочного знака**</span><span class="sxs-lookup"><span data-stu-id="182ab-368">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="182ab-369">**DLL-файлы для разных платформ**</span><span class="sxs-lookup"><span data-stu-id="182ab-369">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="182ab-370">**Исключение файлов**</span><span class="sxs-lookup"><span data-stu-id="182ab-370">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="182ab-371">Включение файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="182ab-371">Including content files</span></span>

<span data-ttu-id="182ab-372">Файлы содержимого — это неизменяемые файлы, которые пакету необходимо включить в проект.</span><span class="sxs-lookup"><span data-stu-id="182ab-372">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="182ab-373">Такие файлы не подлежат изменению проектом, который потребляет их.</span><span class="sxs-lookup"><span data-stu-id="182ab-373">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="182ab-374">Примеры файлов содержимого:</span><span class="sxs-lookup"><span data-stu-id="182ab-374">Example content files include:</span></span>

- <span data-ttu-id="182ab-375">Изображения, внедряемые в качестве ресурсов</span><span class="sxs-lookup"><span data-stu-id="182ab-375">Images that are embedded as resources</span></span>
- <span data-ttu-id="182ab-376">Файлы исходного кода, которые уже были скомпилированы</span><span class="sxs-lookup"><span data-stu-id="182ab-376">Source files that are already compiled</span></span>
- <span data-ttu-id="182ab-377">Скрипты, которые необходимо включить в выходные данные построения проекта</span><span class="sxs-lookup"><span data-stu-id="182ab-377">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="182ab-378">Файлы конфигурации для пакета, которые необходимо включить в проект, но не требуется изменять в рамках отдельного проекта</span><span class="sxs-lookup"><span data-stu-id="182ab-378">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="182ab-379">Файлы содержимого включаются в проект с помощью элемента `<files>`, задающего папку `content` в атрибуте `target`.</span><span class="sxs-lookup"><span data-stu-id="182ab-379">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="182ab-380">Тем не менее такие файлы игнорируются при установке пакета в проект с использованием PackageReference, в которых вместо этого используется элемент `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="182ab-380">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="182ab-381">Чтобы обеспечить максимальную совместимость с потребляющими проектами, в идеальном случае файлы содержимого следует задавать в проекте с использованием обоих элементов.</span><span class="sxs-lookup"><span data-stu-id="182ab-381">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="182ab-382">Использование элемента files для файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="182ab-382">Using the files element for content files</span></span>

<span data-ttu-id="182ab-383">Для файлов содержимого следует использовать тот же формат, что и для файлов сборки, однако необходимо указать в качестве базовой сборки `content` в атрибуте `target`, как показано в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="182ab-383">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="182ab-384">**Базовые файлы содержимого**</span><span class="sxs-lookup"><span data-stu-id="182ab-384">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="182ab-385">**Файлы содержимого со структурой каталогов**</span><span class="sxs-lookup"><span data-stu-id="182ab-385">**Content files with directory structure**</span></span>

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

<span data-ttu-id="182ab-386">**Файлы содержимого, относящиеся к целевой платформе**</span><span class="sxs-lookup"><span data-stu-id="182ab-386">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="182ab-387">**Файлы содержимого, копируемые в папку с точкой в имени**</span><span class="sxs-lookup"><span data-stu-id="182ab-387">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="182ab-388">В этом случае NuGet определяет, что расширение в атрибуте `target` не соответствует расширению в `src` и обрабатывает такую часть имени в атрибуте `target` как папку:</span><span class="sxs-lookup"><span data-stu-id="182ab-388">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="182ab-389">**Файлы содержимого без расширений**</span><span class="sxs-lookup"><span data-stu-id="182ab-389">**Content files without extensions**</span></span>

<span data-ttu-id="182ab-390">Чтобы включить файлы без расширения, используйте подстановочные знаки `*` или `**`:</span><span class="sxs-lookup"><span data-stu-id="182ab-390">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="182ab-391">**Файлы содержимого с глубоким путем и глубоким целевым объектом**</span><span class="sxs-lookup"><span data-stu-id="182ab-391">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="182ab-392">В этом случае из-за совпадения расширений файлов для исходного и целевого объектов NuGet предполагает, что целевой объект задает имя файла, а не папки:</span><span class="sxs-lookup"><span data-stu-id="182ab-392">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="182ab-393">**Переименование файла содержимого в пакете**</span><span class="sxs-lookup"><span data-stu-id="182ab-393">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="182ab-394">**Исключение файлов**</span><span class="sxs-lookup"><span data-stu-id="182ab-394">**Excluding files**</span></span>

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="182ab-395">Использование элемента contentFiles для файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="182ab-395">Using the contentFiles element for content files</span></span>

<span data-ttu-id="182ab-396">*NuGet 4.0 и более поздней версии с PackageReference*</span><span class="sxs-lookup"><span data-stu-id="182ab-396">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="182ab-397">По умолчанию пакет помещает содержимое в папку `contentFiles` (см. ниже), а команда `nuget pack` включает все файлы в этой папке с использованием установленных по умолчанию атрибутов.</span><span class="sxs-lookup"><span data-stu-id="182ab-397">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="182ab-398">В этом случае включать узел `contentFiles` в файл `.nuspec` не требуется.</span><span class="sxs-lookup"><span data-stu-id="182ab-398">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="182ab-399">Чтобы управлять включаемыми файлами, элемент `<contentFiles>` задает коллекцию элементов `<files>`, которая точно определяет включаемые файлы.</span><span class="sxs-lookup"><span data-stu-id="182ab-399">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="182ab-400">Эти файлы задаются с набором атрибутов, который описывает их использование в системе проекта:</span><span class="sxs-lookup"><span data-stu-id="182ab-400">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="182ab-401">Атрибут</span><span class="sxs-lookup"><span data-stu-id="182ab-401">Attribute</span></span> | <span data-ttu-id="182ab-402">Описание</span><span class="sxs-lookup"><span data-stu-id="182ab-402">Description</span></span> |
| --- | --- |
| <span data-ttu-id="182ab-403">**include**</span><span class="sxs-lookup"><span data-stu-id="182ab-403">**include**</span></span> | <span data-ttu-id="182ab-404">Расположение файла или файлов, которые требуется включить, с учетом исключений, задаваемых атрибутом `exclude` (обязательно).</span><span class="sxs-lookup"><span data-stu-id="182ab-404">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="182ab-405">Если не указан абсолютный путь, этот путь задается относительно файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="182ab-405">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="182ab-406">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="182ab-406">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="182ab-407">**exclude**</span><span class="sxs-lookup"><span data-stu-id="182ab-407">**exclude**</span></span> | <span data-ttu-id="182ab-408">Разделенный точками с запятой список файлов или шаблонов файлов, которые исключаются из расположения `src`.</span><span class="sxs-lookup"><span data-stu-id="182ab-408">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="182ab-409">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="182ab-409">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="182ab-410">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="182ab-410">**buildAction**</span></span> | <span data-ttu-id="182ab-411">Действие построения, назначаемое элементу содержимого для MSBuild, например `Content`, `None`, `Embedded Resource`, `Compile` и т. д. Значение по умолчанию — `Compile`.</span><span class="sxs-lookup"><span data-stu-id="182ab-411">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="182ab-412">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="182ab-412">**copyToOutput**</span></span> | <span data-ttu-id="182ab-413">Логическое значение, указывающее, следует ли копировать элементы содержимого сборки (или публикация) выходную папку.</span><span class="sxs-lookup"><span data-stu-id="182ab-413">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="182ab-414">Значение по умолчанию – false.</span><span class="sxs-lookup"><span data-stu-id="182ab-414">The default is false.</span></span> |
| <span data-ttu-id="182ab-415">**flatten**</span><span class="sxs-lookup"><span data-stu-id="182ab-415">**flatten**</span></span> | <span data-ttu-id="182ab-416">Логическое значение, указывающее на необходимость копировать элементы содержимого в одну папку в выходных данных построения (true) или сохранить структуру папок пакета (false).</span><span class="sxs-lookup"><span data-stu-id="182ab-416">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="182ab-417">Этот параметр применяется, только если для параметра copyToOutput установлено значение true.</span><span class="sxs-lookup"><span data-stu-id="182ab-417">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="182ab-418">Значение по умолчанию – false.</span><span class="sxs-lookup"><span data-stu-id="182ab-418">The default is false.</span></span> |

<span data-ttu-id="182ab-419">При установке пакета NuGet применяет дочерние элементы `<contentFiles>` в порядке сверху вниз.</span><span class="sxs-lookup"><span data-stu-id="182ab-419">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="182ab-420">Если одному файлу соответствует несколько записей, применяются все записи.</span><span class="sxs-lookup"><span data-stu-id="182ab-420">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="182ab-421">При обнаружении конфликтов для одного атрибута запись верхнего уровня переопределяет записи на нижних уровнях.</span><span class="sxs-lookup"><span data-stu-id="182ab-421">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="182ab-422">Структура папки пакета</span><span class="sxs-lookup"><span data-stu-id="182ab-422">Package folder structure</span></span>

<span data-ttu-id="182ab-423">Структурирование содержимого в проекте пакета осуществляется по следующему шаблону:</span><span class="sxs-lookup"><span data-stu-id="182ab-423">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="182ab-424">Элемент `codeLanguages` может иметь значение `cs`, `vb`, `fs`, `any` или любой другой эквивалент заданного `$(ProjectLanguage)` в нижнем регистре</span><span class="sxs-lookup"><span data-stu-id="182ab-424">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="182ab-425">Элемент `TxM` представляет любой допустимый моникер целевой платформы, поддерживаемой NuGet (см. раздел [Целевые платформы](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="182ab-425">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="182ab-426">В конце этого синтаксиса может добавляться любая структура папок.</span><span class="sxs-lookup"><span data-stu-id="182ab-426">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="182ab-427">Например:</span><span class="sxs-lookup"><span data-stu-id="182ab-427">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="182ab-428">Для пустых папок можно использовать `.`, чтобы отказаться от предоставления содержимого для определенных комбинаций языка и моникера целевой платформы, например:</span><span class="sxs-lookup"><span data-stu-id="182ab-428">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="182ab-429">Пример раздела contentFiles</span><span class="sxs-lookup"><span data-stu-id="182ab-429">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="182ab-430">Примеры файлов nuspec</span><span class="sxs-lookup"><span data-stu-id="182ab-430">Example nuspec files</span></span>

<span data-ttu-id="182ab-431">**Простой файл `.nuspec`, в котором не задаются зависимости или файлы**</span><span class="sxs-lookup"><span data-stu-id="182ab-431">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="182ab-432">**Файл `.nuspec` с зависимостями**</span><span class="sxs-lookup"><span data-stu-id="182ab-432">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="182ab-433">**Файл `.nuspec` с файлами**</span><span class="sxs-lookup"><span data-stu-id="182ab-433">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="182ab-434">**Файл `.nuspec` со сборками платформы**</span><span class="sxs-lookup"><span data-stu-id="182ab-434">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="182ab-435">В этом примере для целевых объектов проекта устанавливаются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="182ab-435">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="182ab-436">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="182ab-436">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="182ab-437">Клиентский профиль .NET4 -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="182ab-437">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="182ab-438">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="182ab-438">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="182ab-439">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="182ab-439">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
