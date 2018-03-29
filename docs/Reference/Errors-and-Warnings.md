---
title: Справочник предупреждения и ошибки NuGet | Документы Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Полный справочник для предупреждения и ошибки, выданные NuGet при выполнении различных операций NuGet.
keywords: NuGet ошибки, предупреждения NuGet диагностики
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
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
ms.openlocfilehash: 020e31dc8646c43b86bcee555f1772e8b1db7761
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="b50e8-104">Ошибки и предупреждения</span><span class="sxs-lookup"><span data-stu-id="b50e8-104">Errors and warnings</span></span>

<span data-ttu-id="b50e8-105">В NuGet 4.3.0+ ошибки и предупреждения нумеруются, как описано в этом разделе и предоставляют подробные сведения для решения проблемы, связанные.</span><span class="sxs-lookup"><span data-stu-id="b50e8-105">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="b50e8-106">Ошибки и предупреждения, перечисленные здесь доступны только с [на основе PackageReference](../consume-packages/package-references-in-project-files.md) проекты и NuGet 4.3.0+.</span><span class="sxs-lookup"><span data-stu-id="b50e8-106">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="b50e8-107">NuGet также учитывает свойства MSBuild для предупреждений или повысить их к ошибкам.</span><span class="sxs-lookup"><span data-stu-id="b50e8-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="b50e8-108">Дополнительные сведения см. в разделе [как: отключить предупреждения компилятора](/visualstudio/ide/how-to-suppress-compiler-warnings) в документации по Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b50e8-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="b50e8-109">**Ошибки**</span><span class="sxs-lookup"><span data-stu-id="b50e8-109">**Errors**</span></span>

