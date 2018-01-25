---
title: "Команда пакет NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Справочник по командной пакет nuget.exe"
keywords: "ссылка на пакет NuGet, команда пакета"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 732a712f88c6267caae361673a05af0781877cf4
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="pack-command-nuget-cli"></a>команда пакет (NuGet CLI)

**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** 2.7 +

Создает пакет NuGet, на основе указанных `.nuspec` или файла проекта. `dotnet pack` Команды (см. [dotnet команды](dotnet-Commands.md)) и `msbuild /t:pack` (см. [целевые объекты MSBuild](../schema/msbuild-targets.md)) может использоваться в качестве альтернативы.

> [!Important]
> В среде Mono создания пакета из файла проекта не поддерживается. Вам также потребуется изменить нелокальных путей в `.nuspec` файла в стиле Unix пути, что и для nuget.exe не преобразует имена путей Windows, сам.

## <a name="usage"></a>Использование

```cli
nuget pack <nuspecPath | projectPath> [options]
```

где `<nuspecPath>` и `<projectPath>` укажите `.nuspec` или файла, проекта соответственно.

## <a name="options"></a>Параметры

| Параметр | Описание: |
| --- | --- |
| BasePath | Задает базовый путь к файлам, определенным в `.nuspec` файла. |
| Построить | Указывает, что проект должен быть создан до начала сборки пакета. |
| Исключить | Указывает один или несколько шаблонов подстановочный знак, исключаемый при создании пакета. Чтобы указать несколько шаблонов, повторите флаг - исключения. См. пример ниже. |
| ExcludeEmptyDirectories | Предотвращает включение пустых каталогов при построении пакета. |
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Справка | Отображает справку по команде. |
| IncludeReferencedProjects | Указывает, что встроенный пакет должен включать указанных проектов как зависимости или как часть пакета. Если проект, на который указывает ссылка имеет соответствующий `.nuspec` файл, который имеет имя, совпадающее с именем проекта, на который указывает ссылка проекта добавляется как элемент dependency. В противном случае указанный проект добавляется как часть пакета. |
| MinClientVersion | Задать *minClientVersion* атрибут для созданного пакета. Это значение переопределяет значение существующего *minClientVersion* атрибута (если таковые имеются) в `.nuspec` файла. |
| MSBuildPath | *(4.0 +)*  Указывает путь к MSBuild для команды, переназначает `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Указывает версию MSBuild для использования с помощью этой команды. Поддерживаемые значения: 4, 12, 14, 15. По умолчанию выбирается MSBuild в пути в противном случае по умолчанию наибольшую установленную версию MSBuild. |
| NoDefaultExcludes | По умолчанию при исключении NuGet не позволяет упаковать файлы и файлы и папки, начиная с точки, такие как `.svn` и `.gitignore`. |
| NoPackageAnalysis | Указывает, что пакету не нужно запускать анализ пакета после его сборки. |
| Выходной каталог | Указывает папку, в которой будет храниться созданный пакет. Если папка не указана, используется текущая папка. |
| Свойства | Указывает список свойств, которые переопределяют значения в файле проекта. в разделе [общие свойства проектов MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) имен свойств. Аргумент свойства приведен список маркер = пар «значение», разделенных точкой с запятой, где каждое вхождение `$token$` в `.nuspec` заменить файл по заданному значению. Значения могут быть строк в кавычки. Обратите внимание, что для свойства «Конфигурация» значение по умолчанию — «Debug». Чтобы изменить конфигурацию выпуска, используйте `-Properties Configuration=Release`. |
| Суффикс | *(3.4.4+)*  Добавляет суффикс для созданного внутреннего номер_версии, обычно используется для добавления сборки или другими идентификаторами предварительного выпуска. Например, с помощью `-suffix nightly` создаст пакет like номера версии `1.2.3-nightly`. Суффиксы должно начинаться с буквы, чтобы избежать предупреждения, ошибки и потенциальных несовместимость с различными версиями NuGet и диспетчер пакетов NuGet. |
| Символы | Указывает, что пакет содержит источники и символы. При использовании с `.nuspec` файла, эта команда создает файл регулярного пакета NuGet и соответствующего пакета символов. |
| Средство | Указывает, что следует поместить выходные файлы проекта в `tool` папки. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*. |
| Версия | Переопределяет номером версии из `.nuspec` файла. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Исключение зависимостей разработки

Некоторые пакеты NuGet, полезны в качестве зависимости разработки, которые позволяют создавать собственные библиотеки, но не требуется обязательно как зависимости сам пакет.

`pack` Команда будет игнорировать `package` записей в `packages.config` , имеющих `developmentDependency` атрибуту присвоено значение `true`. Эти записи не будут включены в качестве зависимостей в созданный пакет.

Например, рассмотрим следующие `packages.config` файла исходного проекта:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Для этого проекта путем создания пакета `nuget pack` , имеют зависимость `jQuery` и `microsoft-web-helpers` , но не `netfx-Guard`.

## <a name="examples"></a>Примеры

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
