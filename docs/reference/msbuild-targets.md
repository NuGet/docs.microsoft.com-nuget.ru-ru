---
title: Объекты pack и restore NuGet в качестве целевых объектов MSBuild
description: Объекты pack и restore NuGet могут выступать непосредственно в качестве целевых объектов MSBuild в NuGet 4.0+.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 7b3fc72ddd3ad6c9185c2bd0f2563df59e77f1c8
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453550"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>Объекты pack и restore NuGet в качестве целевых объектов MSBuild

*NuGet 4.0+*

Благодаря формату PackageReference в NuGet 4.0 и более поздних версиях все метаданные манифеста могут храниться прямо в файле проекта, не требуя использования отдельного файла `.nuspec`.

При использовании MSBuild 15.1+ NuGet также является привилегированным компонентом MSBuild с целевыми объектами `pack` и `restore`, как описано ниже. Эти целевые объекты позволяют работать с NuGet, как с любой другой задачей или другим целевым объектом MSBuild. (Для NuGet 3.x и более ранних версий можно использовать команды [pack](../tools/cli-ref-pack.md) и [restore](../tools/cli-ref-restore.md) в NuGet CLI.)

## <a name="target-build-order"></a>Порядок сборки целевого объекта

Так как `pack` и `restore` являются целевыми объектами MSBuild, вы можете обращаться к ним для улучшения рабочего процесса. Например, предположим, что вам нужно скопировать пакет в общую сетевую папку после его упаковки. Это можно сделать, добавив следующий код в файл проекта:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

Аналогичным образом, вы можете создать задачу MSBuild и собственный целевой объект и использовать свойства NuGet в этой задаче MSBuild.

## <a name="pack-target"></a>Целевой объект pack

Для проектов .NET Standard с помощью формата PackageReference, `msbuild -t:pack` рисует входные данные из файла проекта для использования при создании пакета NuGet.

В следующей таблице описываются свойства MSBuild, которые можно добавить в файл проекта в первом узле `<PropertyGroup>`. Эти изменения легко внести в Visual Studio 2017 и более поздней версии, щелкнув проект правой кнопкой мыши и выбрав пункт **Изменить {project_name}**. Для удобства таблица упорядочена по эквивалентным свойствам в [файле `.nuspec`](../reference/nuspec.md).

Обратите внимание, что свойства `Owners` и `Summary` из `.nuspec` не поддерживаются в MSBuild.

| Значение атрибута или NuSpec | Свойство MSBuild | Значение по умолчанию | Примечания |
|--------|--------|--------|--------|
| Идентификатор | PackageId | AssemblyName | $(AssemblyName) из MSBuild |
| Версия | PackageVersion | Версия | Это значение совместимо с SemVer, например "1.0.0", "1.0.0-beta" или "1.0.0-beta-00345" |
| VersionPrefix | PackageVersionPrefix | пустой | Задав PackageVersion, вы перезапишите PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | пустой | $(VersionSuffix) из MSBuild. Задав PackageVersion, вы перезапишите PackageVersionSuffix |
| Authors | Authors | Имя текущего пользователя | |
| Владельцы | Н/Д | Не существует в NuSpec | |
| Заголовок | Заголовок | Идентификатор пакета| |
| Описание: | Описание: | "Описание пакета" | |
| Copyright | Copyright | пустой | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | False | |
| лицензии | PackageLicenseExpression | пустой | Соответствует `<license type="expression">` |
| лицензии | PackageLicenseFile | пустой | Соответствует `<license type="file">`. Может потребоваться явно пакета файл лицензии, на которую указывает ссылка. |
| LicenseUrl | PackageLicenseUrl | пустой | `licenseUrl` является устаревшим, используйте свойство PackageLicenseExpression или PackageLicenseFile |
| ProjectUrl | PackageProjectUrl | пустой | |
| IconUrl | PackageIconUrl | пустой | |
| Теги | PackageTags | пустой | Теги разделяются точкой с запятой. |
| ReleaseNotes | PackageReleaseNotes | пустой | |
| URL-адрес репозитория / | RepositoryUrl | пустой | URL-адрес репозитория можно клонировать или загрузить исходный код. Пример: *https://github.com/NuGet/NuGet.Client.git* |
| / Тип репозитория | RepositoryType | пустой | Тип репозитория. Примеры: *git*, *tfs*. |
| Репозитория или ветви | RepositoryBranch | пустой | Сведения о ветви необязательно репозитории. *RepositoryUrl* также должен быть указан для этого свойства для включения. Пример: *master* (NuGet 4.7.0+) |
| Репозиторий и фиксации | RepositoryCommit | пустой | Необязательный репозитория фиксацию или набор изменений, чтобы указать, что источник пакета было выполнено построение. *RepositoryUrl* также должен быть указан для этого свойства для включения. Пример: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Сводка | Не поддерживается | | |

