---
title: Многоплатформенное нацеливание пакетов NuGet в файле проекта
description: Описание различных способов нацеливания на несколько версий .NET Framework из одного пакета NuGet в файле проекта.
author: JonDouglas
ms.author: jodou
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: a05d053340bb2fe795991dfa5a2b95d8625dfd44
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774375"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a><span data-ttu-id="703a3-103">Поддержка выбора нескольких версий платформ .NET в файле проекта</span><span class="sxs-lookup"><span data-stu-id="703a3-103">Support multiple .NET Framework versions in your project file</span></span>

<span data-ttu-id="703a3-104">При создании проекта рекомендуется также создать библиотеку классов .NET Standard, так как она обеспечивает совместимость с самыми разными потребляющими проектами.</span><span class="sxs-lookup"><span data-stu-id="703a3-104">When you first create a project, we recommend you create a .NET Standard class library, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="703a3-105">С помощью .NET Standard можно добавить в библиотеку .NET. [поддержку разных платформ](/dotnet/standard/library-guidance/cross-platform-targeting) по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="703a3-105">By using .NET Standard, you add [cross-platform support](/dotnet/standard/library-guidance/cross-platform-targeting) to a .NET library by default.</span></span> <span data-ttu-id="703a3-106">Но в некоторых сценариях также может потребоваться включить код, предназначенный для конкретной платформы.</span><span class="sxs-lookup"><span data-stu-id="703a3-106">However, in some scenarios, you may also need to include code that targets a particular framework.</span></span> <span data-ttu-id="703a3-107">В этой статье показано, как это сделать для проектов [на основе пакетов SDK](../resources/check-project-format.md).</span><span class="sxs-lookup"><span data-stu-id="703a3-107">This article shows you how to do that for [SDK-style](../resources/check-project-format.md) projects.</span></span>

<span data-ttu-id="703a3-108">Для таких проектов можно настроить поддержку нескольких целевых платформ ([TFM](/dotnet/standard/frameworks)) в файле проекта, а затем использовать `dotnet pack` или `msbuild /t:pack` для создания пакета.</span><span class="sxs-lookup"><span data-stu-id="703a3-108">For SDK-style projects, you can configure support for multiple targets frameworks ([TFM](/dotnet/standard/frameworks)) in your project file, then use `dotnet pack` or `msbuild /t:pack` to create the package.</span></span>

