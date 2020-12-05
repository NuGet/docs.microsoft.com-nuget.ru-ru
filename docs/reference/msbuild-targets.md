---
title: Объекты pack и restore NuGet в качестве целевых объектов MSBuild
description: Объекты pack и restore NuGet могут выступать непосредственно в качестве целевых объектов MSBuild в NuGet 4.0+.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 4a04c6dd7993fc47bcf7a6fe46236ed700a0d105
ms.sourcegitcommit: e39e5a5ddf68bf41e816617e7f0339308523bbb3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2020
ms.locfileid: "96738933"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>Объекты pack и restore NuGet в качестве целевых объектов MSBuild

*NuGet 4.0+*

В формате [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + может хранить все метаданные манифеста непосредственно в файле проекта вместо использования отдельного `.nuspec` файла.

При использовании MSBuild 15.1+ NuGet также является привилегированным компонентом MSBuild с целевыми объектами `pack` и `restore`, как описано ниже. Эти целевые объекты позволяют работать с NuGet, как с любой другой задачей или другим целевым объектом MSBuild. Инструкции по созданию пакета NuGet с помощью MSBuild см. в статье [Создание пакета NuGet с помощью MSBuild](../create-packages/creating-a-package-msbuild.md). (Для NuGet 3.x и более ранних версий можно использовать команды [pack](../reference/cli-reference/cli-ref-pack.md) и [restore](../reference/cli-reference/cli-ref-restore.md) в NuGet CLI.)

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

> [!NOTE]
> `$(OutputPath)` является относительным и предполагает, что команда выполняется из корневого каталога проекта.

## <a name="pack-target"></a>Целевой объект pack

Для .NET Standard проектов, использующих формат PackageReference, команда `msbuild -t:pack` рисует входные данные из файла проекта для использования при создании пакета NuGet.

В следующей таблице описываются свойства MSBuild, которые можно добавить в файл проекта в первом узле `<PropertyGroup>`. Эти изменения легко внести в Visual Studio 2017 и более поздней версии, щелкнув проект правой кнопкой мыши и выбрав пункт **Изменить {project_name}**. Для удобства таблица упорядочивается по эквивалентному свойству в [ `.nuspec` файле](../reference/nuspec.md).

Обратите внимание, что свойства `Owners` и `Summary` из `.nuspec` не поддерживаются в MSBuild.

| Значение атрибута или NuSpec | Свойство MSBuild | По умолчанию | Примечания |
|--------|--------|--------|--------|
| Id | PackageId | AssemblyName | $(AssemblyName) из MSBuild |
| Версия | PackageVersion | Версия | Это значение совместимо с SemVer, например "1.0.0", "1.0.0-beta" или "1.0.0-beta-00345" |
| VersionPrefix | PackageVersionPrefix | пустых | Задав PackageVersion, вы перезапишите PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | пустых | $(VersionSuffix) из MSBuild. Задав PackageVersion, вы перезапишите PackageVersionSuffix |
| Авторы | Авторы | Имя текущего пользователя | |
| Владельцы | Н/Д | Не существует в NuSpec | |
| Заголовок | Заголовок | Идентификатор пакета| |
| Description | Описание | "Описание пакета" | |
| Copyright | Copyright | пустых | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | false | |
| license | PackageLicenseExpression | пустых | Соответствует `<license type="expression">` |
| license | PackageLicenseFile | пустых | Соответствует `<license type="file">`. Необходимо явно упаковать файл лицензии, на который указывает ссылка. |
| LicenseUrl | PackageLicenseUrl | пустых | `PackageLicenseUrl` является устаревшим, используйте свойство Паккажелиценсикспрессион или Паккажелиценсефиле. |
| ProjectUrl | PackageProjectUrl | пустых | |
| Значок | PackageIcon | пустых | Необходимо явно упаковать файл изображения значка, на который указывает ссылка.|
| IconUrl | PackageIconUrl | пустых | Для лучшей работы с предыдущими версиями `PackageIconUrl` следует указать в дополнение к `PackageIcon` . Более длительное выражение `PackageIconUrl` будет считаться устаревшим. |
| Теги | PackageTags | пустых | Теги разделяются точкой с запятой. |
| ReleaseNotes | PackageReleaseNotes | пустых | |
| Репозиторий/URL-адрес | RepositoryUrl | пустых | URL-адрес репозитория, используемый для клонирования или извлечения исходного кода. Например *https://github.com/NuGet/NuGet.Client.git* |
| Репозиторий или тип | RepositoryType | пустых | Тип репозитория. Примеры: *Git*, *TFS*. |
| Репозиторий или ветвь | RepositoryBranch | пустых | Дополнительные сведения о ветви репозитория. Для включения этого свойства также необходимо указать *репоситорюрл* . Пример: *master* (NuGet 4.7.0 +) |
| Репозиторий/фиксация | RepositoryCommit | пустых | Необязательная фиксация или набор изменений репозитория для указания источника, на основе которого был создан пакет. Для включения этого свойства также необходимо указать *репоситорюрл* . Пример: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Сводка | Не поддерживается | | |

### <a name="pack-target-inputs"></a>Входные данные целевого объекта pack

- IsPackable
- суппрессдепенденЦиесвхенпаккинг
- PackageVersion
- PackageId
- Авторы
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

### <a name="suppress-dependencies"></a>Подавлять зависимости

Чтобы исключить зависимости пакета из созданного пакета NuGet, задайте для значение, `SuppressDependenciesWhenPacking` `true` которое позволит пропустить все зависимости из созданного файла nupkg.

### <a name="packageiconurl"></a>PackageIconUrl

`PackageIconUrl` будет считаться устаревшим в пользу нового [`PackageIcon`](#packageicon) Свойства.

Начиная с NuGet 5,3 & Visual Studio 2019 версии 16,3, `pack` вызовет предупреждение [NU5048](./errors-and-warnings/nu5048.md) , если только метаданные пакета указывают только `PackageIconUrl` .

### <a name="packageicon"></a>PackageIcon

> [!Tip]
> `PackageIcon` `PackageIconUrl` Для обеспечения обратной совместимости с клиентами и источниками, которые еще не поддерживаются, необходимо указать и, и `PackageIcon` . Visual Studio будет поддерживать `PackageIcon` пакеты, поступающие из источника на основе папок в будущем выпуске.

#### <a name="packing-an-icon-image-file"></a>Упаковка файла изображения значка

При упаковке файла изображения значка необходимо использовать `PackageIcon` свойство, чтобы указать путь к пакету относительно корня пакета. Кроме того, необходимо убедиться, что файл включен в пакет. Размер файла изображения ограничен 1 МБ. Поддерживаются следующие форматы файлов: JPEG и PNG. Рекомендуется разрешение изображения 128x128.

Пример:

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

[Пример значка пакета](https://github.com/NuGet/Samples/tree/master/PackageIconExample).

Чтобы получить nuspec эквивалент, просмотрите [ссылку на nuspec для значка](nuspec.md#icon).

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

### <a name="packing-a-license-expression-or-a-license-file"></a>Упаковка выражения лицензии или файла лицензии

При использовании выражения лицензии следует использовать свойство Паккажелиценсикспрессион. 
[Пример выражения лицензии](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

Дополнительные [сведения о лицензионных выражениях и лицензиях, принимаемых NuGet.org](nuspec.md#license).

При упаковке файла лицензии необходимо использовать свойство Паккажелиценсефиле, чтобы указать путь к пакету относительно корня пакета. Кроме того, необходимо убедиться, что файл включен в пакет. Пример:

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

Хотя рекомендуется включить в файл проекта [все свойства](../reference/msbuild-targets.md#pack-target) , которые обычно находятся в файле `.nuspec` , можно использовать `.nuspec` файл для упаковки проекта. Для проекта в стиле, отличном от SDK, который использует `PackageReference` , необходимо импортировать, `NuGet.Build.Tasks.Pack.targets` чтобы можно было выполнить задачу «Pack». Вам по-прежнему потребуется восстановить проект, чтобы можно было упаковать файл nuspec. (Проект в стиле SDK включает целевые объекты Pack по умолчанию.)

Целевая платформа файла проекта несущественна и не используется при упаковке nuspec. Следующие три свойства MSBuild связаны с упаковкой с помощью `.nuspec`:

1. `NuspecFile`: относительный или абсолютный путь к файлу `.nuspec`, используемому для упаковки.
1. `NuspecProperties`: список разделенных точками с запятой пар "ключ-значение". Из-за особенностей работы анализа в командной строке MSBuild несколько свойств нужно указать следующим образом: `-p:NuspecProperties="key1=value1;key2=value2"`.  
1. `NuspecBasePath`: базовый путь для файла `.nuspec`.

Если вы используете `dotnet.exe` для упаковки проекта, воспользуйтесь командой, аналогичной следующей:

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Если вы используете MSBuild для упаковки проекта, воспользуйтесь командой, аналогичной следующей:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Обратите внимание, что упаковка a nuspec с помощью dotnet.exe или MSBuild также ведет к построению проекта по умолчанию. Это можно избежать, передав ```--no-build``` свойство в dotnet.exe, которое является аналогом параметра ```<NoBuild>true</NoBuild> ``` в файле проекта, а также параметром ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` в файле проекта.

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

### <a name="advanced-extension-points-to-create-customized-package"></a>Улучшенные точки расширения для создания настраиваемого пакета

`pack`Целевой объект предоставляет две точки расширения, которые выполняются во внутренней и целевой сборке конкретной платформы. Поддержка точек расширения включает в пакет содержимое и сборки, относящиеся к целевой платформе.

- `TargetsForTfmSpecificBuildOutput` target: используйте для файлов в `lib` папке или в папке, указанной с помощью `BuildOutputTargetFolder` .
- `TargetsForTfmSpecificContentInPackage` target: используйте для файлов за пределами `BuildOutputTargetFolder` .

#### <a name="targetsfortfmspecificbuildoutput"></a>таржетсфортфмспеЦификбуилдаутпут

Напишите настраиваемый целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificBuildOutput)` Свойства. Для файлов, которые необходимо переключать в `BuildOutputTargetFolder` (LIB по умолчанию), целевой объект должен записать эти файлы в ItemGroup `BuildOutputInPackage` и задать следующие два значения метаданных:

- `FinalOutputPath`: Абсолютный путь к файлу; Если этот параметр не указан, для вычисления исходного пути используется удостоверение.
- `TargetPath`: (Необязательно) задайте, когда файл необходимо переключиться во вложенную папку в `lib\<TargetFramework>` , например вспомогательные сборки, которые находятся в соответствующих папках языка и региональных параметров. По умолчанию используется имя файла.

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

Напишите настраиваемый целевой объект и укажите его в качестве значения `$(TargetsForTfmSpecificContentInPackage)` Свойства. Для всех файлов, включаемых в пакет, целевой объект должен записать эти файлы в ItemGroup `TfmSpecificPackageFile` и задать следующие необязательные метаданные:

- `PackagePath`: Путь, по которому файл должен быть выведен в пакете. NuGet выдает предупреждение, если в один и тот же путь к пакету добавляется несколько файлов.
- `BuildAction`: Действие сборки, присваиваемое файлу, требуется только в том случае, если путь к пакету находится в `contentFiles` папке. По умолчанию используется значение "нет".

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
1. Передача данных MSBuild в NuGet.Build.Tasks.dll
1. Запуск восстановления.
1. Скачивание пакетов
1. Запись файла ресурсов, целевых объектов и свойств.

`restore`Целевой объект работает для проектов, использующих формат PackageReference.
`MSBuild 16.5+` также имеет [поддержку согласия](#restoring-packagereference-and-packages.config-with-msbuild) для `packages.config` формата.

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
| рестореаддитионалпрожектфаллбаккфолдерсексклудес | Исключает резервные папки, указанные в `RestoreAdditionalProjectFallbackFolders` |
| RestoreTaskAssemblyFile | Путь к `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Разделенный точками с запятой список проектов для восстановления, который должен содержать абсолютные пути. |
| рестореусескипнонексистенттаржетс  | При сборе проектов с помощью MSBuild определяет, будут ли они собраны с помощью `SkipNonexistentTargets` оптимизации. Если значение не задано, по умолчанию используется значение `true` . Следствием является быстрое поведение при сбое, если целевые объекты проекта не могут быть импортированы. |
| MSBuildProjectExtensionsPath | Папка Output, по умолчанию — `BaseIntermediateOutputPath` и `obj` Папка. |
| ресторефорце | В проектах на основе PackageReference принудительно разрешаются все зависимости, даже если последнее восстановление прошло успешно. Установка этого флага аналогична удалению `project.assets.json` файла. Это не позволяет обходить HTTP-кэш. |
| RestorePackagesWithLockFile | Разрешение использовать файл блокировки. |
| RestoreLockedMode | Запустите восстановление в заблокированном режиме. Это означает, что восстановление не будет переоценивать зависимости. |
| NuGetLockFilePath | Пользовательское расположение файла блокировки. Расположение по умолчанию находится рядом с проектом и имеет имя `packages.lock.json` . |
| RestoreForceEvaluate | Принудительное восстановление для повторного расчета зависимостей и обновление файла блокировки без предупреждения. |
| ресторепаккажесконфиг | Переключатель opt, который восстанавливает проекты с packages.config. Поддерживается `MSBuild -t:restore` только с. |

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

Одна и та же логика применяется к другим целевым объектам, аналогичным `build` .

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a>Восстановление PackageReference и packages.config с помощью MSBuild

С помощью MSBuild 16.5 + packages.config также поддерживаются для `msbuild -t:restore` .

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> `packages.config` Restore доступен только в `MSBuild 16.5+` , а не в `dotnet.exe`

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
