---
title: Формат NuGet PackageReference (ссылки на пакеты в файлах проектов)
description: Подробные сведения о формате NuGet PackageReference в файлах проектов, который поддерживается в NuGet 4.0 и более поздних версиях, в VS2017 и в .NET Core 2.0
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 8f277a8af7f988d6fdcfa75c43a10b3792c2ae22
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="e8423-103">Ссылки на пакеты (PackageReference) в файлах проектов</span><span class="sxs-lookup"><span data-stu-id="e8423-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="e8423-104">Ссылки на пакеты в узле `PackageReference` позволяют напрямую управлять зависимостями NuGet в файлах проекта (вместо использования отдельного файла `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="e8423-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="e8423-105">Использование PackageReference не влияет на другие аспекты NuGet. Например, параметры в файлах `NuGet.Config` (включая источники пакетов) по-прежнему применяются, как описано в разделе [Настройка поведения NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="e8423-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="e8423-106">PackageReference также позволяет использовать условия MSBuild для выбора ссылок на пакеты в соответствии с целевой платформой, конфигурацией, платформой устройств и другими признаками.</span><span class="sxs-lookup"><span data-stu-id="e8423-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="e8423-107">Он также обеспечивает детальный контроль над зависимостями и потоком содержимого.</span><span class="sxs-lookup"><span data-stu-id="e8423-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="e8423-108">(Дополнительные сведения см. в разделе [Объекты pack и restore NuGet в качестве целевых объектов MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="e8423-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="e8423-109">По умолчанию PackageReference используется для проектов .NET Core, проектов .NET Standard и проектов универсальной платформы Windows, предназначенных для сборки 15063 системы Windows 10 (Creators Update), за исключением проектов C++ UWP.</span><span class="sxs-lookup"><span data-stu-id="e8423-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="e8423-110">Проекты полной версии .NET Framework поддерживают PackageReference, но сейчас по умолчанию используют `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="e8423-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="e8423-111">Чтобы использовать PackageReference, перенесите зависимости из `packages.config` в файл проекта, а затем удалите packages.config.</span><span class="sxs-lookup"><span data-stu-id="e8423-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="e8423-112">Добавление PackageReference</span><span class="sxs-lookup"><span data-stu-id="e8423-112">Adding a PackageReference</span></span>

<span data-ttu-id="e8423-113">Добавьте зависимость в файл проекта, используя следующий синтаксис:</span><span class="sxs-lookup"><span data-stu-id="e8423-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="e8423-114">Управление версией зависимости</span><span class="sxs-lookup"><span data-stu-id="e8423-114">Controlling dependency version</span></span>

<span data-ttu-id="e8423-115">При указании версии пакета действует то же соглашение, что и при использовании файла `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="e8423-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="e8423-116">В приведенном выше примере значение 3.6.0 означает версию 3.6.0 или любую более позднюю версию, причем предпочтение отдается самой ранней версии, как описано в разделе [Управление версиями пакета](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="e8423-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="e8423-117">Гибкие версии</span><span class="sxs-lookup"><span data-stu-id="e8423-117">Floating Versions</span></span>

<span data-ttu-id="e8423-118">[Гибкие версии](../consume-packages/dependency-resolution.md#floating-versions) можно использовать с `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="e8423-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="e8423-119">Управление ресурсами зависимости</span><span class="sxs-lookup"><span data-stu-id="e8423-119">Controlling dependency assets</span></span>

<span data-ttu-id="e8423-120">Зависимость может применяться исключительно для удобства разработки. В этом случае доступ к ней не нужно предоставлять проектам, использующим пакет.</span><span class="sxs-lookup"><span data-stu-id="e8423-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="e8423-121">Для управления таким поведением могут служить метаданные `PrivateAssets`.</span><span class="sxs-lookup"><span data-stu-id="e8423-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="e8423-122">Ниже перечислены теги метаданных, управляющие ресурсами зависимостей.</span><span class="sxs-lookup"><span data-stu-id="e8423-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="e8423-123">Тег</span><span class="sxs-lookup"><span data-stu-id="e8423-123">Tag</span></span> | <span data-ttu-id="e8423-124">Описание:</span><span class="sxs-lookup"><span data-stu-id="e8423-124">Description</span></span> | <span data-ttu-id="e8423-125">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e8423-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8423-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="e8423-126">IncludeAssets</span></span> | <span data-ttu-id="e8423-127">Эти ресурсы будут использоваться.</span><span class="sxs-lookup"><span data-stu-id="e8423-127">These assets will be consumed</span></span> | <span data-ttu-id="e8423-128">все</span><span class="sxs-lookup"><span data-stu-id="e8423-128">all</span></span> |
| <span data-ttu-id="e8423-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="e8423-129">ExcludeAssets</span></span> | <span data-ttu-id="e8423-130">Эти ресурсы не будут использоваться.</span><span class="sxs-lookup"><span data-stu-id="e8423-130">These assets will not be consumed</span></span> | <span data-ttu-id="e8423-131">Нет</span><span class="sxs-lookup"><span data-stu-id="e8423-131">none</span></span> |
| <span data-ttu-id="e8423-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="e8423-132">PrivateAssets</span></span> | <span data-ttu-id="e8423-133">Эти ресурсы будут использоваться, но не будут передаваться в родительский проект.</span><span class="sxs-lookup"><span data-stu-id="e8423-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="e8423-134">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="e8423-134">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="e8423-135">Ниже приводятся допустимые значения этих тегов. Несколько значений должны разделяться точкой с запятой. Это не относится к значениям `all` и `none`, которые должны использоваться отдельно.</span><span class="sxs-lookup"><span data-stu-id="e8423-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="e8423-136">Значение</span><span class="sxs-lookup"><span data-stu-id="e8423-136">Value</span></span> | <span data-ttu-id="e8423-137">Описание:</span><span class="sxs-lookup"><span data-stu-id="e8423-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="e8423-138">compile</span><span class="sxs-lookup"><span data-stu-id="e8423-138">compile</span></span> | <span data-ttu-id="e8423-139">Содержимое папки `lib`; управляет возможностью компиляции проекта с использованием сборок в этой папке</span><span class="sxs-lookup"><span data-stu-id="e8423-139">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="e8423-140">исполняющая среда</span><span class="sxs-lookup"><span data-stu-id="e8423-140">runtime</span></span> | <span data-ttu-id="e8423-141">Содержимое папки `lib` и `runtimes`; управляет возможностью копирования этих сборок в выходной каталог сборки</span><span class="sxs-lookup"><span data-stu-id="e8423-141">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="e8423-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="e8423-142">contentFiles</span></span> | <span data-ttu-id="e8423-143">Содержимое папки `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="e8423-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="e8423-144">выполнить сборку</span><span class="sxs-lookup"><span data-stu-id="e8423-144">build</span></span> | <span data-ttu-id="e8423-145">Свойства и цели в папке `build`</span><span class="sxs-lookup"><span data-stu-id="e8423-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="e8423-146">analyzers</span><span class="sxs-lookup"><span data-stu-id="e8423-146">analyzers</span></span> | <span data-ttu-id="e8423-147">Анализаторы .NET</span><span class="sxs-lookup"><span data-stu-id="e8423-147">.NET analyzers</span></span> |
| <span data-ttu-id="e8423-148">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="e8423-148">native</span></span> | <span data-ttu-id="e8423-149">Содержимое папки `native`</span><span class="sxs-lookup"><span data-stu-id="e8423-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="e8423-150">Нет</span><span class="sxs-lookup"><span data-stu-id="e8423-150">none</span></span> | <span data-ttu-id="e8423-151">Никакие из перечисленных выше ресурсов не используются.</span><span class="sxs-lookup"><span data-stu-id="e8423-151">None of the above are used.</span></span> |
| <span data-ttu-id="e8423-152">все</span><span class="sxs-lookup"><span data-stu-id="e8423-152">all</span></span> | <span data-ttu-id="e8423-153">Используются все перечисленные выше ресурсы (кроме `none`).</span><span class="sxs-lookup"><span data-stu-id="e8423-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="e8423-154">В приведенном ниже примере проектом используются все ресурсы, кроме файлов содержимого из пакета, и в родительский проект передаются все ресурсы, кроме файлов содержимого и анализаторов.</span><span class="sxs-lookup"><span data-stu-id="e8423-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="e8423-155">Обратите внимание: так как папка `build` не включена в `PrivateAssets`, цели и свойства *будут* передаваться в родительский проект.</span><span class="sxs-lookup"><span data-stu-id="e8423-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="e8423-156">Предположим, что приведенная выше ссылка используется в проекте, в рамках которого выполняется сборка пакета NuGet с именем AppLogger.</span><span class="sxs-lookup"><span data-stu-id="e8423-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="e8423-157">Пакет AppLogger может использовать цели и свойства из `Contoso.Utility.UsefulStuff`, так же как и проекты, использующие AppLogger.</span><span class="sxs-lookup"><span data-stu-id="e8423-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="e8423-158">Добавление условия PackageReference</span><span class="sxs-lookup"><span data-stu-id="e8423-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="e8423-159">С помощью условий можно управлять тем, когда следует включать пакет. В условиях можно использовать любые переменные MSBuild или переменные, определенные в файлах целей или свойств.</span><span class="sxs-lookup"><span data-stu-id="e8423-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="e8423-160">Однако в настоящее время поддерживается только переменная `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="e8423-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="e8423-161">Например, предположим, что целевыми платформами являются `netstandard1.4` и `net452`, но зависимость применима только для `net452`.</span><span class="sxs-lookup"><span data-stu-id="e8423-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="e8423-162">В этом случае в проект `netstandard1.4`, который использует пакет, не следует добавлять эту ненужную зависимость.</span><span class="sxs-lookup"><span data-stu-id="e8423-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="e8423-163">В этом случае в узле `PackageReference` можно указать следующее условие:</span><span class="sxs-lookup"><span data-stu-id="e8423-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="e8423-164">В пакет, сборка которого выполнена с помощью этого проекта, файл Newtonsoft.json будет включен в качестве зависимости только для целевой платформы `net452`.</span><span class="sxs-lookup"><span data-stu-id="e8423-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Результат применения условия к PackageReference в Visual Studio 2017](media/PackageReference-Condition.png)

<span data-ttu-id="e8423-166">Условия можно также применять на уровне `ItemGroup`. В этом случае они применяются ко всем дочерним элементам `PackageReference`.</span><span class="sxs-lookup"><span data-stu-id="e8423-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
