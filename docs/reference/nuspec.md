---
title: Ссылка на файл. nuspec для NuGet
description: Файл с расширением .nuspec содержит метаданные пакета, которые используются при построении пакета и предоставляют дополнительную информацию для его потребителей.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 67bc95135f746c4a4685773808756df399cbf01e
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959705"
---
# <a name="nuspec-reference"></a><span data-ttu-id="7b831-103">Справочник по файлу NUSPEC</span><span class="sxs-lookup"><span data-stu-id="7b831-103">.nuspec reference</span></span>

<span data-ttu-id="7b831-104">Файл `.nuspec` представляет собой манифест в формате XML и содержит метаданные пакета.</span><span class="sxs-lookup"><span data-stu-id="7b831-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="7b831-105">Этот манифест используется при построении пакета и содержит дополнительные сведения для его потребителей.</span><span class="sxs-lookup"><span data-stu-id="7b831-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="7b831-106">Манифест всегда включается в пакет.</span><span class="sxs-lookup"><span data-stu-id="7b831-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="7b831-107">В этом разделе.</span><span class="sxs-lookup"><span data-stu-id="7b831-107">In this topic:</span></span>

- [<span data-ttu-id="7b831-108">Общая форма и схема</span><span class="sxs-lookup"><span data-stu-id="7b831-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="7b831-109">[Замена маркеров](#replacement-tokens) (при использовании с проектом Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="7b831-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="7b831-110">Зависимости</span><span class="sxs-lookup"><span data-stu-id="7b831-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="7b831-111">Явные ссылки на сборку</span><span class="sxs-lookup"><span data-stu-id="7b831-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="7b831-112">Ссылки на сборку платформы</span><span class="sxs-lookup"><span data-stu-id="7b831-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="7b831-113">Включение файлов сборки</span><span class="sxs-lookup"><span data-stu-id="7b831-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="7b831-114">Включение файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="7b831-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="7b831-115">Пример файлов nuspec</span><span class="sxs-lookup"><span data-stu-id="7b831-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="7b831-116">Совместимость типов проектов</span><span class="sxs-lookup"><span data-stu-id="7b831-116">Project type compatibility</span></span>

- <span data-ttu-id="7b831-117">Используйте `.nuspec` с `nuget.exe pack` для проектов в стиле, не являющихся SDK `packages.config`, которые используют.</span><span class="sxs-lookup"><span data-stu-id="7b831-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="7b831-118">Файл не требуется для создания пакетов для проектов в [стиле SDK](../resources/check-project-format.md) (обычно это проекты .NET Core и .NET Standard, использующие [атрибут SDK](/dotnet/core/tools/csproj#additions)). `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="7b831-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="7b831-119">(Обратите внимание `.nuspec` , что создается при создании пакета.)</span><span class="sxs-lookup"><span data-stu-id="7b831-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="7b831-120">При создании пакета с `dotnet.exe pack` помощью или `msbuild pack target`рекомендуется включить в файл проекта [все](../reference/msbuild-targets.md#pack-target) `.nuspec` свойства, которые обычно находятся в файле.</span><span class="sxs-lookup"><span data-stu-id="7b831-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="7b831-121">Однако вместо этого можно [использовать `.nuspec` файл для упаковки `dotnet.exe` с помощью или `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="7b831-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="7b831-122">Для проектов, перенесенных из `packages.config` в `.nuspec` [PackageReference](../consume-packages/package-references-in-project-files.md), для создания пакета не требуется файл.</span><span class="sxs-lookup"><span data-stu-id="7b831-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="7b831-123">Вместо этого используйте [MSBuild-т:ПАКК](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="7b831-123">Instead, use [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="7b831-124">Общая форма и схема</span><span class="sxs-lookup"><span data-stu-id="7b831-124">General form and schema</span></span>

<span data-ttu-id="7b831-125">Текущий файл схемы `nuspec.xsd` представлен в [репозитории GitHub для NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="7b831-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="7b831-126">В рамках этой схемы файл `.nuspec` имеет следующую общую форму:</span><span class="sxs-lookup"><span data-stu-id="7b831-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="7b831-127">Чтобы получить наглядное представление схемы, откройте файл в режиме конструктора Visual Studio и щелкните ссылку **Обозреватель схемы XML**.</span><span class="sxs-lookup"><span data-stu-id="7b831-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="7b831-128">Также можно открыть этот файл в виде кода. Для этого щелкните правой кнопкой мыши в редакторе и выберите команду **Показать в обозревателе схемы XML**.</span><span class="sxs-lookup"><span data-stu-id="7b831-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="7b831-129">В любом случае при развертывании большинства узлов схема будет иметь примерно следующий вид:</span><span class="sxs-lookup"><span data-stu-id="7b831-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Обозреватель схемы Visual Studio с открытым файлом nuspec.xsd](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="7b831-131">Обязательные элементы метаданных</span><span class="sxs-lookup"><span data-stu-id="7b831-131">Required metadata elements</span></span>

<span data-ttu-id="7b831-132">Следующие элементы являются минимальным требованием для пакета, однако, несмотря на это, рекомендуется добавить [дополнительные элементы метаданных](#optional-metadata-elements), чтобы оптимизировать работу с вашим пакетом для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="7b831-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="7b831-133">Эти элементы должны использоваться внутри элемента `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="7b831-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="7b831-134">id</span><span class="sxs-lookup"><span data-stu-id="7b831-134">id</span></span> 
<span data-ttu-id="7b831-135">Идентификатор пакета без учета регистра, который должен быть уникальным в пределах сайта nuget.org или иной коллекции, в которой находится пакет.</span><span class="sxs-lookup"><span data-stu-id="7b831-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="7b831-136">Идентификаторы не должны содержать пробелов или символов, которые недопустимы в URL-адресах, и в них должны соблюдаться общие правила касательно пространств имен .NET.</span><span class="sxs-lookup"><span data-stu-id="7b831-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="7b831-137">Инструкции см. в разделе [Выбор уникального идентификатора пакета](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="7b831-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="7b831-138">version</span><span class="sxs-lookup"><span data-stu-id="7b831-138">version</span></span>
<span data-ttu-id="7b831-139">Версия пакета, указываемая согласно шаблону *основной_номер.дополнительный_номер.исправление*.</span><span class="sxs-lookup"><span data-stu-id="7b831-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="7b831-140">Номер версии может включать в себя суффикс предварительной версии, как описано в разделе [Управление версиями пакета](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="7b831-140">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="7b831-141">Описание</span><span class="sxs-lookup"><span data-stu-id="7b831-141">description</span></span>
<span data-ttu-id="7b831-142">Подробное описание пакета для отображения пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="7b831-142">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="7b831-143">authors</span><span class="sxs-lookup"><span data-stu-id="7b831-143">authors</span></span>
<span data-ttu-id="7b831-144">Разделенный запятыми список авторов пакетов, совпадающих с именами профилей на сайте nuget.org. Они отображаются в коллекции NuGet на сайте nuget.org и используются для перекрестных ссылок на пакеты тех же авторов.</span><span class="sxs-lookup"><span data-stu-id="7b831-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="7b831-145">Необязательные элементы метаданных</span><span class="sxs-lookup"><span data-stu-id="7b831-145">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="7b831-146">owners</span><span class="sxs-lookup"><span data-stu-id="7b831-146">owners</span></span>
<span data-ttu-id="7b831-147">Разделенный запятыми список создателей пакета, совпадающих с именами профилей на сайте nuget.org. Часто совпадает со списком в элементе `authors` и игнорируется при загрузке пакета на веб-сайт nuget.org. См. раздел [Управление владельцами пакетов на веб-сайте nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="7b831-147">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="7b831-148">projectUrl</span><span class="sxs-lookup"><span data-stu-id="7b831-148">projectUrl</span></span>
<span data-ttu-id="7b831-149">URL-адрес для домашней страницы пакета, часто указываемый при отображении пользовательского интерфейса, также как и nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7b831-149">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

#### <a name="licenseurl"></a><span data-ttu-id="7b831-150">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="7b831-150">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="7b831-151">licenseUrl является устаревшим.</span><span class="sxs-lookup"><span data-stu-id="7b831-151">licenseUrl is being deprecated.</span></span> <span data-ttu-id="7b831-152">Используйте вместо этого лицензию.</span><span class="sxs-lookup"><span data-stu-id="7b831-152">Use license instead.</span></span>

<span data-ttu-id="7b831-153">URL-адрес для лицензии пакета, часто показанный в пользовательских интерфейсах, таких как nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7b831-153">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

#### <a name="license"></a><span data-ttu-id="7b831-154">лицензии</span><span class="sxs-lookup"><span data-stu-id="7b831-154">license</span></span>
<span data-ttu-id="7b831-155">Выражение лицензии СПДКС или путь к файлу лицензии в пакете, который часто отображается в пользовательских интерфейсах, например nuget.org. Если вы намерены лицензирование пакета с помощью обычной лицензии, например MIT или BSD-2-предложения, используйте соответствующий [идентификатор лицензии спдкс](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="7b831-155">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="7b831-156">Например:</span><span class="sxs-lookup"><span data-stu-id="7b831-156">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="7b831-157">NuGet.org принимает только те лицензионные выражения, которые утверждены инициативой Open Source или Free Software Foundation.</span><span class="sxs-lookup"><span data-stu-id="7b831-157">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="7b831-158">Если пакет лицензирован в нескольких распространенных лицензиях, можно указать составную лицензию с помощью синтаксиса [выражений спдкс версии 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="7b831-158">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="7b831-159">Например:</span><span class="sxs-lookup"><span data-stu-id="7b831-159">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="7b831-160">При использовании пользовательской лицензии, которая не поддерживается в выражениях лицензий, можно упаковать `.txt` файл или `.md` с текстом лицензии.</span><span class="sxs-lookup"><span data-stu-id="7b831-160">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="7b831-161">Например:</span><span class="sxs-lookup"><span data-stu-id="7b831-161">For example:</span></span>

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

<span data-ttu-id="7b831-162">Для эквивалента MSBuild ознакомьтесь с [упаковкой лицензионного выражения или файла лицензии](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="7b831-162">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="7b831-163">Точный синтаксис выражений лицензии NuGet описывается ниже в [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="7b831-163">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="7b831-164">iconUrl</span><span class="sxs-lookup"><span data-stu-id="7b831-164">iconUrl</span></span>
<span data-ttu-id="7b831-165">URL-адрес для изображения размером 64x64 с прозрачным фоном, используемого в качестве значка для пакета при отображении пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="7b831-165">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="7b831-166">Убедитесь, что этот элемент содержит *прямой URL-адрес изображения*, а не URL-адрес веб-страницы, на которой содержится изображение.</span><span class="sxs-lookup"><span data-stu-id="7b831-166">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="7b831-167">Например, чтобы использовать изображение из GitHub, используйте URL-адрес необработанного файла <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>, например.</span><span class="sxs-lookup"><span data-stu-id="7b831-167">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="7b831-168">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="7b831-168">requireLicenseAcceptance</span></span>
<span data-ttu-id="7b831-169">Логическое значение, указывающее, должен ли клиент просить потребителя принять условия лицензии перед установкой пакета.</span><span class="sxs-lookup"><span data-stu-id="7b831-169">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="7b831-170">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="7b831-170">developmentDependency</span></span>
<span data-ttu-id="7b831-171">*(Версия 2.8 и более поздние)* Логическое значение, указывающее, помечен ли пакет как зависимость только для разработки, что позволяет запретить его включение в качестве зависимости в другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="7b831-171">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="7b831-172">При использовании PackageReference (NuGet 4.8 +) этот флаг также означает, что он будет исключать ресурсы времени компиляции из компиляции.</span><span class="sxs-lookup"><span data-stu-id="7b831-172">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="7b831-173">См. раздел [Поддержка DevelopmentDependency для PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) .</span><span class="sxs-lookup"><span data-stu-id="7b831-173">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="7b831-174">сводка</span><span class="sxs-lookup"><span data-stu-id="7b831-174">summary</span></span>
<span data-ttu-id="7b831-175">Краткое описание пакета для отображения пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="7b831-175">A short description of the package for UI display.</span></span> <span data-ttu-id="7b831-176">Если этот элемент опущен, используется сокращенная версия элемента `description`.</span><span class="sxs-lookup"><span data-stu-id="7b831-176">If omitted, a truncated version of `description` is used.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="7b831-177">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="7b831-177">releaseNotes</span></span>
<span data-ttu-id="7b831-178">*(Версия 1.5 и более поздние)* Описание изменений, внесенных в этом выпуске пакета NuGet; часто используется в пользовательском интерфейсе как вкладка **Обновления** диспетчера пакетов Visual Studio вместо описания пакета.</span><span class="sxs-lookup"><span data-stu-id="7b831-178">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

#### <a name="copyright"></a><span data-ttu-id="7b831-179">авторские права</span><span class="sxs-lookup"><span data-stu-id="7b831-179">copyright</span></span>
<span data-ttu-id="7b831-180">*(Версия 1.5 и более поздние)* Сведения об авторских правах для пакета.</span><span class="sxs-lookup"><span data-stu-id="7b831-180">*(1.5+)* Copyright details for the package.</span></span>

#### <a name="language"></a><span data-ttu-id="7b831-181">язык</span><span class="sxs-lookup"><span data-stu-id="7b831-181">language</span></span>
<span data-ttu-id="7b831-182">Идентификатор языкового стандарта для пакета.</span><span class="sxs-lookup"><span data-stu-id="7b831-182">The locale ID for the package.</span></span> <span data-ttu-id="7b831-183">См. раздел [Создание локализованных пакетов](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="7b831-183">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="7b831-184">теги</span><span class="sxs-lookup"><span data-stu-id="7b831-184">tags</span></span>
<span data-ttu-id="7b831-185">Список разделенных пробелами тегов и ключевых слов, описывающих пакет NuGet и помогающих находить пакеты NuGet с помощью функций поиска и фильтрации.</span><span class="sxs-lookup"><span data-stu-id="7b831-185">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

#### <a name="serviceable"></a><span data-ttu-id="7b831-186">обслуживанию</span><span class="sxs-lookup"><span data-stu-id="7b831-186">serviceable</span></span> 
<span data-ttu-id="7b831-187">*(Версия 3.3 и более поздние)* Только для внутреннего использования в NuGet.</span><span class="sxs-lookup"><span data-stu-id="7b831-187">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="7b831-188">репозиторий</span><span class="sxs-lookup"><span data-stu-id="7b831-188">repository</span></span>
<span data-ttu-id="7b831-189">Метаданные репозитория, состоящие из четырех необязательных `type` атрибутов `url` : и *(4.0 +)* `branch` и `commit` и *(4.6 +)* .</span><span class="sxs-lookup"><span data-stu-id="7b831-189">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="7b831-190">Эти атрибуты позволяют сопоставлять объект `.nupkg` с репозиторием, в котором он построен, с возможностью получения таких сведений, как имя отдельной ветви и/или фиксация хэша SHA-1, который создал пакет.</span><span class="sxs-lookup"><span data-stu-id="7b831-190">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="7b831-191">Это должен быть общедоступный URL-адрес, который может вызываться непосредственно программным обеспечением управления версиями.</span><span class="sxs-lookup"><span data-stu-id="7b831-191">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="7b831-192">Это не должна быть HTML-страница, так как она предназначена для компьютера.</span><span class="sxs-lookup"><span data-stu-id="7b831-192">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="7b831-193">Для ссылки на страницу проекта используйте `projectUrl` вместо этого поле.</span><span class="sxs-lookup"><span data-stu-id="7b831-193">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="7b831-194">Например:</span><span class="sxs-lookup"><span data-stu-id="7b831-194">For example:</span></span>
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2016/06/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

#### <a name="title"></a><span data-ttu-id="7b831-195">заголовок</span><span class="sxs-lookup"><span data-stu-id="7b831-195">title</span></span>
<span data-ttu-id="7b831-196">Удобное для человека название пакета, которое может использоваться в некоторых интерфейсах пользователя.</span><span class="sxs-lookup"><span data-stu-id="7b831-196">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="7b831-197">(nuget.org и диспетчер пакетов в Visual Studio не отображают заголовок)</span><span class="sxs-lookup"><span data-stu-id="7b831-197">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="7b831-198">Элементы коллекции</span><span class="sxs-lookup"><span data-stu-id="7b831-198">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="7b831-199">Элемента packagetypes</span><span class="sxs-lookup"><span data-stu-id="7b831-199">packageTypes</span></span>
<span data-ttu-id="7b831-200">*(Версия 3.5 и более поздние)* Пустая коллекция или без нескольких элементов `<packageType>`, определяющих тип пакета, если он отличается от обычного пакета зависимостей.</span><span class="sxs-lookup"><span data-stu-id="7b831-200">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="7b831-201">Каждый элемент packageType имеет атрибуты *name* и *version*.</span><span class="sxs-lookup"><span data-stu-id="7b831-201">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="7b831-202">См. раздел [Указание типа пакета](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="7b831-202">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="7b831-203">зависимости</span><span class="sxs-lookup"><span data-stu-id="7b831-203">dependencies</span></span>
<span data-ttu-id="7b831-204">Коллекция из нуля или более элементов `<dependency>`, задающих зависимости для пакета.</span><span class="sxs-lookup"><span data-stu-id="7b831-204">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="7b831-205">Каждый элемент dependency имеет атрибуты *id*, *version*, *include* (версия 3.x и более поздние) и *exclude* (версия 3.x и более поздние).</span><span class="sxs-lookup"><span data-stu-id="7b831-205">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="7b831-206">См. раздел [Зависимости](#dependencies-element) далее.</span><span class="sxs-lookup"><span data-stu-id="7b831-206">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="7b831-207">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="7b831-207">frameworkAssemblies</span></span>
<span data-ttu-id="7b831-208">*(Версия 1.2 и более поздние)* Коллекция из одного или более элементов `<frameworkAssembly>`, идентифицирующих ссылки на сборки .NET Framework, необходимые для этого пакета, что гарантирует добавление ссылок в проекты, использующие пакет.</span><span class="sxs-lookup"><span data-stu-id="7b831-208">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="7b831-209">Каждый элемент frameworkAssembly имеет атрибуты *assemblyName* и *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="7b831-209">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="7b831-210">См. раздел [Указание ссылок на сборки платформы в глобальном кэше сборок ](#specifying-framework-assembly-references-gac) ниже.</span><span class="sxs-lookup"><span data-stu-id="7b831-210">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="7b831-211">ссылки</span><span class="sxs-lookup"><span data-stu-id="7b831-211">references</span></span>
<span data-ttu-id="7b831-212">*(Версия 1.5 и более поздние)* Коллекция из нуля или более элементов `<reference>`, задающие имена сборок в папке `lib` пакета, которые добавляются в качестве ссылок проекта.</span><span class="sxs-lookup"><span data-stu-id="7b831-212">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="7b831-213">Каждый элемент reference имеет атрибут *file*.</span><span class="sxs-lookup"><span data-stu-id="7b831-213">Each reference has a *file* attribute.</span></span> <span data-ttu-id="7b831-214">Коллекция `<references>` также может содержать элемент `<group>` с атрибутом *targetFramework*, который, в свою очередь, содержит элементы `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="7b831-214">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="7b831-215">Если этот элемент опущен, включаются все ссылки в папке `lib`.</span><span class="sxs-lookup"><span data-stu-id="7b831-215">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="7b831-216">См. раздел [Указание явных ссылок на сборки](#specifying-explicit-assembly-references) ниже.</span><span class="sxs-lookup"><span data-stu-id="7b831-216">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="7b831-217">contentFiles</span><span class="sxs-lookup"><span data-stu-id="7b831-217">contentFiles</span></span>
<span data-ttu-id="7b831-218">*(Версия 3.3 и более поздние)* Коллекция элементов `<files>`, которые идентифицируют файлы содержимого, включаемые в потребляющий проект.</span><span class="sxs-lookup"><span data-stu-id="7b831-218">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="7b831-219">Эти файлы задаются с набором атрибутов, который описывает их использование в системе проекта.</span><span class="sxs-lookup"><span data-stu-id="7b831-219">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="7b831-220">См. раздел [Указание включаемых в пакет файлов](#specifying-files-to-include-in-the-package) ниже.</span><span class="sxs-lookup"><span data-stu-id="7b831-220">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="7b831-221">файлы</span><span class="sxs-lookup"><span data-stu-id="7b831-221">files</span></span> 
<span data-ttu-id="7b831-222">`<package>` Узел может `<metadata>`содержать узел в `<metadata>` качестве`<contentFiles>` одноуровневого элемента для и дочерний элемент в, чтобы указать, какие файлы сборки и содержимого следует включить в пакет. `<files>`</span><span class="sxs-lookup"><span data-stu-id="7b831-222">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="7b831-223">Дополнительные сведения см. далее в разделах [Включение файлов сборки](#including-assembly-files) и [Включение файлов содержимого](#including-content-files) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="7b831-223">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="7b831-224">атрибуты метаданных</span><span class="sxs-lookup"><span data-stu-id="7b831-224">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="7b831-225">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="7b831-225">minClientVersion</span></span>
<span data-ttu-id="7b831-226">Указывает минимальную версию клиента NuGet, который может установить этот пакет с использованием nuget.exe и диспетчера пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b831-226">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="7b831-227">Используется во всех случаях, когда пакет зависит от конкретных функций в файле `.nuspec`, которые были добавлены в определенной версии клиента NuGet.</span><span class="sxs-lookup"><span data-stu-id="7b831-227">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="7b831-228">Например, для пакета, использующего атрибут `developmentDependency`, атрибуту `minClientVersion` необходимо присвоить значение "2.8".</span><span class="sxs-lookup"><span data-stu-id="7b831-228">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="7b831-229">Аналогичным образом, для пакета, использующего элемент `contentFiles` (см. следующий раздел), атрибуту `minClientVersion` необходимо присвоить значение "3.3".</span><span class="sxs-lookup"><span data-stu-id="7b831-229">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="7b831-230">Также обратите внимание, что клиенты NuGet версий, предшествующих 2.5, не распознают этот флаг и поэтому *всегда* отклоняют установку пакета независимо от значения атрибута `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="7b831-230">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/01/nuspec.xsd">
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

## <a name="replacement-tokens"></a><span data-ttu-id="7b831-231">Замена маркеров</span><span class="sxs-lookup"><span data-stu-id="7b831-231">Replacement tokens</span></span>

<span data-ttu-id="7b831-232">При создании пакета [команда `nuget pack`](../reference/cli-reference/cli-ref-pack.md) заменяет маркеры с разделителями $ в узле `<metadata>` файла `.nuspec` значениями из файла проекта или параметра `-properties` команды `pack`.</span><span class="sxs-lookup"><span data-stu-id="7b831-232">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="7b831-233">Маркеры задаются в командной строке следующим образом: `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="7b831-233">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="7b831-234">Например, вы можете использовать маркер, такой как `$owners$` и `$desc$`, в файле `.nuspec` и предоставить значения во время упаковки следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7b831-234">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="7b831-235">Чтобы использовать значения из проекта, укажите маркеры, описываемые в следующей таблице (AssemblyInfo ссылается на файл в `Properties`, например `AssemblyInfo.cs` или `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="7b831-235">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="7b831-236">Чтобы использовать эти маркеры, выполните команду `nuget pack` с файлом проекта, а не просто с файлом `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="7b831-236">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="7b831-237">Например, при использовании следующей команды маркеры `$id$` и `$version$` в файле `.nuspec` заменяются значениями проекта `AssemblyName` и `AssemblyVersion`:</span><span class="sxs-lookup"><span data-stu-id="7b831-237">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="7b831-238">Как правило, при наличии проекта вы изначально создаете файл `.nuspec` с использованием команды `nuget spec MyProject.csproj`, которая автоматически включает некоторые из этих стандартных маркеров.</span><span class="sxs-lookup"><span data-stu-id="7b831-238">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="7b831-239">Тем не менее, если в проекте отсутствуют значения для обязательных элементов `.nuspec`, команда `nuget pack` завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="7b831-239">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="7b831-240">Кроме того, при изменении значений проекта необходимо выполнить перестроение до создания пакета. Это можно легко сделать с помощью параметра `build` команды pack.</span><span class="sxs-lookup"><span data-stu-id="7b831-240">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="7b831-241">За исключением элемента `$configuration$`, значения в проекте используются в приоритетном порядке относительно любых значений, назначенных тому же маркеру в командной строке.</span><span class="sxs-lookup"><span data-stu-id="7b831-241">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="7b831-242">Токен</span><span class="sxs-lookup"><span data-stu-id="7b831-242">Token</span></span> | <span data-ttu-id="7b831-243">Источник значения</span><span class="sxs-lookup"><span data-stu-id="7b831-243">Value source</span></span> | <span data-ttu-id="7b831-244">Значение</span><span class="sxs-lookup"><span data-stu-id="7b831-244">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="7b831-245">**$id$**</span><span class="sxs-lookup"><span data-stu-id="7b831-245">**$id$**</span></span> | <span data-ttu-id="7b831-246">Файл проекта</span><span class="sxs-lookup"><span data-stu-id="7b831-246">Project file</span></span> | <span data-ttu-id="7b831-247">AssemblyName (Title) из файла проекта</span><span class="sxs-lookup"><span data-stu-id="7b831-247">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="7b831-248">**$version$**</span><span class="sxs-lookup"><span data-stu-id="7b831-248">**$version$**</span></span> | <span data-ttu-id="7b831-249">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="7b831-249">AssemblyInfo</span></span> | <span data-ttu-id="7b831-250">AssemblyInformationalVersion, если присутствует, в противном случае AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="7b831-250">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="7b831-251">**$author$**</span><span class="sxs-lookup"><span data-stu-id="7b831-251">**$author$**</span></span> | <span data-ttu-id="7b831-252">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="7b831-252">AssemblyInfo</span></span> | <span data-ttu-id="7b831-253">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="7b831-253">AssemblyCompany</span></span> |
| <span data-ttu-id="7b831-254">**$title $**</span><span class="sxs-lookup"><span data-stu-id="7b831-254">**$title$**</span></span> | <span data-ttu-id="7b831-255">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="7b831-255">AssemblyInfo</span></span> | <span data-ttu-id="7b831-256">ассемблититле</span><span class="sxs-lookup"><span data-stu-id="7b831-256">AssemblyTitle</span></span> |
| <span data-ttu-id="7b831-257">**$description$**</span><span class="sxs-lookup"><span data-stu-id="7b831-257">**$description$**</span></span> | <span data-ttu-id="7b831-258">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="7b831-258">AssemblyInfo</span></span> | <span data-ttu-id="7b831-259">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="7b831-259">AssemblyDescription</span></span> |
| <span data-ttu-id="7b831-260">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="7b831-260">**$copyright$**</span></span> | <span data-ttu-id="7b831-261">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="7b831-261">AssemblyInfo</span></span> | <span data-ttu-id="7b831-262">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="7b831-262">AssemblyCopyright</span></span> |
| <span data-ttu-id="7b831-263">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="7b831-263">**$configuration$**</span></span> | <span data-ttu-id="7b831-264">DLL-файл сборки</span><span class="sxs-lookup"><span data-stu-id="7b831-264">Assembly DLL</span></span> | <span data-ttu-id="7b831-265">Конфигурация, используемая для построения сборки, по умолчанию используется тип отладки.</span><span class="sxs-lookup"><span data-stu-id="7b831-265">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="7b831-266">Обратите внимание, что для создания пакета с помощью конфигурации выпуска в командной строке всегда используется параметр `-properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="7b831-266">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="7b831-267">Маркеры также можно использовать для разрешения путей при включении [файлов сборок](#including-assembly-files) и [файлов содержимого](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="7b831-267">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="7b831-268">Маркеры имеют те же имена, что и свойства MSBuild, что позволяет выбирать файлы для включения в зависимости в текущей конфигурации построения.</span><span class="sxs-lookup"><span data-stu-id="7b831-268">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="7b831-269">Например, если вы используете следующие маркеры в файле `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="7b831-269">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="7b831-270">И выполняете построение сборки, для которой `AssemblyName` имеет значение `LoggingLibrary` с конфигурацией `Release` в MSBuild, в файле `.nuspec` в пакете будут присутствовать следующие строки:</span><span class="sxs-lookup"><span data-stu-id="7b831-270">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="7b831-271">DEPENDENCIES, элемент</span><span class="sxs-lookup"><span data-stu-id="7b831-271">Dependencies element</span></span>

<span data-ttu-id="7b831-272">Элемент `<dependencies>` внутри элемента `<metadata>` содержит любое число элементов `<dependency>`, идентифицирующих другие пакеты, от которых зависит пакет верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="7b831-272">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="7b831-273">Ниже перечислены атрибуты каждого элемента `<dependency>`:</span><span class="sxs-lookup"><span data-stu-id="7b831-273">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="7b831-274">Атрибут</span><span class="sxs-lookup"><span data-stu-id="7b831-274">Attribute</span></span> | <span data-ttu-id="7b831-275">Описание</span><span class="sxs-lookup"><span data-stu-id="7b831-275">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="7b831-276">Идентификатор пакета зависимости, например EntityFramework и NUnit, являющийся именем пакета nuget.org, показан на странице пакета (обязательно).</span><span class="sxs-lookup"><span data-stu-id="7b831-276">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="7b831-277">Диапазон версий, которые допустимы в качестве зависимости (обязательно).</span><span class="sxs-lookup"><span data-stu-id="7b831-277">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="7b831-278">Точный синтаксис см. в разделе [Управление версиями пакета](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="7b831-278">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> <span data-ttu-id="7b831-279">Версии с подстановочными знаками (плавающие) не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="7b831-279">Wildcard (floating) versions are not supported.</span></span> |
| <span data-ttu-id="7b831-280">include</span><span class="sxs-lookup"><span data-stu-id="7b831-280">include</span></span> | <span data-ttu-id="7b831-281">Разделенный запятыми список тегов включения или исключения (см. ниже), определяющий зависимости, включаемые в конечный пакет.</span><span class="sxs-lookup"><span data-stu-id="7b831-281">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="7b831-282">Значение по умолчанию — `all`.</span><span class="sxs-lookup"><span data-stu-id="7b831-282">The default value is `all`.</span></span> |
| <span data-ttu-id="7b831-283">exclude</span><span class="sxs-lookup"><span data-stu-id="7b831-283">exclude</span></span> | <span data-ttu-id="7b831-284">Разделенный запятыми список тегов включения или исключения (см. ниже), определяющий зависимости, исключаемые из конечного пакета.</span><span class="sxs-lookup"><span data-stu-id="7b831-284">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="7b831-285">Значение по умолчанию `build,analyzers` , которое может быть перезаписано.</span><span class="sxs-lookup"><span data-stu-id="7b831-285">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="7b831-286">Но `content/ ContentFiles` также неявно исключаются в окончательном пакете, который не может быть перезаписан.</span><span class="sxs-lookup"><span data-stu-id="7b831-286">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="7b831-287">Теги в свойстве `exclude` имеют приоритет перед тегами в свойстве `include`.</span><span class="sxs-lookup"><span data-stu-id="7b831-287">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="7b831-288">Например, `include="runtime, compile" exclude="compile"` равносильно `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="7b831-288">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="7b831-289">Тег включения или исключения</span><span class="sxs-lookup"><span data-stu-id="7b831-289">Include/Exclude tag</span></span> | <span data-ttu-id="7b831-290">Затрагиваемые папки пакета</span><span class="sxs-lookup"><span data-stu-id="7b831-290">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="7b831-291">contentFiles</span><span class="sxs-lookup"><span data-stu-id="7b831-291">contentFiles</span></span> | <span data-ttu-id="7b831-292">Content</span><span class="sxs-lookup"><span data-stu-id="7b831-292">Content</span></span> |
| <span data-ttu-id="7b831-293">исполняющая среда</span><span class="sxs-lookup"><span data-stu-id="7b831-293">runtime</span></span> | <span data-ttu-id="7b831-294">Runtime, Resources и FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="7b831-294">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="7b831-295">compile</span><span class="sxs-lookup"><span data-stu-id="7b831-295">compile</span></span> | <span data-ttu-id="7b831-296">lib</span><span class="sxs-lookup"><span data-stu-id="7b831-296">lib</span></span> |
| <span data-ttu-id="7b831-297">выполнить сборку</span><span class="sxs-lookup"><span data-stu-id="7b831-297">build</span></span> | <span data-ttu-id="7b831-298">build (свойства и цели MSBuild)</span><span class="sxs-lookup"><span data-stu-id="7b831-298">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="7b831-299">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="7b831-299">native</span></span> | <span data-ttu-id="7b831-300">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="7b831-300">native</span></span> |
| <span data-ttu-id="7b831-301">none</span><span class="sxs-lookup"><span data-stu-id="7b831-301">none</span></span> | <span data-ttu-id="7b831-302">Нет</span><span class="sxs-lookup"><span data-stu-id="7b831-302">No folders</span></span> |
| <span data-ttu-id="7b831-303">все</span><span class="sxs-lookup"><span data-stu-id="7b831-303">all</span></span> | <span data-ttu-id="7b831-304">Все папки</span><span class="sxs-lookup"><span data-stu-id="7b831-304">All folders</span></span> |

<span data-ttu-id="7b831-305">Например, следующие строки указывают зависимости от `PackageA` версии 1.1.0 или более поздней и `PackageB` версии 1.x.</span><span class="sxs-lookup"><span data-stu-id="7b831-305">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="7b831-306">Следующие строки указывают зависимости от тех же пакетов и включают папки `contentFiles` и `build` для `PackageA`, а также все папки, кроме `native` и `compile`, для `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="7b831-306">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="7b831-307">При создании `.nuspec` из проекта с помощью `nuget spec`, зависимости, существующие в этом проекте, не включаются автоматически в результирующий `.nuspec` файл.</span><span class="sxs-lookup"><span data-stu-id="7b831-307">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="7b831-308">Вместо этого используйте `nuget pack myproject.csproj`и получите файл с *расширением nuspec* в созданном nupkgном файле.</span><span class="sxs-lookup"><span data-stu-id="7b831-308">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="7b831-309">Этот *nuspec* содержит зависимости.</span><span class="sxs-lookup"><span data-stu-id="7b831-309">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="7b831-310">Группы зависимостей</span><span class="sxs-lookup"><span data-stu-id="7b831-310">Dependency groups</span></span>

<span data-ttu-id="7b831-311">*Версия 2.0 и более поздние*</span><span class="sxs-lookup"><span data-stu-id="7b831-311">*Version 2.0+*</span></span>

<span data-ttu-id="7b831-312">В качестве альтернативы простому неструктурированному списку зависимости могут задаваться в соответствии с профилем платформы целевого проекта с использованием элементов `<group>` в элементе `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="7b831-312">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="7b831-313">Каждый элемент group имеет атрибут `targetFramework` и содержит ноль или более элементов `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="7b831-313">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="7b831-314">Эти зависимости устанавливаются вместе в том случае, если целевая платформа совместима с профилем платформы проекта.</span><span class="sxs-lookup"><span data-stu-id="7b831-314">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="7b831-315">Элемент `<group>` без атрибута `targetFramework` используется в качестве установленного по умолчанию или резервного списка зависимостей.</span><span class="sxs-lookup"><span data-stu-id="7b831-315">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="7b831-316">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="7b831-316">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="7b831-317">Формат группы не может смешиваться с неструктурированным списком.</span><span class="sxs-lookup"><span data-stu-id="7b831-317">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="7b831-318">В следующем примере приводятся различные варианты элемента `<group>`:</span><span class="sxs-lookup"><span data-stu-id="7b831-318">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="7b831-319">Явные ссылки на сборку</span><span class="sxs-lookup"><span data-stu-id="7b831-319">Explicit assembly references</span></span>

<span data-ttu-id="7b831-320">Элемент используется проектами с `packages.config` целью явного указания сборок, на которые должен ссылаться целевой проект при использовании пакета. `<references>`</span><span class="sxs-lookup"><span data-stu-id="7b831-320">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="7b831-321">Явные ссылки обычно применяются для сборок, используемых только во время разработки.</span><span class="sxs-lookup"><span data-stu-id="7b831-321">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="7b831-322">Дополнительные сведения см. на странице [Выбор сборок, на которые ссылаются проекты](../create-packages/select-assemblies-referenced-by-projects.md) .</span><span class="sxs-lookup"><span data-stu-id="7b831-322">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="7b831-323">Например, следующий элемент `<references>` указывает NuGet на необходимость добавлять ссылки только на сборки `xunit.dll` и `xunit.extensions.dll`, даже если в пакете есть другие сборки:</span><span class="sxs-lookup"><span data-stu-id="7b831-323">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="7b831-324">Группы ссылок</span><span class="sxs-lookup"><span data-stu-id="7b831-324">Reference groups</span></span>

<span data-ttu-id="7b831-325">В качестве альтернативы простому неструктурированному списку ссылки могут задаваться в соответствии с профилем платформы целевого проекта с использованием элементов `<group>` в элементе `<references>`.</span><span class="sxs-lookup"><span data-stu-id="7b831-325">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="7b831-326">Каждый элемент group имеет атрибут `targetFramework` и содержит ноль или более элементов `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="7b831-326">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="7b831-327">Эти ссылки добавляются в проект в том случае, если целевая платформа совместима с профилем платформы проекта.</span><span class="sxs-lookup"><span data-stu-id="7b831-327">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="7b831-328">Элемент `<group>` без атрибута `targetFramework` используется в качестве установленного по умолчанию или резервного списка ссылок.</span><span class="sxs-lookup"><span data-stu-id="7b831-328">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="7b831-329">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="7b831-329">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="7b831-330">Формат группы не может смешиваться с неструктурированным списком.</span><span class="sxs-lookup"><span data-stu-id="7b831-330">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="7b831-331">В следующем примере приводятся различные варианты элемента `<group>`:</span><span class="sxs-lookup"><span data-stu-id="7b831-331">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="7b831-332">Ссылки на сборку платформы</span><span class="sxs-lookup"><span data-stu-id="7b831-332">Framework assembly references</span></span>

<span data-ttu-id="7b831-333">Сборки платформы входят в состав .NET Framework и должны находиться в глобальном кэше сборок любого заданного компьютера.</span><span class="sxs-lookup"><span data-stu-id="7b831-333">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="7b831-334">Идентифицируя такие сборки с помощью элемента `<frameworkAssemblies>`, пакет может гарантировать, что ссылки, отсутствующие в проекте, будут при необходимости добавлены в него.</span><span class="sxs-lookup"><span data-stu-id="7b831-334">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="7b831-335">Естественно, напрямую в пакет такие сборки не включаются.</span><span class="sxs-lookup"><span data-stu-id="7b831-335">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="7b831-336">Элемент `<frameworkAssemblies>` содержит ноль или более элементов `<frameworkAssembly>`, каждый из которых задает следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="7b831-336">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="7b831-337">Атрибут</span><span class="sxs-lookup"><span data-stu-id="7b831-337">Attribute</span></span> | <span data-ttu-id="7b831-338">Описание</span><span class="sxs-lookup"><span data-stu-id="7b831-338">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7b831-339">**имя_сборки**</span><span class="sxs-lookup"><span data-stu-id="7b831-339">**assemblyName**</span></span> | <span data-ttu-id="7b831-340">Полное имя сборки (обязательно).</span><span class="sxs-lookup"><span data-stu-id="7b831-340">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="7b831-341">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="7b831-341">**targetFramework**</span></span> | <span data-ttu-id="7b831-342">Указывает целевую платформу, к которой применяется эта ссылка (необязательно).</span><span class="sxs-lookup"><span data-stu-id="7b831-342">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="7b831-343">Если этот атрибут опущен, указывает, что ссылка применяется ко всем платформам.</span><span class="sxs-lookup"><span data-stu-id="7b831-343">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="7b831-344">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="7b831-344">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="7b831-345">В следующем примере показаны ссылка на `System.Net` для всех целевых платформ и ссылка на `System.ServiceModel` только для платформы .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="7b831-345">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="7b831-346">Включение файлов сборки</span><span class="sxs-lookup"><span data-stu-id="7b831-346">Including assembly files</span></span>

<span data-ttu-id="7b831-347">Если вы придерживаетесь соглашений, описываемых в разделе [Создание пакета](../create-packages/creating-a-package.md), вам не нужно явно задавать список файлов в файле `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="7b831-347">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="7b831-348">Команда `nuget pack` автоматически выбирает необходимые файлы.</span><span class="sxs-lookup"><span data-stu-id="7b831-348">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="7b831-349">Когда пакет устанавливается в проекте, NuGet автоматически добавляет ссылки на библиотеки DLL сборок в пакете, *кроме* тех из них, в именах которых есть `.resources.dll`, так как они считаются локализованными вспомогательными сборками.</span><span class="sxs-lookup"><span data-stu-id="7b831-349">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="7b831-350">По этой причине следует избегать использования `.resources.dll` в именах файлов пакета, которые содержат важный код.</span><span class="sxs-lookup"><span data-stu-id="7b831-350">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="7b831-351">Чтобы обойти такое автоматическое поведение и явно управлять включением сборок в пакет, поместите элемент `<files>` в качестве дочернего для `<package>` (на одном уровне с `<metadata>`), указывая каждый файл с помощью элемента `<file>`.</span><span class="sxs-lookup"><span data-stu-id="7b831-351">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="7b831-352">Например:</span><span class="sxs-lookup"><span data-stu-id="7b831-352">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="7b831-353">В NuGet версии 2.x и более ранних в проектах, использующих `packages.config`, элемент `<files>` также используется для включения неизменяемых файлов содержимого при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="7b831-353">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="7b831-354">В NuGet версии 3.3 и более поздних и проектах PackageReference используется элемент `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="7b831-354">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="7b831-355">Дополнительные сведения см. в разделе [Включение файлов содержимого](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="7b831-355">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="7b831-356">Атрибуты элементов файла</span><span class="sxs-lookup"><span data-stu-id="7b831-356">File element attributes</span></span>

<span data-ttu-id="7b831-357">Каждый элемент `<file>` задает указанные ниже атрибуты:</span><span class="sxs-lookup"><span data-stu-id="7b831-357">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="7b831-358">Атрибут</span><span class="sxs-lookup"><span data-stu-id="7b831-358">Attribute</span></span> | <span data-ttu-id="7b831-359">Описание</span><span class="sxs-lookup"><span data-stu-id="7b831-359">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7b831-360">**src**</span><span class="sxs-lookup"><span data-stu-id="7b831-360">**src**</span></span> | <span data-ttu-id="7b831-361">Расположение файла или файлов, которые требуется включить, с учетом исключений, задаваемых атрибутом `exclude`.</span><span class="sxs-lookup"><span data-stu-id="7b831-361">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="7b831-362">Если не указан абсолютный путь, этот путь задается относительно файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="7b831-362">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="7b831-363">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="7b831-363">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="7b831-364">**target**</span><span class="sxs-lookup"><span data-stu-id="7b831-364">**target**</span></span> | <span data-ttu-id="7b831-365">Относительный путь к папке в пакете, куда помещаются файлы исходного кода. Должен начинаться с `lib`, `content`, `build` или `tools`.</span><span class="sxs-lookup"><span data-stu-id="7b831-365">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="7b831-366">См. раздел [Создание файла NUSPEC на основе рабочего каталога, соответствующего соглашениям](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="7b831-366">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="7b831-367">**exclude**</span><span class="sxs-lookup"><span data-stu-id="7b831-367">**exclude**</span></span> | <span data-ttu-id="7b831-368">Разделенный точками с запятой список файлов или шаблонов файлов, которые исключаются из расположения `src`.</span><span class="sxs-lookup"><span data-stu-id="7b831-368">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="7b831-369">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="7b831-369">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="7b831-370">Примеры</span><span class="sxs-lookup"><span data-stu-id="7b831-370">Examples</span></span>

<span data-ttu-id="7b831-371">**Одна сборка**</span><span class="sxs-lookup"><span data-stu-id="7b831-371">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="7b831-372">**Одна сборка, относящаяся к целевой платформе**</span><span class="sxs-lookup"><span data-stu-id="7b831-372">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="7b831-373">**Набор DLL-файлов с использованием подстановочного знака**</span><span class="sxs-lookup"><span data-stu-id="7b831-373">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="7b831-374">**DLL-файлы для разных платформ**</span><span class="sxs-lookup"><span data-stu-id="7b831-374">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="7b831-375">**Исключение файлов**</span><span class="sxs-lookup"><span data-stu-id="7b831-375">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="7b831-376">Включение файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="7b831-376">Including content files</span></span>

<span data-ttu-id="7b831-377">Файлы содержимого — это неизменяемые файлы, которые пакету необходимо включить в проект.</span><span class="sxs-lookup"><span data-stu-id="7b831-377">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="7b831-378">Такие файлы не подлежат изменению проектом, который потребляет их.</span><span class="sxs-lookup"><span data-stu-id="7b831-378">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="7b831-379">Примеры файлов содержимого:</span><span class="sxs-lookup"><span data-stu-id="7b831-379">Example content files include:</span></span>

- <span data-ttu-id="7b831-380">Изображения, внедряемые в качестве ресурсов</span><span class="sxs-lookup"><span data-stu-id="7b831-380">Images that are embedded as resources</span></span>
- <span data-ttu-id="7b831-381">Файлы исходного кода, которые уже были скомпилированы</span><span class="sxs-lookup"><span data-stu-id="7b831-381">Source files that are already compiled</span></span>
- <span data-ttu-id="7b831-382">Скрипты, которые необходимо включить в выходные данные построения проекта</span><span class="sxs-lookup"><span data-stu-id="7b831-382">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="7b831-383">Файлы конфигурации для пакета, которые необходимо включить в проект, но не требуется изменять в рамках отдельного проекта</span><span class="sxs-lookup"><span data-stu-id="7b831-383">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="7b831-384">Файлы содержимого включаются в проект с помощью элемента `<files>`, задающего папку `content` в атрибуте `target`.</span><span class="sxs-lookup"><span data-stu-id="7b831-384">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="7b831-385">Тем не менее такие файлы игнорируются при установке пакета в проект с использованием PackageReference, в которых вместо этого используется элемент `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="7b831-385">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="7b831-386">Чтобы обеспечить максимальную совместимость с потребляющими проектами, в идеальном случае файлы содержимого следует задавать в проекте с использованием обоих элементов.</span><span class="sxs-lookup"><span data-stu-id="7b831-386">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="7b831-387">Использование элемента files для файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="7b831-387">Using the files element for content files</span></span>

<span data-ttu-id="7b831-388">Для файлов содержимого следует использовать тот же формат, что и для файлов сборки, однако необходимо указать в качестве базовой сборки `content` в атрибуте `target`, как показано в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="7b831-388">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="7b831-389">**Базовые файлы содержимого**</span><span class="sxs-lookup"><span data-stu-id="7b831-389">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="7b831-390">**Файлы содержимого со структурой каталогов**</span><span class="sxs-lookup"><span data-stu-id="7b831-390">**Content files with directory structure**</span></span>

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

<span data-ttu-id="7b831-391">**Файлы содержимого, относящиеся к целевой платформе**</span><span class="sxs-lookup"><span data-stu-id="7b831-391">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="7b831-392">**Файлы содержимого, копируемые в папку с точкой в имени**</span><span class="sxs-lookup"><span data-stu-id="7b831-392">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="7b831-393">В этом случае NuGet определяет, что расширение в атрибуте `target` не соответствует расширению в `src` и обрабатывает такую часть имени в атрибуте `target` как папку:</span><span class="sxs-lookup"><span data-stu-id="7b831-393">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="7b831-394">**Файлы содержимого без расширений**</span><span class="sxs-lookup"><span data-stu-id="7b831-394">**Content files without extensions**</span></span>

<span data-ttu-id="7b831-395">Чтобы включить файлы без расширения, используйте подстановочные знаки `*` или `**`:</span><span class="sxs-lookup"><span data-stu-id="7b831-395">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="7b831-396">**Файлы содержимого с глубоким путем и глубоким целевым объектом**</span><span class="sxs-lookup"><span data-stu-id="7b831-396">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="7b831-397">В этом случае из-за совпадения расширений файлов для исходного и целевого объектов NuGet предполагает, что целевой объект задает имя файла, а не папки:</span><span class="sxs-lookup"><span data-stu-id="7b831-397">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="7b831-398">**Переименование файла содержимого в пакете**</span><span class="sxs-lookup"><span data-stu-id="7b831-398">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="7b831-399">**Исключение файлов**</span><span class="sxs-lookup"><span data-stu-id="7b831-399">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="7b831-400">Использование элемента contentFiles для файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="7b831-400">Using the contentFiles element for content files</span></span>

<span data-ttu-id="7b831-401">*NuGet 4.0 и более поздней версии с PackageReference*</span><span class="sxs-lookup"><span data-stu-id="7b831-401">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="7b831-402">По умолчанию пакет помещает содержимое в папку `contentFiles` (см. ниже), а команда `nuget pack` включает все файлы в этой папке с использованием установленных по умолчанию атрибутов.</span><span class="sxs-lookup"><span data-stu-id="7b831-402">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="7b831-403">В этом случае включать узел `contentFiles` в файл `.nuspec` не требуется.</span><span class="sxs-lookup"><span data-stu-id="7b831-403">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="7b831-404">Чтобы управлять включаемыми файлами, элемент `<contentFiles>` задает коллекцию элементов `<files>`, которая точно определяет включаемые файлы.</span><span class="sxs-lookup"><span data-stu-id="7b831-404">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="7b831-405">Эти файлы задаются с набором атрибутов, который описывает их использование в системе проекта:</span><span class="sxs-lookup"><span data-stu-id="7b831-405">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="7b831-406">Атрибут</span><span class="sxs-lookup"><span data-stu-id="7b831-406">Attribute</span></span> | <span data-ttu-id="7b831-407">Описание</span><span class="sxs-lookup"><span data-stu-id="7b831-407">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7b831-408">**include**</span><span class="sxs-lookup"><span data-stu-id="7b831-408">**include**</span></span> | <span data-ttu-id="7b831-409">Расположение файла или файлов, которые требуется включить, с учетом исключений, задаваемых атрибутом `exclude` (обязательно).</span><span class="sxs-lookup"><span data-stu-id="7b831-409">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="7b831-410">Путь задается относительно `contentFiles` папки, если не указан абсолютный путь.</span><span class="sxs-lookup"><span data-stu-id="7b831-410">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="7b831-411">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="7b831-411">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="7b831-412">**exclude**</span><span class="sxs-lookup"><span data-stu-id="7b831-412">**exclude**</span></span> | <span data-ttu-id="7b831-413">Разделенный точками с запятой список файлов или шаблонов файлов, которые исключаются из расположения `src`.</span><span class="sxs-lookup"><span data-stu-id="7b831-413">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="7b831-414">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="7b831-414">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="7b831-415">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="7b831-415">**buildAction**</span></span> | <span data-ttu-id="7b831-416">Действие построения, назначаемое элементу содержимого для MSBuild, например `Content`, `None`, `Embedded Resource`, `Compile` и т. д. Значение по умолчанию — `Compile`.</span><span class="sxs-lookup"><span data-stu-id="7b831-416">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="7b831-417">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="7b831-417">**copyToOutput**</span></span> | <span data-ttu-id="7b831-418">Логическое значение, указывающее, следует ли копировать элементы содержимого в выходную папку сборки (или публикации).</span><span class="sxs-lookup"><span data-stu-id="7b831-418">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="7b831-419">Значение по умолчанию – false.</span><span class="sxs-lookup"><span data-stu-id="7b831-419">The default is false.</span></span> |
| <span data-ttu-id="7b831-420">**flatten**</span><span class="sxs-lookup"><span data-stu-id="7b831-420">**flatten**</span></span> | <span data-ttu-id="7b831-421">Логическое значение, указывающее на необходимость копировать элементы содержимого в одну папку в выходных данных построения (true) или сохранить структуру папок пакета (false).</span><span class="sxs-lookup"><span data-stu-id="7b831-421">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="7b831-422">Этот параметр применяется, только если для параметра copyToOutput установлено значение true.</span><span class="sxs-lookup"><span data-stu-id="7b831-422">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="7b831-423">Значение по умолчанию – false.</span><span class="sxs-lookup"><span data-stu-id="7b831-423">The default is false.</span></span> |

<span data-ttu-id="7b831-424">При установке пакета NuGet применяет дочерние элементы `<contentFiles>` в порядке сверху вниз.</span><span class="sxs-lookup"><span data-stu-id="7b831-424">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="7b831-425">Если одному файлу соответствует несколько записей, применяются все записи.</span><span class="sxs-lookup"><span data-stu-id="7b831-425">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="7b831-426">При обнаружении конфликтов для одного атрибута запись верхнего уровня переопределяет записи на нижних уровнях.</span><span class="sxs-lookup"><span data-stu-id="7b831-426">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="7b831-427">Структура папки пакета</span><span class="sxs-lookup"><span data-stu-id="7b831-427">Package folder structure</span></span>

<span data-ttu-id="7b831-428">Структурирование содержимого в проекте пакета осуществляется по следующему шаблону:</span><span class="sxs-lookup"><span data-stu-id="7b831-428">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="7b831-429">Элемент `codeLanguages` может иметь значение `cs`, `vb`, `fs`, `any` или любой другой эквивалент заданного `$(ProjectLanguage)` в нижнем регистре</span><span class="sxs-lookup"><span data-stu-id="7b831-429">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="7b831-430">Элемент `TxM` представляет любой допустимый моникер целевой платформы, поддерживаемой NuGet (см. раздел [Целевые платформы](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="7b831-430">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="7b831-431">В конце этого синтаксиса может добавляться любая структура папок.</span><span class="sxs-lookup"><span data-stu-id="7b831-431">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="7b831-432">Например:</span><span class="sxs-lookup"><span data-stu-id="7b831-432">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="7b831-433">Для пустых папок можно использовать `.`, чтобы отказаться от предоставления содержимого для определенных комбинаций языка и моникера целевой платформы, например:</span><span class="sxs-lookup"><span data-stu-id="7b831-433">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="7b831-434">Пример раздела contentFiles</span><span class="sxs-lookup"><span data-stu-id="7b831-434">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="7b831-435">Пример файлов nuspec</span><span class="sxs-lookup"><span data-stu-id="7b831-435">Example nuspec files</span></span>

<span data-ttu-id="7b831-436">**Простой файл `.nuspec`, в котором не задаются зависимости или файлы**</span><span class="sxs-lookup"><span data-stu-id="7b831-436">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="7b831-437">**Файл `.nuspec` с зависимостями**</span><span class="sxs-lookup"><span data-stu-id="7b831-437">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="7b831-438">**Файл `.nuspec` с файлами**</span><span class="sxs-lookup"><span data-stu-id="7b831-438">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="7b831-439">**Файл `.nuspec` со сборками платформы**</span><span class="sxs-lookup"><span data-stu-id="7b831-439">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="7b831-440">В этом примере для целевых объектов проекта устанавливаются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="7b831-440">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="7b831-441">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="7b831-441">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="7b831-442">Клиентский профиль .NET4 -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="7b831-442">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="7b831-443">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="7b831-443">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="7b831-444">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="7b831-444">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
