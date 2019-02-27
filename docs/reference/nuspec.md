---
title: Справочник по файлу nuspec для NuGet
description: Файл с расширением .nuspec содержит метаданные пакета, которые используются при построении пакета и предоставляют дополнительную информацию для его потребителей.
author: karann-msft
ms.author: karann
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: a8be66f5871df260581b6baca8eb7959279d66cd
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852589"
---
# <a name="nuspec-reference"></a><span data-ttu-id="efa10-103">Справочник по файлу NUSPEC</span><span class="sxs-lookup"><span data-stu-id="efa10-103">.nuspec reference</span></span>

<span data-ttu-id="efa10-104">Файл `.nuspec` представляет собой манифест в формате XML и содержит метаданные пакета.</span><span class="sxs-lookup"><span data-stu-id="efa10-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="efa10-105">Этот манифест используется при построении пакета и содержит дополнительные сведения для его потребителей.</span><span class="sxs-lookup"><span data-stu-id="efa10-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="efa10-106">Манифест всегда включается в пакет.</span><span class="sxs-lookup"><span data-stu-id="efa10-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="efa10-107">В этом разделе.</span><span class="sxs-lookup"><span data-stu-id="efa10-107">In this topic:</span></span>

- [<span data-ttu-id="efa10-108">Общая форма и схема</span><span class="sxs-lookup"><span data-stu-id="efa10-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="efa10-109">[Замена маркеров](#replacement-tokens) (при использовании с проектом Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="efa10-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="efa10-110">Зависимости</span><span class="sxs-lookup"><span data-stu-id="efa10-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="efa10-111">Явные ссылки на сборку</span><span class="sxs-lookup"><span data-stu-id="efa10-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="efa10-112">Ссылки на сборку платформы</span><span class="sxs-lookup"><span data-stu-id="efa10-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="efa10-113">Включение файлов сборки</span><span class="sxs-lookup"><span data-stu-id="efa10-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="efa10-114">Включение файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="efa10-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="efa10-115">Примеры файлов nuspec</span><span class="sxs-lookup"><span data-stu-id="efa10-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="general-form-and-schema"></a><span data-ttu-id="efa10-116">Общая форма и схема</span><span class="sxs-lookup"><span data-stu-id="efa10-116">General form and schema</span></span>

<span data-ttu-id="efa10-117">Текущий файл схемы `nuspec.xsd` представлен в [репозитории GitHub для NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="efa10-117">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="efa10-118">В рамках этой схемы файл `.nuspec` имеет следующую общую форму:</span><span class="sxs-lookup"><span data-stu-id="efa10-118">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="efa10-119">Чтобы получить наглядное представление схемы, откройте файл в режиме конструктора Visual Studio и щелкните ссылку **Обозреватель схемы XML**.</span><span class="sxs-lookup"><span data-stu-id="efa10-119">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="efa10-120">Также можно открыть этот файл в виде кода. Для этого щелкните правой кнопкой мыши в редакторе и выберите команду **Показать в обозревателе схемы XML**.</span><span class="sxs-lookup"><span data-stu-id="efa10-120">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="efa10-121">В любом случае при развертывании большинства узлов схема будет иметь примерно следующий вид:</span><span class="sxs-lookup"><span data-stu-id="efa10-121">Either way you get a view like the one below (when mostly expanded):</span></span>

![Обозреватель схемы Visual Studio с открытым файлом nuspec.xsd](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="efa10-123">Обязательные элементы метаданных</span><span class="sxs-lookup"><span data-stu-id="efa10-123">Required metadata elements</span></span>

<span data-ttu-id="efa10-124">Следующие элементы являются минимальным требованием для пакета, однако, несмотря на это, рекомендуется добавить [дополнительные элементы метаданных](#optional-metadata-elements), чтобы оптимизировать работу с вашим пакетом для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="efa10-124">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="efa10-125">Эти элементы должны использоваться внутри элемента `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="efa10-125">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="efa10-126">id</span><span class="sxs-lookup"><span data-stu-id="efa10-126">id</span></span> 
<span data-ttu-id="efa10-127">Идентификатор пакета без учета регистра, который должен быть уникальным в пределах сайта nuget.org или иной коллекции, в которой находится пакет.</span><span class="sxs-lookup"><span data-stu-id="efa10-127">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="efa10-128">Идентификаторы не должны содержать пробелов или символов, которые недопустимы в URL-адресах, и в них должны соблюдаться общие правила касательно пространств имен .NET.</span><span class="sxs-lookup"><span data-stu-id="efa10-128">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="efa10-129">Инструкции см. в разделе [Выбор уникального идентификатора пакета](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="efa10-129">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="efa10-130">version</span><span class="sxs-lookup"><span data-stu-id="efa10-130">version</span></span>
<span data-ttu-id="efa10-131">Версия пакета, указываемая согласно шаблону *основной_номер.дополнительный_номер.исправление*.</span><span class="sxs-lookup"><span data-stu-id="efa10-131">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="efa10-132">Номер версии может включать в себя суффикс предварительной версии, как описано в разделе [Управление версиями пакета](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="efa10-132">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="efa10-133">Описание</span><span class="sxs-lookup"><span data-stu-id="efa10-133">description</span></span>
<span data-ttu-id="efa10-134">Подробное описание пакета для отображения пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="efa10-134">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="efa10-135">authors</span><span class="sxs-lookup"><span data-stu-id="efa10-135">authors</span></span>
<span data-ttu-id="efa10-136">Разделенный запятыми список авторов пакетов, совпадающих с именами профилей на сайте nuget.org. Они отображаются в коллекции NuGet на сайте nuget.org и используются для перекрестных ссылок на пакеты тех же авторов.</span><span class="sxs-lookup"><span data-stu-id="efa10-136">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="efa10-137">Необязательные элементы метаданных</span><span class="sxs-lookup"><span data-stu-id="efa10-137">Optional metadata elements</span></span>

#### <a name="title"></a><span data-ttu-id="efa10-138">заголовок</span><span class="sxs-lookup"><span data-stu-id="efa10-138">title</span></span>
<span data-ttu-id="efa10-139">Понятный заголовок пакета, обычно используемый при отображении пользовательского интерфейса, как на сайте nuget.org и в диспетчере пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="efa10-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="efa10-140">Если значение не указано, используется идентификатор пакета.</span><span class="sxs-lookup"><span data-stu-id="efa10-140">If not specified, the package ID is used.</span></span> 
#### <a name="owners"></a><span data-ttu-id="efa10-141">owners</span><span class="sxs-lookup"><span data-stu-id="efa10-141">owners</span></span>
<span data-ttu-id="efa10-142">Разделенный запятыми список создателей пакета, совпадающих с именами профилей на сайте nuget.org. Часто совпадает со списком в элементе `authors` и игнорируется при загрузке пакета на веб-сайт nuget.org. См. раздел [Управление владельцами пакетов на веб-сайте nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="efa10-142">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 
#### <a name="projecturl"></a><span data-ttu-id="efa10-143">projectUrl</span><span class="sxs-lookup"><span data-stu-id="efa10-143">projectUrl</span></span>
<span data-ttu-id="efa10-144">URL-адрес для домашней страницы пакета, часто указываемый при отображении пользовательского интерфейса, также как и nuget.org.</span><span class="sxs-lookup"><span data-stu-id="efa10-144">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 
#### <a name="licenseurl"></a><span data-ttu-id="efa10-145">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="efa10-145">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="efa10-146">licenseUrl устарел.</span><span class="sxs-lookup"><span data-stu-id="efa10-146">licenseUrl is being deprecated.</span></span> <span data-ttu-id="efa10-147">Вместо этого используйте лицензию.</span><span class="sxs-lookup"><span data-stu-id="efa10-147">Use license instead.</span></span>

<span data-ttu-id="efa10-148">URL-адрес для лицензии пакета, часто указываемый при отображении пользовательского интерфейса, так же как и nuget.org.</span><span class="sxs-lookup"><span data-stu-id="efa10-148">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span>
#### <a name="license"></a><span data-ttu-id="efa10-149">лицензии</span><span class="sxs-lookup"><span data-stu-id="efa10-149">license</span></span>
<span data-ttu-id="efa10-150">Выражение SPDX лицензии или путь к файлу лицензии внутри пакета, часто отображающийся в пользовательском интерфейсе как nuget.org. Если лицензируется пакета распространенных лицензия, например BSD-2-предложение или MIT, используйте связанный идентификатор SPDX лицензии.</span><span class="sxs-lookup"><span data-stu-id="efa10-150">An SPDX license expression or path to a license file within the package, often shown in UI displays as well as nuget.org. If you’re licensing the package under a common license such as BSD-2-Clause or MIT, use the associated SPDX license identifier.</span></span><br><span data-ttu-id="efa10-151">Пример: `<license type="expression">MIT</license>`</span><span class="sxs-lookup"><span data-stu-id="efa10-151">For example: `<license type="expression">MIT</license>`</span></span>

<span data-ttu-id="efa10-152">Ниже приведен полный список [SPDX лицензии идентификаторы](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="efa10-152">Here is the complete list of [SPDX license identifiers](https://spdx.org/licenses/).</span></span> <span data-ttu-id="efa10-153">NuGet.org принимает только OSI или утверждены FSF лицензии при использовании лицензий выражение типа.</span><span class="sxs-lookup"><span data-stu-id="efa10-153">NuGet.org accepts only OSI or FSF approved licenses when using license type expression.</span></span>

<span data-ttu-id="efa10-154">Если ваш пакет лицензируется распространенных сразу несколько лицензий, можно указать составного лицензии с помощью [SPDX выражение синтаксис версии 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="efa10-154">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span><br><span data-ttu-id="efa10-155">Пример: `<license type="expression">BSD-2-Clause OR MIT</license>`</span><span class="sxs-lookup"><span data-stu-id="efa10-155">For example: `<license type="expression">BSD-2-Clause OR MIT</license>`</span></span>

<span data-ttu-id="efa10-156">Если вы используете лицензию, которая не была назначена SPDX идентификатор или он является пользовательской лицензии, вы можете упаковать файл (только `.txt.` или `.md`) с текстом лицензии.</span><span class="sxs-lookup"><span data-stu-id="efa10-156">If you are using a license that hasn’t been assigned an SPDX identifier, or it is a custom license, you can package a file (only `.txt.` or `.md`) with the license text.</span></span> <span data-ttu-id="efa10-157">Пример:</span><span class="sxs-lookup"><span data-stu-id="efa10-157">For example:</span></span>
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

<span data-ttu-id="efa10-158">Для эквивалентных MSBuild, взгляните на [упаковки выражении лицензии или файл лицензии](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="efa10-158">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="efa10-159">Точный синтаксис выражений лицензии NuGet описан ниже в [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="efa10-159">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="efa10-160">iconUrl</span><span class="sxs-lookup"><span data-stu-id="efa10-160">iconUrl</span></span>
<span data-ttu-id="efa10-161">URL-адрес для изображения размером 64x64 с прозрачным фоном, используемого в качестве значка для пакета при отображении пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="efa10-161">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="efa10-162">Убедитесь, что этот элемент содержит *прямой URL-адрес изображения*, а не URL-адрес веб-страницы, на которой содержится изображение.</span><span class="sxs-lookup"><span data-stu-id="efa10-162">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="efa10-163">Например, чтобы использовать изображение из GitHub, используйте необработанного файла, URL-адрес, например <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="efa10-163">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="efa10-164">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="efa10-164">requireLicenseAcceptance</span></span>
<span data-ttu-id="efa10-165">Логическое значение, указывающее, должен ли клиент просить потребителя принять условия лицензии перед установкой пакета.</span><span class="sxs-lookup"><span data-stu-id="efa10-165">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>
#### <a name="developmentdependency"></a><span data-ttu-id="efa10-166">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="efa10-166">developmentDependency</span></span>
<span data-ttu-id="efa10-167">*(Версия 2.8 и более поздние)* Логическое значение, указывающее, помечен ли пакет как зависимость только для разработки, что позволяет запретить его включение в качестве зависимости в другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="efa10-167">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="efa10-168">С помощью PackageReference (NuGet 4.8 +) этот флаг также означает, что исключает средств компиляции от компиляции.</span><span class="sxs-lookup"><span data-stu-id="efa10-168">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="efa10-169">См. в разделе [DevelopmentDependency поддержка формата PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="efa10-169">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>
#### <a name="summary"></a><span data-ttu-id="efa10-170">сводка</span><span class="sxs-lookup"><span data-stu-id="efa10-170">summary</span></span>
<span data-ttu-id="efa10-171">Краткое описание пакета для отображения пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="efa10-171">A short description of the package for UI display.</span></span> <span data-ttu-id="efa10-172">Если этот элемент опущен, используется сокращенная версия элемента `description`.</span><span class="sxs-lookup"><span data-stu-id="efa10-172">If omitted, a truncated version of `description` is used.</span></span>
#### <a name="releasenotes"></a><span data-ttu-id="efa10-173">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="efa10-173">releaseNotes</span></span>
<span data-ttu-id="efa10-174">*(Версия 1.5 и более поздние)* Описание изменений, внесенных в этом выпуске пакета NuGet; часто используется в пользовательском интерфейсе как вкладка **Обновления** диспетчера пакетов Visual Studio вместо описания пакета.</span><span class="sxs-lookup"><span data-stu-id="efa10-174">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>
#### <a name="copyright"></a><span data-ttu-id="efa10-175">авторские права</span><span class="sxs-lookup"><span data-stu-id="efa10-175">copyright</span></span>
<span data-ttu-id="efa10-176">*(Версия 1.5 и более поздние)* Сведения об авторских правах для пакета.</span><span class="sxs-lookup"><span data-stu-id="efa10-176">*(1.5+)* Copyright details for the package.</span></span>
#### <a name="language"></a><span data-ttu-id="efa10-177">язык</span><span class="sxs-lookup"><span data-stu-id="efa10-177">language</span></span>
<span data-ttu-id="efa10-178">Идентификатор языкового стандарта для пакета.</span><span class="sxs-lookup"><span data-stu-id="efa10-178">The locale ID for the package.</span></span> <span data-ttu-id="efa10-179">См. раздел [Создание локализованных пакетов](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="efa10-179">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>
#### <a name="tags"></a><span data-ttu-id="efa10-180">теги</span><span class="sxs-lookup"><span data-stu-id="efa10-180">tags</span></span>
<span data-ttu-id="efa10-181">Список разделенных пробелами тегов и ключевых слов, описывающих пакет NuGet и помогающих находить пакеты NuGet с помощью функций поиска и фильтрации.</span><span class="sxs-lookup"><span data-stu-id="efa10-181">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 
#### <a name="serviceable"></a><span data-ttu-id="efa10-182">обслуживанию</span><span class="sxs-lookup"><span data-stu-id="efa10-182">serviceable</span></span> 
<span data-ttu-id="efa10-183">*(Версия 3.3 и более поздние)* Только для внутреннего использования в NuGet.</span><span class="sxs-lookup"><span data-stu-id="efa10-183">*(3.3+)* For internal NuGet use only.</span></span>
#### <a name="repository"></a><span data-ttu-id="efa10-184">репозиторий</span><span class="sxs-lookup"><span data-stu-id="efa10-184">repository</span></span>
<span data-ttu-id="efa10-185">Репозиторий метаданных, состоящий из четыре необязательных атрибута: *тип* и *URL-адрес* *(4.0 или более поздней)*, и *ветви* и  *фиксации* *(4.6 или более поздней)*.</span><span class="sxs-lookup"><span data-stu-id="efa10-185">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="efa10-186">Эти атрибуты позволяют сопоставлять файла nupkg в репозиторий, построении, с потенциально могут стать как описано, как отдельные ветви или фиксации, который создан пакет.</span><span class="sxs-lookup"><span data-stu-id="efa10-186">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="efa10-187">Это должен быть общедоступным URL-адрес, который может вызываться напрямую по для управления версиями.</span><span class="sxs-lookup"><span data-stu-id="efa10-187">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="efa10-188">Он не должно быть HTML-страницы, как это предназначено для компьютера.</span><span class="sxs-lookup"><span data-stu-id="efa10-188">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="efa10-189">Для связывания страницу проекта, используйте `projectUrl` , вместо этого поле.</span><span class="sxs-lookup"><span data-stu-id="efa10-189">For linking to project page, use the `projectUrl` field, instead.</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="efa10-190">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="efa10-190">minClientVersion</span></span>
<span data-ttu-id="efa10-191">Указывает минимальную версию клиента NuGet, который может установить этот пакет с использованием nuget.exe и диспетчера пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="efa10-191">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="efa10-192">Используется во всех случаях, когда пакет зависит от конкретных функций в файле `.nuspec`, которые были добавлены в определенной версии клиента NuGet.</span><span class="sxs-lookup"><span data-stu-id="efa10-192">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="efa10-193">Например, для пакета, использующего атрибут `developmentDependency`, атрибуту `minClientVersion` необходимо присвоить значение "2.8".</span><span class="sxs-lookup"><span data-stu-id="efa10-193">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="efa10-194">Аналогичным образом, для пакета, использующего элемент `contentFiles` (см. следующий раздел), атрибуту `minClientVersion` необходимо присвоить значение "3.3".</span><span class="sxs-lookup"><span data-stu-id="efa10-194">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="efa10-195">Также обратите внимание, что клиенты NuGet версий, предшествующих 2.5, не распознают этот флаг и поэтому *всегда* отклоняют установку пакета независимо от значения атрибута `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="efa10-195">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="efa10-196">Элементы коллекции</span><span class="sxs-lookup"><span data-stu-id="efa10-196">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="efa10-197">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="efa10-197">packageTypes</span></span>
<span data-ttu-id="efa10-198">*(Версия 3.5 и более поздние)* Пустая коллекция или без нескольких элементов `<packageType>`, определяющих тип пакета, если он отличается от обычного пакета зависимостей.</span><span class="sxs-lookup"><span data-stu-id="efa10-198">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="efa10-199">Каждый элемент packageType имеет атрибуты *name* и *version*.</span><span class="sxs-lookup"><span data-stu-id="efa10-199">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="efa10-200">См. раздел [Указание типа пакета](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="efa10-200">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="efa10-201">зависимости</span><span class="sxs-lookup"><span data-stu-id="efa10-201">dependencies</span></span>
<span data-ttu-id="efa10-202">Коллекция из нуля или более элементов `<dependency>`, задающих зависимости для пакета.</span><span class="sxs-lookup"><span data-stu-id="efa10-202">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="efa10-203">Каждый элемент dependency имеет атрибуты *id*, *version*, *include* (версия 3.x и более поздние) и *exclude* (версия 3.x и более поздние).</span><span class="sxs-lookup"><span data-stu-id="efa10-203">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="efa10-204">См. раздел [Зависимости](#dependencies-element) далее.</span><span class="sxs-lookup"><span data-stu-id="efa10-204">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="efa10-205">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="efa10-205">frameworkAssemblies</span></span>
<span data-ttu-id="efa10-206">*(Версия 1.2 и более поздние)* Коллекция из одного или более элементов `<frameworkAssembly>`, идентифицирующих ссылки на сборки .NET Framework, необходимые для этого пакета, что гарантирует добавление ссылок в проекты, использующие пакет.</span><span class="sxs-lookup"><span data-stu-id="efa10-206">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="efa10-207">Каждый элемент frameworkAssembly имеет атрибуты *assemblyName* и *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="efa10-207">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="efa10-208">См. раздел [Указание ссылок на сборки платформы в глобальном кэше сборок ](#specifying-framework-assembly-references-gac) ниже.</span><span class="sxs-lookup"><span data-stu-id="efa10-208">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="efa10-209">ссылки</span><span class="sxs-lookup"><span data-stu-id="efa10-209">references</span></span>
<span data-ttu-id="efa10-210">*(Версия 1.5 и более поздние)* Коллекция из нуля или более элементов `<reference>`, задающие имена сборок в папке `lib` пакета, которые добавляются в качестве ссылок проекта.</span><span class="sxs-lookup"><span data-stu-id="efa10-210">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="efa10-211">Каждый элемент reference имеет атрибут *file*.</span><span class="sxs-lookup"><span data-stu-id="efa10-211">Each reference has a *file* attribute.</span></span> <span data-ttu-id="efa10-212">Коллекция `<references>` также может содержать элемент `<group>` с атрибутом *targetFramework*, который, в свою очередь, содержит элементы `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="efa10-212">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="efa10-213">Если этот элемент опущен, включаются все ссылки в папке `lib`.</span><span class="sxs-lookup"><span data-stu-id="efa10-213">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="efa10-214">См. раздел [Указание явных ссылок на сборки](#specifying-explicit-assembly-references) ниже.</span><span class="sxs-lookup"><span data-stu-id="efa10-214">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="efa10-215">contentFiles</span><span class="sxs-lookup"><span data-stu-id="efa10-215">contentFiles</span></span>
<span data-ttu-id="efa10-216">*(Версия 3.3 и более поздние)* Коллекция элементов `<files>`, которые идентифицируют файлы содержимого, включаемые в потребляющий проект.</span><span class="sxs-lookup"><span data-stu-id="efa10-216">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="efa10-217">Эти файлы задаются с набором атрибутов, который описывает их использование в системе проекта.</span><span class="sxs-lookup"><span data-stu-id="efa10-217">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="efa10-218">См. раздел [Указание включаемых в пакет файлов](#specifying-files-to-include-in-the-package) ниже.</span><span class="sxs-lookup"><span data-stu-id="efa10-218">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="efa10-219">файлы</span><span class="sxs-lookup"><span data-stu-id="efa10-219">files</span></span> 
<span data-ttu-id="efa10-220">`<package>` Узел может содержать `<files>` узел как одноуровневый элемент `<metadata>`и `<contentFiles>` дочерний элемент в `<metadata>`, чтобы указать, какие файлы сборки и содержимого, следует включить в пакет.</span><span class="sxs-lookup"><span data-stu-id="efa10-220">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="efa10-221">Дополнительные сведения см. далее в разделах [Включение файлов сборки](#including-assembly-files) и [Включение файлов содержимого](#including-content-files) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="efa10-221">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="efa10-222">Замена маркеров</span><span class="sxs-lookup"><span data-stu-id="efa10-222">Replacement tokens</span></span>

<span data-ttu-id="efa10-223">При создании пакета [команда `nuget pack`](../tools/cli-ref-pack.md) заменяет маркеры с разделителями $ в узле `<metadata>` файла `.nuspec` значениями из файла проекта или параметра `-properties` команды `pack`.</span><span class="sxs-lookup"><span data-stu-id="efa10-223">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="efa10-224">Маркеры задаются в командной строке следующим образом: `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="efa10-224">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="efa10-225">Например, вы можете использовать маркер, такой как `$owners$` и `$desc$`, в файле `.nuspec` и предоставить значения во время упаковки следующим образом:</span><span class="sxs-lookup"><span data-stu-id="efa10-225">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="efa10-226">Чтобы использовать значения из проекта, укажите маркеры, описываемые в следующей таблице (AssemblyInfo ссылается на файл в `Properties`, например `AssemblyInfo.cs` или `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="efa10-226">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="efa10-227">Чтобы использовать эти маркеры, выполните команду `nuget pack` с файлом проекта, а не просто с файлом `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="efa10-227">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="efa10-228">Например, при использовании следующей команды маркеры `$id$` и `$version$` в файле `.nuspec` заменяются значениями проекта `AssemblyName` и `AssemblyVersion`:</span><span class="sxs-lookup"><span data-stu-id="efa10-228">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="efa10-229">Как правило, при наличии проекта вы изначально создаете файл `.nuspec` с использованием команды `nuget spec MyProject.csproj`, которая автоматически включает некоторые из этих стандартных маркеров.</span><span class="sxs-lookup"><span data-stu-id="efa10-229">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="efa10-230">Тем не менее, если в проекте отсутствуют значения для обязательных элементов `.nuspec`, команда `nuget pack` завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="efa10-230">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="efa10-231">Кроме того, при изменении значений проекта необходимо выполнить перестроение до создания пакета. Это можно легко сделать с помощью параметра `build` команды pack.</span><span class="sxs-lookup"><span data-stu-id="efa10-231">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="efa10-232">За исключением элемента `$configuration$`, значения в проекте используются в приоритетном порядке относительно любых значений, назначенных тому же маркеру в командной строке.</span><span class="sxs-lookup"><span data-stu-id="efa10-232">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="efa10-233">Токен</span><span class="sxs-lookup"><span data-stu-id="efa10-233">Token</span></span> | <span data-ttu-id="efa10-234">Источник значения</span><span class="sxs-lookup"><span data-stu-id="efa10-234">Value source</span></span> | <span data-ttu-id="efa10-235">Значение</span><span class="sxs-lookup"><span data-stu-id="efa10-235">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="efa10-236">**$id$**</span><span class="sxs-lookup"><span data-stu-id="efa10-236">**$id$**</span></span> | <span data-ttu-id="efa10-237">Файл проекта</span><span class="sxs-lookup"><span data-stu-id="efa10-237">Project file</span></span> | <span data-ttu-id="efa10-238">AssemblyName (заголовок) из файла проекта</span><span class="sxs-lookup"><span data-stu-id="efa10-238">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="efa10-239">**$version$**</span><span class="sxs-lookup"><span data-stu-id="efa10-239">**$version$**</span></span> | <span data-ttu-id="efa10-240">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="efa10-240">AssemblyInfo</span></span> | <span data-ttu-id="efa10-241">AssemblyInformationalVersion, если присутствует, в противном случае AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="efa10-241">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="efa10-242">**$author$**</span><span class="sxs-lookup"><span data-stu-id="efa10-242">**$author$**</span></span> | <span data-ttu-id="efa10-243">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="efa10-243">AssemblyInfo</span></span> | <span data-ttu-id="efa10-244">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="efa10-244">AssemblyCompany</span></span> |
| <span data-ttu-id="efa10-245">**$title$**</span><span class="sxs-lookup"><span data-stu-id="efa10-245">**$title$**</span></span> | <span data-ttu-id="efa10-246">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="efa10-246">AssemblyInfo</span></span> | <span data-ttu-id="efa10-247">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="efa10-247">AssemblyTitle</span></span> |
| <span data-ttu-id="efa10-248">**$description$**</span><span class="sxs-lookup"><span data-stu-id="efa10-248">**$description$**</span></span> | <span data-ttu-id="efa10-249">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="efa10-249">AssemblyInfo</span></span> | <span data-ttu-id="efa10-250">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="efa10-250">AssemblyDescription</span></span> |
| <span data-ttu-id="efa10-251">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="efa10-251">**$copyright$**</span></span> | <span data-ttu-id="efa10-252">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="efa10-252">AssemblyInfo</span></span> | <span data-ttu-id="efa10-253">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="efa10-253">AssemblyCopyright</span></span> |
| <span data-ttu-id="efa10-254">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="efa10-254">**$configuration$**</span></span> | <span data-ttu-id="efa10-255">DLL-файл сборки</span><span class="sxs-lookup"><span data-stu-id="efa10-255">Assembly DLL</span></span> | <span data-ttu-id="efa10-256">Конфигурация, используемая для построения сборки, по умолчанию используется тип отладки.</span><span class="sxs-lookup"><span data-stu-id="efa10-256">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="efa10-257">Обратите внимание, что для создания пакета с помощью конфигурации выпуска в командной строке всегда используется параметр `-properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="efa10-257">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="efa10-258">Маркеры также можно использовать для разрешения путей при включении [файлов сборок](#including-assembly-files) и [файлов содержимого](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="efa10-258">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="efa10-259">Маркеры имеют те же имена, что и свойства MSBuild, что позволяет выбирать файлы для включения в зависимости в текущей конфигурации построения.</span><span class="sxs-lookup"><span data-stu-id="efa10-259">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="efa10-260">Например, если вы используете следующие маркеры в файле `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="efa10-260">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="efa10-261">И выполняете построение сборки, для которой `AssemblyName` имеет значение `LoggingLibrary` с конфигурацией `Release` в MSBuild, в файле `.nuspec` в пакете будут присутствовать следующие строки:</span><span class="sxs-lookup"><span data-stu-id="efa10-261">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="efa10-262">Dependencies-элемент</span><span class="sxs-lookup"><span data-stu-id="efa10-262">Dependencies element</span></span>

<span data-ttu-id="efa10-263">Элемент `<dependencies>` внутри элемента `<metadata>` содержит любое число элементов `<dependency>`, идентифицирующих другие пакеты, от которых зависит пакет верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="efa10-263">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="efa10-264">Ниже перечислены атрибуты каждого элемента `<dependency>`:</span><span class="sxs-lookup"><span data-stu-id="efa10-264">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="efa10-265">Атрибут</span><span class="sxs-lookup"><span data-stu-id="efa10-265">Attribute</span></span> | <span data-ttu-id="efa10-266">Описание</span><span class="sxs-lookup"><span data-stu-id="efa10-266">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="efa10-267">Идентификатор пакета зависимости, например EntityFramework и NUnit, являющийся именем пакета nuget.org, показан на странице пакета (обязательно).</span><span class="sxs-lookup"><span data-stu-id="efa10-267">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="efa10-268">Диапазон версий, которые допустимы в качестве зависимости (обязательно).</span><span class="sxs-lookup"><span data-stu-id="efa10-268">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="efa10-269">Точный синтаксис см. в разделе [Управление версиями пакета](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="efa10-269">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="efa10-270">include</span><span class="sxs-lookup"><span data-stu-id="efa10-270">include</span></span> | <span data-ttu-id="efa10-271">Разделенный запятыми список тегов включения или исключения (см. ниже), определяющий зависимости, включаемые в конечный пакет.</span><span class="sxs-lookup"><span data-stu-id="efa10-271">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="efa10-272">Значение по умолчанию — `all`.</span><span class="sxs-lookup"><span data-stu-id="efa10-272">The default value is `all`.</span></span> |
| <span data-ttu-id="efa10-273">exclude</span><span class="sxs-lookup"><span data-stu-id="efa10-273">exclude</span></span> | <span data-ttu-id="efa10-274">Разделенный запятыми список тегов включения или исключения (см. ниже), определяющий зависимости, исключаемые из конечного пакета.</span><span class="sxs-lookup"><span data-stu-id="efa10-274">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="efa10-275">Значение по умолчанию — `build,analyzers` которого может быть возможна перезапись.</span><span class="sxs-lookup"><span data-stu-id="efa10-275">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="efa10-276">Но `content/ ContentFiles` исключаются также неявно в окончательный пакет, который не может быть возможна перезапись.</span><span class="sxs-lookup"><span data-stu-id="efa10-276">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="efa10-277">Теги в свойстве `exclude` имеют приоритет перед тегами в свойстве `include`.</span><span class="sxs-lookup"><span data-stu-id="efa10-277">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="efa10-278">Например, `include="runtime, compile" exclude="compile"` равносильно `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="efa10-278">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="efa10-279">Тег включения или исключения</span><span class="sxs-lookup"><span data-stu-id="efa10-279">Include/Exclude tag</span></span> | <span data-ttu-id="efa10-280">Затрагиваемые папки пакета</span><span class="sxs-lookup"><span data-stu-id="efa10-280">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="efa10-281">contentFiles</span><span class="sxs-lookup"><span data-stu-id="efa10-281">contentFiles</span></span> | <span data-ttu-id="efa10-282">Content</span><span class="sxs-lookup"><span data-stu-id="efa10-282">Content</span></span> |
| <span data-ttu-id="efa10-283">исполняющая среда</span><span class="sxs-lookup"><span data-stu-id="efa10-283">runtime</span></span> | <span data-ttu-id="efa10-284">Runtime, Resources и FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="efa10-284">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="efa10-285">compile</span><span class="sxs-lookup"><span data-stu-id="efa10-285">compile</span></span> | <span data-ttu-id="efa10-286">lib</span><span class="sxs-lookup"><span data-stu-id="efa10-286">lib</span></span> |
| <span data-ttu-id="efa10-287">выполнить сборку</span><span class="sxs-lookup"><span data-stu-id="efa10-287">build</span></span> | <span data-ttu-id="efa10-288">build (свойства и цели MSBuild)</span><span class="sxs-lookup"><span data-stu-id="efa10-288">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="efa10-289">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="efa10-289">native</span></span> | <span data-ttu-id="efa10-290">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="efa10-290">native</span></span> |
| <span data-ttu-id="efa10-291">Нет</span><span class="sxs-lookup"><span data-stu-id="efa10-291">none</span></span> | <span data-ttu-id="efa10-292">Нет</span><span class="sxs-lookup"><span data-stu-id="efa10-292">No folders</span></span> |
| <span data-ttu-id="efa10-293">все</span><span class="sxs-lookup"><span data-stu-id="efa10-293">all</span></span> | <span data-ttu-id="efa10-294">Все папки</span><span class="sxs-lookup"><span data-stu-id="efa10-294">All folders</span></span> |

<span data-ttu-id="efa10-295">Например, следующие строки указывают зависимости от `PackageA` версии 1.1.0 или более поздней и `PackageB` версии 1.x.</span><span class="sxs-lookup"><span data-stu-id="efa10-295">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="efa10-296">Следующие строки указывают зависимости от тех же пакетов и включают папки `contentFiles` и `build` для `PackageA`, а также все папки, кроме `native` и `compile`, для `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="efa10-296">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="efa10-297">Примечание. При создании `.nuspec` из проекта с помощью `nuget spec`, зависимости, существующие в проекте автоматически включаются в итоговый `.nuspec` файл.</span><span class="sxs-lookup"><span data-stu-id="efa10-297">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="efa10-298">Группы зависимостей</span><span class="sxs-lookup"><span data-stu-id="efa10-298">Dependency groups</span></span>

<span data-ttu-id="efa10-299">*Версия 2.0 и более поздние*</span><span class="sxs-lookup"><span data-stu-id="efa10-299">*Version 2.0+*</span></span>

<span data-ttu-id="efa10-300">В качестве альтернативы простому неструктурированному списку зависимости могут задаваться в соответствии с профилем платформы целевого проекта с использованием элементов `<group>` в элементе `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="efa10-300">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="efa10-301">Каждый элемент group имеет атрибут `targetFramework` и содержит ноль или более элементов `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="efa10-301">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="efa10-302">Эти зависимости устанавливаются вместе в том случае, если целевая платформа совместима с профилем платформы проекта.</span><span class="sxs-lookup"><span data-stu-id="efa10-302">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="efa10-303">Элемент `<group>` без атрибута `targetFramework` используется в качестве установленного по умолчанию или резервного списка зависимостей.</span><span class="sxs-lookup"><span data-stu-id="efa10-303">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="efa10-304">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="efa10-304">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="efa10-305">Формат группы не может смешиваться с неструктурированным списком.</span><span class="sxs-lookup"><span data-stu-id="efa10-305">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="efa10-306">В следующем примере приводятся различные варианты элемента `<group>`:</span><span class="sxs-lookup"><span data-stu-id="efa10-306">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="efa10-307">Явные ссылки на сборку</span><span class="sxs-lookup"><span data-stu-id="efa10-307">Explicit assembly references</span></span>

<span data-ttu-id="efa10-308">Элемент `<references>` явно задает сборки, на которые целевой проект должен ссылаться при использовании пакета.</span><span class="sxs-lookup"><span data-stu-id="efa10-308">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="efa10-309">Если этот элемент присутствует, NuGet добавляет ссылки только на указанные в списке сборки, но не на какие-либо другие сборки в папке `lib` проекта.</span><span class="sxs-lookup"><span data-stu-id="efa10-309">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="efa10-310">Например, следующий элемент `<references>` указывает NuGet на необходимость добавлять ссылки только на сборки `xunit.dll` и `xunit.extensions.dll`, даже если в пакете есть другие сборки:</span><span class="sxs-lookup"><span data-stu-id="efa10-310">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="efa10-311">Явные ссылки обычно применяются для сборок, используемых только во время разработки.</span><span class="sxs-lookup"><span data-stu-id="efa10-311">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="efa10-312">При использовании [контрактов для кода](/dotnet/framework/debug-trace-profile/code-contracts) сборки контракта должны располагаться рядом со сборками среды выполнения, которые они расширяют, чтобы среда Visual Studio могла находить их. При этом не требуются ссылки на сборки контракта из проекта и эти сборки не нужно копировать в папку `bin` проекта.</span><span class="sxs-lookup"><span data-stu-id="efa10-312">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="efa10-313">Аналогичным образом, явные ссылки можно использовать для платформ модульного тестирования, таких как XUnit, сборки средств которых должны располагаться рядом со сборками среды выполнения, но не требуют включения в ссылки проекта.</span><span class="sxs-lookup"><span data-stu-id="efa10-313">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="efa10-314">Группы ссылок</span><span class="sxs-lookup"><span data-stu-id="efa10-314">Reference groups</span></span>

<span data-ttu-id="efa10-315">В качестве альтернативы простому неструктурированному списку ссылки могут задаваться в соответствии с профилем платформы целевого проекта с использованием элементов `<group>` в элементе `<references>`.</span><span class="sxs-lookup"><span data-stu-id="efa10-315">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="efa10-316">Каждый элемент group имеет атрибут `targetFramework` и содержит ноль или более элементов `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="efa10-316">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="efa10-317">Эти ссылки добавляются в проект в том случае, если целевая платформа совместима с профилем платформы проекта.</span><span class="sxs-lookup"><span data-stu-id="efa10-317">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="efa10-318">Элемент `<group>` без атрибута `targetFramework` используется в качестве установленного по умолчанию или резервного списка ссылок.</span><span class="sxs-lookup"><span data-stu-id="efa10-318">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="efa10-319">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="efa10-319">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="efa10-320">Формат группы не может смешиваться с неструктурированным списком.</span><span class="sxs-lookup"><span data-stu-id="efa10-320">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="efa10-321">В следующем примере приводятся различные варианты элемента `<group>`:</span><span class="sxs-lookup"><span data-stu-id="efa10-321">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="efa10-322">Ссылки на сборку платформы</span><span class="sxs-lookup"><span data-stu-id="efa10-322">Framework assembly references</span></span>

<span data-ttu-id="efa10-323">Сборки платформы входят в состав .NET Framework и должны находиться в глобальном кэше сборок любого заданного компьютера.</span><span class="sxs-lookup"><span data-stu-id="efa10-323">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="efa10-324">Идентифицируя такие сборки с помощью элемента `<frameworkAssemblies>`, пакет может гарантировать, что ссылки, отсутствующие в проекте, будут при необходимости добавлены в него.</span><span class="sxs-lookup"><span data-stu-id="efa10-324">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="efa10-325">Естественно, напрямую в пакет такие сборки не включаются.</span><span class="sxs-lookup"><span data-stu-id="efa10-325">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="efa10-326">Элемент `<frameworkAssemblies>` содержит ноль или более элементов `<frameworkAssembly>`, каждый из которых задает следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="efa10-326">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="efa10-327">Атрибут</span><span class="sxs-lookup"><span data-stu-id="efa10-327">Attribute</span></span> | <span data-ttu-id="efa10-328">Описание</span><span class="sxs-lookup"><span data-stu-id="efa10-328">Description</span></span> |
| --- | --- |
| <span data-ttu-id="efa10-329">**имя_сборки**</span><span class="sxs-lookup"><span data-stu-id="efa10-329">**assemblyName**</span></span> | <span data-ttu-id="efa10-330">Полное имя сборки (обязательно).</span><span class="sxs-lookup"><span data-stu-id="efa10-330">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="efa10-331">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="efa10-331">**targetFramework**</span></span> | <span data-ttu-id="efa10-332">Указывает целевую платформу, к которой применяется эта ссылка (необязательно).</span><span class="sxs-lookup"><span data-stu-id="efa10-332">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="efa10-333">Если этот атрибут опущен, указывает, что ссылка применяется ко всем платформам.</span><span class="sxs-lookup"><span data-stu-id="efa10-333">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="efa10-334">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="efa10-334">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="efa10-335">В следующем примере показаны ссылка на `System.Net` для всех целевых платформ и ссылка на `System.ServiceModel` только для платформы .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="efa10-335">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="efa10-336">Включение файлов сборки</span><span class="sxs-lookup"><span data-stu-id="efa10-336">Including assembly files</span></span>

<span data-ttu-id="efa10-337">Если вы придерживаетесь соглашений, описываемых в разделе [Создание пакета](../create-packages/creating-a-package.md), вам не нужно явно задавать список файлов в файле `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="efa10-337">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="efa10-338">Команда `nuget pack` автоматически выбирает необходимые файлы.</span><span class="sxs-lookup"><span data-stu-id="efa10-338">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="efa10-339">Когда пакет устанавливается в проекте, NuGet автоматически добавляет ссылки на библиотеки DLL сборок в пакете, *кроме* тех из них, в именах которых есть `.resources.dll`, так как они считаются локализованными вспомогательными сборками.</span><span class="sxs-lookup"><span data-stu-id="efa10-339">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="efa10-340">По этой причине следует избегать использования `.resources.dll` в именах файлов пакета, которые содержат важный код.</span><span class="sxs-lookup"><span data-stu-id="efa10-340">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="efa10-341">Чтобы обойти такое автоматическое поведение и явно управлять включением сборок в пакет, поместите элемент `<files>` в качестве дочернего для `<package>` (на одном уровне с `<metadata>`), указывая каждый файл с помощью элемента `<file>`.</span><span class="sxs-lookup"><span data-stu-id="efa10-341">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="efa10-342">Пример:</span><span class="sxs-lookup"><span data-stu-id="efa10-342">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="efa10-343">В NuGet версии 2.x и более ранних в проектах, использующих `packages.config`, элемент `<files>` также используется для включения неизменяемых файлов содержимого при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="efa10-343">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="efa10-344">В NuGet версии 3.3 и более поздних и проектах PackageReference используется элемент `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="efa10-344">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="efa10-345">Дополнительные сведения см. в разделе [Включение файлов содержимого](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="efa10-345">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="efa10-346">Атрибуты элементов файла</span><span class="sxs-lookup"><span data-stu-id="efa10-346">File element attributes</span></span>

<span data-ttu-id="efa10-347">Каждый элемент `<file>` задает указанные ниже атрибуты:</span><span class="sxs-lookup"><span data-stu-id="efa10-347">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="efa10-348">Атрибут</span><span class="sxs-lookup"><span data-stu-id="efa10-348">Attribute</span></span> | <span data-ttu-id="efa10-349">Описание</span><span class="sxs-lookup"><span data-stu-id="efa10-349">Description</span></span> |
| --- | --- |
| <span data-ttu-id="efa10-350">**src**</span><span class="sxs-lookup"><span data-stu-id="efa10-350">**src**</span></span> | <span data-ttu-id="efa10-351">Расположение файла или файлов, которые требуется включить, с учетом исключений, задаваемых атрибутом `exclude`.</span><span class="sxs-lookup"><span data-stu-id="efa10-351">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="efa10-352">Если не указан абсолютный путь, этот путь задается относительно файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="efa10-352">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="efa10-353">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="efa10-353">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="efa10-354">**target**</span><span class="sxs-lookup"><span data-stu-id="efa10-354">**target**</span></span> | <span data-ttu-id="efa10-355">Относительный путь к папке в пакете, куда помещаются файлы исходного кода. Должен начинаться с `lib`, `content`, `build` или `tools`.</span><span class="sxs-lookup"><span data-stu-id="efa10-355">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="efa10-356">См. раздел [Создание файла NUSPEC на основе рабочего каталога, соответствующего соглашениям](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="efa10-356">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="efa10-357">**exclude**</span><span class="sxs-lookup"><span data-stu-id="efa10-357">**exclude**</span></span> | <span data-ttu-id="efa10-358">Разделенный точками с запятой список файлов или шаблонов файлов, которые исключаются из расположения `src`.</span><span class="sxs-lookup"><span data-stu-id="efa10-358">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="efa10-359">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="efa10-359">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="efa10-360">Примеры</span><span class="sxs-lookup"><span data-stu-id="efa10-360">Examples</span></span>

<span data-ttu-id="efa10-361">**Одна сборка**</span><span class="sxs-lookup"><span data-stu-id="efa10-361">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="efa10-362">**Одна сборка, относящаяся к целевой платформе**</span><span class="sxs-lookup"><span data-stu-id="efa10-362">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="efa10-363">**Набор DLL-файлов с использованием подстановочного знака**</span><span class="sxs-lookup"><span data-stu-id="efa10-363">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="efa10-364">**DLL-файлы для разных платформ**</span><span class="sxs-lookup"><span data-stu-id="efa10-364">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="efa10-365">**Исключение файлов**</span><span class="sxs-lookup"><span data-stu-id="efa10-365">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="efa10-366">Включение файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="efa10-366">Including content files</span></span>

<span data-ttu-id="efa10-367">Файлы содержимого — это неизменяемые файлы, которые пакету необходимо включить в проект.</span><span class="sxs-lookup"><span data-stu-id="efa10-367">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="efa10-368">Такие файлы не подлежат изменению проектом, который потребляет их.</span><span class="sxs-lookup"><span data-stu-id="efa10-368">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="efa10-369">Примеры файлов содержимого:</span><span class="sxs-lookup"><span data-stu-id="efa10-369">Example content files include:</span></span>

- <span data-ttu-id="efa10-370">Изображения, внедряемые в качестве ресурсов</span><span class="sxs-lookup"><span data-stu-id="efa10-370">Images that are embedded as resources</span></span>
- <span data-ttu-id="efa10-371">Файлы исходного кода, которые уже были скомпилированы</span><span class="sxs-lookup"><span data-stu-id="efa10-371">Source files that are already compiled</span></span>
- <span data-ttu-id="efa10-372">Скрипты, которые необходимо включить в выходные данные построения проекта</span><span class="sxs-lookup"><span data-stu-id="efa10-372">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="efa10-373">Файлы конфигурации для пакета, которые необходимо включить в проект, но не требуется изменять в рамках отдельного проекта</span><span class="sxs-lookup"><span data-stu-id="efa10-373">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="efa10-374">Файлы содержимого включаются в проект с помощью элемента `<files>`, задающего папку `content` в атрибуте `target`.</span><span class="sxs-lookup"><span data-stu-id="efa10-374">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="efa10-375">Тем не менее такие файлы игнорируются при установке пакета в проект с использованием PackageReference, в которых вместо этого используется элемент `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="efa10-375">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="efa10-376">Чтобы обеспечить максимальную совместимость с потребляющими проектами, в идеальном случае файлы содержимого следует задавать в проекте с использованием обоих элементов.</span><span class="sxs-lookup"><span data-stu-id="efa10-376">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="efa10-377">Использование элемента files для файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="efa10-377">Using the files element for content files</span></span>

<span data-ttu-id="efa10-378">Для файлов содержимого следует использовать тот же формат, что и для файлов сборки, однако необходимо указать в качестве базовой сборки `content` в атрибуте `target`, как показано в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="efa10-378">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="efa10-379">**Базовые файлы содержимого**</span><span class="sxs-lookup"><span data-stu-id="efa10-379">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="efa10-380">**Файлы содержимого со структурой каталогов**</span><span class="sxs-lookup"><span data-stu-id="efa10-380">**Content files with directory structure**</span></span>

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

<span data-ttu-id="efa10-381">**Файлы содержимого, относящиеся к целевой платформе**</span><span class="sxs-lookup"><span data-stu-id="efa10-381">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="efa10-382">**Файлы содержимого, копируемые в папку с точкой в имени**</span><span class="sxs-lookup"><span data-stu-id="efa10-382">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="efa10-383">В этом случае NuGet определяет, что расширение в атрибуте `target` не соответствует расширению в `src` и обрабатывает такую часть имени в атрибуте `target` как папку:</span><span class="sxs-lookup"><span data-stu-id="efa10-383">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="efa10-384">**Файлы содержимого без расширений**</span><span class="sxs-lookup"><span data-stu-id="efa10-384">**Content files without extensions**</span></span>

<span data-ttu-id="efa10-385">Чтобы включить файлы без расширения, используйте подстановочные знаки `*` или `**`:</span><span class="sxs-lookup"><span data-stu-id="efa10-385">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="efa10-386">**Файлы содержимого с глубоким путем и глубоким целевым объектом**</span><span class="sxs-lookup"><span data-stu-id="efa10-386">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="efa10-387">В этом случае из-за совпадения расширений файлов для исходного и целевого объектов NuGet предполагает, что целевой объект задает имя файла, а не папки:</span><span class="sxs-lookup"><span data-stu-id="efa10-387">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="efa10-388">**Переименование файла содержимого в пакете**</span><span class="sxs-lookup"><span data-stu-id="efa10-388">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="efa10-389">**Исключение файлов**</span><span class="sxs-lookup"><span data-stu-id="efa10-389">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="efa10-390">Использование элемента contentFiles для файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="efa10-390">Using the contentFiles element for content files</span></span>

<span data-ttu-id="efa10-391">*NuGet 4.0 и более поздней версии с PackageReference*</span><span class="sxs-lookup"><span data-stu-id="efa10-391">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="efa10-392">По умолчанию пакет помещает содержимое в папку `contentFiles` (см. ниже), а команда `nuget pack` включает все файлы в этой папке с использованием установленных по умолчанию атрибутов.</span><span class="sxs-lookup"><span data-stu-id="efa10-392">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="efa10-393">В этом случае включать узел `contentFiles` в файл `.nuspec` не требуется.</span><span class="sxs-lookup"><span data-stu-id="efa10-393">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="efa10-394">Чтобы управлять включаемыми файлами, элемент `<contentFiles>` задает коллекцию элементов `<files>`, которая точно определяет включаемые файлы.</span><span class="sxs-lookup"><span data-stu-id="efa10-394">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="efa10-395">Эти файлы задаются с набором атрибутов, который описывает их использование в системе проекта:</span><span class="sxs-lookup"><span data-stu-id="efa10-395">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="efa10-396">Атрибут</span><span class="sxs-lookup"><span data-stu-id="efa10-396">Attribute</span></span> | <span data-ttu-id="efa10-397">Описание:</span><span class="sxs-lookup"><span data-stu-id="efa10-397">Description</span></span> |
| --- | --- |
| <span data-ttu-id="efa10-398">**include**</span><span class="sxs-lookup"><span data-stu-id="efa10-398">**include**</span></span> | <span data-ttu-id="efa10-399">Расположение файла или файлов, которые требуется включить, с учетом исключений, задаваемых атрибутом `exclude` (обязательно).</span><span class="sxs-lookup"><span data-stu-id="efa10-399">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="efa10-400">Если не указан абсолютный путь, этот путь задается относительно файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="efa10-400">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="efa10-401">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="efa10-401">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="efa10-402">**exclude**</span><span class="sxs-lookup"><span data-stu-id="efa10-402">**exclude**</span></span> | <span data-ttu-id="efa10-403">Разделенный точками с запятой список файлов или шаблонов файлов, которые исключаются из расположения `src`.</span><span class="sxs-lookup"><span data-stu-id="efa10-403">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="efa10-404">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="efa10-404">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="efa10-405">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="efa10-405">**buildAction**</span></span> | <span data-ttu-id="efa10-406">Действие построения, назначаемое элементу содержимого для MSBuild, например `Content`, `None`, `Embedded Resource`, `Compile` и т. д. Значение по умолчанию — `Compile`.</span><span class="sxs-lookup"><span data-stu-id="efa10-406">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="efa10-407">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="efa10-407">**copyToOutput**</span></span> | <span data-ttu-id="efa10-408">Логическое значение, указывающее, следует ли копировать элементы содержимого сборки (или публикация) выходную папку.</span><span class="sxs-lookup"><span data-stu-id="efa10-408">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="efa10-409">Значение по умолчанию – false.</span><span class="sxs-lookup"><span data-stu-id="efa10-409">The default is false.</span></span> |
| <span data-ttu-id="efa10-410">**flatten**</span><span class="sxs-lookup"><span data-stu-id="efa10-410">**flatten**</span></span> | <span data-ttu-id="efa10-411">Логическое значение, указывающее на необходимость копировать элементы содержимого в одну папку в выходных данных построения (true) или сохранить структуру папок пакета (false).</span><span class="sxs-lookup"><span data-stu-id="efa10-411">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="efa10-412">Этот параметр применяется, только если для параметра copyToOutput установлено значение true.</span><span class="sxs-lookup"><span data-stu-id="efa10-412">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="efa10-413">Значение по умолчанию – false.</span><span class="sxs-lookup"><span data-stu-id="efa10-413">The default is false.</span></span> |

<span data-ttu-id="efa10-414">При установке пакета NuGet применяет дочерние элементы `<contentFiles>` в порядке сверху вниз.</span><span class="sxs-lookup"><span data-stu-id="efa10-414">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="efa10-415">Если одному файлу соответствует несколько записей, применяются все записи.</span><span class="sxs-lookup"><span data-stu-id="efa10-415">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="efa10-416">При обнаружении конфликтов для одного атрибута запись верхнего уровня переопределяет записи на нижних уровнях.</span><span class="sxs-lookup"><span data-stu-id="efa10-416">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="efa10-417">Структура папки пакета</span><span class="sxs-lookup"><span data-stu-id="efa10-417">Package folder structure</span></span>

<span data-ttu-id="efa10-418">Структурирование содержимого в проекте пакета осуществляется по следующему шаблону:</span><span class="sxs-lookup"><span data-stu-id="efa10-418">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="efa10-419">Элемент `codeLanguages` может иметь значение `cs`, `vb`, `fs`, `any` или любой другой эквивалент заданного `$(ProjectLanguage)` в нижнем регистре</span><span class="sxs-lookup"><span data-stu-id="efa10-419">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="efa10-420">Элемент `TxM` представляет любой допустимый моникер целевой платформы, поддерживаемой NuGet (см. раздел [Целевые платформы](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="efa10-420">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="efa10-421">В конце этого синтаксиса может добавляться любая структура папок.</span><span class="sxs-lookup"><span data-stu-id="efa10-421">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="efa10-422">Пример:</span><span class="sxs-lookup"><span data-stu-id="efa10-422">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="efa10-423">Для пустых папок можно использовать `.`, чтобы отказаться от предоставления содержимого для определенных комбинаций языка и моникера целевой платформы, например:</span><span class="sxs-lookup"><span data-stu-id="efa10-423">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="efa10-424">Пример раздела contentFiles</span><span class="sxs-lookup"><span data-stu-id="efa10-424">Example contentFiles section</span></span>

```xml
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
```

## <a name="example-nuspec-files"></a><span data-ttu-id="efa10-425">Примеры файлов nuspec</span><span class="sxs-lookup"><span data-stu-id="efa10-425">Example nuspec files</span></span>

<span data-ttu-id="efa10-426">**Простой файл `.nuspec`, в котором не задаются зависимости или файлы**</span><span class="sxs-lookup"><span data-stu-id="efa10-426">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="efa10-427">**Файл `.nuspec` с зависимостями**</span><span class="sxs-lookup"><span data-stu-id="efa10-427">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="efa10-428">**Файл `.nuspec` с файлами**</span><span class="sxs-lookup"><span data-stu-id="efa10-428">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="efa10-429">**Файл `.nuspec` со сборками платформы**</span><span class="sxs-lookup"><span data-stu-id="efa10-429">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="efa10-430">В этом примере для целевых объектов проекта устанавливаются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="efa10-430">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="efa10-431">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="efa10-431">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="efa10-432">Клиентский профиль .NET4 -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="efa10-432">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="efa10-433">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="efa10-433">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="efa10-434">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="efa10-434">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="efa10-435">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="efa10-435">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
