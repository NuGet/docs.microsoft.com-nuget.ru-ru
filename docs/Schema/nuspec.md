---
title: "Справочник по файлу NUSPEC для NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/29/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d4a4db9b-5c2d-46aa-9107-d2b01733df7c
description: "Файл с расширением .nuspec содержит метаданные пакета, которые используются при построении пакета и предоставляют дополнительную информацию для его потребителей."
keywords: "справочник по nuspec, метаданные пакета NuGet, манифест пакета NuGet, схема файла nuspec"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 91efd4b4cd2ec0bee4425ab66e0152e580e7975c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="nuspec-reference"></a><span data-ttu-id="d263c-104">Справочник по файлу NUSPEC</span><span class="sxs-lookup"><span data-stu-id="d263c-104">.nuspec reference</span></span>

<span data-ttu-id="d263c-105">Файл `.nuspec` представляет собой манифест в формате XML и содержит метаданные пакета.</span><span class="sxs-lookup"><span data-stu-id="d263c-105">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="d263c-106">Этот манифест используется при построении пакета и содержит дополнительные сведения для его потребителей.</span><span class="sxs-lookup"><span data-stu-id="d263c-106">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="d263c-107">Манифест всегда включается в пакет.</span><span class="sxs-lookup"><span data-stu-id="d263c-107">The manifest is always included in a package.</span></span>

<span data-ttu-id="d263c-108">Содержание раздела</span><span class="sxs-lookup"><span data-stu-id="d263c-108">In this topic:</span></span>

