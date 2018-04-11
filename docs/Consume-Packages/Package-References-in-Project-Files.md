---
title: Формат NuGet PackageReference (ссылки на пакет в файлах проектов) | Документация Майкрософт
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Подробные сведения о формате NuGet PackageReference в файлах проектов, который поддерживается в NuGet 4.0 и более поздних версиях, в VS2017 и в .NET Core 2.0
keywords: зависимости пакета NuGet, ссылки на пакеты, файлы проекта, PackageReference, packages.config, VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 7844ace0565b2e70f8f68e6e61548f0f28171689
ms.sourcegitcommit: 5b223c5814799caa6309e95792a2d338df692778
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="f1662-104">Ссылки на пакеты (PackageReference) в файлах проектов</span><span class="sxs-lookup"><span data-stu-id="f1662-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="f1662-105">Ссылки на пакеты в узле `PackageReference` позволяют напрямую управлять зависимостями NuGet в файлах проекта (вместо использования отдельного файла `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="f1662-105">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="f1662-106">Использование PackageReference не влияет на другие аспекты NuGet. Например, параметры в файлах `NuGet.Config` (включая источники пакетов) по-прежнему применяются, как описано в разделе [Настройка поведения NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="f1662-106">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="f1662-107">PackageReference также позволяет использовать условия MSBuild для выбора ссылок на пакеты в соответствии с целевой платформой, конфигурацией, платформой устройств и другими признаками.</span><span class="sxs-lookup"><span data-stu-id="f1662-107">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="f1662-108">Он также обеспечивает детальный контроль над зависимостями и потоком содержимого.</span><span class="sxs-lookup"><span data-stu-id="f1662-108">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="f1662-109">(Дополнительные сведения см. в разделе [Объекты pack и restore NuGet в качестве целевых объектов MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="f1662-109">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="f1662-110">По умолчанию PackageReference используется для проектов .NET Core, проектов .NET Standard и проектов универсальной платформы Windows, предназначенных для сборки 15063 системы Windows 10 (Creators Update), за исключением проектов C++ UWP.</span><span class="sxs-lookup"><span data-stu-id="f1662-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="f1662-111">Проекты полной версии .NET Framework поддерживают PackageReference, но сейчас по умолчанию используют `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="f1662-111">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="f1662-112">Чтобы использовать PackageReference, перенесите зависимости из `packages.config` в файл проекта, а затем удалите packages.config.</span><span class="sxs-lookup"><span data-stu-id="f1662-112">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="f1662-113">Добавление PackageReference</span><span class="sxs-lookup"><span data-stu-id="f1662-113">Adding a PackageReference</span></span>

<span data-ttu-id="f1662-114">Добавьте зависимость в файл проекта, используя следующий синтаксис:</span><span class="sxs-lookup"><span data-stu-id="f1662-114">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="f1662-115">Управление версией зависимости</span><span class="sxs-lookup"><span data-stu-id="f1662-115">Controlling dependency version</span></span>

<span data-ttu-id="f1662-116">При указании версии пакета действует то же соглашение, что и при использовании файла `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="f1662-116">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="f1662-117">В приведенном выше примере значение 3.6.0 означает версию 3.6.0 или любую более позднюю версию, причем предпочтение отдается самой ранней версии, как описано в разделе [Управление версиями пакета](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="f1662-117">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="f1662-118">Гибкие версии</span><span class="sxs-lookup"><span data-stu-id="f1662-118">Floating Versions</span></span>

<span data-ttu-id="f1662-119">[Гибкие версии](../consume-packages/dependency-resolution.md#floating-versions) можно использовать с `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="f1662-119">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="f1662-120">Управление ресурсами зависимости</span><span class="sxs-lookup"><span data-stu-id="f1662-120">Controlling dependency assets</span></span>

<span data-ttu-id="f1662-121">Зависимость может применяться исключительно для удобства разработки. В этом случае доступ к ней не нужно предоставлять проектам, использующим пакет.</span><span class="sxs-lookup"><span data-stu-id="f1662-121">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="f1662-122">Для управления таким поведением могут служить метаданные `PrivateAssets`.</span><span class="sxs-lookup"><span data-stu-id="f1662-122">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="f1662-123">Ниже перечислены теги метаданных, управляющие ресурсами зависимостей.</span><span class="sxs-lookup"><span data-stu-id="f1662-123">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="f1662-124">Тег</span><span class="sxs-lookup"><span data-stu-id="f1662-124">Tag</span></span> | <span data-ttu-id="f1662-125">Описание:</span><span class="sxs-lookup"><span data-stu-id="f1662-125">Description</span></span> | <span data-ttu-id="f1662-126">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="f1662-126">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1662-127">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="f1662-127">IncludeAssets</span></span> | <span data-ttu-id="f1662-128">Эти ресурсы будут использоваться.</span><span class="sxs-lookup"><span data-stu-id="f1662-128">These assets will be consumed</span></span> | <span data-ttu-id="f1662-129">все</span><span class="sxs-lookup"><span data-stu-id="f1662-129">all</span></span> |
| <span data-ttu-id="f1662-130">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="f1662-130">ExcludeAssets</span></span> | <span data-ttu-id="f1662-131">Эти ресурсы не будут использоваться.</span><span class="sxs-lookup"><span data-stu-id="f1662-131">These assets will not be consumed</span></span> | <span data-ttu-id="f1662-132">Нет</span><span class="sxs-lookup"><span data-stu-id="f1662-132">none</span></span> |
| <span data-ttu-id="f1662-133">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="f1662-133">PrivateAssets</span></span> | <span data-ttu-id="f1662-134">Эти ресурсы будут использоваться, но не будут передаваться в родительский проект.</span><span class="sxs-lookup"><span data-stu-id="f1662-134">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="f1662-135">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="f1662-135">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="f1662-136">Ниже приводятся допустимые значения этих тегов. Несколько значений должны разделяться точкой с запятой. Это не относится к значениям `all` и `none`, которые должны использоваться отдельно.</span><span class="sxs-lookup"><span data-stu-id="f1662-136">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="f1662-137">Значение</span><span class="sxs-lookup"><span data-stu-id="f1662-137">Value</span></span> | <span data-ttu-id="f1662-138">Описание:</span><span class="sxs-lookup"><span data-stu-id="f1662-138">Description</span></span> |
| --- | ---
| <span data-ttu-id="f1662-139">compile</span><span class="sxs-lookup"><span data-stu-id="f1662-139">compile</span></span> | <span data-ttu-id="f1662-140">Содержимое папки `lib`; управляет возможностью компиляции проекта с использованием сборок в этой папке</span><span class="sxs-lookup"><span data-stu-id="f1662-140">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="f1662-141">исполняющая среда</span><span class="sxs-lookup"><span data-stu-id="f1662-141">runtime</span></span> | <span data-ttu-id="f1662-142">Содержимое папки `lib` и `runtimes`; управляет возможностью копирования этих сборок в выходной каталог сборки</span><span class="sxs-lookup"><span data-stu-id="f1662-142">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="f1662-143">contentFiles</span><span class="sxs-lookup"><span data-stu-id="f1662-143">contentFiles</span></span> | <span data-ttu-id="f1662-144">Содержимое папки `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="f1662-144">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="f1662-145">выполнить сборку</span><span class="sxs-lookup"><span data-stu-id="f1662-145">build</span></span> | <span data-ttu-id="f1662-146">Свойства и цели в папке `build`</span><span class="sxs-lookup"><span data-stu-id="f1662-146">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="f1662-147">analyzers</span><span class="sxs-lookup"><span data-stu-id="f1662-147">analyzers</span></span> | <span data-ttu-id="f1662-148">Анализаторы .NET</span><span class="sxs-lookup"><span data-stu-id="f1662-148">.NET analyzers</span></span> |
| <span data-ttu-id="f1662-149">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="f1662-149">native</span></span> | <span data-ttu-id="f1662-150">Содержимое папки `native`</span><span class="sxs-lookup"><span data-stu-id="f1662-150">Contents of the `native` folder</span></span> |
| <span data-ttu-id="f1662-151">Нет</span><span class="sxs-lookup"><span data-stu-id="f1662-151">none</span></span> | <span data-ttu-id="f1662-152">Никакие из перечисленных выше ресурсов не используются.</span><span class="sxs-lookup"><span data-stu-id="f1662-152">None of the above are used.</span></span> |
| <span data-ttu-id="f1662-153">все</span><span class="sxs-lookup"><span data-stu-id="f1662-153">all</span></span> | <span data-ttu-id="f1662-154">Используются все перечисленные выше ресурсы (кроме `none`).</span><span class="sxs-lookup"><span data-stu-id="f1662-154">All of the above (except `none`)</span></span> |

<span data-ttu-id="f1662-155">В приведенном ниже примере проектом используются все ресурсы, кроме файлов содержимого из пакета, и в родительский проект передаются все ресурсы, кроме файлов содержимого и анализаторов.</span><span class="sxs-lookup"><span data-stu-id="f1662-155">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="f1662-156">Обратите внимание: так как папка `build` не включена в `PrivateAssets`, цели и свойства *будут* передаваться в родительский проект.</span><span class="sxs-lookup"><span data-stu-id="f1662-156">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="f1662-157">Предположим, что приведенная выше ссылка используется в проекте, в рамках которого выполняется сборка пакета NuGet с именем AppLogger.</span><span class="sxs-lookup"><span data-stu-id="f1662-157">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="f1662-158">Пакет AppLogger может использовать цели и свойства из `Contoso.Utility.UsefulStuff`, так же как и проекты, использующие AppLogger.</span><span class="sxs-lookup"><span data-stu-id="f1662-158">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="f1662-159">Добавление условия PackageReference</span><span class="sxs-lookup"><span data-stu-id="f1662-159">Adding a PackageReference condition</span></span>

<span data-ttu-id="f1662-160">С помощью условий можно управлять тем, когда следует включать пакет. В условиях можно использовать любые переменные MSBuild или переменные, определенные в файлах целей или свойств.</span><span class="sxs-lookup"><span data-stu-id="f1662-160">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="f1662-161">Однако в настоящее время поддерживается только переменная `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="f1662-161">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="f1662-162">Например, предположим, что целевыми платформами являются `netstandard1.4` и `net452`, но зависимость применима только для `net452`.</span><span class="sxs-lookup"><span data-stu-id="f1662-162">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="f1662-163">В этом случае в проект `netstandard1.4`, который использует пакет, не следует добавлять эту ненужную зависимость.</span><span class="sxs-lookup"><span data-stu-id="f1662-163">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="f1662-164">В этом случае в узле `PackageReference` можно указать следующее условие:</span><span class="sxs-lookup"><span data-stu-id="f1662-164">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="f1662-165">В пакет, сборка которого выполнена с помощью этого проекта, файл Newtonsoft.json будет включен в качестве зависимости только для целевой платформы `net452`.</span><span class="sxs-lookup"><span data-stu-id="f1662-165">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Результат применения условия к PackageReference в Visual Studio 2017](media/PackageReference-Condition.png)

<span data-ttu-id="f1662-167">Условия можно также применять на уровне `ItemGroup`. В этом случае они применяются ко всем дочерним элементам `PackageReference`.</span><span class="sxs-lookup"><span data-stu-id="f1662-167">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
