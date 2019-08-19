---
title: Создание пакета NuGet с помощью MSBuild
description: Подробное руководство по проектированию и созданию пакета NuGet, включая принятие решений по ключевым аспектам, таким как файлы и управление версиями.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: 92b42f0a6133565844d0b6df2cb50770793055ec
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860635"
---
# <a name="create-a-nuget-package-using-msbuild"></a>Создание пакета NuGet с помощью MSBuild

При создании пакета NuGet из кода вы формируете компонент, которым можно поделиться с любым количеством разработчиков для совместного использования. В этой статье описывается, как создать пакет с помощью MSBuild. MSBuild предустанавливается с каждой рабочей нагрузкой Visual Studio, содержащей NuGet. Кроме того, можно использовать MSBuild через dotnet CLI с помощью команды [dotnet msbuild](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild).

Для проектов .NET Core и .NET Standard с [форматом в стиле пакета SDK](../resources/check-project-format.md) и других проектов в таком стиле NuGet использует сведения в файле проекта напрямую для создания пакета.  Для проекта в стиле, отличном от SDK, который использует `<PackageReference>`, NuGet также использует файл проекта для создания пакета.

Проекты в стиле SDK имеют функциональные возможности пакетирования по умолчанию. Для проектов PackageReference в стиле, отличном от SDK, необходимо добавить пакет NuGet.Build.Tasks.Pack в зависимости проекта. Подробные сведения о целевых объектах пакета MSBuild см. в разделе [Пакет NuGet и восстановление в качестве целевых объектов MSBuild](../reference/msbuild-targets.md).

Команда, создающая пакет, `msbuild -t:pack`, эквивалентна `dotnet pack`.

> [!IMPORTANT]
> Эта статья применяется к проектам [в стиле SDK](../resources/check-project-format.md) (обычно это проекты .NET Core и .NET Standard), а также к проектам в других стилях, использующим PackageReference.

## <a name="set-properties"></a>Настройка свойств

Для создания пакета необходимы следующие свойства:

- `PackageId` — идентификатор пакета, который должен быть уникальным в пределах коллекции, содержащей пакет. Если не задано, по умолчанию используется значение `AssemblyName`.
- `Version` —определенный номер версии в формате *основной_номер.дополнительный_номер.исправление[-суффикс]* , где *-суффикс* указывает на [предварительные версии](prerelease-packages.md). По умолчанию используется значение 1.0.0.
- название пакета, которое должно отображаться на сайте размещения (например, nuget.org);
- `Authors` — сведения об авторе и владельце. Если не задано, по умолчанию используется значение `AssemblyName`.
- `Company` — название компании. Если не задано, по умолчанию используется значение `AssemblyName`.

В Visual Studio эти значения можно задать в свойствах проекта (щелкните правой кнопкой мыши проект в обозревателе решений, выберите **Свойства** и перейдите на вкладку **Пакет**). Эти свойства также можно задать напрямую в файле проекта ( *.csproj*).

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Присвойте пакету идентификатор, который будет уникальным на сайте nuget.org или в другом используемом источнике пакета.

В следующем примере показан простой полный файл проекта, в котором содержатся эти свойства.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

