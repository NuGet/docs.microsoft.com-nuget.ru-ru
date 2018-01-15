---
title: "Формат NuGet PackageReference в файлах проектов Visual Studio | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "Подробные сведения о формате NuGet PackageReference в файлах проектов, который поддерживается в NuGet 4.0 и более поздних версиях и в Visual Studio 2017"
keywords: "зависимости пакета NuGet, ссылки на пакеты, файлы проекта, PackageReference, packages.config, project.json, VS2017, Visual Studio 2017, NuGet 4"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 275957c94e4a4bb45f359cd48816acf4f286ebad
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="package-references-packagereference-in-project-files"></a>Ссылки на пакеты (PackageReference) в файлах проектов

Ссылки на пакеты в узле `PackageReference` позволяют напрямую управлять зависимостями NuGet в файлах проекта вместо использования отдельного файла `packages.config` или `project.json`. Этот метод не влияет на другие аспекты NuGet. Например, параметры в файлах `NuGet.Config` (включая источники пакетов) по-прежнему применяются, как описано в разделе [Настройка поведения NuGet](Configuring-NuGet-Behavior.md).

> [!Important]
> В настоящее время ссылки на пакеты поддерживаются только в Visual Studio 2017 для проектов .NET Core, проектов .NET Standard и проектов универсальной платформы Windows, предназначенных для сборки 15063 системы Windows 10 (Creators Update).

Подход на основе `PackageReference` позволяет использовать условия MSBuild для выбора ссылок на пакеты в соответствии с целевой платформой, конфигурацией, платформой устройств и другими признаками. Он также обеспечивает детальный контроль над зависимостями и потоком содержимого. В плане реакции на события и [разрешения зависимостей](Dependency-Resolution.md) он аналогичен использованию `project.json`.

Дополнительные сведения об интеграции MSBuild со ссылками на пакеты в файлах проектов см. в разделе [Команды NuGet pack и restore как цели MSBuild](../schema/msbuild-targets.md).

## <a name="adding-a-packagereference"></a>Добавление PackageReference

Добавьте зависимость в файл проекта, используя следующий синтаксис:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />    
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Управление версией зависимости

При указании версии пакета действует то же соглашение, что и при использовании файла `packages.config` или `project.json`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

В приведенном выше примере значение 3.6.0 означает версию 3.6.0 или любую более позднюю версию, причем предпочтение отдается самой ранней версии, как описано в разделе [Управление версиями пакета](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="floating-versions"></a>Гибкие версии

[Гибкие версии](../consume-packages/dependency-resolution.md#floating-versions) можно использовать с `PackageReference`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Управление ресурсами зависимости

Зависимость может применяться исключительно для удобства разработки. В этом случае доступ к ней не нужно предоставлять проектам, использующим пакет. Для управления таким поведением могут служить метаданные `PrivateAssets`.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Ниже перечислены теги метаданных, управляющие ресурсами зависимостей.

| Тег | Описание: | Значение по умолчанию |
| --- | --- | --- |
| IncludeAssets | Эти ресурсы будут использоваться. | все |
| ExcludeAssets | Эти ресурсы не будут использоваться. | Нет | 
| PrivateAssets | Эти ресурсы будут использоваться, но не будут передаваться в родительский проект. | contentfiles;analyzers;build |


Ниже приводятся допустимые значения этих тегов. Несколько значений должны разделяться точкой с запятой. Это не относится к значениям `all` и `none`, которые должны использоваться отдельно.

| Значение | Описание: |
| --- | ---
| compile | Содержимое папки `lib` |
| исполняющая среда | Содержимое папки `runtime` |
| contentFiles | Содержимое папки `contentfiles` |
| выполнить сборку | Свойства и цели в папке `build` |
| analyzers | Анализаторы .NET |
| в машинном коде | Содержимое папки `native` |
| Нет | Никакие из перечисленных выше ресурсов не используются. |
| все | Используются все перечисленные выше ресурсы (кроме `none`). |

В приведенном ниже примере проектом используются все ресурсы, кроме файлов содержимого из пакета, и в родительский проект передаются все ресурсы, кроме файлов содержимого и анализаторов.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Обратите внимание: так как папка `build` не включена в `PrivateAssets`, цели и свойства *будут* передаваться в родительский проект. Предположим, что приведенная выше ссылка используется в проекте, в рамках которого выполняется сборка пакета NuGet с именем AppLogger. Пакет AppLogger может использовать цели и свойства из `Contoso.Utility.UsefulStuff`, так же как и проекты, использующие AppLogger.

## <a name="adding-a-packagereference-condition"></a>Добавление условия PackageReference

С помощью условий можно управлять тем, когда следует включать пакет. В условиях можно использовать любые переменные MSBuild или переменные, определенные в файлах целей или свойств. Однако в настоящее время поддерживается только переменная `TargetFramework`.

Например, предположим, что целевыми платформами являются `netstandard1.4` и `net452`, но зависимость применима только для `net452`. В этом случае в проект `netstandard1.4`, который использует пакет, не следует добавлять эту ненужную зависимость. В этом случае в узле `PackageReference` можно указать следующее условие:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

В пакет, сборка которого выполнена с помощью этого проекта, файл Newtonsoft.json будет включен в качестве зависимости только для целевой платформы `net452`.

![Результат применения условия к PackageReference в Visual Studio 2017](media/PackageReference-Condition.png)

Условия можно также применять на уровне `ItemGroup`. В этом случае они применяются ко всем дочерним элементам `PackageReference`.

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
