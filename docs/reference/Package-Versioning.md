---
title: Ссылка на версию пакета NuGet
description: Точные сведения об указании номеров версий и диапазонов для других пакетов, от которых зависит пакет NuGet, и о том, как устанавливаются зависимости.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/14/2019
ms.locfileid: "69019996"
---
# <a name="package-versioning"></a><span data-ttu-id="6ca14-103">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="6ca14-103">Package versioning</span></span>

<span data-ttu-id="6ca14-104">Конкретный пакет всегда называется идентификатором пакета и точным номером версии.</span><span class="sxs-lookup"><span data-stu-id="6ca14-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="6ca14-105">Например, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) в NuGet.org содержит несколько десятков отдельных пакетов, от версии *4.1.10311* до версии *6.1.3* (последний стабильный выпуск) и различных предварительных версий, таких как *6.2.0-Beta1.* .</span><span class="sxs-lookup"><span data-stu-id="6ca14-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="6ca14-106">При создании пакета вы назначаете определенный номер версии с помощью необязательного текстового суффикса предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="6ca14-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="6ca14-107">При использовании пакетов, с другой стороны, можно указать либо точный номер версии, либо диапазон допустимых версий.</span><span class="sxs-lookup"><span data-stu-id="6ca14-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="6ca14-108">В этом разделе.</span><span class="sxs-lookup"><span data-stu-id="6ca14-108">In this topic:</span></span>