> [!NOTE]
> <span data-ttu-id="703a3-109">CLI nuget.exe не поддерживает упаковку проектов на основе пакетов SDK, поэтому используйте только `dotnet pack` или `msbuild /t:pack`.</span><span class="sxs-lookup"><span data-stu-id="703a3-109">nuget.exe CLI does not support packing SDK-style projects, so you should only use `dotnet pack` or `msbuild /t:pack`.</span></span> <span data-ttu-id="703a3-110">Рекомендуется [включить все свойства](../reference/msbuild-targets.md#pack-target), которые обычно находятся в файле `.nuspec` файла проекта.</span><span class="sxs-lookup"><span data-stu-id="703a3-110">We recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="703a3-111">Чтобы выбрать несколько версий .NET Framework в проекте не на основе пакетов SDK, см. руководство по [обеспечению поддержки нескольких версий .NET Framework](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="703a3-111">To target multiple .NET Framework versions in a non-SDK-style project, see [Supporting multiple .NET Framework versions](supporting-multiple-target-frameworks.md).</span></span>

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a><span data-ttu-id="703a3-112">Создание проекта с поддержкой нескольких версий .NET Framework</span><span class="sxs-lookup"><span data-stu-id="703a3-112">Create a project that supports multiple .NET Framework versions</span></span>

1. <span data-ttu-id="703a3-113">Создайте библиотеку классов .NET Standard в Visual Studio или используйте `dotnet new classlib`.</span><span class="sxs-lookup"><span data-stu-id="703a3-113">Create a new .NET Standard class library either in Visual Studio or use `dotnet new classlib`.</span></span>

   <span data-ttu-id="703a3-114">Рекомендуется создать библиотеку классов .NET Standard для обеспечения лучшей совместимости.</span><span class="sxs-lookup"><span data-stu-id="703a3-114">We recommend that you create a .NET Standard class library for best compatibility.</span></span>

2. <span data-ttu-id="703a3-115">Измените файл *.csproj*, чтобы обеспечить поддержку целевых платформ.</span><span class="sxs-lookup"><span data-stu-id="703a3-115">Edit the *.csproj* file to support the target frameworks.</span></span> <span data-ttu-id="703a3-116">Например, измените</span><span class="sxs-lookup"><span data-stu-id="703a3-116">For example, change</span></span>
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   <span data-ttu-id="703a3-117">на:</span><span class="sxs-lookup"><span data-stu-id="703a3-117">to:</span></span>
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   <span data-ttu-id="703a3-118">Убедитесь, что для XML-элемента единственное число изменено на множественное (добавьте s в теги открытия и закрытия).</span><span class="sxs-lookup"><span data-stu-id="703a3-118">Make sure that you change the XML element changed from singular to plural (add the "s" to both the open and close tags).</span></span>

3. <span data-ttu-id="703a3-119">Если у вас есть код, который работает только на одной целевой платформе (TFM), можно использовать `#if NET45` или `#if NETSTANDARD2_0` для разделения кода, зависящего от TFM</span><span class="sxs-lookup"><span data-stu-id="703a3-119">If you have any code that only works in one TFM, you can use `#if NET45` or `#if NETSTANDARD2_0` to separate TFM-dependent code.</span></span> <span data-ttu-id="703a3-120">(см. подробнее об [использовании нескольких целевых платформ](/dotnet/core/tutorials/libraries#how-to-multitarget)). Например, используйте приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="703a3-120">(For more information, see [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) For example, you can use the following code:</span></span>

   ```csharp
   public string Platform {
      get {
   #if NET45
         return ".NET Framework"
   #elif NETSTANDARD2_0
         return ".NET Standard"
   #else
   #error This code block does not match csproj TargetFrameworks list
   #endif
      }
   }
   ```

4. <span data-ttu-id="703a3-121">Добавьте необходимые метаданные NuGet в файл *.csproj* как свойства MSBuild.</span><span class="sxs-lookup"><span data-stu-id="703a3-121">Add any NuGet metadata you want to the *.csproj* as MSBuild properties.</span></span>

   <span data-ttu-id="703a3-122">Список доступных метаданных пакета и имен свойств MSBuild см. в разделе об [упаковке целевого объекта](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="703a3-122">For the list of available package metadata and the MSBuild property names, see [pack target](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="703a3-123">Также см. раздел [Управление ресурсами зависимости](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="703a3-123">Also see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

   <span data-ttu-id="703a3-124">Если необходимо отделить свойства, связанные со сборкой, от метаданных NuGet, можно использовать другое свойство `PropertyGroup` или поместить свойства NuGet в другой файл и использовать директиву `Import` MSBuild для включения.</span><span class="sxs-lookup"><span data-stu-id="703a3-124">If you want to separate build-related properties from NuGet metadata, you can use a different `PropertyGroup`, or put the NuGet properties in another file and use MSBuild's `Import` directive to include it.</span></span> <span data-ttu-id="703a3-125">Начиная с MSBuild 15.0, также поддерживаются значения `Directory.Build.Props` и `Directory.Build.Targets`.</span><span class="sxs-lookup"><span data-stu-id="703a3-125">`Directory.Build.Props` and `Directory.Build.Targets` are also supported starting with MSBuild 15.0.</span></span>

5. <span data-ttu-id="703a3-126">Теперь используйте `dotnet pack` и полученные целевые объекты *.nupkg*, предназначенные как для .NET Standard 2.0, так и для .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="703a3-126">Now, use `dotnet pack` and the resulting *.nupkg* targets both .NET Standard 2.0 and .NET Framework 4.5.</span></span>

<span data-ttu-id="703a3-127">Ниже приведен файл *.csproj*, созданный с помощью предыдущих действий, и пакет SDK для .NET Core 2.2.</span><span class="sxs-lookup"><span data-stu-id="703a3-127">Here is the *.csproj* file that is generated using the preceding steps and .NET Core SDK 2.2.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a><span data-ttu-id="703a3-128">См. также</span><span class="sxs-lookup"><span data-stu-id="703a3-128">See also</span></span>

* [<span data-ttu-id="703a3-129">Как указать целевые платформы</span><span class="sxs-lookup"><span data-stu-id="703a3-129">How to specify target frameworks</span></span>](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [<span data-ttu-id="703a3-130">Разработка для различных платформ</span><span class="sxs-lookup"><span data-stu-id="703a3-130">Cross-platform targeting</span></span>](/dotnet/standard/library-guidance/cross-platform-targeting)
