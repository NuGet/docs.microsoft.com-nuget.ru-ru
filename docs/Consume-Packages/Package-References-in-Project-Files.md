---
title: "Формат NuGet PackageReference в файлах проектов Visual Studio | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "Подробные сведения о формате NuGet PackageReference в файлах проектов, который поддерживается в NuGet 4.0 и более поздних версиях и в Visual Studio 2017"
keywords: "зависимости пакета NuGet, ссылки на пакеты, файлы проекта, PackageReference, packages.config, project.json, VS2017, Visual Studio 2017, NuGet 4"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 275957c94e4a4bb45f359cd48816acf4f286ebad
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="81d54-104">Ссылки на пакеты (PackageReference) в файлах проектов</span><span class="sxs-lookup"><span data-stu-id="81d54-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="81d54-105">Ссылки на пакеты в узле `PackageReference` позволяют напрямую управлять зависимостями NuGet в файлах проекта вместо использования отдельного файла `packages.config` или `project.json`.</span><span class="sxs-lookup"><span data-stu-id="81d54-105">Package references, using the `PackageReference` node, allow you to manage NuGet dependencies directly within project files, rather than needing a separate `packages.config` or `project.json` file.</span></span> <span data-ttu-id="81d54-106">Этот метод не влияет на другие аспекты NuGet. Например, параметры в файлах `NuGet.Config` (включая источники пакетов) по-прежнему применяются, как описано в разделе [Настройка поведения NuGet](Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="81d54-106">This method doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](Configuring-NuGet-Behavior.md).</span></span>

> [!Important]
> <span data-ttu-id="81d54-107">В настоящее время ссылки на пакеты поддерживаются только в Visual Studio 2017 для проектов .NET Core, проектов .NET Standard и проектов универсальной платформы Windows, предназначенных для сборки 15063 системы Windows 10 (Creators Update).</span><span class="sxs-lookup"><span data-stu-id="81d54-107">At present, package references are supported in Visual Studio 2017 only, for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update).</span></span>

<span data-ttu-id="81d54-108">Подход на основе `PackageReference` позволяет использовать условия MSBuild для выбора ссылок на пакеты в соответствии с целевой платформой, конфигурацией, платформой устройств и другими признаками.</span><span class="sxs-lookup"><span data-stu-id="81d54-108">The `PackageReference` approach allows you to use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="81d54-109">Он также обеспечивает детальный контроль над зависимостями и потоком содержимого.</span><span class="sxs-lookup"><span data-stu-id="81d54-109">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="81d54-110">В плане реакции на события и [разрешения зависимостей](Dependency-Resolution.md) он аналогичен использованию `project.json`.</span><span class="sxs-lookup"><span data-stu-id="81d54-110">In terms of behavior and [dependency resolution](Dependency-Resolution.md), it's the same as using `project.json`.</span></span>

