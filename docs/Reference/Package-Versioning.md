---
title: "Пакет NuGet версии ссылку | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Точные сведения о задании номера версий и диапазонов для других пакетов, от которого зависит от пакета NuGet и установка зависимостей."
keywords: "Управление версиями, зависимости пакетов NuGet, версии зависимостей NuGet, номера версий NuGet, версия пакета NuGet, диапазон версий, версии спецификации, номера нормализованную версию"
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.openlocfilehash: 70472d7d97d073009237a047e0fdf528b221dfd0
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="package-versioning"></a><span data-ttu-id="b6694-104">Пакет управления версиями</span><span class="sxs-lookup"><span data-stu-id="b6694-104">Package versioning</span></span>

<span data-ttu-id="b6694-105">Конкретный пакет всегда называется его идентификатором пакета и точный номер версии.</span><span class="sxs-lookup"><span data-stu-id="b6694-105">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="b6694-106">Например [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org имеет несколько десятков определенные пакеты, доступные, начиная с версии *4.1.10311* до версии *6.1.3 размещается* (последняя стабильная выпуск) и широкий набор предварительных версий, например *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="b6694-106">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="b6694-107">При создании пакета, можно назначить определенный номер версии с суффиксом дополнительный текст предварительного выпуска.</span><span class="sxs-lookup"><span data-stu-id="b6694-107">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="b6694-108">При использовании пакетов, с другой стороны, можно указать точный номер версии или диапазон допустимых версий.</span><span class="sxs-lookup"><span data-stu-id="b6694-108">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="b6694-109">В этом разделе.</span><span class="sxs-lookup"><span data-stu-id="b6694-109">In this topic:</span></span>

- <span data-ttu-id="b6694-110">[Основные сведения о версии](#version-basics) включая суффиксы предварительного выпуска.</span><span class="sxs-lookup"><span data-stu-id="b6694-110">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="b6694-111">Диапазон версий и подстановочные знаки</span><span class="sxs-lookup"><span data-stu-id="b6694-111">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="b6694-112">Номера нормализованную версию</span><span class="sxs-lookup"><span data-stu-id="b6694-112">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="b6694-113">Основные сведения о версии</span><span class="sxs-lookup"><span data-stu-id="b6694-113">Version basics</span></span>

<span data-ttu-id="b6694-114">Определенный номер версии указывается в формате *основной.дополнительный.исправление [-суффикс]*, где компоненты имеют следующий смысл:</span><span class="sxs-lookup"><span data-stu-id="b6694-114">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="b6694-115">*Основные*: критические изменения</span><span class="sxs-lookup"><span data-stu-id="b6694-115">*Major*: Breaking changes</span></span>
- <span data-ttu-id="b6694-116">*Дополнительный номер*: новые возможности, но обратная совместимость</span><span class="sxs-lookup"><span data-stu-id="b6694-116">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="b6694-117">*Исправление для*: исправления ошибок, связанных в обратной совместимости</span><span class="sxs-lookup"><span data-stu-id="b6694-117">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="b6694-118">*-Суффикс* (необязательно): дефис следуют за строкой, указывающей на этапе предварительной версии (следующие [семантического управления версиями или SemVer 1.0 соглашение о](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="b6694-118">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="b6694-119">**Примеры:**</span><span class="sxs-lookup"><span data-stu-id="b6694-119">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="b6694-120">NuGet.org отклоняет все отправка пакета не обеспечивает точный номер версии.</span><span class="sxs-lookup"><span data-stu-id="b6694-120">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="b6694-121">Версия должна быть указана в `.nuspec` или файл проекта используется для создания пакета.</span><span class="sxs-lookup"><span data-stu-id="b6694-121">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="b6694-122">Предварительные версии</span><span class="sxs-lookup"><span data-stu-id="b6694-122">Pre-release versions</span></span>

<span data-ttu-id="b6694-123">Технической точки зрения автору пакета можно использовать любую строку как суффикс для обозначения предварительной версии, как NuGet считает любую версию такого предварительного выпуска и делает без других интерпретации.</span><span class="sxs-lookup"><span data-stu-id="b6694-123">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="b6694-124">То есть NuGet отображает полную версию строки в пользовательском Интерфейсе, независимо от участвует, оставляя Любая обработка значение суффикса потребителю.</span><span class="sxs-lookup"><span data-stu-id="b6694-124">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="b6694-125">С другой стороны, разработчики пакетов в целом следовать распознаваемым соглашения об именовании:</span><span class="sxs-lookup"><span data-stu-id="b6694-125">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="b6694-126">`-alpha`: Альфа-версии, как правило, используется для экспериментов и работы процесса.</span><span class="sxs-lookup"><span data-stu-id="b6694-126">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="b6694-127">`-beta`: бета-версия, которая обычно содержит полный набор функций для следующего запланированного выпуска, но может иметь известные ошибки;</span><span class="sxs-lookup"><span data-stu-id="b6694-127">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="b6694-128">`-rc`: версия-кандидат, которая обычно может служить итоговой (стабильной), если не будут выявлены серьезные ошибки.</span><span class="sxs-lookup"><span data-stu-id="b6694-128">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="b6694-129">Поддерживает NuGet 4.3.0+ [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), поддерживающей предварительного выпуска чисел с помощью точечной нотации, как в *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="b6694-129">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="b6694-130">Нотация с точками не поддерживается с версии NuGet до 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="b6694-130">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="b6694-131">Можно использовать в форме, как *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="b6694-131">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="b6694-132">При разрешении ссылки на пакет, а также несколько версий пакета отличаются только суффикс, NuGet сначала выбирает версии без суффикса, а затем применяется приоритет к предварительным версиям в обратном алфавитном порядке.</span><span class="sxs-lookup"><span data-stu-id="b6694-132">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="b6694-133">Например следующие версии будет выбрана в точной последовательности:</span><span class="sxs-lookup"><span data-stu-id="b6694-133">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="b6694-134">Семантического управления версиями 2.0.0</span><span class="sxs-lookup"><span data-stu-id="b6694-134">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="b6694-135">С помощью NuGet 4.3.0+ и версии 15,3 + 2017 г. Visual Studio, поддерживает NuGet [семантического управления версиями 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="b6694-135">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="b6694-136">Некоторые семантику SemVer v2.0.0 не поддерживаются в старых клиентах.</span><span class="sxs-lookup"><span data-stu-id="b6694-136">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="b6694-137">NuGet считает, что версия пакета для конкретного v2.0.0 SemVer при выполнении любого из следующих инструкций:</span><span class="sxs-lookup"><span data-stu-id="b6694-137">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="b6694-138">Метка предварительного выпуска разделенный точками, например, *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="b6694-138">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="b6694-139">Версия имеет сборки метаданных, например, *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="b6694-139">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="b6694-140">Nuget.org пакета определяется как пакет v2.0.0 SemVer при выполнении любого из следующих инструкций:</span><span class="sxs-lookup"><span data-stu-id="b6694-140">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="b6694-141">Версия пакета собственные — совместимые v2.0.0 SemVer, но не SemVer версии 1.0.0 соответствующим, как указано выше.</span><span class="sxs-lookup"><span data-stu-id="b6694-141">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="b6694-142">Любой диапазон версий пакета зависимостей имеет версию минимальное или максимальное значение, соответствующие v2.0.0 SemVer, но не SemVer версии 1.0.0 соответствующим, описанный выше; например *[1.0.0-alpha.1,)*.</span><span class="sxs-lookup"><span data-stu-id="b6694-142">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="b6694-143">При отправке пакета конкретного v2.0.0 SemVer в nuget.org пакет является невидимым для старых клиентов и доступны только к следующим клиентам NuGet:</span><span class="sxs-lookup"><span data-stu-id="b6694-143">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="b6694-144">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="b6694-144">NuGet 4.3.0+</span></span>
- <span data-ttu-id="b6694-145">Visual Studio 2017 г. версия 15,3 +</span><span class="sxs-lookup"><span data-stu-id="b6694-145">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="b6694-146">Visual Studio 2015 с [v3.6.0 NuGet VSIX](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="b6694-146">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="b6694-147">DotNet.exe (2.0.0+ .NET SDK)</span><span class="sxs-lookup"><span data-stu-id="b6694-147">dotnet.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="b6694-148">Сторонние клиенты:</span><span class="sxs-lookup"><span data-stu-id="b6694-148">Third-party clients:</span></span>

- <span data-ttu-id="b6694-149">Страхование JetBrains</span><span class="sxs-lookup"><span data-stu-id="b6694-149">JetBrains Rider</span></span>
- <span data-ttu-id="b6694-150">Paket версии 5.0 +</span><span class="sxs-lookup"><span data-stu-id="b6694-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="b6694-151">Диапазон версий и подстановочные знаки</span><span class="sxs-lookup"><span data-stu-id="b6694-151">Version ranges and wildcards</span></span>

<span data-ttu-id="b6694-152">Применительно к зависимости пакетов NuGet поддерживает нотации интервал для указания диапазонов версий, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b6694-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="b6694-153">Notation</span><span class="sxs-lookup"><span data-stu-id="b6694-153">Notation</span></span> | <span data-ttu-id="b6694-154">Примененное правило</span><span class="sxs-lookup"><span data-stu-id="b6694-154">Applied rule</span></span> | <span data-ttu-id="b6694-155">Описание:</span><span class="sxs-lookup"><span data-stu-id="b6694-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="b6694-156">1.0</span><span class="sxs-lookup"><span data-stu-id="b6694-156">1.0</span></span> | <span data-ttu-id="b6694-157">1.0 ≤ x</span><span class="sxs-lookup"><span data-stu-id="b6694-157">1.0 ≤ x</span></span> | <span data-ttu-id="b6694-158">Минимальная версия включительно</span><span class="sxs-lookup"><span data-stu-id="b6694-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="b6694-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="b6694-159">(1.0,)</span></span> | <span data-ttu-id="b6694-160">1.0 < x</span><span class="sxs-lookup"><span data-stu-id="b6694-160">1.0 < x</span></span> | <span data-ttu-id="b6694-161">Минимальная версия монопольного</span><span class="sxs-lookup"><span data-stu-id="b6694-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="b6694-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="b6694-162">[1.0]</span></span> | <span data-ttu-id="b6694-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="b6694-163">x == 1.0</span></span> | <span data-ttu-id="b6694-164">Точного сопоставления версии</span><span class="sxs-lookup"><span data-stu-id="b6694-164">Exact version match</span></span> |
| <span data-ttu-id="b6694-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="b6694-165">(,1.0]</span></span> | <span data-ttu-id="b6694-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="b6694-166">x ≤ 1.0</span></span> | <span data-ttu-id="b6694-167">Максимальная версия включительно</span><span class="sxs-lookup"><span data-stu-id="b6694-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="b6694-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="b6694-168">(,1.0)</span></span> | <span data-ttu-id="b6694-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="b6694-169">x < 1.0</span></span> | <span data-ttu-id="b6694-170">Максимальная версия монопольного</span><span class="sxs-lookup"><span data-stu-id="b6694-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="b6694-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="b6694-171">[1.0,2.0]</span></span> | <span data-ttu-id="b6694-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="b6694-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="b6694-173">Точный диапазон включительно</span><span class="sxs-lookup"><span data-stu-id="b6694-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="b6694-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="b6694-174">(1.0,2.0)</span></span> | <span data-ttu-id="b6694-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="b6694-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="b6694-176">Точное монопольного диапазона</span><span class="sxs-lookup"><span data-stu-id="b6694-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="b6694-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="b6694-177">[1.0,2.0)</span></span> | <span data-ttu-id="b6694-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="b6694-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="b6694-179">Смешанный включительно минимальное и эксклюзивных Максимальная версия</span><span class="sxs-lookup"><span data-stu-id="b6694-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="b6694-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="b6694-180">(1.0)</span></span>    | <span data-ttu-id="b6694-181">недействительные</span><span class="sxs-lookup"><span data-stu-id="b6694-181">invalid</span></span> | <span data-ttu-id="b6694-182">недействительные</span><span class="sxs-lookup"><span data-stu-id="b6694-182">invalid</span></span> |

<span data-ttu-id="b6694-183">При использовании формата PackageReference NuGet также поддерживает использование нотацию подстановочных знаков, \*основной, незначительное, исправление и частей предварительной версии суффикс числа.</span><span class="sxs-lookup"><span data-stu-id="b6694-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="b6694-184">Подстановочные знаки не поддерживаются с `packages.config` формат.</span><span class="sxs-lookup"><span data-stu-id="b6694-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="b6694-185">Предварительные версии, не включаются при разрешении диапазон версий.</span><span class="sxs-lookup"><span data-stu-id="b6694-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="b6694-186">Предварительные версии *,* включены при использовании подстановочного знака (\*).</span><span class="sxs-lookup"><span data-stu-id="b6694-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="b6694-187">Диапазон версий *[1.0,2.0]*, например, не включает бета-версии 2.0, но в нотацию подстановочных знаков _2.0-\*_ does.</span><span class="sxs-lookup"><span data-stu-id="b6694-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-\*_ does.</span></span> <span data-ttu-id="b6694-188">В разделе [выдачи 912](https://github.com/NuGet/Home/issues/912) Дополнительные сведения о предварительной версии подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="b6694-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="b6694-189">Примеры</span><span class="sxs-lookup"><span data-stu-id="b6694-189">Examples</span></span>

<span data-ttu-id="b6694-190">Всегда указывайте версию или диапазон версий для зависимости пакетов в файлах проектов `packages.config` файлы, и `.nuspec` файлов.</span><span class="sxs-lookup"><span data-stu-id="b6694-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="b6694-191">Без версии или диапазон версий, NuGet 2.8.x и более ранних версий выбирает последнюю версию пакета доступны при разрешении зависимостей, тогда как NuGet 3.x и более поздней версии выбирает самую раннюю версию пакета.</span><span class="sxs-lookup"><span data-stu-id="b6694-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="b6694-192">Указание версии и версии, что диапазон позволяет избежать этой неопределенности.</span><span class="sxs-lookup"><span data-stu-id="b6694-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="b6694-193">Ссылки в файлы проекта (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="b6694-193">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="b6694-194">**Ссылки в `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="b6694-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="b6694-195">В `packages.config`, каждая зависимость отмечены точного `version` атрибут, который используется при восстановлении пакетов.</span><span class="sxs-lookup"><span data-stu-id="b6694-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="b6694-196">`allowedVersions` Атрибут используется только во время операций обновления для ограничения версии, к которым могут быть обновлены пакета.</span><span class="sxs-lookup"><span data-stu-id="b6694-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

<span data-ttu-id="b6694-197">**Ссылки в `.nuspec` файлов**</span><span class="sxs-lookup"><span data-stu-id="b6694-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="b6694-198">`version` Атрибута в `<dependency>` элемент описывает диапазон версий, допустимые для зависимости.</span><span class="sxs-lookup"><span data-stu-id="b6694-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a><span data-ttu-id="b6694-199">Номера нормализованную версию</span><span class="sxs-lookup"><span data-stu-id="b6694-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="b6694-200">Это критическое изменение NuGet 3.4 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="b6694-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="b6694-201">После получения пакетов из репозитория во время установки, переустановки или восстановления, NuGet 3.4 + обрабатывает номера версий следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b6694-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="b6694-202">Начальные нули удаляются из номеров версий:</span><span class="sxs-lookup"><span data-stu-id="b6694-202">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="b6694-203">Ноль в четвертой части номера версии будет пропущен.</span><span class="sxs-lookup"><span data-stu-id="b6694-203">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="b6694-204">Эта нормализация не влияет на номера версий в пакеты отдельно. он действует как NuGet соответствует только версии при разрешении зависимостей.</span><span class="sxs-lookup"><span data-stu-id="b6694-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="b6694-205">Тем не менее репозитории NuGet пакет должен обрабатывать эти значения в так же, как NuGet во избежание дублирования версии пакета.</span><span class="sxs-lookup"><span data-stu-id="b6694-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="b6694-206">Таким образом, содержащий версию репозиторий *1.0* пакета не также размещают версии *1.0.0* как отдельное пакет.</span><span class="sxs-lookup"><span data-stu-id="b6694-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
