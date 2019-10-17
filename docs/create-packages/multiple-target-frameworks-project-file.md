---
title: Многоплатформенное нацеливание пакетов NuGet в файле проекта
description: Описание различных способов нацеливания на несколько версий .NET Framework из одного пакета NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 1d23759433efb405fa5f0035049befced2c43d6b
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380676"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a>Поддержка выбора нескольких версий платформ .NET в файле проекта

При создании проекта рекомендуется также создать библиотеку классов .NET Standard, так как она обеспечивает совместимость с самыми разными потребляющими проектами. С помощью .NET Standard можно добавить в библиотеку .NET. [поддержку разных платформ](/dotnet/standard/library-guidance/cross-platform-targeting) по умолчанию. Но в некоторых сценариях также может потребоваться включить код, предназначенный для конкретной платформы. В этой статье показано, как это сделать для проектов [на основе пакетов SDK](../resources/check-project-format.md).

Для таких проектов можно настроить поддержку нескольких целевых платформ ([TFM](/dotnet/standard/frameworks)) в файле проекта, а затем использовать `dotnet pack` или `msbuild /t:pack` для создания пакета.

> [!NOTE]
> CLI nuget.exe не поддерживает упаковку проектов на основе пакетов SDK, поэтому используйте только `dotnet pack` или `msbuild /t:pack`. Рекомендуется [включить все свойства](../reference/msbuild-targets.md#pack-target), которые обычно находятся в файле `.nuspec` файла проекта. Чтобы выбрать несколько версий .NET Framework в проекте не на основе пакетов SDK, см. руководство по [обеспечению поддержки нескольких версий .NET Framework](supporting-multiple-target-frameworks.md).

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a>Создание проекта с поддержкой нескольких версий .NET Framework

1. Создайте библиотеку классов .NET Standard в Visual Studio или используйте `dotnet new classlib`.

   Рекомендуется создать библиотеку классов .NET Standard для обеспечения лучшей совместимости.

2. Измените файл *.csproj*, чтобы обеспечить поддержку целевых платформ. Например, измените
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   на:
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   Убедитесь, что для XML-элемента единственное число изменено на множественное (добавьте s в теги открытия и закрытия).

3. Если у вас есть код, который работает только на одной целевой платформе (TFM), можно использовать `#if NET45` или `#if NETSTANDARD2_0` для разделения кода, зависящего от TFM (см. подробнее об [использовании нескольких целевых платформ](/dotnet/core/tutorials/libraries#how-to-multitarget)). Например, используйте приведенный ниже код.

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

4. Добавьте необходимые метаданные NuGet в файл *.csproj* как свойства MSBuild.

   Список доступных метаданных пакета и имен свойств MSBuild см. в разделе об [упаковке целевого объекта](../reference/msbuild-targets.md#pack-target). Также см. раздел [Управление ресурсами зависимости](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

   Если необходимо отделить свойства, связанные со сборкой, от метаданных NuGet, можно использовать другое свойство `PropertyGroup` или поместить свойства NuGet в другой файл и использовать директиву `Import` MSBuild для включения. Начиная с MSBuild 15.0, также поддерживаются значения `Directory.Build.Props` и `Directory.Build.Targets`.

5. Теперь используйте `dotnet pack` и полученные целевые объекты *.nupkg*, предназначенные как для .NET Standard 2.0, так и для .NET Framework 4.5.

Ниже приведен файл *.csproj*, созданный с помощью предыдущих действий, и пакет SDK для .NET Core 2.2.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a>См. также

* [Как указать целевые платформы](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [Разработка для различных платформ](/dotnet/standard/library-guidance/cross-platform-targeting)
