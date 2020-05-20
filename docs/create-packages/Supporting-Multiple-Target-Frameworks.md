---
title: Многоплатформенное нацеливание пакетов NuGet
description: Описание различных способов нацеливания на несколько версий .NET Framework из одного пакета NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 34f7c6132ba6050e20114642932ccf29a5ec088d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428627"
---
# <a name="support-multiple-net-versions"></a><span data-ttu-id="b2063-103">Поддержка нескольких версий .NET</span><span class="sxs-lookup"><span data-stu-id="b2063-103">Support multiple .NET versions</span></span>

<span data-ttu-id="b2063-104">Многие библиотеки предназначаются для определенной версии платформы .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="b2063-104">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="b2063-105">Например, у вас может быть одна версия библиотеки для универсальной платформы Windows и другая версия, использующая возможности .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="b2063-105">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span> <span data-ttu-id="b2063-106">Для этого NuGet поддерживает включение нескольких версий одной и той же библиотеки в один пакет.</span><span class="sxs-lookup"><span data-stu-id="b2063-106">To accommodate this, NuGet supports putting multiple versions of the same library in a single package.</span></span>

<span data-ttu-id="b2063-107">В этой статье описывается структура пакета NuGet независимо от того, как созданы пакет или сборки (то есть, когда компоновка одинакова при использовании нескольких файлов *.csproj* не на основе пакетов SDK и пользовательского файла *.nuspec* или одного файла *.csproj* на основе пакетов SDK с многоплатформенным нацеливанием).</span><span class="sxs-lookup"><span data-stu-id="b2063-107">This article describes the layout of a NuGet package, regardless of how the package or assemblies are built (that is, the layout is the same whether using multiple non-SDK-style *.csproj* files and a custom *.nuspec* file, or a single multi-targeted SDK-style *.csproj*).</span></span> <span data-ttu-id="b2063-108">Для проекта в стиле пакета SDK [целевой объект pack](../reference/msbuild-targets.md) NuGet распознает, как должен располагаться пакет, и автоматизирует помещение сборок в правильные папки библиотеки и создание групп зависимостей для каждой целевой платформы (TFM).</span><span class="sxs-lookup"><span data-stu-id="b2063-108">For an SDK-style project, NuGet [pack targets](../reference/msbuild-targets.md) knows how the package must be layed out and automates putting the assemblies in the correct lib folders and creating dependency groups for each target framework (TFM).</span></span> <span data-ttu-id="b2063-109">См. подробнее о [включении поддержки выбора нескольких версий платформ .NET в файле проекта](multiple-target-frameworks-project-file.md).</span><span class="sxs-lookup"><span data-stu-id="b2063-109">For detailed instructions, see [Support multiple .NET Framework versions in your project file](multiple-target-frameworks-project-file.md).</span></span>

