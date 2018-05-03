---
title: Справочник предупреждения и ошибки NuGet
description: Полный справочник для предупреждения и ошибки, выданные NuGet при выполнении различных операций NuGet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: anangaur
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
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: dcff20e35adc0a3dbcc7bef482f81a937cf059c5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="1d91d-103">Ошибки и предупреждения</span><span class="sxs-lookup"><span data-stu-id="1d91d-103">Errors and warnings</span></span>

<span data-ttu-id="1d91d-104">В NuGet 4.3.0+ ошибки и предупреждения нумеруются, как описано в этом разделе и предоставляют подробные сведения для решения проблемы, связанные.</span><span class="sxs-lookup"><span data-stu-id="1d91d-104">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="1d91d-105">Ошибки и предупреждения, перечисленные здесь доступны только с [на основе PackageReference](../consume-packages/package-references-in-project-files.md) проекты и NuGet 4.3.0+.</span><span class="sxs-lookup"><span data-stu-id="1d91d-105">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="1d91d-106">NuGet также учитывает свойства MSBuild для предупреждений или повысить их к ошибкам.</span><span class="sxs-lookup"><span data-stu-id="1d91d-106">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="1d91d-107">Дополнительные сведения см. в разделе [как: отключить предупреждения компилятора](/visualstudio/ide/how-to-suppress-compiler-warnings) в документации по Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1d91d-107">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="1d91d-108">**Ошибки**</span><span class="sxs-lookup"><span data-stu-id="1d91d-108">**Errors**</span></span>

| <span data-ttu-id="1d91d-109">Группа</span><span class="sxs-lookup"><span data-stu-id="1d91d-109">Group</span></span> | <span data-ttu-id="1d91d-110">Номера ошибок</span><span class="sxs-lookup"><span data-stu-id="1d91d-110">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="1d91d-111">Недопустимый ошибок ввода</span><span class="sxs-lookup"><span data-stu-id="1d91d-111">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="1d91d-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="1d91d-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="1d91d-113">Отсутствуют ошибки пакетов и проектов</span><span class="sxs-lookup"><span data-stu-id="1d91d-113">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="1d91d-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (ранее NU1607), [NU1108](#nu1108) (ранее NU1606)</span><span class="sxs-lookup"><span data-stu-id="1d91d-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="1d91d-115">Ошибки совместимости</span><span class="sxs-lookup"><span data-stu-id="1d91d-115">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="1d91d-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="1d91d-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="1d91d-117">**Предупреждения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-117">**Warnings**</span></span>

| <span data-ttu-id="1d91d-118">Группа</span><span class="sxs-lookup"><span data-stu-id="1d91d-118">Group</span></span> | <span data-ttu-id="1d91d-119">Номеров предупреждений</span><span class="sxs-lookup"><span data-stu-id="1d91d-119">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="1d91d-120">Недопустимый входной предупреждения</span><span class="sxs-lookup"><span data-stu-id="1d91d-120">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="1d91d-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="1d91d-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="1d91d-122">Непредвиденная пакета версии предупреждения</span><span class="sxs-lookup"><span data-stu-id="1d91d-122">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="1d91d-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="1d91d-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="1d91d-124">Арбитр конфликтов предупреждения</span><span class="sxs-lookup"><span data-stu-id="1d91d-124">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="1d91d-125">NU1608</span><span class="sxs-lookup"><span data-stu-id="1d91d-125">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="1d91d-126">Резервный предупреждения пакетов</span><span class="sxs-lookup"><span data-stu-id="1d91d-126">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="1d91d-127">NU1701</span><span class="sxs-lookup"><span data-stu-id="1d91d-127">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="1d91d-128">Предупреждения веб-канала</span><span class="sxs-lookup"><span data-stu-id="1d91d-128">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="1d91d-129">NU1801</span><span class="sxs-lookup"><span data-stu-id="1d91d-129">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="1d91d-130">NuGet внутренних ошибок и предупреждений</span><span class="sxs-lookup"><span data-stu-id="1d91d-130">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="1d91d-131">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="1d91d-131">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="1d91d-132">Подписанные пакеты (создания и проверки)</span><span class="sxs-lookup"><span data-stu-id="1d91d-132">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="1d91d-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="1d91d-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="1d91d-134">Недопустимый ошибок ввода</span><span class="sxs-lookup"><span data-stu-id="1d91d-134">Invalid input errors</span></span>

<span data-ttu-id="1d91d-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="1d91d-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="1d91d-136">NU1001</span><span class="sxs-lookup"><span data-stu-id="1d91d-136">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-137">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-137">**Issue**</span></span> | <span data-ttu-id="1d91d-138">Проект не содержит один или несколько платформ.</span><span class="sxs-lookup"><span data-stu-id="1d91d-138">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="1d91d-139">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-139">**Example message**</span></span> | <span data-ttu-id="1d91d-140">*ProjA проекта не указывает целевые платформы в c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="1d91d-140">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="1d91d-141">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-141">**Solution**</span></span> | <span data-ttu-id="1d91d-142">Добавить `TargetFramework` или `TargetFrameworks` свойства для указанного файла проекта.</span><span class="sxs-lookup"><span data-stu-id="1d91d-142">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="1d91d-143">NU1002</span><span class="sxs-lookup"><span data-stu-id="1d91d-143">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-144">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-144">**Issue**</span></span> | <span data-ttu-id="1d91d-145">Недопустимое сочетание входных данных вместе с ключевым словом, снимите ФЛАЖОК.</span><span class="sxs-lookup"><span data-stu-id="1d91d-145">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="1d91d-146">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-146">**Example message**</span></span> | <span data-ttu-id="1d91d-147">*«CLEAR» не может использоваться в сочетании с другими значениями*</span><span class="sxs-lookup"><span data-stu-id="1d91d-147">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="1d91d-148">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-148">**Solution**</span></span> | <span data-ttu-id="1d91d-149">Использовать СНИМИТЕ сам по себе и опустить остальные потоки входа.</span><span class="sxs-lookup"><span data-stu-id="1d91d-149">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="1d91d-150">NU1003</span><span class="sxs-lookup"><span data-stu-id="1d91d-150">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-151">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-151">**Issue**</span></span> | <span data-ttu-id="1d91d-152">`PackageTargetFallback` и `AssetTargetFallback` поддержки разных режимов работы для выбора средств и не могут использоваться вместе.</span><span class="sxs-lookup"><span data-stu-id="1d91d-152">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="1d91d-153">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-153">**Example message**</span></span> | <span data-ttu-id="1d91d-154">*PackageTargetFallback и AssetTargetFallback не может использоваться вместе. Удалите PackageTargetFallback(deprecated) ссылки из проекта среды.*</span><span class="sxs-lookup"><span data-stu-id="1d91d-154">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="1d91d-155">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-155">**Solution**</span></span> | <span data-ttu-id="1d91d-156">Удалить устаревшие `PackageTargetFallback` элемент из проекта.</span><span class="sxs-lookup"><span data-stu-id="1d91d-156">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="1d91d-157">Отсутствуют ошибки пакетов и проектов</span><span class="sxs-lookup"><span data-stu-id="1d91d-157">Missing package and project errors</span></span>

