---
title: Установка типа пакета NuGet
description: Здесь описаны типы пакетов для определения их назначения.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: fa369e8327330e13f5adda39a75008e42ac99896
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067286"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="67f46-103">Установка типа пакета NuGet</span><span class="sxs-lookup"><span data-stu-id="67f46-103">Set a NuGet package type</span></span>

<span data-ttu-id="67f46-104">Пакету можно присвоить один или несколько *типов пакетов*, чтобы указать предполагаемое использование.</span><span class="sxs-lookup"><span data-stu-id="67f46-104">Packages can be marked with one more more *package types* to indicate its intended use.</span></span>

## <a name="known-package-types"></a><span data-ttu-id="67f46-105">Известные типы пакетов</span><span class="sxs-lookup"><span data-stu-id="67f46-105">Known package types</span></span>

- <span data-ttu-id="67f46-106">Пакеты типа `Dependency` добавляют ресурсы времени сборки или времени выполнения в библиотеки и приложения, и их можно устанавливать в проектах любого типа (при условии, что они совместимы).</span><span class="sxs-lookup"><span data-stu-id="67f46-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="67f46-107">Пакеты типа `DotnetTool` — это инструменты .NET, которые можно установить с помощью [.NET CLI](/dotnet/articles/core/tools/index).</span><span class="sxs-lookup"><span data-stu-id="67f46-107">`DotnetTool` type packages are .NET tools that can be installed by the [dotnet CLI](/dotnet/articles/core/tools/index).</span></span>

- <span data-ttu-id="67f46-108">Пакеты типов `Template` предоставляют [пользовательские шаблоны](/dotnet/core/tools/custom-templates), которые можно использовать для создания файлов или проектов, таких как приложение, служба, средство или библиотека классов.</span><span class="sxs-lookup"><span data-stu-id="67f46-108">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

<span data-ttu-id="67f46-109">Пакеты, которым не назначен тип, включая все пакеты, созданные в более ранних версиях NuGet, по умолчанию имеют тип `Dependency`.</span><span class="sxs-lookup"><span data-stu-id="67f46-109">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

> [!NOTE]
> <span data-ttu-id="67f46-110">Поддержка типов пакетов была добавлена в NuGet 3.5.</span><span class="sxs-lookup"><span data-stu-id="67f46-110">Support for package types was added in NuGet 3.5.</span></span>
> <span data-ttu-id="67f46-111">Если пользовательский тип пакета не требуется, *не* рекомендуется явно задавать тип пакета.</span><span class="sxs-lookup"><span data-stu-id="67f46-111">If you don't need a custom package type, it's best to *not* explicitly set the package type.</span></span>
> <span data-ttu-id="67f46-112">В NuGet по умолчанию используется тип `Dependency`, если тип не указан.</span><span class="sxs-lookup"><span data-stu-id="67f46-112">NuGet defaults to the `Dependency` type when no type is specified.</span></span>

## <a name="custom-package-types"></a><span data-ttu-id="67f46-113">Пользовательские типы пакетов</span><span class="sxs-lookup"><span data-stu-id="67f46-113">Custom package types</span></span>