### <a name="pack-target-inputs"></a>Входные данные целевого объекта pack

- IsPackable
- PackageVersion
- PackageId
- Authors
- Описание:
- Copyright
- PackageRequireLicenseAcceptance
- DevelopmentDependency
- PackageLicenseExpression
- PackageLicenseFile
- PackageLicenseUrl
- PackageProjectUrl
- PackageIconUrl
- PackageReleaseNotes
- PackageTags
- PackageOutputPath
- IncludeSymbols
- IncludeSource
- PackageTypes
- IsTool
- RepositoryUrl
- RepositoryType
- RepositoryBranch
- RepositoryCommit
- NoPackageAnalysis
- MinClientVersion
- IncludeBuildOutput
- IncludeContentInPack
- BuildOutputTargetFolder
- ContentTargetFolders
- NuspecFile
- NuspecBasePath
- NuspecProperties

## <a name="pack-scenarios"></a>Сценарии использования pack

### <a name="packageiconurl"></a>PackageIconUrl

В процессе изменения для [352 проблема NuGet](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` со временем изменяется `PackageIconUri` и может быть относительным путем к файлу значка, который будет включен в корень итогового пакета.

### <a name="output-assemblies"></a>Выходные сборки

`nuget pack` копирует выходные файлы с расширениями `.exe`, `.dll`, `.xml`, `.winmd`, `.json` и `.pri`. Копируемые выходные файлы зависят от того, что MSBuild предоставляет из целевого объекта `BuiltOutputProjectGroup`.

Существует два свойства MSBuild, которые можно использовать в файле проекта или командной строке для управления местом назначения для выходных сборок:

- `IncludeBuildOutput`: логическое значение, определяющее, следует ли включать выходные сборки в пакете.
- `BuildOutputTargetFolder`: указывает папку, куда следует помещать выходные сборки. Выходные сборки (и другие выходные файлы) копируются в соответствующие папки платформы.

### <a name="package-references"></a>Ссылки на пакеты

См. раздел [Ссылки на пакеты в файлах проекта](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Перекрестные ссылки между проектами

Перекрестные ссылки между проектами по умолчанию считаются ссылками на пакет NuGet, например:

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

Вы также можете добавить в ссылку на проект следующие метаданные:

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>Включение содержимого в пакет

Чтобы включить содержимое, добавьте дополнительные метаданные для существующего элемента `<Content>`. По умолчанию все данные типа "Content" включаются в пакет, если только вы не переопределите такое поведение с помощью записей, аналогичных следующим:

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

По умолчанию все данные добавляются в корень папки `content` и `contentFiles\any\<target_framework>` в пакете и сохраняют относительную структуру папок, если только не указан путь к пакету:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Если требуется скопировать все содержимое только в определенные корневые папки (вместо `content` и `contentFiles`), можно использовать свойство MSBuild `ContentTargetFolders`, которое по умолчанию имеет значение "content;contentFiles", но может принимать любые другие имена папок. Обратите внимание, если указать "contentFiles" в `ContentTargetFolders`, файлы помещаются в `contentFiles\any\<target_framework>` или `contentFiles\<language>\<target_framework>` в зависимости от `buildAction`.

`PackagePath` может быть набором целевых путей, разделенных точкой с запятой. Если указан пустой путь к пакету, файл добавляется в корневой каталог пакета. Например, следующий код добавляет `libuv.txt` в `content\myfiles`, `content\samples` и корневой каталог пакета:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Имеется также свойство MSBuild `$(IncludeContentInPack)`, которое по умолчанию равно `true`. Если оно имеет значение `false` для какого-либо проекта, то содержимое этого проекта не включается в пакет NuGet.

Другие относящиеся к pack метаданные, которые можно задать для любого из указанных выше элементов, включают ```<PackageCopyToOutput>``` и ```<PackageFlatten>```, задающие значения ```CopyToOutput``` и ```Flatten``` для записи ```contentFiles``` в выходном файле NUSPEC.

> [!Note]
> Кроме элементов содержимого, метаданные `<Pack>` и `<PackagePath>` также можно задать для файлов с действием сборки Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource или None.
>
> Чтобы объект pack добавил имя файла в путь к пакету при использовании стандартных масок, путь к пакету должен заканчиваться символом разделителя папок, в противном случае этот путь считается полным путем, включающим имя файла.

### <a name="includesymbols"></a>IncludeSymbols

При использовании `MSBuild -t:pack -p:IncludeSymbols=true` соответствующие файлы `.pdb` копируются вместе с другими выходными файлами (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Обратите внимание, что при задании `IncludeSymbols=true` создается обычный пакет *и* пакет символов.

### <a name="includesource"></a>IncludeSource

Аналогично `IncludeSymbols`, только копирует исходные файлы вместе с файлами `.pdb`. Все файлы типа `Compile` копируются в `src\<ProjectName>\` с сохранением относительной структуры папок в итоговом пакете. То же самое происходит с исходными файлами любого `ProjectReference`, у которого `TreatAsPackageReference` имеет значение `false`.

Если файл типа Compile находится вне папки проекта, он просто добавляется в `src\<ProjectName>\`.

### <a name="packing-a-license-expression-or-a-license-file"></a>Упаковка выражении лицензии или файл лицензии

При использовании выражения лицензии, следует использовать свойство PackageLicenseExpression. 
[Пример выражения лицензии](#https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).

При упаковке файл лицензии, необходимо использовать свойство PackageLicenseFile чтобы указать путь к пакету, относительно корня пакета. Кроме того необходимо убедиться, что файл включается в пакет. Пример:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath="$(PackageLicenseFile)"/>
</ItemGroup>
```
[Образец лицензии жизнь](#https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).

### <a name="istool"></a>IsTool

При использовании `MSBuild -t:pack -p:IsTool=true` все выходные файлы, как указано в сценарии [Выходные сборки](#output-assemblies), копируются в папку `tools` вместо папки `lib`. Обратите внимание, что это свойство отличается от `DotNetCliTool`, которое указывается путем задания `PackageType` в файле `.csproj`.

### <a name="packing-using-a-nuspec"></a>Упаковка с помощью NUSPEC

Можно использовать `.nuspec` файл для упаковки проекта, при условии, что у вас есть файл проекта SDK для импорта `NuGet.Build.Tasks.Pack.targets` , чтобы можно было выполнить задачу пакета. По-прежнему необходимо восстановить проект, прежде чем можно упаковать в файл nuspec. Требуемая версия .NET framework файл проекта не имеет значения и не использовались при упаковке nuspec. Следующие три свойства MSBuild связаны с упаковкой с помощью `.nuspec`:

1. `NuspecFile`: относительный или абсолютный путь к файлу `.nuspec`, используемому для упаковки.
1. `NuspecProperties`: список разделенных точками с запятой пар "ключ-значение". Из-за особенностей работы анализа в командной строке MSBuild несколько свойств нужно указать следующим образом: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.  
1. `NuspecBasePath`: базовый путь для файла `.nuspec`.

Если вы используете `dotnet.exe` для упаковки проекта, воспользуйтесь командой, аналогичной следующей:

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Если вы используете MSBuild для упаковки проекта, воспользуйтесь командой, аналогичной следующей:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Обратите внимание на то, что упаковки nuspec использование dotnet.exe или msbuild также приводит к сборке проекта по умолчанию. Этого можно избежать путем передачи ```--no-build``` dotnet.exe, это эквивалентно заданию свойства ```<NoBuild>true</NoBuild> ``` в файле проекта, а также параметр ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` в файле проекта

Приведен пример файла csproj, упаковать в файл nuspec.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a>Дополнительные точки расширения, чтобы создать настроенный пакет

`pack` Целевой предоставляет две точки расширения, которые работают в определенной сборки внутренний целевой платформы. Точки расширения поддерживают определенное содержимое целевой платформы и сборки в пакет:

- `TargetsForTfmSpecificBuildOutput` целевой объект: используется для файлов в `lib` папка или папка, заданные с помощью `BuildOutputTargetFolder`.
- `TargetsForTfmSpecificContentInPackage` целевой объект: используется для файлов за пределами `BuildOutputTargetFolder`.

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

Запишите пользовательский целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificBuildOutput)` свойство. Для всех файлов, которые необходимо перевести в `BuildOutputTargetFolder` (по умолчанию), lib целевой объект должен записывать файлы в ItemGroup `BuildOutputInPackage` и задайте следующие два значения метаданных:

- `FinalOutputPath`: Абсолютный путь к файлу; Если не указано, удостоверение используется для оценки исходный путь.
- `TargetPath`: (Необязательно) значение, когда файл должен располагаться в подпапке в `lib\<TargetFramework>` , такие как вспомогательные сборки, учитываемых в своих папках соответствующего языка и региональных параметров. По умолчанию указывается имя файла.

Пример

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a>TargetsForTfmSpecificContentInPackage

Запишите пользовательский целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificContentInPackage)` свойство. Для всех файлов, включаемых в пакет, целевой объект должен записывать файлы в ItemGroup `TfmSpecificPackageFile` и задайте следующие необязательные метаданные:

- `PackagePath`: Путь, где этот файл должен быть выходные данные в пакете. NuGet выдает предупреждение, если же путь к пакету добавляется более одного файла.
- `BuildAction`: Действие построения файла, требуется только путь к пакету в `contentFiles` папку. По умолчанию — «None».

Пример:
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a>Целевой объект restore

`MSBuild -t:restore` (который `nuget restore` и `dotnet restore` используют с проектами .NET Core) восстанавливает пакеты, на которые ссылается файл проекта:

1. Чтение перекрестных ссылок между проектами.
1. Чтение свойств проекта, чтобы найти промежуточную папку и целевые платформы.
1. Передача данных MSBuild в NuGet.Build.Tasks.dll.
1. Запуск восстановления.
1. Скачивание пакетов.
1. Запись файла ресурсов, целевых объектов и свойств.

`restore` Целевой works **только** для проектов, использующих формат PackageReference. Да **не** работают для проектов с помощью `packages.config` форматирования; используйте [восстановление nuget](../tools/cli-ref-restore.md) вместо этого.

### <a name="restore-properties"></a>Свойства восстановления

Дополнительные параметры восстановления могут поступать из свойств MSBuild в файле проекта. Значения также можно задать из командной строки с помощью параметра `-p:` (см. примеры ниже).

| Свойство. | Описание: |
|--------|--------|
| RestoreSources | Разделенный точками с запятой список источников пакетов. |
| RestorePackagesPath | Путь к папке пакетов пользователя. |
| RestoreDisableParallel | Ограничение скачиваний до одного за раз. |
| RestoreConfigFile | Путь к применяемому файлу `Nuget.Config`. |
| RestoreNoCache | Если значение равно true, позволяет избежать использования кэшированные пакеты. См. в разделе [управление папкой установки глобальных пакетов и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| RestoreIgnoreFailedSources | Если значение равно true, нерабочие или отсутствующие источники пакетов игнорируются. |
| RestoreTaskAssemblyFile | Путь к `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Разделенный точками с запятой список проектов для восстановления, который должен содержать абсолютные пути. |
| RestoreOutputPath | Выходная папка, по умолчанию используется `obj`. |

#### <a name="examples"></a>Примеры

Командная строка:

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

Файл проекта:

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a>Выходные данные восстановления

Операция восстановления создает в папке сборки `obj` следующие файлы:

| Файл | Описание: |
|--------|--------|
| `project.assets.json` | Содержит все ссылки на пакеты в графе зависимостей. |
| `{projectName}.projectFileExtension.nuget.g.props` | Ссылки на свойства MSBuild, содержащиеся в пакетах. |
| `{projectName}.projectFileExtension.nuget.g.targets` | Ссылки на целевые объекты MSBuild, содержащиеся в пакетах. |

### <a name="packagetargetfallback"></a>PackageTargetFallback

Элемент `PackageTargetFallback` позволяет указать набор совместимых целевых объектов, которые следует использовать при восстановлении пакетов. Он разрешает пакетам, использующим dotnet [TxM](../reference/target-frameworks.md), взаимодействовать с совместимыми пакетами, которые не объявляют dotnet TxM. Таким образом, если в проекте используется dotnet TxM, все пакеты, от которых вы зависите, должны также содержать dotnet TxM. В противном случае нужно добавить `<PackageTargetFallback>` в проект, чтобы обеспечить совместимость с платформами, отличными от dotnet.

Например, если в проекте используется `netstandard1.6` TxM, а зависимый пакет содержит только `lib/net45/a.dll` и `lib/portable-net45+win81/a.dll`, то сборка проекта завершится со сбоем. Если вы хотите использовать вторую библиотеку DLL, можете добавить `PackageTargetFallback` следующим образом, чтобы обозначить совместимость библиотеки DLL `portable-net45+win81`:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

Чтобы объявить откат для всех целевых объектов в проекте, оставьте атрибут `Condition`. Кроме того, можно расширить существующий `PackageTargetFallback`, включив `$(PackageTargetFallback)`, как показано ниже:

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a>Замена одной библиотеки из графа восстановления

Если операция восстановления предоставляет неправильную сборку, вы можете исключить значение по умолчанию для этого пакета, заменив его своим значением. Первый с `PackageReference` верхнего уровня, исключите все ресурсы:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

После этого добавьте собственную ссылку на соответствующую локальную копию библиотеки DLL:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