<span data-ttu-id="1d91d-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="1d91d-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="1d91d-159">NU1100</span><span class="sxs-lookup"><span data-stu-id="1d91d-159">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-160">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-160">**Issue**</span></span> | <span data-ttu-id="1d91d-161">Не удается разрешить группе зависимостей.</span><span class="sxs-lookup"><span data-stu-id="1d91d-161">A dependency group not be resolved.</span></span> <span data-ttu-id="1d91d-162">Это проблема универсальных типов, которые не являются пакетами или проектов.</span><span class="sxs-lookup"><span data-stu-id="1d91d-162">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="1d91d-163">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-163">**Example message**</span></span> | <span data-ttu-id="1d91d-164">*Не удается разрешить System.Missing для net45*</span><span class="sxs-lookup"><span data-stu-id="1d91d-164">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="1d91d-165">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-165">**Solution**</span></span> | <span data-ttu-id="1d91d-166">Откройте файл проекта и просмотрите список его зависимостей.</span><span class="sxs-lookup"><span data-stu-id="1d91d-166">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="1d91d-167">Проверьте наличие каждой зависимости на источники пакетов, которую вы используете, и что пакет поддерживает целевая платформа проекта.</span><span class="sxs-lookup"><span data-stu-id="1d91d-167">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="1d91d-168">NU1101</span><span class="sxs-lookup"><span data-stu-id="1d91d-168">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-169">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-169">**Issue**</span></span> | <span data-ttu-id="1d91d-170">Не удается найти пакет на любые источники.</span><span class="sxs-lookup"><span data-stu-id="1d91d-170">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="1d91d-171">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-171">**Example message**</span></span> | <span data-ttu-id="1d91d-172">*Не удалось найти пакет System.Missing. Пакеты не существовать с этим идентификатором в источниках: dotnet core, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="1d91d-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="1d91d-173">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-173">**Solution**</span></span> | <span data-ttu-id="1d91d-174">Проверьте зависимости проекта в Visual Studio, чтобы убедиться в том, что вы используете правильный пакет идентификатор и номер версии.</span><span class="sxs-lookup"><span data-stu-id="1d91d-174">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="1d91d-175">Также убедитесь, что [конфигурация NuGet](../consume-packages/Configuring-NuGet-Behavior.md) определяет источники пакетов вашей предполагается использовать.</span><span class="sxs-lookup"><span data-stu-id="1d91d-175">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="1d91d-176">Если вы используете пакеты, имеющие [семантического управления версиями 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), убедитесь в том, что вы используете [V3 веб-канал](https://api.nuget.org/v3/index.json) в [конфигурация NuGet](../consume-packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="1d91d-176">If you use packages that have [Semantic Versioning 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), please make sure that you are using the [V3 feed](https://api.nuget.org/v3/index.json) in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="1d91d-177">NU1102</span><span class="sxs-lookup"><span data-stu-id="1d91d-177">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-178">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-178">**Issue**</span></span> | <span data-ttu-id="1d91d-179">Найти идентификатор пакета, но не удается найти версию в пределах диапазона задана зависимость на любом из источников.</span><span class="sxs-lookup"><span data-stu-id="1d91d-179">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="1d91d-180">Диапазон может быть указана в пакете и не пользователем.</span><span class="sxs-lookup"><span data-stu-id="1d91d-180">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="1d91d-181">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-181">**Example message**</span></span> | <span data-ttu-id="1d91d-182">*Не удалось найти пакет NuGet.Versioning версии (> = 9.0.1)<br/> -версии найден 30 в nuget.org [ближайшего версии: 4.0.0]<br/> -версии 10 найдено в dotnet buildtools [ближайшего версии: 4.0.0-rc-2129]<br/> -найдено 9 версии в NuGetVolatile [ближайшего версии: 3.0.0-beta-00032]<br/> -найдено 0 версии ядра dotnet<br/> -найдено 0 версии в dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="1d91d-182">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="1d91d-183">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-183">**Solution**</span></span> | <span data-ttu-id="1d91d-184">В файле проекта исправление версии пакета.</span><span class="sxs-lookup"><span data-stu-id="1d91d-184">Edit the project file to correct the package version.</span></span> <span data-ttu-id="1d91d-185">Также убедитесь, что [конфигурация NuGet](../consume-packages/Configuring-NuGet-Behavior.md) определяет источники пакетов вашей предполагается использовать.</span><span class="sxs-lookup"><span data-stu-id="1d91d-185">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="1d91d-186">Может потребоваться изменить версию requeted, если этот пакет находится непосредственно ссылается проект.</span><span class="sxs-lookup"><span data-stu-id="1d91d-186">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="1d91d-187">NU1103</span><span class="sxs-lookup"><span data-stu-id="1d91d-187">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-188">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-188">**Issue**</span></span> | <span data-ttu-id="1d91d-189">Проект указан стабильная версия для диапазона зависимостей, но не стабильной версии не найдены в этом диапазоне.</span><span class="sxs-lookup"><span data-stu-id="1d91d-189">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="1d91d-190">Предварительные версии найдены, однако не допускаются.</span><span class="sxs-lookup"><span data-stu-id="1d91d-190">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="1d91d-191">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-191">**Example message**</span></span> | <span data-ttu-id="1d91d-192">*Не удается найти стабильного пакета NuGet.Versioning с версией (> = 3.0.0)<br/> -версии 10 найдено в dotnet buildtools [ближайшего версии: 4.0.0-rc-2129]<br/> -версии 9 найден в NuGetVolatile [ближайшего версии: 3.0.0-beta-00032] <br/> -Найдено 0 версии ядра dotnet<br/> -найдено 0 версии в dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="1d91d-192">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="1d91d-193">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-193">**Solution**</span></span> |  <span data-ttu-id="1d91d-194">Измените диапазон версий в файле проекта для включения предварительных версий.</span><span class="sxs-lookup"><span data-stu-id="1d91d-194">Edit the version range in the project file to include pre-release versions.</span></span> <span data-ttu-id="1d91d-195">В разделе [управления версиями пакета](../reference/Package-Versioning.md).</span><span class="sxs-lookup"><span data-stu-id="1d91d-195">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="1d91d-196">NU1104</span><span class="sxs-lookup"><span data-stu-id="1d91d-196">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-197">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-197">**Issue**</span></span> | <span data-ttu-id="1d91d-198">Ссылкунапроект указывает на файл, который не существует.</span><span class="sxs-lookup"><span data-stu-id="1d91d-198">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="1d91d-199">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-199">**Example message**</span></span> | <span data-ttu-id="1d91d-200">*Ссылки на проект «c:\a.csproj» не существует. Проверьте допустимость ссылку на проект и существование файла проекта.*</span><span class="sxs-lookup"><span data-stu-id="1d91d-200">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="1d91d-201">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-201">**Solution**</span></span> | <span data-ttu-id="1d91d-202">Измените файл проекта, либо измените путь к ссылке проекта или удалить ссылку, если он больше не нужен.</span><span class="sxs-lookup"><span data-stu-id="1d91d-202">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="1d91d-203">NU1105</span><span class="sxs-lookup"><span data-stu-id="1d91d-203">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-204">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-204">**Issue**</span></span> | <span data-ttu-id="1d91d-205">Файл проекта существует, но не данные восстановления не указаны для него.</span><span class="sxs-lookup"><span data-stu-id="1d91d-205">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="1d91d-206">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-206">**Example message**</span></span> | <span data-ttu-id="1d91d-207">*Не удается прочитать сведения о проекте для «c:\a.csproj». Файл проекта может быть недопустим или отсутствует целевые объекты, необходимые для восстановления.*</span><span class="sxs-lookup"><span data-stu-id="1d91d-207">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="1d91d-208">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-208">**Solution**</span></span> | <span data-ttu-id="1d91d-209">В Visual Studio ошибка может означать, что проект будет выгружен в этом случае перезагрузить проект.</span><span class="sxs-lookup"><span data-stu-id="1d91d-209">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="1d91d-210">Из командной строки, это может означать, что файл поврежден или не содержит пользовательский «после импорта» целевой для восстановления для чтения проекта.</span><span class="sxs-lookup"><span data-stu-id="1d91d-210">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="1d91d-211">Убедитесь, что файл проекта является допустимым и содержит целевой объект «по окончании imports».</span><span class="sxs-lookup"><span data-stu-id="1d91d-211">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="1d91d-212">NU1106</span><span class="sxs-lookup"><span data-stu-id="1d91d-212">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-213">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-213">**Issue**</span></span> | <span data-ttu-id="1d91d-214">Ограничений на зависимости невозможно разрешить.</span><span class="sxs-lookup"><span data-stu-id="1d91d-214">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="1d91d-215">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-215">**Example message**</span></span> | <span data-ttu-id="1d91d-216">*Не удалось удовлетворить конфликтующие запросы для {id}: {конфликт путь} Framework: {целевого графа}*</span><span class="sxs-lookup"><span data-stu-id="1d91d-216">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |
| <span data-ttu-id="1d91d-217">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-217">**Solution**</span></span> | <span data-ttu-id="1d91d-218">В файле проекта для указания диапазона больше зависимостей, а не точную версию.</span><span class="sxs-lookup"><span data-stu-id="1d91d-218">Edit the project file to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="1d91d-219">NU1107 (ранее NU1607)</span><span class="sxs-lookup"><span data-stu-id="1d91d-219">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-220">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-220">**Issue**</span></span> | <span data-ttu-id="1d91d-221">Не удается разрешить ограничений на зависимости между пакетами.</span><span class="sxs-lookup"><span data-stu-id="1d91d-221">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="1d91d-222">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-222">**Example message**</span></span> | <span data-ttu-id="1d91d-223">*Для NuGet.Versioning обнаружен конфликт версий. Непосредственно из проекта, чтобы устранить эту проблему, ссылающиеся на пакет.<br/>  NuGet.Packaging 3.5.0 -> (= 3.5.0) NuGet.Versioning<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="1d91d-223">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="1d91d-224">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-224">**Solution**</span></span> | <span data-ttu-id="1d91d-225">Пакеты с ограничениями зависимостей точные версии не позволяют увеличить версии, при необходимости другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="1d91d-225">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="1d91d-226">Добавьте ссылку на проект напрямую (в файле проекта) к той самой версии требуется.</span><span class="sxs-lookup"><span data-stu-id="1d91d-226">Add a reference to the project directly (in the project file) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="1d91d-227">NU1108 (ранее NU1606)</span><span class="sxs-lookup"><span data-stu-id="1d91d-227">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-228">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-228">**Issue**</span></span> | <span data-ttu-id="1d91d-229">Обнаружена циклическая зависимость.</span><span class="sxs-lookup"><span data-stu-id="1d91d-229">A circular dependency was detected.</span></span> |
| <span data-ttu-id="1d91d-230">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-230">**Example message**</span></span> | <span data-ttu-id="1d91d-231">*Обнаружен цикл: A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="1d91d-231">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="1d91d-232">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-232">**Solution**</span></span> | <span data-ttu-id="1d91d-233">Пакет создается неправильно; Обратитесь к владельцу пакета, чтобы исправить ошибку.</span><span class="sxs-lookup"><span data-stu-id="1d91d-233">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="1d91d-234">Ошибки совместимости</span><span class="sxs-lookup"><span data-stu-id="1d91d-234">Compatibility errors</span></span>