<span data-ttu-id="67f46-114">Вы можете присвоить пакету один или несколько пользовательских типов, если его использование не соответствует [известным типам пакетов](#known-package-types).</span><span class="sxs-lookup"><span data-stu-id="67f46-114">You can mark your package with one or more custom package types if its use does not fit the [known package types](#known-package-types).</span></span>

<span data-ttu-id="67f46-115">Например, клиенты приложения `Contoso` могут устанавливать расширения.</span><span class="sxs-lookup"><span data-stu-id="67f46-115">For example, imagine that customers of the `Contoso` app can install extensions.</span></span> <span data-ttu-id="67f46-116">Приложение может потребовать от авторов расширений использовать пользовательский тип пакетов `ContosoExtension`, чтобы указать свои пакеты в качестве подходящих расширений, соответствующих необходимым соглашениям.</span><span class="sxs-lookup"><span data-stu-id="67f46-116">The app could require extension authors to use the custom package type `ContosoExtension` to identify their packages as proper extensions that follow the required conventions.</span></span>

> [!WARNING]
> <span data-ttu-id="67f46-117">Пакет с пользовательским типом нельзя установить с помощью Visual Studio или nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="67f46-117">A package with a custom package type cannot be installed by Visual Studio or nuget.exe.</span></span> <span data-ttu-id="67f46-118">Дополнительные сведения см. на странице [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468).</span><span class="sxs-lookup"><span data-stu-id="67f46-118">See [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468) for more information.</span></span>

# <a name="using-dotnet-cli"></a>[<span data-ttu-id="67f46-119">Использование .NET CLI</span><span class="sxs-lookup"><span data-stu-id="67f46-119">Using dotnet CLI</span></span>](#tab/dotnet)

<span data-ttu-id="67f46-120">Типы пакетов можно задать в файле проекта (`.csproj`):</span><span class="sxs-lookup"><span data-stu-id="67f46-120">Package types can be set in the project file (`.csproj`):</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="67f46-121">Пакетам с несколькими предполагаемыми применениями можно присвоить несколько типов с помощью разделителя `;`:</span><span class="sxs-lookup"><span data-stu-id="67f46-121">Packages with multiple intended uses can be marked with multiple package types using the `;` delimiter:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="67f46-122">Для обозначения версий типов пакета можно использовать разделитель `,` между типом пакета и его строкой [`Version`](/dotnet/api/system.version):</span><span class="sxs-lookup"><span data-stu-id="67f46-122">Package types can be versioned using a `,` delimiter between the package type and its [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[<span data-ttu-id="67f46-123">Использование nuget.exe</span><span class="sxs-lookup"><span data-stu-id="67f46-123">Using nuget.exe</span></span>](#tab/nugetexe)

<span data-ttu-id="67f46-124">Типы пакетов задаются в файле `.nuspec` внутри узла `packageTypes\packageType` в элементе `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="67f46-124">Package types are set in the `.nuspec` file within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="ContosoExtension" />
        </packageTypes>
    </metadata>
</package>
```

<span data-ttu-id="67f46-125">Пакетам с несколькими предполагаемыми применениями можно присвоить несколько типов:</span><span class="sxs-lookup"><span data-stu-id="67f46-125">Packages with multiple intended uses may be marked with multiple package types:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

<span data-ttu-id="67f46-126">Для типов пакетов можно указать версию с помощью строки [`Version`](/dotnet/api/system.version):</span><span class="sxs-lookup"><span data-stu-id="67f46-126">Package types can be versioned using a [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" version="1.0.0.0" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

---

<span data-ttu-id="67f46-127">Формат строки типа пакета аналогичен используемому для идентификатора пакета.</span><span class="sxs-lookup"><span data-stu-id="67f46-127">The format of a package type string is exactly like a package ID.</span></span> <span data-ttu-id="67f46-128">Иными словами, тип пакета — это строка без учета регистра, соответствующая регулярному выражению `^\w+([_.-]\w+)*$` и включающая от одного до 100 символов.</span><span class="sxs-lookup"><span data-stu-id="67f46-128">That is, a package type is a case-insensitive string matching the regular expression `^\w+([_.-]\w+)*$` having at least one character and at most 100 characters.</span></span>

<span data-ttu-id="67f46-129">Если версия типа пакета задана, она является строкой [`Version`](/dotnet/api/system.version).</span><span class="sxs-lookup"><span data-stu-id="67f46-129">If provided, the package type version is a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="67f46-130">Версия типа пакета является необязательной и по умолчанию имеет значение `0.0`.</span><span class="sxs-lookup"><span data-stu-id="67f46-130">The package type version is optional and defaults to `0.0`.</span></span>
