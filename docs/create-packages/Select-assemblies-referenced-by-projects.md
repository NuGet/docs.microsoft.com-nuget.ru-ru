---
title: Выбор сборок, на которые ссылаются проекты
description: Выбор подмножества сборок в пакете, которые будут доступны компилятору, в то время как все сборки будут доступны во время выполнения.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b32075c3f2c06c15c07d36602bdabdaee8b9405a
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427479"
---
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="11a17-103">Выбор сборок, на которые ссылаются проекты</span><span class="sxs-lookup"><span data-stu-id="11a17-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="11a17-104">Применение явных ссылок на сборки позволяет использовать для технологии IntelliSense и компилятора подмножество сборок, в то время как все сборки будут доступны во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="11a17-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="11a17-105">`PackageReference` и `packages.config` работают по-разному, в связи с чем авторам пакета может потребоваться обеспечить поддержку обоих типов проекта при создании пакета.</span><span class="sxs-lookup"><span data-stu-id="11a17-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="11a17-106">Явно задаваемые ссылки на сборки связаны со сборками .NET.</span><span class="sxs-lookup"><span data-stu-id="11a17-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="11a17-107">Это не способ распространения машинных сборок, для которых управляемые сборки осуществляют платформенные вызовы.</span><span class="sxs-lookup"><span data-stu-id="11a17-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="11a17-108">Поддержка `PackageReference`</span><span class="sxs-lookup"><span data-stu-id="11a17-108">`PackageReference` support</span></span>

<span data-ttu-id="11a17-109">Если в проекте используется пакет с `PackageReference`, который содержит каталог `ref\<tfm>\`, NuGet будет классифицировать расположенные в нем сборки как ресурсы времени компиляции. Сборки в каталоге `lib\<tfm>\` при этом будут классифицироваться как ресурсы времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="11a17-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="11a17-110">Сборки в каталоге `ref\<tfm>\` не используются во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="11a17-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="11a17-111">Это означает, что для любой сборки в каталоге `ref\<tfm>\` должна присутствовать соответствующая сборка в каталоге `lib\<tfm>\` или `runtime\`, иначе во время выполнения скорее всего произойдет ошибка.</span><span class="sxs-lookup"><span data-stu-id="11a17-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="11a17-112">Поскольку сборки из каталога `ref\<tfm>\` не используются во время выполнения, они могут [содержать только метаданные](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) в целях уменьшения размера пакета.</span><span class="sxs-lookup"><span data-stu-id="11a17-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="11a17-113">Если пакет содержит элемент nuspec `<references>` (используется в `packages.config`, как описывается ниже) и не имеет сборок в каталоге `ref\<tfm>\`, NuGet объявит сборки, перечисленные в элементе nuspec `<references>`, одновременно как сборки времени компиляции и выполнения.</span><span class="sxs-lookup"><span data-stu-id="11a17-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="11a17-114">Это означает, что когда вызываемые по ссылке сборки будут пробовать загрузить любую другую сборку из каталога `lib\<tfm>\`, произойдет исключение времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="11a17-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="11a17-115">Если пакет содержит каталог `runtime\`, NuGet может не использовать ресурсы из каталога `lib\`.</span><span class="sxs-lookup"><span data-stu-id="11a17-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="11a17-116">Поддержка `packages.config`</span><span class="sxs-lookup"><span data-stu-id="11a17-116">`packages.config` support</span></span>

<span data-ttu-id="11a17-117">Проекты, использующие `packages.config` для управления пакетами NuGet, как правило добавляют ссылки на все сборки в каталоге `lib\<tfm>\`.</span><span class="sxs-lookup"><span data-stu-id="11a17-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="11a17-118">Каталог `ref\` был добавлен для поддержки `PackageReference` и не учитывается при использовании `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="11a17-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="11a17-119">Чтобы явно указать сборки, на которые ссылки для проектов задаются с использованием `packages.config`, пакет должен использовать элемент [`<references>` в файле nuspec ](../reference/nuspec.md#explicit-assembly-references).</span><span class="sxs-lookup"><span data-stu-id="11a17-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="11a17-120">Например:</span><span class="sxs-lookup"><span data-stu-id="11a17-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="11a17-121">Проект `packages.config` использует процесс [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) для копирования сборок в выходной каталог `bin\<configuration>\`.</span><span class="sxs-lookup"><span data-stu-id="11a17-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="11a17-122">Сборка проекта копируется, после чего система сборки проверяет манифест сборки на наличие вызываемых по ссылке сборок, а затем копирует эти сборки и рекурсивно повторяет эту операцию для всех сборок.</span><span class="sxs-lookup"><span data-stu-id="11a17-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="11a17-123">Это означает, что если какая-либо сборка в вашем каталоге `lib\<tfm>\` не используются в манифесте какой-либо другой сборки в качестве зависимого компонента (если сборка загружается во время выполнения с использованием `Assembly.Load`, MEF или другой платформы внедрения зависимостей), она может не копироваться в выходной каталог `bin\<configuration>\` вашего проекта, несмотря на присутствие в каталоге `bin\<tfm>\`.</span><span class="sxs-lookup"><span data-stu-id="11a17-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="11a17-124">Пример</span><span class="sxs-lookup"><span data-stu-id="11a17-124">Example</span></span>

<span data-ttu-id="11a17-125">Мой пакет будет содержать три сборки (`MyLib.dll`, `MyHelpers.dll` и `MyUtilities.dll`), нацеленные на платформу .NET Framework 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="11a17-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="11a17-126">`MyUtilities.dll` содержит классы, предназначенные для использования только двумя другими сборками, поэтому мне не требуется использовать эти классы для функции IntelliSense или во время компиляции в проектах, использующих мой пакет.</span><span class="sxs-lookup"><span data-stu-id="11a17-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="11a17-127">Мой файл `nuspec` должен содержать следующие элементы XML:</span><span class="sxs-lookup"><span data-stu-id="11a17-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="11a17-128">в пакете будут присутствовать следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="11a17-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
