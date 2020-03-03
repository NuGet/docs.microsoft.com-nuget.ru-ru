---
title: Команда пакета CLI для NuGet
description: Справочник по команде NuGet. exe Pack
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 2358cedc05520a3ec82a39aef34b6d467e44460b
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231166"
---
# <a name="pack-command-nuget-cli"></a>Команда pack (NuGet CLI)

Область **применения:** создание пакета &bullet; **Поддерживаемые версии:** 2.7 +

Создает пакет NuGet на основе указанного файла [. nuspec](../nuspec.md) или проекта. Команда `dotnet pack` (см. [команды DotNet](../dotnet-Commands.md)) и `msbuild -t:pack` (см. раздел [целевые объекты MSBuild](../msbuild-targets.md)) может использоваться в качестве альтернативы.

> [!Important]
> Используйте [`dotnet pack`](../dotnet-Commands.md) или [`msbuild -t:pack`](../msbuild-targets.md) для проектов на основе [PackageReference](../../consume-packages/package-references-in-project-files.md) .
> В группе Mono создание пакета из файла проекта не поддерживается. Кроме того, необходимо изменить нелокальные пути в файле `.nuspec` на пути в стиле UNIX, так как NuGet. exe не преобразует пути Windows.

## <a name="usage"></a>Использование

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

где `<nuspecPath>` и `<projectPath>` указать `.nuspec` или файл проекта соответственно.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| BasePath | Задает базовый путь к файлам, определенным в файле [nuspec](../nuspec.md) . |
| Сборка | Указывает, что проект должен быть построен перед построением пакета. |
| Исключить | Задает шаблоны с подстановочными знаками, исключаемые при создании пакета. Чтобы указать более одного шаблона, повторите флаг-Exclude. См. пример ниже. |
| ексклудимптидиректориес | Предотвращает включение пустых каталогов при сборке пакета. |
| ForceEnglishOutput | *(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке. |
| ConfigFile | Укажите файл конфигурации для команды Pack. |
| Справка | Отображает справочные сведения для команды. |
| инклудереференцедпрожектс | Указывает, что построенный пакет должен включать проекты, на которые указывают ссылки, либо как зависимости, либо как часть пакета. Если проект, на который указывает ссылка, имеет соответствующий файл `.nuspec`, имя которого совпадает с именем проекта, то этот проект добавляется в качестве зависимости. В противном случае проект, на который указывает ссылка, добавляется как часть пакета. |
| MinClientVersion | Задайте атрибут *minClientVersion* для созданного пакета. Это значение переопределит значение существующего атрибута *minClientVersion* (если таковое имеется) в файле `.nuspec`. |
| мсбуилдпас | *(4.0 +)* Указывает путь MSBuild для использования с командой, который имеет приоритет над `-MSBuildVersion`. |
| мсбуилдверсион | *(3.2 +)* Указывает версию MSBuild, которая будет использоваться с этой командой. Поддерживаемые значения: 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. По умолчанию в пути выбирается MSBuild, в противном случае — по умолчанию — самая высокая установленная версия MSBuild. |
| нодефаултексклудес | Предотвращает исключение по умолчанию файлов и папок пакета NuGet, начинающихся с точки, например `.svn` и `.gitignore`. |
| NoPackageAnalysis | Указывает, что пакету не нужно запускать анализ пакета после его сборки. |
| OutputDirectory | Указывает папку, в которой хранится созданный пакет. Если папка не указана, используется текущая папка. |
| Свойства | Должно отобразиться в командной строке в последнюю очередь после других параметров. Указывает список свойств, переопределяющих значения в файле проекта. см. раздел [Общие свойства проекта MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) для имен свойств. Аргумент Properties здесь представляет собой список пар token = значение, разделенных точкой с запятой, где каждое вхождение `$token$` в `.nuspec`ном файле будет заменено заданным значением. Значения могут быть строками в кавычках. Обратите внимание, что для свойства "Configuration" значение по умолчанию — "Debug". Чтобы изменить конфигурацию выпуска, используйте `-Properties Configuration=Release`. Как **правило**, свойства должны быть теми же, которые использовались во время соответствующего `nuget build`, чтобы избежать потенциально странного поведения. |
| Суффикс | *(3.4.4 +)* Добавляет суффикс ко внутреннему номеру версии, который обычно используется для присоединения сборки или других идентификаторов предварительной версии. Например, при использовании `-suffix nightly` будет создан пакет с номером версии, например `1.2.3-nightly`. Суффиксы должны начинаться с буквы, чтобы избежать предупреждений, ошибок и потенциальных несовместимости с различными версиями NuGet и диспетчером пакетов NuGet. |
| Символы | Указывает, что пакет содержит источники и символы. При использовании с файлом `.nuspec` создается обычный файл пакета NuGet и соответствующий пакет символов. По умолчанию он создает [устаревший пакет символов](../../create-packages/Symbol-Packages.md). Новый рекомендуемый формат для пакетов символов — .snupkg. См. раздел [Создание пакетов символов (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md). |
| Средство | Указывает, что выходные файлы проекта должны размещаться в папке `tool`. |
| Уровень детализации | Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*. |
| Версия | Переопределяет номер версии из файла `.nuspec`. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Исключение зависимостей разработки

Некоторые пакеты NuGet полезны в качестве зависимостей разработки, которые помогают создавать собственные библиотеки, но не обязательно должны быть реальными зависимостями пакетов.

Команда `pack` пропустит `package` записи в `packages.config`, у которых для атрибута `developmentDependency` задано значение `true`. Эти записи не будут включены в качестве зависимостей в созданный пакет.

Например, рассмотрим следующий файл `packages.config` в исходном проекте:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Для этого проекта пакет, созданный `nuget pack`, будет иметь зависимость от `jQuery` и `microsoft-web-helpers`, но не `netfx-Guard`.

## <a name="suppressing-pack-warnings"></a>Подавление предупреждений о пакете

Хотя рекомендуется разрешать все предупреждения NuGet во время операций с пакетами, в некоторых ситуациях их подавление не гарантируется.

Это можно сделать следующим образом: 

> пакет NuGet. exe Pack. nuspec — Properties не warn = NU5104

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
