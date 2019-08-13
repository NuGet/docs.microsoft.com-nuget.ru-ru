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
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="eaaae-103">Команда pack (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="eaaae-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="eaaae-104">Область **применения:** &bullet; **Поддерживаемые версии** для создания пакетов: 2.7+</span><span class="sxs-lookup"><span data-stu-id="eaaae-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="eaaae-105">Создает пакет NuGet на основе указанного файла [. nuspec](../nuspec.md) или проекта.</span><span class="sxs-lookup"><span data-stu-id="eaaae-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="eaaae-106">Команда (см. [команды DotNet](../dotnet-Commands.md)) и `msbuild -t:pack` (см. [целевые объекты MSBuild](../msbuild-targets.md)) могут использоваться в качестве альтернатив. `dotnet pack`</span><span class="sxs-lookup"><span data-stu-id="eaaae-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="eaaae-107">В группе Mono создание пакета из файла проекта не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="eaaae-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="eaaae-108">Кроме того, необходимо изменить нелокальные пути в `.nuspec` файле на пути в стиле UNIX, так как NuGet. exe не преобразует сами пути Windows.</span><span class="sxs-lookup"><span data-stu-id="eaaae-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="eaaae-109">Использование</span><span class="sxs-lookup"><span data-stu-id="eaaae-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="eaaae-110">где `<nuspecPath>` и `<projectPath>` укажите`.nuspec` файл проекта или соответственно.</span><span class="sxs-lookup"><span data-stu-id="eaaae-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="eaaae-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="eaaae-111">Options</span></span>

| <span data-ttu-id="eaaae-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="eaaae-112">Option</span></span> | <span data-ttu-id="eaaae-113">Описание</span><span class="sxs-lookup"><span data-stu-id="eaaae-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eaaae-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="eaaae-114">BasePath</span></span> | <span data-ttu-id="eaaae-115">Задает базовый путь к файлам, определенным в файле [nuspec](../nuspec.md) .</span><span class="sxs-lookup"><span data-stu-id="eaaae-115">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span> |
| <span data-ttu-id="eaaae-116">Построить</span><span class="sxs-lookup"><span data-stu-id="eaaae-116">Build</span></span> | <span data-ttu-id="eaaae-117">Указывает, что проект должен быть построен перед построением пакета.</span><span class="sxs-lookup"><span data-stu-id="eaaae-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="eaaae-118">Исключить</span><span class="sxs-lookup"><span data-stu-id="eaaae-118">Exclude</span></span> | <span data-ttu-id="eaaae-119">Задает шаблоны с подстановочными знаками, исключаемые при создании пакета.</span><span class="sxs-lookup"><span data-stu-id="eaaae-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="eaaae-120">Чтобы указать более одного шаблона, повторите флаг-Exclude.</span><span class="sxs-lookup"><span data-stu-id="eaaae-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="eaaae-121">См. пример ниже.</span><span class="sxs-lookup"><span data-stu-id="eaaae-121">See example below.</span></span> |
| <span data-ttu-id="eaaae-122">ексклудимптидиректориес</span><span class="sxs-lookup"><span data-stu-id="eaaae-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="eaaae-123">Предотвращает включение пустых каталогов при сборке пакета.</span><span class="sxs-lookup"><span data-stu-id="eaaae-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="eaaae-124">форцеенглишаутпут</span><span class="sxs-lookup"><span data-stu-id="eaaae-124">ForceEnglishOutput</span></span> | <span data-ttu-id="eaaae-125">*(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="eaaae-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="eaaae-126">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="eaaae-126">ConfigFile</span></span> | <span data-ttu-id="eaaae-127">Укажите файл конфигурации для команды Pack.</span><span class="sxs-lookup"><span data-stu-id="eaaae-127">Specify the configuration file for the pack command.</span></span> |
| <span data-ttu-id="eaaae-128">Help</span><span class="sxs-lookup"><span data-stu-id="eaaae-128">Help</span></span> | <span data-ttu-id="eaaae-129">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="eaaae-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="eaaae-130">инклудереференцедпрожектс</span><span class="sxs-lookup"><span data-stu-id="eaaae-130">IncludeReferencedProjects</span></span> | <span data-ttu-id="eaaae-131">Указывает, что построенный пакет должен включать проекты, на которые указывают ссылки, либо как зависимости, либо как часть пакета.</span><span class="sxs-lookup"><span data-stu-id="eaaae-131">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="eaaae-132">Если проект, на который указывает ссылка `.nuspec` , имеет соответствующий файл, имя которого совпадает с именем проекта, то указанный проект добавляется как зависимость.</span><span class="sxs-lookup"><span data-stu-id="eaaae-132">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="eaaae-133">В противном случае проект, на который указывает ссылка, добавляется как часть пакета.</span><span class="sxs-lookup"><span data-stu-id="eaaae-133">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="eaaae-134">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="eaaae-134">MinClientVersion</span></span> | <span data-ttu-id="eaaae-135">Задайте атрибут *minClientVersion* для созданного пакета.</span><span class="sxs-lookup"><span data-stu-id="eaaae-135">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="eaaae-136">Это значение переопределит значение существующего атрибута *minClientVersion* (если он есть) в `.nuspec` файле.</span><span class="sxs-lookup"><span data-stu-id="eaaae-136">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="eaaae-137">мсбуилдпас</span><span class="sxs-lookup"><span data-stu-id="eaaae-137">MSBuildPath</span></span> | <span data-ttu-id="eaaae-138">*(4.0 +)* Указывает путь MSBuild для использования с командой, который имеет приоритет над `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="eaaae-138">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="eaaae-139">мсбуилдверсион</span><span class="sxs-lookup"><span data-stu-id="eaaae-139">MSBuildVersion</span></span> | <span data-ttu-id="eaaae-140">*(3.2 +)* Указывает версию MSBuild, которая будет использоваться с этой командой.</span><span class="sxs-lookup"><span data-stu-id="eaaae-140">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="eaaae-141">Поддерживаемые значения: 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="eaaae-141">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="eaaae-142">По умолчанию в пути выбирается MSBuild, в противном случае — по умолчанию — самая высокая установленная версия MSBuild.</span><span class="sxs-lookup"><span data-stu-id="eaaae-142">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="eaaae-143">нодефаултексклудес</span><span class="sxs-lookup"><span data-stu-id="eaaae-143">NoDefaultExcludes</span></span> | <span data-ttu-id="eaaae-144">Предотвращает исключение по умолчанию для файлов пакетов NuGet и файлов и папок, начинающихся с точки `.svn` , `.gitignore`например и.</span><span class="sxs-lookup"><span data-stu-id="eaaae-144">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="eaaae-145">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="eaaae-145">NoPackageAnalysis</span></span> | <span data-ttu-id="eaaae-146">Указывает, что пакету не нужно запускать анализ пакета после его сборки.</span><span class="sxs-lookup"><span data-stu-id="eaaae-146">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="eaaae-147">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="eaaae-147">OutputDirectory</span></span> | <span data-ttu-id="eaaae-148">Указывает папку, в которой хранится созданный пакет.</span><span class="sxs-lookup"><span data-stu-id="eaaae-148">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="eaaae-149">Если папка не указана, используется текущая папка.</span><span class="sxs-lookup"><span data-stu-id="eaaae-149">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="eaaae-150">Свойства</span><span class="sxs-lookup"><span data-stu-id="eaaae-150">Properties</span></span> | <span data-ttu-id="eaaae-151">Должно отобразиться в командной строке в последнюю очередь после других параметров.</span><span class="sxs-lookup"><span data-stu-id="eaaae-151">Should appear last on the command line after other options.</span></span> <span data-ttu-id="eaaae-152">Указывает список свойств, переопределяющих значения в файле проекта. см. раздел [Общие свойства проекта MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) для имен свойств.</span><span class="sxs-lookup"><span data-stu-id="eaaae-152">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="eaaae-153">Аргумент Properties здесь представляет собой список пар token = значение, разделенных точкой с запятой, где каждое вхождение `$token$` `.nuspec` в файле будет заменено заданным значением.</span><span class="sxs-lookup"><span data-stu-id="eaaae-153">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="eaaae-154">Значения могут быть строками в кавычках.</span><span class="sxs-lookup"><span data-stu-id="eaaae-154">Values can be strings in quotation marks.</span></span> <span data-ttu-id="eaaae-155">Обратите внимание, что для свойства "Configuration" значение по умолчанию — "Debug".</span><span class="sxs-lookup"><span data-stu-id="eaaae-155">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="eaaae-156">Чтобы изменить конфигурацию выпуска, используйте `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="eaaae-156">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="eaaae-157">Суффикс</span><span class="sxs-lookup"><span data-stu-id="eaaae-157">Suffix</span></span> | <span data-ttu-id="eaaae-158">*(3.4.4 +)* Добавляет суффикс ко внутреннему номеру версии, который обычно используется для присоединения сборки или других идентификаторов предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="eaaae-158">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="eaaae-159">Например, при использовании `-suffix nightly` будет создан пакет с номером версии, например. `1.2.3-nightly`</span><span class="sxs-lookup"><span data-stu-id="eaaae-159">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="eaaae-160">Суффиксы должны начинаться с буквы, чтобы избежать предупреждений, ошибок и потенциальных несовместимости с различными версиями NuGet и диспетчером пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="eaaae-160">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="eaaae-161">Символы</span><span class="sxs-lookup"><span data-stu-id="eaaae-161">Symbols</span></span> | <span data-ttu-id="eaaae-162">Указывает, что пакет содержит источники и символы.</span><span class="sxs-lookup"><span data-stu-id="eaaae-162">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="eaaae-163">При использовании с `.nuspec` файлом он создает обычный файл пакета NuGet и соответствующий пакет символов.</span><span class="sxs-lookup"><span data-stu-id="eaaae-163">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="eaaae-164">По умолчанию он создает [устаревший пакет символов](../../create-packages/Symbol-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="eaaae-164">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="eaaae-165">Новый рекомендуемый формат для пакетов символов — .snupkg.</span><span class="sxs-lookup"><span data-stu-id="eaaae-165">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="eaaae-166">См. раздел [Создание пакетов символов (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="eaaae-166">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span> |
| <span data-ttu-id="eaaae-167">Средство</span><span class="sxs-lookup"><span data-stu-id="eaaae-167">Tool</span></span> | <span data-ttu-id="eaaae-168">Указывает, что выходные файлы проекта должны быть помещены в `tool` папку.</span><span class="sxs-lookup"><span data-stu-id="eaaae-168">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="eaaae-169">Verbosity</span><span class="sxs-lookup"><span data-stu-id="eaaae-169">Verbosity</span></span> | <span data-ttu-id="eaaae-170">Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*.</span><span class="sxs-lookup"><span data-stu-id="eaaae-170">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="eaaae-171">Версия</span><span class="sxs-lookup"><span data-stu-id="eaaae-171">Version</span></span> | <span data-ttu-id="eaaae-172">Переопределяет номер версии из `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="eaaae-172">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="eaaae-173">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="eaaae-173">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="eaaae-174">Исключение зависимостей разработки</span><span class="sxs-lookup"><span data-stu-id="eaaae-174">Excluding development dependencies</span></span>

<span data-ttu-id="eaaae-175">Некоторые пакеты NuGet полезны в качестве зависимостей разработки, которые помогают создавать собственные библиотеки, но не обязательно должны быть реальными зависимостями пакетов.</span><span class="sxs-lookup"><span data-stu-id="eaaae-175">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="eaaae-176">`package` Командабудет`packages.config` игнорировать записив`true`, для которых атрибутуприсвоенозначение.`developmentDependency` `pack`</span><span class="sxs-lookup"><span data-stu-id="eaaae-176">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="eaaae-177">Эти записи не будут включены в качестве зависимостей в созданный пакет.</span><span class="sxs-lookup"><span data-stu-id="eaaae-177">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="eaaae-178">Например, рассмотрим следующий `packages.config` файл в исходном проекте:</span><span class="sxs-lookup"><span data-stu-id="eaaae-178">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="eaaae-179">Для этого проекта пакет, созданный `nuget pack` , будет иметь зависимость от `jQuery` и, `microsoft-web-helpers` но не `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="eaaae-179">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="eaaae-180">Примеры</span><span class="sxs-lookup"><span data-stu-id="eaaae-180">Examples</span></span>

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
