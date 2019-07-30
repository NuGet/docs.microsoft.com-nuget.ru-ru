---
title: Создание пакета NuGet с помощью CLI dotnet
description: Подробное руководство по проектированию и созданию пакета NuGet, включая принятие решений по ключевым аспектам, таким как файлы и управление версиями.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: da5dbc8b1659cef66e8439b9a3c3bb2c9205cbe6
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/24/2019
ms.locfileid: "68462457"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>Создание пакета NuGet с помощью CLI dotnet

Независимо от назначения вашего пакета или содержащегося в нем кода, с помощью одного из средств CLI (`nuget.exe` или `dotnet.exe`) вы можете создать компонент, которым можно поделиться с любым количеством разработчиков для совместного использования. В этой статье описывается, как создать пакет с помощью CLI dotnet. См. подробнее об установке средств CLI `dotnet` в руководстве по [установке клиентских средств NuGet](../install-nuget-client-tools.md). Начиная с Visual Studio 2017, CLI dotnet входит в состав рабочих нагрузок .NET Core.

Для проектов .NET Core и .NET Standard с [форматом в стиле пакета SDK](../resources/check-project-format.md) и других проектов в таком стиле NuGet использует сведения в файле проекта напрямую для создания пакета. См. пошаговые руководства по созданию пакетов .NET Standard с использованием [CLI dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) и [Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).

`msbuild -t:pack` — это функциональный эквивалент `dotnet pack`. Сборка с помощью MSBuild в целом выполняется, как описано в этой статье, но команды командной строки немного отличаются. Аналогичным образом, если вы используете проект не на основе пакета SDK и `<PackageReference>`, можно также использовать `msbuild /t:pack`. В этих сценариях в зависимости необходимо добавить пакет NuGet.Build.Tasks.Pack. См. подробнее об использовании [объектов pack и restore в NuGet в качестве целевых объектов MSBuild](../reference/msbuild-targets.md).

> [!IMPORTANT]
> Этот раздел относится к проектам [на основе пакетов SDK](../resources/check-project-format.md), в частности, к проектам .NET Core и .NET Standard.

## <a name="set-properties"></a>Настройка свойств

Для создания пакета необходимы следующие свойства:

- `PackageId` — идентификатор пакета, который должен быть уникальным в пределах коллекции, содержащей пакет. Если не задано, по умолчанию используется значение `AssemblyName`.
- `Version` —определенный номер версии в формате *основной_номер.дополнительный_номер.исправление[-суффикс]*, где *-суффикс* указывает на [предварительные версии](prerelease-packages.md). По умолчанию используется значение 1.0.0.
- название пакета, которое должно отображаться на сайте размещения (например, nuget.org);
- `Authors` — сведения об авторе и владельце. Если не задано, по умолчанию используется значение `AssemblyName`.
- `Company` — название компании. Если не задано, по умолчанию используется значение `AssemblyName`.

В Visual Studio эти значения можно задать в свойствах проекта (щелкните правой кнопкой мыши проект в обозревателе решений, выберите **Свойства** и перейдите на вкладку **Пакет**). Эти свойства также можно задать напрямую в файле проекта (`.csproj`).

    ```xml
    <PropertyGroup>
      ...
      <PackageId>AppLogger</PackageId>
      <Version>1.0.0</Version>
      <Authors>your_name</Authors>
      <Company>your_company</Company>
    </PropertyGroup>
    ```

> [!Important]
> Присвойте пакету идентификатор, который будет уникальным на сайте nuget.org или в другом используемом источнике пакета.