<span data-ttu-id="b2063-110">Вам нужно вручную разместить пакет, как описано в этой статье, при использовании метода рабочего каталога на основе соглашения, описанного в разделе [Создание пакета](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="b2063-110">You must manually lay out the package as described in this article when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> <span data-ttu-id="b2063-111">Для проекта на основе пакета SDK рекомендуется, чтобы это было сделано автоматически, но вы также можете вручную разместить пакет, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="b2063-111">For an SDK-style project, the automated method is recommended, but you may also choose to manually lay out the package as described in this article.</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="b2063-112">Структура папок, соответствующих версиям платформы</span><span class="sxs-lookup"><span data-stu-id="b2063-112">Framework version folder structure</span></span>

<span data-ttu-id="b2063-113">При создании пакета, который содержит только одну версию библиотеки или предназначается для нескольких платформ, вы всегда создаете в папке `lib` вложенные папки с именами платформ (с учетом регистра) согласно следующим соглашениям:</span><span class="sxs-lookup"><span data-stu-id="b2063-113">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="b2063-114">Полный список поддерживаемых имен см. в [справочнике по целевым платформам](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="b2063-114">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="b2063-115">Никогда не следует включать версию библиотеки, не относящуюся к конкретной платформе, помещая ее непосредственно в корневую папку `lib`.</span><span class="sxs-lookup"><span data-stu-id="b2063-115">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="b2063-116">(Такая возможность поддерживалась только в `packages.config`.)</span><span class="sxs-lookup"><span data-stu-id="b2063-116">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="b2063-117">В таком случае библиотека будет совместима с любой целевой платформой и ее можно будет установить где угодно, что, скорее всего, приведет к непредвиденным ошибкам во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="b2063-117">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="b2063-118">Возможность добавления сборок в корневую папку (например, `lib\abc.dll`) или ее вложенные папки (например, `lib\abc\abc.dll`) является нерекомендуемой и игнорируется при использовании формата PackagesReference.</span><span class="sxs-lookup"><span data-stu-id="b2063-118">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="b2063-119">Например, следующая структура папок поддерживает четыре версии сборки для конкретных платформ:</span><span class="sxs-lookup"><span data-stu-id="b2063-119">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="b2063-120">Чтобы легко включить все эти файлы при сборке пакета, используйте рекурсивный подстановочный знак `**` в разделе `<files>` файла `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="b2063-120">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="b2063-121">Папки для конкретных архитектур</span><span class="sxs-lookup"><span data-stu-id="b2063-121">Architecture-specific folders</span></span>

<span data-ttu-id="b2063-122">Если имеются сборки для конкретных архитектур, то есть отдельные сборки для архитектур ARM, x86 и x64, их необходимо поместить в папку с именем `runtimes` во вложенные папки `{platform}-{architecture}\lib\{framework}` или `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="b2063-122">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="b2063-123">Например, следующая структура папок содержит как библиотеки DLL в машинном коде, так и управляемые библиотеки DLL для Windows 10 и платформы `uap10.0`:</span><span class="sxs-lookup"><span data-stu-id="b2063-123">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

<span data-ttu-id="b2063-124">Эти сборки будут доступны только во время выполнения. Поэтому если вы хотите предоставить соответствующую сборку, используемую во время компиляции, добавьте сборку `AnyCPU` в папку `/ref/{tfm}`.</span><span class="sxs-lookup"><span data-stu-id="b2063-124">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref/{tfm}` folder.</span></span> 

<span data-ttu-id="b2063-125">Обратите внимание, что NuGet всегда извлекает ресурсы, используемые во время компиляции или выполнения, из одной папки. Если в папке `/ref` есть совместимые ресурсы, то из папки `/lib` не будут добавляться сборки, используемые во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="b2063-125">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="b2063-126">Соответственно, если в папке `/runtimes` есть совместимые ресурсы, то ресурсы из папки `/lib` будут игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="b2063-126">Similarly, if there are some compatible assets from `/runtimes` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="b2063-127">Пример указания ссылок на эти файлы в манифесте `.nuspec` см. в разделе [Создание пакетов универсальной платформы Windows](../guides/create-uwp-packages.md).</span><span class="sxs-lookup"><span data-stu-id="b2063-127">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="b2063-128">Также ознакомьтесь с записью блога об [упаковке компонента приложения для Магазина Windows с помощью NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2).</span><span class="sxs-lookup"><span data-stu-id="b2063-128">Also, see [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="b2063-129">Сопоставление версий сборки и целевых платформ в проекте</span><span class="sxs-lookup"><span data-stu-id="b2063-129">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="b2063-130">Когда диспетчер NuGet устанавливает пакет с несколькими версиями сборки, он пытается сопоставить имя платформы, для которой предназначена сборка, с целевой платформой проекта.</span><span class="sxs-lookup"><span data-stu-id="b2063-130">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="b2063-131">Если соответствия не найдено, NuGet копирует сборку с самой старшей версией, которая не старше версии целевой платформы проекта, при условии, что такая версия сборки доступна.</span><span class="sxs-lookup"><span data-stu-id="b2063-131">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="b2063-132">Если совместимая сборка не найдена, NuGet возвращает соответствующее сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="b2063-132">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="b2063-133">Например, рассмотрим следующую структуру папок в пакете:</span><span class="sxs-lookup"><span data-stu-id="b2063-133">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="b2063-134">При установке этого пакета в проекте, предназначенном для .NET Framework 4.6, NuGet устанавливает сборку из папки `net45`, так как это самая старшая доступная версия не выше 4.6.</span><span class="sxs-lookup"><span data-stu-id="b2063-134">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="b2063-135">Если же проект предназначен для .NET Framework 4.6.1, NuGet устанавливает сборку в папке `net461`.</span><span class="sxs-lookup"><span data-stu-id="b2063-135">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="b2063-136">Если проект предназначен для .NET Framework 4.0 или более ранней версии, NuGet выдает сообщение об ошибке отсутствия совместимой сборки.</span><span class="sxs-lookup"><span data-stu-id="b2063-136">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="b2063-137">Группирование сборок по версии платформы</span><span class="sxs-lookup"><span data-stu-id="b2063-137">Grouping assemblies by framework version</span></span>

<span data-ttu-id="b2063-138">NuGet копирует сборки только из одной папки библиотеки в проекте.</span><span class="sxs-lookup"><span data-stu-id="b2063-138">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="b2063-139">Предположим, есть пакет со следующей структурой папок:</span><span class="sxs-lookup"><span data-stu-id="b2063-139">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="b2063-140">Когда этот пакет устанавливается в проекте, предназначенном для .NET Framework 4.5, устанавливается только сборка `MyAssembly.dll` (версия 2.0).</span><span class="sxs-lookup"><span data-stu-id="b2063-140">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="b2063-141">Сборка `MyAssembly.Core.dll` (версия 1.0) не устанавливается, так как ее нет в папке `net45`.</span><span class="sxs-lookup"><span data-stu-id="b2063-141">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="b2063-142">Такое поведение NuGet обусловлено тем, что сборка `MyAssembly.Core.dll` могла быть объединена с версией 2.0 сборки `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="b2063-142">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="b2063-143">Чтобы установить сборку `MyAssembly.Core.dll` для .NET Framework 4.5, поместите ее копию в папку `net45`.</span><span class="sxs-lookup"><span data-stu-id="b2063-143">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="b2063-144">Группирование сборок по профилю платформы</span><span class="sxs-lookup"><span data-stu-id="b2063-144">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="b2063-145">NuGet также поддерживает нацеливание на определенный профиль платформы путем добавления дефиса и имени платформы в конце имени папки.</span><span class="sxs-lookup"><span data-stu-id="b2063-145">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="b2063-146">Поддерживаются следующие профили:</span><span class="sxs-lookup"><span data-stu-id="b2063-146">The supported profiles are as follows:</span></span>

- <span data-ttu-id="b2063-147">`client`: клиентский профиль;</span><span class="sxs-lookup"><span data-stu-id="b2063-147">`client`: Client Profile</span></span>
- <span data-ttu-id="b2063-148">`full`: полный профиль;</span><span class="sxs-lookup"><span data-stu-id="b2063-148">`full`: Full Profile</span></span>
- <span data-ttu-id="b2063-149">`wp`: Windows Phone;</span><span class="sxs-lookup"><span data-stu-id="b2063-149">`wp`: Windows Phone</span></span>
- <span data-ttu-id="b2063-150">`cf`: Compact Framework.</span><span class="sxs-lookup"><span data-stu-id="b2063-150">`cf`: Compact Framework</span></span>

## <a name="declaring-dependencies-advanced"></a><span data-ttu-id="b2063-151">Объявление зависимостей (расширенные сценарии)</span><span class="sxs-lookup"><span data-stu-id="b2063-151">Declaring dependencies (Advanced)</span></span>

<span data-ttu-id="b2063-152">При упаковке файла проекта NuGet пытается автоматически создать зависимости из проекта.</span><span class="sxs-lookup"><span data-stu-id="b2063-152">When packing a project file, NuGet tries to automatically generate the dependencies from the project.</span></span> <span data-ttu-id="b2063-153">Приведенные в этом разделе инструкции по объявлению зависимостей с помощью файла *.nuspec* обычно выполняются только в расширенных сценариях.</span><span class="sxs-lookup"><span data-stu-id="b2063-153">The information in this section about using a *.nuspec* file to declare dependencies is typically necessary for advanced scenarios only.</span></span>

<span data-ttu-id="b2063-154">*(Версия 2.0+)* Зависимости пакетов можно объявить в файле *.nuspec* с учетом целевой платформы целевого проекта с помощью элементов `<group>` в элементе `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="b2063-154">*(Version 2.0+)* You can declare package dependencies in the *.nuspec* corresponding to the target framework of the target project using `<group>` elements within the `<dependencies>` element.</span></span> <span data-ttu-id="b2063-155">См. об [элементах зависимостей](../reference/nuspec.md#dependencies-element).</span><span class="sxs-lookup"><span data-stu-id="b2063-155">For more information, see [dependencies element](../reference/nuspec.md#dependencies-element).</span></span>

<span data-ttu-id="b2063-156">Каждый элемент group имеет атрибут `targetFramework` и содержит ноль или более элементов `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="b2063-156">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="b2063-157">Эти зависимости устанавливаются вместе, если целевая платформа совместима с профилем платформы проекта.</span><span class="sxs-lookup"><span data-stu-id="b2063-157">Those dependencies are installed together when the target framework is compatible with the project's framework profile.</span></span> <span data-ttu-id="b2063-158">Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="b2063-158">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

<span data-ttu-id="b2063-159">Мы рекомендуем использовать одну группу для моникера целевой платформы (TFM) для файлов в папках *lib/* и *ref/* .</span><span class="sxs-lookup"><span data-stu-id="b2063-159">We recommend using one group per Target Framework Moniker (TFM) for files in the *lib/* and *ref/* folders.</span></span>

<span data-ttu-id="b2063-160">В следующем примере приводятся различные варианты элемента `<group>`:</span><span class="sxs-lookup"><span data-stu-id="b2063-160">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>

    <group targetFramework="net472">
        <dependency id="jQuery" version="1.10.2" />
        <dependency id="WebActivatorEx" version="2.2.0" />
    </group>

    <group targetFramework="net20">
    </group>

</dependencies>
```

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="b2063-161">Определение требуемой цели NuGet</span><span class="sxs-lookup"><span data-stu-id="b2063-161">Determining which NuGet target to use</span></span>

<span data-ttu-id="b2063-162">При упаковке библиотек, предназначенных для переносимой библиотеки классов, может быть нелегко определить цель NuGet, которую следует использовать в именах папок и файле `.nuspec`, особенно если нацеливание производится лишь на подмножество переносимой библиотеки классов.</span><span class="sxs-lookup"><span data-stu-id="b2063-162">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="b2063-163">Следующие внешние ресурсы могут помочь в решении этой задачи:</span><span class="sxs-lookup"><span data-stu-id="b2063-163">The following external resources will help you with this:</span></span>

- <span data-ttu-id="b2063-164">[Framework profiles in .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (Профили платформы в .NET) (stephencleary.com);</span><span class="sxs-lookup"><span data-stu-id="b2063-164">[Framework profiles in .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span></span>
- <span data-ttu-id="b2063-165">[Профили переносимой библиотеки классов](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): таблица, в которой перечисляются профили переносимой библиотеки классов и эквивалентные цели NuGet</span><span class="sxs-lookup"><span data-stu-id="b2063-165">[Portable Class Library profiles](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="b2063-166">[Программа для работы с профилями переносимой библиотеки классов](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): программа командной строки, позволяющая определить профили переносимой библиотеки классов, доступные в системе</span><span class="sxs-lookup"><span data-stu-id="b2063-166">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="b2063-167">Файлы содержимого и скрипты PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2063-167">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="b2063-168">Изменяемые файлы содержимого и выполнение скриптов можно использовать только с форматом `packages.config`. Их не рекомендуется использовать с другими форматами и не следует применять для новых пакетов.</span><span class="sxs-lookup"><span data-stu-id="b2063-168">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="b2063-169">При использовании `packages.config` файлы содержимого и скрипты PowerShell можно группировать по целевой платформе в папках `content` и `tools`, используя те же соглашения в отношении папок.</span><span class="sxs-lookup"><span data-stu-id="b2063-169">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="b2063-170">Пример:</span><span class="sxs-lookup"><span data-stu-id="b2063-170">For example:</span></span>

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

<span data-ttu-id="b2063-171">Если папка платформы пуста, NuGet не добавляет ссылки на сборки или файлы содержимого и не выполняет скрипты PowerShell для этой платформы.</span><span class="sxs-lookup"><span data-stu-id="b2063-171">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="b2063-172">Так как скрипт `init.ps1` выполняется на уровне решения независимо от проекта, его необходимо поместить непосредственно в папку `tools`.</span><span class="sxs-lookup"><span data-stu-id="b2063-172">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="b2063-173">Если он находится в папке платформы, то он игнорируется.</span><span class="sxs-lookup"><span data-stu-id="b2063-173">It's ignored if placed under a framework folder.</span></span>