<span data-ttu-id="1d91d-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="1d91d-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="1d91d-236">NU1201</span><span class="sxs-lookup"><span data-stu-id="1d91d-236">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-237">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-237">**Issue**</span></span> | <span data-ttu-id="1d91d-238">Зависимости проекта не содержит framework, совместимый с текущим проектом.</span><span class="sxs-lookup"><span data-stu-id="1d91d-238">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="1d91d-239">Как правило с целевой платформой проекта является более поздней версии, чем проект потребителя.</span><span class="sxs-lookup"><span data-stu-id="1d91d-239">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="1d91d-240">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-240">**Example message**</span></span> | <span data-ttu-id="1d91d-241">*ServerWeb проект несовместим с netstandard1.3 (. Моникеров NETStandard, Version = версия 1.3). Проект поддерживает ServerWeb:<br/> -netstandard1.6 (. Моникеров NETStandard, версия = версии 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = версия 1.0)*</span><span class="sxs-lookup"><span data-stu-id="1d91d-241">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="1d91d-242">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-242">**Solution**</span></span> | <span data-ttu-id="1d91d-243">Изменения целевой платформы проекта для версии равно или ниже, чем требуется много проекта.</span><span class="sxs-lookup"><span data-stu-id="1d91d-243">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="1d91d-244">NU1202</span><span class="sxs-lookup"><span data-stu-id="1d91d-244">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-245">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-245">**Issue**</span></span> | <span data-ttu-id="1d91d-246">Зависимость пакета не содержит все активы, совместимые с проектом.</span><span class="sxs-lookup"><span data-stu-id="1d91d-246">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="1d91d-247">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-247">**Example message**</span></span> | <span data-ttu-id="1d91d-248">*Пакет System.ComponentModel.EventBasedAsync 4.0.11 не совместим с netstandard1.3 (. Моникеров NETStandard, Version = версия 1.3). Пакет поддерживает System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, Version = версия 1.0)<br/> -monotouch10 (MonoTouch, версия = версия 1.0)<br/> -net45 (. NETFramework, версия = v4.5)<br/> -netcore50 (. NETCore, версия = версии 5.0)<br/> -netstandard1.0 (. Моникеров NETStandard, Version = версия 1.0)<br/> -portable net45 + win8 + wp8 + wpa81 (. NETPortable, версия = v0.0 профиль = Profile259)<br/> -win8 (Windows, версия = версии 8.0)<br/> -wp8 (WindowsPhone, версия = версии 8.0)<br/> -wpa81 (WindowsPhoneApp, версия = v8.1)<br/> -xamarinios10 () Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="1d91d-248">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="1d91d-249">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-249">**Solution**</span></span> | <span data-ttu-id="1d91d-250">Изменения целевой платформы проекта на ту, которая поддерживает пакет.</span><span class="sxs-lookup"><span data-stu-id="1d91d-250">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="1d91d-251">NU1203</span><span class="sxs-lookup"><span data-stu-id="1d91d-251">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-252">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-252">**Issue**</span></span> | <span data-ttu-id="1d91d-253">Пакет не поддерживает проекта `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="1d91d-253">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="1d91d-254">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-254">**Example message**</span></span> | <span data-ttu-id="1d91d-255">*System.Example 1.0.0 обеспечивается компиляции ссылочную сборку для a.dll net461, но отсутствует совместимый сборка во время выполнения.*</span><span class="sxs-lookup"><span data-stu-id="1d91d-255">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="1d91d-256">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-256">**Solution**</span></span> | <span data-ttu-id="1d91d-257">Изменение `RuntimeIdentifier` значения, используемые в проекте, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="1d91d-257">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="1d91d-258">NU1401</span><span class="sxs-lookup"><span data-stu-id="1d91d-258">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-259">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-259">**Issue**</span></span> | <span data-ttu-id="1d91d-260">Для пакета требуется функции или платформ, в настоящее время не поддерживается установленной версией NuGet.</span><span class="sxs-lookup"><span data-stu-id="1d91d-260">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="1d91d-261">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-261">**Example message**</span></span> | <span data-ttu-id="1d91d-262">*Требует NuGet версии клиента "5.0.0» пакет «NuGet.Versioning» или выше, но текущая версия NuGet —"4.3.0».*</span><span class="sxs-lookup"><span data-stu-id="1d91d-262">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="1d91d-263">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-263">**Solution**</span></span> | <span data-ttu-id="1d91d-264">Установите более новую версию NuGet.</span><span class="sxs-lookup"><span data-stu-id="1d91d-264">Install a newer version of NuGet.</span></span> <span data-ttu-id="1d91d-265">В разделе [NuGet Установка клиентских средств](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="1d91d-265">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="1d91d-266">Недопустимый входной предупреждения</span><span class="sxs-lookup"><span data-stu-id="1d91d-266">Invalid input warnings</span></span>

<span data-ttu-id="1d91d-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="1d91d-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="1d91d-268">NU1501</span><span class="sxs-lookup"><span data-stu-id="1d91d-268">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-269">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-269">**Issue**</span></span> | <span data-ttu-id="1d91d-270">Восстановить проект пытается работать в не найден.</span><span class="sxs-lookup"><span data-stu-id="1d91d-270">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="1d91d-271">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-271">**Example message**</span></span> | <span data-ttu-id="1d91d-272">*Папка «c:\projects\a» не содержит проектов для восстановления.*</span><span class="sxs-lookup"><span data-stu-id="1d91d-272">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="1d91d-273">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-273">**Solution**</span></span> | <span data-ttu-id="1d91d-274">Выполните восстановление nuget в папке, которая содержит проект.</span><span class="sxs-lookup"><span data-stu-id="1d91d-274">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="1d91d-275">NU1502</span><span class="sxs-lookup"><span data-stu-id="1d91d-275">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-276">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-276">**Issue**</span></span> | <span data-ttu-id="1d91d-277">`RuntimeSupports` содержит недопустимый профиль.</span><span class="sxs-lookup"><span data-stu-id="1d91d-277">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="1d91d-278">Как правило, поддерживает профиль не найден в `runtime.json` файл из текущего зависимостей пакетов.</span><span class="sxs-lookup"><span data-stu-id="1d91d-278">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="1d91d-279">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-279">**Example message**</span></span> | <span data-ttu-id="1d91d-280">*Неизвестный совместимости профиля: aaa*</span><span class="sxs-lookup"><span data-stu-id="1d91d-280">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="1d91d-281">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-281">**Solution**</span></span> | <span data-ttu-id="1d91d-282">Проверьте `RuntimeSupports` значение в проекте.</span><span class="sxs-lookup"><span data-stu-id="1d91d-282">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="1d91d-283">NU1503</span><span class="sxs-lookup"><span data-stu-id="1d91d-283">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-284">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-284">**Issue**</span></span> | <span data-ttu-id="1d91d-285">Зависимости проекта не импортирует целевые объекты восстановления NuGet.</span><span class="sxs-lookup"><span data-stu-id="1d91d-285">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="1d91d-286">Это похоже на NU1105, но здесь пропускается проект и пропускаются, а не вызывает все восстановления к сбою.</span><span class="sxs-lookup"><span data-stu-id="1d91d-286">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="1d91d-287">В сложных решениях часто возникают других типов проектов, которые могут не поддерживать восстановления.</span><span class="sxs-lookup"><span data-stu-id="1d91d-287">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="1d91d-288">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-288">**Example message**</span></span> | <span data-ttu-id="1d91d-289">*Пропуск восстановления для проекта «c:\a.csproj». Файл проекта может быть недопустим или отсутствует целевые объекты, необходимые для восстановления.*</span><span class="sxs-lookup"><span data-stu-id="1d91d-289">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="1d91d-290">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-290">**Solution**</span></span> | <span data-ttu-id="1d91d-291">Это может произойти для проектов, которые не импортировать общие props/объекты, которые автоматически импортировать восстановления.</span><span class="sxs-lookup"><span data-stu-id="1d91d-291">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="1d91d-292">Если проект не нуждаются в восстановлении это сообщение можно проигнорировать.</span><span class="sxs-lookup"><span data-stu-id="1d91d-292">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="1d91d-293">В противном случае измените затронутых проект, чтобы добавить целевые объекты для восстановления.</span><span class="sxs-lookup"><span data-stu-id="1d91d-293">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="1d91d-294">Непредвиденная пакета версии предупреждения</span><span class="sxs-lookup"><span data-stu-id="1d91d-294">Unexpected package version warnings</span></span>

<span data-ttu-id="1d91d-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="1d91d-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="1d91d-296">NU1601</span><span class="sxs-lookup"><span data-stu-id="1d91d-296">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-297">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-297">**Issue**</span></span> | <span data-ttu-id="1d91d-298">Зависимость прямой проекта был увеличить на один на более позднюю версию, чем указанный проект.</span><span class="sxs-lookup"><span data-stu-id="1d91d-298">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="1d91d-299">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-299">**Example message**</span></span> | <span data-ttu-id="1d91d-300">*Указанная зависимость — NuGet.Versioning (> = 3.5.0), но завершено с NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="1d91d-300">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="1d91d-301">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-301">**Solution**</span></span> | <span data-ttu-id="1d91d-302">Обновление зависимостей в проекте соответствующей версии.</span><span class="sxs-lookup"><span data-stu-id="1d91d-302">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="1d91d-303">NU1602</span><span class="sxs-lookup"><span data-stu-id="1d91d-303">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-304">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-304">**Issue**</span></span> | <span data-ttu-id="1d91d-305">Зависимость пакета отсутствует нижняя граница.</span><span class="sxs-lookup"><span data-stu-id="1d91d-305">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="1d91d-306">Это не позволяет восстановления найти *наилучшего соответствия*.</span><span class="sxs-lookup"><span data-stu-id="1d91d-306">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="1d91d-307">Каждый восстановления будет находиться вниз при попытке найти более ранней версии, который может использоваться.</span><span class="sxs-lookup"><span data-stu-id="1d91d-307">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="1d91d-308">Это означает, что процесс восстановления в оперативный режим для проверки всех источников каждый раз, вместо того чтобы использовать пакеты, которые уже существуют в папке пользователя пакета.</span><span class="sxs-lookup"><span data-stu-id="1d91d-308">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="1d91d-309">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-309">**Example message**</span></span> | <span data-ttu-id="1d91d-310">*NuGet.Packaging 4.0.0 не предоставляет инклюзивную нижнюю границу для зависимостей NuGet.Versioning (> 3.5.0). Приблизительное наиболее подходящие 3.6.0 был разрешен.*</span><span class="sxs-lookup"><span data-stu-id="1d91d-310">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="1d91d-311">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-311">**Solution**</span></span> | <span data-ttu-id="1d91d-312">Обычно это пакет разработки ошибки.</span><span class="sxs-lookup"><span data-stu-id="1d91d-312">This is usually a package authoring error.</span></span> <span data-ttu-id="1d91d-313">Обратитесь к автору пакета для устранения проблемы.</span><span class="sxs-lookup"><span data-stu-id="1d91d-313">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="1d91d-314">NU1603</span><span class="sxs-lookup"><span data-stu-id="1d91d-314">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-315">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-315">**Issue**</span></span> | <span data-ttu-id="1d91d-316">Зависимость пакета указаны версии, не найден.</span><span class="sxs-lookup"><span data-stu-id="1d91d-316">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="1d91d-317">Как правило источники пакетов не содержат версии ожидаемый нижней границы.</span><span class="sxs-lookup"><span data-stu-id="1d91d-317">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="1d91d-318">Более поздняя версия вместо него используется, которая отличается от пакет был создан для.</span><span class="sxs-lookup"><span data-stu-id="1d91d-318">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="1d91d-319">Это означает, что восстановление не удалось найти *наилучшего соответствия*.</span><span class="sxs-lookup"><span data-stu-id="1d91d-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="1d91d-320">Каждый восстановления будет находиться вниз при попытке найти более ранней версии, который может использоваться.</span><span class="sxs-lookup"><span data-stu-id="1d91d-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="1d91d-321">Это означает, что процесс восстановления в оперативный режим для проверки всех источников каждый раз, вместо того чтобы использовать пакеты, которые уже существуют в папке пользователя пакета.</span><span class="sxs-lookup"><span data-stu-id="1d91d-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="1d91d-322">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-322">**Example message**</span></span> | <span data-ttu-id="1d91d-323">NuGet.Packaging 4.0.0 зависит от NuGet.Versioning (> = 4.0.0), но 4.0.0 не найден.</span><span class="sxs-lookup"><span data-stu-id="1d91d-323">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="1d91d-324">Приблизительное наиболее подходящие 5.0.0 был разрешен.</span><span class="sxs-lookup"><span data-stu-id="1d91d-324">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="1d91d-325">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-325">**Solution**</span></span> | <span data-ttu-id="1d91d-326">Если требуется пакет не был выпущен, это может быть ошибка создания пакета.</span><span class="sxs-lookup"><span data-stu-id="1d91d-326">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="1d91d-327">Обратитесь к автору пакета для устранения проблемы.</span><span class="sxs-lookup"><span data-stu-id="1d91d-327">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="1d91d-328">Если пакет запущен, проверьте, что он доступен на источники пакетов, которую вы используете.</span><span class="sxs-lookup"><span data-stu-id="1d91d-328">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="1d91d-329">При использовании закрытого источника, может потребоваться обновить пакет, веб-канала.</span><span class="sxs-lookup"><span data-stu-id="1d91d-329">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="1d91d-330">NU1604</span><span class="sxs-lookup"><span data-stu-id="1d91d-330">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-331">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-331">**Issue**</span></span> | <span data-ttu-id="1d91d-332">Зависимости проекта не определяет нижнюю границу.</span><span class="sxs-lookup"><span data-stu-id="1d91d-332">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="1d91d-333">Это означает, что восстановление не удалось найти *наилучшего соответствия*.</span><span class="sxs-lookup"><span data-stu-id="1d91d-333">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="1d91d-334">Каждый восстановления будет находиться вниз при попытке найти более ранней версии, который может использоваться.</span><span class="sxs-lookup"><span data-stu-id="1d91d-334">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="1d91d-335">Это означает, что процесс восстановления в оперативный режим для проверки всех источников каждый раз, вместо того чтобы использовать пакеты, которые уже существуют в папке пользователя пакета.</span><span class="sxs-lookup"><span data-stu-id="1d91d-335">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="1d91d-336">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-336">**Example message**</span></span> | <span data-ttu-id="1d91d-337">*Проект зависимостей NuGet.Versioning (< = от 9.0.0) doe содержит инклюзивную нижнюю границу. Включите нижняя граница в версию зависимостей для обеспечения восстановления, согласованные результаты.*</span><span class="sxs-lookup"><span data-stu-id="1d91d-337">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="1d91d-338">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-338">**Solution**</span></span> | <span data-ttu-id="1d91d-339">Обновление проекта `PackageReference` `Version` атрибут для включения нижней границы.</span><span class="sxs-lookup"><span data-stu-id="1d91d-339">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="1d91d-340">NU1605</span><span class="sxs-lookup"><span data-stu-id="1d91d-340">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-341">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-341">**Issue**</span></span> | <span data-ttu-id="1d91d-342">Пакета зависимостей указано ограничение версии на более поздняя версия пакета, чем для восстановления в конечном счете.</span><span class="sxs-lookup"><span data-stu-id="1d91d-342">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="1d91d-343">То есть из-за «ближайшего wins» правила при разрешении пакеты, ближе к пакета на диаграмме может был переопределен отдаленных пакета.</span><span class="sxs-lookup"><span data-stu-id="1d91d-343">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="1d91d-344">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-344">**Example message**</span></span> | <span data-ttu-id="1d91d-345">*Обнаружен пакет переход к более раннему: NuGet.Versioning из 4.0.0 для 3.5.0. Ссылающиеся на пакет непосредственно из проекта, чтобы выбрать другую версию.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="1d91d-345">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="1d91d-346">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-346">**Solution**</span></span> | <span data-ttu-id="1d91d-347">Добавьте прямую ссылку на проект для более новой версии пакета, который вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="1d91d-347">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="1d91d-348">Арбитр конфликтов предупреждения</span><span class="sxs-lookup"><span data-stu-id="1d91d-348">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="1d91d-349">NU1608</span><span class="sxs-lookup"><span data-stu-id="1d91d-349">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-350">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-350">**Issue**</span></span> | <span data-ttu-id="1d91d-351">Разрешить пакета превышает ограничение зависимостей позволяет.</span><span class="sxs-lookup"><span data-stu-id="1d91d-351">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="1d91d-352">Это означает, что пакет непосредственно ссылается проект переопределяет ограничения зависимостей от других пакетов.</span><span class="sxs-lookup"><span data-stu-id="1d91d-352">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="1d91d-353">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-353">**Example message**</span></span> | <span data-ttu-id="1d91d-354">*Версия пакета обнаруженных вне зависимости ограничение: x 1.0.0 требуется y (= 1.0.0), но версии y 2.0.0 был разрешен.*</span><span class="sxs-lookup"><span data-stu-id="1d91d-354">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="1d91d-355">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-355">**Solution**</span></span> | <span data-ttu-id="1d91d-356">В некоторых случаях это сделано намеренно, а предупреждение может быть отменено.</span><span class="sxs-lookup"><span data-stu-id="1d91d-356">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="1d91d-357">В противном случае измените ссылка проекта в пакет, чтобы расширить его ограничения версии.</span><span class="sxs-lookup"><span data-stu-id="1d91d-357">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="1d91d-358">Резервный предупреждения пакетов</span><span class="sxs-lookup"><span data-stu-id="1d91d-358">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="1d91d-359">NU1701</span><span class="sxs-lookup"><span data-stu-id="1d91d-359">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-360">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-360">**Issue**</span></span> | <span data-ttu-id="1d91d-361">`PackageTargetFallback` / `AssetTargetFallback` была использована для выбора средств из пакета.</span><span class="sxs-lookup"><span data-stu-id="1d91d-361">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="1d91d-362">Предупреждение Проинформируйте пользователей, ОС может быть не совместимы 100%.</span><span class="sxs-lookup"><span data-stu-id="1d91d-362">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="1d91d-363">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-363">**Example message**</span></span> | <span data-ttu-id="1d91d-364">*Пакет «NuGet.Versioning» был восстановлен, вместо этого использовать «portable net45 + win8» целевая платформа проекта «netstandard1.5». Этот пакет не может быть полностью совместим с проектом.*</span><span class="sxs-lookup"><span data-stu-id="1d91d-364">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="1d91d-365">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-365">**Solution**</span></span> | <span data-ttu-id="1d91d-366">Изменения целевой платформы проекта на ту, которая поддерживает пакет.</span><span class="sxs-lookup"><span data-stu-id="1d91d-366">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="1d91d-367">Предупреждения веб-канала</span><span class="sxs-lookup"><span data-stu-id="1d91d-367">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="1d91d-368">NU1801</span><span class="sxs-lookup"><span data-stu-id="1d91d-368">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-369">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-369">**Issue**</span></span> | <span data-ttu-id="1d91d-370">Произошла ошибка при чтении веб-канала при `IgnoreFailedSources` имеет значение true, преобразование ее устранимая предупреждение.</span><span class="sxs-lookup"><span data-stu-id="1d91d-370">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="1d91d-371">Это может содержать любые сообщения и является универсальным.</span><span class="sxs-lookup"><span data-stu-id="1d91d-371">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="1d91d-372">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-372">**Example message**</span></span> | <span data-ttu-id="1d91d-373">Н/Д</span><span class="sxs-lookup"><span data-stu-id="1d91d-373">n/a</span></span> |
| <span data-ttu-id="1d91d-374">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-374">**Solution**</span></span> | <span data-ttu-id="1d91d-375">Измените конфигурацию таким образом, чтобы указать допустимые источники.</span><span class="sxs-lookup"><span data-stu-id="1d91d-375">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="1d91d-376">NuGet внутренних ошибок и предупреждений</span><span class="sxs-lookup"><span data-stu-id="1d91d-376">NuGet internal errors and warnings</span></span>

<span data-ttu-id="1d91d-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="1d91d-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="1d91d-378">NU1000</span><span class="sxs-lookup"><span data-stu-id="1d91d-378">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-379">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-379">**Issue**</span></span> | <span data-ttu-id="1d91d-380">Неопределенный Внутренняя ошибка на NuGet.</span><span class="sxs-lookup"><span data-stu-id="1d91d-380">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="1d91d-381">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-381">**Solution**</span></span> | <span data-ttu-id="1d91d-382">Дополнительные сведения в журнале</span><span class="sxs-lookup"><span data-stu-id="1d91d-382">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="1d91d-383">NU1500</span><span class="sxs-lookup"><span data-stu-id="1d91d-383">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-384">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-384">**Issue**</span></span> | <span data-ttu-id="1d91d-385">Неопределенный внутренние предупреждения NuGet.</span><span class="sxs-lookup"><span data-stu-id="1d91d-385">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="1d91d-386">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-386">**Solution**</span></span> | <span data-ttu-id="1d91d-387">Дополнительные сведения в журнале</span><span class="sxs-lookup"><span data-stu-id="1d91d-387">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="1d91d-388">Подписанные пакеты (создания и проверки)</span><span class="sxs-lookup"><span data-stu-id="1d91d-388">Signed packages (creation and verification)</span></span>

<span data-ttu-id="1d91d-389">*NuGet 4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="1d91d-389">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="1d91d-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="1d91d-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="1d91d-391">NU3000</span><span class="sxs-lookup"><span data-stu-id="1d91d-391">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-392">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-392">**Issue**</span></span> | <span data-ttu-id="1d91d-393">Общая ошибка, связанные с Подписание пакета и подпись проверки пакета.</span><span class="sxs-lookup"><span data-stu-id="1d91d-393">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="1d91d-394">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-394">**Solution**</span></span> | <span data-ttu-id="1d91d-395">Дополнительные сведения в журнале.</span><span class="sxs-lookup"><span data-stu-id="1d91d-395">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="1d91d-396">NU3001</span><span class="sxs-lookup"><span data-stu-id="1d91d-396">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-397">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-397">**Issue**</span></span> | <span data-ttu-id="1d91d-398">Недопустимые аргументы либо [входа команда](../tools/cli-ref-sign.md) или [проверьте команду](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="1d91d-398">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="1d91d-399">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-399">**Solution**</span></span> | <span data-ttu-id="1d91d-400">Проверьте и исправьте передаваемых методу аргументов.</span><span class="sxs-lookup"><span data-stu-id="1d91d-400">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="1d91d-401">NU3002</span><span class="sxs-lookup"><span data-stu-id="1d91d-401">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-402">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-402">**Issue**</span></span> | <span data-ttu-id="1d91d-403">`-Timestamper` Не указан параметр с [входа команды nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="1d91d-403">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="1d91d-404">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-404">**Example message**</span></span> | <span data-ttu-id="1d91d-405">*"-Timestamper" параметр не указан. Подписанный пакет не будет отметку времени.*</span><span class="sxs-lookup"><span data-stu-id="1d91d-405">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="1d91d-406">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-406">**Solution**</span></span> | <span data-ttu-id="1d91d-407">Укажите `-Timestamper` вариант с `nuget sign`.</span><span class="sxs-lookup"><span data-stu-id="1d91d-407">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="1d91d-408">NU3004</span><span class="sxs-lookup"><span data-stu-id="1d91d-408">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-409">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-409">**Issue**</span></span> | <span data-ttu-id="1d91d-410">Пакет без знака, предоставленная [nuget проверьте команду](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="1d91d-410">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="1d91d-411">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-411">**Solution**</span></span> | <span data-ttu-id="1d91d-412">Запустите `nuget verify` с подписанных пакетов.</span><span class="sxs-lookup"><span data-stu-id="1d91d-412">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="1d91d-413">В разделе [подписать пакет](../create-packages/Sign-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="1d91d-413">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="1d91d-414">NU3008</span><span class="sxs-lookup"><span data-stu-id="1d91d-414">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-415">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-415">**Issue**</span></span> | <span data-ttu-id="1d91d-416">Сбой при проверке целостности пакета, это означает, что подписанного пакета было изменено при передаче с момента подписан.</span><span class="sxs-lookup"><span data-stu-id="1d91d-416">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="1d91d-417">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-417">**Solution**</span></span> | <span data-ttu-id="1d91d-418">Проверьте компьютер с помощью антивирусной программы.</span><span class="sxs-lookup"><span data-stu-id="1d91d-418">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="1d91d-419">Удалите пакет на компьютере, переустановите его и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="1d91d-419">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="1d91d-420">Если проблема сохранится, обратитесь к владельцу исходного пакета и владелец пакета.</span><span class="sxs-lookup"><span data-stu-id="1d91d-420">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="1d91d-421">NU3018</span><span class="sxs-lookup"><span data-stu-id="1d91d-421">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-422">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-422">**Issue**</span></span> | <span data-ttu-id="1d91d-423">Сбой при создании цепочки сертификатов для основной сигнатуры.</span><span class="sxs-lookup"><span data-stu-id="1d91d-423">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="1d91d-424">Основной сертификат подписи не является доверенным, отозван, или сведения об отзыве сертификата недоступен.</span><span class="sxs-lookup"><span data-stu-id="1d91d-424">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="1d91d-425">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-425">**Example message**</span></span> | <span data-ttu-id="1d91d-426">*Предупреждение: NU3018: функции отзыва не удалось проверить отзыв сертификата.*</span><span class="sxs-lookup"><span data-stu-id="1d91d-426">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="1d91d-427">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-427">**Solution**</span></span> | <span data-ttu-id="1d91d-428">Используйте доверенные и допустимый сертификат.</span><span class="sxs-lookup"><span data-stu-id="1d91d-428">Use a trusted and valid certificate.</span></span> <span data-ttu-id="1d91d-429">Проверьте подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="1d91d-429">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="1d91d-430">NU3028</span><span class="sxs-lookup"><span data-stu-id="1d91d-430">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1d91d-431">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="1d91d-431">**Issue**</span></span> | <span data-ttu-id="1d91d-432">Не удалось выполнить построения цепочки сертификатов для подписи отметки времени.</span><span class="sxs-lookup"><span data-stu-id="1d91d-432">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="1d91d-433">Сертификат подписи отметки времени не является доверенным, отозван, или сведения об отзыве сертификата недоступен.</span><span class="sxs-lookup"><span data-stu-id="1d91d-433">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="1d91d-434">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="1d91d-434">**Example message**</span></span> | <span data-ttu-id="1d91d-435">*Предупреждение: NU3028: функции отзыва не удалось проверить отзыв сертификата.*</span><span class="sxs-lookup"><span data-stu-id="1d91d-435">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="1d91d-436">**Решение**</span><span class="sxs-lookup"><span data-stu-id="1d91d-436">**Solution**</span></span> | <span data-ttu-id="1d91d-437">Используйте доверенные и допустимый сертификат.</span><span class="sxs-lookup"><span data-stu-id="1d91d-437">Use a trusted and valid certificate.</span></span> <span data-ttu-id="1d91d-438">Проверьте подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="1d91d-438">Check internet connectivity.</span></span> |