Можно также задать дополнительные свойства, такие как `Title`, `PackageDescription` и `PackageTags` (см. подробнее об [использовании целевых объектов пакета MSBuild](../reference/msbuild-targets.md#pack-target), [управлении ресурсами зависимостей](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) и [использовании свойств метаданных NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties)).

> [!NOTE]
> Если пакет будет общедоступным, обратите особое внимание на свойство **PackageTags**, так как теги помогают найти ваш пакет и понять его назначение.

Подробные сведения об объявлении зависимостей и указании номеров версий см. в разделе [Управление версиями пакета](../reference/package-versioning.md). Доступ к ресурсам зависимостей в пакете можно также предоставлять напрямую с помощью атрибутов `<IncludeAssets>` и `<ExcludeAssets>`. См. подробнее об [управлении ресурсами зависимостей](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Выбор уникального идентификатора пакета и номера версии

Идентификатор пакета и номер версии — два самых важных значения в проекте, так как они однозначно определяют код, содержащийся в пакете.

**Рекомендации в отношении идентификатора пакета**

- **Уникальность**. Идентификатор должен быть уникальным в пределах nuget.org или другой коллекции, в которой размещается пакет. Прежде чем задавать идентификатор, проверьте, не используется ли оно уже в соответствующей коллекции. Во избежание конфликтов рекомендуется использовать в качестве первой части идентификатора название организации, например `Contoso.`.
- **Имена в стиле пространств имен**. Используйте шаблон, по которому строятся имена пространств имен в .NET, используя нотацию с точками, а не с дефисами. Например, используйте идентификатор `Contoso.Utility.UsefulStuff` вместо `Contoso-Utility-UsefulStuff` или `Contoso_Utility_UsefulStuff`. Пользователям также удобно, когда идентификатор пакета соответствует пространствам имен, используемым в коде.
- **Примеры пакетов**. Если вы создаете пакет с примером кода, демонстрирующим использование другого пакета, добавьте к идентификатору суффикс `.Sample`, например `Contoso.Utility.UsefulStuff.Sample`. (Образец пакета, конечно, должен иметь зависимость от другого пакета.) При создании примера пакета используйте значение `contentFiles` в `<IncludeAssets>`. В папке `content` разместите код образца в папке с именем `\Samples\<identifier>`, например `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Рекомендации в отношении версии пакета**

- Как правило, версия пакета должна соответствовать версии проекта (или сборки), хотя это не строгое требование. Но это упрощает работу, когда вы используете для пакета одну сборку. В целом помните, что при разрешении зависимостей диспетчер NuGet ориентируется на версии пакетов, а не на версии сборок.
- При применении нестандартной схемы версий обязательно учитывайте правила управления версиями в NuGet, которые изложены в разделе [Управление версиями пакета](../reference/package-versioning.md). NuGet в основном поддерживает [SemVer 2](../reference/package-versioning.md#semantic-versioning-200).

> См. подробнее о [разрешении зависимостей с помощью PackageReference](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference). Более старые сведения, которые помогут вам узнать об управлении версиями, см. в этой серии записей блога.
>
> - [Часть 1. Решение проблем с DLL](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Часть 2. Базовый алгоритм](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Часть 3. Унификация путем переадресации привязок](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="run-the-pack-command"></a>Выполнение команды pack

Чтобы создать пакет NuGet (`.nupkg` файл) из проекта, запустите команду `dotnet pack`, которая также автоматически построит проект:

```cli
# Uses the project file in the current folder by default
dotnet pack
```

На выходе показан путь к `.nupkg` файлу:

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

Перед публикацией пакета, как правило, необходимо протестировать процесс его установки в проекте. Это позволяет убедиться в том, что все необходимые файлы помещаются в нужные места.

Установку можно протестировать вручную в Visual Studio или в командной строке, выполнив стандартную [процедуру установки пакета](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

> [!IMPORTANT]
> Пакеты не изменяются. Если вы устраните проблему, измените содержимое пакета и снова выполните упаковку, при повторном тестировании вы все равно будете использовать старую версию пакета до тех пор, [пока не будет очищена папка глобальных пакетов](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders). Это особенно важно при тестировании пакетов, которые не используют уникальную метку предварительной версии при каждой сборке.

## <a name="next-steps"></a>Следующие шаги

Создав пакет, то есть файл `.nupkg`, вы можете опубликовать его в любой коллекции на ваш выбор, как описано в разделе [Публикация пакета](../nuget-org/publish-a-package.md).

Вы также можете расширить возможности пакета или обеспечить поддержку других сценариев, как описано в следующих разделах:

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
