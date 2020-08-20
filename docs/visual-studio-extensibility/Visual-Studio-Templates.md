---
title: Пакеты NuGet в шаблонах Visual Studio
description: Инструкции по включению пакетов NuGet в состав шаблонов проектов и элементов Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/03/2018
ms.topic: conceptual
ms.openlocfilehash: 2dfbd793eee05169f051d9c8943bc065945b92da
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622646"
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="dc889-103">Пакеты в шаблонах Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dc889-103">Packages in Visual Studio templates</span></span>

<span data-ttu-id="dc889-104">Шаблонам проектов и элементов Visual Studio часто требуется обеспечить установку определенных пакетов при создании проекта или элемента.</span><span class="sxs-lookup"><span data-stu-id="dc889-104">Visual Studio project and item templates often need to ensure that certain packages are installed when a project or item is created.</span></span> <span data-ttu-id="dc889-105">Например, шаблон ASP.NET MVC 3 устанавливает jQuery, Modernizr и другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="dc889-105">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="dc889-106">Для этого авторы шаблонов могут настроить NuGet для установки необходимых пакетов, а не отдельных библиотек.</span><span class="sxs-lookup"><span data-stu-id="dc889-106">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="dc889-107">Позднее разработчики могут в любое время легко обновить эти пакеты.</span><span class="sxs-lookup"><span data-stu-id="dc889-107">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="dc889-108">Дополнительные сведения о создании шаблонов см. в разделе [Практическое руководство. Создание шаблонов проектов](/visualstudio/ide/how-to-create-project-templates) и [Создание настраиваемых шаблонов проектов и элементов](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span><span class="sxs-lookup"><span data-stu-id="dc889-108">To learn more about authoring templates themselves, refer to [How to: Create Project Templates](/visualstudio/ide/how-to-create-project-templates) or [Creating Custom Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span></span>

<span data-ttu-id="dc889-109">Оставшаяся часть этого раздела посвящена конкретным шагам, которые следует предпринять при создании шаблона, чтобы правильно включить пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="dc889-109">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="dc889-110">Добавление пакетов в шаблон</span><span class="sxs-lookup"><span data-stu-id="dc889-110">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="dc889-111">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="dc889-111">Best practices</span></span>](#best-practices)

<span data-ttu-id="dc889-112">Например, ознакомьтесь с [примером NuGetInVsTemplates](https://bitbucket.org/marcind/nugetinvstemplates).</span><span class="sxs-lookup"><span data-stu-id="dc889-112">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>

## <a name="adding-packages-to-a-template"></a><span data-ttu-id="dc889-113">Добавление пакетов в шаблон</span><span class="sxs-lookup"><span data-stu-id="dc889-113">Adding packages to a template</span></span>

<span data-ttu-id="dc889-114">При создании шаблона вызывается [мастер шаблонов](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) для загрузки списка устанавливаемых пакетов, а также сведений об их расположении.</span><span class="sxs-lookup"><span data-stu-id="dc889-114">When a template is instantiated, a [template wizard](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="dc889-115">Пакеты могут быть внедрены в VSIX, в шаблон или расположены на локальном жестком диске, в случае чего вы используете раздел реестра, чтобы сослаться на путь к файлу.</span><span class="sxs-lookup"><span data-stu-id="dc889-115">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="dc889-116">Сведения об этих расположениях приведены ниже в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="dc889-116">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="dc889-117">Предустановленные пакеты используют для работы [мастеры шаблонов](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span><span class="sxs-lookup"><span data-stu-id="dc889-117">Preinstalled packages work using [template wizards](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span></span> <span data-ttu-id="dc889-118">Специальный мастер вызывается при создании экземпляра шаблона.</span><span class="sxs-lookup"><span data-stu-id="dc889-118">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="dc889-119">Он загружает список пакетов, которые нужно установить, и передает эти сведения соответствующим API NuGet.</span><span class="sxs-lookup"><span data-stu-id="dc889-119">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="dc889-120">Шаги по включению пакетов в шаблон:</span><span class="sxs-lookup"><span data-stu-id="dc889-120">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="dc889-121">Добавьте в свой файл `vstemplate` ссылку на мастер шаблонов NuGet, добавив элемент [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates):</span><span class="sxs-lookup"><span data-stu-id="dc889-121">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="dc889-122">`NuGet.VisualStudio.Interop.dll` — это сборка, содержащая только класс`TemplateWizard`, который представляет собой простую программу-оболочку, вызывающую фактическую реализацию в `NuGet.VisualStudio.dll`.</span><span class="sxs-lookup"><span data-stu-id="dc889-122">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="dc889-123">Версия сборки не изменится, поэтому эти шаблоны проектов и элементов продолжат работать с новыми версиями NuGet.</span><span class="sxs-lookup"><span data-stu-id="dc889-123">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="dc889-124">Добавьте список устанавливаемых пакетов в проект:</span><span class="sxs-lookup"><span data-stu-id="dc889-124">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="dc889-125">Мастер поддерживает несколько элементов `<package>`, что обеспечивает поддержку нескольких источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="dc889-125">The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="dc889-126">Требуются оба атрибута `id` и `version`, то есть эта конкретная версия пакета будет установлена, даже если доступна более новая версия.</span><span class="sxs-lookup"><span data-stu-id="dc889-126">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="dc889-127">Это не позволяет обновлениям пакета нарушить работу шаблона и предоставляет возможность обновить пакет разработчику, использующему шаблон.</span><span class="sxs-lookup"><span data-stu-id="dc889-127">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>

1. <span data-ttu-id="dc889-128">Укажите репозиторий, где NuGet может найти пакеты, как описано в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="dc889-128">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="dc889-129">Репозиторий пакетов VSIX</span><span class="sxs-lookup"><span data-stu-id="dc889-129">VSIX package repository</span></span>

<span data-ttu-id="dc889-130">Для развертывания шаблонов проектов и элементов Visual Studio рекомендуется использовать [расширение VSIX](/visualstudio/extensibility/shipping-visual-studio-extensions), так как оно дает возможность упаковать вместе несколько шаблонов проектов или элементов и позволяет разработчикам легко находить ваши шаблоны с помощью диспетчера расширений VS или коллекции Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dc889-130">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](/visualstudio/extensibility/shipping-visual-studio-extensions) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="dc889-131">Обновления для этого расширения также легко развернуть с помощью [механизма автоматического обновления в диспетчере расширений Visual Studio](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span><span class="sxs-lookup"><span data-stu-id="dc889-131">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span></span>

<span data-ttu-id="dc889-132">Сам VSIX может служить источником необходимых шаблону пакетов:</span><span class="sxs-lookup"><span data-stu-id="dc889-132">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="dc889-133">Измените элемент `<packages>` в файле `.vstemplate` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="dc889-133">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="dc889-134">Атрибут `repository` задает тип репозитория как `extension`, а `repositoryId` является уникальным идентификатором самого VSIX (это значение атрибута `ID` в файле `vsixmanifest` расширения, см. [Справочник по схеме 2.0 расширения VSIX](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span><span class="sxs-lookup"><span data-stu-id="dc889-134">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the `ID` attribute in the extension’s `vsixmanifest` file, see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span></span>

1. <span data-ttu-id="dc889-135">Поместите файлы `nupkg` в папку `Packages` внутри VSIX.</span><span class="sxs-lookup"><span data-stu-id="dc889-135">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>

1. <span data-ttu-id="dc889-136">Добавьте нужные файлы пакетов как `<Asset>` в файл `vsixmanifest` (см. [Справочник по схеме 2.0 расширения VSIX](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span><span class="sxs-lookup"><span data-stu-id="dc889-136">Add the necessary package files as `<Asset>` in your `vsixmanifest` file (see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. <span data-ttu-id="dc889-137">Обратите внимание, что можно доставить пакеты в тот же VSIX, что и шаблоны проекта, либо поместить их в отдельный VSIX, если это лучше подходит для вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="dc889-137">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="dc889-138">Однако не следует ссылаться на любой VSIX, которым вы не управляете, так как изменения в этом расширении могут нарушить работу шаблона.</span><span class="sxs-lookup"><span data-stu-id="dc889-138">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>

### <a name="template-package-repository"></a><span data-ttu-id="dc889-139">Репозиторий пакетов шаблонов</span><span class="sxs-lookup"><span data-stu-id="dc889-139">Template package repository</span></span>

<span data-ttu-id="dc889-140">Если вы распространяете только один шаблон проектов или элементов и вам не нужно паковать вместе несколько шаблонов, можно использовать более простой, хотя и ограниченный, подход, включающий пакеты непосредственно в ZIP-файл шаблона проектов или элементов:</span><span class="sxs-lookup"><span data-stu-id="dc889-140">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="dc889-141">Измените элемент `<packages>` в файле `.vstemplate` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="dc889-141">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="dc889-142">Атрибут `repository` имеет значение `template`, а атрибут `repositoryId` не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="dc889-142">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="dc889-143">Поместите пакеты в корневую папку в ZIP-файле шаблона проектов или элементов.</span><span class="sxs-lookup"><span data-stu-id="dc889-143">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="dc889-144">Обратите внимание, что применение такого подхода для VSIX, содержащего несколько шаблонов, приводит к ненужному раздуванию, когда один или несколько пакетов являются общими для шаблонов.</span><span class="sxs-lookup"><span data-stu-id="dc889-144">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="dc889-145">В таких случаях используйте [VSIX в качестве репозитория](#vsix-package-repository), как описано в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="dc889-145">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>

### <a name="registry-specified-folder-path"></a><span data-ttu-id="dc889-146">Путь к папке, указанный для реестра</span><span class="sxs-lookup"><span data-stu-id="dc889-146">Registry-specified folder path</span></span>

<span data-ttu-id="dc889-147">Пакеты SDK, устанавливаемые с помощью MSI, могут устанавливать пакеты NuGet непосредственно на компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="dc889-147">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="dc889-148">В результате их не требуется извлекать при использовании шаблона проектов или элементов, они доступны сразу же.</span><span class="sxs-lookup"><span data-stu-id="dc889-148">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="dc889-149">Этот подход используется в шаблонах ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="dc889-149">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="dc889-150">Позвольте MSI установить пакеты на компьютере.</span><span class="sxs-lookup"><span data-stu-id="dc889-150">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="dc889-151">Вы можете установить файлы `.nupkg` отдельно либо вместе с расширенным содержимым, которое позволяет пропустить один из шагов при использовании шаблона.</span><span class="sxs-lookup"><span data-stu-id="dc889-151">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="dc889-152">В этом случае следуйте стандартной структуре папок NuGet, когда файлы `.nupkg` находятся в корневой папке, а каждый пакет имеет вложенную папку, имя которой состоит из пары идентификатора и версии.</span><span class="sxs-lookup"><span data-stu-id="dc889-152">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="dc889-153">Запишите раздел реестра для определения расположения пакета:</span><span class="sxs-lookup"><span data-stu-id="dc889-153">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="dc889-154">Расположение ключа: либо на уровне компьютера `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository`, либо, если шаблоны и пакеты установлены для конкретного пользователя, можно также использовать `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`.</span><span class="sxs-lookup"><span data-stu-id="dc889-154">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="dc889-155">Имя ключа: используйте уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="dc889-155">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="dc889-156">Например, шаблоны ASP.NET MVC 4 для Visual Studio 2012 используют `AspNetMvc4VS11`.</span><span class="sxs-lookup"><span data-stu-id="dc889-156">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="dc889-157">Значения: полный путь к папке пакетов.</span><span class="sxs-lookup"><span data-stu-id="dc889-157">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="dc889-158">Добавьте в элемент `<packages>` в файле `.vstemplate` атрибут `repository="registry"` и укажите имя раздела реестра в атрибуте `keyName`.</span><span class="sxs-lookup"><span data-stu-id="dc889-158">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="dc889-159">Если вы заранее распаковали пакеты, используйте атрибут `isPreunzipped="true"`.</span><span class="sxs-lookup"><span data-stu-id="dc889-159">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="dc889-160">*(NuGet 3.2+)* Если вы хотите принудительно выполнить сборку времени разработки в конце установки пакета, добавьте атрибут `forceDesignTimeBuild="true"`.</span><span class="sxs-lookup"><span data-stu-id="dc889-160">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="dc889-161">Для оптимизации добавьте `skipAssemblyReferences="true"`, так как шаблон уже включает в себя необходимые ссылки.</span><span class="sxs-lookup"><span data-stu-id="dc889-161">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="dc889-162">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="dc889-162">Best Practices</span></span>

1. <span data-ttu-id="dc889-163">Объявите о зависимости от NuGet VSIX, добавив ссылку на него в манифесте VSIX:</span><span class="sxs-lookup"><span data-stu-id="dc889-163">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="dc889-164">Настройте сохранение шаблонов проектов и элементов при их создании, включив [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) в файл `.vstemplate`.</span><span class="sxs-lookup"><span data-stu-id="dc889-164">Require project/item templates to be saved on creation by including [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="dc889-165">Шаблоны не содержат файл `packages.config`, а также ссылки или содержимое, которое следует добавить при установке пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="dc889-165">Templates do not include a `packages.config` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
