---
title: Команда пакета CLI для NuGet
description: Справочник по команде nuget.exe Pack
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0483a75c7ee1fd851f935f44d96a417e2e86bf20
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622958"
---
# <a name="pack-command-nuget-cli"></a>Команда Pack (интерфейс командной строки NuGet)

Область **применения:** &bullet; **Поддерживаемые версии** для создания пакетов: 2.7 +

Создает пакет NuGet на основе указанного файла [. nuspec](../nuspec.md) или проекта. `dotnet pack`Команда (см. [команды DotNet](../dotnet-Commands.md)) и `msbuild -t:pack` (см. [целевые объекты MSBuild](../msbuild-targets.md)) могут использоваться в качестве альтернатив.

> [!Important]
> Используйте [`dotnet pack`](../dotnet-Commands.md) или [`msbuild -t:pack`](../msbuild-targets.md) для проектов на основе [PackageReference](../../consume-packages/package-references-in-project-files.md) .
> В группе Mono создание пакета из файла проекта не поддерживается. Кроме того, необходимо изменить нелокальные пути в `.nuspec` файле на пути в стиле UNIX, так как nuget.exe не преобразует пути Windows.

## <a name="usage"></a>Использование

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

где `<nuspecPath>` и `<projectPath>` укажите `.nuspec` файл проекта или соответственно.

## <a name="options"></a>Параметры
- **`-BasePath`**

   Задает базовый путь к файлам, определенным в файле [nuspec](../nuspec.md) .

- **`-Build`**

  Указывает, что проект должен быть построен перед построением пакета.

- **`-ConfigFile`**

  Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-Exclude`**

  Задает шаблоны с подстановочными знаками, исключаемые при создании пакета. Чтобы указать более одного шаблона, повторите флаг-Exclude. См. пример ниже.

- **`-ExcludeEmptyDirectories`**

  Предотвращает включение пустых каталогов при сборке пакета.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.

- **`-?|-help`**

  Отображает справочные сведения для команды.

- **`-IncludeReferencedProjects`**

  Указывает, что построенный пакет должен включать проекты, на которые указывают ссылки, либо как зависимости, либо как часть пакета. Если проект, на который указывает ссылка, имеет соответствующий `.nuspec` файл, имя которого совпадает с именем проекта, то указанный проект добавляется как зависимость. В противном случае проект, на который указывает ссылка, добавляется как часть пакета.

- **`-InstallPackageToOutputPath`**

  Укажите, должна ли команда подготовить выходной каталог пакета для поддержки общего доступа к веб-каналу.

- **`-MinClientVersion`**

  Задайте атрибут *minClientVersion* для созданного пакета. Это значение переопределит значение существующего атрибута *minClientVersion* (если он есть) в `.nuspec` файле.

- **`-MSBuildPath`**

  *(4.0 +)* Указывает путь MSBuild для использования с командой, который имеет приоритет над `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 +)* Указывает версию MSBuild, которая будет использоваться с этой командой. Поддерживаемые значения: 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. По умолчанию в пути выбирается MSBuild, в противном случае — по умолчанию — самая высокая установленная версия MSBuild.

- **`-NoDefaultExcludes`**

  Предотвращает исключение по умолчанию для файлов пакетов NuGet и файлов и папок, начинающихся с точки, например `.svn` и `.gitignore` .

- **`-NonInteractive`**

  Подавляет запросы на ввод или подтверждение пользователя.

- **`-NoPackageAnalysis`**

  Указывает, что пакету не нужно запускать анализ пакета после его сборки.

- **`-OutputDirectory`**

  Указывает папку, в которой хранится созданный пакет. Если папка не указана, используется текущая папка.

- **`-OutputFileNamesWithoutVersion`**

  Укажите, должна ли команда подготовить имя выхода пакета без версии.

- **`-PackagesDirectory`**

  Указывает папку Packages.

- **`-p|-Properties`**

  Должно отобразиться в командной строке в последнюю очередь после других параметров. Указывает список свойств, переопределяющих значения в файле проекта. см. раздел [Общие свойства проекта MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) для имен свойств. Аргумент Properties здесь представляет собой список пар token = значение, разделенных точкой с запятой, где каждое вхождение `$token$` в `.nuspec` файле будет заменено заданным значением. Значения могут быть строками в кавычках. Обратите внимание, что для свойства "Configuration" значение по умолчанию — "Debug". Чтобы изменить конфигурацию выпуска, используйте `-Properties Configuration=Release` . Как **правило**, свойства должны быть теми же, которые использовались во время соответствующей сборки проекта, чтобы избежать потенциально странного поведения.

- **`-SolutionDirectory`**

  Указывает каталог решения.

- **`-Suffix`**

  *(3.4.4 +)* Добавляет суффикс ко внутреннему номеру версии, который обычно используется для присоединения сборки или других идентификаторов предварительной версии. Например, при использовании `-suffix nightly` будет создан пакет с номером версии, например `1.2.3-nightly` . Суффиксы должны начинаться с буквы, чтобы избежать предупреждений, ошибок и потенциальных несовместимости с различными версиями NuGet и диспетчером пакетов NuGet.

- **`-SymbolPackageFormat`**

  При создании пакета символов позволяет выбрать `snupkg` `symbols.nupkg` Формат и.

- **`-Symbols`**

  Указывает, что пакет содержит источники и символы. При использовании с `.nuspec` файлом он создает обычный файл пакета NuGet и соответствующий пакет символов. По умолчанию он создает [устаревший пакет символов](../../create-packages/Symbol-Packages.md). Новый рекомендуемый формат для пакетов символов — .snupkg. См. раздел [Создание пакетов символов (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).

- **`-Tool`**

   Указывает, что выходные файлы проекта должны быть помещены в `tool` папку.

- **`-Verbosity [normal|quiet|detailed]`**

  Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .

- **`-Version`**

  Переопределяет номер версии из `.nuspec` файла.

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Исключение зависимостей разработки

Некоторые пакеты NuGet полезны в качестве зависимостей разработки, которые помогают создавать собственные библиотеки, но не обязательно должны быть реальными зависимостями пакетов.

`pack`Команда будет игнорировать `package` записи в `packages.config` , для которых `developmentDependency` атрибуту присвоено значение `true` . Эти записи не будут включены в качестве зависимостей в созданный пакет.

Например, рассмотрим следующий `packages.config` файл в исходном проекте:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Для этого проекта пакет, созданный, `nuget pack` будет иметь зависимость от `jQuery` и, `microsoft-web-helpers` но не `netfx-Guard` .

## <a name="suppressing-pack-warnings"></a>Подавление предупреждений о пакете

Хотя рекомендуется разрешать все предупреждения NuGet во время операций с пакетами, в некоторых ситуациях их подавление не гарантируется.

Это можно сделать следующим образом: 

> Пакет nuget.exe пакета. nuspec-Properties не warn = NU5104

## <a name="examples"></a>Примеры

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