| <span data-ttu-id="b50e8-110">Группа</span><span class="sxs-lookup"><span data-stu-id="b50e8-110">Group</span></span> | <span data-ttu-id="b50e8-111">Номера ошибок</span><span class="sxs-lookup"><span data-stu-id="b50e8-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="b50e8-112">Недопустимый ошибок ввода</span><span class="sxs-lookup"><span data-stu-id="b50e8-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="b50e8-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="b50e8-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="b50e8-114">Отсутствуют ошибки пакетов и проектов</span><span class="sxs-lookup"><span data-stu-id="b50e8-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="b50e8-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (ранее NU1607), [NU1108](#nu1108) (ранее NU1606)</span><span class="sxs-lookup"><span data-stu-id="b50e8-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="b50e8-116">Ошибки совместимости</span><span class="sxs-lookup"><span data-stu-id="b50e8-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="b50e8-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="b50e8-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="b50e8-118">**Предупреждения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-118">**Warnings**</span></span>

| <span data-ttu-id="b50e8-119">Группа</span><span class="sxs-lookup"><span data-stu-id="b50e8-119">Group</span></span> | <span data-ttu-id="b50e8-120">Номеров предупреждений</span><span class="sxs-lookup"><span data-stu-id="b50e8-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="b50e8-121">Недопустимый входной предупреждения</span><span class="sxs-lookup"><span data-stu-id="b50e8-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="b50e8-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="b50e8-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="b50e8-123">Непредвиденная пакета версии предупреждения</span><span class="sxs-lookup"><span data-stu-id="b50e8-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="b50e8-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="b50e8-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="b50e8-125">Арбитр конфликтов предупреждения</span><span class="sxs-lookup"><span data-stu-id="b50e8-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="b50e8-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="b50e8-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="b50e8-127">Резервный предупреждения пакетов</span><span class="sxs-lookup"><span data-stu-id="b50e8-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="b50e8-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="b50e8-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="b50e8-129">Предупреждения веб-канала</span><span class="sxs-lookup"><span data-stu-id="b50e8-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="b50e8-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="b50e8-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="b50e8-131">NuGet внутренних ошибок и предупреждений</span><span class="sxs-lookup"><span data-stu-id="b50e8-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="b50e8-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="b50e8-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="b50e8-133">Подписанные пакеты (создания и проверки)</span><span class="sxs-lookup"><span data-stu-id="b50e8-133">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="b50e8-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="b50e8-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="b50e8-135">Недопустимый ошибок ввода</span><span class="sxs-lookup"><span data-stu-id="b50e8-135">Invalid input errors</span></span>

<span data-ttu-id="b50e8-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="b50e8-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="b50e8-137">NU1001</span><span class="sxs-lookup"><span data-stu-id="b50e8-137">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-138">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-138">**Issue**</span></span> | <span data-ttu-id="b50e8-139">Проект не содержит один или несколько платформ.</span><span class="sxs-lookup"><span data-stu-id="b50e8-139">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="b50e8-140">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-140">**Example message**</span></span> | <span data-ttu-id="b50e8-141">*ProjA проекта не указывает целевые платформы в c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="b50e8-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="b50e8-142">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-142">**Solution**</span></span> | <span data-ttu-id="b50e8-143">Добавить `TargetFramework` или `TargetFrameworks` свойства для указанного файла проекта.</span><span class="sxs-lookup"><span data-stu-id="b50e8-143">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="b50e8-144">NU1002</span><span class="sxs-lookup"><span data-stu-id="b50e8-144">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-145">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-145">**Issue**</span></span> | <span data-ttu-id="b50e8-146">Недопустимое сочетание входных данных вместе с ключевым словом, снимите ФЛАЖОК.</span><span class="sxs-lookup"><span data-stu-id="b50e8-146">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="b50e8-147">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-147">**Example message**</span></span> | <span data-ttu-id="b50e8-148">*«CLEAR» не может использоваться в сочетании с другими значениями*</span><span class="sxs-lookup"><span data-stu-id="b50e8-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="b50e8-149">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-149">**Solution**</span></span> | <span data-ttu-id="b50e8-150">Использовать СНИМИТЕ сам по себе и опустить остальные потоки входа.</span><span class="sxs-lookup"><span data-stu-id="b50e8-150">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="b50e8-151">NU1003</span><span class="sxs-lookup"><span data-stu-id="b50e8-151">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-152">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-152">**Issue**</span></span> | <span data-ttu-id="b50e8-153">`PackageTargetFallback` и `AssetTargetFallback` поддержки разных режимов работы для выбора средств и не могут использоваться вместе.</span><span class="sxs-lookup"><span data-stu-id="b50e8-153">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="b50e8-154">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-154">**Example message**</span></span> | <span data-ttu-id="b50e8-155">*PackageTargetFallback и AssetTargetFallback не может использоваться вместе. Удалите PackageTargetFallback(deprecated) ссылки из проекта среды.*</span><span class="sxs-lookup"><span data-stu-id="b50e8-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="b50e8-156">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-156">**Solution**</span></span> | <span data-ttu-id="b50e8-157">Удалить устаревшие `PackageTargetFallback` элемент из проекта.</span><span class="sxs-lookup"><span data-stu-id="b50e8-157">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="b50e8-158">Отсутствуют ошибки пакетов и проектов</span><span class="sxs-lookup"><span data-stu-id="b50e8-158">Missing package and project errors</span></span>

<span data-ttu-id="b50e8-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="b50e8-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="b50e8-160">NU1100</span><span class="sxs-lookup"><span data-stu-id="b50e8-160">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-161">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-161">**Issue**</span></span> | <span data-ttu-id="b50e8-162">Не удается разрешить группе зависимостей.</span><span class="sxs-lookup"><span data-stu-id="b50e8-162">A dependency group not be resolved.</span></span> <span data-ttu-id="b50e8-163">Это проблема универсальных типов, которые не являются пакетами или проектов.</span><span class="sxs-lookup"><span data-stu-id="b50e8-163">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="b50e8-164">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-164">**Example message**</span></span> | <span data-ttu-id="b50e8-165">*Не удается разрешить System.Missing для net45*</span><span class="sxs-lookup"><span data-stu-id="b50e8-165">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="b50e8-166">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-166">**Solution**</span></span> | <span data-ttu-id="b50e8-167">Откройте файл проекта и просмотрите список его зависимостей.</span><span class="sxs-lookup"><span data-stu-id="b50e8-167">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="b50e8-168">Проверьте наличие каждой зависимости на источники пакетов, которую вы используете, и что пакет поддерживает целевая платформа проекта.</span><span class="sxs-lookup"><span data-stu-id="b50e8-168">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="b50e8-169">NU1101</span><span class="sxs-lookup"><span data-stu-id="b50e8-169">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-170">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-170">**Issue**</span></span> | <span data-ttu-id="b50e8-171">Не удается найти пакет на любые источники.</span><span class="sxs-lookup"><span data-stu-id="b50e8-171">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="b50e8-172">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-172">**Example message**</span></span> | <span data-ttu-id="b50e8-173">*Не удалось найти пакет System.Missing. Пакеты не существовать с этим идентификатором в источниках: dotnet core, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="b50e8-173">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="b50e8-174">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-174">**Solution**</span></span> | <span data-ttu-id="b50e8-175">Проверьте зависимости проекта в Visual Studio, чтобы убедиться в том, что вы используете правильный пакет идентификатор и номер версии.</span><span class="sxs-lookup"><span data-stu-id="b50e8-175">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="b50e8-176">Также убедитесь, что [конфигурация NuGet](../consume-packages/Configuring-NuGet-Behavior.md) определяет источники пакетов вашей предполагается использовать.</span><span class="sxs-lookup"><span data-stu-id="b50e8-176">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="b50e8-177">Если вы используете пакеты, имеющие [семантического управления версиями 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), убедитесь в том, что вы используете [V3 веб-канал](https://api.nuget.org/v3/index.json) в [конфигурация NuGet](../consume-packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="b50e8-177">If you use packages that have [Semantic Versioning 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), please make sure that you are using the [V3 feed](https://api.nuget.org/v3/index.json) in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="b50e8-178">NU1102</span><span class="sxs-lookup"><span data-stu-id="b50e8-178">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-179">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-179">**Issue**</span></span> | <span data-ttu-id="b50e8-180">Найти идентификатор пакета, но не удается найти версию в пределах диапазона задана зависимость на любом из источников.</span><span class="sxs-lookup"><span data-stu-id="b50e8-180">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="b50e8-181">Диапазон может быть указана в пакете и не пользователем.</span><span class="sxs-lookup"><span data-stu-id="b50e8-181">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="b50e8-182">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-182">**Example message**</span></span> | <span data-ttu-id="b50e8-183">*Не удалось найти пакет NuGet.Versioning версии (> = 9.0.1)<br/> -версии найден 30 в nuget.org [ближайшего версии: 4.0.0]<br/> -версии 10 найдено в dotnet buildtools [ближайшего версии: 4.0.0-rc-2129]<br/> -найдено 9 версии в NuGetVolatile [ближайшего версии: 3.0.0-beta-00032]<br/> -найдено 0 версии ядра dotnet<br/> -найдено 0 версии в dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="b50e8-183">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="b50e8-184">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-184">**Solution**</span></span> | <span data-ttu-id="b50e8-185">В файле проекта исправление версии пакета.</span><span class="sxs-lookup"><span data-stu-id="b50e8-185">Edit the project file to correct the package version.</span></span> <span data-ttu-id="b50e8-186">Также убедитесь, что [конфигурация NuGet](../consume-packages/Configuring-NuGet-Behavior.md) определяет источники пакетов вашей предполагается использовать.</span><span class="sxs-lookup"><span data-stu-id="b50e8-186">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="b50e8-187">Может потребоваться изменить версию requeted, если этот пакет находится непосредственно ссылается проект.</span><span class="sxs-lookup"><span data-stu-id="b50e8-187">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="b50e8-188">NU1103</span><span class="sxs-lookup"><span data-stu-id="b50e8-188">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-189">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-189">**Issue**</span></span> | <span data-ttu-id="b50e8-190">Проект указан стабильная версия для диапазона зависимостей, но не стабильной версии не найдены в этом диапазоне.</span><span class="sxs-lookup"><span data-stu-id="b50e8-190">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="b50e8-191">Предварительные версии найдены, однако не допускаются.</span><span class="sxs-lookup"><span data-stu-id="b50e8-191">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="b50e8-192">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-192">**Example message**</span></span> | <span data-ttu-id="b50e8-193">*Не удается найти стабильного пакета NuGet.Versioning с версией (> = 3.0.0)<br/> -версии 10 найдено в dotnet buildtools [ближайшего версии: 4.0.0-rc-2129]<br/> -версии 9 найден в NuGetVolatile [ближайшего версии: 3.0.0-beta-00032] <br/> -Найдено 0 версии ядра dotnet<br/> -найдено 0 версии в dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="b50e8-193">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="b50e8-194">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-194">**Solution**</span></span> |  <span data-ttu-id="b50e8-195">Измените диапазон версий в файле проекта для включения предварительных версий.</span><span class="sxs-lookup"><span data-stu-id="b50e8-195">Edit the version range in the project file to include pre-release versions.</span></span> <span data-ttu-id="b50e8-196">В разделе [управления версиями пакета](../reference/Package-Versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b50e8-196">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="b50e8-197">NU1104</span><span class="sxs-lookup"><span data-stu-id="b50e8-197">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-198">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-198">**Issue**</span></span> | <span data-ttu-id="b50e8-199">Ссылкунапроект указывает на файл, который не существует.</span><span class="sxs-lookup"><span data-stu-id="b50e8-199">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="b50e8-200">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-200">**Example message**</span></span> | <span data-ttu-id="b50e8-201">*Ссылки на проект «c:\a.csproj» не существует. Проверьте допустимость ссылку на проект и существование файла проекта.*</span><span class="sxs-lookup"><span data-stu-id="b50e8-201">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="b50e8-202">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-202">**Solution**</span></span> | <span data-ttu-id="b50e8-203">Измените файл проекта, либо измените путь к ссылке проекта или удалить ссылку, если он больше не нужен.</span><span class="sxs-lookup"><span data-stu-id="b50e8-203">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="b50e8-204">NU1105</span><span class="sxs-lookup"><span data-stu-id="b50e8-204">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-205">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-205">**Issue**</span></span> | <span data-ttu-id="b50e8-206">Файл проекта существует, но не данные восстановления не указаны для него.</span><span class="sxs-lookup"><span data-stu-id="b50e8-206">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="b50e8-207">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-207">**Example message**</span></span> | <span data-ttu-id="b50e8-208">*Не удается прочитать сведения о проекте для «c:\a.csproj». Файл проекта может быть недопустим или отсутствует целевые объекты, необходимые для восстановления.*</span><span class="sxs-lookup"><span data-stu-id="b50e8-208">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="b50e8-209">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-209">**Solution**</span></span> | <span data-ttu-id="b50e8-210">В Visual Studio ошибка может означать, что проект будет выгружен в этом случае перезагрузить проект.</span><span class="sxs-lookup"><span data-stu-id="b50e8-210">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="b50e8-211">Из командной строки, это может означать, что файл поврежден или не содержит пользовательский «после импорта» целевой для восстановления для чтения проекта.</span><span class="sxs-lookup"><span data-stu-id="b50e8-211">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="b50e8-212">Убедитесь, что файл проекта является допустимым и содержит целевой объект «по окончании imports».</span><span class="sxs-lookup"><span data-stu-id="b50e8-212">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="b50e8-213">NU1106</span><span class="sxs-lookup"><span data-stu-id="b50e8-213">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-214">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-214">**Issue**</span></span> | <span data-ttu-id="b50e8-215">Ограничений на зависимости невозможно разрешить.</span><span class="sxs-lookup"><span data-stu-id="b50e8-215">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="b50e8-216">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-216">**Example message**</span></span> | <span data-ttu-id="b50e8-217">*Не удалось удовлетворить конфликтующие запросы для {id}: {конфликт путь} Framework: {целевого графа}*</span><span class="sxs-lookup"><span data-stu-id="b50e8-217">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |
| <span data-ttu-id="b50e8-218">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-218">**Solution**</span></span> | <span data-ttu-id="b50e8-219">В файле проекта для указания диапазона больше зависимостей, а не точную версию.</span><span class="sxs-lookup"><span data-stu-id="b50e8-219">Edit the project file to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="b50e8-220">NU1107 (ранее NU1607)</span><span class="sxs-lookup"><span data-stu-id="b50e8-220">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-221">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-221">**Issue**</span></span> | <span data-ttu-id="b50e8-222">Не удается разрешить ограничений на зависимости между пакетами.</span><span class="sxs-lookup"><span data-stu-id="b50e8-222">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="b50e8-223">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-223">**Example message**</span></span> | <span data-ttu-id="b50e8-224">*Для NuGet.Versioning обнаружен конфликт версий. Непосредственно из проекта, чтобы устранить эту проблему, ссылающиеся на пакет.<br/>  NuGet.Packaging 3.5.0 -> (= 3.5.0) NuGet.Versioning<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="b50e8-224">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="b50e8-225">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-225">**Solution**</span></span> | <span data-ttu-id="b50e8-226">Пакеты с ограничениями зависимостей точные версии не позволяют увеличить версии, при необходимости другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="b50e8-226">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="b50e8-227">Добавьте ссылку на проект напрямую (в файле проекта) к той самой версии требуется.</span><span class="sxs-lookup"><span data-stu-id="b50e8-227">Add a reference to the project directly (in the project file) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="b50e8-228">NU1108 (ранее NU1606)</span><span class="sxs-lookup"><span data-stu-id="b50e8-228">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-229">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-229">**Issue**</span></span> | <span data-ttu-id="b50e8-230">Обнаружена циклическая зависимость.</span><span class="sxs-lookup"><span data-stu-id="b50e8-230">A circular dependency was detected.</span></span> |
| <span data-ttu-id="b50e8-231">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-231">**Example message**</span></span> | <span data-ttu-id="b50e8-232">*Обнаружен цикл: A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="b50e8-232">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="b50e8-233">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-233">**Solution**</span></span> | <span data-ttu-id="b50e8-234">Пакет создается неправильно; Обратитесь к владельцу пакета, чтобы исправить ошибку.</span><span class="sxs-lookup"><span data-stu-id="b50e8-234">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="b50e8-235">Ошибки совместимости</span><span class="sxs-lookup"><span data-stu-id="b50e8-235">Compatibility errors</span></span>

<span data-ttu-id="b50e8-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="b50e8-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="b50e8-237">NU1201</span><span class="sxs-lookup"><span data-stu-id="b50e8-237">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-238">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-238">**Issue**</span></span> | <span data-ttu-id="b50e8-239">Зависимости проекта не содержит framework, совместимый с текущим проектом.</span><span class="sxs-lookup"><span data-stu-id="b50e8-239">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="b50e8-240">Как правило с целевой платформой проекта является более поздней версии, чем проект потребителя.</span><span class="sxs-lookup"><span data-stu-id="b50e8-240">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="b50e8-241">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-241">**Example message**</span></span> | <span data-ttu-id="b50e8-242">*ServerWeb проект несовместим с netstandard1.3 (. Моникеров NETStandard, Version = версия 1.3). Проект поддерживает ServerWeb:<br/> -netstandard1.6 (. Моникеров NETStandard, версия = версии 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = версия 1.0)*</span><span class="sxs-lookup"><span data-stu-id="b50e8-242">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="b50e8-243">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-243">**Solution**</span></span> | <span data-ttu-id="b50e8-244">Изменения целевой платформы проекта для версии равно или ниже, чем требуется много проекта.</span><span class="sxs-lookup"><span data-stu-id="b50e8-244">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="b50e8-245">NU1202</span><span class="sxs-lookup"><span data-stu-id="b50e8-245">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-246">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-246">**Issue**</span></span> | <span data-ttu-id="b50e8-247">Зависимость пакета не содержит все активы, совместимые с проектом.</span><span class="sxs-lookup"><span data-stu-id="b50e8-247">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="b50e8-248">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-248">**Example message**</span></span> | <span data-ttu-id="b50e8-249">*Пакет System.ComponentModel.EventBasedAsync 4.0.11 не совместим с netstandard1.3 (. Моникеров NETStandard, Version = версия 1.3). Пакет поддерживает System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, Version = версия 1.0)<br/> -monotouch10 (MonoTouch, версия = версия 1.0)<br/> -net45 (. NETFramework, версия = v4.5)<br/> -netcore50 (. NETCore, версия = версии 5.0)<br/> -netstandard1.0 (. Моникеров NETStandard, Version = версия 1.0)<br/> -portable net45 + win8 + wp8 + wpa81 (. NETPortable, версия = v0.0 профиль = Profile259)<br/> -win8 (Windows, версия = версии 8.0)<br/> -wp8 (WindowsPhone, версия = версии 8.0)<br/> -wpa81 (WindowsPhoneApp, версия = v8.1)<br/> -xamarinios10 () Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="b50e8-249">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="b50e8-250">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-250">**Solution**</span></span> | <span data-ttu-id="b50e8-251">Изменения целевой платформы проекта на ту, которая поддерживает пакет.</span><span class="sxs-lookup"><span data-stu-id="b50e8-251">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="b50e8-252">NU1203</span><span class="sxs-lookup"><span data-stu-id="b50e8-252">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-253">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-253">**Issue**</span></span> | <span data-ttu-id="b50e8-254">Пакет не поддерживает проекта `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="b50e8-254">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="b50e8-255">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-255">**Example message**</span></span> | <span data-ttu-id="b50e8-256">*System.Example 1.0.0 обеспечивается компиляции ссылочную сборку для a.dll net461, но отсутствует совместимый сборка во время выполнения.*</span><span class="sxs-lookup"><span data-stu-id="b50e8-256">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="b50e8-257">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-257">**Solution**</span></span> | <span data-ttu-id="b50e8-258">Изменение `RuntimeIdentifier` значения, используемые в проекте, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="b50e8-258">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="b50e8-259">NU1401</span><span class="sxs-lookup"><span data-stu-id="b50e8-259">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-260">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-260">**Issue**</span></span> | <span data-ttu-id="b50e8-261">Для пакета требуется функции или платформ, в настоящее время не поддерживается установленной версией NuGet.</span><span class="sxs-lookup"><span data-stu-id="b50e8-261">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="b50e8-262">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-262">**Example message**</span></span> | <span data-ttu-id="b50e8-263">*Требует NuGet версии клиента "5.0.0» пакет «NuGet.Versioning» или выше, но текущая версия NuGet —"4.3.0».*</span><span class="sxs-lookup"><span data-stu-id="b50e8-263">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="b50e8-264">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-264">**Solution**</span></span> | <span data-ttu-id="b50e8-265">Установите более новую версию NuGet.</span><span class="sxs-lookup"><span data-stu-id="b50e8-265">Install a newer version of NuGet.</span></span> <span data-ttu-id="b50e8-266">В разделе [NuGet Установка клиентских средств](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="b50e8-266">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="b50e8-267">Недопустимый входной предупреждения</span><span class="sxs-lookup"><span data-stu-id="b50e8-267">Invalid input warnings</span></span>

<span data-ttu-id="b50e8-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="b50e8-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="b50e8-269">NU1501</span><span class="sxs-lookup"><span data-stu-id="b50e8-269">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-270">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-270">**Issue**</span></span> | <span data-ttu-id="b50e8-271">Восстановить проект пытается работать в не найден.</span><span class="sxs-lookup"><span data-stu-id="b50e8-271">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="b50e8-272">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-272">**Example message**</span></span> | <span data-ttu-id="b50e8-273">*Папка «c:\projects\a» не содержит проектов для восстановления.*</span><span class="sxs-lookup"><span data-stu-id="b50e8-273">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="b50e8-274">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-274">**Solution**</span></span> | <span data-ttu-id="b50e8-275">Выполните восстановление nuget в папке, которая содержит проект.</span><span class="sxs-lookup"><span data-stu-id="b50e8-275">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="b50e8-276">NU1502</span><span class="sxs-lookup"><span data-stu-id="b50e8-276">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-277">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-277">**Issue**</span></span> | <span data-ttu-id="b50e8-278">`RuntimeSupports` содержит недопустимый профиль.</span><span class="sxs-lookup"><span data-stu-id="b50e8-278">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="b50e8-279">Как правило, поддерживает профиль не найден в `runtime.json` файл из текущего зависимостей пакетов.</span><span class="sxs-lookup"><span data-stu-id="b50e8-279">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="b50e8-280">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-280">**Example message**</span></span> | <span data-ttu-id="b50e8-281">*Неизвестный совместимости профиля: aaa*</span><span class="sxs-lookup"><span data-stu-id="b50e8-281">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="b50e8-282">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-282">**Solution**</span></span> | <span data-ttu-id="b50e8-283">Проверьте `RuntimeSupports` значение в проекте.</span><span class="sxs-lookup"><span data-stu-id="b50e8-283">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="b50e8-284">NU1503</span><span class="sxs-lookup"><span data-stu-id="b50e8-284">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-285">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-285">**Issue**</span></span> | <span data-ttu-id="b50e8-286">Зависимости проекта не импортирует целевые объекты восстановления NuGet.</span><span class="sxs-lookup"><span data-stu-id="b50e8-286">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="b50e8-287">Это похоже на NU1105, но здесь пропускается проект и пропускаются, а не вызывает все восстановления к сбою.</span><span class="sxs-lookup"><span data-stu-id="b50e8-287">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="b50e8-288">В сложных решениях часто возникают других типов проектов, которые могут не поддерживать восстановления.</span><span class="sxs-lookup"><span data-stu-id="b50e8-288">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="b50e8-289">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-289">**Example message**</span></span> | <span data-ttu-id="b50e8-290">*Пропуск восстановления для проекта «c:\a.csproj». Файл проекта может быть недопустим или отсутствует целевые объекты, необходимые для восстановления.*</span><span class="sxs-lookup"><span data-stu-id="b50e8-290">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="b50e8-291">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-291">**Solution**</span></span> | <span data-ttu-id="b50e8-292">Это может произойти для проектов, которые не импортировать общие props/объекты, которые автоматически импортировать восстановления.</span><span class="sxs-lookup"><span data-stu-id="b50e8-292">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="b50e8-293">Если проект не нуждаются в восстановлении это сообщение можно проигнорировать.</span><span class="sxs-lookup"><span data-stu-id="b50e8-293">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="b50e8-294">В противном случае измените затронутых проект, чтобы добавить целевые объекты для восстановления.</span><span class="sxs-lookup"><span data-stu-id="b50e8-294">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="b50e8-295">Непредвиденная пакета версии предупреждения</span><span class="sxs-lookup"><span data-stu-id="b50e8-295">Unexpected package version warnings</span></span>

<span data-ttu-id="b50e8-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="b50e8-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="b50e8-297">NU1601</span><span class="sxs-lookup"><span data-stu-id="b50e8-297">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-298">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-298">**Issue**</span></span> | <span data-ttu-id="b50e8-299">Зависимость прямой проекта был увеличить на один на более позднюю версию, чем указанный проект.</span><span class="sxs-lookup"><span data-stu-id="b50e8-299">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="b50e8-300">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-300">**Example message**</span></span> | <span data-ttu-id="b50e8-301">*Указанная зависимость — NuGet.Versioning (> = 3.5.0), но завершено с NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="b50e8-301">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="b50e8-302">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-302">**Solution**</span></span> | <span data-ttu-id="b50e8-303">Обновление зависимостей в проекте соответствующей версии.</span><span class="sxs-lookup"><span data-stu-id="b50e8-303">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="b50e8-304">NU1602</span><span class="sxs-lookup"><span data-stu-id="b50e8-304">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-305">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-305">**Issue**</span></span> | <span data-ttu-id="b50e8-306">Зависимость пакета отсутствует нижняя граница.</span><span class="sxs-lookup"><span data-stu-id="b50e8-306">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="b50e8-307">Это не позволяет восстановления найти *наилучшего соответствия*.</span><span class="sxs-lookup"><span data-stu-id="b50e8-307">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="b50e8-308">Каждый восстановления будет находиться вниз при попытке найти более ранней версии, который может использоваться.</span><span class="sxs-lookup"><span data-stu-id="b50e8-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="b50e8-309">Это означает, что процесс восстановления в оперативный режим для проверки всех источников каждый раз, вместо того чтобы использовать пакеты, которые уже существуют в папке пользователя пакета.</span><span class="sxs-lookup"><span data-stu-id="b50e8-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="b50e8-310">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-310">**Example message**</span></span> | <span data-ttu-id="b50e8-311">*NuGet.Packaging 4.0.0 не предоставляет инклюзивную нижнюю границу для зависимостей NuGet.Versioning (> 3.5.0). Приблизительное наиболее подходящие 3.6.0 был разрешен.*</span><span class="sxs-lookup"><span data-stu-id="b50e8-311">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="b50e8-312">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-312">**Solution**</span></span> | <span data-ttu-id="b50e8-313">Обычно это пакет разработки ошибки.</span><span class="sxs-lookup"><span data-stu-id="b50e8-313">This is usually a package authoring error.</span></span> <span data-ttu-id="b50e8-314">Обратитесь к автору пакета для устранения проблемы.</span><span class="sxs-lookup"><span data-stu-id="b50e8-314">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="b50e8-315">NU1603</span><span class="sxs-lookup"><span data-stu-id="b50e8-315">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-316">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-316">**Issue**</span></span> | <span data-ttu-id="b50e8-317">Зависимость пакета указаны версии, не найден.</span><span class="sxs-lookup"><span data-stu-id="b50e8-317">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="b50e8-318">Как правило источники пакетов не содержат версии ожидаемый нижней границы.</span><span class="sxs-lookup"><span data-stu-id="b50e8-318">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="b50e8-319">Более поздняя версия вместо него используется, которая отличается от пакет был создан для.</span><span class="sxs-lookup"><span data-stu-id="b50e8-319">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="b50e8-320">Это означает, что восстановление не удалось найти *наилучшего соответствия*.</span><span class="sxs-lookup"><span data-stu-id="b50e8-320">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="b50e8-321">Каждый восстановления будет находиться вниз при попытке найти более ранней версии, который может использоваться.</span><span class="sxs-lookup"><span data-stu-id="b50e8-321">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="b50e8-322">Это означает, что процесс восстановления в оперативный режим для проверки всех источников каждый раз, вместо того чтобы использовать пакеты, которые уже существуют в папке пользователя пакета.</span><span class="sxs-lookup"><span data-stu-id="b50e8-322">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="b50e8-323">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-323">**Example message**</span></span> | <span data-ttu-id="b50e8-324">NuGet.Packaging 4.0.0 зависит от NuGet.Versioning (> = 4.0.0), но 4.0.0 не найден.</span><span class="sxs-lookup"><span data-stu-id="b50e8-324">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="b50e8-325">Приблизительное наиболее подходящие 5.0.0 был разрешен.</span><span class="sxs-lookup"><span data-stu-id="b50e8-325">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="b50e8-326">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-326">**Solution**</span></span> | <span data-ttu-id="b50e8-327">Если требуется пакет не был выпущен, это может быть ошибка создания пакета.</span><span class="sxs-lookup"><span data-stu-id="b50e8-327">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="b50e8-328">Обратитесь к автору пакета для устранения проблемы.</span><span class="sxs-lookup"><span data-stu-id="b50e8-328">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="b50e8-329">Если пакет запущен, проверьте, что он доступен на источники пакетов, которую вы используете.</span><span class="sxs-lookup"><span data-stu-id="b50e8-329">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="b50e8-330">При использовании закрытого источника, может потребоваться обновить пакет, веб-канала.</span><span class="sxs-lookup"><span data-stu-id="b50e8-330">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="b50e8-331">NU1604</span><span class="sxs-lookup"><span data-stu-id="b50e8-331">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-332">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-332">**Issue**</span></span> | <span data-ttu-id="b50e8-333">Зависимости проекта не определяет нижнюю границу.</span><span class="sxs-lookup"><span data-stu-id="b50e8-333">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="b50e8-334">Это означает, что восстановление не удалось найти *наилучшего соответствия*.</span><span class="sxs-lookup"><span data-stu-id="b50e8-334">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="b50e8-335">Каждый восстановления будет находиться вниз при попытке найти более ранней версии, который может использоваться.</span><span class="sxs-lookup"><span data-stu-id="b50e8-335">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="b50e8-336">Это означает, что процесс восстановления в оперативный режим для проверки всех источников каждый раз, вместо того чтобы использовать пакеты, которые уже существуют в папке пользователя пакета.</span><span class="sxs-lookup"><span data-stu-id="b50e8-336">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="b50e8-337">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-337">**Example message**</span></span> | <span data-ttu-id="b50e8-338">*Проект зависимостей NuGet.Versioning (< = от 9.0.0) doe содержит инклюзивную нижнюю границу. Включите нижняя граница в версию зависимостей для обеспечения восстановления, согласованные результаты.*</span><span class="sxs-lookup"><span data-stu-id="b50e8-338">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="b50e8-339">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-339">**Solution**</span></span> | <span data-ttu-id="b50e8-340">Обновление проекта `PackageReference` `Version` атрибут для включения нижней границы.</span><span class="sxs-lookup"><span data-stu-id="b50e8-340">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="b50e8-341">NU1605</span><span class="sxs-lookup"><span data-stu-id="b50e8-341">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-342">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-342">**Issue**</span></span> | <span data-ttu-id="b50e8-343">Пакета зависимостей указано ограничение версии на более поздняя версия пакета, чем для восстановления в конечном счете.</span><span class="sxs-lookup"><span data-stu-id="b50e8-343">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="b50e8-344">То есть из-за «ближайшего wins» правила при разрешении пакеты, ближе к пакета на диаграмме может был переопределен отдаленных пакета.</span><span class="sxs-lookup"><span data-stu-id="b50e8-344">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="b50e8-345">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-345">**Example message**</span></span> | <span data-ttu-id="b50e8-346">*Обнаружен пакет переход к более раннему: NuGet.Versioning из 4.0.0 для 3.5.0. Ссылающиеся на пакет непосредственно из проекта, чтобы выбрать другую версию.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="b50e8-346">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="b50e8-347">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-347">**Solution**</span></span> | <span data-ttu-id="b50e8-348">Добавьте прямую ссылку на проект для более новой версии пакета, который вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="b50e8-348">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="b50e8-349">Арбитр конфликтов предупреждения</span><span class="sxs-lookup"><span data-stu-id="b50e8-349">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="b50e8-350">NU1608</span><span class="sxs-lookup"><span data-stu-id="b50e8-350">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-351">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-351">**Issue**</span></span> | <span data-ttu-id="b50e8-352">Разрешить пакета превышает ограничение зависимостей позволяет.</span><span class="sxs-lookup"><span data-stu-id="b50e8-352">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="b50e8-353">Это означает, что пакет непосредственно ссылается проект переопределяет ограничения зависимостей от других пакетов.</span><span class="sxs-lookup"><span data-stu-id="b50e8-353">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="b50e8-354">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-354">**Example message**</span></span> | <span data-ttu-id="b50e8-355">*Версия пакета обнаруженных вне зависимости ограничение: x 1.0.0 требуется y (= 1.0.0), но версии y 2.0.0 был разрешен.*</span><span class="sxs-lookup"><span data-stu-id="b50e8-355">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="b50e8-356">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-356">**Solution**</span></span> | <span data-ttu-id="b50e8-357">В некоторых случаях это сделано намеренно, а предупреждение может быть отменено.</span><span class="sxs-lookup"><span data-stu-id="b50e8-357">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="b50e8-358">В противном случае измените ссылка проекта в пакет, чтобы расширить его ограничения версии.</span><span class="sxs-lookup"><span data-stu-id="b50e8-358">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="b50e8-359">Резервный предупреждения пакетов</span><span class="sxs-lookup"><span data-stu-id="b50e8-359">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="b50e8-360">NU1701</span><span class="sxs-lookup"><span data-stu-id="b50e8-360">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-361">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-361">**Issue**</span></span> | <span data-ttu-id="b50e8-362">`PackageTargetFallback` / `AssetTargetFallback` была использована для выбора средств из пакета.</span><span class="sxs-lookup"><span data-stu-id="b50e8-362">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="b50e8-363">Предупреждение Проинформируйте пользователей, ОС может быть не совместимы 100%.</span><span class="sxs-lookup"><span data-stu-id="b50e8-363">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="b50e8-364">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-364">**Example message**</span></span> | <span data-ttu-id="b50e8-365">*Пакет «NuGet.Versioning» был восстановлен, вместо этого использовать «portable net45 + win8» целевая платформа проекта «netstandard1.5». Этот пакет не может быть полностью совместим с проектом.*</span><span class="sxs-lookup"><span data-stu-id="b50e8-365">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="b50e8-366">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-366">**Solution**</span></span> | <span data-ttu-id="b50e8-367">Изменения целевой платформы проекта на ту, которая поддерживает пакет.</span><span class="sxs-lookup"><span data-stu-id="b50e8-367">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="b50e8-368">Предупреждения веб-канала</span><span class="sxs-lookup"><span data-stu-id="b50e8-368">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="b50e8-369">NU1801</span><span class="sxs-lookup"><span data-stu-id="b50e8-369">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-370">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-370">**Issue**</span></span> | <span data-ttu-id="b50e8-371">Произошла ошибка при чтении веб-канала при `IgnoreFailedSources` имеет значение true, преобразование ее устранимая предупреждение.</span><span class="sxs-lookup"><span data-stu-id="b50e8-371">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="b50e8-372">Это может содержать любые сообщения и является универсальным.</span><span class="sxs-lookup"><span data-stu-id="b50e8-372">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="b50e8-373">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-373">**Example message**</span></span> | <span data-ttu-id="b50e8-374">неприменимо</span><span class="sxs-lookup"><span data-stu-id="b50e8-374">n/a</span></span> |
| <span data-ttu-id="b50e8-375">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-375">**Solution**</span></span> | <span data-ttu-id="b50e8-376">Измените конфигурацию таким образом, чтобы указать допустимые источники.</span><span class="sxs-lookup"><span data-stu-id="b50e8-376">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="b50e8-377">NuGet внутренних ошибок и предупреждений</span><span class="sxs-lookup"><span data-stu-id="b50e8-377">NuGet internal errors and warnings</span></span>

<span data-ttu-id="b50e8-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="b50e8-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="b50e8-379">NU1000</span><span class="sxs-lookup"><span data-stu-id="b50e8-379">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-380">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-380">**Issue**</span></span> | <span data-ttu-id="b50e8-381">Неопределенный Внутренняя ошибка на NuGet.</span><span class="sxs-lookup"><span data-stu-id="b50e8-381">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="b50e8-382">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-382">**Solution**</span></span> | <span data-ttu-id="b50e8-383">Дополнительные сведения в журнале</span><span class="sxs-lookup"><span data-stu-id="b50e8-383">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="b50e8-384">NU1500</span><span class="sxs-lookup"><span data-stu-id="b50e8-384">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-385">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-385">**Issue**</span></span> | <span data-ttu-id="b50e8-386">Неопределенный внутренние предупреждения NuGet.</span><span class="sxs-lookup"><span data-stu-id="b50e8-386">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="b50e8-387">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-387">**Solution**</span></span> | <span data-ttu-id="b50e8-388">Дополнительные сведения в журнале</span><span class="sxs-lookup"><span data-stu-id="b50e8-388">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="b50e8-389">Подписанные пакеты (создания и проверки)</span><span class="sxs-lookup"><span data-stu-id="b50e8-389">Signed packages (creation and verification)</span></span>

<span data-ttu-id="b50e8-390">*NuGet 4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="b50e8-390">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="b50e8-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="b50e8-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="b50e8-392">NU3000</span><span class="sxs-lookup"><span data-stu-id="b50e8-392">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-393">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-393">**Issue**</span></span> | <span data-ttu-id="b50e8-394">Общая ошибка, связанные с Подписание пакета и подпись проверки пакета.</span><span class="sxs-lookup"><span data-stu-id="b50e8-394">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="b50e8-395">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-395">**Solution**</span></span> | <span data-ttu-id="b50e8-396">Дополнительные сведения в журнале.</span><span class="sxs-lookup"><span data-stu-id="b50e8-396">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="b50e8-397">NU3001</span><span class="sxs-lookup"><span data-stu-id="b50e8-397">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-398">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-398">**Issue**</span></span> | <span data-ttu-id="b50e8-399">Недопустимые аргументы либо [входа команда](../tools/cli-ref-sign.md) или [проверьте команду](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="b50e8-399">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="b50e8-400">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-400">**Solution**</span></span> | <span data-ttu-id="b50e8-401">Проверьте и исправьте передаваемых методу аргументов.</span><span class="sxs-lookup"><span data-stu-id="b50e8-401">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="b50e8-402">NU3002</span><span class="sxs-lookup"><span data-stu-id="b50e8-402">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-403">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-403">**Issue**</span></span> | <span data-ttu-id="b50e8-404">`-Timestamper` Не указан параметр с [входа команды nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="b50e8-404">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="b50e8-405">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-405">**Example message**</span></span> | <span data-ttu-id="b50e8-406">*"-Timestamper" параметр не указан. Подписанный пакет не будет отметку времени.*</span><span class="sxs-lookup"><span data-stu-id="b50e8-406">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="b50e8-407">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-407">**Solution**</span></span> | <span data-ttu-id="b50e8-408">Укажите `-Timestamper` вариант с `nuget sign`.</span><span class="sxs-lookup"><span data-stu-id="b50e8-408">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="b50e8-409">NU3004</span><span class="sxs-lookup"><span data-stu-id="b50e8-409">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-410">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-410">**Issue**</span></span> | <span data-ttu-id="b50e8-411">Пакет без знака, предоставленная [nuget проверьте команду](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="b50e8-411">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="b50e8-412">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-412">**Solution**</span></span> | <span data-ttu-id="b50e8-413">Запустите `nuget verify` с подписанных пакетов.</span><span class="sxs-lookup"><span data-stu-id="b50e8-413">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="b50e8-414">В разделе [подписать пакет](../create-packages/Sign-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="b50e8-414">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="b50e8-415">NU3008</span><span class="sxs-lookup"><span data-stu-id="b50e8-415">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-416">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-416">**Issue**</span></span> | <span data-ttu-id="b50e8-417">Сбой при проверке целостности пакета, это означает, что подписанного пакета было изменено при передаче с момента подписан.</span><span class="sxs-lookup"><span data-stu-id="b50e8-417">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="b50e8-418">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-418">**Solution**</span></span> | <span data-ttu-id="b50e8-419">Проверьте компьютер с помощью антивирусной программы.</span><span class="sxs-lookup"><span data-stu-id="b50e8-419">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="b50e8-420">Удалите пакет на компьютере, переустановите его и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="b50e8-420">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="b50e8-421">Если проблема сохранится, обратитесь к владельцу исходного пакета и владелец пакета.</span><span class="sxs-lookup"><span data-stu-id="b50e8-421">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="b50e8-422">NU3018</span><span class="sxs-lookup"><span data-stu-id="b50e8-422">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-423">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-423">**Issue**</span></span> | <span data-ttu-id="b50e8-424">Сбой при создании цепочки сертификатов для основной сигнатуры.</span><span class="sxs-lookup"><span data-stu-id="b50e8-424">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="b50e8-425">Основной сертификат подписи не является доверенным, отозван, или сведения об отзыве сертификата недоступен.</span><span class="sxs-lookup"><span data-stu-id="b50e8-425">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="b50e8-426">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-426">**Example message**</span></span> | <span data-ttu-id="b50e8-427">*Предупреждение: NU3018: функции отзыва не удалось проверить отзыв сертификата.*</span><span class="sxs-lookup"><span data-stu-id="b50e8-427">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="b50e8-428">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-428">**Solution**</span></span> | <span data-ttu-id="b50e8-429">Используйте доверенные и допустимый сертификат.</span><span class="sxs-lookup"><span data-stu-id="b50e8-429">Use a trusted and valid certificate.</span></span> <span data-ttu-id="b50e8-430">Проверьте подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="b50e8-430">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="b50e8-431">NU3028</span><span class="sxs-lookup"><span data-stu-id="b50e8-431">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b50e8-432">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="b50e8-432">**Issue**</span></span> | <span data-ttu-id="b50e8-433">Не удалось выполнить построения цепочки сертификатов для подписи отметки времени.</span><span class="sxs-lookup"><span data-stu-id="b50e8-433">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="b50e8-434">Сертификат подписи отметки времени не является доверенным, отозван, или сведения об отзыве сертификата недоступен.</span><span class="sxs-lookup"><span data-stu-id="b50e8-434">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="b50e8-435">**Пример сообщения**</span><span class="sxs-lookup"><span data-stu-id="b50e8-435">**Example message**</span></span> | <span data-ttu-id="b50e8-436">*Предупреждение: NU3028: функции отзыва не удалось проверить отзыв сертификата.*</span><span class="sxs-lookup"><span data-stu-id="b50e8-436">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="b50e8-437">**Решение**</span><span class="sxs-lookup"><span data-stu-id="b50e8-437">**Solution**</span></span> | <span data-ttu-id="b50e8-438">Используйте доверенные и допустимый сертификат.</span><span class="sxs-lookup"><span data-stu-id="b50e8-438">Use a trusted and valid certificate.</span></span> <span data-ttu-id="b50e8-439">Проверьте подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="b50e8-439">Check internet connectivity.</span></span> |
