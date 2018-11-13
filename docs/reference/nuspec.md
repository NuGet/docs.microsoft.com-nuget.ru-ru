---
title: Справочник по файлу nuspec для NuGet
description: Файл с расширением .nuspec содержит метаданные пакета, которые используются при построении пакета и предоставляют дополнительную информацию для его потребителей.
author: karann-msft
ms.author: karann
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 48f56ec5f042f6e78e38a202f0879c6949e7ee11
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580402"
---
# <a name="nuspec-reference"></a><span data-ttu-id="cc7f1-103">Справочник по файлу NUSPEC</span><span class="sxs-lookup"><span data-stu-id="cc7f1-103">.nuspec reference</span></span>

<span data-ttu-id="cc7f1-104">Файл `.nuspec` представляет собой манифест в формате XML и содержит метаданные пакета.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="cc7f1-105">Этот манифест используется при построении пакета и содержит дополнительные сведения для его потребителей.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="cc7f1-106">Манифест всегда включается в пакет.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="cc7f1-107">В этом разделе.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-107">In this topic:</span></span>

- [<span data-ttu-id="cc7f1-108">Общая форма и схема</span><span class="sxs-lookup"><span data-stu-id="cc7f1-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="cc7f1-109">[Замена маркеров](#replacement-tokens) (при использовании с проектом Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="cc7f1-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="cc7f1-110">Зависимости</span><span class="sxs-lookup"><span data-stu-id="cc7f1-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="cc7f1-111">Явные ссылки на сборку</span><span class="sxs-lookup"><span data-stu-id="cc7f1-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="cc7f1-112">Ссылки на сборку платформы</span><span class="sxs-lookup"><span data-stu-id="cc7f1-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="cc7f1-113">Включение файлов сборки</span><span class="sxs-lookup"><span data-stu-id="cc7f1-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="cc7f1-114">Включение файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="cc7f1-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="cc7f1-115">Примеры файлов nuspec</span><span class="sxs-lookup"><span data-stu-id="cc7f1-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="general-form-and-schema"></a><span data-ttu-id="cc7f1-116">Общая форма и схема</span><span class="sxs-lookup"><span data-stu-id="cc7f1-116">General form and schema</span></span>

<span data-ttu-id="cc7f1-117">Текущий файл схемы `nuspec.xsd` представлен в [репозитории GitHub для NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-117">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="cc7f1-118">В рамках этой схемы файл `.nuspec` имеет следующую общую форму:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-118">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="cc7f1-119">Чтобы получить наглядное представление схемы, откройте файл в режиме конструктора Visual Studio и щелкните ссылку **Обозреватель схемы XML**.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-119">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="cc7f1-120">Также можно открыть этот файл в виде кода. Для этого щелкните правой кнопкой мыши в редакторе и выберите команду **Показать в обозревателе схемы XML**.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-120">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="cc7f1-121">В любом случае при развертывании большинства узлов схема будет иметь примерно следующий вид:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-121">Either way you get a view like the one below (when mostly expanded):</span></span>

![Обозреватель схемы Visual Studio с открытым файлом nuspec.xsd](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="cc7f1-123">Обязательные элементы метаданных</span><span class="sxs-lookup"><span data-stu-id="cc7f1-123">Required metadata elements</span></span>

<span data-ttu-id="cc7f1-124">Следующие элементы являются минимальным требованием для пакета, однако, несмотря на это, рекомендуется добавить [дополнительные элементы метаданных](#optional-metadata-elements), чтобы оптимизировать работу с вашим пакетом для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-124">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="cc7f1-125">Эти элементы должны использоваться внутри элемента `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-125">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="cc7f1-126">id</span><span class="sxs-lookup"><span data-stu-id="cc7f1-126">id</span></span> 
<span data-ttu-id="cc7f1-127">Идентификатор пакета без учета регистра, который должен быть уникальным в пределах сайта nuget.org или иной коллекции, в которой находится пакет.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-127">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="cc7f1-128">Идентификаторы не должны содержать пробелов или символов, которые недопустимы в URL-адресах, и в них должны соблюдаться общие правила касательно пространств имен .NET.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-128">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="cc7f1-129">Инструкции см. в разделе [Выбор уникального идентификатора пакета](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-129">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="cc7f1-130">version</span><span class="sxs-lookup"><span data-stu-id="cc7f1-130">version</span></span>
<span data-ttu-id="cc7f1-131">Версия пакета, указываемая согласно шаблону *основной_номер.дополнительный_номер.исправление*.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-131">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="cc7f1-132">Номер версии может включать в себя суффикс предварительной версии, как описано в разделе [Управление версиями пакета](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-132">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="cc7f1-133">Описание</span><span class="sxs-lookup"><span data-stu-id="cc7f1-133">description</span></span>
<span data-ttu-id="cc7f1-134">Подробное описание пакета для отображения пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-134">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="cc7f1-135">authors</span><span class="sxs-lookup"><span data-stu-id="cc7f1-135">authors</span></span>
<span data-ttu-id="cc7f1-136">Разделенный запятыми список авторов пакетов, совпадающих с именами профилей на сайте nuget.org. Они отображаются в коллекции NuGet на сайте nuget.org и используются для перекрестных ссылок на пакеты тех же авторов.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-136">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="cc7f1-137">Необязательные элементы метаданных</span><span class="sxs-lookup"><span data-stu-id="cc7f1-137">Optional metadata elements</span></span>

#### <a name="title"></a><span data-ttu-id="cc7f1-138">заголовок</span><span class="sxs-lookup"><span data-stu-id="cc7f1-138">title</span></span>
<span data-ttu-id="cc7f1-139">Понятный заголовок пакета, обычно используемый при отображении пользовательского интерфейса, как на сайте nuget.org и в диспетчере пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="cc7f1-140">Если значение не указано, используется идентификатор пакета.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-140">If not specified, the package ID is used.</span></span> 
#### <a name="owners"></a><span data-ttu-id="cc7f1-141">owners</span><span class="sxs-lookup"><span data-stu-id="cc7f1-141">owners</span></span>
<span data-ttu-id="cc7f1-142">Разделенный запятыми список создателей пакета, совпадающих с именами профилей на сайте nuget.org. Часто совпадает со списком в элементе `authors` и игнорируется при загрузке пакета на веб-сайт nuget.org. См. раздел [Управление владельцами пакетов на веб-сайте nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-142">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 
#### <a name="projecturl"></a><span data-ttu-id="cc7f1-143">projectUrl</span><span class="sxs-lookup"><span data-stu-id="cc7f1-143">projectUrl</span></span>
<span data-ttu-id="cc7f1-144">URL-адрес для домашней страницы пакета, часто указываемый при отображении пользовательского интерфейса, также как и nuget.org.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-144">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 
#### <a name="licenseurl"></a><span data-ttu-id="cc7f1-145">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="cc7f1-145">licenseUrl</span></span>
<span data-ttu-id="cc7f1-146">URL-адрес для лицензии пакета, часто указываемый при отображении пользовательского интерфейса, так же как и nuget.org.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-146">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span>
#### <a name="iconurl"></a><span data-ttu-id="cc7f1-147">iconUrl</span><span class="sxs-lookup"><span data-stu-id="cc7f1-147">iconUrl</span></span>
<span data-ttu-id="cc7f1-148">URL-адрес для изображения размером 64x64 с прозрачным фоном, используемого в качестве значка для пакета при отображении пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-148">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="cc7f1-149">Убедитесь, что этот элемент содержит *прямой URL-адрес изображения*, а не URL-адрес веб-страницы, на которой содержится изображение.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-149">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="cc7f1-150">Например, чтобы использовать изображение из GitHub, используйте необработанного файла, URL-адрес, например <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-150">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="cc7f1-151">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="cc7f1-151">requireLicenseAcceptance</span></span>
<span data-ttu-id="cc7f1-152">Логическое значение, указывающее, должен ли клиент просить потребителя принять условия лицензии перед установкой пакета.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-152">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>
#### <a name="developmentdependency"></a><span data-ttu-id="cc7f1-153">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="cc7f1-153">developmentDependency</span></span>
<span data-ttu-id="cc7f1-154">*(Версия 2.8 и более поздние)* Логическое значение, указывающее, помечен ли пакет как зависимость только для разработки, что позволяет запретить его включение в качестве зависимости в другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-154">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="cc7f1-155">С помощью PackageReference (NuGet 4.8 +) этот флаг также означает, что исключает средств компиляции от компиляции.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-155">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="cc7f1-156">См. в разделе [DevelopmentDependency поддержка формата PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="cc7f1-156">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>
#### <a name="summary"></a><span data-ttu-id="cc7f1-157">сводка</span><span class="sxs-lookup"><span data-stu-id="cc7f1-157">summary</span></span>
<span data-ttu-id="cc7f1-158">Краткое описание пакета для отображения пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-158">A short description of the package for UI display.</span></span> <span data-ttu-id="cc7f1-159">Если этот элемент опущен, используется сокращенная версия элемента `description`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-159">If omitted, a truncated version of `description` is used.</span></span>
#### <a name="releasenotes"></a><span data-ttu-id="cc7f1-160">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="cc7f1-160">releaseNotes</span></span>
<span data-ttu-id="cc7f1-161">*(Версия 1.5 и более поздние)* Описание изменений, внесенных в этом выпуске пакета NuGet; часто используется в пользовательском интерфейсе как вкладка **Обновления** диспетчера пакетов Visual Studio вместо описания пакета.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-161">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>
#### <a name="copyright"></a><span data-ttu-id="cc7f1-162">авторские права</span><span class="sxs-lookup"><span data-stu-id="cc7f1-162">copyright</span></span>
<span data-ttu-id="cc7f1-163">*(Версия 1.5 и более поздние)* Сведения об авторских правах для пакета.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-163">*(1.5+)* Copyright details for the package.</span></span>
#### <a name="language"></a><span data-ttu-id="cc7f1-164">язык</span><span class="sxs-lookup"><span data-stu-id="cc7f1-164">language</span></span>
<span data-ttu-id="cc7f1-165">Идентификатор языкового стандарта для пакета.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-165">The locale ID for the package.</span></span> <span data-ttu-id="cc7f1-166">См. раздел [Создание локализованных пакетов](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-166">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>
#### <a name="tags"></a><span data-ttu-id="cc7f1-167">теги</span><span class="sxs-lookup"><span data-stu-id="cc7f1-167">tags</span></span>
<span data-ttu-id="cc7f1-168">Список разделенных пробелами тегов и ключевых слов, описывающих пакет NuGet и помогающих находить пакеты NuGet с помощью функций поиска и фильтрации.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-168">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 
#### <a name="serviceable"></a><span data-ttu-id="cc7f1-169">обслуживанию</span><span class="sxs-lookup"><span data-stu-id="cc7f1-169">serviceable</span></span> 
<span data-ttu-id="cc7f1-170">*(Версия 3.3 и более поздние)* Только для внутреннего использования в NuGet.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-170">*(3.3+)* For internal NuGet use only.</span></span>
#### <a name="repository"></a><span data-ttu-id="cc7f1-171">репозиторий</span><span class="sxs-lookup"><span data-stu-id="cc7f1-171">repository</span></span>
<span data-ttu-id="cc7f1-172">Репозиторий метаданных, состоящий из четыре необязательных атрибута: *тип* и *URL-адрес* *(4.0 или более поздней)*, и *ветви* и  *фиксации* *(4.6 или более поздней)*.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-172">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="cc7f1-173">Эти атрибуты позволяют сопоставлять файла nupkg в репозиторий, построении, с потенциально могут стать как описано, как отдельные ветви или фиксации, который создан пакет.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-173">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="cc7f1-174">Это должен быть общедоступным URL-адрес, который может вызываться напрямую по для управления версиями.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-174">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="cc7f1-175">Он не должно быть HTML-страницы, как это предназначено для компьютера.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-175">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="cc7f1-176">Для связывания страницу проекта, используйте `projectUrl` , вместо этого поле.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-176">For linking to project page, use the `projectUrl` field, instead.</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="cc7f1-177">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="cc7f1-177">minClientVersion</span></span>
<span data-ttu-id="cc7f1-178">Указывает минимальную версию клиента NuGet, который может установить этот пакет с использованием nuget.exe и диспетчера пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-178">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="cc7f1-179">Используется во всех случаях, когда пакет зависит от конкретных функций в файле `.nuspec`, которые были добавлены в определенной версии клиента NuGet.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-179">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="cc7f1-180">Например, для пакета, использующего атрибут `developmentDependency`, атрибуту `minClientVersion` необходимо присвоить значение "2.8".</span><span class="sxs-lookup"><span data-stu-id="cc7f1-180">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="cc7f1-181">Аналогичным образом, для пакета, использующего элемент `contentFiles` (см. следующий раздел), атрибуту `minClientVersion` необходимо присвоить значение "3.3".</span><span class="sxs-lookup"><span data-stu-id="cc7f1-181">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="cc7f1-182">Также обратите внимание, что клиенты NuGet версий, предшествующих 2.5, не распознают этот флаг и поэтому *всегда* отклоняют установку пакета независимо от значения атрибута `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-182">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="cc7f1-183">Элементы коллекции</span><span class="sxs-lookup"><span data-stu-id="cc7f1-183">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="cc7f1-184">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="cc7f1-184">packageTypes</span></span>
<span data-ttu-id="cc7f1-185">*(Версия 3.5 и более поздние)* Пустая коллекция или без нескольких элементов `<packageType>`, определяющих тип пакета, если он отличается от обычного пакета зависимостей.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-185">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="cc7f1-186">Каждый элемент packageType имеет атрибуты *name* и *version*.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-186">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="cc7f1-187">См. раздел [Указание типа пакета](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-187">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="cc7f1-188">зависимости</span><span class="sxs-lookup"><span data-stu-id="cc7f1-188">dependencies</span></span>
<span data-ttu-id="cc7f1-189">Коллекция из нуля или более элементов `<dependency>`, задающих зависимости для пакета.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-189">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="cc7f1-190">Каждый элемент dependency имеет атрибуты *id*, *version*, *include* (версия 3.x и более поздние) и *exclude* (версия 3.x и более поздние).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-190">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="cc7f1-191">См. раздел [Зависимости](#dependencies-element) далее.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-191">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="cc7f1-192">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="cc7f1-192">frameworkAssemblies</span></span>
<span data-ttu-id="cc7f1-193">*(Версия 1.2 и более поздние)* Коллекция из одного или более элементов `<frameworkAssembly>`, идентифицирующих ссылки на сборки .NET Framework, необходимые для этого пакета, что гарантирует добавление ссылок в проекты, использующие пакет.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-193">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="cc7f1-194">Каждый элемент frameworkAssembly имеет атрибуты *assemblyName* и *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-194">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="cc7f1-195">См. раздел [Указание ссылок на сборки платформы в глобальном кэше сборок ](#specifying-framework-assembly-references-gac) ниже.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-195">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="cc7f1-196">ссылки</span><span class="sxs-lookup"><span data-stu-id="cc7f1-196">references</span></span>
<span data-ttu-id="cc7f1-197">*(Версия 1.5 и более поздние)* Коллекция из нуля или более элементов `<reference>`, задающие имена сборок в папке `lib` пакета, которые добавляются в качестве ссылок проекта.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-197">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="cc7f1-198">Каждый элемент reference имеет атрибут *file*.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-198">Each reference has a *file* attribute.</span></span> <span data-ttu-id="cc7f1-199">Коллекция `<references>` также может содержать элемент `<group>` с атрибутом *targetFramework*, который, в свою очередь, содержит элементы `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-199">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="cc7f1-200">Если этот элемент опущен, включаются все ссылки в папке `lib`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-200">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="cc7f1-201">См. раздел [Указание явных ссылок на сборки](#specifying-explicit-assembly-references) ниже.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-201">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="cc7f1-202">contentFiles</span><span class="sxs-lookup"><span data-stu-id="cc7f1-202">contentFiles</span></span>
<span data-ttu-id="cc7f1-203">*(Версия 3.3 и более поздние)* Коллекция элементов `<files>`, которые идентифицируют файлы содержимого, включаемые в потребляющий проект.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-203">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="cc7f1-204">Эти файлы задаются с набором атрибутов, который описывает их использование в системе проекта.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-204">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="cc7f1-205">См. раздел [Указание включаемых в пакет файлов](#specifying-files-to-include-in-the-package) ниже.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-205">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="cc7f1-206">файлы</span><span class="sxs-lookup"><span data-stu-id="cc7f1-206">files</span></span> 
<span data-ttu-id="cc7f1-207">`<package>` Узел может содержать `<files>` узел как одноуровневый элемент `<metadata>`и `<contentFiles>` дочерний элемент в `<metadata>`, чтобы указать, какие файлы сборки и содержимого, следует включить в пакет.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-207">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="cc7f1-208">Дополнительные сведения см. далее в разделах [Включение файлов сборки](#including-assembly-files) и [Включение файлов содержимого](#including-content-files) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-208">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="cc7f1-209">Замена маркеров</span><span class="sxs-lookup"><span data-stu-id="cc7f1-209">Replacement tokens</span></span>

<span data-ttu-id="cc7f1-210">При создании пакета [команда `nuget pack`](../tools/cli-ref-pack.md) заменяет маркеры с разделителями $ в узле `<metadata>` файла `.nuspec` значениями из файла проекта или параметра `-properties` команды `pack`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-210">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="cc7f1-211">Маркеры задаются в командной строке следующим образом: `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-211">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="cc7f1-212">Например, вы можете использовать маркер, такой как `$owners$` и `$desc$`, в файле `.nuspec` и предоставить значения во время упаковки следующим образом:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-212">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="cc7f1-213">Чтобы использовать значения из проекта, укажите маркеры, описываемые в следующей таблице (AssemblyInfo ссылается на файл в `Properties`, например `AssemblyInfo.cs` или `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-213">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="cc7f1-214">Чтобы использовать эти маркеры, выполните команду `nuget pack` с файлом проекта, а не просто с файлом `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-214">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="cc7f1-215">Например, при использовании следующей команды маркеры `$id$` и `$version$` в файле `.nuspec` заменяются значениями проекта `AssemblyName` и `AssemblyVersion`:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-215">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="cc7f1-216">Как правило, при наличии проекта вы изначально создаете файл `.nuspec` с использованием команды `nuget spec MyProject.csproj`, которая автоматически включает некоторые из этих стандартных маркеров.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-216">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="cc7f1-217">Тем не менее, если в проекте отсутствуют значения для обязательных элементов `.nuspec`, команда `nuget pack` завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-217">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="cc7f1-218">Кроме того, при изменении значений проекта необходимо выполнить перестроение до создания пакета. Это можно легко сделать с помощью параметра `build` команды pack.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-218">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="cc7f1-219">За исключением элемента `$configuration$`, значения в проекте используются в приоритетном порядке относительно любых значений, назначенных тому же маркеру в командной строке.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-219">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="cc7f1-220">Токен</span><span class="sxs-lookup"><span data-stu-id="cc7f1-220">Token</span></span> | <span data-ttu-id="cc7f1-221">Источник значения</span><span class="sxs-lookup"><span data-stu-id="cc7f1-221">Value source</span></span> | <span data-ttu-id="cc7f1-222">Значение</span><span class="sxs-lookup"><span data-stu-id="cc7f1-222">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="cc7f1-223">**$id$**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-223">**$id$**</span></span> | <span data-ttu-id="cc7f1-224">Файл проекта</span><span class="sxs-lookup"><span data-stu-id="cc7f1-224">Project file</span></span> | <span data-ttu-id="cc7f1-225">AssemblyName (заголовок) из файла проекта</span><span class="sxs-lookup"><span data-stu-id="cc7f1-225">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="cc7f1-226">**$version$**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-226">**$version$**</span></span> | <span data-ttu-id="cc7f1-227">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="cc7f1-227">AssemblyInfo</span></span> | <span data-ttu-id="cc7f1-228">AssemblyInformationalVersion, если присутствует, в противном случае AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="cc7f1-228">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="cc7f1-229">**$authors$**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-229">**$authors$**</span></span> | <span data-ttu-id="cc7f1-230">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="cc7f1-230">AssemblyInfo</span></span> | <span data-ttu-id="cc7f1-231">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="cc7f1-231">AssemblyCompany</span></span> |
| <span data-ttu-id="cc7f1-232">**$title$**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-232">**$title$**</span></span> | <span data-ttu-id="cc7f1-233">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="cc7f1-233">AssemblyInfo</span></span> | <span data-ttu-id="cc7f1-234">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="cc7f1-234">AssemblyTitle</span></span> |
| <span data-ttu-id="cc7f1-235">**$description$**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-235">**$description$**</span></span> | <span data-ttu-id="cc7f1-236">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="cc7f1-236">AssemblyInfo</span></span> | <span data-ttu-id="cc7f1-237">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="cc7f1-237">AssemblyDescription</span></span> |
| <span data-ttu-id="cc7f1-238">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-238">**$copyright$**</span></span> | <span data-ttu-id="cc7f1-239">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="cc7f1-239">AssemblyInfo</span></span> | <span data-ttu-id="cc7f1-240">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="cc7f1-240">AssemblyCopyright</span></span> |
| <span data-ttu-id="cc7f1-241">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-241">**$configuration$**</span></span> | <span data-ttu-id="cc7f1-242">DLL-файл сборки</span><span class="sxs-lookup"><span data-stu-id="cc7f1-242">Assembly DLL</span></span> | <span data-ttu-id="cc7f1-243">Конфигурация, используемая для построения сборки, по умолчанию используется тип отладки.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-243">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="cc7f1-244">Обратите внимание, что для создания пакета с помощью конфигурации выпуска в командной строке всегда используется параметр `-properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-244">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="cc7f1-245">Маркеры также можно использовать для разрешения путей при включении [файлов сборок](#including-assembly-files) и [файлов содержимого](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-245">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="cc7f1-246">Маркеры имеют те же имена, что и свойства MSBuild, что позволяет выбирать файлы для включения в зависимости в текущей конфигурации построения.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-246">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="cc7f1-247">Например, если вы используете следующие маркеры в файле `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-247">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="cc7f1-248">И выполняете построение сборки, для которой `AssemblyName` имеет значение `LoggingLibrary` с конфигурацией `Release` в MSBuild, в файле `.nuspec` в пакете будут присутствовать следующие строки:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-248">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="cc7f1-249">Dependencies-элемент</span><span class="sxs-lookup"><span data-stu-id="cc7f1-249">Dependencies element</span></span>

<span data-ttu-id="cc7f1-250">Элемент `<dependencies>` внутри элемента `<metadata>` содержит любое число элементов `<dependency>`, идентифицирующих другие пакеты, от которых зависит пакет верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-250">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="cc7f1-251">Ниже перечислены атрибуты каждого элемента `<dependency>`:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-251">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="cc7f1-252">Атрибут</span><span class="sxs-lookup"><span data-stu-id="cc7f1-252">Attribute</span></span> | <span data-ttu-id="cc7f1-253">Описание</span><span class="sxs-lookup"><span data-stu-id="cc7f1-253">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="cc7f1-254">Идентификатор пакета зависимости, например EntityFramework и NUnit, являющийся именем пакета nuget.org, показан на странице пакета (обязательно).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-254">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="cc7f1-255">Диапазон версий, которые допустимы в качестве зависимости (обязательно).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-255">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="cc7f1-256">Точный синтаксис см. в разделе [Управление версиями пакета](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-256">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="cc7f1-257">include</span><span class="sxs-lookup"><span data-stu-id="cc7f1-257">include</span></span> | <span data-ttu-id="cc7f1-258">Разделенный запятыми список тегов включения или исключения (см. ниже), определяющий зависимости, включаемые в конечный пакет.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-258">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="cc7f1-259">Значение по умолчанию — `all`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-259">The default value is `all`.</span></span> |
| <span data-ttu-id="cc7f1-260">exclude</span><span class="sxs-lookup"><span data-stu-id="cc7f1-260">exclude</span></span> | <span data-ttu-id="cc7f1-261">Разделенный запятыми список тегов включения или исключения (см. ниже), определяющий зависимости, исключаемые из конечного пакета.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-261">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="cc7f1-262">Значение по умолчанию — `build,analyzers` которого может быть возможна перезапись.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-262">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="cc7f1-263">Но `content/ ContentFiles` исключаются также неявно в окончательный пакет, который не может быть возможна перезапись.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-263">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="cc7f1-264">Теги в свойстве `exclude` имеют приоритет перед тегами в свойстве `include`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-264">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="cc7f1-265">Например, `include="runtime, compile" exclude="compile"` равносильно `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-265">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="cc7f1-266">Тег включения или исключения</span><span class="sxs-lookup"><span data-stu-id="cc7f1-266">Include/Exclude tag</span></span> | <span data-ttu-id="cc7f1-267">Затрагиваемые папки пакета</span><span class="sxs-lookup"><span data-stu-id="cc7f1-267">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="cc7f1-268">contentFiles</span><span class="sxs-lookup"><span data-stu-id="cc7f1-268">contentFiles</span></span> | <span data-ttu-id="cc7f1-269">Content</span><span class="sxs-lookup"><span data-stu-id="cc7f1-269">Content</span></span> |
| <span data-ttu-id="cc7f1-270">исполняющая среда</span><span class="sxs-lookup"><span data-stu-id="cc7f1-270">runtime</span></span> | <span data-ttu-id="cc7f1-271">Runtime, Resources и FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="cc7f1-271">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="cc7f1-272">compile</span><span class="sxs-lookup"><span data-stu-id="cc7f1-272">compile</span></span> | <span data-ttu-id="cc7f1-273">lib</span><span class="sxs-lookup"><span data-stu-id="cc7f1-273">lib</span></span> |
| <span data-ttu-id="cc7f1-274">выполнить сборку</span><span class="sxs-lookup"><span data-stu-id="cc7f1-274">build</span></span> | <span data-ttu-id="cc7f1-275">build (свойства и цели MSBuild)</span><span class="sxs-lookup"><span data-stu-id="cc7f1-275">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="cc7f1-276">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="cc7f1-276">native</span></span> | <span data-ttu-id="cc7f1-277">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="cc7f1-277">native</span></span> |
| <span data-ttu-id="cc7f1-278">Нет</span><span class="sxs-lookup"><span data-stu-id="cc7f1-278">none</span></span> | <span data-ttu-id="cc7f1-279">Нет</span><span class="sxs-lookup"><span data-stu-id="cc7f1-279">No folders</span></span> |
| <span data-ttu-id="cc7f1-280">все</span><span class="sxs-lookup"><span data-stu-id="cc7f1-280">all</span></span> | <span data-ttu-id="cc7f1-281">Все папки</span><span class="sxs-lookup"><span data-stu-id="cc7f1-281">All folders</span></span> |

<span data-ttu-id="cc7f1-282">Например, следующие строки указывают зависимости от `PackageA` версии 1.1.0 или более поздней и `PackageB` версии 1.x.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-282">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="cc7f1-283">Следующие строки указывают зависимости от тех же пакетов и включают папки `contentFiles` и `build` для `PackageA`, а также все папки, кроме `native` и `compile`, для `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="cc7f1-283">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="cc7f1-284">Примечание. При создании файла `.nuspec` для проекта с использованием команды `nuget spec` существующие в проекте зависимости автоматически включаются в полученный файл `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-284">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="cc7f1-285">Группы зависимостей</span><span class="sxs-lookup"><span data-stu-id="cc7f1-285">Dependency groups</span></span>

<span data-ttu-id="cc7f1-286">*Версия 2.0 и более поздние*</span><span class="sxs-lookup"><span data-stu-id="cc7f1-286">*Version 2.0+*</span></span>

<span data-ttu-id="cc7f1-287">В качестве альтернативы простому неструктурированному списку зависимости могут задаваться в соответствии с профилем платформы целевого проекта с использованием элементов `<group>` в элементе `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-287">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="cc7f1-288">Каждый элемент group имеет атрибут `targetFramework` и содержит ноль или более элементов `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-288">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="cc7f1-289">Эти зависимости устанавливаются вместе в том случае, если целевая платформа совместима с профилем платформы проекта.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-289">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="cc7f1-290">Элемент `<group>` без атрибута `targetFramework` используется в качестве установленного по умолчанию или резервного списка зависимостей.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-290">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="cc7f1-291">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-291">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="cc7f1-292">Формат группы не может смешиваться с неструктурированным списком.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-292">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="cc7f1-293">В следующем примере приводятся различные варианты элемента `<group>`:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-293">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="cc7f1-294">Явные ссылки на сборку</span><span class="sxs-lookup"><span data-stu-id="cc7f1-294">Explicit assembly references</span></span>

<span data-ttu-id="cc7f1-295">Элемент `<references>` явно задает сборки, на которые целевой проект должен ссылаться при использовании пакета.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-295">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="cc7f1-296">Если этот элемент присутствует, NuGet добавляет ссылки только на указанные в списке сборки, но не на какие-либо другие сборки в папке `lib` проекта.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-296">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="cc7f1-297">Например, следующий элемент `<references>` указывает NuGet на необходимость добавлять ссылки только на сборки `xunit.dll` и `xunit.extensions.dll`, даже если в пакете есть другие сборки:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-297">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="cc7f1-298">Явные ссылки обычно применяются для сборок, используемых только во время разработки.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-298">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="cc7f1-299">При использовании [контрактов для кода](/dotnet/framework/debug-trace-profile/code-contracts) сборки контракта должны располагаться рядом со сборками среды выполнения, которые они расширяют, чтобы среда Visual Studio могла находить их. При этом не требуются ссылки на сборки контракта из проекта и эти сборки не нужно копировать в папку `bin` проекта.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-299">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="cc7f1-300">Аналогичным образом, явные ссылки можно использовать для платформ модульного тестирования, таких как XUnit, сборки средств которых должны располагаться рядом со сборками среды выполнения, но не требуют включения в ссылки проекта.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-300">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="cc7f1-301">Группы ссылок</span><span class="sxs-lookup"><span data-stu-id="cc7f1-301">Reference groups</span></span>

<span data-ttu-id="cc7f1-302">В качестве альтернативы простому неструктурированному списку ссылки могут задаваться в соответствии с профилем платформы целевого проекта с использованием элементов `<group>` в элементе `<references>`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-302">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="cc7f1-303">Каждый элемент group имеет атрибут `targetFramework` и содержит ноль или более элементов `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-303">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="cc7f1-304">Эти ссылки добавляются в проект в том случае, если целевая платформа совместима с профилем платформы проекта.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-304">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="cc7f1-305">Элемент `<group>` без атрибута `targetFramework` используется в качестве установленного по умолчанию или резервного списка ссылок.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-305">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="cc7f1-306">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-306">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="cc7f1-307">Формат группы не может смешиваться с неструктурированным списком.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-307">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="cc7f1-308">В следующем примере приводятся различные варианты элемента `<group>`:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-308">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="cc7f1-309">Ссылки на сборку платформы</span><span class="sxs-lookup"><span data-stu-id="cc7f1-309">Framework assembly references</span></span>

<span data-ttu-id="cc7f1-310">Сборки платформы входят в состав .NET Framework и должны находиться в глобальном кэше сборок любого заданного компьютера.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-310">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="cc7f1-311">Идентифицируя такие сборки с помощью элемента `<frameworkAssemblies>`, пакет может гарантировать, что ссылки, отсутствующие в проекте, будут при необходимости добавлены в него.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-311">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="cc7f1-312">Естественно, напрямую в пакет такие сборки не включаются.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-312">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="cc7f1-313">Элемент `<frameworkAssemblies>` содержит ноль или более элементов `<frameworkAssembly>`, каждый из которых задает следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-313">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="cc7f1-314">Атрибут</span><span class="sxs-lookup"><span data-stu-id="cc7f1-314">Attribute</span></span> | <span data-ttu-id="cc7f1-315">Описание</span><span class="sxs-lookup"><span data-stu-id="cc7f1-315">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc7f1-316">**имя_сборки**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-316">**assemblyName**</span></span> | <span data-ttu-id="cc7f1-317">Полное имя сборки (обязательно).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-317">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="cc7f1-318">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-318">**targetFramework**</span></span> | <span data-ttu-id="cc7f1-319">Указывает целевую платформу, к которой применяется эта ссылка (необязательно).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-319">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="cc7f1-320">Если этот атрибут опущен, указывает, что ссылка применяется ко всем платформам.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-320">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="cc7f1-321">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-321">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="cc7f1-322">В следующем примере показаны ссылка на `System.Net` для всех целевых платформ и ссылка на `System.ServiceModel` только для платформы .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-322">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="cc7f1-323">Включение файлов сборки</span><span class="sxs-lookup"><span data-stu-id="cc7f1-323">Including assembly files</span></span>

<span data-ttu-id="cc7f1-324">Если вы придерживаетесь соглашений, описываемых в разделе [Создание пакета](../create-packages/creating-a-package.md), вам не нужно явно задавать список файлов в файле `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-324">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="cc7f1-325">Команда `nuget pack` автоматически выбирает необходимые файлы.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-325">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="cc7f1-326">Когда пакет устанавливается в проекте, NuGet автоматически добавляет ссылки на библиотеки DLL сборок в пакете, *кроме* тех из них, в именах которых есть `.resources.dll`, так как они считаются локализованными вспомогательными сборками.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-326">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="cc7f1-327">По этой причине следует избегать использования `.resources.dll` в именах файлов пакета, которые содержат важный код.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-327">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="cc7f1-328">Чтобы обойти такое автоматическое поведение и явно управлять включением сборок в пакет, поместите элемент `<files>` в качестве дочернего для `<package>` (на одном уровне с `<metadata>`), указывая каждый файл с помощью элемента `<file>`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-328">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="cc7f1-329">Пример:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-329">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="cc7f1-330">В NuGet версии 2.x и более ранних в проектах, использующих `packages.config`, элемент `<files>` также используется для включения неизменяемых файлов содержимого при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-330">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="cc7f1-331">В NuGet версии 3.3 и более поздних и проектах PackageReference используется элемент `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-331">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="cc7f1-332">Дополнительные сведения см. в разделе [Включение файлов содержимого](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-332">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="cc7f1-333">Атрибуты элементов файла</span><span class="sxs-lookup"><span data-stu-id="cc7f1-333">File element attributes</span></span>

<span data-ttu-id="cc7f1-334">Каждый элемент `<file>` задает указанные ниже атрибуты:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-334">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="cc7f1-335">Атрибут</span><span class="sxs-lookup"><span data-stu-id="cc7f1-335">Attribute</span></span> | <span data-ttu-id="cc7f1-336">Описание</span><span class="sxs-lookup"><span data-stu-id="cc7f1-336">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc7f1-337">**src**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-337">**src**</span></span> | <span data-ttu-id="cc7f1-338">Расположение файла или файлов, которые требуется включить, с учетом исключений, задаваемых атрибутом `exclude`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-338">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="cc7f1-339">Если не указан абсолютный путь, этот путь задается относительно файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-339">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="cc7f1-340">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-340">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="cc7f1-341">**target**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-341">**target**</span></span> | <span data-ttu-id="cc7f1-342">Относительный путь к папке в пакете, куда помещаются файлы исходного кода. Должен начинаться с `lib`, `content`, `build` или `tools`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-342">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="cc7f1-343">См. раздел [Создание файла NUSPEC на основе рабочего каталога, соответствующего соглашениям](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-343">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="cc7f1-344">**exclude**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-344">**exclude**</span></span> | <span data-ttu-id="cc7f1-345">Разделенный точками с запятой список файлов или шаблонов файлов, которые исключаются из расположения `src`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-345">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="cc7f1-346">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-346">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="cc7f1-347">Примеры</span><span class="sxs-lookup"><span data-stu-id="cc7f1-347">Examples</span></span>

<span data-ttu-id="cc7f1-348">**Одна сборка**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-348">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="cc7f1-349">**Одна сборка, относящаяся к целевой платформе**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-349">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="cc7f1-350">**Набор DLL-файлов с использованием подстановочного знака**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-350">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="cc7f1-351">**DLL-файлы для разных платформ**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-351">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="cc7f1-352">**Исключение файлов**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-352">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="cc7f1-353">Включение файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="cc7f1-353">Including content files</span></span>

<span data-ttu-id="cc7f1-354">Файлы содержимого — это неизменяемые файлы, которые пакету необходимо включить в проект.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-354">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="cc7f1-355">Такие файлы не подлежат изменению проектом, который потребляет их.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-355">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="cc7f1-356">Примеры файлов содержимого:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-356">Example content files include:</span></span>

- <span data-ttu-id="cc7f1-357">Изображения, внедряемые в качестве ресурсов</span><span class="sxs-lookup"><span data-stu-id="cc7f1-357">Images that are embedded as resources</span></span>
- <span data-ttu-id="cc7f1-358">Файлы исходного кода, которые уже были скомпилированы</span><span class="sxs-lookup"><span data-stu-id="cc7f1-358">Source files that are already compiled</span></span>
- <span data-ttu-id="cc7f1-359">Скрипты, которые необходимо включить в выходные данные построения проекта</span><span class="sxs-lookup"><span data-stu-id="cc7f1-359">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="cc7f1-360">Файлы конфигурации для пакета, которые необходимо включить в проект, но не требуется изменять в рамках отдельного проекта</span><span class="sxs-lookup"><span data-stu-id="cc7f1-360">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="cc7f1-361">Файлы содержимого включаются в проект с помощью элемента `<files>`, задающего папку `content` в атрибуте `target`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-361">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="cc7f1-362">Тем не менее такие файлы игнорируются при установке пакета в проект с использованием PackageReference, в которых вместо этого используется элемент `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-362">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="cc7f1-363">Чтобы обеспечить максимальную совместимость с потребляющими проектами, в идеальном случае файлы содержимого следует задавать в проекте с использованием обоих элементов.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-363">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="cc7f1-364">Использование элемента files для файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="cc7f1-364">Using the files element for content files</span></span>

<span data-ttu-id="cc7f1-365">Для файлов содержимого следует использовать тот же формат, что и для файлов сборки, однако необходимо указать в качестве базовой сборки `content` в атрибуте `target`, как показано в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-365">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="cc7f1-366">**Базовые файлы содержимого**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-366">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="cc7f1-367">**Файлы содержимого со структурой каталогов**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-367">**Content files with directory structure**</span></span>

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

<span data-ttu-id="cc7f1-368">**Файлы содержимого, относящиеся к целевой платформе**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-368">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="cc7f1-369">**Файлы содержимого, копируемые в папку с точкой в имени**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-369">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="cc7f1-370">В этом случае NuGet определяет, что расширение в атрибуте `target` не соответствует расширению в `src` и обрабатывает такую часть имени в атрибуте `target` как папку:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-370">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="cc7f1-371">**Файлы содержимого без расширений**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-371">**Content files without extensions**</span></span>

<span data-ttu-id="cc7f1-372">Чтобы включить файлы без расширения, используйте подстановочные знаки `*` или `**`:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-372">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="cc7f1-373">**Файлы содержимого с глубоким путем и глубоким целевым объектом**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-373">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="cc7f1-374">В этом случае из-за совпадения расширений файлов для исходного и целевого объектов NuGet предполагает, что целевой объект задает имя файла, а не папки:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-374">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="cc7f1-375">**Переименование файла содержимого в пакете**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-375">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="cc7f1-376">**Исключение файлов**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-376">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="cc7f1-377">Использование элемента contentFiles для файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="cc7f1-377">Using the contentFiles element for content files</span></span>

<span data-ttu-id="cc7f1-378">*NuGet 4.0 и более поздней версии с PackageReference*</span><span class="sxs-lookup"><span data-stu-id="cc7f1-378">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="cc7f1-379">По умолчанию пакет помещает содержимое в папку `contentFiles` (см. ниже), а команда `nuget pack` включает все файлы в этой папке с использованием установленных по умолчанию атрибутов.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-379">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="cc7f1-380">В этом случае включать узел `contentFiles` в файл `.nuspec` не требуется.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-380">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="cc7f1-381">Чтобы управлять включаемыми файлами, элемент `<contentFiles>` задает коллекцию элементов `<files>`, которая точно определяет включаемые файлы.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-381">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="cc7f1-382">Эти файлы задаются с набором атрибутов, который описывает их использование в системе проекта:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-382">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="cc7f1-383">Атрибут</span><span class="sxs-lookup"><span data-stu-id="cc7f1-383">Attribute</span></span> | <span data-ttu-id="cc7f1-384">Описание</span><span class="sxs-lookup"><span data-stu-id="cc7f1-384">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc7f1-385">**include**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-385">**include**</span></span> | <span data-ttu-id="cc7f1-386">Расположение файла или файлов, которые требуется включить, с учетом исключений, задаваемых атрибутом `exclude` (обязательно).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-386">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="cc7f1-387">Если не указан абсолютный путь, этот путь задается относительно файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-387">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="cc7f1-388">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-388">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="cc7f1-389">**exclude**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-389">**exclude**</span></span> | <span data-ttu-id="cc7f1-390">Разделенный точками с запятой список файлов или шаблонов файлов, которые исключаются из расположения `src`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-390">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="cc7f1-391">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-391">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="cc7f1-392">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-392">**buildAction**</span></span> | <span data-ttu-id="cc7f1-393">Действие построения, назначаемое элементу содержимого для MSBuild, например `Content`, `None`, `Embedded Resource`, `Compile` и т. д. Значение по умолчанию — `Compile`.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-393">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="cc7f1-394">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-394">**copyToOutput**</span></span> | <span data-ttu-id="cc7f1-395">Логическое значение, указывающее, следует ли копировать элементы содержимого сборки (или публикация) выходную папку.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-395">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="cc7f1-396">Значение по умолчанию – false.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-396">The default is false.</span></span> |
| <span data-ttu-id="cc7f1-397">**flatten**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-397">**flatten**</span></span> | <span data-ttu-id="cc7f1-398">Логическое значение, указывающее на необходимость копировать элементы содержимого в одну папку в выходных данных построения (true) или сохранить структуру папок пакета (false).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-398">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="cc7f1-399">Этот параметр применяется, только если для параметра copyToOutput установлено значение true.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-399">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="cc7f1-400">Значение по умолчанию – false.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-400">The default is false.</span></span> |

<span data-ttu-id="cc7f1-401">При установке пакета NuGet применяет дочерние элементы `<contentFiles>` в порядке сверху вниз.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-401">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="cc7f1-402">Если одному файлу соответствует несколько записей, применяются все записи.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-402">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="cc7f1-403">При обнаружении конфликтов для одного атрибута запись верхнего уровня переопределяет записи на нижних уровнях.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-403">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="cc7f1-404">Структура папки пакета</span><span class="sxs-lookup"><span data-stu-id="cc7f1-404">Package folder structure</span></span>

<span data-ttu-id="cc7f1-405">Структурирование содержимого в проекте пакета осуществляется по следующему шаблону:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-405">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="cc7f1-406">Элемент `codeLanguages` может иметь значение `cs`, `vb`, `fs`, `any` или любой другой эквивалент заданного `$(ProjectLanguage)` в нижнем регистре</span><span class="sxs-lookup"><span data-stu-id="cc7f1-406">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="cc7f1-407">Элемент `TxM` представляет любой допустимый моникер целевой платформы, поддерживаемой NuGet (см. раздел [Целевые платформы](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="cc7f1-407">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="cc7f1-408">В конце этого синтаксиса может добавляться любая структура папок.</span><span class="sxs-lookup"><span data-stu-id="cc7f1-408">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="cc7f1-409">Пример:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-409">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="cc7f1-410">Для пустых папок можно использовать `.`, чтобы отказаться от предоставления содержимого для определенных комбинаций языка и моникера целевой платформы, например:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-410">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="cc7f1-411">Пример раздела contentFiles</span><span class="sxs-lookup"><span data-stu-id="cc7f1-411">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="cc7f1-412">Примеры файлов nuspec</span><span class="sxs-lookup"><span data-stu-id="cc7f1-412">Example nuspec files</span></span>

<span data-ttu-id="cc7f1-413">**Простой файл `.nuspec`, в котором не задаются зависимости или файлы**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-413">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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
        <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
    </metadata>
</package>
```

<span data-ttu-id="cc7f1-414">**Файл `.nuspec` с зависимостями**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-414">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="cc7f1-415">**Файл `.nuspec` с файлами**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-415">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="cc7f1-416">**Файл `.nuspec` со сборками платформы**</span><span class="sxs-lookup"><span data-stu-id="cc7f1-416">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="cc7f1-417">В этом примере для целевых объектов проекта устанавливаются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="cc7f1-417">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="cc7f1-418">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="cc7f1-418">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="cc7f1-419">Клиентский профиль .NET4 -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="cc7f1-419">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="cc7f1-420">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="cc7f1-420">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="cc7f1-421">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="cc7f1-421">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="cc7f1-422">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="cc7f1-422">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
