---
title: Ссылку на файл .nuspec для NuGet
description: Файл с расширением .nuspec содержит метаданные пакета, которые используются при построении пакета и предоставляют дополнительную информацию для его потребителей.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: c11b50aa1637c00f0f0e71a6e20ce5d435db402b
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2018
---
# <a name="nuspec-reference"></a>Справочник по файлу NUSPEC

Файл `.nuspec` представляет собой манифест в формате XML и содержит метаданные пакета. Этот манифест используется при построении пакета и содержит дополнительные сведения для его потребителей. Манифест всегда включается в пакет.

В этом разделе.

- [Общая форма и схема](#general-form-and-schema)
- [Замена маркеров](#replacement-tokens) (при использовании с проектом Visual Studio)
- [Зависимости](#dependencies)
- [Явные ссылки на сборку](#explicit-assembly-references)
- [Ссылки на сборку платформы](#framework-assembly-references)
- [Включение файлов сборки](#including-assembly-files)
- [Включение файлов содержимого](#including-content-files)
- [Примеры](#examples)

## <a name="general-form-and-schema"></a>Общая форма и схема

Текущий файл схемы `nuspec.xsd` представлен в [репозитории GitHub для NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).

В рамках этой схемы файл `.nuspec` имеет следующую общую форму:

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

Чтобы получить наглядное представление схемы, откройте файл в режиме конструктора Visual Studio и щелкните ссылку **Обозреватель схемы XML**. Также можно открыть этот файл в виде кода. Для этого щелкните правой кнопкой мыши в редакторе и выберите команду **Показать в обозревателе схемы XML**. В любом случае при развертывании большинства узлов схема будет иметь примерно следующий вид:

![Обозреватель схемы Visual Studio с открытым файлом nuspec.xsd](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a>Атрибуты метаданных

Элемент `<metadata>` поддерживает атрибуты, описываемые в следующей таблице.

| Атрибут | Обязательно | Описание |
| --- | --- | --- | 
| **minClientVersion** | Нет | Указывает минимальную версию клиента NuGet, который может установить этот пакет с использованием nuget.exe и диспетчера пакетов Visual Studio. Используется во всех случаях, когда пакет зависит от конкретных функций в файле `.nuspec`, которые были добавлены в определенной версии клиента NuGet. Например, для пакета, использующего атрибут `developmentDependency`, атрибуту `minClientVersion` необходимо присвоить значение "2.8". Аналогичным образом, для пакета, использующего элемент `contentFiles` (см. следующий раздел), атрибуту `minClientVersion` необходимо присвоить значение "3.3". Также обратите внимание, что клиенты NuGet версий, предшествующих 2.5, не распознают этот флаг и поэтому *всегда* отклоняют установку пакета независимо от значения атрибута `minClientVersion`. |

### <a name="required-metadata-elements"></a>Обязательные элементы метаданных

Следующие элементы являются минимальным требованием для пакета, однако, несмотря на это, рекомендуется добавить [дополнительные элементы метаданных](#optional-metadata-elements), чтобы оптимизировать работу с вашим пакетом для разработчиков.

Эти элементы должны использоваться внутри элемента `<metadata>`.

| Элемент | Описание |
| --- | --- |
| **id** | Идентификатор пакета без учета регистра, который должен быть уникальным в пределах сайта nuget.org или иной коллекции, в которой находится пакет. Идентификаторы не должны содержать пробелов или символов, которые недопустимы в URL-адресах, и в них должны соблюдаться общие правила касательно пространств имен .NET. Инструкции см. в разделе [Выбор уникального идентификатора пакета](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). |
| **version** | Версия пакета, указываемая согласно шаблону *основной_номер.дополнительный_номер.исправление*. Номер версии может включать в себя суффикс предварительной версии, как описано в разделе [Управление версиями пакета](../reference/package-versioning.md#pre-release-versions). |
| **description** | Подробное описание пакета для отображения пользовательского интерфейса. |
| **authors** | Разделенный запятыми список авторов пакетов, совпадающих с именами профилей на сайте nuget.org. Они отображаются в коллекции NuGet на сайте nuget.org и используются для перекрестных ссылок на пакеты тех же авторов. |

### <a name="optional-metadata-elements"></a>Необязательные элементы метаданных

Эти элементы могут использоваться внутри элемента `<metadata>`.

#### <a name="single-elements"></a>Одиночные элементы

| Элемент | Описание |
| --- | --- |
| **title** | Понятный заголовок пакета, обычно используемый при отображении пользовательского интерфейса, как на сайте nuget.org и в диспетчере пакетов Visual Studio. Если значение не указано, используется идентификатор пакета. |
| **owners** | Разделенный запятыми список создателей пакета, совпадающих с именами профилей на сайте nuget.org. Часто совпадает со списком в элементе `authors` и игнорируется при загрузке пакета на веб-сайт nuget.org. См. раздел [Управление владельцами пакетов на веб-сайте nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg). |
| **projectUrl** | URL-адрес для домашней страницы пакета, часто указываемый при отображении пользовательского интерфейса, также как и nuget.org. |
| **licenseUrl** | URL-адрес для лицензии пакета, часто указываемый при отображении пользовательского интерфейса, так же как и nuget.org. |
| **iconUrl** | URL-адрес для изображения размером 64x64 с прозрачным фоном, используемого в качестве значка для пакета при отображении пользовательского интерфейса. Убедитесь, что этот элемент содержит *прямой URL-адрес изображения*, а не URL-адрес веб-страницы, на которой содержится изображение. Например, чтобы использовать изображение из GitHub, использовать Необработанный файл, URL-адрес, например  <em>https://github.com/ \<username\>/\<репозитория\>/raw/\<ветви\> / \<logo.png\></em>. |
| **requireLicenseAcceptance** | Логическое значение, указывающее, должен ли клиент просить потребителя принять условия лицензии перед установкой пакета. |
| **developmentDependency** | *(Версия 2.8 и более поздние)* Логическое значение, указывающее, помечен ли пакет как зависимость только для разработки, что позволяет запретить его включение в качестве зависимости в другие пакеты. |
| **summary** | Краткое описание пакета для отображения пользовательского интерфейса. Если этот элемент опущен, используется сокращенная версия элемента `description`. |
| **releaseNotes** | *(Версия 1.5 и более поздние)* Описание изменений, внесенных в этом выпуске пакета NuGet; часто используется в пользовательском интерфейсе как вкладка **Обновления** диспетчера пакетов Visual Studio вместо описания пакета. |
| **copyright** | *(Версия 1.5 и более поздние)* Сведения об авторских правах для пакета. |
| **language** | Идентификатор языкового стандарта для пакета. См. раздел [Создание локализованных пакетов](../create-packages/creating-localized-packages.md). |
| **tags**  | Список разделенных пробелами тегов и ключевых слов, описывающих пакет NuGet и помогающих находить пакеты NuGet с помощью функций поиска и фильтрации. |
| **serviceable** | *(Версия 3.3 и более поздние)* Только для внутреннего использования в NuGet. |

#### <a name="collection-elements"></a>Элементы коллекции

| Элемент | Описание |
| --- | --- |
**packageTypes** | *(Версия 3.5 и более поздние)* Пустая коллекция или без нескольких элементов `<packageType>`, определяющих тип пакета, если он отличается от обычного пакета зависимостей. Каждый элемент packageType имеет атрибуты *name* и *version*. См. раздел [Указание типа пакета](../create-packages/creating-a-package.md#setting-a-package-type). |
| **dependencies** | Коллекция из нуля или более элементов `<dependency>`, задающих зависимости для пакета. Каждый элемент dependency имеет атрибуты *id*, *version*, *include* (версия 3.x и более поздние) и *exclude* (версия 3.x и более поздние). См. раздел [Зависимости](#dependencies) далее. |
| **frameworkAssemblies** | *(Версия 1.2 и более поздние)* Коллекция из одного или более элементов `<frameworkAssembly>`, идентифицирующих ссылки на сборки .NET Framework, необходимые для этого пакета, что гарантирует добавление ссылок в проекты, использующие пакет. Каждый элемент frameworkAssembly имеет атрибуты *assemblyName* и *targetFramework*. См. раздел [Указание ссылок на сборки платформы в глобальном кэше сборок ](#specifying-framework-assembly-references-gac) ниже. |
| **references** | *(Версия 1.5 и более поздние)* Коллекция из нуля или более элементов `<reference>`, задающие имена сборок в папке `lib` пакета, которые добавляются в качестве ссылок проекта. Каждый элемент reference имеет атрибут *file*. Коллекция `<references>` также может содержать элемент `<group>` с атрибутом *targetFramework*, который, в свою очередь, содержит элементы `<reference>`. Если этот элемент опущен, включаются все ссылки в папке `lib`. См. раздел [Указание явных ссылок на сборки](#specifying-explicit-assembly-references) ниже. |
| **contentFiles** | *(Версия 3.3 и более поздние)* Коллекция элементов `<files>`, которые идентифицируют файлы содержимого, включаемые в потребляющий проект. Эти файлы задаются с набором атрибутов, который описывает их использование в системе проекта. См. раздел [Указание включаемых в пакет файлов](#specifying-files-to-include-in-the-package) ниже. |

### <a name="files-element"></a>Files - элемент

Узел `<package>` может содержать узел `<files>`, который является одноуровневым для узла `<metadata>`, или дочерний узел `<contentFiles>` в узле `<metadata>`, который задает файлы сборки и содержимого, включаемые в пакет. Дополнительные сведения см. далее в разделах [Включение файлов сборки](#including-assembly-files) и [Включение файлов содержимого](#including-content-files) этой статьи.

## <a name="replacement-tokens"></a>Замена маркеров

При создании пакета [команда `nuget pack`](../tools/cli-ref-pack.md) заменяет маркеры с разделителями $ в узле `<metadata>` файла `.nuspec` значениями из файла проекта или параметра `-properties` команды `pack`.

Маркеры задаются в командной строке следующим образом: `nuget pack -properties <name>=<value>;<name>=<value>`. Например, вы можете использовать маркер, такой как `$owners$` и `$desc$`, в файле `.nuspec` и предоставить значения во время упаковки следующим образом:

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

Чтобы использовать значения из проекта, укажите маркеры, описываемые в следующей таблице (AssemblyInfo ссылается на файл в `Properties`, например `AssemblyInfo.cs` или `AssemblyInfo.vb`).

Чтобы использовать эти маркеры, выполните команду `nuget pack` с файлом проекта, а не просто с файлом `.nuspec`. Например, при использовании следующей команды маркеры `$id$` и `$version$` в файле `.nuspec` заменяются значениями проекта `AssemblyName` и `AssemblyVersion`:

```ps
nuget pack MyProject.csproj
```

Как правило, при наличии проекта вы изначально создаете файл `.nuspec` с использованием команды `nuget spec MyProject.csproj`, которая автоматически включает некоторые из этих стандартных маркеров. Тем не менее, если в проекте отсутствуют значения для обязательных элементов `.nuspec`, команда `nuget pack` завершается сбоем. Кроме того, при изменении значений проекта необходимо выполнить перестроение до создания пакета. Это можно легко сделать с помощью параметра `build` команды pack.

За исключением элемента `$configuration$`, значения в проекте используются в приоритетном порядке относительно любых значений, назначенных тому же маркеру в командной строке.

| Токен | Источник значения | Значение
| --- | --- | ---
| **$id$** | Файл проекта | Имя сборки (название) из файла проекта |
| **$version$** | AssemblyInfo | AssemblyInformationalVersion, если присутствует, в противном случае AssemblyVersion |
| **$author$** | AssemblyInfo | AssemblyCompany |
| **$title$** | AssemblyInfo | AssemblyTitle |
| **$description$** | AssemblyInfo | AssemblyDescription |
| **$copyright$** | AssemblyInfo | AssemblyCopyright |
| **$configuration$** | DLL-файл сборки | Конфигурация, используемая для построения сборки, по умолчанию используется тип отладки. Обратите внимание, что для создания пакета с помощью конфигурации выпуска в командной строке всегда используется параметр `-properties Configuration=Release`. |

Маркеры также можно использовать для разрешения путей при включении [файлов сборок](#including-assembly-files) и [файлов содержимого](#including-content-files). Маркеры имеют те же имена, что и свойства MSBuild, что позволяет выбирать файлы для включения в зависимости в текущей конфигурации построения. Например, если вы используете следующие маркеры в файле `.nuspec`:

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

И выполняете построение сборки, для которой `AssemblyName` имеет значение `LoggingLibrary` с конфигурацией `Release` в MSBuild, в файле `.nuspec` в пакете будут присутствовать следующие строки:

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a>Зависимости

Элемент `<dependencies>` внутри элемента `<metadata>` содержит любое число элементов `<dependency>`, идентифицирующих другие пакеты, от которых зависит пакет верхнего уровня. Ниже перечислены атрибуты каждого элемента `<dependency>`:

| Атрибут | Описание |
| --- | --- |
| `id` | Идентификатор пакета зависимости, например EntityFramework и NUnit, являющийся именем пакета nuget.org, показан на странице пакета (обязательно). |
| `version` | Диапазон версий, которые допустимы в качестве зависимости (обязательно). Точный синтаксис см. в разделе [Управление версиями пакета](../reference/package-versioning.md#version-ranges-and-wildcards). |
| include | Разделенный запятыми список тегов включения или исключения (см. ниже), определяющий зависимости, включаемые в конечный пакет. Значение по умолчанию — `none`. |
| exclude | Разделенный запятыми список тегов включения или исключения (см. ниже), определяющий зависимости, исключаемые из конечного пакета. Значение по умолчанию — `all`. Теги в свойстве `exclude` имеют приоритет перед тегами в свойстве `include`. Например, `include="runtime, compile" exclude="compile"` равносильно `include="runtime"`. |

| Тег включения или исключения | Затрагиваемые папки пакета |
| --- | --- |
| contentFiles | Content |
| исполняющая среда | Runtime, Resources и FrameworkAssemblies |
| compile | lib |
| выполнить сборку | build (свойства и цели MSBuild) |
| в машинном коде | в машинном коде |
| Нет | Нет |
| все | Все папки |

Например, следующие строки указывают зависимости от `PackageA` версии 1.1.0 или более поздней и `PackageB` версии 1.x.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

Следующие строки указывают зависимости от тех же пакетов и включают папки `contentFiles` и `build` для `PackageA`, а также все папки, кроме `native` и `compile`, для `PackageB`"

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

Примечание. При создании файла `.nuspec` для проекта с использованием команды `nuget spec` существующие в проекте зависимости автоматически включаются в полученный файл `.nuspec`.

### <a name="dependency-groups"></a>Группы зависимостей

*Версия 2.0 и более поздние*

В качестве альтернативы простому неструктурированному списку зависимости могут задаваться в соответствии с профилем платформы целевого проекта с использованием элементов `<group>` в элементе `<dependencies>`.

Каждый элемент group имеет атрибут `targetFramework` и содержит ноль или более элементов `<dependency>`. Эти зависимости устанавливаются вместе в том случае, если целевая платформа совместима с профилем платформы проекта.

Элемент `<group>` без атрибута `targetFramework` используется в качестве установленного по умолчанию или резервного списка зависимостей. Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).

> [!Important]
> Формат группы не может смешиваться с неструктурированным списком.

В следующем примере приводятся различные варианты элемента `<group>`:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>Явные ссылки на сборку

Элемент `<references>` явно задает сборки, на которые целевой проект должен ссылаться при использовании пакета. Если этот элемент присутствует, NuGet добавляет ссылки только на указанные в списке сборки, но не на какие-либо другие сборки в папке `lib` проекта.

Например, следующий элемент `<references>` указывает NuGet на необходимость добавлять ссылки только на сборки `xunit.dll` и `xunit.extensions.dll`, даже если в пакете есть другие сборки:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Явные ссылки обычно применяются для сборок, используемых только во время разработки. При использовании [контрактов для кода](/dotnet/framework/debug-trace-profile/code-contracts) сборки контракта должны располагаться рядом со сборками среды выполнения, которые они расширяют, чтобы среда Visual Studio могла находить их. При этом не требуются ссылки на сборки контракта из проекта и эти сборки не нужно копировать в папку `bin` проекта.

Аналогичным образом, явные ссылки можно использовать для платформ модульного тестирования, таких как XUnit, сборки средств которых должны располагаться рядом со сборками среды выполнения, но не требуют включения в ссылки проекта.

### <a name="reference-groups"></a>Группы ссылок

В качестве альтернативы простому неструктурированному списку ссылки могут задаваться в соответствии с профилем платформы целевого проекта с использованием элементов `<group>` в элементе `<references>`.

Каждый элемент group имеет атрибут `targetFramework` и содержит ноль или более элементов `<reference>`. Эти ссылки добавляются в проект в том случае, если целевая платформа совместима с профилем платформы проекта.

Элемент `<group>` без атрибута `targetFramework` используется в качестве установленного по умолчанию или резервного списка ссылок. Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).

> [!Important]
> Формат группы не может смешиваться с неструктурированным списком.

В следующем примере приводятся различные варианты элемента `<group>`:

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a>Ссылки на сборку платформы

Сборки платформы входят в состав .NET Framework и должны находиться в глобальном кэше сборок любого заданного компьютера. Идентифицируя такие сборки с помощью элемента `<frameworkAssemblies>`, пакет может гарантировать, что ссылки, отсутствующие в проекте, будут при необходимости добавлены в него. Естественно, напрямую в пакет такие сборки не включаются.

Элемент `<frameworkAssemblies>` содержит ноль или более элементов `<frameworkAssembly>`, каждый из которых задает следующие атрибуты:

| Атрибут | Описание |
| --- | --- |
| **имя_сборки** | Полное имя сборки (обязательно). |
| **targetFramework** | Указывает целевую платформу, к которой применяется эта ссылка (необязательно). Если этот атрибут опущен, указывает, что ссылка применяется ко всем платформам. Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md). |

В следующем примере показаны ссылка на `System.Net` для всех целевых платформ и ссылка на `System.ServiceModel` только для платформы .NET Framework 4.0:

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>Включение файлов сборки

Если вы придерживаетесь соглашений, описываемых в разделе [Создание пакета](../create-packages/creating-a-package.md), вам не нужно явно задавать список файлов в файле `.nuspec`. Команда `nuget pack` автоматически выбирает необходимые файлы.

> [!Important]
> Когда пакет устанавливается в проекте, NuGet автоматически добавляет ссылки на библиотеки DLL сборок в пакете, *кроме* тех из них, в именах которых есть `.resources.dll`, так как они считаются локализованными вспомогательными сборками. По этой причине следует избегать использования `.resources.dll` в именах файлов пакета, которые содержат важный код.

Чтобы обойти такое автоматическое поведение и явно управлять включением сборок в пакет, поместите элемент `<files>` в качестве дочернего для `<package>` (на одном уровне с `<metadata>`), указывая каждый файл с помощью элемента `<file>`. Пример:

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

В NuGet версии 2.x и более ранних в проектах, использующих `packages.config`, элемент `<files>` также используется для включения неизменяемых файлов содержимого при установке пакета. В NuGet версии 3.3 и более поздних и проектах PackageReference используется элемент `<contentFiles>`. Дополнительные сведения см. в разделе [Включение файлов содержимого](#including-content-files).

### <a name="file-element-attributes"></a>Атрибуты элементов файла

Каждый элемент `<file>` задает указанные ниже атрибуты:

| Атрибут | Описание |
| --- | --- |
| **src** | Расположение файла или файлов, которые требуется включить, с учетом исключений, задаваемых атрибутом `exclude`. Если не указан абсолютный путь, этот путь задается относительно файла `.nuspec`. Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке. |
| **target** | Относительный путь к папке в пакете, куда помещаются файлы исходного кода. Должен начинаться с `lib`, `content`, `build` или `tools`. См. раздел [Создание файла NUSPEC на основе рабочего каталога, соответствующего соглашениям](../create-packages/creating-a-package.md#from-a-convention-based-working-directory). |
| **exclude** | Разделенный точками с запятой список файлов или шаблонов файлов, которые исключаются из расположения `src`. Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке. |

### <a name="examples"></a>Примеры

**Одна сборка**

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

**Одна сборка, относящаяся к целевой платформе**

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

**Набор DLL-файлов с использованием подстановочного знака**

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

**DLL-файлы для разных платформ**

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

**Исключение файлов**

    Source files:
        \tools\*.bak
        \tools\*.log
        \tools\build\*.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a>Включение файлов содержимого

Файлы содержимого — это неизменяемые файлы, которые пакету необходимо включить в проект. Такие файлы не подлежат изменению проектом, который потребляет их. Примеры файлов содержимого:

- Изображения, внедряемые в качестве ресурсов
- Файлы исходного кода, которые уже были скомпилированы
- Скрипты, которые необходимо включить в выходные данные построения проекта
- Файлы конфигурации для пакета, которые необходимо включить в проект, но не требуется изменять в рамках отдельного проекта

Файлы содержимого включаются в проект с помощью элемента `<files>`, задающего папку `content` в атрибуте `target`. Тем не менее такие файлы игнорируются при установке пакета в проект с использованием PackageReference, в которых вместо этого используется элемент `<contentFiles>`.

Чтобы обеспечить максимальную совместимость с потребляющими проектами, в идеальном случае файлы содержимого следует задавать в проекте с использованием обоих элементов.

### <a name="using-the-files-element-for-content-files"></a>Использование элемента files для файлов содержимого

Для файлов содержимого следует использовать тот же формат, что и для файлов сборки, однако необходимо указать в качестве базовой сборки `content` в атрибуте `target`, как показано в следующих примерах.

**Базовые файлы содержимого**

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

**Файлы содержимого со структурой каталогов**

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

**Файлы содержимого, относящиеся к целевой платформе**

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

**Файлы содержимого, копируемые в папку с точкой в имени**

В этом случае NuGet определяет, что расширение в атрибуте `target` не соответствует расширению в `src` и обрабатывает такую часть имени в атрибуте `target` как папку:

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

**Файлы содержимого без расширений**

Чтобы включить файлы без расширения, используйте подстановочные знаки `*` или `**`:

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

**Файлы содержимого с глубоким путем и глубоким целевым объектом**

В этом случае из-за совпадения расширений файлов для исходного и целевого объектов NuGet предполагает, что целевой объект задает имя файла, а не папки:

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

**Переименование файла содержимого в пакете**

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

**Исключение файлов**

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a>Использование элемента contentFiles для файлов содержимого

*NuGet 4.0 и более поздней версии с PackageReference*

По умолчанию пакет помещает содержимое в папку `contentFiles` (см. ниже), а команда `nuget pack` включает все файлы в этой папке с использованием установленных по умолчанию атрибутов. В этом случае включать узел `contentFiles` в файл `.nuspec` не требуется.

Чтобы управлять включаемыми файлами, элемент `<contentFiles>` задает коллекцию элементов `<files>`, которая точно определяет включаемые файлы.

Эти файлы задаются с набором атрибутов, который описывает их использование в системе проекта:

| Атрибут | Описание |
| --- | --- |
| **include** | Расположение файла или файлов, которые требуется включить, с учетом исключений, задаваемых атрибутом `exclude` (обязательно). Если не указан абсолютный путь, этот путь задается относительно файла `.nuspec`. Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке. |
| **exclude** | Разделенный точками с запятой список файлов или шаблонов файлов, которые исключаются из расположения `src`. Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке. |
| **buildAction** | Действие построения, назначаемое элементу содержимого для MSBuild, например `Content`, `None`, `Embedded Resource`, `Compile` и т. д. Значение по умолчанию — `Compile`. |
| **copyToOutput** | Логическое значение, определяющее необходимость копирования содержимого элементов в сборку (или публикация) выходную папку. Значение по умолчанию – false. |
| **flatten** | Логическое значение, указывающее на необходимость копировать элементы содержимого в одну папку в выходных данных построения (true) или сохранить структуру папок пакета (false). Этот параметр применяется, только если для параметра copyToOutput установлено значение true. Значение по умолчанию – false. |

При установке пакета NuGet применяет дочерние элементы `<contentFiles>` в порядке сверху вниз. Если одному файлу соответствует несколько записей, применяются все записи. При обнаружении конфликтов для одного атрибута запись верхнего уровня переопределяет записи на нижних уровнях.

#### <a name="package-folder-structure"></a>Структура папки пакета

Структурирование содержимого в проекте пакета осуществляется по следующему шаблону:

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- Элемент `codeLanguages` может иметь значение `cs`, `vb`, `fs`, `any` или любой другой эквивалент заданного `$(ProjectLanguage)` в нижнем регистре
- Элемент `TxM` представляет любой допустимый моникер целевой платформы, поддерживаемой NuGet (см. раздел [Целевые платформы](../reference/target-frameworks.md)).
- В конце этого синтаксиса может добавляться любая структура папок.

Пример:

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

Для пустых папок можно использовать `.`, чтобы отказаться от предоставления содержимого для определенных комбинаций языка и моникера целевой платформы, например:

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a>Пример раздела contentFiles

```xml
<contentFiles>
    <!-- Embed image resources -->
    <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
    <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

    <!-- Embed all image resources under contentFiles/cs/ -->
    <files include="cs/**/*.png" buildAction="EmbeddedResource" />

    <!-- Copy config.xml to the root of the output folder -->
    <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

    <!-- Copy run.cmd to the output folder and keep the directory structure -->
    <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

    <!-- Include everything in the scripts folder except exe files -->
    <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
</contentFiles>
```

## <a name="example-nuspec-files"></a>Примеры файлов NUSPEC

**Простой файл `.nuspec`, в котором не задаются зависимости или файлы**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
    </metadata>
</package>
```

**Файл `.nuspec` с зависимостями**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

**Файл `.nuspec` с файлами**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

**Файл `.nuspec` со сборками платформы**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

В этом примере для целевых объектов проекта устанавливаются следующие компоненты:

- .NET4 -> `System.Web`, `System.Net`
- Клиентский профиль .NET4 -> `System.Net`
- Silverlight 3 -> `System.Json`
- Silverlight 4 -> `System.Windows.Controls.DomainServices`
- WindowsPhone -> `Microsoft.Devices.Sensors`
