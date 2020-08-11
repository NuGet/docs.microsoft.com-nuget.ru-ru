---
title: Создание пакета NuGet с помощью CLI dotnet
description: Подробное руководство по проектированию и созданию пакета NuGet, включая принятие решений по ключевым аспектам, таким как файлы и управление версиями.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 2fcba9dd6bbc7ff4e9b5b8b57250c399f59a1c5e
ms.sourcegitcommit: e02482e15c0cef63153086ed50d14f5b2a38f598
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473848"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>Создание пакета NuGet с помощью CLI dotnet

Независимо от назначения вашего пакета или содержащегося в нем кода, с помощью одного из средств CLI (`nuget.exe` или `dotnet.exe`) вы можете создать компонент, которым можно поделиться с любым количеством разработчиков для совместного использования. В этой статье описывается, как создать пакет с помощью CLI dotnet. См. подробнее об установке средств CLI `dotnet` в руководстве по [установке клиентских средств NuGet](../install-nuget-client-tools.md). Начиная с Visual Studio 2017, CLI dotnet входит в состав рабочих нагрузок .NET Core.

Для проектов .NET Core и .NET Standard с [форматом в стиле пакета SDK](../resources/check-project-format.md) и других проектов в таком стиле NuGet использует сведения в файле проекта напрямую для создания пакета. См. пошаговые руководства по созданию пакетов .NET Standard с использованием [CLI dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) и [Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).

`msbuild -t:pack` — это функциональный эквивалент `dotnet pack`. Чтобы выполнить сборку с помощью MSBuild, см. раздел [Создание пакета NuGet с помощью MSBuild](creating-a-package-msbuild.md).

> [!IMPORTANT]
> Этот раздел относится к проектам [на основе пакетов SDK](../resources/check-project-format.md), в частности, к проектам .NET Core и .NET Standard.

## <a name="set-properties"></a>Настройка свойств

Для создания пакета необходимы следующие свойства:

- `PackageId` — идентификатор пакета, который должен быть уникальным в пределах коллекции, содержащей пакет. Если не задано, по умолчанию используется значение `AssemblyName`.
- `Version` —определенный номер версии в формате *основной_номер.дополнительный_номер.исправление[-суффикс]* , где *-суффикс* указывает на [предварительные версии](prerelease-packages.md). По умолчанию используется значение 1.0.0.
- название пакета, которое должно отображаться на сайте размещения (например, nuget.org);
- `Authors` — сведения об авторе и владельце. Если не задано, по умолчанию используется значение `AssemblyName`.
- `Company` — название компании. Если не задано, по умолчанию используется значение `AssemblyName`.

В Visual Studio эти значения можно задать в свойствах проекта (щелкните правой кнопкой мыши проект в обозревателе решений, выберите **Свойства** и перейдите на вкладку **Пакет**). Эти свойства также можно задать напрямую в файле проекта (`.csproj`).

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Присвойте пакету идентификатор, который будет уникальным на сайте nuget.org или в другом используемом источнике пакета.

В следующем примере показан простой полный файл проекта, в котором содержатся эти свойства. (Можно создать новый проект по умолчанию с помощью команды `dotnet new classlib`.)

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

Можно также задать дополнительные свойства, такие как `Title`, `PackageDescription` и `PackageTags` (см. подробнее об [использовании целевых объектов пакета MSBuild](../reference/msbuild-targets.md#pack-target), [управлении ресурсами зависимостей](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) и [использовании свойств метаданных NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties)).

> [!NOTE]
> Если пакет будет общедоступным, обратите особое внимание на свойство **PackageTags**, так как теги помогают найти ваш пакет и понять его назначение.

Подробные сведения об объявлении зависимостей и указании номеров версий см. в разделе [Ссылки на пакеты в файлах проекта](../consume-packages/package-references-in-project-files.md) и [Управление версиями пакетов](../concepts/package-versioning.md). Доступ к ресурсам зависимостей в пакете можно также предоставлять напрямую с помощью атрибутов `<IncludeAssets>` и `<ExcludeAssets>`. См. подробнее об [управлении ресурсами зависимостей](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="add-an-optional-description-field"></a>Добавление необязательного поля описания

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Выбор уникального идентификатора пакета и номера версии

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a>Выполнение команды pack

Чтобы создать пакет NuGet (`.nupkg` файл) из проекта, запустите команду `dotnet pack`, которая также автоматически построит проект:

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

На выходе показан путь к файлу `.nupkg`.

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Автоматическое создание пакета при сборке

Чтобы автоматически выполнить команду `dotnet pack` вместе с командой `dotnet build`, в разделе `<PropertyGroup>` файла проекта добавьте следующую строку:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Выполнив `dotnet pack` в решении, вы упакуете все проекты в решении, которые можно упаковать (свойство [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) имеет значение `true`).

> [!NOTE]
> При автоматическом создании пакета время на упаковку увеличивает время сборки проекта.

### <a name="test-package-installation"></a>Тестирование установки пакета

Перед публикацией пакета, как правило, необходимо протестировать процесс его установки в проекте. Это позволяет убедиться в том, что все необходимые файлы размещены в надлежащих расположениях в проекте.

Установку можно протестировать вручную в Visual Studio или в командной строке, выполнив стандартную [процедуру установки пакета](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

> [!IMPORTANT]
> Пакеты не изменяются. Если вы устраните проблему, измените содержимое пакета и снова выполните упаковку, при повторном тестировании вы все равно будете использовать старую версию пакета до тех пор, [пока не будет очищена папка глобальных пакетов](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders). Это особенно важно при тестировании пакетов, которые не используют уникальную метку предварительной версии при каждой сборке.

## <a name="next-steps"></a>Next Steps

Создав пакет, то есть файл `.nupkg`, вы можете опубликовать его в любой коллекции на ваш выбор, как описано в разделе [Публикация пакета](../nuget-org/publish-a-package.md).

Вы также можете расширить возможности пакета или обеспечить поддержку других сценариев, как описано в следующих разделах:

- [Управление версиями пакета](../concepts/package-versioning.md)
- [Поддержка нескольких целевых платформ](../create-packages/multiple-target-frameworks-project-file.md)
- [Добавление значка пакета](../reference/nuspec.md#icon)
- [Преобразования исходных файлов и файлов конфигурации](../create-packages/source-and-config-file-transformations.md)
- [Локализация](../create-packages/creating-localized-packages.md)
- [Предварительные версии](../create-packages/prerelease-packages.md)
- [Определение типа пакета](../create-packages/set-package-type.md)
- [Создание пакетов, содержащих сборки COM-взаимодействия](../create-packages/author-packages-with-COM-interop-assemblies.md)

Наконец, существуют дополнительные типы пакетов, о которых нужно знать:

- [Собственные пакеты](../guides/native-packages.md)
- [Пакеты символов](../create-packages/symbol-packages-snupkg.md)
