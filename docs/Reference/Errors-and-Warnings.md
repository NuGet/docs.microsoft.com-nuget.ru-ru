---
title: "Восстановление NuGet предупреждения Справочник по ошибкам и | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Полный справочник для предупреждения и ошибки, выданные NuGet во время восстановления пакета"
keywords: "NuGet ошибки, предупреждения NuGet диагностики"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
ms.openlocfilehash: c7d77af04744888ce8af92d617a2ffc7daef4eb0
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="91af6-104">Ошибки и предупреждения</span><span class="sxs-lookup"><span data-stu-id="91af6-104">Errors and warnings</span></span>

<span data-ttu-id="91af6-105">В NuGet 4.3.0 ошибки и предупреждения нумеруются, как описано в этом разделе и предоставляют подробные сведения для решения проблемы, связанные.</span><span class="sxs-lookup"><span data-stu-id="91af6-105">In NuGet 4.3.0, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span> 

<span data-ttu-id="91af6-106">Ошибки и предупреждения, перечисленные здесь доступны только с [на основе PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) проекты и NuGet 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="91af6-106">The errors and warnings listed here are available only with [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) projects and NuGet 4.3.0.</span></span> <span data-ttu-id="91af6-107">NuGet также учитывает свойства MSBuild для предупреждений или повысить их к ошибкам.</span><span class="sxs-lookup"><span data-stu-id="91af6-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="91af6-108">Дополнительные сведения см. в разделе [как: отключить предупреждения компилятора](/visualstudio/ide/how-to-suppress-compiler-warnings) в документации по Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="91af6-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="91af6-109">**Ошибки**</span><span class="sxs-lookup"><span data-stu-id="91af6-109">**Errors**</span></span>

