---
title: "Пакеты NuGet в шаблонах Visual Studio | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/03/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Инструкции по включению пакетов NuGet в состав шаблонов проектов и элементов Visual Studio."
keywords: "NuGet в Visual Studio, шаблоны проектов Visual Studio, шаблоны элементов Visual Studio, пакеты в шаблонах проектов, пакеты в шаблонах элементов"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 65b914e1fa59c28615f195b470880a12bf80efbb
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2018
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="872fc-104">Пакеты в шаблонах Visual Studio</span><span class="sxs-lookup"><span data-stu-id="872fc-104">Packages in Visual Studio templates</span></span>

<span data-ttu-id="872fc-105">Шаблонам проектов и элементов Visual Studio часто требуется обеспечить установку определенных пакетов при создании проекта или элемента.</span><span class="sxs-lookup"><span data-stu-id="872fc-105">Visual Studio project and item templates often need to ensure that certain packages are installed when a project or item is created.</span></span> <span data-ttu-id="872fc-106">Например, шаблон ASP.NET MVC 3 устанавливает jQuery, Modernizr и другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="872fc-106">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="872fc-107">Для этого авторы шаблонов могут настроить NuGet для установки необходимых пакетов, а не отдельных библиотек.</span><span class="sxs-lookup"><span data-stu-id="872fc-107">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="872fc-108">Позднее разработчики могут в любое время легко обновить эти пакеты.</span><span class="sxs-lookup"><span data-stu-id="872fc-108">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="872fc-109">Дополнительные сведения о создании шаблонов см. в разделе [Практическое руководство. Создание шаблонов проектов](/visualstudio/ide/how-to-create-project-templates) и [Создание настраиваемых шаблонов проектов и элементов](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span><span class="sxs-lookup"><span data-stu-id="872fc-109">To learn more about authoring templates themselves, refer to [How to: Create Project Templates](/visualstudio/ide/how-to-create-project-templates) or [Creating Custom Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span></span>

<span data-ttu-id="872fc-110">Оставшаяся часть этого раздела посвящена конкретным шагам, которые следует предпринять при создании шаблона, чтобы правильно включить пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="872fc-110">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="872fc-111">Добавление пакетов в шаблон</span><span class="sxs-lookup"><span data-stu-id="872fc-111">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="872fc-112">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="872fc-112">Best practices</span></span>](#best-practices)

<span data-ttu-id="872fc-113">Например, ознакомьтесь с [примером NuGetInVsTemplates](https://bitbucket.org/marcind/nugetinvstemplates).</span><span class="sxs-lookup"><span data-stu-id="872fc-113">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>

## <a name="adding-packages-to-a-template"></a><span data-ttu-id="872fc-114">Добавление пакетов в шаблон</span><span class="sxs-lookup"><span data-stu-id="872fc-114">Adding packages to a template</span></span>

<span data-ttu-id="872fc-115">При создании шаблона вызывается [мастер шаблонов](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) для загрузки списка устанавливаемых пакетов, а также сведений об их расположении.</span><span class="sxs-lookup"><span data-stu-id="872fc-115">When a template is instantiated, a [template wizard](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="872fc-116">Пакеты могут быть внедрены в VSIX, в шаблон или расположены на локальном жестком диске, в случае чего вы используете раздел реестра, чтобы сослаться на путь к файлу.</span><span class="sxs-lookup"><span data-stu-id="872fc-116">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="872fc-117">Сведения об этих расположениях приведены ниже в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="872fc-117">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="872fc-118">Предустановленные пакеты используют для работы [мастеры шаблонов](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span><span class="sxs-lookup"><span data-stu-id="872fc-118">Preinstalled packages work using [template wizards](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span></span> <span data-ttu-id="872fc-119">Специальный мастер вызывается при создании экземпляра шаблона.</span><span class="sxs-lookup"><span data-stu-id="872fc-119">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="872fc-120">Он загружает список пакетов, которые нужно установить, и передает эти сведения соответствующим API NuGet.</span><span class="sxs-lookup"><span data-stu-id="872fc-120">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="872fc-121">Шаги по включению пакетов в шаблон:</span><span class="sxs-lookup"><span data-stu-id="872fc-121">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="872fc-122">Добавьте в свой файл `vstemplate` ссылку на мастер шаблонов NuGet, добавив элемент [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates):</span><span class="sxs-lookup"><span data-stu-id="872fc-122">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="872fc-123">`NuGet.VisualStudio.Interop.dll` — это сборка, содержащая только класс`TemplateWizard`, который представляет собой простую программу-оболочку, вызывающую фактическую реализацию в `NuGet.VisualStudio.dll`.</span><span class="sxs-lookup"><span data-stu-id="872fc-123">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="872fc-124">Версия сборки не изменится, поэтому эти шаблоны проектов и элементов продолжат работать с новыми версиями NuGet.</span><span class="sxs-lookup"><span data-stu-id="872fc-124">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="872fc-125">Добавьте список устанавливаемых пакетов в проект:</span><span class="sxs-lookup"><span data-stu-id="872fc-125">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="872fc-126">*(NuGet 2.2.1+)*  Мастер поддерживает несколько элементов `<package>` для поддержки нескольких источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="872fc-126">*(NuGet 2.2.1+)* The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="872fc-127">Требуются оба атрибута `id` и `version`, то есть эта конкретная версия пакета будет установлена, даже если доступна более новая версия.</span><span class="sxs-lookup"><span data-stu-id="872fc-127">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="872fc-128">Это не позволяет обновлениям пакета нарушить работу шаблона и предоставляет возможность обновить пакет разработчику, использующему шаблон.</span><span class="sxs-lookup"><span data-stu-id="872fc-128">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>

1. <span data-ttu-id="872fc-129">Укажите репозиторий, где NuGet может найти пакеты, как описано в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="872fc-129">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="872fc-130">Репозиторий пакетов VSIX</span><span class="sxs-lookup"><span data-stu-id="872fc-130">VSIX package repository</span></span>

<span data-ttu-id="872fc-131">Для развертывания шаблонов проектов и элементов Visual Studio рекомендуется использовать [расширение VSIX](/visualstudio/extensibility/shipping-visual-studio-extensions), так как оно дает возможность упаковать вместе несколько шаблонов проектов или элементов и позволяет разработчикам легко находить ваши шаблоны с помощью диспетчера расширений VS или коллекции Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="872fc-131">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](/visualstudio/extensibility/shipping-visual-studio-extensions) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="872fc-132">Обновления для этого расширения также легко развернуть с помощью [механизма автоматического обновления в диспетчере расширений Visual Studio](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span><span class="sxs-lookup"><span data-stu-id="872fc-132">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span></span>

<span data-ttu-id="872fc-133">Сам VSIX может служить источником необходимых шаблону пакетов:</span><span class="sxs-lookup"><span data-stu-id="872fc-133">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="872fc-134">Измените элемент `<packages>` в файле `.vstemplate` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="872fc-134">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="872fc-135">Атрибут `repository` задает тип репозитория как `extension`, а `repositoryId` является уникальным идентификатором самого VSIX (это значение атрибута `ID` в файле `vsixmanifest` расширения, см. [Справочник по схеме 2.0 расширения VSIX](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span><span class="sxs-lookup"><span data-stu-id="872fc-135">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the `ID` attribute in the extension’s `vsixmanifest` file, see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span></span>

1. <span data-ttu-id="872fc-136">Поместите файлы `nupkg` в папку `Packages` внутри VSIX.</span><span class="sxs-lookup"><span data-stu-id="872fc-136">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>

1. <span data-ttu-id="872fc-137">Добавьте нужные файлы пакетов как `<Asset>` в файл `vsixmanifest` (см. [Справочник по схеме 2.0 расширения VSIX](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span><span class="sxs-lookup"><span data-stu-id="872fc-137">Add the necessary package files as `<Asset>` in your `vsixmanifest` file (see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. <span data-ttu-id="872fc-138">Обратите внимание, что можно доставить пакеты в тот же VSIX, что и шаблоны проекта, либо поместить их в отдельный VSIX, если это лучше подходит для вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="872fc-138">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="872fc-139">Однако не следует ссылаться на любой VSIX, которым вы не управляете, так как изменения в этом расширении могут нарушить работу шаблона.</span><span class="sxs-lookup"><span data-stu-id="872fc-139">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>

### <a name="template-package-repository"></a><span data-ttu-id="872fc-140">Репозиторий пакетов шаблонов</span><span class="sxs-lookup"><span data-stu-id="872fc-140">Template package repository</span></span>

<span data-ttu-id="872fc-141">Если вы распространяете только один шаблон проектов или элементов и вам не нужно паковать вместе несколько шаблонов, можно использовать более простой, хотя и ограниченный, подход, включающий пакеты непосредственно в ZIP-файл шаблона проектов или элементов:</span><span class="sxs-lookup"><span data-stu-id="872fc-141">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="872fc-142">Измените элемент `<packages>` в файле `.vstemplate` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="872fc-142">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="872fc-143">Атрибут `repository` имеет значение `template`, а атрибут `repositoryId` не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="872fc-143">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="872fc-144">Поместите пакеты в корневую папку в ZIP-файле шаблона проектов или элементов.</span><span class="sxs-lookup"><span data-stu-id="872fc-144">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="872fc-145">Обратите внимание, что применение такого подхода для VSIX, содержащего несколько шаблонов, приводит к ненужному раздуванию, когда один или несколько пакетов являются общими для шаблонов.</span><span class="sxs-lookup"><span data-stu-id="872fc-145">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="872fc-146">В таких случаях используйте [VSIX в качестве репозитория](#vsix-package-repository), как описано в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="872fc-146">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>

### <a name="registry-specified-folder-path"></a><span data-ttu-id="872fc-147">Путь к папке, указанный для реестра</span><span class="sxs-lookup"><span data-stu-id="872fc-147">Registry-specified folder path</span></span>

<span data-ttu-id="872fc-148">Пакеты SDK, устанавливаемые с помощью MSI, могут устанавливать пакеты NuGet непосредственно на компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="872fc-148">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="872fc-149">В результате их не требуется извлекать при использовании шаблона проектов или элементов, они доступны сразу же.</span><span class="sxs-lookup"><span data-stu-id="872fc-149">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="872fc-150">Этот подход используется в шаблонах ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="872fc-150">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="872fc-151">Позвольте MSI установить пакеты на компьютере.</span><span class="sxs-lookup"><span data-stu-id="872fc-151">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="872fc-152">Вы можете установить файлы `.nupkg` отдельно либо вместе с расширенным содержимым, которое позволяет пропустить один из шагов при использовании шаблона.</span><span class="sxs-lookup"><span data-stu-id="872fc-152">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="872fc-153">В этом случае следуйте стандартной структуре папок NuGet, когда файлы `.nupkg` находятся в корневой папке, а каждый пакет имеет вложенную папку, имя которой состоит из пары идентификатора и версии.</span><span class="sxs-lookup"><span data-stu-id="872fc-153">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="872fc-154">Запишите раздел реестра для определения расположения пакета:</span><span class="sxs-lookup"><span data-stu-id="872fc-154">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="872fc-155">Расположение ключа: либо на уровне компьютера `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository`, либо, если шаблоны и пакеты установлены для конкретного пользователя, можно также использовать `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`.</span><span class="sxs-lookup"><span data-stu-id="872fc-155">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="872fc-156">Имя ключа: используйте уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="872fc-156">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="872fc-157">Например, шаблоны ASP.NET MVC 4 для Visual Studio 2012 используют `AspNetMvc4VS11`.</span><span class="sxs-lookup"><span data-stu-id="872fc-157">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="872fc-158">Значения: полный путь к папке пакетов.</span><span class="sxs-lookup"><span data-stu-id="872fc-158">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="872fc-159">Добавьте в элемент `<packages>` в файле `.vstemplate` атрибут `repository="registry"` и укажите имя раздела реестра в атрибуте `keyName`.</span><span class="sxs-lookup"><span data-stu-id="872fc-159">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="872fc-160">Если вы заранее распаковали пакеты, используйте атрибут `isPreunzipped="true"`.</span><span class="sxs-lookup"><span data-stu-id="872fc-160">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="872fc-161">*(NuGet 3.2+)* Если вы хотите принудительно выполнить сборку времени разработки в конце установки пакета, добавьте атрибут `forceDesignTimeBuild="true"`.</span><span class="sxs-lookup"><span data-stu-id="872fc-161">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="872fc-162">Для оптимизации добавьте `skipAssemblyReferences="true"`, так как шаблон уже включает в себя необходимые ссылки.</span><span class="sxs-lookup"><span data-stu-id="872fc-162">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="872fc-163">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="872fc-163">Best Practices</span></span>

1. <span data-ttu-id="872fc-164">Объявите о зависимости от NuGet VSIX, добавив ссылку на него в манифесте VSIX:</span><span class="sxs-lookup"><span data-stu-id="872fc-164">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="872fc-165">Настройте сохранение шаблонов проектов и элементов при их создании, включив [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) в файл `.vstemplate`.</span><span class="sxs-lookup"><span data-stu-id="872fc-165">Require project/item templates to be saved on creation by including [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="872fc-166">Шаблоны не содержат файл `packages.config`, а также ссылки или содержимое, которое следует добавить при установке пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="872fc-166">Templates do not include a `packages.config` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
