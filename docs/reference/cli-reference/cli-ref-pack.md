---
title: Команда пакета CLI для NuGet
description: Справочник по команде NuGet. exe Pack
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: cab56cb87f46335f9fdebdbc1649fead16459877
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959726"
---
# <a name="pack-command-nuget-cli"></a>Команда pack (NuGet CLI)

Область **применения:** &bullet; **Поддерживаемые версии** для создания пакетов: 2.7+

Создает пакет NuGet на основе указанного файла [. nuspec](../nuspec.md) или проекта. Команда (см. [команды DotNet](../dotnet-Commands.md)) и `msbuild -t:pack` (см. [целевые объекты MSBuild](../msbuild-targets.md)) могут использоваться в качестве альтернатив. `dotnet pack`

> [!Important]
> В группе Mono создание пакета из файла проекта не поддерживается. Кроме того, необходимо изменить нелокальные пути в `.nuspec` файле на пути в стиле UNIX, так как NuGet. exe не преобразует сами пути Windows.

## <a name="usage"></a>Использование

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

где `<nuspecPath>` и `<projectPath>` укажите`.nuspec` файл проекта или соответственно.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| BasePath | Задает базовый путь к файлам, определенным в файле [nuspec](../nuspec.md) . |
| Построить | Указывает, что проект должен быть построен перед построением пакета. |
| Исключить | Задает шаблоны с подстановочными знаками, исключаемые при создании пакета. Чтобы указать более одного шаблона, повторите флаг-Exclude. См. пример ниже. |
| ексклудимптидиректориес | Предотвращает включение пустых каталогов при сборке пакета. |
| форцеенглишаутпут | *(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке. |
| ConfigFile | Укажите файл конфигурации для команды Pack. |
| Help | Отображает справочные сведения для команды. |
| инклудереференцедпрожектс | Указывает, что построенный пакет должен включать проекты, на которые указывают ссылки, либо как зависимости, либо как часть пакета. Если проект, на который указывает ссылка `.nuspec` , имеет соответствующий файл, имя которого совпадает с именем проекта, то указанный проект добавляется как зависимость. В противном случае проект, на который указывает ссылка, добавляется как часть пакета. |
| MinClientVersion | Задайте атрибут *minClientVersion* для созданного пакета. Это значение переопределит значение существующего атрибута *minClientVersion* (если он есть) в `.nuspec` файле. |
| мсбуилдпас | *(4.0 +)* Указывает путь MSBuild для использования с командой, который имеет приоритет над `-MSBuildVersion`. |
| мсбуилдверсион | *(3.2 +)* Указывает версию MSBuild, которая будет использоваться с этой командой. Поддерживаемые значения: 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. По умолчанию в пути выбирается MSBuild, в противном случае — по умолчанию — самая высокая установленная версия MSBuild. |
| нодефаултексклудес | Предотвращает исключение по умолчанию для файлов пакетов NuGet и файлов и папок, начинающихся с точки `.svn` , `.gitignore`например и. |
| NoPackageAnalysis | Указывает, что пакету не нужно запускать анализ пакета после его сборки. |
| OutputDirectory | Указывает папку, в которой хранится созданный пакет. Если папка не указана, используется текущая папка. |
| Свойства | Должно отобразиться в командной строке в последнюю очередь после других параметров. Указывает список свойств, переопределяющих значения в файле проекта. см. раздел [Общие свойства проекта MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) для имен свойств. Аргумент Properties здесь представляет собой список пар token = значение, разделенных точкой с запятой, где каждое вхождение `$token$` `.nuspec` в файле будет заменено заданным значением. Значения могут быть строками в кавычках. Обратите внимание, что для свойства "Configuration" значение по умолчанию — "Debug". Чтобы изменить конфигурацию выпуска, используйте `-Properties Configuration=Release`. |
| Суффикс | *(3.4.4 +)* Добавляет суффикс ко внутреннему номеру версии, который обычно используется для присоединения сборки или других идентификаторов предварительной версии. Например, при использовании `-suffix nightly` будет создан пакет с номером версии, например. `1.2.3-nightly` Суффиксы должны начинаться с буквы, чтобы избежать предупреждений, ошибок и потенциальных несовместимости с различными версиями NuGet и диспетчером пакетов NuGet. |
| Символы | Указывает, что пакет содержит источники и символы. При использовании с `.nuspec` файлом он создает обычный файл пакета NuGet и соответствующий пакет символов. По умолчанию он создает [устаревший пакет символов](../../create-packages/Symbol-Packages.md). Новый рекомендуемый формат для пакетов символов — .snupkg. См. раздел [Создание пакетов символов (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md). |
| Средство | Указывает, что выходные файлы проекта должны быть помещены в `tool` папку. |
| Verbosity | Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*. |
| Версия | Переопределяет номер версии из `.nuspec` файла. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Исключение зависимостей разработки

Некоторые пакеты NuGet полезны в качестве зависимостей разработки, которые помогают создавать собственные библиотеки, но не обязательно должны быть реальными зависимостями пакетов.

`package` Командабудет`packages.config` игнорировать записив`true`, для которых атрибутуприсвоенозначение.`developmentDependency` `pack` Эти записи не будут включены в качестве зависимостей в созданный пакет.

Например, рассмотрим следующий `packages.config` файл в исходном проекте:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Для этого проекта пакет, созданный `nuget pack` , будет иметь зависимость от `jQuery` и, `microsoft-web-helpers` но не `netfx-Guard`.

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
