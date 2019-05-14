---
title: Предварительные версии в пакетах NuGet
description: Инструкции по созданию пакетов предварительных версий
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 696f51905198defdbfd475ba7d010ac3e27ac557
ms.sourcegitcommit: 3fc93f7a64be040699fe12125977dd25a7948470
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/29/2019
ms.locfileid: "64877940"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="ec01d-103">Сборка пакетов предварительных версий</span><span class="sxs-lookup"><span data-stu-id="ec01d-103">Building pre-release packages</span></span>

<span data-ttu-id="ec01d-104">При выпуске обновленного пакета с новым номером версии NuGet считает его "последней стабильной версией", что указывается, например, в пользовательском интерфейсе диспетчера пакетов в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ec01d-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Указание последней стабильной версии в пользовательском интерфейсе диспетчера пакетов](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="ec01d-106">Стабильная версия — это версия, которая считается достаточно надежной для использования в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ec01d-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="ec01d-107">Последняя стабильная версия также устанавливается в качестве обновления пакета или во время восстановления пакета (с учетом ограничений, которые описываются в разделе [Повторная установка и обновление пакетов](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="ec01d-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="ec01d-108">Для поддержки жизненного цикла выпуска программного обеспечения в NuGet 1.6 и более поздних версиях возможно распространение пакетов предварительных версий, номера версий которых включают в себя суффикс семантического версионирования, например `-alpha`, `-beta` или `-rc`.</span><span class="sxs-lookup"><span data-stu-id="ec01d-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="ec01d-109">Дополнительные сведения см. в разделе [Управление версиями пакета](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="ec01d-109">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="ec01d-110">Такие версии можно указывать тремя способами.</span><span class="sxs-lookup"><span data-stu-id="ec01d-110">You can specify such versions in three ways:</span></span>

- <span data-ttu-id="ec01d-111">Файл `.nuspec`: включите суффикс семантического версионирования в элемент `version`.</span><span class="sxs-lookup"><span data-stu-id="ec01d-111">`.nuspec` file: include the semantic version suffix in the `version` element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

- <span data-ttu-id="ec01d-112">Файл `.csproj`: включите суффикс семантического версионирования в элемент `PackageVersion`.</span><span class="sxs-lookup"><span data-stu-id="ec01d-112">`.csproj` file: include the semantic version suffix in the `PackageVersion` element:</span></span>

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- <span data-ttu-id="ec01d-113">Атрибуты сборки: укажите версию с помощью `AssemblyInformationalVersionAttribute`.</span><span class="sxs-lookup"><span data-stu-id="ec01d-113">Assembly attributes: specify the version using `AssemblyInformationalVersionAttribute`:</span></span>

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    <span data-ttu-id="ec01d-114">NuGet использует это значение вместо указанного в атрибуте `AssemblyVersion`, который не поддерживает семантическое версионирование.</span><span class="sxs-lookup"><span data-stu-id="ec01d-114">NuGet picks up this value instead of the one specified in the `AssemblyVersion` attribute, which does not support semantic versioning.</span></span>

<span data-ttu-id="ec01d-115">Когда вы будете готовы выпустить стабильную версию, просто удалите суффикс, и пакет будет иметь приоритет над любыми предварительными версиями.</span><span class="sxs-lookup"><span data-stu-id="ec01d-115">When you’re ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="ec01d-116">См. раздел [Управление версиями пакета](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="ec01d-116">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="ec01d-117">Установка и обновление пакетов предварительных версий</span><span class="sxs-lookup"><span data-stu-id="ec01d-117">Installing and updating pre-release packages</span></span>

<span data-ttu-id="ec01d-118">По умолчанию NuGet не включает предварительные версии при работе с пакетами, но это поведение можно изменить, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="ec01d-118">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="ec01d-119">**Пользовательский интерфейс диспетчера пакетов в Visual Studio**. В окне **Управление пакетами NuGet** установите флажок **Включить предварительные версии**.</span><span class="sxs-lookup"><span data-stu-id="ec01d-119">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Флажок "Включить предварительные версии" в Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="ec01d-121">При установке или снятии этого флажка список доступных версий, которые можно установить, в пользовательском интерфейсе диспетчера пакетов обновляется.</span><span class="sxs-lookup"><span data-stu-id="ec01d-121">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="ec01d-122">**Консоль диспетчера пакетов**. Используйте параметр `-IncludePrerelease` с командами `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` и `Update-Package`.</span><span class="sxs-lookup"><span data-stu-id="ec01d-122">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="ec01d-123">См. [справочник по PowerShell](../tools/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="ec01d-123">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="ec01d-124">**Интерфейс командной строки NuGet**. Используйте параметр `-prerelease` с командами `install`, `update`, `delete` и `mirror`.</span><span class="sxs-lookup"><span data-stu-id="ec01d-124">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="ec01d-125">См. [справочник по интерфейсу командной строки NuGet](../tools/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="ec01d-125">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="ec01d-126">Семантическое версионирование</span><span class="sxs-lookup"><span data-stu-id="ec01d-126">Semantic versioning</span></span>

<span data-ttu-id="ec01d-127">[Соглашение о семантическом версионировании (SemVer)](http://semver.org/spec/v1.0.0.html) описывает, как следует использовать строки в номерах версий для передачи назначения базового кода.</span><span class="sxs-lookup"><span data-stu-id="ec01d-127">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="ec01d-128">Согласно этому соглашению каждый номер версии состоит из трех частей (`Major.Minor.Patch`) со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="ec01d-128">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="ec01d-129">`Major`: Критические изменения</span><span class="sxs-lookup"><span data-stu-id="ec01d-129">`Major`: Breaking changes</span></span>
- <span data-ttu-id="ec01d-130">`Minor`: новые функции; сохраняется обратная совместимость;</span><span class="sxs-lookup"><span data-stu-id="ec01d-130">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="ec01d-131">`Patch`: исправления ошибок; сохраняется обратная совместимость.</span><span class="sxs-lookup"><span data-stu-id="ec01d-131">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="ec01d-132">Предварительные версии в этом случае обозначаются с помощью дефиса и строки, которые добавляются после номера исправления.</span><span class="sxs-lookup"><span data-stu-id="ec01d-132">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="ec01d-133">После дефиса можно использовать *любую* строку, чтобы пакет распознавался в NuGet как предварительная версия.</span><span class="sxs-lookup"><span data-stu-id="ec01d-133">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="ec01d-134">В этом случае NuGet выводит полный номер версии в соответствующем пользовательском интерфейсе, а интерпретировать его значение пользователям приходится самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="ec01d-134">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="ec01d-135">Учитывая это, желательно придерживаться общепринятых соглашений об именовании, например следующих:</span><span class="sxs-lookup"><span data-stu-id="ec01d-135">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="ec01d-136">`-alpha`: альфа-версия, обычно используемая для текущей работы и экспериментирования;</span><span class="sxs-lookup"><span data-stu-id="ec01d-136">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="ec01d-137">`-beta`: бета-версия, которая обычно содержит полный набор функций для следующего запланированного выпуска, но может иметь известные ошибки;</span><span class="sxs-lookup"><span data-stu-id="ec01d-137">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="ec01d-138">`-rc`: версия-кандидат, которая обычно может служить итоговой (стабильной), если не будут выявлены серьезные ошибки.</span><span class="sxs-lookup"><span data-stu-id="ec01d-138">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="ec01d-139">NuGet 4.3.0+ поддерживает [Семантическое версионирование версии 2.0.0](http://semver.org/spec/v2.0.0.html), которое позволяет использовать номера предварительных версий с точечной нотацией, как в случае `1.0.1-build.23`.</span><span class="sxs-lookup"><span data-stu-id="ec01d-139">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="ec01d-140">В версиях NuGet, предшествующих 4.3.0, точечная нотация не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="ec01d-140">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="ec01d-141">В предыдущих версиях NuGet можно было использовать формат наподобие `1.0.1-build23`, но такие номера всегда распознавались как номера предварительных версий.</span><span class="sxs-lookup"><span data-stu-id="ec01d-141">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="ec01d-142">Какие бы суффиксы ни использовались, в NuGet их приоритет определяется в обратном алфавитном порядке:</span><span class="sxs-lookup"><span data-stu-id="ec01d-142">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

<span data-ttu-id="ec01d-143">Из этого следует, что версия с номером без суффикса всегда будет иметь приоритет над предварительными версиями.</span><span class="sxs-lookup"><span data-stu-id="ec01d-143">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="ec01d-144">Кроме того, имейте в виду, что если в тегах предварительных версий используются числовые суффиксы из двух или более цифр, следует добавлять начальные нули, например beta01 или beta05. Это позволит обеспечить правильную сортировку номеров.</span><span class="sxs-lookup"><span data-stu-id="ec01d-144">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>