- <span data-ttu-id="6ca14-109">[Основы версии](#version-basics) , включая суффиксы предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="6ca14-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="6ca14-110">Диапазоны версий и подстановочные знаки</span><span class="sxs-lookup"><span data-stu-id="6ca14-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="6ca14-111">Нормализованные номера версий</span><span class="sxs-lookup"><span data-stu-id="6ca14-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="6ca14-112">Основные сведения о версии</span><span class="sxs-lookup"><span data-stu-id="6ca14-112">Version basics</span></span>

<span data-ttu-id="6ca14-113">Конкретный номер версии указан в формате *основной. дополнительный. patch [-суффикс]* , где компоненты имеют следующие значения:</span><span class="sxs-lookup"><span data-stu-id="6ca14-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="6ca14-114">*Основной*: Критические изменения</span><span class="sxs-lookup"><span data-stu-id="6ca14-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="6ca14-115">*Дополнительный номер*: новые функции; сохраняется обратная совместимость;</span><span class="sxs-lookup"><span data-stu-id="6ca14-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="6ca14-116">*Исправление*: исправления ошибок; сохраняется обратная совместимость.</span><span class="sxs-lookup"><span data-stu-id="6ca14-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="6ca14-117">*-Суффикс* (необязательно): дефис, за которым следует строка, обозначающая предварительную версию (следуя [правилам семантического управления версиями или SemVer 1,0](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="6ca14-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="6ca14-118">**Примеров**</span><span class="sxs-lookup"><span data-stu-id="6ca14-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="6ca14-119">nuget.org отклоняет передачу пакетов, в которой отсутствует точный номер версии.</span><span class="sxs-lookup"><span data-stu-id="6ca14-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="6ca14-120">Версия должна быть указана в `.nuspec` файле проекта или, который используется для создания пакета.</span><span class="sxs-lookup"><span data-stu-id="6ca14-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="6ca14-121">Предварительные версии</span><span class="sxs-lookup"><span data-stu-id="6ca14-121">Pre-release versions</span></span>

<span data-ttu-id="6ca14-122">Технически говоря, создатели пакетов могут использовать любую строку в качестве суффикса, чтобы обозначить предварительную версию, так как NuGet рассматривает любую такую версию как предварительную и не делает других интерпретаций.</span><span class="sxs-lookup"><span data-stu-id="6ca14-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="6ca14-123">Это значит, что NuGet отображает полную строку версии в любом используемом пользовательском интерфейсе, в результате чего любая интерпретация значения суффикса для потребителя.</span><span class="sxs-lookup"><span data-stu-id="6ca14-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="6ca14-124">С другой стороны, разработчики пакетов обычно следуют признанным соглашениям об именовании:</span><span class="sxs-lookup"><span data-stu-id="6ca14-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="6ca14-125">`-alpha`: Альфа-выпуск, обычно используемый для выполнения и экспериментирования.</span><span class="sxs-lookup"><span data-stu-id="6ca14-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="6ca14-126">`-beta`: бета-версия, которая обычно содержит полный набор функций для следующего запланированного выпуска, но может иметь известные ошибки;</span><span class="sxs-lookup"><span data-stu-id="6ca14-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="6ca14-127">`-rc`: версия-кандидат, которая обычно может служить итоговой (стабильной), если не будут выявлены серьезные ошибки.</span><span class="sxs-lookup"><span data-stu-id="6ca14-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="6ca14-128">NuGet 4.3.0 + поддерживает [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), который поддерживает номера предварительных версий с точечной нотацией, как в *1.0.1-Build. 23*.</span><span class="sxs-lookup"><span data-stu-id="6ca14-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="6ca14-129">В версиях NuGet, предшествующих 4.3.0, точечная нотация не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="6ca14-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="6ca14-130">Можно использовать форму, например *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="6ca14-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="6ca14-131">При разрешении ссылок на пакеты и нескольких версий пакетов по суффиксу NuGet выбирает версию без суффикса, а затем применяет приоритет к предварительным версиям в обратный алфавитный порядок.</span><span class="sxs-lookup"><span data-stu-id="6ca14-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="6ca14-132">Например, следующие версии будут выбраны в указанном порядке:</span><span class="sxs-lookup"><span data-stu-id="6ca14-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="6ca14-133">2\.0.0 семантического управления версиями</span><span class="sxs-lookup"><span data-stu-id="6ca14-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="6ca14-134">С помощью NuGet 4.3.0 + и Visual Studio 2017 версии 15.3 + NuGet поддерживает [семантическую версию 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="6ca14-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="6ca14-135">Определенная семантика SemVer v 2.0.0 не поддерживается в старых клиентах.</span><span class="sxs-lookup"><span data-stu-id="6ca14-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="6ca14-136">NuGet считает версию пакета SemVer v 2.0.0 конкретной, если выполняется одно из следующих условий:</span><span class="sxs-lookup"><span data-stu-id="6ca14-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="6ca14-137">Метка предварительного выпуска отделяется точкой с запятой, например *1.0.0-Alpha. 1*</span><span class="sxs-lookup"><span data-stu-id="6ca14-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="6ca14-138">Версия содержит метаданные сборки, например *1.0.0 + гисаш*</span><span class="sxs-lookup"><span data-stu-id="6ca14-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="6ca14-139">Для nuget.org пакет определяется как пакет SemVer v, если выполняется одно из следующих условий.</span><span class="sxs-lookup"><span data-stu-id="6ca14-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="6ca14-140">Собственная версия пакета — SemVer v 2.0.0 соответствует требованиям, но не совместим с SemVer v 1.0.0, как определено выше.</span><span class="sxs-lookup"><span data-stu-id="6ca14-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="6ca14-141">Любой из диапазонов версий зависимостей пакета имеет минимальную или максимальную версию, совместимую с SemVer v 2.0.0, но не совместимую с SemVer v 1.0.0, определенную выше. Например, *[1.0.0-Alpha. 1,)* .</span><span class="sxs-lookup"><span data-stu-id="6ca14-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="6ca14-142">При передаче пакета SemVer v 2.0.0 в nuget.org пакет невидим для старых клиентов и доступен только следующим клиентам NuGet:</span><span class="sxs-lookup"><span data-stu-id="6ca14-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="6ca14-143">NuGet 4.3.0 +</span><span class="sxs-lookup"><span data-stu-id="6ca14-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="6ca14-144">Visual Studio 2017 версии 15.3 +</span><span class="sxs-lookup"><span data-stu-id="6ca14-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="6ca14-145">Visual Studio 2015 с [NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="6ca14-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="6ca14-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="6ca14-146">dotnet</span></span>
  - <span data-ttu-id="6ca14-147">Команда dotnetcore. exe (пакет SDK для .NET 2.0.0 +)</span><span class="sxs-lookup"><span data-stu-id="6ca14-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="6ca14-148">Сторонние клиенты:</span><span class="sxs-lookup"><span data-stu-id="6ca14-148">Third-party clients:</span></span>

- <span data-ttu-id="6ca14-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="6ca14-149">JetBrains Rider</span></span>
- <span data-ttu-id="6ca14-150">Пакет версии 5.0 +</span><span class="sxs-lookup"><span data-stu-id="6ca14-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="6ca14-151">Диапазоны версий и подстановочные знаки</span><span class="sxs-lookup"><span data-stu-id="6ca14-151">Version ranges and wildcards</span></span>

<span data-ttu-id="6ca14-152">При ссылке на зависимости пакетов NuGet поддерживает использование нотации интервала для указания диапазонов версий, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="6ca14-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="6ca14-153">Notation</span><span class="sxs-lookup"><span data-stu-id="6ca14-153">Notation</span></span> | <span data-ttu-id="6ca14-154">Примененное правило</span><span class="sxs-lookup"><span data-stu-id="6ca14-154">Applied rule</span></span> | <span data-ttu-id="6ca14-155">Описание</span><span class="sxs-lookup"><span data-stu-id="6ca14-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="6ca14-156">1.0</span><span class="sxs-lookup"><span data-stu-id="6ca14-156">1.0</span></span> | <span data-ttu-id="6ca14-157">x ≥ 1,0</span><span class="sxs-lookup"><span data-stu-id="6ca14-157">x ≥ 1.0</span></span> | <span data-ttu-id="6ca14-158">Минимальная версия, включительно</span><span class="sxs-lookup"><span data-stu-id="6ca14-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="6ca14-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="6ca14-159">(1.0,)</span></span> | <span data-ttu-id="6ca14-160">x > 1,0</span><span class="sxs-lookup"><span data-stu-id="6ca14-160">x > 1.0</span></span> | <span data-ttu-id="6ca14-161">Минимальная версия, монопольная</span><span class="sxs-lookup"><span data-stu-id="6ca14-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="6ca14-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="6ca14-162">[1.0]</span></span> | <span data-ttu-id="6ca14-163">x = = 1,0</span><span class="sxs-lookup"><span data-stu-id="6ca14-163">x == 1.0</span></span> | <span data-ttu-id="6ca14-164">Точное соответствие версии</span><span class="sxs-lookup"><span data-stu-id="6ca14-164">Exact version match</span></span> |
| <span data-ttu-id="6ca14-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="6ca14-165">(,1.0]</span></span> | <span data-ttu-id="6ca14-166">x ≤ 1,0</span><span class="sxs-lookup"><span data-stu-id="6ca14-166">x ≤ 1.0</span></span> | <span data-ttu-id="6ca14-167">Максимальная версия, включительно</span><span class="sxs-lookup"><span data-stu-id="6ca14-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="6ca14-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="6ca14-168">(,1.0)</span></span> | <span data-ttu-id="6ca14-169">x < 1,0</span><span class="sxs-lookup"><span data-stu-id="6ca14-169">x < 1.0</span></span> | <span data-ttu-id="6ca14-170">Максимальная версия, монопольная</span><span class="sxs-lookup"><span data-stu-id="6ca14-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="6ca14-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="6ca14-171">[1.0,2.0]</span></span> | <span data-ttu-id="6ca14-172">1,0 ≤ x ≤ 2,0</span><span class="sxs-lookup"><span data-stu-id="6ca14-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="6ca14-173">Точный диапазон, включительно</span><span class="sxs-lookup"><span data-stu-id="6ca14-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="6ca14-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="6ca14-174">(1.0,2.0)</span></span> | <span data-ttu-id="6ca14-175">1,0 < x < 2,0</span><span class="sxs-lookup"><span data-stu-id="6ca14-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="6ca14-176">Точный диапазон, исключающий</span><span class="sxs-lookup"><span data-stu-id="6ca14-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="6ca14-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="6ca14-177">[1.0,2.0)</span></span> | <span data-ttu-id="6ca14-178">1,0 ≤ x < 2,0</span><span class="sxs-lookup"><span data-stu-id="6ca14-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="6ca14-179">Смешанная включающая минимальная и эксклюзивная Максимальная версия</span><span class="sxs-lookup"><span data-stu-id="6ca14-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="6ca14-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="6ca14-180">(1.0)</span></span>    | <span data-ttu-id="6ca14-181">недействительные</span><span class="sxs-lookup"><span data-stu-id="6ca14-181">invalid</span></span> | <span data-ttu-id="6ca14-182">недействительные</span><span class="sxs-lookup"><span data-stu-id="6ca14-182">invalid</span></span> |

<span data-ttu-id="6ca14-183">При использовании формата PackageReference NuGet также поддерживает использование нотации \*с подстановочными знаками, для основных, дополнительных, исправлений и предварительных версий суффиксов номера.</span><span class="sxs-lookup"><span data-stu-id="6ca14-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="6ca14-184">Подстановочные знаки не поддерживаются `packages.config` в формате.</span><span class="sxs-lookup"><span data-stu-id="6ca14-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="6ca14-185">Диапазоны версий в PackageReference включают предварительные версии.</span><span class="sxs-lookup"><span data-stu-id="6ca14-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="6ca14-186">В режиме с плавающей версией не разрешаются предварительные версии, кроме случая, когда они участвуют в.</span><span class="sxs-lookup"><span data-stu-id="6ca14-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="6ca14-187">Сведения о состоянии соответствующего запроса функции см. в описании [проблемы 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="6ca14-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="6ca14-188">Примеры</span><span class="sxs-lookup"><span data-stu-id="6ca14-188">Examples</span></span>

<span data-ttu-id="6ca14-189">Всегда указывайте версию или диапазон версий для зависимостей пакетов в файлах проекта, `packages.config` файлах и `.nuspec` файлах.</span><span class="sxs-lookup"><span data-stu-id="6ca14-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="6ca14-190">Без версии или диапазона версий, NuGet 2.8. x и более ранних версий выбирает последнюю доступную версию пакета при разрешении зависимости, тогда как NuGet 3. x и более поздних версий выбирает наименьшую версию пакета.</span><span class="sxs-lookup"><span data-stu-id="6ca14-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="6ca14-191">Указание версии или диапазона версий позволяет избежать этой неопределенности.</span><span class="sxs-lookup"><span data-stu-id="6ca14-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="6ca14-192">Ссылки в файлах проекта (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="6ca14-192">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="6ca14-193">**Ссылки в `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="6ca14-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="6ca14-194">В `packages.config`каждой зависимости указывается точный `version` атрибут, используемый при восстановлении пакетов.</span><span class="sxs-lookup"><span data-stu-id="6ca14-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="6ca14-195">`allowedVersions` Атрибут используется только во время операций обновления, чтобы ограничить версии, в которые может быть обновлен пакет.</span><span class="sxs-lookup"><span data-stu-id="6ca14-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="6ca14-196">**Ссылки в `.nuspec` файлах**</span><span class="sxs-lookup"><span data-stu-id="6ca14-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="6ca14-197">`version` Атрибут`<dependency>` в элементе описывает версии диапазона, допустимые для зависимости.</span><span class="sxs-lookup"><span data-stu-id="6ca14-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="6ca14-198">Нормализованные номера версий</span><span class="sxs-lookup"><span data-stu-id="6ca14-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="6ca14-199">Это критическое изменение для NuGet 3,4 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="6ca14-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="6ca14-200">При получении пакетов из репозитория во время операций установки, переустановки или восстановления NuGet 3.4 + обрабатывает номера версий следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6ca14-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="6ca14-201">Начальные нули удаляются из номеров версий:</span><span class="sxs-lookup"><span data-stu-id="6ca14-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="6ca14-202">Ноль в четвертой части номера версии будет опущен.</span><span class="sxs-lookup"><span data-stu-id="6ca14-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="6ca14-203">`pack`и `restore` операции нормализации версий везде, где это возможно.</span><span class="sxs-lookup"><span data-stu-id="6ca14-203">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="6ca14-204">Для уже собранных пакетов эта нормализация не влияет на номера версий в самих пакетах. Он влияет только на то, как NuGet соответствует версиям при разрешении зависимостей.</span><span class="sxs-lookup"><span data-stu-id="6ca14-204">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="6ca14-205">Однако репозитории пакетов NuGet должны интерпретировать эти значения так же, как NuGet, чтобы предотвратить дублирование версий пакета.</span><span class="sxs-lookup"><span data-stu-id="6ca14-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="6ca14-206">Таким образом, репозиторий, содержащий пакет версии *1,0* , не должен размещать версию *1.0.0* как отдельный и другой пакет.</span><span class="sxs-lookup"><span data-stu-id="6ca14-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
