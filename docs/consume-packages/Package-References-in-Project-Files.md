---
title: Формат NuGet PackageReference (ссылки на пакеты в файлах проектов)
description: Подробные сведения о формате NuGet PackageReference в файлах проектов, который поддерживается в NuGet 4.0 и более поздних версиях, в VS2017 и в .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428507"
---
# <a name="package-references-packagereference-in-project-files"></a>Ссылки на пакеты (PackageReference) в файлах проектов

Ссылки на пакеты в узле `PackageReference` позволяют напрямую управлять зависимостями NuGet в файлах проекта (вместо использования отдельного файла `packages.config`). Использование PackageReference не влияет на другие аспекты NuGet. Например, параметры в файлах `NuGet.config` (включая источники пакетов) по-прежнему применяются, как описано в разделе [Распространенные конфигурации NuGet](configuring-nuget-behavior.md).

PackageReference также позволяет использовать условия MSBuild для выбора ссылок на пакеты в соответствии с целевой платформой и другими признаками. Он также обеспечивает детальный контроль над зависимостями и потоком содержимого. (Дополнительные сведения см. в разделе [Объекты pack и restore NuGet в качестве целевых объектов MSBuild](../reference/msbuild-targets.md).)

## <a name="project-type-support"></a>Поддержка типов проектов

По умолчанию PackageReference используется для проектов .NET Core, проектов .NET Standard и проектов универсальной платформы Windows, предназначенных для сборки 15063 системы Windows 10 (Creators Update), за исключением проектов C++ UWP. Проекты .NET Framework поддерживают PackageReference, но сейчас по умолчанию используют `packages.config`. Чтобы использовать PackageReference, [перенесите](../consume-packages/migrate-packages-config-to-package-reference.md) зависимости из `packages.config` в файл проекта, а затем удалите packages.config.

