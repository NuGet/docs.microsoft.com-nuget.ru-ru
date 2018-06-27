---
title: Формат NuGet PackageReference (ссылки на пакеты в файлах проектов)
description: Подробные сведения о формате NuGet PackageReference в файлах проектов, который поддерживается в NuGet 4.0 и более поздних версиях, в VS2017 и в .NET Core 2.0
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 61f447877459764906cf9a2b88b32a8bc0553689
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817675"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="8e79c-103">Ссылки на пакеты (PackageReference) в файлах проектов</span><span class="sxs-lookup"><span data-stu-id="8e79c-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="8e79c-104">Ссылки на пакеты в узле `PackageReference` позволяют напрямую управлять зависимостями NuGet в файлах проекта (вместо использования отдельного файла `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="8e79c-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="8e79c-105">Использование PackageReference не влияет на другие аспекты NuGet. Например, параметры в файлах `NuGet.Config` (включая источники пакетов) по-прежнему применяются, как описано в разделе [Настройка поведения NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="8e79c-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="8e79c-106">PackageReference также позволяет использовать условия MSBuild для выбора ссылок на пакеты в соответствии с целевой платформой, конфигурацией, платформой устройств и другими признаками.</span><span class="sxs-lookup"><span data-stu-id="8e79c-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="8e79c-107">Он также обеспечивает детальный контроль над зависимостями и потоком содержимого.</span><span class="sxs-lookup"><span data-stu-id="8e79c-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="8e79c-108">(Дополнительные сведения см. в разделе [Объекты pack и restore NuGet в качестве целевых объектов MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="8e79c-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="8e79c-109">По умолчанию PackageReference используется для проектов .NET Core, проектов .NET Standard и проектов универсальной платформы Windows, предназначенных для сборки 15063 системы Windows 10 (Creators Update), за исключением проектов C++ UWP.</span><span class="sxs-lookup"><span data-stu-id="8e79c-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="8e79c-110">Проекты полной версии .NET Framework поддерживают PackageReference, но сейчас по умолчанию используют `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="8e79c-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="8e79c-111">Чтобы использовать PackageReference, перенесите зависимости из `packages.config` в файл проекта, а затем удалите packages.config.</span><span class="sxs-lookup"><span data-stu-id="8e79c-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="8e79c-112">Добавление PackageReference</span><span class="sxs-lookup"><span data-stu-id="8e79c-112">Adding a PackageReference</span></span>

<span data-ttu-id="8e79c-113">Добавьте зависимость в файл проекта, используя следующий синтаксис:</span><span class="sxs-lookup"><span data-stu-id="8e79c-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="8e79c-114">Управление версией зависимости</span><span class="sxs-lookup"><span data-stu-id="8e79c-114">Controlling dependency version</span></span>

<span data-ttu-id="8e79c-115">При указании версии пакета действует то же соглашение, что и при использовании файла `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="8e79c-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="8e79c-116">В приведенном выше примере значение 3.6.0 означает версию 3.6.0 или любую более позднюю версию, причем предпочтение отдается самой ранней версии, как описано в разделе [Управление версиями пакета](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="8e79c-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="8e79c-117">Использование PackageReference для проекта без объектов PackageReference</span><span class="sxs-lookup"><span data-stu-id="8e79c-117">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="8e79c-118">Дополнительно: если в проекте нет установленных пакетов (нет объектов PackageReference в файле, а также файла packages.config), но вы хотите восстанавливать проект в стиле PackageReference, можно задать для свойства RestoreProjectStyle проекта значение PackageReference в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="8e79c-118">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="8e79c-119">Это может быть удобно при ссылке на проекты в стиле PackageReference (существующие CSPROJ- или SDK-проекты).</span><span class="sxs-lookup"><span data-stu-id="8e79c-119">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="8e79c-120">Это позволит вашему проекту транзитивно ссылаться на пакеты, на которые ссылаются эти проекты.</span><span class="sxs-lookup"><span data-stu-id="8e79c-120">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="8e79c-121">Гибкие версии</span><span class="sxs-lookup"><span data-stu-id="8e79c-121">Floating Versions</span></span>

<span data-ttu-id="8e79c-122">[Гибкие версии](../consume-packages/dependency-resolution.md#floating-versions) можно использовать с `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="8e79c-122">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="8e79c-123">Управление ресурсами зависимости</span><span class="sxs-lookup"><span data-stu-id="8e79c-123">Controlling dependency assets</span></span>

<span data-ttu-id="8e79c-124">Зависимость может применяться исключительно для удобства разработки. В этом случае доступ к ней не нужно предоставлять проектам, использующим пакет.</span><span class="sxs-lookup"><span data-stu-id="8e79c-124">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="8e79c-125">Для управления таким поведением могут служить метаданные `PrivateAssets`.</span><span class="sxs-lookup"><span data-stu-id="8e79c-125">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="8e79c-126">Ниже перечислены теги метаданных, управляющие ресурсами зависимостей.</span><span class="sxs-lookup"><span data-stu-id="8e79c-126">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="8e79c-127">Тег</span><span class="sxs-lookup"><span data-stu-id="8e79c-127">Tag</span></span> | <span data-ttu-id="8e79c-128">Описание:</span><span class="sxs-lookup"><span data-stu-id="8e79c-128">Description</span></span> | <span data-ttu-id="8e79c-129">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="8e79c-129">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8e79c-130">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="8e79c-130">IncludeAssets</span></span> | <span data-ttu-id="8e79c-131">Эти ресурсы будут использоваться.</span><span class="sxs-lookup"><span data-stu-id="8e79c-131">These assets will be consumed</span></span> | <span data-ttu-id="8e79c-132">все</span><span class="sxs-lookup"><span data-stu-id="8e79c-132">all</span></span> |
| <span data-ttu-id="8e79c-133">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="8e79c-133">ExcludeAssets</span></span> | <span data-ttu-id="8e79c-134">Эти ресурсы не будут использоваться.</span><span class="sxs-lookup"><span data-stu-id="8e79c-134">These assets will not be consumed</span></span> | <span data-ttu-id="8e79c-135">Нет</span><span class="sxs-lookup"><span data-stu-id="8e79c-135">none</span></span> |
| <span data-ttu-id="8e79c-136">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="8e79c-136">PrivateAssets</span></span> | <span data-ttu-id="8e79c-137">Эти ресурсы будут использоваться, но не будут передаваться в родительский проект.</span><span class="sxs-lookup"><span data-stu-id="8e79c-137">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="8e79c-138">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="8e79c-138">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="8e79c-139">Ниже приводятся допустимые значения этих тегов. Несколько значений должны разделяться точкой с запятой. Это не относится к значениям `all` и `none`, которые должны использоваться отдельно.</span><span class="sxs-lookup"><span data-stu-id="8e79c-139">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="8e79c-140">Значение</span><span class="sxs-lookup"><span data-stu-id="8e79c-140">Value</span></span> | <span data-ttu-id="8e79c-141">Описание:</span><span class="sxs-lookup"><span data-stu-id="8e79c-141">Description</span></span> |
| --- | ---
| <span data-ttu-id="8e79c-142">compile</span><span class="sxs-lookup"><span data-stu-id="8e79c-142">compile</span></span> | <span data-ttu-id="8e79c-143">Содержимое папки `lib`; управляет возможностью компиляции проекта с использованием сборок в этой папке</span><span class="sxs-lookup"><span data-stu-id="8e79c-143">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="8e79c-144">исполняющая среда</span><span class="sxs-lookup"><span data-stu-id="8e79c-144">runtime</span></span> | <span data-ttu-id="8e79c-145">Содержимое папки `lib` и `runtimes`; управляет возможностью копирования этих сборок в выходной каталог сборки</span><span class="sxs-lookup"><span data-stu-id="8e79c-145">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="8e79c-146">contentFiles</span><span class="sxs-lookup"><span data-stu-id="8e79c-146">contentFiles</span></span> | <span data-ttu-id="8e79c-147">Содержимое папки `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="8e79c-147">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="8e79c-148">выполнить сборку</span><span class="sxs-lookup"><span data-stu-id="8e79c-148">build</span></span> | <span data-ttu-id="8e79c-149">Свойства и цели в папке `build`</span><span class="sxs-lookup"><span data-stu-id="8e79c-149">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="8e79c-150">analyzers</span><span class="sxs-lookup"><span data-stu-id="8e79c-150">analyzers</span></span> | <span data-ttu-id="8e79c-151">Анализаторы .NET</span><span class="sxs-lookup"><span data-stu-id="8e79c-151">.NET analyzers</span></span> |
| <span data-ttu-id="8e79c-152">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="8e79c-152">native</span></span> | <span data-ttu-id="8e79c-153">Содержимое папки `native`</span><span class="sxs-lookup"><span data-stu-id="8e79c-153">Contents of the `native` folder</span></span> |
| <span data-ttu-id="8e79c-154">Нет</span><span class="sxs-lookup"><span data-stu-id="8e79c-154">none</span></span> | <span data-ttu-id="8e79c-155">Никакие из перечисленных выше ресурсов не используются.</span><span class="sxs-lookup"><span data-stu-id="8e79c-155">None of the above are used.</span></span> |
| <span data-ttu-id="8e79c-156">все</span><span class="sxs-lookup"><span data-stu-id="8e79c-156">all</span></span> | <span data-ttu-id="8e79c-157">Используются все перечисленные выше ресурсы (кроме `none`).</span><span class="sxs-lookup"><span data-stu-id="8e79c-157">All of the above (except `none`)</span></span> |

<span data-ttu-id="8e79c-158">В приведенном ниже примере проектом используются все ресурсы, кроме файлов содержимого из пакета, и в родительский проект передаются все ресурсы, кроме файлов содержимого и анализаторов.</span><span class="sxs-lookup"><span data-stu-id="8e79c-158">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="8e79c-159">Обратите внимание: так как папка `build` не включена в `PrivateAssets`, цели и свойства *будут* передаваться в родительский проект.</span><span class="sxs-lookup"><span data-stu-id="8e79c-159">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="8e79c-160">Предположим, что приведенная выше ссылка используется в проекте, в рамках которого выполняется сборка пакета NuGet с именем AppLogger.</span><span class="sxs-lookup"><span data-stu-id="8e79c-160">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="8e79c-161">Пакет AppLogger может использовать цели и свойства из `Contoso.Utility.UsefulStuff`, так же как и проекты, использующие AppLogger.</span><span class="sxs-lookup"><span data-stu-id="8e79c-161">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="8e79c-162">Добавление условия PackageReference</span><span class="sxs-lookup"><span data-stu-id="8e79c-162">Adding a PackageReference condition</span></span>

<span data-ttu-id="8e79c-163">С помощью условий можно управлять тем, когда следует включать пакет. В условиях можно использовать любые переменные MSBuild или переменные, определенные в файлах целей или свойств.</span><span class="sxs-lookup"><span data-stu-id="8e79c-163">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="8e79c-164">Однако в настоящее время поддерживается только переменная `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="8e79c-164">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="8e79c-165">Например, предположим, что целевыми платформами являются `netstandard1.4` и `net452`, но зависимость применима только для `net452`.</span><span class="sxs-lookup"><span data-stu-id="8e79c-165">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="8e79c-166">В этом случае в проект `netstandard1.4`, который использует пакет, не следует добавлять эту ненужную зависимость.</span><span class="sxs-lookup"><span data-stu-id="8e79c-166">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="8e79c-167">В этом случае в узле `PackageReference` можно указать следующее условие:</span><span class="sxs-lookup"><span data-stu-id="8e79c-167">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="8e79c-168">В пакет, сборка которого выполнена с помощью этого проекта, файл Newtonsoft.json будет включен в качестве зависимости только для целевой платформы `net452`.</span><span class="sxs-lookup"><span data-stu-id="8e79c-168">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Результат применения условия к PackageReference в Visual Studio 2017](media/PackageReference-Condition.png)

<span data-ttu-id="8e79c-170">Условия можно также применять на уровне `ItemGroup`. В этом случае они применяются ко всем дочерним элементам `PackageReference`.</span><span class="sxs-lookup"><span data-stu-id="8e79c-170">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
