---
title: Ссылка на пакет NuGet версии
description: Точные сведения об указании номеров версий и диапазонов для других пакетов, от которых зависит пакет NuGet, и способ установки зависимостей.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6407cd2ea5e5e7a9c9e2be679764a8a0d5dd9260
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852472"
---
# <a name="package-versioning"></a><span data-ttu-id="40cef-103">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="40cef-103">Package versioning</span></span>

<span data-ttu-id="40cef-104">Конкретный пакет всегда называются с помощью его идентификатора пакета и точный номер версии.</span><span class="sxs-lookup"><span data-stu-id="40cef-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="40cef-105">Например [Entity Framework](https://www.nuget.org/packages/EntityFramework/) на сайте nuget.org имеет несколько десятков конкретных доступных пакетов, начиная с версии *4.1.10311* до версии *6.1.3* (последняя стабильная версия выпуск) и широкий набор предварительных версий, например *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="40cef-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="40cef-106">При создании пакета, можно назначить определенный номер версии с суффиксом дополнительный текст для предварительного выпуска.</span><span class="sxs-lookup"><span data-stu-id="40cef-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="40cef-107">При использовании пакетов, с другой стороны, можно указать точный номер версии или диапазон допустимых версий.</span><span class="sxs-lookup"><span data-stu-id="40cef-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="40cef-108">В этом разделе.</span><span class="sxs-lookup"><span data-stu-id="40cef-108">In this topic:</span></span>

