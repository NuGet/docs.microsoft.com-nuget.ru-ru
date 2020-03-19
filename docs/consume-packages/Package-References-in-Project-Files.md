---
title: Формат NuGet PackageReference (ссылки на пакеты в файлах проектов)
description: Подробные сведения о формате NuGet PackageReference в файлах проектов, который поддерживается в NuGet 4.0 и более поздних версиях, в VS2017 и в .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428507"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="aff6c-103">Ссылки на пакеты (PackageReference) в файлах проектов</span><span class="sxs-lookup"><span data-stu-id="aff6c-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="aff6c-104">Ссылки на пакеты в узле `PackageReference` позволяют напрямую управлять зависимостями NuGet в файлах проекта (вместо использования отдельного файла `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="aff6c-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="aff6c-105">Использование PackageReference не влияет на другие аспекты NuGet. Например, параметры в файлах `NuGet.config` (включая источники пакетов) по-прежнему применяются, как описано в разделе [Распространенные конфигурации NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="aff6c-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="aff6c-106">PackageReference также позволяет использовать условия MSBuild для выбора ссылок на пакеты в соответствии с целевой платформой и другими признаками.</span><span class="sxs-lookup"><span data-stu-id="aff6c-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="aff6c-107">Он также обеспечивает детальный контроль над зависимостями и потоком содержимого.</span><span class="sxs-lookup"><span data-stu-id="aff6c-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="aff6c-108">(Дополнительные сведения см. в разделе [Объекты pack и restore NuGet в качестве целевых объектов MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="aff6c-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="aff6c-109">Поддержка типов проектов</span><span class="sxs-lookup"><span data-stu-id="aff6c-109">Project type support</span></span>

<span data-ttu-id="aff6c-110">По умолчанию PackageReference используется для проектов .NET Core, проектов .NET Standard и проектов универсальной платформы Windows, предназначенных для сборки 15063 системы Windows 10 (Creators Update), за исключением проектов C++ UWP.</span><span class="sxs-lookup"><span data-stu-id="aff6c-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="aff6c-111">Проекты .NET Framework поддерживают PackageReference, но сейчас по умолчанию используют `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="aff6c-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="aff6c-112">Чтобы использовать PackageReference, [перенесите](../consume-packages/migrate-packages-config-to-package-reference.md) зависимости из `packages.config` в файл проекта, а затем удалите packages.config.</span><span class="sxs-lookup"><span data-stu-id="aff6c-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="aff6c-113">Приложения ASP.NET, предназначенные для полной версии .NET Framework, включают только [ограниченную поддержку](https://github.com/NuGet/Home/issues/5877) для PackageReference.</span><span class="sxs-lookup"><span data-stu-id="aff6c-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="aff6c-114">Типы проектов C++и JavaScript не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="aff6c-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="aff6c-115">Добавление PackageReference</span><span class="sxs-lookup"><span data-stu-id="aff6c-115">Adding a PackageReference</span></span>

<span data-ttu-id="aff6c-116">Добавьте зависимость в файл проекта, используя следующий синтаксис:</span><span class="sxs-lookup"><span data-stu-id="aff6c-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="aff6c-117">Управление версией зависимости</span><span class="sxs-lookup"><span data-stu-id="aff6c-117">Controlling dependency version</span></span>

<span data-ttu-id="aff6c-118">При указании версии пакета действует то же соглашение, что и при использовании файла `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="aff6c-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="aff6c-119">В приведенном выше примере значение 3.6.0 означает версию 3.6.0 или любую более позднюю версию, причем предпочтение отдается самой ранней версии, как описано в разделе [Управление версиями пакета](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="aff6c-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="aff6c-120">Использование PackageReference для проекта без объектов PackageReference</span><span class="sxs-lookup"><span data-stu-id="aff6c-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="aff6c-121">Дополнительно: Eсли в проекте нет установленных пакетов (нет объектов PackageReference в файле, а также файла packages.config), но вы хотите восстанавливать проект в стиле PackageReference, можно задать для свойства RestoreProjectStyle проекта значение PackageReference в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="aff6c-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="aff6c-122">Это может быть удобно при ссылке на проекты в стиле PackageReference (существующие CSPROJ- или SDK-проекты).</span><span class="sxs-lookup"><span data-stu-id="aff6c-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="aff6c-123">Это позволит вашему проекту транзитивно ссылаться на пакеты, на которые ссылаются эти проекты.</span><span class="sxs-lookup"><span data-stu-id="aff6c-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="aff6c-124">PackageReference и источники</span><span class="sxs-lookup"><span data-stu-id="aff6c-124">PackageReference and sources</span></span>

<span data-ttu-id="aff6c-125">В проектах PackageReference временные версии зависимостей разрешаются во время восстановления.</span><span class="sxs-lookup"><span data-stu-id="aff6c-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="aff6c-126">Поэтому в них все источники должны быть доступны для всех операций восстановления.</span><span class="sxs-lookup"><span data-stu-id="aff6c-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="aff6c-127">Гибкие версии</span><span class="sxs-lookup"><span data-stu-id="aff6c-127">Floating Versions</span></span>

<span data-ttu-id="aff6c-128">[Гибкие версии](../concepts/dependency-resolution.md#floating-versions) можно использовать с `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="aff6c-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="aff6c-129">Управление ресурсами зависимости</span><span class="sxs-lookup"><span data-stu-id="aff6c-129">Controlling dependency assets</span></span>

<span data-ttu-id="aff6c-130">Зависимость может применяться исключительно для удобства разработки. В этом случае доступ к ней не нужно предоставлять проектам, использующим пакет.</span><span class="sxs-lookup"><span data-stu-id="aff6c-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="aff6c-131">Для управления таким поведением могут служить метаданные `PrivateAssets`.</span><span class="sxs-lookup"><span data-stu-id="aff6c-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="aff6c-132">Ниже перечислены теги метаданных, управляющие ресурсами зависимостей.</span><span class="sxs-lookup"><span data-stu-id="aff6c-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="aff6c-133">Тег</span><span class="sxs-lookup"><span data-stu-id="aff6c-133">Tag</span></span> | <span data-ttu-id="aff6c-134">Описание</span><span class="sxs-lookup"><span data-stu-id="aff6c-134">Description</span></span> | <span data-ttu-id="aff6c-135">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="aff6c-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="aff6c-136">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="aff6c-136">IncludeAssets</span></span> | <span data-ttu-id="aff6c-137">Эти ресурсы будут использоваться.</span><span class="sxs-lookup"><span data-stu-id="aff6c-137">These assets will be consumed</span></span> | <span data-ttu-id="aff6c-138">все</span><span class="sxs-lookup"><span data-stu-id="aff6c-138">all</span></span> |
| <span data-ttu-id="aff6c-139">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="aff6c-139">ExcludeAssets</span></span> | <span data-ttu-id="aff6c-140">Эти ресурсы не будут использоваться.</span><span class="sxs-lookup"><span data-stu-id="aff6c-140">These assets will not be consumed</span></span> | <span data-ttu-id="aff6c-141">Нет</span><span class="sxs-lookup"><span data-stu-id="aff6c-141">none</span></span> |
| <span data-ttu-id="aff6c-142">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="aff6c-142">PrivateAssets</span></span> | <span data-ttu-id="aff6c-143">Эти ресурсы будут использоваться, но не будут передаваться в родительский проект.</span><span class="sxs-lookup"><span data-stu-id="aff6c-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="aff6c-144">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="aff6c-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="aff6c-145">Ниже приводятся допустимые значения этих тегов. Несколько значений должны разделяться точкой с запятой. Это не относится к значениям `all` и `none`, которые должны использоваться отдельно.</span><span class="sxs-lookup"><span data-stu-id="aff6c-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="aff6c-146">Значение</span><span class="sxs-lookup"><span data-stu-id="aff6c-146">Value</span></span> | <span data-ttu-id="aff6c-147">Описание</span><span class="sxs-lookup"><span data-stu-id="aff6c-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="aff6c-148">compile</span><span class="sxs-lookup"><span data-stu-id="aff6c-148">compile</span></span> | <span data-ttu-id="aff6c-149">Содержимое папки `lib`; управляет возможностью компиляции проекта с использованием сборок в этой папке</span><span class="sxs-lookup"><span data-stu-id="aff6c-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="aff6c-150">исполняющая среда</span><span class="sxs-lookup"><span data-stu-id="aff6c-150">runtime</span></span> | <span data-ttu-id="aff6c-151">Содержимое папки `lib` и `runtimes`; управляет возможностью копирования этих сборок в выходной каталог сборки</span><span class="sxs-lookup"><span data-stu-id="aff6c-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="aff6c-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="aff6c-152">contentFiles</span></span> | <span data-ttu-id="aff6c-153">Содержимое папки `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="aff6c-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="aff6c-154">выполнить сборку</span><span class="sxs-lookup"><span data-stu-id="aff6c-154">build</span></span> | <span data-ttu-id="aff6c-155">`.props` и `.targets` в папке `build`</span><span class="sxs-lookup"><span data-stu-id="aff6c-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="aff6c-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="aff6c-156">buildMultitargeting</span></span> | <span data-ttu-id="aff6c-157">Файлы `.props` и `.targets` *(4.0)* в папке `buildMultitargeting` для кроссплатформенного определения.</span><span class="sxs-lookup"><span data-stu-id="aff6c-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="aff6c-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="aff6c-158">buildTransitive</span></span> | <span data-ttu-id="aff6c-159">Файлы `.props` и `.targets` *(5.0+)* в папке `buildTransitive` для ресурсов, которые можно транзитивно передавать в любой соответствующий проект.</span><span class="sxs-lookup"><span data-stu-id="aff6c-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="aff6c-160">См. об [этой функции](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior).</span><span class="sxs-lookup"><span data-stu-id="aff6c-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="aff6c-161">analyzers</span><span class="sxs-lookup"><span data-stu-id="aff6c-161">analyzers</span></span> | <span data-ttu-id="aff6c-162">Анализаторы .NET</span><span class="sxs-lookup"><span data-stu-id="aff6c-162">.NET analyzers</span></span> |
| <span data-ttu-id="aff6c-163">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="aff6c-163">native</span></span> | <span data-ttu-id="aff6c-164">Содержимое папки `native`</span><span class="sxs-lookup"><span data-stu-id="aff6c-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="aff6c-165">Нет</span><span class="sxs-lookup"><span data-stu-id="aff6c-165">none</span></span> | <span data-ttu-id="aff6c-166">Никакие из перечисленных выше ресурсов не используются.</span><span class="sxs-lookup"><span data-stu-id="aff6c-166">None of the above are used.</span></span> |
| <span data-ttu-id="aff6c-167">все</span><span class="sxs-lookup"><span data-stu-id="aff6c-167">all</span></span> | <span data-ttu-id="aff6c-168">Используются все перечисленные выше ресурсы (кроме `none`).</span><span class="sxs-lookup"><span data-stu-id="aff6c-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="aff6c-169">В приведенном ниже примере проектом используются все ресурсы, кроме файлов содержимого из пакета, и в родительский проект передаются все ресурсы, кроме файлов содержимого и анализаторов.</span><span class="sxs-lookup"><span data-stu-id="aff6c-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="aff6c-170">Обратите внимание: так как папка `build` не включена в `PrivateAssets`, цели и свойства *будут* передаваться в родительский проект.</span><span class="sxs-lookup"><span data-stu-id="aff6c-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="aff6c-171">Предположим, что приведенная выше ссылка используется в проекте, в рамках которого выполняется сборка пакета NuGet с именем AppLogger.</span><span class="sxs-lookup"><span data-stu-id="aff6c-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="aff6c-172">Пакет AppLogger может использовать цели и свойства из `Contoso.Utility.UsefulStuff`, так же как и проекты, использующие AppLogger.</span><span class="sxs-lookup"><span data-stu-id="aff6c-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="aff6c-173">Когда для `developmentDependency` в файле `.nuspec` задано значение `true`, это указывает на то, что пакет помечен как зависимость только для разработки, что позволяет запретить его включение в качестве зависимости в другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="aff6c-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="aff6c-174">При использовании PackageReference *(NuGet 4.8+)* этот флажок также указывает на исключение ресурсов времени компиляции из компиляции.</span><span class="sxs-lookup"><span data-stu-id="aff6c-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="aff6c-175">Дополнительные сведения см. в статье [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) (Поддержка DevelopmentDependency для PackageReference).</span><span class="sxs-lookup"><span data-stu-id="aff6c-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="aff6c-176">Добавление условия PackageReference</span><span class="sxs-lookup"><span data-stu-id="aff6c-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="aff6c-177">С помощью условий можно управлять тем, когда следует включать пакет. В условиях можно использовать любые переменные MSBuild или переменные, определенные в файлах целей или свойств.</span><span class="sxs-lookup"><span data-stu-id="aff6c-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="aff6c-178">Однако в настоящее время поддерживается только переменная `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="aff6c-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="aff6c-179">Например, предположим, что целевыми платформами являются `netstandard1.4` и `net452`, но зависимость применима только для `net452`.</span><span class="sxs-lookup"><span data-stu-id="aff6c-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="aff6c-180">В этом случае в проект `netstandard1.4`, который использует пакет, не следует добавлять эту ненужную зависимость.</span><span class="sxs-lookup"><span data-stu-id="aff6c-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="aff6c-181">В этом случае в узле `PackageReference` можно указать следующее условие:</span><span class="sxs-lookup"><span data-stu-id="aff6c-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="aff6c-182">При сборке пакета с использованием этого проекта файл Newtonsoft.Json будет отображаться как включенный только в виде зависимости для целевого объекта `net452`:</span><span class="sxs-lookup"><span data-stu-id="aff6c-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Результат применения условия к PackageReference в Visual Studio 2017](media/PackageReference-Condition.png)

<span data-ttu-id="aff6c-184">Условия можно также применять на уровне `ItemGroup`. В этом случае они применяются ко всем дочерним элементам `PackageReference`.</span><span class="sxs-lookup"><span data-stu-id="aff6c-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="aff6c-185">GeneratePathProperty</span><span class="sxs-lookup"><span data-stu-id="aff6c-185">GeneratePathProperty</span></span>

<span data-ttu-id="aff6c-186">Эта функция доступна в NuGet **5.0** или более поздней версии и в Visual Studio 2019 **16.0** или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="aff6c-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="aff6c-187">Иногда требуется ссылаться на файлы в пакете из целевого объекта MSBuild.</span><span class="sxs-lookup"><span data-stu-id="aff6c-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="aff6c-188">В проектах на основе `packages.config` пакеты устанавливаются в папку относительно файла проекта.</span><span class="sxs-lookup"><span data-stu-id="aff6c-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="aff6c-189">Однако в PackageReference пакеты [используются](../concepts/package-installation-process.md) из папки *global-packages*, которая может отличаться на разных компьютерах.</span><span class="sxs-lookup"><span data-stu-id="aff6c-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="aff6c-190">Чтобы устранить эту проблему, NuGet предоставляет свойство, указывающее на расположение, из которого будет использоваться пакет.</span><span class="sxs-lookup"><span data-stu-id="aff6c-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="aff6c-191">Пример.</span><span class="sxs-lookup"><span data-stu-id="aff6c-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="aff6c-192">Кроме того, NuGet автоматически создаст свойства для пакетов, содержащих папку tools.</span><span class="sxs-lookup"><span data-stu-id="aff6c-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

<span data-ttu-id="aff6c-193">Свойства MSBuild и удостоверения пакетов не имеют одинаковых ограничений, поэтому удостоверение пакета необходимо изменить на понятное имя MSBuild с префиксом в виде слова `Pkg`.</span><span class="sxs-lookup"><span data-stu-id="aff6c-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="aff6c-194">Чтобы проверить точное имя создаваемого свойства, изучите созданный файл [nuget.g.props](../reference/msbuild-targets.md#restore-outputs).</span><span class="sxs-lookup"><span data-stu-id="aff6c-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="aff6c-195">Предупреждения и ошибки NuGet</span><span class="sxs-lookup"><span data-stu-id="aff6c-195">NuGet warnings and errors</span></span>

<span data-ttu-id="aff6c-196">*Эта функция доступна в NuGet **4.3** или более поздней версии и в Visual Studio 2017 **15.3** или более поздней версии.*</span><span class="sxs-lookup"><span data-stu-id="aff6c-196">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="aff6c-197">Для многих сценариев упаковки и восстановления все предупреждения и ошибки NuGet кодируются и начинаются с `NU****`.</span><span class="sxs-lookup"><span data-stu-id="aff6c-197">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="aff6c-198">Все предупреждения и ошибки NuGet перечислены в [справочной](../reference/errors-and-warnings.md) документации.</span><span class="sxs-lookup"><span data-stu-id="aff6c-198">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="aff6c-199">NuGet следит за следующими свойствами предупреждения:</span><span class="sxs-lookup"><span data-stu-id="aff6c-199">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="aff6c-200">`TreatWarningsAsErrors` — обработка всех предупреждений как ошибок.</span><span class="sxs-lookup"><span data-stu-id="aff6c-200">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="aff6c-201">`WarningsAsErrors` — обработка указанных предупреждений как ошибок.</span><span class="sxs-lookup"><span data-stu-id="aff6c-201">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="aff6c-202">`NoWarn` — скрытие определенных предупреждений в масштабе проекта или пакета.</span><span class="sxs-lookup"><span data-stu-id="aff6c-202">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="aff6c-203">Примеры</span><span class="sxs-lookup"><span data-stu-id="aff6c-203">Examples:</span></span>

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="aff6c-204">Подавление предупреждений NuGet</span><span class="sxs-lookup"><span data-stu-id="aff6c-204">Suppressing NuGet warnings</span></span>

<span data-ttu-id="aff6c-205">Хотя рекомендуется разрешать все предупреждения NuGet во время выполнения операций упаковки и восстановления, в некоторых ситуациях их подавление гарантируется.</span><span class="sxs-lookup"><span data-stu-id="aff6c-205">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="aff6c-206">Чтобы подавить предупреждение в масштабе проекта, рекомендуется сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="aff6c-206">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="aff6c-207">Иногда предупреждения применяются только к определенному пакету в графе.</span><span class="sxs-lookup"><span data-stu-id="aff6c-207">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="aff6c-208">Мы можем выборочно подавить такое предупреждение, добавив `NoWarn` к элементу PackageReference.</span><span class="sxs-lookup"><span data-stu-id="aff6c-208">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="aff6c-209">Подавление предупреждений пакета NuGet в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aff6c-209">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="aff6c-210">В Visual Studio можно также [подавить предупреждения](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) в интегрированной среде разработки.</span><span class="sxs-lookup"><span data-stu-id="aff6c-210">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="aff6c-211">Блокировка зависимостей</span><span class="sxs-lookup"><span data-stu-id="aff6c-211">Locking dependencies</span></span>

<span data-ttu-id="aff6c-212">*Эта функция доступна в NuGet **4.9** или более поздней версии и в Visual Studio 2017 **15.9** или более поздней версии.*</span><span class="sxs-lookup"><span data-stu-id="aff6c-212">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="aff6c-213">Входные данные для восстановления в NuGet — это набор ссылок на пакеты из файла проекта (зависимости верхнего уровня или прямые зависимости). Выходные данные — это полный набор всех зависимостей пакета, включая транзитивные зависимости.</span><span class="sxs-lookup"><span data-stu-id="aff6c-213">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="aff6c-214">NuGet всегда пытается создать одну и ту же полную систему зависимостей пакета, если входной список PackageReference не был изменен.</span><span class="sxs-lookup"><span data-stu-id="aff6c-214">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="aff6c-215">Но в некоторых случаях это нельзя осуществить.</span><span class="sxs-lookup"><span data-stu-id="aff6c-215">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="aff6c-216">Пример:</span><span class="sxs-lookup"><span data-stu-id="aff6c-216">For example:</span></span>

* <span data-ttu-id="aff6c-217">При использовании гибких версий, таких как `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="aff6c-217">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="aff6c-218">При каждом восстановлении пакетов предполагается перейти к последней версии. Но иногда пользователям требуется, чтобы граф был закреплен за определенной последней версией, а переход к более поздней версии, если она доступна, происходил при явном указании.</span><span class="sxs-lookup"><span data-stu-id="aff6c-218">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="aff6c-219">Опубликована более новая версия пакета PackageReference, которая соответствует требованиям к версии.</span><span class="sxs-lookup"><span data-stu-id="aff6c-219">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="aff6c-220">Например,</span><span class="sxs-lookup"><span data-stu-id="aff6c-220">E.g.</span></span> 

  * <span data-ttu-id="aff6c-221">День 1. Предположим, вы указали `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, но в репозиториях NuGet были доступны версии 4.1.0, 4.2.0 и 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="aff6c-221">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="aff6c-222">В таком случае NuGet будет разрешен до версии 4.1.0 (ближайшей минимальной версии).</span><span class="sxs-lookup"><span data-stu-id="aff6c-222">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="aff6c-223">День 2: Публикуется версия 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="aff6c-223">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="aff6c-224">NuGet найдет точное соответствие и приступит разрешению до версии 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="aff6c-224">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="aff6c-225">Указанная версия пакета будет удалена из репозитория.</span><span class="sxs-lookup"><span data-stu-id="aff6c-225">A given package version is removed from the repository.</span></span> <span data-ttu-id="aff6c-226">Хотя на сайте nuget.org нельзя удалять пакеты, не все репозитории пакетов имеют такие ограничения.</span><span class="sxs-lookup"><span data-stu-id="aff6c-226">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="aff6c-227">В результате этого в NuGet выполняется поиск наиболее соответствующей версии, если не удается разрешить удаленную версию.</span><span class="sxs-lookup"><span data-stu-id="aff6c-227">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="aff6c-228">Включение функции файла блокировки</span><span class="sxs-lookup"><span data-stu-id="aff6c-228">Enabling lock file</span></span>

<span data-ttu-id="aff6c-229">Чтобы сохранить всю систему зависимостей пакета, можно воспользоваться функцией файла блокировки. Для этого задайте свойство MSBuild `RestorePackagesWithLockFile` для проекта:</span><span class="sxs-lookup"><span data-stu-id="aff6c-229">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="aff6c-230">Если это свойство задано, при восстановлении в NuGet будет создан файл блокировки — `packages.lock.json`. Он содержит список всех зависимостей пакета и находится в корневом каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="aff6c-230">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="aff6c-231">Когда в корневом каталоге проекта появится файл блокировки `packages.lock.json`, он будет использоваться при каждом восстановлении, даже если свойство `RestorePackagesWithLockFile` не задано.</span><span class="sxs-lookup"><span data-stu-id="aff6c-231">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="aff6c-232">Еще один способ воспользоваться этой функцией — создать пустой файл `packages.lock.json` в корневом каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="aff6c-232">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="aff6c-233">Поведение `restore` при использовании файла блокировки</span><span class="sxs-lookup"><span data-stu-id="aff6c-233">`restore` behavior with lock file</span></span>
<span data-ttu-id="aff6c-234">Если для проекта создан файл блокировки, NuGet использует этот файл для запуска `restore`.</span><span class="sxs-lookup"><span data-stu-id="aff6c-234">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="aff6c-235">NuGet быстро проверяет наличие изменений в зависимостях пакетов, как указано в файле проекта (или в зависимых файлах проекта). Если такие изменения не обнаружены, NuGet просто восстанавливает пакеты, указанные в файле блокировки.</span><span class="sxs-lookup"><span data-stu-id="aff6c-235">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="aff6c-236">Повторная проверка зависимостей пакета не выполняется.</span><span class="sxs-lookup"><span data-stu-id="aff6c-236">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="aff6c-237">Если диспетчер NuGet обнаруживает изменения в определенных зависимостях, указанных в файлах проекта, NuGet повторно проверяет граф пакета и обновляет файл блокировки в соответствии с новой схемой пакета для проекта.</span><span class="sxs-lookup"><span data-stu-id="aff6c-237">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="aff6c-238">В сценариях CI/CD и других сценариях, не требующих изменения зависимостей пакета во время выполнения, это можно сделать, задав для `lockedmode` значение `true`:</span><span class="sxs-lookup"><span data-stu-id="aff6c-238">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="aff6c-239">Для dotnet.exe выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="aff6c-239">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="aff6c-240">Для msbuild.exe выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="aff6c-240">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="aff6c-241">Это условное свойство MSBuild также можно задать в файле проекта:</span><span class="sxs-lookup"><span data-stu-id="aff6c-241">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="aff6c-242">Если для режима блокировки задано значение `true`, восстановятся именно те пакеты, которые перечислены в файле блокировки. Либо восстановление завершится ошибкой, если вы обновили определенные зависимости пакетов для проекта после создания файла блокировки.</span><span class="sxs-lookup"><span data-stu-id="aff6c-242">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="aff6c-243">Добавление файла блокировки в исходный репозиторий</span><span class="sxs-lookup"><span data-stu-id="aff6c-243">Make lock file part of your source repository</span></span>
<span data-ttu-id="aff6c-244">Если при создании приложения вы обнаружили, что исполняемый файл и рассматриваемый проект находятся в начале цепочки зависимостей, верните файл блокировки в репозиторий исходного кода. Так диспетчер NuGet сможет использовать его во время восстановления.</span><span class="sxs-lookup"><span data-stu-id="aff6c-244">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="aff6c-245">Но если это проект библиотеки, который не следует отправлять, или проект общего кода, от которого зависят другие проекты, **не нужно** возвращать файл блокировки в исходный код.</span><span class="sxs-lookup"><span data-stu-id="aff6c-245">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="aff6c-246">Сохранение файла блокировки не причинит вреда. Но заблокированные зависимости пакетов, перечисленные в файле блокировки, нельзя использовать для проекта общего кода во время восстановления или сборки проекта, который зависит от этого проекта общего кода.</span><span class="sxs-lookup"><span data-stu-id="aff6c-246">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="aff6c-247">Пример</span><span class="sxs-lookup"><span data-stu-id="aff6c-247">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="aff6c-248">Если `ProjectA` зависит от `PackageX` версии `2.0.0` и ссылается на проект `ProjectB`, который зависит от `PackageX` версии `1.0.0`, файл блокировки для `ProjectB` будет содержать зависимость от `PackageX` версии `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="aff6c-248">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="aff6c-249">Но при создании проекта `ProjectA` его файл блокировки будет содержать зависимость от `PackageX` версии **`2.0.0`** , а **не** `1.0.0`, как указано в файле блокировки для `ProjectB`.</span><span class="sxs-lookup"><span data-stu-id="aff6c-249">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="aff6c-250">Таким образом, файл блокировки проекта общего кода играет незначительную роль для разрешенных пакетов, от которых зависят проекты.</span><span class="sxs-lookup"><span data-stu-id="aff6c-250">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="aff6c-251">Расширяемость файла блокировки</span><span class="sxs-lookup"><span data-stu-id="aff6c-251">Lock file extensibility</span></span>

<span data-ttu-id="aff6c-252">Вы можете управлять различным поведением восстановления с использованием файла блокировки, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="aff6c-252">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="aff6c-253">Вариант NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="aff6c-253">NuGet.exe option</span></span> | <span data-ttu-id="aff6c-254">Вариант dotnet</span><span class="sxs-lookup"><span data-stu-id="aff6c-254">dotnet option</span></span> | <span data-ttu-id="aff6c-255">Вариант, аналогичный использованию MSBuild</span><span class="sxs-lookup"><span data-stu-id="aff6c-255">MSBuild equivalent option</span></span> | <span data-ttu-id="aff6c-256">Описание</span><span class="sxs-lookup"><span data-stu-id="aff6c-256">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="aff6c-257">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="aff6c-257">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="aff6c-258">Разрешение использовать файл блокировки.</span><span class="sxs-lookup"><span data-stu-id="aff6c-258">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="aff6c-259">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="aff6c-259">RestoreLockedMode</span></span> | <span data-ttu-id="aff6c-260">Включение режима блокировки для восстановления.</span><span class="sxs-lookup"><span data-stu-id="aff6c-260">Enables locked mode for restore.</span></span> <span data-ttu-id="aff6c-261">Это полезно в сценариях CI/CD, когда нужно реализовать воспроизводимые сборки.</span><span class="sxs-lookup"><span data-stu-id="aff6c-261">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="aff6c-262">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="aff6c-262">RestoreForceEvaluate</span></span> | <span data-ttu-id="aff6c-263">Этот параметр удобно использовать с пакетами с гибкими версиями, определенными в проекте.</span><span class="sxs-lookup"><span data-stu-id="aff6c-263">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="aff6c-264">По умолчанию в NuGet версия пакета не обновляется автоматически после каждого восстановления, если вы не запустили восстановление с этим параметром.</span><span class="sxs-lookup"><span data-stu-id="aff6c-264">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="aff6c-265">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="aff6c-265">NuGetLockFilePath</span></span> | <span data-ttu-id="aff6c-266">Определение размещения пользовательского файла блокировки для проекта.</span><span class="sxs-lookup"><span data-stu-id="aff6c-266">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="aff6c-267">По умолчанию в NuGet файл `packages.lock.json` хранится в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="aff6c-267">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="aff6c-268">Если в одном каталоге хранится несколько проектов, NuGet поддерживает использование файла блокировки `packages.<project_name>.lock.json` для определенного проекта.</span><span class="sxs-lookup"><span data-stu-id="aff6c-268">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
