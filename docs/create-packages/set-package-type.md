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
# <a name="set-a-nuget-package-type"></a>Установка типа пакета NuGet

Пакету можно присвоить один или несколько *типов пакетов*, чтобы указать предполагаемое использование.

## <a name="known-package-types"></a>Известные типы пакетов

- Пакеты типа `Dependency` добавляют ресурсы времени сборки или времени выполнения в библиотеки и приложения, и их можно устанавливать в проектах любого типа (при условии, что они совместимы).

- Пакеты типа `DotnetTool` — это инструменты .NET, которые можно установить с помощью [.NET CLI](/dotnet/articles/core/tools/index).

- Пакеты типов `Template` предоставляют [пользовательские шаблоны](/dotnet/core/tools/custom-templates), которые можно использовать для создания файлов или проектов, таких как приложение, служба, средство или библиотека классов.

Пакеты, которым не назначен тип, включая все пакеты, созданные в более ранних версиях NuGet, по умолчанию имеют тип `Dependency`.

> [!NOTE]
> Поддержка типов пакетов была добавлена в NuGet 3.5.
> Если пользовательский тип пакета не требуется, *не* рекомендуется явно задавать тип пакета.
> В NuGet по умолчанию используется тип `Dependency`, если тип не указан.

## <a name="custom-package-types"></a>Пользовательские типы пакетов

Вы можете присвоить пакету один или несколько пользовательских типов, если его использование не соответствует [известным типам пакетов](#known-package-types).

Например, клиенты приложения `Contoso` могут устанавливать расширения. Приложение может потребовать от авторов расширений использовать пользовательский тип пакетов `ContosoExtension`, чтобы указать свои пакеты в качестве подходящих расширений, соответствующих необходимым соглашениям.

> [!WARNING]
> Пакет с пользовательским типом нельзя установить с помощью Visual Studio или nuget.exe. Дополнительные сведения см. на странице [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468).

# <a name="using-dotnet-cli"></a>[Использование .NET CLI](#tab/dotnet)

Типы пакетов можно задать в файле проекта (`.csproj`):

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

Пакетам с несколькими предполагаемыми применениями можно присвоить несколько типов с помощью разделителя `;`:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

Для обозначения версий типов пакета можно использовать разделитель `,` между типом пакета и его строкой [`Version`](/dotnet/api/system.version):

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[Использование nuget.exe](#tab/nugetexe)

Типы пакетов задаются в файле `.nuspec` внутри узла `packageTypes\packageType` в элементе `<metadata>`:

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

Пакетам с несколькими предполагаемыми применениями можно присвоить несколько типов:

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

Для типов пакетов можно указать версию с помощью строки [`Version`](/dotnet/api/system.version):

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

Формат строки типа пакета аналогичен используемому для идентификатора пакета. Иными словами, тип пакета — это строка без учета регистра, соответствующая регулярному выражению `^\w+([_.-]\w+)*$` и включающая от одного до 100 символов.

Если версия типа пакета задана, она является строкой [`Version`](/dotnet/api/system.version). Версия типа пакета является необязательной и по умолчанию имеет значение `0.0`.