| <span data-ttu-id="91af6-110">Группа</span><span class="sxs-lookup"><span data-stu-id="91af6-110">Group</span></span> | <span data-ttu-id="91af6-111">Номера ошибок</span><span class="sxs-lookup"><span data-stu-id="91af6-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="91af6-112">Недопустимый ошибок ввода</span><span class="sxs-lookup"><span data-stu-id="91af6-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="91af6-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="91af6-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="91af6-114">Отсутствуют ошибки пакетов и проектов</span><span class="sxs-lookup"><span data-stu-id="91af6-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="91af6-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (ранее NU1607), [NU1108](#nu1108) (ранее NU1606)</span><span class="sxs-lookup"><span data-stu-id="91af6-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="91af6-116">Ошибки совместимости</span><span class="sxs-lookup"><span data-stu-id="91af6-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="91af6-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="91af6-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="91af6-118">**Предупреждения**</span><span class="sxs-lookup"><span data-stu-id="91af6-118">**Warnings**</span></span>

| <span data-ttu-id="91af6-119">Группа</span><span class="sxs-lookup"><span data-stu-id="91af6-119">Group</span></span> | <span data-ttu-id="91af6-120">Номеров предупреждений</span><span class="sxs-lookup"><span data-stu-id="91af6-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="91af6-121">Недопустимый входной предупреждения</span><span class="sxs-lookup"><span data-stu-id="91af6-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="91af6-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="91af6-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="91af6-123">Непредвиденная пакета версии предупреждения</span><span class="sxs-lookup"><span data-stu-id="91af6-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="91af6-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="91af6-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="91af6-125">Арбитр конфликтов предупреждения</span><span class="sxs-lookup"><span data-stu-id="91af6-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="91af6-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="91af6-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="91af6-127">Резервный предупреждения пакетов</span><span class="sxs-lookup"><span data-stu-id="91af6-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="91af6-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="91af6-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="91af6-129">Предупреждения веб-канала</span><span class="sxs-lookup"><span data-stu-id="91af6-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="91af6-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="91af6-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="91af6-131">NuGet внутренних ошибок и предупреждений</span><span class="sxs-lookup"><span data-stu-id="91af6-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="91af6-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="91af6-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="91af6-133">Недопустимый ошибок ввода</span><span class="sxs-lookup"><span data-stu-id="91af6-133">Invalid input errors</span></span>

<span data-ttu-id="91af6-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="91af6-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="91af6-135">NU1001</span><span class="sxs-lookup"><span data-stu-id="91af6-135">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-136">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-136">**Issue**</span></span> | <span data-ttu-id="91af6-137">Проект не содержит один или несколько платформ.</span><span class="sxs-lookup"><span data-stu-id="91af6-137">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="91af6-138">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-138">**Common causes**</span></span> | <span data-ttu-id="91af6-139">Проект не содержит `TargetFramework` или `TargetFrameworks` свойства.</span><span class="sxs-lookup"><span data-stu-id="91af6-139">The project doesn't contain a `TargetFramework` or `TargetFrameworks` property.</span></span> |
| <span data-ttu-id="91af6-140">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-140">**Example message**</span></span> | <span data-ttu-id="91af6-141">*ProjA проекта не указывает целевые платформы в c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="91af6-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |

### <a name="nu1002"></a><span data-ttu-id="91af6-142">NU1002</span><span class="sxs-lookup"><span data-stu-id="91af6-142">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-143">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-143">**Issue**</span></span> | <span data-ttu-id="91af6-144">Недопустимое сочетание входных данных вместе с ключевым словом, снимите ФЛАЖОК.</span><span class="sxs-lookup"><span data-stu-id="91af6-144">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="91af6-145">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-145">**Common causes**</span></span> | <span data-ttu-id="91af6-146">CLEAR не может быть объединен с другими входными данными.</span><span class="sxs-lookup"><span data-stu-id="91af6-146">CLEAR may not be combined with other inputs.</span></span> |
| <span data-ttu-id="91af6-147">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-147">**Example message**</span></span> | <span data-ttu-id="91af6-148">*«CLEAR» не может использоваться в сочетании с другими значениями*</span><span class="sxs-lookup"><span data-stu-id="91af6-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |

### <a name="nu1003"></a><span data-ttu-id="91af6-149">NU1003</span><span class="sxs-lookup"><span data-stu-id="91af6-149">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-150">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-150">**Issue**</span></span> | <span data-ttu-id="91af6-151">`PackageTargetFallback`и `AssetTargetFallback` поддержки разных режимов работы для выбора средств и не могут использоваться вместе.</span><span class="sxs-lookup"><span data-stu-id="91af6-151">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="91af6-152">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-152">**Common causes**</span></span> | <span data-ttu-id="91af6-153">Оба `PackageTargetFallback` и `AssetTargetFallback` существует в проекте.</span><span class="sxs-lookup"><span data-stu-id="91af6-153">Both `PackageTargetFallback` and `AssetTargetFallback` exist in the project.</span></span> |
| <span data-ttu-id="91af6-154">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-154">**Example message**</span></span> | <span data-ttu-id="91af6-155">*PackageTargetFallback и AssetTargetFallback не может использоваться вместе. Удалите PackageTargetFallback(deprecated) ссылки из проекта среды.*</span><span class="sxs-lookup"><span data-stu-id="91af6-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="91af6-156">Отсутствуют ошибки пакетов и проектов</span><span class="sxs-lookup"><span data-stu-id="91af6-156">Missing package and project errors</span></span>

<span data-ttu-id="91af6-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="91af6-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="91af6-158">NU1100</span><span class="sxs-lookup"><span data-stu-id="91af6-158">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-159">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-159">**Issue**</span></span> | <span data-ttu-id="91af6-160">Не удается разрешить группе зависимостей.</span><span class="sxs-lookup"><span data-stu-id="91af6-160">A dependency group not be resolved.</span></span> <span data-ttu-id="91af6-161">Это проблема универсальных типов, которые не являются пакетами или проектов.</span><span class="sxs-lookup"><span data-stu-id="91af6-161">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="91af6-162">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-162">**Common causes**</span></span> | <span data-ttu-id="91af6-163">Проект содержит зависимость от элемента, который не существует.</span><span class="sxs-lookup"><span data-stu-id="91af6-163">The project contains a dependency on an item that doesn't exist.</span></span> |
| <span data-ttu-id="91af6-164">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-164">**Example message**</span></span> | <span data-ttu-id="91af6-165">*Не удается разрешить System.Missing для net45*</span><span class="sxs-lookup"><span data-stu-id="91af6-165">*Unable to resolve System.Missing for net45*</span></span> |

### <a name="nu1101"></a><span data-ttu-id="91af6-166">NU1101</span><span class="sxs-lookup"><span data-stu-id="91af6-166">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-167">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-167">**Issue**</span></span> | <span data-ttu-id="91af6-168">Не удается найти пакет на любые источники.</span><span class="sxs-lookup"><span data-stu-id="91af6-168">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="91af6-169">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-169">**Common causes**</span></span> | <span data-ttu-id="91af6-170">Источник правильный пакет отсутствует или неверный идентификатор пакета.</span><span class="sxs-lookup"><span data-stu-id="91af6-170">The correct package source is missing or the package identifier is incorrect.</span></span> |
| <span data-ttu-id="91af6-171">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-171">**Example message**</span></span> | <span data-ttu-id="91af6-172">*Не удалось найти пакет System.Missing. Пакеты не существовать с этим идентификатором в источниках: dotnet core, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="91af6-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |

### <a name="nu1102"></a><span data-ttu-id="91af6-173">NU1102</span><span class="sxs-lookup"><span data-stu-id="91af6-173">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-174">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-174">**Issue**</span></span> | <span data-ttu-id="91af6-175">Найти идентификатор пакета, но не удается найти версию в пределах диапазона задана зависимость на любом из источников.</span><span class="sxs-lookup"><span data-stu-id="91af6-175">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> |
| <span data-ttu-id="91af6-176">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-176">**Common causes**</span></span> | <span data-ttu-id="91af6-177">Источник правильный пакет отсутствует или неверен диапазона зависимостей.</span><span class="sxs-lookup"><span data-stu-id="91af6-177">The correct package source is missing or the dependency range is incorrect.</span></span> <span data-ttu-id="91af6-178">Диапазон может быть указана в пакете и не пользователем.</span><span class="sxs-lookup"><span data-stu-id="91af6-178">The range might be specified by a package and not the user.</span></span> <span data-ttu-id="91af6-179">Пользователь может потребоваться переключиться доступная версия, если этот пакет находится непосредственно ссылается проект.</span><span class="sxs-lookup"><span data-stu-id="91af6-179">The user may need to switch to an available version if this package is referenced by the project directly.</span></span> |
| <span data-ttu-id="91af6-180">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-180">**Example message**</span></span> | <span data-ttu-id="91af6-181">*Не удалось найти пакет NuGet.Versioning версии (> = 9.0.1)<br/> -версии найден 30 в nuget.org [ближайшего версии: 4.0.0]<br/> -версии 10 найдено в dotnet buildtools [ближайшего версии: 4.0.0-rc-2129]<br/> -найдено 9 версии в NuGetVolatile [ближайшего версии: 3.0.0-beta-00032]<br/> -найдено 0 версии ядра dotnet<br/> -найдено 0 версии в dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="91af6-181">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1103"></a><span data-ttu-id="91af6-182">NU1103</span><span class="sxs-lookup"><span data-stu-id="91af6-182">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-183">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-183">**Issue**</span></span> | <span data-ttu-id="91af6-184">Стабильные версий не обнаружено в диапазоне зависимостей.</span><span class="sxs-lookup"><span data-stu-id="91af6-184">No stable versions were found in the dependency range.</span></span> <span data-ttu-id="91af6-185">Предварительные версии найдены, однако не допускаются.</span><span class="sxs-lookup"><span data-stu-id="91af6-185">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="91af6-186">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-186">**Common causes**</span></span> | <span data-ttu-id="91af6-187">Проект указан стабильная версия для диапазона зависимостей.</span><span class="sxs-lookup"><span data-stu-id="91af6-187">The project specified a stable version for the dependency range.</span></span> <span data-ttu-id="91af6-188">Пользователи должны изменить диапазон версий для включения предварительных версий.</span><span class="sxs-lookup"><span data-stu-id="91af6-188">Users need to change the version range to include pre-release versions.</span></span> |
| <span data-ttu-id="91af6-189">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-189">**Example message**</span></span> | <span data-ttu-id="91af6-190">*Не удается найти стабильного пакета NuGet.Versioning с версией (> = 3.0.0)<br/> -версии 10 найдено в dotnet buildtools [ближайшего версии: 4.0.0-rc-2129]<br/> -версии 9 найден в NuGetVolatile [ближайшего версии: 3.0.0-beta-00032] <br/> -Найдено 0 версии ядра dotnet<br/> -найдено 0 версии в dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="91af6-190">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1104"></a><span data-ttu-id="91af6-191">NU1104</span><span class="sxs-lookup"><span data-stu-id="91af6-191">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-192">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-192">**Issue**</span></span> | <span data-ttu-id="91af6-193">Ссылкунапроект указывает на файл, который не существует.</span><span class="sxs-lookup"><span data-stu-id="91af6-193">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="91af6-194">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-194">**Common causes**</span></span> | <span data-ttu-id="91af6-195">Отсутствует файл проекта с диска или Неверная ссылка.</span><span class="sxs-lookup"><span data-stu-id="91af6-195">The project file is missing from disk or the reference is incorrect.</span></span> |
| <span data-ttu-id="91af6-196">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-196">**Example message**</span></span> | <span data-ttu-id="91af6-197">*Ссылки на проект «c:\a.csproj» не существует. Проверьте допустимость ссылку на проект и существование файла проекта.*</span><span class="sxs-lookup"><span data-stu-id="91af6-197">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |

### <a name="nu1105"></a><span data-ttu-id="91af6-198">NU1105</span><span class="sxs-lookup"><span data-stu-id="91af6-198">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-199">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-199">**Issue**</span></span> | <span data-ttu-id="91af6-200">Файл проекта существует, но не данные восстановления не указаны для него.</span><span class="sxs-lookup"><span data-stu-id="91af6-200">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="91af6-201">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-201">**Common causes**</span></span> | <span data-ttu-id="91af6-202">В Visual Studio это может означать, что проект будет выгружен.</span><span class="sxs-lookup"><span data-stu-id="91af6-202">In Visual Studio this could mean that the project is unloaded.</span></span> <span data-ttu-id="91af6-203">Из командной строки это может означать, что файл поврежден или не содержит пользовательский после импорта целевого объекта для восстановления для чтения проекта.</span><span class="sxs-lookup"><span data-stu-id="91af6-203">From the command line this could mean that the file is corrupt or that it doesn't contain the custom after imports target needed for restore to read the project.</span></span> |
| <span data-ttu-id="91af6-204">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-204">**Example message**</span></span> | <span data-ttu-id="91af6-205">*Не удается прочитать сведения о проекте для «c:\a.csproj». Файл проекта может быть недопустим или отсутствует целевые объекты, необходимые для восстановления.*</span><span class="sxs-lookup"><span data-stu-id="91af6-205">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

### <a name="nu1106"></a><span data-ttu-id="91af6-206">NU1106</span><span class="sxs-lookup"><span data-stu-id="91af6-206">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-207">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-207">**Issue**</span></span> | <span data-ttu-id="91af6-208">Ограничений на зависимости невозможно разрешить.</span><span class="sxs-lookup"><span data-stu-id="91af6-208">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="91af6-209">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-209">**Common causes**</span></span> | <span data-ttu-id="91af6-210">Пакеты содержат зависимость от точные версии пакета, вместо неограниченного диапазонов.</span><span class="sxs-lookup"><span data-stu-id="91af6-210">Packages contain dependency on exact versions of a package instead of open-ended ranges.</span></span> |
| <span data-ttu-id="91af6-211">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-211">**Example message**</span></span> | <span data-ttu-id="91af6-212">*Не удалось удовлетворить конфликтующие запросы для {id}: {конфликт путь} Framework: {целевого графа}*</span><span class="sxs-lookup"><span data-stu-id="91af6-212">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |

<a name="nu1107"></a> 

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="91af6-213">NU1107 (ранее NU1607)</span><span class="sxs-lookup"><span data-stu-id="91af6-213">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-214">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-214">**Issue**</span></span> | <span data-ttu-id="91af6-215">Не удается разрешить ограничений на зависимости между пакетами.</span><span class="sxs-lookup"><span data-stu-id="91af6-215">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="91af6-216">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-216">**Common causes**</span></span> | <span data-ttu-id="91af6-217">Пакеты с ограничениями зависимостей точные версии не позволяют увеличить версии, при необходимости другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="91af6-217">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> |
| <span data-ttu-id="91af6-218">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-218">**Example message**</span></span> | <span data-ttu-id="91af6-219">*Для NuGet.Versioning обнаружен конфликт версий. Непосредственно из проекта, чтобы устранить эту проблему, ссылающиеся на пакет.<br/>  NuGet.Packaging 3.5.0 -> (= 3.5.0) NuGet.Versioning<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="91af6-219">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="91af6-220">NU1108 (ранее NU1606)</span><span class="sxs-lookup"><span data-stu-id="91af6-220">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-221">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-221">**Issue**</span></span> | <span data-ttu-id="91af6-222">Обнаружена циклическая зависимость.</span><span class="sxs-lookup"><span data-stu-id="91af6-222">A circular dependency was detected.</span></span> |
| <span data-ttu-id="91af6-223">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-223">**Common causes**</span></span> | <span data-ttu-id="91af6-224">Пакет созданы неправильно.</span><span class="sxs-lookup"><span data-stu-id="91af6-224">A package is authored incorrectly.</span></span> |
| <span data-ttu-id="91af6-225">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-225">**Example message**</span></span> | <span data-ttu-id="91af6-226">*Обнаружен цикл: A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="91af6-226">*Cycle detected: A -> B -> A*</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="91af6-227">Ошибки совместимости</span><span class="sxs-lookup"><span data-stu-id="91af6-227">Compatibility errors</span></span>

<span data-ttu-id="91af6-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="91af6-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="91af6-229">NU1201</span><span class="sxs-lookup"><span data-stu-id="91af6-229">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-230">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-230">**Issue**</span></span> | <span data-ttu-id="91af6-231">Зависимости проекта не содержит framework, совместимый с текущим проектом.</span><span class="sxs-lookup"><span data-stu-id="91af6-231">A dependency project doesn't contain a framework compatible with the current project.</span></span> |
| <span data-ttu-id="91af6-232">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-232">**Common causes**</span></span> | <span data-ttu-id="91af6-233">С целевой платформой проекта является более поздней версии, чем проект потребителя.</span><span class="sxs-lookup"><span data-stu-id="91af6-233">The project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="91af6-234">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-234">**Example message**</span></span> | <span data-ttu-id="91af6-235">*ServerWeb проект несовместим с netstandard1.3 (. Моникеров NETStandard, Version = версия 1.3). Проект поддерживает ServerWeb:<br/> -netstandard1.6 (. Моникеров NETStandard, версия = версии 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = версия 1.0)*</span><span class="sxs-lookup"><span data-stu-id="91af6-235">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |

### <a name="nu1202"></a><span data-ttu-id="91af6-236">NU1202</span><span class="sxs-lookup"><span data-stu-id="91af6-236">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-237">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-237">**Issue**</span></span> | <span data-ttu-id="91af6-238">Зависимость пакета не содержит все активы, совместимые с проектом.</span><span class="sxs-lookup"><span data-stu-id="91af6-238">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="91af6-239">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-239">**Common causes**</span></span> | <span data-ttu-id="91af6-240">Пакет не поддерживает целевую исполняющую среду проекта.</span><span class="sxs-lookup"><span data-stu-id="91af6-240">The package doesn't support the project's target framework.</span></span> |
| <span data-ttu-id="91af6-241">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-241">**Example message**</span></span> | <span data-ttu-id="91af6-242">*Пакет System.ComponentModel.EventBasedAsync 4.0.11 не совместим с netstandard1.3 (. Моникеров NETStandard, Version = версия 1.3). Пакет поддерживает System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, Version = версия 1.0)<br/> -monotouch10 (MonoTouch, версия = версия 1.0)<br/> -net45 (. NETFramework, версия = v4.5)<br/> -netcore50 (. NETCore, версия = версии 5.0)<br/> -netstandard1.0 (. Моникеров NETStandard, Version = версия 1.0)<br/> -portable net45 + win8 + wp8 + wpa81 (. NETPortable, версия = v0.0 профиль = Profile259)<br/> -win8 (Windows, версия = версии 8.0)<br/> -wp8 (WindowsPhone, версия = версии 8.0)<br/> -wpa81 (WindowsPhoneApp, версия = v8.1)<br/> -xamarinios10 () Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="91af6-242">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|

### <a name="nu1203"></a><span data-ttu-id="91af6-243">NU1203</span><span class="sxs-lookup"><span data-stu-id="91af6-243">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-244">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-244">**Issue**</span></span> | <span data-ttu-id="91af6-245">Пакет не поддерживает проекта `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="91af6-245">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="91af6-246">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-246">**Common causes**</span></span> | <span data-ttu-id="91af6-247">Пакет не поддерживает текущий `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="91af6-247">The package doesn't support the current `RuntimeIdentifier`.</span></span> <span data-ttu-id="91af6-248">Изменение `RuntimeIdentifier` значения, используемые в проекте, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="91af6-248">Change the `RuntimeIdentifier` values used in the project if needed.</span></span> |
| <span data-ttu-id="91af6-249">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-249">**Example message**</span></span> | <span data-ttu-id="91af6-250">*System.Example 1.0.0 обеспечивается компиляции ссылочную сборку для a.dll net461, но отсутствует совместимый сборка во время выполнения.*</span><span class="sxs-lookup"><span data-stu-id="91af6-250">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |

### <a name="nu1401"></a><span data-ttu-id="91af6-251">NU1401</span><span class="sxs-lookup"><span data-stu-id="91af6-251">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-252">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-252">**Issue**</span></span> | <span data-ttu-id="91af6-253">Для пакета требуется функции или платформ, в настоящее время не поддерживается установленной версией NuGet.</span><span class="sxs-lookup"><span data-stu-id="91af6-253">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="91af6-254">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-254">**Common causes**</span></span> | <span data-ttu-id="91af6-255">Обновите NuGet, чтобы устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="91af6-255">Upgrade NuGet to fix the issue.</span></span> |
| <span data-ttu-id="91af6-256">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-256">**Example message**</span></span> | <span data-ttu-id="91af6-257">*Требует NuGet версии клиента "5.0.0» пакет «NuGet.Versioning» или выше, но текущая версия NuGet —"4.3.0». Чтобы обновить NuGet, перейдите к http://docs.nuget.org/consume/installing-nuget.*</span><span class="sxs-lookup"><span data-stu-id="91af6-257">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'. To upgrade NuGet, please go to http://docs.nuget.org/consume/installing-nuget.*</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="91af6-258">Недопустимый входной предупреждения</span><span class="sxs-lookup"><span data-stu-id="91af6-258">Invalid input warnings</span></span>

<span data-ttu-id="91af6-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="91af6-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="91af6-260">NU1501</span><span class="sxs-lookup"><span data-stu-id="91af6-260">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-261">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-261">**Issue**</span></span> | <span data-ttu-id="91af6-262">Восстановить проект пытается работать в не найден.</span><span class="sxs-lookup"><span data-stu-id="91af6-262">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="91af6-263">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-263">**Common causes**</span></span> | <span data-ttu-id="91af6-264">Отсутствует проект.</span><span class="sxs-lookup"><span data-stu-id="91af6-264">The project is missing.</span></span> |
| <span data-ttu-id="91af6-265">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-265">**Example message**</span></span> | <span data-ttu-id="91af6-266">*Папка «c:\projects\a» не содержит проектов для восстановления.*</span><span class="sxs-lookup"><span data-stu-id="91af6-266">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |

### <a name="nu1502"></a><span data-ttu-id="91af6-267">NU1502</span><span class="sxs-lookup"><span data-stu-id="91af6-267">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-268">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-268">**Issue**</span></span> | <span data-ttu-id="91af6-269">`RuntimeSupports`содержит недопустимый профиль.</span><span class="sxs-lookup"><span data-stu-id="91af6-269">`RuntimeSupports` contains an invalid profile.</span></span> |
| <span data-ttu-id="91af6-270">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-270">**Common causes**</span></span> | <span data-ttu-id="91af6-271">Поддерживает профиль не найден в `runtime.json` файл из текущего зависимостей пакетов.</span><span class="sxs-lookup"><span data-stu-id="91af6-271">The supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span> |
| <span data-ttu-id="91af6-272">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-272">**Example message**</span></span> | <span data-ttu-id="91af6-273">*Неизвестный совместимости профиля: aaa*</span><span class="sxs-lookup"><span data-stu-id="91af6-273">*Unknown Compatibility Profile: aaa*</span></span> |

### <a name="nu1503"></a><span data-ttu-id="91af6-274">NU1503</span><span class="sxs-lookup"><span data-stu-id="91af6-274">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-275">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-275">**Issue**</span></span> | <span data-ttu-id="91af6-276">Зависимости проекта не импортирует целевые объекты восстановления NuGet.</span><span class="sxs-lookup"><span data-stu-id="91af6-276">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="91af6-277">Это похоже на NU1105, но здесь пропускается проект и пропускаются, а не вызывает все восстановления к сбою.</span><span class="sxs-lookup"><span data-stu-id="91af6-277">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="91af6-278">В сложных решениях часто возникают других типов проектов, которые могут не поддерживать восстановления.</span><span class="sxs-lookup"><span data-stu-id="91af6-278">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="91af6-279">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-279">**Common causes**</span></span> | <span data-ttu-id="91af6-280">Это может произойти для проектов, которые не импортировать общие props/объекты, которые автоматически импортировать восстановления.</span><span class="sxs-lookup"><span data-stu-id="91af6-280">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="91af6-281">Если проект не нуждаются в восстановлении это сообщение можно проигнорировать.</span><span class="sxs-lookup"><span data-stu-id="91af6-281">If the project doesn't need to be restored this can be ignored.</span></span> |
| <span data-ttu-id="91af6-282">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-282">**Example message**</span></span> | <span data-ttu-id="91af6-283">*Пропуск восстановления для проекта «c:\a.csproj». Файл проекта может быть недопустим или отсутствует целевые объекты, необходимые для восстановления.*</span><span class="sxs-lookup"><span data-stu-id="91af6-283">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="91af6-284">Непредвиденная пакета версии предупреждения</span><span class="sxs-lookup"><span data-stu-id="91af6-284">Unexpected package version warnings</span></span>

<span data-ttu-id="91af6-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="91af6-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="91af6-286">NU1601</span><span class="sxs-lookup"><span data-stu-id="91af6-286">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-287">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-287">**Issue**</span></span> | <span data-ttu-id="91af6-288">Зависимость прямой проекта был увеличить на один на более позднюю версию, чем указанный проект.</span><span class="sxs-lookup"><span data-stu-id="91af6-288">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="91af6-289">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-289">**Common causes**</span></span> | <span data-ttu-id="91af6-290">Другой пакет зависимостей требуется более поздняя версия и увеличить один пакет.</span><span class="sxs-lookup"><span data-stu-id="91af6-290">Another dependency package required a higher version and bumped the package up.</span></span> |
| <span data-ttu-id="91af6-291">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-291">**Example message**</span></span> | <span data-ttu-id="91af6-292">*Указанная зависимость — NuGet.Versioning (> = 3.5.0), но завершено с NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="91af6-292">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |

### <a name="nu1602"></a><span data-ttu-id="91af6-293">NU1602</span><span class="sxs-lookup"><span data-stu-id="91af6-293">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-294">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-294">**Issue**</span></span> | <span data-ttu-id="91af6-295">Зависимость пакета отсутствует нижняя граница.</span><span class="sxs-lookup"><span data-stu-id="91af6-295">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="91af6-296">Это не позволяет восстановления найти *наилучшего соответствия*.</span><span class="sxs-lookup"><span data-stu-id="91af6-296">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="91af6-297">Каждый восстановления будет находиться вниз при попытке найти более ранней версии, который может использоваться.</span><span class="sxs-lookup"><span data-stu-id="91af6-297">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="91af6-298">Это означает, что процесс восстановления в оперативный режим для проверки всех источников каждый раз, вместо того чтобы использовать пакеты, которые уже существуют в папке пользователя пакета.</span><span class="sxs-lookup"><span data-stu-id="91af6-298">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="91af6-299">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-299">**Common causes**</span></span> | <span data-ttu-id="91af6-300">Обычно это пакет разработки ошибки.</span><span class="sxs-lookup"><span data-stu-id="91af6-300">This is usually a package authoring error.</span></span> |
| <span data-ttu-id="91af6-301">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-301">**Example message**</span></span> | <span data-ttu-id="91af6-302">*NuGet.Packaging 4.0.0 не предоставляет инклюзивную нижнюю границу для зависимостей NuGet.Versioning (> 3.5.0). Приблизительное наиболее подходящие 3.6.0 был разрешен.*</span><span class="sxs-lookup"><span data-stu-id="91af6-302">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |

### <a name="nu1603"></a><span data-ttu-id="91af6-303">NU1603</span><span class="sxs-lookup"><span data-stu-id="91af6-303">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-304">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-304">**Issue**</span></span> | <span data-ttu-id="91af6-305">Зависимость пакета указаны версии, не найден.</span><span class="sxs-lookup"><span data-stu-id="91af6-305">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="91af6-306">Более поздняя версия вместо него используется, которая отличается от пакет был создан для.</span><span class="sxs-lookup"><span data-stu-id="91af6-306">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="91af6-307">Это означает, что восстановление не удалось найти *наилучшего соответствия*.</span><span class="sxs-lookup"><span data-stu-id="91af6-307">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="91af6-308">Каждый восстановления будет находиться вниз при попытке найти более ранней версии, который может использоваться.</span><span class="sxs-lookup"><span data-stu-id="91af6-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="91af6-309">Это означает, что процесс восстановления в оперативный режим для проверки всех источников каждый раз, вместо того чтобы использовать пакеты, которые уже существуют в папке пользователя пакета.</span><span class="sxs-lookup"><span data-stu-id="91af6-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="91af6-310">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-310">**Common causes**</span></span> | <span data-ttu-id="91af6-311">Источники пакетов не содержат версии ожидаемый нижней границы.</span><span class="sxs-lookup"><span data-stu-id="91af6-311">The package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="91af6-312">Если требуется пакет не был выпущен, это может быть ошибка создания пакета.</span><span class="sxs-lookup"><span data-stu-id="91af6-312">If the package expected has not been released then this may be a package authoring error.</span></span> |
| <span data-ttu-id="91af6-313">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-313">**Example message**</span></span> | <span data-ttu-id="91af6-314">NuGet.Packaging 4.0.0 зависит от NuGet.Versioning (> = 4.0.0), но 4.0.0 не найден.</span><span class="sxs-lookup"><span data-stu-id="91af6-314">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="91af6-315">Приблизительное наиболее подходящие 5.0.0 был разрешен.</span><span class="sxs-lookup"><span data-stu-id="91af6-315">An approximate best match of 5.0.0 was resolved.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="91af6-316">NU1604</span><span class="sxs-lookup"><span data-stu-id="91af6-316">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-317">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-317">**Issue**</span></span> | <span data-ttu-id="91af6-318">Зависимости проекта не определяет нижнюю границу.</span><span class="sxs-lookup"><span data-stu-id="91af6-318">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="91af6-319">Это означает, что восстановление не удалось найти *наилучшего соответствия*.</span><span class="sxs-lookup"><span data-stu-id="91af6-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="91af6-320">Каждый восстановления будет находиться вниз при попытке найти более ранней версии, который может использоваться.</span><span class="sxs-lookup"><span data-stu-id="91af6-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="91af6-321">Это означает, что процесс восстановления в оперативный режим для проверки всех источников каждый раз, вместо того чтобы использовать пакеты, которые уже существуют в папке пользователя пакета.</span><span class="sxs-lookup"><span data-stu-id="91af6-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="91af6-322">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-322">**Common causes**</span></span> | <span data-ttu-id="91af6-323">Проект *PackageReference* *версии* атрибута должны быть обновлены для включения нижняя граница.</span><span class="sxs-lookup"><span data-stu-id="91af6-323">The project's *PackageReference* *Version* attribute should be updated to include a lower bound.</span></span> |
| <span data-ttu-id="91af6-324">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-324">**Example message**</span></span> | <span data-ttu-id="91af6-325">*Проект зависимостей NuGet.Versioning (< = от 9.0.0) doe содержит инклюзивную нижнюю границу. Включите нижняя граница в версию зависимостей для обеспечения восстановления, согласованные результаты.*</span><span class="sxs-lookup"><span data-stu-id="91af6-325">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |

### <a name="nu1605"></a><span data-ttu-id="91af6-326">NU1605</span><span class="sxs-lookup"><span data-stu-id="91af6-326">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-327">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-327">**Issue**</span></span> | <span data-ttu-id="91af6-328">Пакета зависимостей указано ограничение версии на более поздняя версия пакета, чем для восстановления в конечном счете.</span><span class="sxs-lookup"><span data-stu-id="91af6-328">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> |
| <span data-ttu-id="91af6-329">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-329">**Common causes**</span></span> | <span data-ttu-id="91af6-330">При разрешении пакеты ближайшего wins.</span><span class="sxs-lookup"><span data-stu-id="91af6-330">Nearest wins when resolving packages.</span></span> <span data-ttu-id="91af6-331">Чем ближе пакета в графе переопределены отдаленных пакета.</span><span class="sxs-lookup"><span data-stu-id="91af6-331">A nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="91af6-332">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-332">**Example message**</span></span> | <span data-ttu-id="91af6-333">*Обнаружен пакет переход к более раннему: NuGet.Versioning из 4.0.0 для 3.5.0. Ссылающиеся на пакет непосредственно из проекта, чтобы выбрать другую версию.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="91af6-333">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="91af6-334">Арбитр конфликтов предупреждения</span><span class="sxs-lookup"><span data-stu-id="91af6-334">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="91af6-335">NU1608</span><span class="sxs-lookup"><span data-stu-id="91af6-335">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-336">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-336">**Issue**</span></span> | <span data-ttu-id="91af6-337">Пакет, разрешения, выше, чем позволяет ограничение зависимостей.</span><span class="sxs-lookup"><span data-stu-id="91af6-337">A resolve package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="91af6-338">В некоторых случаях это сделано намеренно, а предупреждение может быть отменено.</span><span class="sxs-lookup"><span data-stu-id="91af6-338">In some cases this is intentional and the warning can be suppressed.</span></span> |
| <span data-ttu-id="91af6-339">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-339">**Common causes**</span></span> | <span data-ttu-id="91af6-340">Пакет непосредственно ссылается проект переопределит ограничений на зависимости от других пакетов.</span><span class="sxs-lookup"><span data-stu-id="91af6-340">A package referenced directly by a project will override dependency constraints from other packages.</span></span>   |
| <span data-ttu-id="91af6-341">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-341">**Example message**</span></span> | <span data-ttu-id="91af6-342">*Версия пакета обнаруженных вне зависимости ограничение: x 1.0.0 требуется y (= 1.0.0), но версии y 2.0.0 был разрешен.*</span><span class="sxs-lookup"><span data-stu-id="91af6-342">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="91af6-343">Резервный предупреждения пакетов</span><span class="sxs-lookup"><span data-stu-id="91af6-343">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="91af6-344">NU1701</span><span class="sxs-lookup"><span data-stu-id="91af6-344">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-345">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-345">**Issue**</span></span> | <span data-ttu-id="91af6-346">*PackageTargetFallback/AssetTargetFallback* был использован для выбора средств из пакета.</span><span class="sxs-lookup"><span data-stu-id="91af6-346">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span></span> <span data-ttu-id="91af6-347">Это предупреждение для оповещения пользователя о, ОС может быть не совместимы 100%.</span><span class="sxs-lookup"><span data-stu-id="91af6-347">This is a warning to let the user know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="91af6-348">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-348">**Common causes**</span></span> | <span data-ttu-id="91af6-349">Пакет не поддерживает среду проекта.</span><span class="sxs-lookup"><span data-stu-id="91af6-349">The package doesn't support the project framework.</span></span> |
| <span data-ttu-id="91af6-350">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-350">**Example message**</span></span> | <span data-ttu-id="91af6-351">*Пакет «NuGet.Versioning» был восстановлен, вместо этого использовать «portable net45 + win8» целевая платформа проекта «netstandard1.5». Этот пакет не может быть полностью совместим с проектом.*</span><span class="sxs-lookup"><span data-stu-id="91af6-351">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="91af6-352">Предупреждения веб-канала</span><span class="sxs-lookup"><span data-stu-id="91af6-352">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="91af6-353">NU1801</span><span class="sxs-lookup"><span data-stu-id="91af6-353">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-354">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-354">**Issue**</span></span> | <span data-ttu-id="91af6-355">Произошла ошибка при чтении веб-канала при `IgnoreFailedSources` имеет значение true, преобразование ее устранимая предупреждение.</span><span class="sxs-lookup"><span data-stu-id="91af6-355">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="91af6-356">Это может содержать любые сообщения и является универсальным.</span><span class="sxs-lookup"><span data-stu-id="91af6-356">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="91af6-357">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-357">**Common causes**</span></span> | <span data-ttu-id="91af6-358">Недопустимый источник.</span><span class="sxs-lookup"><span data-stu-id="91af6-358">The source is invalid.</span></span> |
| <span data-ttu-id="91af6-359">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="91af6-359">**Example message**</span></span> | <span data-ttu-id="91af6-360">Н/Д</span><span class="sxs-lookup"><span data-stu-id="91af6-360">n/a</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="91af6-361">NuGet внутренних ошибок и предупреждений</span><span class="sxs-lookup"><span data-stu-id="91af6-361">NuGet internal errors and warnings</span></span>

<span data-ttu-id="91af6-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="91af6-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="91af6-363">NU1000</span><span class="sxs-lookup"><span data-stu-id="91af6-363">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-364">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-364">**Issue**</span></span> | <span data-ttu-id="91af6-365">Неопределенный Внутренняя ошибка на NuGet.</span><span class="sxs-lookup"><span data-stu-id="91af6-365">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="91af6-366">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-366">**Common causes**</span></span> | <span data-ttu-id="91af6-367">Дополнительные сведения в журнале</span><span class="sxs-lookup"><span data-stu-id="91af6-367">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="91af6-368">NU1500</span><span class="sxs-lookup"><span data-stu-id="91af6-368">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91af6-369">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="91af6-369">**Issue**</span></span> | <span data-ttu-id="91af6-370">Неопределенный внутренние предупреждения NuGet.</span><span class="sxs-lookup"><span data-stu-id="91af6-370">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="91af6-371">**Основные причины**</span><span class="sxs-lookup"><span data-stu-id="91af6-371">**Common causes**</span></span> | <span data-ttu-id="91af6-372">Дополнительные сведения в журнале</span><span class="sxs-lookup"><span data-stu-id="91af6-372">Check the logs for more information</span></span> |