Можно также задать дополнительные свойства, такие как `Title`, `PackageDescription` и `PackageTags` (см. подробнее об [использовании целевых объектов пакета MSBuild](../reference/msbuild-targets.md#pack-target), [управлении ресурсами зависимостей](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) и [использовании свойств метаданных NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties)).

> [!NOTE]
> Если пакет будет общедоступным, обратите особое внимание на свойство **PackageTags**, так как теги помогают найти ваш пакет и понять его назначение.

Подробные сведения об объявлении зависимостей и указании номеров версий см. в разделе [Ссылки на пакеты в файлах проекта](../consume-packages/package-references-in-project-files.md) и [Управление версиями пакетов](../reference/package-versioning.md). Доступ к ресурсам зависимостей в пакете можно также предоставлять напрямую с помощью атрибутов `<IncludeAssets>` и `<ExcludeAssets>`. См. подробнее об [управлении ресурсами зависимостей](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Выбор уникального идентификатора пакета и номера версии

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a>Добавление пакета NuGet.Build.Tasks.Pack

Если вы используете MSBuild с проектом в стиле, отличном от SDK, и PackageReference, добавьте пакет NuGet.Build.Tasks.Pack в проект.

1. Откройте файл проекта и добавьте следующее после элемента `<PropertyGroup>`:

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. Откройте командную строку разработчика (в **поле поиска** введите **Командная строка разработчика**).

   В общем случае следует запустить Командную строку разработчика для Visual Studio из меню **Пуск**, так как в этом случае настраиваются все необходимые пути для MSBuild.

3. Перейдите в папку, содержащую файл проекта, и введите следующую команду, чтобы установить пакет NuGet.Build.Tasks.Pack.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   Убедитесь, что выходные данные MSBuild показывают, что сборка выполнена успешно.

## <a name="run-the-msbuild--tpack-command"></a>Выполните команду msbuild -t:pack

Чтобы создать пакет NuGet (`.nupkg` файл) из проекта, запустите команду `msbuild -t:pack`, которая также автоматически построит проект:

В командной строке разработчика для Visual Studio введите следующую команду:

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

На выходе показан путь к файлу `.nupkg`.

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a>Автоматическое создание пакета при сборке

Чтобы автоматически выполнить команду `msbuild -t:pack` при сборке или восстановлении проекта, в разделе `<PropertyGroup>` файла проекта добавьте следующую строку:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Выполнив `msbuild -t:pack` в решении, вы упакуете все проекты в решении, которые можно упаковать (свойство [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) имеет значение `true`).

> [!NOTE]
> При автоматическом создании пакета время на упаковку увеличивает время сборки проекта.

### <a name="test-package-installation"></a>Тестирование установки пакета

Перед публикацией пакета, как правило, необходимо протестировать процесс его установки в проекте. Это позволяет убедиться в том, что все необходимые файлы помещаются в нужные места.

Установку можно протестировать вручную в Visual Studio или в командной строке, выполнив стандартную [процедуру установки пакета](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

> [!IMPORTANT]
> Пакеты не изменяются. Если вы устраните проблему, измените содержимое пакета и снова выполните упаковку, при повторном тестировании вы все равно будете использовать старую версию пакета до тех пор, [пока не будет очищена папка глобальных пакетов](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders). Это особенно важно при тестировании пакетов, которые не используют уникальную метку предварительной версии при каждой сборке.

## <a name="next-steps"></a>Следующие шаги

Создав пакет, то есть файл `.nupkg`, вы можете опубликовать его в любой коллекции на ваш выбор, как описано в разделе [Публикация пакета](../nuget-org/publish-a-package.md).

Вы также можете расширить возможности пакета или обеспечить поддержку других сценариев, как описано в следующих разделах:

- [Объекты pack и restore NuGet в качестве целевых объектов MSBuild](../reference/msbuild-targets.md)
- [Управление версиями пакета](../reference/package-versioning.md)
- [Поддержка нескольких целевых платформ](../create-packages/multiple-target-frameworks-project-file.md)
- [Преобразования исходных файлов и файлов конфигурации](../create-packages/source-and-config-file-transformations.md)
- [Локализация](../create-packages/creating-localized-packages.md)
- [Предварительные версии](../create-packages/prerelease-packages.md)
- [Определение типа пакета](../create-packages/set-package-type.md)
- [Создание пакетов, содержащих сборки COM-взаимодействия](../create-packages/author-packages-with-COM-interop-assemblies.md)

Наконец, существуют дополнительные типы пакетов, о которых нужно знать:

- [Собственные пакеты](../create-packages/native-packages.md)
- [Пакеты символов](../create-packages/symbol-packages.md)