- <span data-ttu-id="40cef-109">[Основные сведения о версии](#version-basics) включая суффиксы предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="40cef-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="40cef-110">Диапазон версий и подстановочные знаки</span><span class="sxs-lookup"><span data-stu-id="40cef-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="40cef-111">Номера нормализованную версию</span><span class="sxs-lookup"><span data-stu-id="40cef-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="40cef-112">Основные сведения о версии</span><span class="sxs-lookup"><span data-stu-id="40cef-112">Version basics</span></span>

<span data-ttu-id="40cef-113">Определенный номер версии указывается в формате *основной_номер.дополнительный_номер.исправление [-суффикс]*, где компоненты имеют следующий смысл:</span><span class="sxs-lookup"><span data-stu-id="40cef-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="40cef-114">*Основные*: Критические изменения</span><span class="sxs-lookup"><span data-stu-id="40cef-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="40cef-115">*Дополнительный номер*: новые функции; сохраняется обратная совместимость;</span><span class="sxs-lookup"><span data-stu-id="40cef-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="40cef-116">*Исправление*: исправления ошибок; сохраняется обратная совместимость.</span><span class="sxs-lookup"><span data-stu-id="40cef-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="40cef-117">*-Суффикс* (необязательно): дефиса и строки в предварительной версии, обозначающая (ниже [семантического управления версиями или SemVer 1.0 соглашение](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="40cef-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="40cef-118">**Примеры:**</span><span class="sxs-lookup"><span data-stu-id="40cef-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="40cef-119">NuGet.org отклоняет любые отправить пакет, который не имеет точный номер версии.</span><span class="sxs-lookup"><span data-stu-id="40cef-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="40cef-120">Должна быть указана версия в `.nuspec` или файл проекта, используемый для создания пакета.</span><span class="sxs-lookup"><span data-stu-id="40cef-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="40cef-121">Предварительные версии</span><span class="sxs-lookup"><span data-stu-id="40cef-121">Pre-release versions</span></span>

<span data-ttu-id="40cef-122">Говоря техническим языком, создатели пакета можно использовать любую строку как суффикс для обозначения предварительной версии, поскольку NuGet считает любой такой версии предварительной версии и делает без других интерпретации.</span><span class="sxs-lookup"><span data-stu-id="40cef-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="40cef-123">Т. е участвует полной версии строки в любой пользовательский Интерфейс отображает NuGet, оставив Любая обработка значение суффикса объекту-получателю.</span><span class="sxs-lookup"><span data-stu-id="40cef-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="40cef-124">С другой стороны, разработчики пакетов соблюдаться общепринятых соглашений об именовании:</span><span class="sxs-lookup"><span data-stu-id="40cef-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="40cef-125">`-alpha`: Альфа-версии, обычно используемых для ветви стадии и экспериментов.</span><span class="sxs-lookup"><span data-stu-id="40cef-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="40cef-126">`-beta`: бета-версия, которая обычно содержит полный набор функций для следующего запланированного выпуска, но может иметь известные ошибки;</span><span class="sxs-lookup"><span data-stu-id="40cef-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="40cef-127">`-rc`: версия-кандидат, которая обычно может служить итоговой (стабильной), если не будут выявлены серьезные ошибки.</span><span class="sxs-lookup"><span data-stu-id="40cef-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="40cef-128">NuGet 4.3.0+ поддерживает [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), который поддерживает номера предварительных с точечной нотацией, как показано на *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="40cef-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="40cef-129">В версиях NuGet, предшествующих 4.3.0, точечная нотация не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="40cef-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="40cef-130">Можно использовать формат наподобие *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="40cef-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="40cef-131">При разрешении ссылок на пакеты, а также несколько версий пакета отличаются только суффиксами, NuGet сначала выбирает версии без суффикса, а затем применяется приоритет к предварительным версиям в обратном алфавитном порядке.</span><span class="sxs-lookup"><span data-stu-id="40cef-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="40cef-132">Например следующие версии будет выбрана в точной последовательности:</span><span class="sxs-lookup"><span data-stu-id="40cef-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="40cef-133">Семантического Версионирования 2.0.0</span><span class="sxs-lookup"><span data-stu-id="40cef-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="40cef-134">NuGet 4.3.0+ и Visual Studio 2017 версии 15.3 и более поздних, NuGet поддерживает [семантического Версионирования 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="40cef-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="40cef-135">Определенные семантики версии SemVer 2.0.0 не поддерживаются в старых клиентов.</span><span class="sxs-lookup"><span data-stu-id="40cef-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="40cef-136">NuGet считает, что версия пакета, чтобы быть определенной v2.0.0 SemVer, если выполняется любое из следующих инструкций:</span><span class="sxs-lookup"><span data-stu-id="40cef-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="40cef-137">Метка предварительной версии разделенные точками, например, *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="40cef-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="40cef-138">Версия имеет метаданных для построения, например, *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="40cef-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="40cef-139">Для nuget.org пакета определяется как пакет SemVer версии 2.0.0, если выполняется любое из следующих инструкций:</span><span class="sxs-lookup"><span data-stu-id="40cef-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="40cef-140">Собственные версия пакета является совместимым v2.0.0 SemVer, но не о версиях SemVer 1.0.0 соответствует требованиям, как указано выше.</span><span class="sxs-lookup"><span data-stu-id="40cef-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="40cef-141">Какой-либо из диапазонов версий пакета зависимостей имеет минимальную или максимальную версию, которая является совместимым v2.0.0 SemVer, но не о версиях SemVer 1.0.0 соответствует требованиям, определенным выше; например *[1.0.0-alpha.1,)*.</span><span class="sxs-lookup"><span data-stu-id="40cef-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="40cef-142">Если вы отправляете SemVer версии 2.0.0 пакет на сайте nuget.org, пакет невидимым для старых клиентов и доступны только следующих клиентов NuGet:</span><span class="sxs-lookup"><span data-stu-id="40cef-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="40cef-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="40cef-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="40cef-144">Visual Studio 2017 версии 15.3 и более поздних</span><span class="sxs-lookup"><span data-stu-id="40cef-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="40cef-145">Visual Studio 2015 с [v3.6.0 NuGet VSIX](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="40cef-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="40cef-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="40cef-146">dotnet</span></span>
  - <span data-ttu-id="40cef-147">dotnetcore.exe (2.0.0+ пакета SDK для .NET)</span><span class="sxs-lookup"><span data-stu-id="40cef-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="40cef-148">Сторонние клиенты:</span><span class="sxs-lookup"><span data-stu-id="40cef-148">Third-party clients:</span></span>

- <span data-ttu-id="40cef-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="40cef-149">JetBrains Rider</span></span>
- <span data-ttu-id="40cef-150">Paket 5.0 и более поздних версиях</span><span class="sxs-lookup"><span data-stu-id="40cef-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="40cef-151">Диапазон версий и подстановочные знаки</span><span class="sxs-lookup"><span data-stu-id="40cef-151">Version ranges and wildcards</span></span>

<span data-ttu-id="40cef-152">Применительно к зависимости пакетов NuGet поддерживает, используя интервал для указания диапазонов версий, выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="40cef-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="40cef-153">Notation</span><span class="sxs-lookup"><span data-stu-id="40cef-153">Notation</span></span> | <span data-ttu-id="40cef-154">Примененное правило</span><span class="sxs-lookup"><span data-stu-id="40cef-154">Applied rule</span></span> | <span data-ttu-id="40cef-155">Описание:</span><span class="sxs-lookup"><span data-stu-id="40cef-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="40cef-156">1.0</span><span class="sxs-lookup"><span data-stu-id="40cef-156">1.0</span></span> | <span data-ttu-id="40cef-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="40cef-157">x ≥ 1.0</span></span> | <span data-ttu-id="40cef-158">Минимальная версия, включительно</span><span class="sxs-lookup"><span data-stu-id="40cef-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="40cef-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="40cef-159">(1.0,)</span></span> | <span data-ttu-id="40cef-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="40cef-160">x > 1.0</span></span> | <span data-ttu-id="40cef-161">Минимальная версия, эксклюзивные</span><span class="sxs-lookup"><span data-stu-id="40cef-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="40cef-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="40cef-162">[1.0]</span></span> | <span data-ttu-id="40cef-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="40cef-163">x == 1.0</span></span> | <span data-ttu-id="40cef-164">Точное соответствие версии</span><span class="sxs-lookup"><span data-stu-id="40cef-164">Exact version match</span></span> |
| <span data-ttu-id="40cef-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="40cef-165">(,1.0]</span></span> | <span data-ttu-id="40cef-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="40cef-166">x ≤ 1.0</span></span> | <span data-ttu-id="40cef-167">Максимальная версия включительно</span><span class="sxs-lookup"><span data-stu-id="40cef-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="40cef-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="40cef-168">(,1.0)</span></span> | <span data-ttu-id="40cef-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="40cef-169">x < 1.0</span></span> | <span data-ttu-id="40cef-170">Максимальная версия монопольного</span><span class="sxs-lookup"><span data-stu-id="40cef-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="40cef-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="40cef-171">[1.0,2.0]</span></span> | <span data-ttu-id="40cef-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="40cef-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="40cef-173">Точный диапазон, включительно</span><span class="sxs-lookup"><span data-stu-id="40cef-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="40cef-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="40cef-174">(1.0,2.0)</span></span> | <span data-ttu-id="40cef-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="40cef-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="40cef-176">Точное монопольного диапазона</span><span class="sxs-lookup"><span data-stu-id="40cef-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="40cef-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="40cef-177">[1.0,2.0)</span></span> | <span data-ttu-id="40cef-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="40cef-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="40cef-179">Смешанный включительно минимальное и исключающие Максимальная версия</span><span class="sxs-lookup"><span data-stu-id="40cef-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="40cef-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="40cef-180">(1.0)</span></span>    | <span data-ttu-id="40cef-181">недействительные</span><span class="sxs-lookup"><span data-stu-id="40cef-181">invalid</span></span> | <span data-ttu-id="40cef-182">недействительные</span><span class="sxs-lookup"><span data-stu-id="40cef-182">invalid</span></span> |

<span data-ttu-id="40cef-183">При использовании формата PackageReference, NuGet также поддерживает использование в нотацию подстановочных знаков \*, для основной, версии, исправления и суффикс предварительной версии части числа.</span><span class="sxs-lookup"><span data-stu-id="40cef-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="40cef-184">Подстановочные знаки не поддерживаются с `packages.config` формат.</span><span class="sxs-lookup"><span data-stu-id="40cef-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="40cef-185">Предварительные версии не включаются при разрешении диапазон версий.</span><span class="sxs-lookup"><span data-stu-id="40cef-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="40cef-186">Предварительные версии *являются* включены при использовании подстановочного знака (\*).</span><span class="sxs-lookup"><span data-stu-id="40cef-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="40cef-187">Диапазон версий *[1.0,2.0]*, например, не поддерживает бета-версии 2.0, но в нотацию подстановочных знаков _2.0-\*_ does.</span><span class="sxs-lookup"><span data-stu-id="40cef-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-\*_ does.</span></span> <span data-ttu-id="40cef-188">См. в разделе [выдавать 912](https://github.com/NuGet/Home/issues/912) Дополнительные сведения о подстановочных знаках предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="40cef-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="40cef-189">Примеры</span><span class="sxs-lookup"><span data-stu-id="40cef-189">Examples</span></span>

<span data-ttu-id="40cef-190">Всегда указывайте версию или диапазон версий для зависимости пакетов в файлах проекта, `packages.config` файлы, и `.nuspec` файлы.</span><span class="sxs-lookup"><span data-stu-id="40cef-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="40cef-191">Без версию или диапазон версий, NuGet 2.8.x и ранее выбирает последнюю версию пакета, доступные при разрешении зависимостей, тогда как NuGet 3.x и более поздней версии выбирает самую раннюю версию пакета.</span><span class="sxs-lookup"><span data-stu-id="40cef-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="40cef-192">Указание версии или версии, что диапазон позволяет избежать этой неопределенностью.</span><span class="sxs-lookup"><span data-stu-id="40cef-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="40cef-193">Ссылки в файлах проекта (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="40cef-193">References in project files (PackageReference)</span></span>

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
```

<span data-ttu-id="40cef-194">**Ссылки в `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="40cef-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="40cef-195">В `packages.config`, каждая зависимость отмечены точного `version` атрибут, используемый при восстановлении пакетов.</span><span class="sxs-lookup"><span data-stu-id="40cef-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="40cef-196">`allowedVersions` Атрибут используется только во время операций обновления для ограничения версий, к которым могут быть обновлены пакета.</span><span class="sxs-lookup"><span data-stu-id="40cef-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="40cef-197">**Ссылки в `.nuspec` файлов**</span><span class="sxs-lookup"><span data-stu-id="40cef-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="40cef-198">`version` Атрибут в `<dependency>` элемент описывает диапазон версий, которые являются допустимыми для зависимости.</span><span class="sxs-lookup"><span data-stu-id="40cef-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="40cef-199">Номера нормализованную версию</span><span class="sxs-lookup"><span data-stu-id="40cef-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="40cef-200">Это критическое изменение NuGet 3.4 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="40cef-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="40cef-201">После получения пакетов из репозитория во время установки, переустановки или восстановления NuGet 3.4 и более поздних обрабатывает номера версий следующим образом:</span><span class="sxs-lookup"><span data-stu-id="40cef-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="40cef-202">Начальные нули удаляются из номера версий:</span><span class="sxs-lookup"><span data-stu-id="40cef-202">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="40cef-203">Ноль в четвертой части номера версии будет пропущено</span><span class="sxs-lookup"><span data-stu-id="40cef-203">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="40cef-204">Эта нормализация не влияет на номера версий в пакетах отдельно. он затрагивает только, как NuGet соответствует версии при разрешении зависимостей.</span><span class="sxs-lookup"><span data-stu-id="40cef-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="40cef-205">Тем не менее репозиториями пакетов NuGet должен обрабатывать эти значения в так же, как NuGet во избежание дублирования версии пакета.</span><span class="sxs-lookup"><span data-stu-id="40cef-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="40cef-206">Таким образом репозиторий, который содержит версию *1.0* пакета не должно также включать версии *1.0.0* как пакет и отличается.</span><span class="sxs-lookup"><span data-stu-id="40cef-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