<span data-ttu-id="81d54-111">Дополнительные сведения об интеграции MSBuild со ссылками на пакеты в файлах проектов см. в разделе [Команды NuGet pack и restore как цели MSBuild](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="81d54-111">For more details on the integration of MSBuild with package references in project files, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="81d54-112">Добавление PackageReference</span><span class="sxs-lookup"><span data-stu-id="81d54-112">Adding a PackageReference</span></span>

<span data-ttu-id="81d54-113">Добавьте зависимость в файл проекта, используя следующий синтаксис:</span><span class="sxs-lookup"><span data-stu-id="81d54-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />    
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="81d54-114">Управление версией зависимости</span><span class="sxs-lookup"><span data-stu-id="81d54-114">Controlling dependency version</span></span>

<span data-ttu-id="81d54-115">При указании версии пакета действует то же соглашение, что и при использовании файла `packages.config` или `project.json`:</span><span class="sxs-lookup"><span data-stu-id="81d54-115">The convention for specifying the version of a package is the same as when using `packages.config` or `project.json`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="81d54-116">В приведенном выше примере значение 3.6.0 означает версию 3.6.0 или любую более позднюю версию, причем предпочтение отдается самой ранней версии, как описано в разделе [Управление версиями пакета](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="81d54-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="81d54-117">Гибкие версии</span><span class="sxs-lookup"><span data-stu-id="81d54-117">Floating Versions</span></span>

<span data-ttu-id="81d54-118">[Гибкие версии](../consume-packages/dependency-resolution.md#floating-versions) можно использовать с `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="81d54-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="81d54-119">Управление ресурсами зависимости</span><span class="sxs-lookup"><span data-stu-id="81d54-119">Controlling dependency assets</span></span>

<span data-ttu-id="81d54-120">Зависимость может применяться исключительно для удобства разработки. В этом случае доступ к ней не нужно предоставлять проектам, использующим пакет.</span><span class="sxs-lookup"><span data-stu-id="81d54-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="81d54-121">Для управления таким поведением могут служить метаданные `PrivateAssets`.</span><span class="sxs-lookup"><span data-stu-id="81d54-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="81d54-122">Ниже перечислены теги метаданных, управляющие ресурсами зависимостей.</span><span class="sxs-lookup"><span data-stu-id="81d54-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="81d54-123">Тег</span><span class="sxs-lookup"><span data-stu-id="81d54-123">Tag</span></span> | <span data-ttu-id="81d54-124">Описание:</span><span class="sxs-lookup"><span data-stu-id="81d54-124">Description</span></span> | <span data-ttu-id="81d54-125">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="81d54-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="81d54-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="81d54-126">IncludeAssets</span></span> | <span data-ttu-id="81d54-127">Эти ресурсы будут использоваться.</span><span class="sxs-lookup"><span data-stu-id="81d54-127">These assets will be consumed</span></span> | <span data-ttu-id="81d54-128">все</span><span class="sxs-lookup"><span data-stu-id="81d54-128">all</span></span> |
| <span data-ttu-id="81d54-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="81d54-129">ExcludeAssets</span></span> | <span data-ttu-id="81d54-130">Эти ресурсы не будут использоваться.</span><span class="sxs-lookup"><span data-stu-id="81d54-130">These assets will not be consumed</span></span> | <span data-ttu-id="81d54-131">Нет</span><span class="sxs-lookup"><span data-stu-id="81d54-131">none</span></span> | 
| <span data-ttu-id="81d54-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="81d54-132">PrivateAssets</span></span> | <span data-ttu-id="81d54-133">Эти ресурсы будут использоваться, но не будут передаваться в родительский проект.</span><span class="sxs-lookup"><span data-stu-id="81d54-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="81d54-134">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="81d54-134">contentfiles;analyzers;build</span></span> |


<span data-ttu-id="81d54-135">Ниже приводятся допустимые значения этих тегов. Несколько значений должны разделяться точкой с запятой. Это не относится к значениям `all` и `none`, которые должны использоваться отдельно.</span><span class="sxs-lookup"><span data-stu-id="81d54-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="81d54-136">Значение</span><span class="sxs-lookup"><span data-stu-id="81d54-136">Value</span></span> | <span data-ttu-id="81d54-137">Описание:</span><span class="sxs-lookup"><span data-stu-id="81d54-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="81d54-138">compile</span><span class="sxs-lookup"><span data-stu-id="81d54-138">compile</span></span> | <span data-ttu-id="81d54-139">Содержимое папки `lib`</span><span class="sxs-lookup"><span data-stu-id="81d54-139">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="81d54-140">исполняющая среда</span><span class="sxs-lookup"><span data-stu-id="81d54-140">runtime</span></span> | <span data-ttu-id="81d54-141">Содержимое папки `runtime`</span><span class="sxs-lookup"><span data-stu-id="81d54-141">Contents of the `runtime` folder</span></span> |
| <span data-ttu-id="81d54-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="81d54-142">contentFiles</span></span> | <span data-ttu-id="81d54-143">Содержимое папки `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="81d54-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="81d54-144">выполнить сборку</span><span class="sxs-lookup"><span data-stu-id="81d54-144">build</span></span> | <span data-ttu-id="81d54-145">Свойства и цели в папке `build`</span><span class="sxs-lookup"><span data-stu-id="81d54-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="81d54-146">analyzers</span><span class="sxs-lookup"><span data-stu-id="81d54-146">analyzers</span></span> | <span data-ttu-id="81d54-147">Анализаторы .NET</span><span class="sxs-lookup"><span data-stu-id="81d54-147">.NET analyzers</span></span> |
| <span data-ttu-id="81d54-148">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="81d54-148">native</span></span> | <span data-ttu-id="81d54-149">Содержимое папки `native`</span><span class="sxs-lookup"><span data-stu-id="81d54-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="81d54-150">Нет</span><span class="sxs-lookup"><span data-stu-id="81d54-150">none</span></span> | <span data-ttu-id="81d54-151">Никакие из перечисленных выше ресурсов не используются.</span><span class="sxs-lookup"><span data-stu-id="81d54-151">None of the above are used.</span></span> |
| <span data-ttu-id="81d54-152">все</span><span class="sxs-lookup"><span data-stu-id="81d54-152">all</span></span> | <span data-ttu-id="81d54-153">Используются все перечисленные выше ресурсы (кроме `none`).</span><span class="sxs-lookup"><span data-stu-id="81d54-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="81d54-154">В приведенном ниже примере проектом используются все ресурсы, кроме файлов содержимого из пакета, и в родительский проект передаются все ресурсы, кроме файлов содержимого и анализаторов.</span><span class="sxs-lookup"><span data-stu-id="81d54-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="81d54-155">Обратите внимание: так как папка `build` не включена в `PrivateAssets`, цели и свойства *будут* передаваться в родительский проект.</span><span class="sxs-lookup"><span data-stu-id="81d54-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="81d54-156">Предположим, что приведенная выше ссылка используется в проекте, в рамках которого выполняется сборка пакета NuGet с именем AppLogger.</span><span class="sxs-lookup"><span data-stu-id="81d54-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="81d54-157">Пакет AppLogger может использовать цели и свойства из `Contoso.Utility.UsefulStuff`, так же как и проекты, использующие AppLogger.</span><span class="sxs-lookup"><span data-stu-id="81d54-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="81d54-158">Добавление условия PackageReference</span><span class="sxs-lookup"><span data-stu-id="81d54-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="81d54-159">С помощью условий можно управлять тем, когда следует включать пакет. В условиях можно использовать любые переменные MSBuild или переменные, определенные в файлах целей или свойств.</span><span class="sxs-lookup"><span data-stu-id="81d54-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="81d54-160">Однако в настоящее время поддерживается только переменная `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="81d54-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="81d54-161">Например, предположим, что целевыми платформами являются `netstandard1.4` и `net452`, но зависимость применима только для `net452`.</span><span class="sxs-lookup"><span data-stu-id="81d54-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="81d54-162">В этом случае в проект `netstandard1.4`, который использует пакет, не следует добавлять эту ненужную зависимость.</span><span class="sxs-lookup"><span data-stu-id="81d54-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="81d54-163">В этом случае в узле `PackageReference` можно указать следующее условие:</span><span class="sxs-lookup"><span data-stu-id="81d54-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="81d54-164">В пакет, сборка которого выполнена с помощью этого проекта, файл Newtonsoft.json будет включен в качестве зависимости только для целевой платформы `net452`.</span><span class="sxs-lookup"><span data-stu-id="81d54-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Результат применения условия к PackageReference в Visual Studio 2017](media/PackageReference-Condition.png)

<span data-ttu-id="81d54-166">Условия можно также применять на уровне `ItemGroup`. В этом случае они применяются ко всем дочерним элементам `PackageReference`.</span><span class="sxs-lookup"><span data-stu-id="81d54-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