Приложения ASP.NET, предназначенные для полной версии .NET Framework, включают только [ограниченную поддержку](https://github.com/NuGet/Home/issues/5877) для PackageReference. Типы проектов C++и JavaScript не поддерживаются.

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

При указании версии пакета действует то же соглашение, что и при использовании файла `packages.config`.

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

В приведенном выше примере значение 3.6.0 означает версию 3.6.0 или любую более позднюю версию, причем предпочтение отдается самой ранней версии, как описано в разделе [Управление версиями пакета](../concepts/package-versioning.md#version-ranges).

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Использование PackageReference для проекта без объектов PackageReference

Дополнительно: Eсли в проекте нет установленных пакетов (нет объектов PackageReference в файле, а также файла packages.config), но вы хотите восстанавливать проект в стиле PackageReference, можно задать для свойства RestoreProjectStyle проекта значение PackageReference в файле проекта.

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

Это может быть удобно при ссылке на проекты в стиле PackageReference (существующие CSPROJ- или SDK-проекты). Это позволит вашему проекту транзитивно ссылаться на пакеты, на которые ссылаются эти проекты.

## <a name="packagereference-and-sources"></a>PackageReference и источники

В проектах PackageReference временные версии зависимостей разрешаются во время восстановления. Поэтому в них все источники должны быть доступны для всех операций восстановления. 

## <a name="floating-versions"></a>Гибкие версии

[Гибкие версии](../concepts/dependency-resolution.md#floating-versions) можно использовать с `PackageReference`:

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

| Тег | Описание | Значение по умолчанию |
| --- | --- | --- |
| IncludeAssets | Эти ресурсы будут использоваться. | все |
| ExcludeAssets | Эти ресурсы не будут использоваться. | Нет |
| PrivateAssets | Эти ресурсы будут использоваться, но не будут передаваться в родительский проект. | contentfiles;analyzers;build |

Ниже приводятся допустимые значения этих тегов. Несколько значений должны разделяться точкой с запятой. Это не относится к значениям `all` и `none`, которые должны использоваться отдельно.

| Значение | Описание |
| --- | ---
| compile | Содержимое папки `lib`; управляет возможностью компиляции проекта с использованием сборок в этой папке |
| исполняющая среда | Содержимое папки `lib` и `runtimes`; управляет возможностью копирования этих сборок в выходной каталог сборки |
| contentFiles | Содержимое папки `contentfiles` |
| выполнить сборку | `.props` и `.targets` в папке `build` |
| buildMultitargeting | Файлы `.props` и `.targets` *(4.0)* в папке `buildMultitargeting` для кроссплатформенного определения. |
| buildTransitive | Файлы `.props` и `.targets` *(5.0+)* в папке `buildTransitive` для ресурсов, которые можно транзитивно передавать в любой соответствующий проект. См. об [этой функции](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior). |
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

> [!NOTE]
> Когда для `developmentDependency` в файле `.nuspec` задано значение `true`, это указывает на то, что пакет помечен как зависимость только для разработки, что позволяет запретить его включение в качестве зависимости в другие пакеты. При использовании PackageReference *(NuGet 4.8+)* этот флажок также указывает на исключение ресурсов времени компиляции из компиляции. Дополнительные сведения см. в статье [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) (Поддержка DevelopmentDependency для PackageReference).

## <a name="adding-a-packagereference-condition"></a>Добавление условия PackageReference

С помощью условий можно управлять тем, когда следует включать пакет. В условиях можно использовать любые переменные MSBuild или переменные, определенные в файлах целей или свойств. Однако в настоящее время поддерживается только переменная `TargetFramework`.

Например, предположим, что целевыми платформами являются `netstandard1.4` и `net452`, но зависимость применима только для `net452`. В этом случае в проект `netstandard1.4`, который использует пакет, не следует добавлять эту ненужную зависимость. В этом случае в узле `PackageReference` можно указать следующее условие:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

При сборке пакета с использованием этого проекта файл Newtonsoft.Json будет отображаться как включенный только в виде зависимости для целевого объекта `net452`:

![Результат применения условия к PackageReference в Visual Studio 2017](media/PackageReference-Condition.png)

Условия можно также применять на уровне `ItemGroup`. В этом случае они применяются ко всем дочерним элементам `PackageReference`.

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a>GeneratePathProperty

Эта функция доступна в NuGet **5.0** или более поздней версии и в Visual Studio 2019 **16.0** или более поздней версии.

Иногда требуется ссылаться на файлы в пакете из целевого объекта MSBuild.
В проектах на основе `packages.config` пакеты устанавливаются в папку относительно файла проекта. Однако в PackageReference пакеты [используются](../concepts/package-installation-process.md) из папки *global-packages*, которая может отличаться на разных компьютерах.

Чтобы устранить эту проблему, NuGet предоставляет свойство, указывающее на расположение, из которого будет использоваться пакет.

Пример.

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

Кроме того, NuGet автоматически создаст свойства для пакетов, содержащих папку tools.

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

Свойства MSBuild и удостоверения пакетов не имеют одинаковых ограничений, поэтому удостоверение пакета необходимо изменить на понятное имя MSBuild с префиксом в виде слова `Pkg`.
Чтобы проверить точное имя создаваемого свойства, изучите созданный файл [nuget.g.props](../reference/msbuild-targets.md#restore-outputs).

## <a name="nuget-warnings-and-errors"></a>Предупреждения и ошибки NuGet

*Эта функция доступна в NuGet **4.3** или более поздней версии и в Visual Studio 2017 **15.3** или более поздней версии.*

Для многих сценариев упаковки и восстановления все предупреждения и ошибки NuGet кодируются и начинаются с `NU****`. Все предупреждения и ошибки NuGet перечислены в [справочной](../reference/errors-and-warnings.md) документации.

NuGet следит за следующими свойствами предупреждения:

- `TreatWarningsAsErrors` — обработка всех предупреждений как ошибок.
- `WarningsAsErrors` — обработка указанных предупреждений как ошибок.
- `NoWarn` — скрытие определенных предупреждений в масштабе проекта или пакета.

Примеры

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a>Подавление предупреждений NuGet

Хотя рекомендуется разрешать все предупреждения NuGet во время выполнения операций упаковки и восстановления, в некоторых ситуациях их подавление гарантируется.
Чтобы подавить предупреждение в масштабе проекта, рекомендуется сделать следующее:

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

Иногда предупреждения применяются только к определенному пакету в графе. Мы можем выборочно подавить такое предупреждение, добавив `NoWarn` к элементу PackageReference. 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a>Подавление предупреждений пакета NuGet в Visual Studio

В Visual Studio можно также [подавить предупреждения](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) в интегрированной среде разработки.

## <a name="locking-dependencies"></a>Блокировка зависимостей

*Эта функция доступна в NuGet **4.9** или более поздней версии и в Visual Studio 2017 **15.9** или более поздней версии.*

Входные данные для восстановления в NuGet — это набор ссылок на пакеты из файла проекта (зависимости верхнего уровня или прямые зависимости). Выходные данные — это полный набор всех зависимостей пакета, включая транзитивные зависимости. NuGet всегда пытается создать одну и ту же полную систему зависимостей пакета, если входной список PackageReference не был изменен. Но в некоторых случаях это нельзя осуществить. Пример:

* При использовании гибких версий, таких как `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`. При каждом восстановлении пакетов предполагается перейти к последней версии. Но иногда пользователям требуется, чтобы граф был закреплен за определенной последней версией, а переход к более поздней версии, если она доступна, происходил при явном указании.
* Опубликована более новая версия пакета PackageReference, которая соответствует требованиям к версии. Например, 

  * День 1. Предположим, вы указали `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, но в репозиториях NuGet были доступны версии 4.1.0, 4.2.0 и 4.3.0. В таком случае NuGet будет разрешен до версии 4.1.0 (ближайшей минимальной версии).

  * День 2: Публикуется версия 4.0.0. NuGet найдет точное соответствие и приступит разрешению до версии 4.0.0.

* Указанная версия пакета будет удалена из репозитория. Хотя на сайте nuget.org нельзя удалять пакеты, не все репозитории пакетов имеют такие ограничения. В результате этого в NuGet выполняется поиск наиболее соответствующей версии, если не удается разрешить удаленную версию.

### <a name="enabling-lock-file"></a>Включение функции файла блокировки

Чтобы сохранить всю систему зависимостей пакета, можно воспользоваться функцией файла блокировки. Для этого задайте свойство MSBuild `RestorePackagesWithLockFile` для проекта:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Если это свойство задано, при восстановлении в NuGet будет создан файл блокировки — `packages.lock.json`. Он содержит список всех зависимостей пакета и находится в корневом каталоге проекта. 

> [!Note]
> Когда в корневом каталоге проекта появится файл блокировки `packages.lock.json`, он будет использоваться при каждом восстановлении, даже если свойство `RestorePackagesWithLockFile` не задано. Еще один способ воспользоваться этой функцией — создать пустой файл `packages.lock.json` в корневом каталоге проекта.

### <a name="restore-behavior-with-lock-file"></a>Поведение `restore` при использовании файла блокировки
Если для проекта создан файл блокировки, NuGet использует этот файл для запуска `restore`. NuGet быстро проверяет наличие изменений в зависимостях пакетов, как указано в файле проекта (или в зависимых файлах проекта). Если такие изменения не обнаружены, NuGet просто восстанавливает пакеты, указанные в файле блокировки. Повторная проверка зависимостей пакета не выполняется.

Если диспетчер NuGet обнаруживает изменения в определенных зависимостях, указанных в файлах проекта, NuGet повторно проверяет граф пакета и обновляет файл блокировки в соответствии с новой схемой пакета для проекта.

В сценариях CI/CD и других сценариях, не требующих изменения зависимостей пакета во время выполнения, это можно сделать, задав для `lockedmode` значение `true`:

Для dotnet.exe выполните следующую команду:

```
> dotnet.exe restore --locked-mode
```

Для msbuild.exe выполните такую команду:

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

Это условное свойство MSBuild также можно задать в файле проекта:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

Если для режима блокировки задано значение `true`, восстановятся именно те пакеты, которые перечислены в файле блокировки. Либо восстановление завершится ошибкой, если вы обновили определенные зависимости пакетов для проекта после создания файла блокировки.

### <a name="make-lock-file-part-of-your-source-repository"></a>Добавление файла блокировки в исходный репозиторий
Если при создании приложения вы обнаружили, что исполняемый файл и рассматриваемый проект находятся в начале цепочки зависимостей, верните файл блокировки в репозиторий исходного кода. Так диспетчер NuGet сможет использовать его во время восстановления.

Но если это проект библиотеки, который не следует отправлять, или проект общего кода, от которого зависят другие проекты, **не нужно** возвращать файл блокировки в исходный код. Сохранение файла блокировки не причинит вреда. Но заблокированные зависимости пакетов, перечисленные в файле блокировки, нельзя использовать для проекта общего кода во время восстановления или сборки проекта, который зависит от этого проекта общего кода.

Пример

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

Если `ProjectA` зависит от `PackageX` версии `2.0.0` и ссылается на проект `ProjectB`, который зависит от `PackageX` версии `1.0.0`, файл блокировки для `ProjectB` будет содержать зависимость от `PackageX` версии `1.0.0`. Но при создании проекта `ProjectA` его файл блокировки будет содержать зависимость от `PackageX` версии **`2.0.0`** , а **не** `1.0.0`, как указано в файле блокировки для `ProjectB`. Таким образом, файл блокировки проекта общего кода играет незначительную роль для разрешенных пакетов, от которых зависят проекты.

### <a name="lock-file-extensibility"></a>Расширяемость файла блокировки

Вы можете управлять различным поведением восстановления с использованием файла блокировки, как описано ниже.

| Вариант NuGet.exe | Вариант dotnet | Вариант, аналогичный использованию MSBuild | Описание |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | RestorePackagesWithLockFile | Разрешение использовать файл блокировки. |
| `-LockedMode` | `--locked-mode` | RestoreLockedMode | Включение режима блокировки для восстановления. Это полезно в сценариях CI/CD, когда нужно реализовать воспроизводимые сборки.|   
| `-ForceEvaluate` | `--force-evaluate` | RestoreForceEvaluate | Этот параметр удобно использовать с пакетами с гибкими версиями, определенными в проекте. По умолчанию в NuGet версия пакета не обновляется автоматически после каждого восстановления, если вы не запустили восстановление с этим параметром. |
| `-LockFilePath` | `--lock-file-path` | NuGetLockFilePath | Определение размещения пользовательского файла блокировки для проекта. По умолчанию в NuGet файл `packages.lock.json` хранится в корневом каталоге. Если в одном каталоге хранится несколько проектов, NuGet поддерживает использование файла блокировки `packages.<project_name>.lock.json` для определенного проекта. |