- [<span data-ttu-id="d263c-109">Общая форма и схема</span><span class="sxs-lookup"><span data-stu-id="d263c-109">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="d263c-110">[Замена маркеров](#replacement-tokens) (при использовании с проектом Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d263c-110">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="d263c-111">Зависимости</span><span class="sxs-lookup"><span data-stu-id="d263c-111">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="d263c-112">Явные ссылки на сборку</span><span class="sxs-lookup"><span data-stu-id="d263c-112">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="d263c-113">Ссылки на сборку платформы</span><span class="sxs-lookup"><span data-stu-id="d263c-113">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="d263c-114">Включение файлов сборки</span><span class="sxs-lookup"><span data-stu-id="d263c-114">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="d263c-115">Включение файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="d263c-115">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="d263c-116">Примеры</span><span class="sxs-lookup"><span data-stu-id="d263c-116">Examples</span></span>](#examples)

## <a name="general-form-and-schema"></a><span data-ttu-id="d263c-117">Общая форма и схема</span><span class="sxs-lookup"><span data-stu-id="d263c-117">General form and schema</span></span>

<span data-ttu-id="d263c-118">Текущий файл схемы `nuspec.xsd` представлен в [репозитории GitHub для NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="d263c-118">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="d263c-119">В рамках этой схемы файл `.nuspec` имеет следующую общую форму:</span><span class="sxs-lookup"><span data-stu-id="d263c-119">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="d263c-120">Чтобы получить наглядное представление схемы, откройте файл в режиме конструктора Visual Studio и щелкните ссылку **Обозреватель схемы XML**.</span><span class="sxs-lookup"><span data-stu-id="d263c-120">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="d263c-121">Также можно открыть этот файл в виде кода. Для этого щелкните правой кнопкой мыши в редакторе и выберите команду **Показать в обозревателе схемы XML**.</span><span class="sxs-lookup"><span data-stu-id="d263c-121">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="d263c-122">В любом случае при развертывании большинства узлов схема будет иметь примерно следующий вид:</span><span class="sxs-lookup"><span data-stu-id="d263c-122">Either way you get a view like the one below (when mostly expanded):</span></span>

![Обозреватель схемы Visual Studio с открытым файлом nuspec.xsd](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a><span data-ttu-id="d263c-124">Атрибуты метаданных</span><span class="sxs-lookup"><span data-stu-id="d263c-124">Metadata attributes</span></span>

<span data-ttu-id="d263c-125">Элемент `<metadata>` поддерживает атрибуты, описываемые в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="d263c-125">The `<metadata>` element supports the attributes described in the following table.</span></span>

| <span data-ttu-id="d263c-126">Атрибут</span><span class="sxs-lookup"><span data-stu-id="d263c-126">Attribute</span></span> | <span data-ttu-id="d263c-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d263c-127">Required</span></span> | <span data-ttu-id="d263c-128">Описание</span><span class="sxs-lookup"><span data-stu-id="d263c-128">Description</span></span> |
| --- | --- | --- | 
| <span data-ttu-id="d263c-129">**minClientVersion**</span><span class="sxs-lookup"><span data-stu-id="d263c-129">**minClientVersion**</span></span> | <span data-ttu-id="d263c-130">Нет</span><span class="sxs-lookup"><span data-stu-id="d263c-130">No</span></span> | <span data-ttu-id="d263c-131">*(Версия 2.5 и более поздние)* Указывает минимальную версию клиента NuGet, который может установить этот пакет с использованием nuget.exe и диспетчера пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d263c-131">*(2.5+)* Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="d263c-132">Используется во всех случаях, когда пакет зависит от конкретных функций в файле `.nuspec`, которые были добавлены в определенной версии клиента NuGet.</span><span class="sxs-lookup"><span data-stu-id="d263c-132">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="d263c-133">Например, для пакета, использующего атрибут `developmentDependency`, атрибуту `minClientVersion` необходимо присвоить значение "2.8".</span><span class="sxs-lookup"><span data-stu-id="d263c-133">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="d263c-134">Аналогичным образом, для пакета, использующего элемент `contentFiles` (см. следующий раздел), атрибуту `minClientVersion` необходимо присвоить значение "3.3".</span><span class="sxs-lookup"><span data-stu-id="d263c-134">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="d263c-135">Также обратите внимание, что клиенты NuGet версий, предшествующих 2.5, не распознают этот флаг и поэтому *всегда* отклоняют установку пакета независимо от значения атрибута `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="d263c-135">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span> |

### <a name="required-metadata-elements"></a><span data-ttu-id="d263c-136">Обязательные элементы метаданных</span><span class="sxs-lookup"><span data-stu-id="d263c-136">Required metadata elements</span></span>

<span data-ttu-id="d263c-137">Следующие элементы являются минимальным требованием для пакета, однако, несмотря на это, рекомендуется добавить [дополнительные элементы метаданных](#optional-metadata-elements), чтобы оптимизировать работу с вашим пакетом для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="d263c-137">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span>

<span data-ttu-id="d263c-138">Эти элементы должны использоваться внутри элемента `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="d263c-138">These elements must appear within a `<metadata>` element.</span></span>

| <span data-ttu-id="d263c-139">Элемент</span><span class="sxs-lookup"><span data-stu-id="d263c-139">Element</span></span> | <span data-ttu-id="d263c-140">Описание</span><span class="sxs-lookup"><span data-stu-id="d263c-140">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d263c-141">**id**</span><span class="sxs-lookup"><span data-stu-id="d263c-141">**id**</span></span> | <span data-ttu-id="d263c-142">Идентификатор пакета без учета регистра, который должен быть уникальным в пределах сайта nuget.org или иной коллекции, в которой находится пакет.</span><span class="sxs-lookup"><span data-stu-id="d263c-142">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="d263c-143">Идентификаторы не должны содержать пробелов или символов, которые недопустимы в URL-адресах, и в них должны соблюдаться общие правила касательно пространств имен .NET.</span><span class="sxs-lookup"><span data-stu-id="d263c-143">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="d263c-144">Инструкции см. в разделе [Выбор уникального идентификатора пакета](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="d263c-144">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
| <span data-ttu-id="d263c-145">**version**</span><span class="sxs-lookup"><span data-stu-id="d263c-145">**version**</span></span> | <span data-ttu-id="d263c-146">Версия пакета, указываемая согласно шаблону *основной_номер.дополнительный_номер.исправление*.</span><span class="sxs-lookup"><span data-stu-id="d263c-146">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="d263c-147">Номер версии может включать в себя суффикс предварительной версии, как описано в разделе [Управление версиями пакета](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="d263c-147">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> |
| <span data-ttu-id="d263c-148">**description**</span><span class="sxs-lookup"><span data-stu-id="d263c-148">**description**</span></span> | <span data-ttu-id="d263c-149">Подробное описание пакета для отображения пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d263c-149">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="d263c-150">**authors**</span><span class="sxs-lookup"><span data-stu-id="d263c-150">**authors**</span></span> | <span data-ttu-id="d263c-151">Разделенный запятыми список авторов пакетов, совпадающих с именами профилей на сайте nuget.org. Они отображаются в коллекции NuGet на сайте nuget.org и используются для перекрестных ссылок на пакеты тех же авторов.</span><span class="sxs-lookup"><span data-stu-id="d263c-151">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |

### <a name="optional-metadata-elements"></a><span data-ttu-id="d263c-152">Необязательные элементы метаданных</span><span class="sxs-lookup"><span data-stu-id="d263c-152">Optional metadata elements</span></span>

<span data-ttu-id="d263c-153">Эти элементы должны использоваться внутри элемента `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="d263c-153">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="single-elements"></a><span data-ttu-id="d263c-154">Одиночные элементы</span><span class="sxs-lookup"><span data-stu-id="d263c-154">Single elements</span></span>

| <span data-ttu-id="d263c-155">Элемент</span><span class="sxs-lookup"><span data-stu-id="d263c-155">Element</span></span> | <span data-ttu-id="d263c-156">Описание</span><span class="sxs-lookup"><span data-stu-id="d263c-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d263c-157">**title**</span><span class="sxs-lookup"><span data-stu-id="d263c-157">**title**</span></span> | <span data-ttu-id="d263c-158">Понятный заголовок пакета, обычно используемый при отображении пользовательского интерфейса, как на сайте nuget.org и в диспетчере пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d263c-158">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="d263c-159">Если значение не указано, используется идентификатор пакета.</span><span class="sxs-lookup"><span data-stu-id="d263c-159">If not specified, the package ID is used.</span></span> |
| <span data-ttu-id="d263c-160">**owners**</span><span class="sxs-lookup"><span data-stu-id="d263c-160">**owners**</span></span> | <span data-ttu-id="d263c-161">Разделенный запятыми список создателей пакета, совпадающих с именами профилей на сайте nuget.org. Часто совпадает со списком в элементе `authors` и игнорируется при загрузке пакета на веб-сайт nuget.org. См. раздел [Управление владельцами пакетов на веб-сайте nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="d263c-161">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> |
| <span data-ttu-id="d263c-162">**projectUrl**</span><span class="sxs-lookup"><span data-stu-id="d263c-162">**projectUrl**</span></span> | <span data-ttu-id="d263c-163">URL-адрес для домашней страницы пакета, часто указываемый при отображении пользовательского интерфейса, также как и nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d263c-163">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="d263c-164">**licenseUrl**</span><span class="sxs-lookup"><span data-stu-id="d263c-164">**licenseUrl**</span></span> | <span data-ttu-id="d263c-165">URL-адрес для лицензии пакета, часто указываемый при отображении пользовательского интерфейса, так же как и nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d263c-165">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="d263c-166">**iconUrl**</span><span class="sxs-lookup"><span data-stu-id="d263c-166">**iconUrl**</span></span> | <span data-ttu-id="d263c-167">URL-адрес для изображения размером 64x64 с прозрачным фоном, используемого в качестве значка для пакета при отображении пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d263c-167">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="d263c-168">Убедитесь, что этот элемент содержит *прямой URL-адрес изображения*, а не URL-адрес веб-страницы, на которой содержится изображение.</span><span class="sxs-lookup"><span data-stu-id="d263c-168">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="d263c-169">Например, чтобы использовать изображение из GitHub, укажите URL-адрес необработанного файла, такой как `https://github.com/<username>/<repository>/raw/<branch>/<logo.png>`.</span><span class="sxs-lookup"><span data-stu-id="d263c-169">For example, to use an image from GitHub, use the raw file URL like `https://github.com/<username>/<repository>/raw/<branch>/<logo.png>`.</span></span> |
| <span data-ttu-id="d263c-170">**requireLicenseAcceptance**</span><span class="sxs-lookup"><span data-stu-id="d263c-170">**requireLicenseAcceptance**</span></span> | <span data-ttu-id="d263c-171">Логическое значение, указывающее, должен ли клиент просить потребителя принять условия лицензии перед установкой пакета.</span><span class="sxs-lookup"><span data-stu-id="d263c-171">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| <span data-ttu-id="d263c-172">**developmentDependency**</span><span class="sxs-lookup"><span data-stu-id="d263c-172">**developmentDependency**</span></span> | <span data-ttu-id="d263c-173">*(Версия 2.8 и более поздние)* Логическое значение, указывающее, помечен ли пакет как зависимость только для разработки, что позволяет запретить его включение в качестве зависимости в другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="d263c-173">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> |
| <span data-ttu-id="d263c-174">**summary**</span><span class="sxs-lookup"><span data-stu-id="d263c-174">**summary**</span></span> | <span data-ttu-id="d263c-175">Краткое описание пакета для отображения пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d263c-175">A short description of the package for UI display.</span></span> <span data-ttu-id="d263c-176">Если этот элемент опущен, используется сокращенная версия элемента `description`.</span><span class="sxs-lookup"><span data-stu-id="d263c-176">If omitted, a truncated version of `description` is used.</span></span> |
| <span data-ttu-id="d263c-177">**releaseNotes**</span><span class="sxs-lookup"><span data-stu-id="d263c-177">**releaseNotes**</span></span> | <span data-ttu-id="d263c-178">*(Версия 1.5 и более поздние)* Описание изменений, внесенных в этом выпуске пакета NuGet; часто используется в пользовательском интерфейсе как вкладка **Обновления** диспетчера пакетов Visual Studio вместо описания пакета.</span><span class="sxs-lookup"><span data-stu-id="d263c-178">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span> |
| <span data-ttu-id="d263c-179">**copyright**</span><span class="sxs-lookup"><span data-stu-id="d263c-179">**copyright**</span></span> | <span data-ttu-id="d263c-180">*(Версия 1.5 и более поздние)* Сведения об авторских правах для пакета.</span><span class="sxs-lookup"><span data-stu-id="d263c-180">*(1.5+)* Copyright details for the package.</span></span> |
| <span data-ttu-id="d263c-181">**language**</span><span class="sxs-lookup"><span data-stu-id="d263c-181">**language**</span></span> | <span data-ttu-id="d263c-182">Идентификатор языкового стандарта для пакета.</span><span class="sxs-lookup"><span data-stu-id="d263c-182">The locale ID for the package.</span></span> <span data-ttu-id="d263c-183">См. раздел [Создание локализованных пакетов](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="d263c-183">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span> |
| <span data-ttu-id="d263c-184">**tags**</span><span class="sxs-lookup"><span data-stu-id="d263c-184">**tags**</span></span> | <span data-ttu-id="d263c-185">Список разделенных пробелами тегов и ключевых слов, описывающих пакет NuGet и помогающих находить пакеты NuGet с помощью функций поиска и фильтрации.</span><span class="sxs-lookup"><span data-stu-id="d263c-185">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> |
| <span data-ttu-id="d263c-186">**serviceable**</span><span class="sxs-lookup"><span data-stu-id="d263c-186">**serviceable**</span></span> | <span data-ttu-id="d263c-187">*(Версия 3.3 и более поздние)* Только для внутреннего использования в NuGet.</span><span class="sxs-lookup"><span data-stu-id="d263c-187">*(3.3+)* For internal NuGet use only.</span></span> |

#### <a name="collection-elements"></a><span data-ttu-id="d263c-188">Элементы коллекции</span><span class="sxs-lookup"><span data-stu-id="d263c-188">Collection elements</span></span>

| <span data-ttu-id="d263c-189">Элемент</span><span class="sxs-lookup"><span data-stu-id="d263c-189">Element</span></span> | <span data-ttu-id="d263c-190">Описание</span><span class="sxs-lookup"><span data-stu-id="d263c-190">Description</span></span> |
| --- | --- |
<span data-ttu-id="d263c-191">**packageTypes**</span><span class="sxs-lookup"><span data-stu-id="d263c-191">**packageTypes**</span></span> | <span data-ttu-id="d263c-192">*(Версия 3.3 и более поздние)* Коллекция из нуля или более элементов `<packageType>`, определяющих тип пакета, если он отличается от обычного пакета зависимостей.</span><span class="sxs-lookup"><span data-stu-id="d263c-192">*(3.3+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="d263c-193">Каждый элемент packageType имеет атрибуты *name* и *version*.</span><span class="sxs-lookup"><span data-stu-id="d263c-193">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="d263c-194">См. раздел [Указание типа пакета](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="d263c-194">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span> |
| <span data-ttu-id="d263c-195">**dependencies**</span><span class="sxs-lookup"><span data-stu-id="d263c-195">**dependencies**</span></span> | <span data-ttu-id="d263c-196">Коллекция из нуля или более элементов `<dependency>`, задающих зависимости для пакета.</span><span class="sxs-lookup"><span data-stu-id="d263c-196">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="d263c-197">Каждый элемент dependency имеет атрибуты *id*, *version*, *include* (версия 3.x и более поздние) и *exclude* (версия 3.x и более поздние).</span><span class="sxs-lookup"><span data-stu-id="d263c-197">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="d263c-198">См. раздел [Зависимости](#dependencies) далее.</span><span class="sxs-lookup"><span data-stu-id="d263c-198">See [Dependencies](#dependencies) below.</span></span> |
| <span data-ttu-id="d263c-199">**frameworkAssemblies**</span><span class="sxs-lookup"><span data-stu-id="d263c-199">**frameworkAssemblies**</span></span> | <span data-ttu-id="d263c-200">*(Версия 1.2 и более поздние)* Коллекция из одного или более элементов `<frameworkAssembly>`, идентифицирующих ссылки на сборки .NET Framework, необходимые для этого пакета, что гарантирует добавление ссылок в проекты, использующие пакет.</span><span class="sxs-lookup"><span data-stu-id="d263c-200">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="d263c-201">Каждый элемент frameworkAssembly имеет атрибуты *assemblyName* и *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="d263c-201">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="d263c-202">См. раздел [Указание ссылок на сборки платформы в глобальном кэше сборок ](#specifying-framework-assembly-references-gac) ниже.</span><span class="sxs-lookup"><span data-stu-id="d263c-202">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
| <span data-ttu-id="d263c-203">**references**</span><span class="sxs-lookup"><span data-stu-id="d263c-203">**references**</span></span> | <span data-ttu-id="d263c-204">*(Версия 1.5 и более поздние)* Коллекция из нуля или более элементов `<reference>`, задающие имена сборок в папке `lib` пакета, которые добавляются в качестве ссылок проекта.</span><span class="sxs-lookup"><span data-stu-id="d263c-204">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="d263c-205">Каждый элемент reference имеет атрибут *file*.</span><span class="sxs-lookup"><span data-stu-id="d263c-205">Each reference has a *file* attribute.</span></span> <span data-ttu-id="d263c-206">Коллекция `<references>` также может содержать элемент `<group>` с атрибутом *targetFramework*, который, в свою очередь, содержит элементы `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="d263c-206">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="d263c-207">Если этот элемент опущен, включаются все ссылки в папке `lib`.</span><span class="sxs-lookup"><span data-stu-id="d263c-207">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="d263c-208">См. раздел [Указание явных ссылок на сборки](#specifying-explicit-assembly-references) ниже.</span><span class="sxs-lookup"><span data-stu-id="d263c-208">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span> |
| <span data-ttu-id="d263c-209">**contentFiles**</span><span class="sxs-lookup"><span data-stu-id="d263c-209">**contentFiles**</span></span> | <span data-ttu-id="d263c-210">*(Версия 3.3 и более поздние)* Коллекция элементов `<files>`, которые идентифицируют файлы содержимого, включаемые в потребляющий проект.</span><span class="sxs-lookup"><span data-stu-id="d263c-210">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="d263c-211">Эти файлы задаются с набором атрибутов, который описывает их использование в системе проекта.</span><span class="sxs-lookup"><span data-stu-id="d263c-211">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="d263c-212">См. раздел [Указание включаемых в пакет файлов](#specifying-files-to-include-in-the-package) ниже.</span><span class="sxs-lookup"><span data-stu-id="d263c-212">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span> |

### <a name="files-element"></a><span data-ttu-id="d263c-213">Files - элемент</span><span class="sxs-lookup"><span data-stu-id="d263c-213">Files element</span></span>

<span data-ttu-id="d263c-214">Узел `<package>` может содержать узел `<files>`, который является одноуровневым для узла `<metadata>`, или дочерний узел `<contentFiles>` в узле `<metadata>`, который задает файлы сборки и содержимого, включаемые в пакет.</span><span class="sxs-lookup"><span data-stu-id="d263c-214">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="d263c-215">Дополнительные сведения см. далее в разделах [Включение файлов сборки](#including-assembly-files) и [Включение файлов содержимого](#including-content-files) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="d263c-215">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="d263c-216">Замена маркеров</span><span class="sxs-lookup"><span data-stu-id="d263c-216">Replacement tokens</span></span>

<span data-ttu-id="d263c-217">При создании пакета [команда `nuget pack`](../tools/cli-ref-pack.md) заменяет маркеры с разделителями $ в узле `<metadata>` файла `.nuspec` значениями из файла проекта или параметра `-properties` команды `pack`.</span><span class="sxs-lookup"><span data-stu-id="d263c-217">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="d263c-218">Маркеры задаются в командной строке следующим образом: `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="d263c-218">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="d263c-219">Например, вы можете использовать маркер, такой как `$owners$` и `$desc$`, в файле `.nuspec` и предоставить значения во время упаковки следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d263c-219">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="d263c-220">Чтобы использовать значения из проекта, укажите маркеры, описываемые в следующей таблице (AssemblyInfo ссылается на файл в `Properties`, например `AssemblyInfo.cs` или `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="d263c-220">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="d263c-221">Чтобы использовать эти маркеры, выполните команду `nuget pack` с файлом проекта, а не просто с файлом `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="d263c-221">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="d263c-222">Например, при использовании следующей команды маркеры `$id$` и `$version$` в файле `.nuspec` заменяются значениями проекта `AssemblyName` и `AssemblyVersion`:</span><span class="sxs-lookup"><span data-stu-id="d263c-222">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="d263c-223">Как правило, при наличии проекта вы изначально создаете файл `.nuspec` с использованием команды `nuget spec MyProject.csproj`, которая автоматически включает некоторые из этих стандартных маркеров.</span><span class="sxs-lookup"><span data-stu-id="d263c-223">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="d263c-224">Тем не менее, если в проекте отсутствуют значения для обязательных элементов `.nuspec`, команда `nuget pack` завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="d263c-224">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="d263c-225">Кроме того, при изменении значений проекта необходимо выполнить перестроение до создания пакета. Это можно легко сделать с помощью параметра `build` команды pack.</span><span class="sxs-lookup"><span data-stu-id="d263c-225">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="d263c-226">За исключением элемента `$configuration$`, значения в проекте используются в приоритетном порядке относительно любых значений, назначенных тому же маркеру в командной строке.</span><span class="sxs-lookup"><span data-stu-id="d263c-226">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="d263c-227">Токен</span><span class="sxs-lookup"><span data-stu-id="d263c-227">Token</span></span> | <span data-ttu-id="d263c-228">Источник значения</span><span class="sxs-lookup"><span data-stu-id="d263c-228">Value source</span></span> | <span data-ttu-id="d263c-229">Значение</span><span class="sxs-lookup"><span data-stu-id="d263c-229">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="d263c-230">**$id$**</span><span class="sxs-lookup"><span data-stu-id="d263c-230">**$id$**</span></span> | <span data-ttu-id="d263c-231">Файл проекта</span><span class="sxs-lookup"><span data-stu-id="d263c-231">Project file</span></span> | <span data-ttu-id="d263c-232">AssemblyName из файла проекта</span><span class="sxs-lookup"><span data-stu-id="d263c-232">AssemblyName from the project file</span></span> |
| <span data-ttu-id="d263c-233">**$version$**</span><span class="sxs-lookup"><span data-stu-id="d263c-233">**$version$**</span></span> | <span data-ttu-id="d263c-234">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d263c-234">AssemblyInfo</span></span> | <span data-ttu-id="d263c-235">AssemblyInformationalVersion, если присутствует, в противном случае AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="d263c-235">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="d263c-236">**$author$**</span><span class="sxs-lookup"><span data-stu-id="d263c-236">**$author$**</span></span> | <span data-ttu-id="d263c-237">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d263c-237">AssemblyInfo</span></span> | <span data-ttu-id="d263c-238">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="d263c-238">AssemblyCompany</span></span> |
| <span data-ttu-id="d263c-239">**$description$**</span><span class="sxs-lookup"><span data-stu-id="d263c-239">**$description$**</span></span> | <span data-ttu-id="d263c-240">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d263c-240">AssemblyInfo</span></span> | <span data-ttu-id="d263c-241">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="d263c-241">AssemblyDescription</span></span> |
| <span data-ttu-id="d263c-242">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="d263c-242">**$copyright$**</span></span> | <span data-ttu-id="d263c-243">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d263c-243">AssemblyInfo</span></span> | <span data-ttu-id="d263c-244">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="d263c-244">AssemblyCopyright</span></span> |
| <span data-ttu-id="d263c-245">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="d263c-245">**$configuration$**</span></span> | <span data-ttu-id="d263c-246">DLL-файл сборки</span><span class="sxs-lookup"><span data-stu-id="d263c-246">Assembly DLL</span></span> | <span data-ttu-id="d263c-247">Конфигурация, используемая для построения сборки, по умолчанию используется тип отладки.</span><span class="sxs-lookup"><span data-stu-id="d263c-247">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="d263c-248">Обратите внимание, что для создания пакета с помощью конфигурации выпуска в командной строке всегда используется параметр `-properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="d263c-248">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="d263c-249">Маркеры также можно использовать для разрешения путей при включении [файлов сборок](#including-assembly-files) и [файлов содержимого](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="d263c-249">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="d263c-250">Маркеры имеют те же имена, что и свойства MSBuild, что позволяет выбирать файлы для включения в зависимости в текущей конфигурации построения.</span><span class="sxs-lookup"><span data-stu-id="d263c-250">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="d263c-251">Например, если вы используете следующие маркеры в файле `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="d263c-251">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="d263c-252">И выполняете построение сборки, для которой `AssemblyName` имеет значение `LoggingLibrary` с конфигурацией `Release` в MSBuild, в файле `.nuspec` в пакете будут присутствовать следующие строки:</span><span class="sxs-lookup"><span data-stu-id="d263c-252">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a><span data-ttu-id="d263c-253">Зависимости</span><span class="sxs-lookup"><span data-stu-id="d263c-253">Dependencies</span></span>

<span data-ttu-id="d263c-254">Элемент `<dependencies>` внутри элемента `<metadata>` содержит любое число элементов `<dependency>`, идентифицирующих другие пакеты, от которых зависит пакет верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="d263c-254">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="d263c-255">Ниже перечислены атрибуты каждого элемента `<dependency>`:</span><span class="sxs-lookup"><span data-stu-id="d263c-255">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="d263c-256">Атрибут</span><span class="sxs-lookup"><span data-stu-id="d263c-256">Attribute</span></span> | <span data-ttu-id="d263c-257">Описание</span><span class="sxs-lookup"><span data-stu-id="d263c-257">Description</span></span> |
| --- | --- | 
| `id` | <span data-ttu-id="d263c-258">Идентификатор пакета для зависимости (обязательно).</span><span class="sxs-lookup"><span data-stu-id="d263c-258">(Required) The package ID of the dependency.</span></span> |
| `version` | <span data-ttu-id="d263c-259">Диапазон версий, которые допустимы в качестве зависимости (обязательно).</span><span class="sxs-lookup"><span data-stu-id="d263c-259">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="d263c-260">Точный синтаксис см. в разделе [Управление версиями пакета](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="d263c-260">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="d263c-261">include</span><span class="sxs-lookup"><span data-stu-id="d263c-261">include</span></span> | <span data-ttu-id="d263c-262">Разделенный запятыми список тегов включения или исключения (см. ниже), определяющий зависимости, включаемые в конечный пакет.</span><span class="sxs-lookup"><span data-stu-id="d263c-262">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="d263c-263">Значение по умолчанию — `none`.</span><span class="sxs-lookup"><span data-stu-id="d263c-263">The default value is `none`.</span></span> |
| <span data-ttu-id="d263c-264">exclude</span><span class="sxs-lookup"><span data-stu-id="d263c-264">exclude</span></span> | <span data-ttu-id="d263c-265">Разделенный запятыми список тегов включения или исключения (см. ниже), определяющий зависимости, исключаемые из конечного пакета.</span><span class="sxs-lookup"><span data-stu-id="d263c-265">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="d263c-266">Значение по умолчанию — `all`.</span><span class="sxs-lookup"><span data-stu-id="d263c-266">The  default value is `all`.</span></span> <span data-ttu-id="d263c-267">Теги в свойстве `exclude` имеют приоритет перед тегами в свойстве `include`.</span><span class="sxs-lookup"><span data-stu-id="d263c-267">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="d263c-268">Например, `include="runtime, compile" exclude="compile"` равносильно `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="d263c-268">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="d263c-269">Тег включения или исключения</span><span class="sxs-lookup"><span data-stu-id="d263c-269">Include/Exclude tag</span></span> | <span data-ttu-id="d263c-270">Затрагиваемые папки пакета</span><span class="sxs-lookup"><span data-stu-id="d263c-270">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="d263c-271">contentFiles</span><span class="sxs-lookup"><span data-stu-id="d263c-271">contentFiles</span></span> | <span data-ttu-id="d263c-272">Content</span><span class="sxs-lookup"><span data-stu-id="d263c-272">Content</span></span>  |
| <span data-ttu-id="d263c-273">исполняющая среда</span><span class="sxs-lookup"><span data-stu-id="d263c-273">runtime</span></span> | <span data-ttu-id="d263c-274">Runtime, Resources и FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="d263c-274">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="d263c-275">compile</span><span class="sxs-lookup"><span data-stu-id="d263c-275">compile</span></span> | <span data-ttu-id="d263c-276">lib</span><span class="sxs-lookup"><span data-stu-id="d263c-276">lib</span></span> |
| <span data-ttu-id="d263c-277">построение</span><span class="sxs-lookup"><span data-stu-id="d263c-277">build</span></span> | <span data-ttu-id="d263c-278">build (свойства и цели MSBuild)</span><span class="sxs-lookup"><span data-stu-id="d263c-278">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="d263c-279">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="d263c-279">native</span></span> | <span data-ttu-id="d263c-280">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="d263c-280">native</span></span> |
| <span data-ttu-id="d263c-281">Нет</span><span class="sxs-lookup"><span data-stu-id="d263c-281">none</span></span> | <span data-ttu-id="d263c-282">Нет</span><span class="sxs-lookup"><span data-stu-id="d263c-282">No folders</span></span> |
| <span data-ttu-id="d263c-283">все</span><span class="sxs-lookup"><span data-stu-id="d263c-283">all</span></span> | <span data-ttu-id="d263c-284">Все папки</span><span class="sxs-lookup"><span data-stu-id="d263c-284">All folders</span></span> |

<span data-ttu-id="d263c-285">Например, следующие строки указывают зависимости от `PackageA` версии 1.1.0 или более поздней и `PackageB` версии 1.x.</span><span class="sxs-lookup"><span data-stu-id="d263c-285">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="d263c-286">Следующие строки указывают зависимости от тех же пакетов и включают папки `contentFiles` и `build` для `PackageA`, а также все папки, кроме `native` и `compile`, для `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="d263c-286">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="d263c-287">Примечание. При создании файла `.nuspec` для проекта с использованием команды `nuget spec` существующие в проекте зависимости автоматически включаются в полученный файл `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="d263c-287">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="d263c-288">Группы зависимостей</span><span class="sxs-lookup"><span data-stu-id="d263c-288">Dependency groups</span></span>

<span data-ttu-id="d263c-289">*Версия 2.0 и более поздние*</span><span class="sxs-lookup"><span data-stu-id="d263c-289">*Version 2.0+*</span></span>

<span data-ttu-id="d263c-290">В качестве альтернативы простому неструктурированному списку зависимости могут задаваться в соответствии с профилем платформы целевого проекта с использованием элементов `<group>` в элементе `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="d263c-290">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="d263c-291">Каждый элемент group имеет атрибут `targetFramework` и содержит ноль или более элементов `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="d263c-291">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="d263c-292">Эти зависимости устанавливаются вместе в том случае, если целевая платформа совместима с профилем платформы проекта.</span><span class="sxs-lookup"><span data-stu-id="d263c-292">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="d263c-293">Элемент `<group>` без атрибута `targetFramework` используется в качестве установленного по умолчанию или резервного списка зависимостей.</span><span class="sxs-lookup"><span data-stu-id="d263c-293">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="d263c-294">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../schema/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="d263c-294">See [Target frameworks](../schema/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="d263c-295">Формат группы не может смешиваться с неструктурированным списком.</span><span class="sxs-lookup"><span data-stu-id="d263c-295">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="d263c-296">В следующем примере приводятся различные варианты элемента `<group>`:</span><span class="sxs-lookup"><span data-stu-id="d263c-296">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="d263c-297">Явные ссылки на сборку</span><span class="sxs-lookup"><span data-stu-id="d263c-297">Explicit assembly references</span></span>

<span data-ttu-id="d263c-298">Элемент `<references>` явно задает сборки, на которые целевой проект должен ссылаться при использовании пакета.</span><span class="sxs-lookup"><span data-stu-id="d263c-298">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="d263c-299">Если этот элемент присутствует, NuGet добавляет ссылки только на указанные в списке сборки, но не на какие-либо другие сборки в папке `lib` проекта.</span><span class="sxs-lookup"><span data-stu-id="d263c-299">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="d263c-300">Например, следующий элемент `<references>` указывает NuGet на необходимость добавлять ссылки только на сборки `xunit.dll` и `xunit.extensions.dll`, даже если в пакете есть другие сборки:</span><span class="sxs-lookup"><span data-stu-id="d263c-300">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="d263c-301">Явные ссылки обычно применяются для сборок, используемых только во время разработки.</span><span class="sxs-lookup"><span data-stu-id="d263c-301">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="d263c-302">При использовании [контрактов для кода](https://docs.microsoft.com/dotnet/framework/debug-trace-profile/code-contracts) сборки контракта должны располагаться рядом со сборками среды выполнения, которые они расширяют, чтобы среда Visual Studio могла находить их. При этом не требуются ссылки на сборки контракта из проекта и эти сборки не нужно копировать в папку `bin` проекта.</span><span class="sxs-lookup"><span data-stu-id="d263c-302">When using [Code Contracts](https://docs.microsoft.com/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="d263c-303">Аналогичным образом, явные ссылки можно использовать для платформ модульного тестирования, таких как XUnit, сборки средств которых должны располагаться рядом со сборками среды выполнения, но не требуют включения в ссылки проекта.</span><span class="sxs-lookup"><span data-stu-id="d263c-303">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="d263c-304">Группы ссылок</span><span class="sxs-lookup"><span data-stu-id="d263c-304">Reference groups</span></span>

<span data-ttu-id="d263c-305">*Версия 2.5 и более поздние*</span><span class="sxs-lookup"><span data-stu-id="d263c-305">*Version 2.5+*</span></span>

<span data-ttu-id="d263c-306">В качестве альтернативы простому неструктурированному списку ссылки могут задаваться в соответствии с профилем платформы целевого проекта с использованием элементов `<group>` в элементе `<references>`.</span><span class="sxs-lookup"><span data-stu-id="d263c-306">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="d263c-307">Каждый элемент group имеет атрибут `targetFramework` и содержит ноль или более элементов `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="d263c-307">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="d263c-308">Эти ссылки добавляются в проект в том случае, если целевая платформа совместима с профилем платформы проекта.</span><span class="sxs-lookup"><span data-stu-id="d263c-308">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="d263c-309">Элемент `<group>` без атрибута `targetFramework` используется в качестве установленного по умолчанию или резервного списка ссылок.</span><span class="sxs-lookup"><span data-stu-id="d263c-309">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="d263c-310">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../schema/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="d263c-310">See [Target frameworks](../schema/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="d263c-311">Формат группы не может смешиваться с неструктурированным списком.</span><span class="sxs-lookup"><span data-stu-id="d263c-311">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="d263c-312">В следующем примере приводятся различные варианты элемента `<group>`:</span><span class="sxs-lookup"><span data-stu-id="d263c-312">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="d263c-313">Ссылки на сборку платформы</span><span class="sxs-lookup"><span data-stu-id="d263c-313">Framework assembly references</span></span>

<span data-ttu-id="d263c-314">Сборки платформы входят в состав .NET Framework и должны находиться в глобальном кэше сборок любого заданного компьютера.</span><span class="sxs-lookup"><span data-stu-id="d263c-314">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="d263c-315">Идентифицируя такие сборки с помощью элемента `<frameworkAssemblies>`, пакет может гарантировать, что ссылки, отсутствующие в проекте, будут при необходимости добавлены в него.</span><span class="sxs-lookup"><span data-stu-id="d263c-315">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="d263c-316">Естественно, напрямую в пакет такие сборки не включаются.</span><span class="sxs-lookup"><span data-stu-id="d263c-316">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="d263c-317">Элемент `<frameworkAssemblies>` содержит ноль или более элементов `<frameworkAssembly>`, каждый из которых задает следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="d263c-317">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="d263c-318">Атрибут</span><span class="sxs-lookup"><span data-stu-id="d263c-318">Attribute</span></span> | <span data-ttu-id="d263c-319">Описание</span><span class="sxs-lookup"><span data-stu-id="d263c-319">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d263c-320">**имя_сборки**</span><span class="sxs-lookup"><span data-stu-id="d263c-320">**assemblyName**</span></span> | <span data-ttu-id="d263c-321">Полное имя сборки (обязательно).</span><span class="sxs-lookup"><span data-stu-id="d263c-321">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="d263c-322">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="d263c-322">**targetFramework**</span></span> | <span data-ttu-id="d263c-323">Указывает целевую платформу, к которой применяется эта ссылка (необязательно).</span><span class="sxs-lookup"><span data-stu-id="d263c-323">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="d263c-324">Если этот атрибут опущен, указывает, что ссылка применяется ко всем платформам.</span><span class="sxs-lookup"><span data-stu-id="d263c-324">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="d263c-325">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../schema/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="d263c-325">See [Target frameworks](../schema/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="d263c-326">В следующем примере показаны ссылка на `System.Net` для всех целевых платформ и ссылка на `System.ServiceModel` только для платформы .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="d263c-326">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="d263c-327">Включение файлов сборки</span><span class="sxs-lookup"><span data-stu-id="d263c-327">Including assembly files</span></span>

<span data-ttu-id="d263c-328">Если вы придерживаетесь соглашений, описываемых в разделе [Создание пакета](../create-packages/creating-a-package.md), вам не нужно явно задавать список файлов в файле `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="d263c-328">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="d263c-329">Команда `nuget pack` автоматически выбирает необходимые файлы.</span><span class="sxs-lookup"><span data-stu-id="d263c-329">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="d263c-330">Когда пакет устанавливается в проекте, NuGet автоматически добавляет ссылки на библиотеки DLL сборок в пакете, *кроме* тех из них, в именах которых есть `.resources.dll`, так как они считаются локализованными вспомогательными сборками.</span><span class="sxs-lookup"><span data-stu-id="d263c-330">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="d263c-331">По этой причине следует избегать использования `.resources.dll` в именах файлов пакета, которые содержат важный код.</span><span class="sxs-lookup"><span data-stu-id="d263c-331">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="d263c-332">Чтобы обойти такое автоматическое поведение и явно управлять включением сборок в пакет, поместите элемент `<files>` в качестве дочернего для `<package>` (на одном уровне с `<metadata>`), указывая каждый файл с помощью элемента `<file>`.</span><span class="sxs-lookup"><span data-stu-id="d263c-332">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="d263c-333">Пример:</span><span class="sxs-lookup"><span data-stu-id="d263c-333">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="d263c-334">В NuGet версии 2.x и более ранних в проектах, использующих `packages.config`, элемент `<files>` также используется для включения неизменяемых файлов содержимого при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="d263c-334">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="d263c-335">В NuGet версии 3.3 и более поздних для проектов, использующих `project.json` или PackageReference, вместо этого используется элемент `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="d263c-335">With NuGet 3.3+ and projects using `project.json` pr PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="d263c-336">Дополнительные сведения см. в разделе [Включение файлов содержимого](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="d263c-336">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="d263c-337">Атрибуты элементов файла</span><span class="sxs-lookup"><span data-stu-id="d263c-337">File element attributes</span></span>

<span data-ttu-id="d263c-338">Каждый элемент `<file>` задает указанные ниже атрибуты:</span><span class="sxs-lookup"><span data-stu-id="d263c-338">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="d263c-339">Атрибут</span><span class="sxs-lookup"><span data-stu-id="d263c-339">Attribute</span></span> | <span data-ttu-id="d263c-340">Описание</span><span class="sxs-lookup"><span data-stu-id="d263c-340">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d263c-341">**src**</span><span class="sxs-lookup"><span data-stu-id="d263c-341">**src**</span></span> | <span data-ttu-id="d263c-342">Расположение файла или файлов, которые требуется включить, с учетом исключений, задаваемых атрибутом `exclude`.</span><span class="sxs-lookup"><span data-stu-id="d263c-342">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="d263c-343">Если не указан абсолютный путь, этот путь задается относительно файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="d263c-343">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="d263c-344">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="d263c-344">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="d263c-345">**target**</span><span class="sxs-lookup"><span data-stu-id="d263c-345">**target**</span></span> | <span data-ttu-id="d263c-346">Относительный путь к папке в пакете, куда помещаются файлы исходного кода. Должен начинаться с `lib`, `content`, `build` или `tools`.</span><span class="sxs-lookup"><span data-stu-id="d263c-346">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="d263c-347">См. раздел [Создание файла NUSPEC на основе рабочего каталога, соответствующего соглашениям](../Create-Packages/Creating-a-Package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="d263c-347">See [Creating a .nuspec from a convention-based working directory](../Create-Packages/Creating-a-Package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="d263c-348">**exclude**</span><span class="sxs-lookup"><span data-stu-id="d263c-348">**exclude**</span></span> | <span data-ttu-id="d263c-349">Разделенный точками с запятой список файлов или шаблонов файлов, которые исключаются из расположения `src`.</span><span class="sxs-lookup"><span data-stu-id="d263c-349">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="d263c-350">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="d263c-350">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="d263c-351">Примеры</span><span class="sxs-lookup"><span data-stu-id="d263c-351">Examples</span></span>

<span data-ttu-id="d263c-352">**Одна сборка**</span><span class="sxs-lookup"><span data-stu-id="d263c-352">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="d263c-353">**Одна сборка, относящаяся к целевой платформе**</span><span class="sxs-lookup"><span data-stu-id="d263c-353">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="d263c-354">**Набор DLL-файлов с использованием подстановочного знака**</span><span class="sxs-lookup"><span data-stu-id="d263c-354">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="d263c-355">**DLL-файлы для разных платформ**</span><span class="sxs-lookup"><span data-stu-id="d263c-355">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="d263c-356">**Исключение файлов**</span><span class="sxs-lookup"><span data-stu-id="d263c-356">**Excluding files**</span></span>

    Source files:
        \tools\*.bak
        \tools\*.log
        \tools\build\*.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a><span data-ttu-id="d263c-357">Включение файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="d263c-357">Including content files</span></span>

<span data-ttu-id="d263c-358">Файлы содержимого — это неизменяемые файлы, которые пакету необходимо включить в проект.</span><span class="sxs-lookup"><span data-stu-id="d263c-358">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="d263c-359">Такие файлы не подлежат изменению проектом, который потребляет их.</span><span class="sxs-lookup"><span data-stu-id="d263c-359">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="d263c-360">Примеры файлов содержимого:</span><span class="sxs-lookup"><span data-stu-id="d263c-360">Example content files include:</span></span>

- <span data-ttu-id="d263c-361">Изображения, внедряемые в качестве ресурсов</span><span class="sxs-lookup"><span data-stu-id="d263c-361">Images that are embedded as resources</span></span>
- <span data-ttu-id="d263c-362">Файлы исходного кода, которые уже были скомпилированы</span><span class="sxs-lookup"><span data-stu-id="d263c-362">Source files that are already compiled</span></span>
- <span data-ttu-id="d263c-363">Скрипты, которые необходимо включить в выходные данные построения проекта</span><span class="sxs-lookup"><span data-stu-id="d263c-363">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="d263c-364">Файлы конфигурации для пакета, которые необходимо включить в проект, но не требуется изменять в рамках отдельного проекта</span><span class="sxs-lookup"><span data-stu-id="d263c-364">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="d263c-365">Файлы содержимого включаются в проект с помощью элемента `<files>`, задающего папку `content` в атрибуте `target`.</span><span class="sxs-lookup"><span data-stu-id="d263c-365">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="d263c-366">Тем не менее такие файлы игнорируются при установке пакета в проект с использованием системы `project.json` в NuGet версии 3.3 или более поздней, либо PackageReference в NuGet версии 4 или более поздней, в которых вместо этого используется элемент `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="d263c-366">However, such files are ignored when the package is installed in a project using the `project.json` system in NuGet 3.3+ or PackageReference in NuGet 4+, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="d263c-367">Чтобы обеспечить максимальную совместимость с потребляющими проектами, в идеальном случае файлы содержимого следует задавать в проекте с использованием обоих элементов.</span><span class="sxs-lookup"><span data-stu-id="d263c-367">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="d263c-368">Использование элемента files для файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="d263c-368">Using the files element for content files</span></span>

<span data-ttu-id="d263c-369">Для файлов содержимого следует использовать тот же формат, что и для файлов сборки, однако необходимо указать в качестве базовой сборки `content` в атрибуте `target`, как показано в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="d263c-369">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="d263c-370">**Базовые файлы содержимого**</span><span class="sxs-lookup"><span data-stu-id="d263c-370">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="d263c-371">**Файлы содержимого со структурой каталогов**</span><span class="sxs-lookup"><span data-stu-id="d263c-371">**Content files with directory structure**</span></span>

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

<span data-ttu-id="d263c-372">**Файлы содержимого, относящиеся к целевой платформе**</span><span class="sxs-lookup"><span data-stu-id="d263c-372">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="d263c-373">**Файлы содержимого, копируемые в папку с точкой в имени**</span><span class="sxs-lookup"><span data-stu-id="d263c-373">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="d263c-374">В этом случае NuGet определяет, что расширение в атрибуте `target` не соответствует расширению в `src` и обрабатывает такую часть имени в атрибуте `target` как папку:</span><span class="sxs-lookup"><span data-stu-id="d263c-374">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="d263c-375">**Файлы содержимого без расширений**</span><span class="sxs-lookup"><span data-stu-id="d263c-375">**Content files without extensions**</span></span>

<span data-ttu-id="d263c-376">Чтобы включить файлы без расширения, используйте подстановочные знаки `*` или `**`:</span><span class="sxs-lookup"><span data-stu-id="d263c-376">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="d263c-377">**Файлы содержимого с глубоким путем и глубоким целевым объектом**</span><span class="sxs-lookup"><span data-stu-id="d263c-377">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="d263c-378">В этом случае из-за совпадения расширений файлов для исходного и целевого объектов NuGet предполагает, что целевой объект задает имя файла, а не папки:</span><span class="sxs-lookup"><span data-stu-id="d263c-378">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="d263c-379">**Переименование файла содержимого в пакете**</span><span class="sxs-lookup"><span data-stu-id="d263c-379">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="d263c-380">**Исключение файлов**</span><span class="sxs-lookup"><span data-stu-id="d263c-380">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="d263c-381">Использование элемента contentFiles для файлов содержимого</span><span class="sxs-lookup"><span data-stu-id="d263c-381">Using the contentFiles element for content files</span></span>

<span data-ttu-id="d263c-382">*Версия 3.3 и более поздние с project.json и версия 4.0 и более поздние с PackageReference*</span><span class="sxs-lookup"><span data-stu-id="d263c-382">*Version 3.3+ with project.json and 4.0+ with PackageReference*</span></span>

<span data-ttu-id="d263c-383">По умолчанию пакет помещает содержимое в папку `contentFiles` (см. ниже), а команда `nuget pack` включает все файлы в этой папке с использованием установленных по умолчанию атрибутов.</span><span class="sxs-lookup"><span data-stu-id="d263c-383">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="d263c-384">В этом случае включать узел `contentFiles` в файл `.nuspec` не требуется.</span><span class="sxs-lookup"><span data-stu-id="d263c-384">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="d263c-385">Чтобы управлять включаемыми файлами, элемент `<contentFiles>` задает коллекцию элементов `<files>`, которая точно определяет включаемые файлы.</span><span class="sxs-lookup"><span data-stu-id="d263c-385">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="d263c-386">Эти файлы задаются с набором атрибутов, который описывает их использование в системе проекта:</span><span class="sxs-lookup"><span data-stu-id="d263c-386">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="d263c-387">Атрибут</span><span class="sxs-lookup"><span data-stu-id="d263c-387">Attribute</span></span> | <span data-ttu-id="d263c-388">Описание</span><span class="sxs-lookup"><span data-stu-id="d263c-388">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d263c-389">**include**</span><span class="sxs-lookup"><span data-stu-id="d263c-389">**include**</span></span> | <span data-ttu-id="d263c-390">Расположение файла или файлов, которые требуется включить, с учетом исключений, задаваемых атрибутом `exclude` (обязательно).</span><span class="sxs-lookup"><span data-stu-id="d263c-390">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="d263c-391">Если не указан абсолютный путь, этот путь задается относительно файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="d263c-391">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="d263c-392">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="d263c-392">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="d263c-393">**exclude**</span><span class="sxs-lookup"><span data-stu-id="d263c-393">**exclude**</span></span> | <span data-ttu-id="d263c-394">Разделенный точками с запятой список файлов или шаблонов файлов, которые исключаются из расположения `src`.</span><span class="sxs-lookup"><span data-stu-id="d263c-394">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="d263c-395">Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке.</span><span class="sxs-lookup"><span data-stu-id="d263c-395">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="d263c-396">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="d263c-396">**buildAction**</span></span> | <span data-ttu-id="d263c-397">Действие построения, назначаемое элементу содержимого для MSBuild, например `Content`, `None`, `Embedded Resource`, `Compile` и т. д. Значение по умолчанию — `Compile`.</span><span class="sxs-lookup"><span data-stu-id="d263c-397">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="d263c-398">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="d263c-398">**copyToOutput**</span></span> | <span data-ttu-id="d263c-399">Логическое значение, указывающее на необходимость копировать элементы содержимого в папку выходных данных построения.</span><span class="sxs-lookup"><span data-stu-id="d263c-399">A Boolean indicating whether to copy content items to the build output folder.</span></span> <span data-ttu-id="d263c-400">Значение по умолчанию – false.</span><span class="sxs-lookup"><span data-stu-id="d263c-400">The default is false.</span></span> |
| <span data-ttu-id="d263c-401">**flatten**</span><span class="sxs-lookup"><span data-stu-id="d263c-401">**flatten**</span></span> | <span data-ttu-id="d263c-402">Логическое значение, указывающее на необходимость копировать элементы содержимого в одну папку в выходных данных построения (true) или сохранить структуру папок пакета (false).</span><span class="sxs-lookup"><span data-stu-id="d263c-402">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="d263c-403">Значение по умолчанию – false.</span><span class="sxs-lookup"><span data-stu-id="d263c-403">The default is false.</span></span> |

<span data-ttu-id="d263c-404">При установке пакета NuGet применяет дочерние элементы `<contentFiles>` в порядке сверху вниз.</span><span class="sxs-lookup"><span data-stu-id="d263c-404">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="d263c-405">Если одному файлу соответствует несколько записей, применяются все записи.</span><span class="sxs-lookup"><span data-stu-id="d263c-405">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="d263c-406">При обнаружении конфликтов для одного атрибута запись верхнего уровня переопределяет записи на нижних уровнях.</span><span class="sxs-lookup"><span data-stu-id="d263c-406">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="d263c-407">Структура папки пакета</span><span class="sxs-lookup"><span data-stu-id="d263c-407">Package folder structure</span></span>

<span data-ttu-id="d263c-408">Структурирование содержимого в проекте пакета осуществляется по следующему шаблону:</span><span class="sxs-lookup"><span data-stu-id="d263c-408">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="d263c-409">Элемент `codeLanguages` может иметь значение `cs`, `vb`, `fs`, `any` или любой другой эквивалент заданного `$(ProjectLanguage)` в нижнем регистре</span><span class="sxs-lookup"><span data-stu-id="d263c-409">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="d263c-410">Элемент `TxM` представляет любой допустимый моникер целевой платформы, поддерживаемой NuGet (см. раздел [Целевые платформы](../schema/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="d263c-410">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../schema/target-frameworks.md)).</span></span>
- <span data-ttu-id="d263c-411">В конце этого синтаксиса может добавляться любая структура папок.</span><span class="sxs-lookup"><span data-stu-id="d263c-411">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="d263c-412">Пример:</span><span class="sxs-lookup"><span data-stu-id="d263c-412">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="d263c-413">Для пустых папок можно использовать `.`, чтобы отказаться от предоставления содержимого для определенных комбинаций языка и моникера целевой платформы, например:</span><span class="sxs-lookup"><span data-stu-id="d263c-413">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="d263c-414">Пример раздела contentFiles</span><span class="sxs-lookup"><span data-stu-id="d263c-414">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="d263c-415">Примеры файлов NUSPEC</span><span class="sxs-lookup"><span data-stu-id="d263c-415">Example .nuspec files</span></span>

<span data-ttu-id="d263c-416">**Простой файл `.nuspec`, в котором не задаются зависимости или файлы**</span><span class="sxs-lookup"><span data-stu-id="d263c-416">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="d263c-417">**Файл `.nuspec` с зависимостями**</span><span class="sxs-lookup"><span data-stu-id="d263c-417">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="d263c-418">**Файл `.nuspec` с файлами**</span><span class="sxs-lookup"><span data-stu-id="d263c-418">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="d263c-419">**Файл `.nuspec` со сборками платформы**</span><span class="sxs-lookup"><span data-stu-id="d263c-419">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="d263c-420">В этом примере для целевых объектов проекта устанавливаются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="d263c-420">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="d263c-421">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="d263c-421">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="d263c-422">Клиентский профиль .NET4 -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="d263c-422">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="d263c-423">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="d263c-423">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="d263c-424">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="d263c-424">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="d263c-425">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="d263c-425">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
