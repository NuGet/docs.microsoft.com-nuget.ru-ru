---
title: Объекты pack и restore NuGet в качестве целевых объектов MSBuild
description: Объекты pack и restore NuGet могут выступать непосредственно в качестве целевых объектов MSBuild в NuGet 4.0+.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 0c32978baf6146f10c262ba7af94f61fee22272d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777720"
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

Для проектов .NET, использующих `PackageReference` Формат, с помощью команды `msbuild -t:pack` рисует входные данные из файла проекта для использования при создании пакета NuGet.

В следующей таблице описаны свойства MSBuild, которые можно добавить в файл проекта в пределах первого `<PropertyGroup>` узла. Эти изменения легко внести в Visual Studio 2017 и более поздней версии, щелкнув проект правой кнопкой мыши и выбрав пункт **Изменить {project_name}**. Для удобства таблица упорядочивается по эквивалентному свойству в [ `.nuspec` файле](../reference/nuspec.md).

Обратите внимание, что свойства `Owners` и `Summary` из `.nuspec` не поддерживаются в MSBuild.

| Значение атрибута или NuSpec | Свойство MSBuild | По умолчанию | Примечания |
|--------|--------|--------|--------|
| Id | PackageId | AssemblyName | $(AssemblyName) из MSBuild |
| Версия | PackageVersion | Версия | Это значение совместимо с SemVer, например "1.0.0", "1.0.0-beta" или "1.0.0-beta-00345" |
| VersionPrefix | PackageVersionPrefix | пустых | Задав PackageVersion, вы перезапишите PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | пустых | $(VersionSuffix) из MSBuild. Задав PackageVersion, вы перезапишите PackageVersionSuffix |
| Авторы | Авторы | Имя текущего пользователя | Разделенный точками с запятой список авторов пакетов, совпадающих с именами профилей на сайте nuget.org. Они отображаются в коллекции NuGet на сайте nuget.org и используются для перекрестных ссылок на пакеты тех же авторов. |
| Владельцы | Недоступно | Не существует в NuSpec | |
| Заголовок | Заголовок | Идентификатор пакета| Понятный заголовок пакета, обычно используемый при отображении пользовательского интерфейса, как на сайте nuget.org и в диспетчере пакетов Visual Studio. |
| Description | Описание | "Описание пакета" | Подробное описание сборки. Если `PackageDescription` не указывать, это свойство также будет использоваться в качестве описания пакета. |
| Copyright | Copyright | пустых | Сведения об авторских правах для пакета. |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | false | Логическое значение, указывающее, должен ли клиент просить потребителя принять условия лицензии перед установкой пакета. |
| license | PackageLicenseExpression | пустых | Соответствует `<license type="expression">`. См. раздел [Упаковка лицензионного выражения или файла лицензии](#packing-a-license-expression-or-a-license-file). |
| license | PackageLicenseFile | пустых | Путь к файлу лицензии в пакете, если вы используете пользовательскую лицензию или лицензию, которой не назначен идентификатор СПДКС. Необходимо явно упаковать файл лицензии, на который указывает ссылка. Соответствует `<license type="file">`. См. раздел [Упаковка лицензионного выражения или файла лицензии](#packing-a-license-expression-or-a-license-file). |
| LicenseUrl | PackageLicenseUrl | пустых | Параметр `PackageLicenseUrl` использовать не рекомендуется. Вместо него следует использовать элементы `PackageLicenseExpression` или `PackageLicenseFile`. |
| ProjectUrl | PackageProjectUrl | пустых | |
| Значок | PackageIcon | пустых | Путь к образу в пакете, используемому в качестве значка пакета. Необходимо явно упаковать файл изображения значка, на который указывает ссылка. Дополнительные сведения см. в разделе Упаковка изображения и [ `icon` метаданных](/nuget/reference/nuspec#icon) [значка](#packing-an-icon-image-file) . |
| IconUrl | PackageIconUrl | пустых | `PackageIconUrl` является нерекомендуемым в пользу `PackageIcon` . Однако для лучшей работы с предыдущими версиями необходимо указать `PackageIconUrl` в дополнение к `PackageIcon` . |
| Теги | PackageTags | пустых | Разделенный точками с запятой список тегов, обозначающий пакет. |
| ReleaseNotes | PackageReleaseNotes | пустых | Заметки о выпуске для пакета. |
| Репозиторий/URL-адрес | RepositoryUrl | пустых | URL-адрес репозитория, используемый для клонирования или извлечения исходного кода. Пример: *https://github.com/NuGet/NuGet.Client.git* . |
| Репозиторий или тип | RepositoryType | пустых | Тип репозитория. Примеры: `git` (по умолчанию), `tfs` . |
| Репозиторий или ветвь | RepositoryBranch | пустых | Дополнительные сведения о ветви репозитория. Необходимо также указать `RepositoryUrl`, чтобы включить это свойство. Пример: *master* (NuGet 4.7.0 +). |
| Репозиторий/фиксация | RepositoryCommit | пустых | Необязательная фиксация или набор изменений репозитория для указания источника, на основе которого был создан пакет. Необходимо также указать `RepositoryUrl`, чтобы включить это свойство. Пример: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +). |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Сводка | Не поддерживается | | |

### <a name="pack-target-inputs"></a>Входные данные целевого объекта pack

| Свойство | Описание |
| - | - |
| IsPackable | Логическое значение, которое указывает, можно ли упаковать проект. Значение по умолчанию — `true`. |
| суппрессдепенденЦиесвхенпаккинг | Установите значение `true` , чтобы подавить зависимости пакета от созданного пакета NuGet. |
| PackageVersion | Указывает версию, которую будет иметь итоговый пакет. Принимает все формы строки версии NuGet. По умолчанию используется значение `$(Version)`, то есть значение свойства `Version` в проекте. |
| PackageId | Указывает имя для итогового пакета. Если значение не указано, операция `pack` по умолчанию использует в качестве имени пакета `AssemblyName` или имя каталога. |
| PackageDescription | Подробное описание пакета для отображения пользовательского интерфейса. |
| Authors | Разделенный точками с запятой список авторов пакетов, совпадающих с именами профилей на сайте nuget.org. Они отображаются в коллекции NuGet на сайте nuget.org и используются для перекрестных ссылок на пакеты тех же авторов. |
| Описание | Подробное описание сборки. Если `PackageDescription` не указывать, это свойство также будет использоваться в качестве описания пакета. |
| Copyright | Сведения об авторских правах для пакета. |
| PackageRequireLicenseAcceptance | Логическое значение, указывающее, должен ли клиент просить потребителя принять условия лицензии перед установкой пакета. Значение по умолчанию — `false`. |
| DevelopmentDependency | Логическое значение, указывающее на то, помечен ли пакет как зависимость только для разработки, что позволяет запретить его включение в качестве зависимости в другие пакеты. В `PackageReference` (NuGet 4.8 +) этот флаг также означает, что ресурсы времени компиляции исключаются из компиляции. Дополнительные сведения см. в статье [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) (Поддержка DevelopmentDependency для PackageReference). |
| PackageLicenseExpression | Идентификатор или выражение [лицензии спдкс](https://spdx.org/licenses/) , например `Apache-2.0` . Дополнительные сведения см. в разделе Упаковка а. Лицензионное [выражение или файл лицензии](#packing-a-license-expression-or-a-license-file). |
| PackageLicenseFile | Путь к файлу лицензии в пакете, если вы используете пользовательскую лицензию или лицензию, которой не назначен идентификатор СПДКС. |
| PackageLicenseUrl | Параметр `PackageLicenseUrl` использовать не рекомендуется. Вместо него следует использовать элементы `PackageLicenseExpression` или `PackageLicenseFile`. |
| PackageProjectUrl | |
| PackageIcon | Указывает путь к значку пакета относительно корня пакета. Дополнительные сведения см. в разделе [Упаковка файла изображения значка](#packing-an-icon-image-file). |
| PackageReleaseNotes| Заметки о выпуске для пакета. |
| PackageTags | Разделенный точками с запятой список тегов, обозначающий пакет. |
| PackageOutputPath | Определяет выходной путь для размещения упакованного пакета. Значение по умолчанию — `$(OutputPath)`. |
| IncludeSymbols | Это логическое значение указывает, должен ли пакет создавать дополнительный пакет символов при упаковке проекта. Форматом пакета символов управляет свойство `SymbolPackageFormat`. Дополнительные сведения см. в разделе [инклудесимболс](#includesymbols). |
| IncludeSource | Это логическое значение указывает, должен ли процесс упаковки создавать исходный пакет. Исходный пакет содержит библиотеку исходного кода, а также файлы PDB. Исходные файлы помещаются в каталог `src/ProjectName` итогового файла пакета. Дополнительные сведения см. в разделе [инклудесаурце](#includesource). |
| PackageTypes
| IsTool | Указывает, копируются ли все выходные файлы в папку *tools* вместо папки *lib*. Дополнительные сведения см. в разделе [Tool](#istool). |
| RepositoryUrl | URL-адрес репозитория, используемый для клонирования или извлечения исходного кода. Пример: *https://github.com/NuGet/NuGet.Client.git* . |
| RepositoryType | Тип репозитория. Примеры: `git` (по умолчанию), `tfs` . |
| RepositoryBranch | Дополнительные сведения о ветви репозитория. Необходимо также указать `RepositoryUrl`, чтобы включить это свойство. Пример: *master* (NuGet 4.7.0 +). |
| RepositoryCommit | Необязательная фиксация или набор изменений репозитория для указания источника, на основе которого был создан пакет. Необходимо также указать `RepositoryUrl`, чтобы включить это свойство. Пример: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +). |
| SymbolPackageFormat | Задает формат пакета символов. Если "Symbols. nupkg", пакет устаревших символов создается с расширением *. Symbols. nupkg* , содержащим PDB, DLL и другие выходные файлы. Если "снупкг", создается пакет символов снупкг, содержащий переносимые PDB-файлы. Значение по умолчанию — Symbols. nupkg. |
| NoPackageAnalysis | Указывает, что `pack` не следует выполнять анализ пакетов после сборки пакета. |
| MinClientVersion | Указывает минимальную версию клиента NuGet, который может установить этот пакет с использованием nuget.exe и диспетчера пакетов Visual Studio. |
| IncludeBuildOutput | Это логическое значение указывает, следует ли упаковывать выходные сборки в файл *NUPKG*. |
| IncludeContentInPack | Это логическое значение указывает, будут ли все элементы, имеющие тип, `Content` включаться в итоговый пакет автоматически. Значение по умолчанию — `true`. |
| BuildOutputTargetFolder | Указывает папку для размещения выходных сборок. Выходные сборки (и другие выходные файлы) копируются в соответствующие папки платформы. Дополнительные сведения см. в разделе [выходные сборки](#output-assemblies). |
| ContentTargetFolders | Указывает расположение по умолчанию, по которому должны указываться все файлы содержимого, если `PackagePath` для них не задано значение. Значение по умолчанию — "content;contentFiles". Дополнительные сведения см. в статье [Включение содержимого в пакет](#including-content-in-a-package). |
| NuspecFile | Относительный или абсолютный путь к файлу *NUSPEC*, используемому для упаковки. Если он указан, он используется **исключительно** для сведений о упаковке, а любые сведения в проектах не используются. Дополнительные сведения см. [в разделе Упаковка с помощью. nuspec](#packing-using-a-nuspec). |
| NuspecBasePath | Базовый путь для файла *NUSPEC*. Дополнительные сведения см. [в разделе Упаковка с помощью. nuspec](#packing-using-a-nuspec). |
| NuspecProperties | Список разделенных точками с запятой пар "ключ-значение". Дополнительные сведения см. [в разделе Упаковка с помощью. nuspec](#packing-using-a-nuspec). |

## <a name="pack-scenarios"></a>Сценарии использования pack

### <a name="suppress-dependencies"></a>Подавлять зависимости

Чтобы исключить зависимости пакета из созданного пакета NuGet, задайте для значение, `SuppressDependenciesWhenPacking` `true` которое позволит пропустить все зависимости из созданного файла nupkg.

### <a name="packageiconurl"></a>PackageIconUrl

`PackageIconUrl` является нерекомендуемым в пользу [`PackageIcon`](#packageicon) Свойства. Начиная с NuGet 5,3 и Visual Studio 2019 версии 16,3, `pack` создает предупреждение [NU5048](./errors-and-warnings/nu5048.md) , если только метаданные пакета указывают только `PackageIconUrl` .

### <a name="packageicon"></a>PackageIcon

> [!Tip]
> Чтобы обеспечить обратную совместимость с клиентами и источниками, которые еще не поддерживаются `PackageIcon` , укажите `PackageIcon` и `PackageIconUrl` . Visual Studio поддерживает `PackageIcon` пакеты, поступающие из источника, основанного на папках.

#### <a name="packing-an-icon-image-file"></a>Упаковка файла изображения значка

При упаковке файла изображения значка используйте `PackageIcon` свойство, чтобы указать путь к файлу значка относительно корня пакета. Кроме того, убедитесь, что файл включен в пакет. Размер файла изображения ограничен 1 МБ. Поддерживаются следующие форматы файлов: JPEG и PNG. Рекомендуется разрешение изображения 128x128.

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

При использовании выражения лицензии используйте `PackageLicenseExpression` свойство. Пример см. в разделе [пример выражения лицензии](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

Дополнительные сведения о лицензионных выражениях и лицензиях, принимаемых NuGet.org, см. в разделе [метаданные лицензии](nuspec.md#license).

При упаковке файла лицензии используйте свойство, `PackageLicenseFile` чтобы указать путь к пакету относительно корня пакета. Кроме того, убедитесь, что файл включен в пакет. Пример:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

Пример см. в разделе [Пример файла лицензии](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).

> [!NOTE]
> `PackageLicenseExpression`Одновременно можно указать только один из, `PackageLicenseFile` и `PackageLicenseUrl` .

### <a name="packing-a-file-without-an-extension"></a>Упаковка файла без расширения

В некоторых сценариях, например при упаковке файла лицензии, может потребоваться включить файл без расширения.
По историческим причинам NuGet & MSBuild обрабатывает пути без расширения в качестве каталогов.

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

[Файл без примера расширения](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).
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
`MSBuild 16.5+` также имеет [поддержку согласия](#restoring-packagereference-and-packagesconfig-with-msbuild) для `packages.config` формата.

> [!NOTE]
> `restore`Целевой объект [не должен выполняться](#restoring-and-building-with-one-msbuild-command) в сочетании с целевым объектом `build` .

### <a name="restore-properties"></a>Свойства восстановления

Дополнительные параметры восстановления могут поступать из свойств MSBuild в файле проекта. Значения также можно задать из командной строки с помощью параметра `-p:` (см. примеры ниже).

| Свойство | Описание |
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
| ресторепаккажесконфиг | Параметр согласия, который восстанавливает проекты с packages.config. Поддерживается `MSBuild -t:restore` только с. |
| рестореусестатикграфевалуатион | Переключение на использование статического графа MSBuild вместо стандартного вычисления. Статическая Оценка графа — это экспериментальная функция, которая значительно ускоряется для больших репозиториев и решений. |

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

### <a name="restoring-with-msbuild-static-graph-evaluation"></a>Восстановление со статической оценкой графа MSBuild

> [!NOTE]
> С помощью MSBuild 16.6 + NuGet добавил экспериментальную функцию для использования статической оценки графа из командной строки, значительно повышающей время восстановления для больших репозиториев.

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

Кроме того, его можно включить, задав свойство в каталоге. Build. props.

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> Начиная с Visual Studio 2019. x и NuGet 5. x, эта функция считается экспериментальной и явной. Дополнительные сведения о том, когда эта функция будет включена по умолчанию, см. в [под9803е NuGet/Home #](https://github.com/NuGet/Home/issues/9803) .

При восстановлении статического графа изменяется часть MSBuild, вычисление и чтение проекта, но не алгоритм восстановления. Алгоритм восстановления одинаков во всех инструментах NuGet (NuGet.exe, MSBuild.exe, dotnet.exe и Visual Studio).

В очень редких случаях восстановление статических графов может отличаться от текущего при восстановлении, а некоторые объявленные PackageReferences или ссылками могут отсутствовать.

Для упрощения проверки при переходе к статическому восстановлению графа можно выполнить следующие действия.

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

NuGet *не* должен сообщать об изменениях. Если вы видите несоответствие, напишите вопрос в [NuGet/Home](https://github.com/nuget/home/issues/new).

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
