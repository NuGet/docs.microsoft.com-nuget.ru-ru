---
title: Объекты pack и restore NuGet в качестве целевых объектов MSBuild
description: Объекты pack и restore NuGet могут выступать непосредственно в качестве целевых объектов MSBuild в NuGet 4.0+.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 8e662194fffc031d0cfc0aa129a5a15b555a4231
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/23/2019
ms.locfileid: "68420013"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>Объекты pack и restore NuGet в качестве целевых объектов MSBuild

*NuGet 4.0+*

В формате [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + может хранить все метаданные манифеста непосредственно в файле проекта вместо использования отдельного `.nuspec` файла.

При использовании MSBuild 15.1+ NuGet также является привилегированным компонентом MSBuild с целевыми объектами `pack` и `restore`, как описано ниже. Эти целевые объекты позволяют работать с NuGet, как с любой другой задачей или другим целевым объектом MSBuild. (Для NuGet 3.x и более ранних версий можно использовать команды [pack](../reference/cli-reference/cli-ref-pack.md) и [restore](../reference/cli-reference/cli-ref-restore.md) в NuGet CLI.)

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

Для .NET Standard проектов, использующих формат PackageReference `msbuild -t:pack` , команда рисует входные данные из файла проекта для использования при создании пакета NuGet.

В следующей таблице описываются свойства MSBuild, которые можно добавить в файл проекта в первом узле `<PropertyGroup>`. Эти изменения легко внести в Visual Studio 2017 и более поздней версии, щелкнув проект правой кнопкой мыши и выбрав пункт **Изменить {project_name}** . Для удобства таблица упорядочена по эквивалентным свойствам в [файле `.nuspec`](../reference/nuspec.md).

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
| Описание | Описание | "Описание пакета" | |
| Copyright | Copyright | пустой | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | False | |
| Лицензии | PackageLicenseExpression | пустой | Соответствует`<license type="expression">` |
| Лицензии | PackageLicenseFile | пустой | Соответствует `<license type="file">`. Возможно, потребуется явно упаковать файл лицензии, на который указывает ссылка. |
| LicenseUrl | PackageLicenseUrl | пустой | `licenseUrl`является устаревшим, используйте свойство Паккажелиценсикспрессион или Паккажелиценсефиле. |
| ProjectUrl | PackageProjectUrl | пустой | |
| IconUrl | PackageIconUrl | пустой | |
| Теги | PackageTags | пустой | Теги разделяются точкой с запятой. |
| ReleaseNotes | PackageReleaseNotes | пустой | |
| Репозиторий/URL-адрес | RepositoryUrl | пустой | URL-адрес репозитория, используемый для клонирования или извлечения исходного кода. Например *https://github.com/NuGet/NuGet.Client.git* |
| Репозиторий или тип | RepositoryType | пустой | Тип репозитория. Примеры: *Git*, *TFS*. |
| Репозиторий или ветвь | репоситорибранч | пустой | Дополнительные сведения о ветви репозитория. Для включения этого свойства также необходимо указать *репоситорюрл* . Пример: *master* (NuGet 4.7.0 +) |
| Репозиторий/фиксация | репоситорикоммит | пустой | Необязательная фиксация или набор изменений репозитория для указания источника, на основе которого был создан пакет. Для включения этого свойства также необходимо указать *репоситорюрл* . Пример *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Сводка | Не поддерживается | | |

### <a name="pack-target-inputs"></a>Входные данные целевого объекта pack

- IsPackable
- суппрессдепенденЦиесвхенпаккинг
- PackageVersion
- PackageId
- Authors
- Описание
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
- репоситорибранч
- репоситорикоммит
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

### <a name="suppress-dependencies"></a>Подавлять зависимости

Чтобы исключить зависимости пакета из созданного пакета NuGet, `SuppressDependenciesWhenPacking` задайте `true` для значение, которое позволит пропустить все зависимости из созданного файла nupkg.

### <a name="packageiconurl"></a>PackageIconUrl

Как часть изменения для проблемы с [NuGet 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` в конечном итоге будет изменен на `PackageIconUri` и может быть относительным путем к файлу значка, который будет включен в корень полученного пакета.

### <a name="output-assemblies"></a>Выходные сборки

`nuget pack` копирует выходные файлы с расширениями `.exe`, `.dll`, `.xml`, `.winmd`, `.json` и `.pri`. Копируемые выходные файлы зависят от того, что MSBuild предоставляет из целевого объекта `BuiltOutputProjectGroup`.

Существует два свойства MSBuild, которые можно использовать в файле проекта или командной строке для управления местом назначения для выходных сборок:

- `IncludeBuildOutput`: Логическое значение, определяющее, следует ли включать в пакет сборки выходных данных сборки.
- `BuildOutputTargetFolder`: Указывает папку, в которой должны размещаться выходные сборки. Выходные сборки (и другие выходные файлы) копируются в соответствующие папки платформы.

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

### <a name="packing-a-license-expression-or-a-license-file"></a>Упаковка выражения лицензии или файла лицензии

При использовании выражения лицензии следует использовать свойство Паккажелиценсикспрессион. 
[Пример выражения лицензии](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

Дополнительные [сведения о лицензионных выражениях и лицензиях, принимаемых NuGet.org](nuspec.md#license).

При упаковке файла лицензии необходимо использовать свойство Паккажелиценсефиле, чтобы указать путь к пакету относительно корня пакета. Кроме того, необходимо убедиться, что файл включен в пакет. Например:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
[Пример файла лицензии](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).

### <a name="istool"></a>IsTool

При использовании `MSBuild -t:pack -p:IsTool=true` все выходные файлы, как указано в сценарии [Выходные сборки](#output-assemblies), копируются в папку `tools` вместо папки `lib`. Обратите внимание, что это свойство отличается от `DotNetCliTool`, которое указывается путем задания `PackageType` в файле `.csproj`.

### <a name="packing-using-a-nuspec"></a>Упаковка с помощью NUSPEC

Хотя рекомендуется включить в файл проекта [все свойства](../reference/msbuild-targets.md#pack-target) , которые обычно находятся в `.nuspec` файле, можно использовать `.nuspec` файл для упаковки проекта. Для проекта в стиле, отличном от SDK, `PackageReference`который использует, необходимо `NuGet.Build.Tasks.Pack.targets` импортировать, чтобы можно было выполнить задачу «Pack». Вам по-прежнему потребуется восстановить проект, чтобы можно было упаковать файл nuspec. (Проект в стиле SDK включает целевые объекты Pack по умолчанию.)

Целевая платформа файла проекта несущественна и не используется при упаковке nuspec. Следующие три свойства MSBuild связаны с упаковкой с помощью `.nuspec`:

1. `NuspecFile`: относительный или абсолютный путь к файлу `.nuspec`, используемому для упаковки.
1. `NuspecProperties`: список разделенных точками с запятой пар "ключ-значение". Из-за особенностей работы анализа в командной строке MSBuild несколько свойств нужно указать следующим образом: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.  
1. `NuspecBasePath`: Базовый путь `.nuspec` к файлу.

Если вы используете `dotnet.exe` для упаковки проекта, воспользуйтесь командой, аналогичной следующей:

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Если вы используете MSBuild для упаковки проекта, воспользуйтесь командой, аналогичной следующей:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Обратите внимание, что упаковка a nuspec с помощью DotNet. exe или MSBuild также ведет к построению проекта по умолчанию. Это можно избежать, передав ```--no-build``` свойство в файл DotNet. exe, эквивалентное параметру ```<NoBuild>true</NoBuild> ``` в файле проекта, а также задав параметр ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` в файле проекта.

Пример файла *. csproj* для упаковки файла nuspec:

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

### <a name="advanced-extension-points-to-create-customized-package"></a>Дополнительные точки расширения для создания настраиваемого пакета

`pack` Целевой объект предоставляет две точки расширения, которые выполняются во внутренней и целевой сборке конкретной платформы. Поддержка точек расширения включает в пакет содержимое и сборки, относящиеся к целевой платформе.

- `TargetsForTfmSpecificBuildOutput`мишень Используется для файлов в `lib` папке или в папке, заданной с помощью. `BuildOutputTargetFolder`
- `TargetsForTfmSpecificContentInPackage`мишень Используется для файлов за пределами `BuildOutputTargetFolder`.

#### <a name="targetsfortfmspecificbuildoutput"></a>таржетсфортфмспеЦификбуилдаутпут

Напишите настраиваемый целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificBuildOutput)` свойства. Для файлов, которые необходимо `BuildOutputTargetFolder` переключать в (LIB по умолчанию), целевой объект должен записать эти файлы в ItemGroup `BuildOutputInPackage` и задать следующие два значения метаданных:

- `FinalOutputPath`: Абсолютный путь к файлу; Если этот параметр не указан, для вычисления исходного пути используется удостоверение.
- `TargetPath`:  Используемых Задается, когда файл необходимо переключиться во `lib\<TargetFramework>` вложенную папку в, например вспомогательные сборки, которые находятся в соответствующих папках языка и региональных параметров. По умолчанию используется имя файла.

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

#### <a name="targetsfortfmspecificcontentinpackage"></a>таржетсфортфмспеЦификконтентинпаккаже

Напишите настраиваемый целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificContentInPackage)` свойства. Для всех файлов, включаемых в пакет, целевой объект должен записать эти файлы в ItemGroup `TfmSpecificPackageFile` и задать следующие необязательные метаданные:

- `PackagePath`: Путь, по которому файл должен быть выведен в пакете. NuGet выдает предупреждение, если в один и тот же путь к пакету добавляется несколько файлов.
- `BuildAction`: Действие сборки, присваиваемое файлу, требуется только в том случае, если путь к пакету `contentFiles` находится в папке. По умолчанию используется значение "нет".

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
1. Передача данных MSBuild в NuGet. Build. Tasks. dll
1. Запуск восстановления.
1. Скачивание пакетов.
1. Запись файла ресурсов, целевых объектов и свойств.

Целевой объект работает только для проектов, использующих формат PackageReference.  `restore` Он **не** работает для проектов, использующих этот `packages.config` формат; вместо этого используйте [Восстановление NuGet](../reference/cli-reference/cli-ref-restore.md) .

### <a name="restore-properties"></a>Свойства восстановления

Дополнительные параметры восстановления могут поступать из свойств MSBuild в файле проекта. Значения также можно задать из командной строки с помощью параметра `-p:` (см. примеры ниже).

| Свойство. | Описание |
|--------|--------|
| RestoreSources | Разделенный точками с запятой список источников пакетов. |
| RestorePackagesPath | Путь к папке пакетов пользователя. |
| RestoreDisableParallel | Ограничение скачиваний до одного за раз. |
| RestoreConfigFile | Путь к применяемому файлу `Nuget.Config`. |
| RestoreNoCache | Значение true позволяет избежать использования кэшированных пакетов. См. раздел [Управление глобальными пакетами и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| RestoreIgnoreFailedSources | Если значение равно true, нерабочие или отсутствующие источники пакетов игнорируются. |
| ресторефаллбаккфолдерс | Резервные папки используются так же, как и папка User Packages. |
| рестореаддитионалпрожектсаурцес | Дополнительные источники, используемые во время восстановления. |
| рестореаддитионалпрожектфаллбаккфолдерс | Дополнительные резервные папки для использования во время восстановления. |
| рестореаддитионалпрожектфаллбаккфолдерсексклудес | Исключает резервные папки, указанные в`RestoreAdditionalProjectFallbackFolders` |
| RestoreTaskAssemblyFile | Путь к `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Разделенный точками с запятой список проектов для восстановления, который должен содержать абсолютные пути. |
| рестореусескипнонексистенттаржетс  | При сборе проектов с помощью MSBuild определяет, будут ли они собраны с `SkipNonexistentTargets` помощью оптимизации. Если значение не задано, по `true`умолчанию используется значение. Следствием является быстрое поведение при сбое, если целевые объекты проекта не могут быть импортированы. |
| MSBuildProjectExtensionsPath | Папка Output, по умолчанию `BaseIntermediateOutputPath` — `obj` и папка. |

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

| Файл | Описание |
|--------|--------|
| `project.assets.json` | Содержит диаграмму зависимостей всех ссылок на пакеты. |
| `{projectName}.projectFileExtension.nuget.g.props` | Ссылки на свойства MSBuild, содержащиеся в пакетах. |
| `{projectName}.projectFileExtension.nuget.g.targets` | Ссылки на целевые объекты MSBuild, содержащиеся в пакетах. |

### <a name="restoring-and-building-with-one-msbuild-command"></a>Восстановление и сборка с помощью одной команды MSBuild

Из-за того, что NuGet может восстанавливать пакеты, которые выводят цели и свойства MSBuild, оценки восстановления и сборки выполняются с разными глобальными свойствами.
Это означает, что следующие действия будут иметь непредсказуемое и неправильное поведение.

```cli
msbuild -t:restore,build
```

 Вместо этого рекомендуемый подход:

```cli
msbuild -t:build -restore
```

Одна и та же логика применяется к другим `build`целевым объектам, аналогичным.

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
