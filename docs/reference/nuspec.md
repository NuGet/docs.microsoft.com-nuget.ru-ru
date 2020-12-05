---
title: Ссылка на файл. nuspec для NuGet
description: Файл с расширением .nuspec содержит метаданные пакета, которые используются при построении пакета и предоставляют дополнительную информацию для его потребителей.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6e5107ac05046ea46cc819ebe2a504ba6b030634
ms.sourcegitcommit: e39e5a5ddf68bf41e816617e7f0339308523bbb3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2020
ms.locfileid: "96738946"
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
- [Пример файлов nuspec](#example-nuspec-files)

## <a name="project-type-compatibility"></a>Совместимость типов проектов

- Используйте `.nuspec` с `nuget.exe pack` для проектов в стиле, не являющихся SDK, которые используют `packages.config` .

- `.nuspec`Файл не требуется для создания пакетов для проектов в [стиле SDK](../resources/check-project-format.md) (обычно это проекты .net Core и .NET Standard, использующие [атрибут SDK](/dotnet/core/tools/csproj#additions)). (Обратите внимание, что `.nuspec` создается при создании пакета.)

   При создании пакета с помощью `dotnet.exe pack` или `msbuild pack target` рекомендуется включить в файл проекта [все свойства](../reference/msbuild-targets.md#pack-target) , которые обычно находятся в `.nuspec` файле. Однако вместо этого можно [использовать `.nuspec` файл для упаковки с помощью `dotnet.exe` или `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec).

- Для проектов, перенесенных из `packages.config` в [PackageReference](../consume-packages/package-references-in-project-files.md), `.nuspec` для создания пакета не требуется файл. Вместо этого используйте [MSBuild-т:ПАКК](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).

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

Все имена XML-элементов в nuspec-файле чувствительны к регистру, как и в случае с XML в целом. Например, использование элемента metadata `<description>` является правильным и `<Description>` неправильным. Ниже описан правильный регистр для каждого имени элемента.

### <a name="required-metadata-elements"></a>Обязательные элементы метаданных

Следующие элементы являются минимальным требованием для пакета, однако, несмотря на это, рекомендуется добавить [дополнительные элементы метаданных](#optional-metadata-elements), чтобы оптимизировать работу с вашим пакетом для разработчиков. 

Эти элементы должны использоваться внутри элемента `<metadata>`.

#### <a name="id"></a>идентификатор 
Идентификатор пакета без учета регистра, который должен быть уникальным в пределах сайта nuget.org или иной коллекции, в которой находится пакет. Идентификаторы не должны содержать пробелов или символов, которые недопустимы в URL-адресах, и в них должны соблюдаться общие правила касательно пространств имен .NET. Инструкции см. в разделе [Выбор уникального идентификатора пакета](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).

При отправке пакета в nuget.org `id` поле ограничено 128 символами.

#### <a name="version"></a>version
Версия пакета, указываемая согласно шаблону *основной_номер.дополнительный_номер.исправление*. Номер версии может включать в себя суффикс предварительной версии, как описано в разделе [Управление версиями пакета](../concepts/package-versioning.md#pre-release-versions). 

При отправке пакета в nuget.org `version` поле ограничено 64 символами.

#### <a name="description"></a>description
Описание пакета для вывода пользовательского интерфейса.

При отправке пакета в nuget.org `description` поле ограничено 4000 символами.

#### <a name="authors"></a>authors
Разделенный запятыми список авторов пакетов, соответствующих именам профилей в nuget.org. Они отображаются в коллекции NuGet в nuget.org и используются для перекрестных ссылок на пакеты с теми же авторами. 

При отправке пакета в nuget.org `authors` поле ограничено 4000 символами.

### <a name="optional-metadata-elements"></a>Необязательные элементы метаданных

#### <a name="owners"></a>owners
> [!Important]
> владельцы являются устаревшими. Вместо этого используйте авторов.

Разделенный запятыми список авторов пакетов, использующих имена профилей в nuget.org. Часто это тот же список, что `authors` и в, и игнорируется при отправке пакета в NuGet.org. См. раздел [Управление владельцами пакетов в NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg). 

#### <a name="projecturl"></a>projectUrl
URL-адрес для домашней страницы пакета, часто указываемый при отображении пользовательского интерфейса, также как и nuget.org. 

При отправке пакета в nuget.org `projectUrl` поле ограничено 4000 символами.

#### <a name="licenseurl"></a>licenseUrl
> [!Important]
> licenseUrl является устаревшим. Используйте вместо этого лицензию.

URL-адрес для лицензии пакета, часто показанный в пользовательских интерфейсах, таких как nuget.org.

При отправке пакета в nuget.org `licenseUrl` поле ограничено 4000 символами.

#### <a name="license"></a>license

*Поддерживается для **NuGet 4.9.0** и более поздних версий*

Выражение лицензии СПДКС или путь к файлу лицензии в пакете, который часто отображается в пользовательских интерфейсах, например nuget.org. Если вы намерены лицензирование пакета с помощью обычной лицензии, например MIT или BSD-2-предложения, используйте соответствующий [идентификатор лицензии спдкс](https://spdx.org/licenses/). Пример:

`<license type="expression">MIT</license>`

> [!Note]
> NuGet.org принимает только те лицензионные выражения, которые утверждены инициативой Open Source или Free Software Foundation.

Если пакет лицензирован в нескольких распространенных лицензиях, можно указать составную лицензию с помощью [синтаксиса выражений спдкс версии 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60). Пример:

`<license type="expression">BSD-2-Clause OR MIT</license>`

При использовании пользовательской лицензии, которая не поддерживается в выражениях лицензий, можно упаковать `.txt` `.md` файл или с текстом лицензии. Пример:

```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

Для эквивалента MSBuild ознакомьтесь с [упаковкой лицензионного выражения или файла лицензии](msbuild-targets.md#packing-a-license-expression-or-a-license-file).

Точный синтаксис выражений лицензии NuGet описывается ниже в [ABNF](https://tools.ietf.org/html/rfc5234).
```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a>iconUrl

> [!Important]
> Иконурл является устаревшим. Вместо этого используйте значок.

URL-адрес для изображения 128x128 с фоном прозрачности для использования в качестве значка для пакета в пользовательском интерфейсе. Убедитесь, что этот элемент содержит *прямой URL-адрес изображения*, а не URL-адрес веб-страницы, на которой содержится изображение. Например, чтобы использовать изображение из GitHub, используйте URL-адрес необработанного файла, например <em> https://github.com/ \<username\> / \<repository\> /рав/ \<branch\> / \<logo.png\> </em>. 
   
При отправке пакета в nuget.org `iconUrl` поле ограничено 4000 символами.

#### <a name="icon"></a>icon

*Поддерживается для **NuGet 5.3.0** и более поздних версий*

Это путь к файлу изображения в пакете, который часто отображается в пользовательских интерфейсах, таких как nuget.org, как значок пакета. Размер файла изображения ограничен 1 МБ. Поддерживаются следующие форматы файлов: JPEG и PNG. Рекомендуется разрешение изображения 128x128.

Например, при создании пакета с помощью nuget.exe необходимо добавить следующий объект в nuspec:

```xml
<package>
  <metadata>
    ...
    <icon>images\icon.png</icon>
    ...
  </metadata>
  <files>
    ...
    <file src="..\icon.png" target="images\" />
    ...
  </files>
</package>
```

[Значок пакета nuspec Sample.](https://github.com/NuGet/Samples/tree/master/PackageIconNuspecExample)

Чтобы получить эквивалент MSBuild, Взгляните на [упаковку файла изображения значка](msbuild-targets.md#packing-an-icon-image-file).

> [!Tip]
> Можно указать `icon` и, и `iconUrl` для обеспечения обратной совместимости с источниками, которые не поддерживаются `icon` . Visual Studio будет поддерживать `icon` пакеты, поступающие из источника на основе папок в будущем выпуске.

#### <a name="requirelicenseacceptance"></a>requireLicenseAcceptance
Логическое значение, указывающее, должен ли клиент просить потребителя принять условия лицензии перед установкой пакета.

#### <a name="developmentdependency"></a>developmentDependency
*(Версия 2.8 и более поздние)* Логическое значение, указывающее, помечен ли пакет как зависимость только для разработки, что позволяет запретить его включение в качестве зависимости в другие пакеты. При использовании PackageReference (NuGet 4.8+) этот флажок также указывает на исключение ресурсов времени компиляции из компиляции. См. раздел [Поддержка DevelopmentDependency для PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) .

#### <a name="summary"></a>Итоги
> [!Important]
> `summary` является устаревшим. Взамен рекомендуется использовать `description`.

Краткое описание пакета для отображения пользовательского интерфейса. Если этот элемент опущен, используется сокращенная версия элемента `description`.

При отправке пакета в nuget.org `summary` поле ограничено 4000 символами.

#### <a name="releasenotes"></a>releaseNotes
*(Версия 1.5 и более поздние)* Описание изменений, внесенных в этом выпуске пакета NuGet; часто используется в пользовательском интерфейсе как вкладка **Обновления** диспетчера пакетов Visual Studio вместо описания пакета.

При отправке пакета в nuget.org `releaseNotes` поле ограничено 35 000 символами.

#### <a name="copyright"></a>авторские права
*(Версия 1.5 и более поздние)* Сведения об авторских правах для пакета.

При отправке пакета в nuget.org `copyright` поле ограничено 4000 символами.

#### <a name="language"></a>язык
Идентификатор языкового стандарта для пакета. См. раздел [Создание локализованных пакетов](../create-packages/creating-localized-packages.md).

#### <a name="tags"></a>tags
Список разделенных пробелами тегов и ключевых слов, описывающих пакет NuGet и помогающих находить пакеты NuGet с помощью функций поиска и фильтрации. 

При отправке пакета в nuget.org `tags` поле ограничено 4000 символами.

#### <a name="serviceable"></a>serviceable 
*(Версия 3.3 и более поздние)* Только для внутреннего использования в NuGet.

#### <a name="repository"></a>repository
Метаданные репозитория, состоящие из четырех необязательных атрибутов: `type` и `url` *(4.0 +)* и `branch` и `commit` *(4.6 +)*. Эти атрибуты позволяют сопоставлять объект `.nupkg` с репозиторием, в котором он построен, с возможностью получения таких сведений, как имя отдельной ветви и/или фиксация ХЭША SHA-1, который создал пакет. Это должен быть общедоступный URL-адрес, который может вызываться непосредственно программным обеспечением управления версиями. Это не должна быть HTML-страница, так как она предназначена для компьютера. Для ссылки на страницу проекта используйте `projectUrl` вместо этого поле.

Пример:
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

При отправке пакета в nuget.org `type` Длина атрибута ограничена 100 символами, а `url` Длина атрибута ограничена 4000 символами.

#### <a name="title"></a>title
Удобное для человека название пакета, которое может использоваться в некоторых интерфейсах пользователя. (nuget.org и диспетчер пакетов в Visual Studio не отображают заголовок)

При отправке пакета в nuget.org `title` поле ограничено 256 символами, но не используется в целях вывода.

#### <a name="collection-elements"></a>Элементы коллекции

#### <a name="packagetypes"></a>packageTypes
*(Версия 3.5 и более поздние)* Пустая коллекция или без нескольких элементов `<packageType>`, определяющих тип пакета, если он отличается от обычного пакета зависимостей. Каждый элемент packageType имеет атрибуты *name* и *version*. См. раздел [Указание типа пакета](../create-packages/set-package-type.md).
#### <a name="dependencies"></a>зависимости
Коллекция из нуля или более элементов `<dependency>`, задающих зависимости для пакета. Каждый элемент dependency имеет атрибуты *id*, *version*, *include* (версия 3.x и более поздние) и *exclude* (версия 3.x и более поздние). См. раздел [Зависимости](#dependencies-element) далее.
#### <a name="frameworkassemblies"></a>frameworkAssemblies
*(Версия 1.2 и более поздние)* Коллекция из одного или более элементов `<frameworkAssembly>`, идентифицирующих ссылки на сборки .NET Framework, необходимые для этого пакета, что гарантирует добавление ссылок в проекты, использующие пакет. Каждый элемент frameworkAssembly имеет атрибуты *assemblyName* и *targetFramework*. См. раздел [Указание ссылок на сборки платформы в глобальном кэше сборок ](#specifying-framework-assembly-references-gac) ниже.
#### <a name="references"></a>Ссылки
*(Версия 1.5 и более поздние)* Коллекция из нуля или более элементов `<reference>`, задающие имена сборок в папке `lib` пакета, которые добавляются в качестве ссылок проекта. Каждый элемент reference имеет атрибут *file*. Коллекция `<references>` также может содержать элемент `<group>` с атрибутом *targetFramework*, который, в свою очередь, содержит элементы `<reference>`. Если этот элемент опущен, включаются все ссылки в папке `lib`. См. раздел [Указание явных ссылок на сборки](#specifying-explicit-assembly-references) ниже.
#### <a name="contentfiles"></a>contentFiles
*(Версия 3.3 и более поздние)* Коллекция элементов `<files>`, которые идентифицируют файлы содержимого, включаемые в потребляющий проект. Эти файлы задаются с набором атрибутов, который описывает их использование в системе проекта. См. раздел [Указание включаемых в пакет файлов](#specifying-files-to-include-in-the-package) ниже.
#### <a name="files"></a>files 
`<package>`Узел может содержать узел в `<files>` качестве одноуровневого элемента для `<metadata>` и `<contentFiles>` дочерний элемент в `<metadata>` , чтобы указать, какие файлы сборки и содержимого следует включить в пакет. Дополнительные сведения см. далее в разделах [Включение файлов сборки](#including-assembly-files) и [Включение файлов содержимого](#including-content-files) этой статьи.

### <a name="metadata-attributes"></a>атрибуты метаданных

#### <a name="minclientversion"></a>minClientVersion
Указывает минимальную версию клиента NuGet, который может установить этот пакет с использованием nuget.exe и диспетчера пакетов Visual Studio. Используется во всех случаях, когда пакет зависит от конкретных функций в файле `.nuspec`, которые были добавлены в определенной версии клиента NuGet. Например, для пакета, использующего атрибут `developmentDependency`, атрибуту `minClientVersion` необходимо присвоить значение "2.8". Аналогичным образом, для пакета, использующего элемент `contentFiles` (см. следующий раздел), атрибуту `minClientVersion` необходимо присвоить значение "3.3". Также обратите внимание, что клиенты NuGet версий, предшествующих 2.5, не распознают этот флаг и поэтому *всегда* отклоняют установку пакета независимо от значения атрибута `minClientVersion`.

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata minClientVersion="100.0.0.1">
        <id>dasdas</id>
        <version>2.0.0</version>
        <title />
        <authors>dsadas</authors>
        <owners />
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>My package description.</description>
    </metadata>
    <files>
        <file src="content\one.txt" target="content\one.txt" />
    </files>
</package>
```

## <a name="replacement-tokens"></a>Замена маркеров

При создании пакета [ `nuget pack` команда](../reference/cli-reference/cli-ref-pack.md) заменяет маркеры с разделителями $ в `.nuspec` `<metadata>` узле файла значениями, поступающими из файла проекта или `pack` `-properties` переключателя команды.

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
| **$id $** | Файл проекта | AssemblyName (Title) из файла проекта |
| **$version $** | AssemblyInfo | AssemblyInformationalVersion, если присутствует, в противном случае AssemblyVersion |
| **$author $** | AssemblyInfo | AssemblyCompany |
| **$title $** | AssemblyInfo | ассемблититле |
| **$description $** | AssemblyInfo | AssemblyDescription |
| **$copyright $** | AssemblyInfo | AssemblyCopyright |
| **$configuration $** | DLL-файл сборки | Конфигурация, используемая для построения сборки, по умолчанию используется тип отладки. Обратите внимание, что для создания пакета с помощью конфигурации выпуска в командной строке всегда используется параметр `-properties Configuration=Release`. |

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

## <a name="dependencies-element"></a>DEPENDENCIES, элемент

Элемент `<dependencies>` внутри элемента `<metadata>` содержит любое число элементов `<dependency>`, идентифицирующих другие пакеты, от которых зависит пакет верхнего уровня. Ниже перечислены атрибуты каждого элемента `<dependency>`:

| attribute | Описание |
| --- | --- |
| `id` | Идентификатор пакета зависимости, например EntityFramework и NUnit, являющийся именем пакета nuget.org, показан на странице пакета (обязательно). |
| `version` | Диапазон версий, которые допустимы в качестве зависимости (обязательно). Точный синтаксис см. в разделе [Управление версиями пакета](../concepts/package-versioning.md#version-ranges). Плавающие версии не поддерживаются. |
| include | Разделенный запятыми список тегов включения или исключения (см. ниже), определяющий зависимости, включаемые в конечный пакет. Значение по умолчанию — `all`. |
| исключение | Разделенный запятыми список тегов включения или исключения (см. ниже), определяющий зависимости, исключаемые из конечного пакета. Значение по умолчанию, `build,analyzers` которое может быть перезаписано. Но `content/ ContentFiles` также неявно исключаются в окончательном пакете, который не может быть перезаписан. Теги в свойстве `exclude` имеют приоритет перед тегами в свойстве `include`. Например, `include="runtime, compile" exclude="compile"` равносильно `include="runtime"`. |

При отправке пакета в nuget.org длина `id` атрибута зависимости ограничена 128 символами, а `version` Длина атрибута ограничена 256 символами.

| Тег включения или исключения | Затрагиваемые папки пакета |
| --- | --- |
| contentFiles | Содержимое |
| исполняющая среда | Runtime, Resources и FrameworkAssemblies |
| compile | lib |
| build; | build (свойства и цели MSBuild) |
| в машинном коде | в машинном коде |
| нет | Нет |
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

> [!Important]
> При создании `.nuspec` из проекта с помощью `nuget spec` , зависимости, существующие в этом проекте, не включаются автоматически в результирующий `.nuspec` файл. Вместо этого используйте `nuget pack myproject.csproj` и получите файл с *расширением nuspec* в созданном *nupkgном* файле. Этот *nuspec* содержит зависимости.

### <a name="dependency-groups"></a>Группы зависимостей

*Версия 2.0 +*

В качестве альтернативы простому неструктурированному списку зависимости могут задаваться в соответствии с профилем платформы целевого проекта с использованием элементов `<group>` в элементе `<dependencies>`.

Каждый элемент group имеет атрибут `targetFramework` и содержит ноль или более элементов `<dependency>`. Эти зависимости устанавливаются вместе в том случае, если целевая платформа совместима с профилем платформы проекта.

Элемент `<group>` без атрибута `targetFramework` используется в качестве установленного по умолчанию или резервного списка зависимостей. Точное описание идентификаторов платформы см. в разделе [Целевые платформы](../reference/target-frameworks.md).

> [!Important]
> Формат группы не может смешиваться с неструктурированным списком.

> [!Note]
> Формат [моникера целевой платформы (TFM)](../reference/target-frameworks.md) , используемый в `lib/ref` папке, отличается по сравнению с TFM, используемым в `dependency groups` . Если целевые платформы, объявленные в `dependencies group` и в `lib/ref` папке `.nuspec` файла, не имеют точных совпадений, `pack` команда вызовет вызов [предупреждения NuGet NU5128](../reference/errors-and-warnings/nu5128.md).

В следующем примере приводятся различные варианты элемента `<group>`:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework=".NETFramework4.7.2">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="netcoreapp3.1">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>Явные ссылки на сборку

`<references>`Элемент используется проектами с `packages.config` целью явного указания сборок, на которые должен ссылаться целевой проект при использовании пакета. Явные ссылки обычно применяются для сборок, используемых только во время разработки. Дополнительные сведения см. на странице [Выбор сборок, на которые ссылаются проекты](../create-packages/select-assemblies-referenced-by-projects.md) .

Например, следующий элемент `<references>` указывает NuGet на необходимость добавлять ссылки только на сборки `xunit.dll` и `xunit.extensions.dll`, даже если в пакете есть другие сборки:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

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

| attribute | Описание |
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

| attribute | Описание |
| --- | --- |
| **src** | Расположение файла или файлов, которые требуется включить, с учетом исключений, задаваемых атрибутом `exclude`. Если не указан абсолютный путь, этот путь задается относительно файла `.nuspec`. Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке. |
| **target** | Относительный путь к папке в пакете, куда помещаются файлы исходного кода. Должен начинаться с `lib`, `content`, `build` или `tools`. См. раздел [Создание файла NUSPEC на основе рабочего каталога, соответствующего соглашениям](../create-packages/creating-a-package.md#from-a-convention-based-working-directory). |
| **запрет** | Разделенный точками с запятой список файлов или шаблонов файлов, которые исключаются из расположения `src`. Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке. |

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
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

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

| attribute | Описание |
| --- | --- |
| **относится** | Расположение файла или файлов, которые требуется включить, с учетом исключений, задаваемых атрибутом `exclude` (обязательно). Путь задается относительно `contentFiles` папки, если не указан абсолютный путь. Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке. |
| **запрет** | Разделенный точками с запятой список файлов или шаблонов файлов, которые исключаются из расположения `src`. Допускается использовать подстановочный знак `*`. Наличие сдвоенного подстановочного знака `**` подразумевает выполнение рекурсивного поиска в папке. |
| **buildAction** | Действие сборки, присваиваемое элементу содержимого для MSBuild, например,, `Content` , `None` `Embedded Resource` `Compile` и т. д. Значение по умолчанию — `Compile` . |
| **copyToOutput** | Логическое значение, указывающее, следует ли копировать элементы содержимого в выходную папку сборки (или публикации). Значение по умолчанию – false. |
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
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
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
        </metadata>
</package>
```

## <a name="framework-reference-groups"></a>Эталонные группы платформы

*Только версия 5.1 и вих PackageReference*

Ссылки на платформы — это концепция .NET Core, представляющая общие платформы, такие как WPF или Windows Forms.
Если указать общую платформу, пакет гарантирует, что все его зависимости Framework будут включены в ссылающийся проект.

Каждому `<group>` элементу требуется `targetFramework` атрибут и ноль или более `<frameworkReference>` элементов.

В следующем примере показан nuspec, созданный для проекта .NET Core WPF.
Обратите внимание, что создание нуспекс, содержащих ссылки на платформы, не рекомендуется. Вместо этого рекомендуется использовать [целевой](msbuild-targets.md) пакет, который автоматически определит их в проекте.

```xml
<package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
  <metadata>
    <dependencies>
      <group targetFramework=".NETCoreApp3.1" />
    </dependencies>
    <frameworkReferences>
      <group targetFramework=".NETCoreApp3.1">
        <frameworkReference name="Microsoft.WindowsDesktop.App.WPF" />
      </group>
    </frameworkReferences>
  </metadata>
</package>
```

## <a name="example-nuspec-files"></a>Пример файлов nuspec

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
        <license type="expression">MIT</license>
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
- WindowsPhone -> `Microsoft.Devices.Sensors`
