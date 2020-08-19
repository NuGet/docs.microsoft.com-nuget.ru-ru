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
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="3ef62-103">Команда Pack (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="3ef62-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="3ef62-104">Область **применения:** &bullet; **Поддерживаемые версии** для создания пакетов: 2.7 +</span><span class="sxs-lookup"><span data-stu-id="3ef62-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="3ef62-105">Создает пакет NuGet на основе указанного файла [. nuspec](../nuspec.md) или проекта.</span><span class="sxs-lookup"><span data-stu-id="3ef62-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="3ef62-106">`dotnet pack`Команда (см. [команды DotNet](../dotnet-Commands.md)) и `msbuild -t:pack` (см. [целевые объекты MSBuild](../msbuild-targets.md)) могут использоваться в качестве альтернатив.</span><span class="sxs-lookup"><span data-stu-id="3ef62-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="3ef62-107">Используйте [`dotnet pack`](../dotnet-Commands.md) или [`msbuild -t:pack`](../msbuild-targets.md) для проектов на основе [PackageReference](../../consume-packages/package-references-in-project-files.md) .</span><span class="sxs-lookup"><span data-stu-id="3ef62-107">Use [`dotnet pack`](../dotnet-Commands.md) or [`msbuild -t:pack`](../msbuild-targets.md) for [PackageReference](../../consume-packages/package-references-in-project-files.md) based projects.</span></span>
> <span data-ttu-id="3ef62-108">В группе Mono создание пакета из файла проекта не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="3ef62-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="3ef62-109">Кроме того, необходимо изменить нелокальные пути в `.nuspec` файле на пути в стиле UNIX, так как nuget.exe не преобразует пути Windows.</span><span class="sxs-lookup"><span data-stu-id="3ef62-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="3ef62-110">Использование</span><span class="sxs-lookup"><span data-stu-id="3ef62-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="3ef62-111">где `<nuspecPath>` и `<projectPath>` укажите `.nuspec` файл проекта или соответственно.</span><span class="sxs-lookup"><span data-stu-id="3ef62-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="3ef62-112">Параметры</span><span class="sxs-lookup"><span data-stu-id="3ef62-112">Options</span></span>
- **`-BasePath`**

   <span data-ttu-id="3ef62-113">Задает базовый путь к файлам, определенным в файле [nuspec](../nuspec.md) .</span><span class="sxs-lookup"><span data-stu-id="3ef62-113">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span>

- **`-Build`**

  <span data-ttu-id="3ef62-114">Указывает, что проект должен быть построен перед построением пакета.</span><span class="sxs-lookup"><span data-stu-id="3ef62-114">Specifies that the project should be built before building the package.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="3ef62-115">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="3ef62-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3ef62-116">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="3ef62-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Exclude`**

  <span data-ttu-id="3ef62-117">Задает шаблоны с подстановочными знаками, исключаемые при создании пакета.</span><span class="sxs-lookup"><span data-stu-id="3ef62-117">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="3ef62-118">Чтобы указать более одного шаблона, повторите флаг-Exclude.</span><span class="sxs-lookup"><span data-stu-id="3ef62-118">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="3ef62-119">См. пример ниже.</span><span class="sxs-lookup"><span data-stu-id="3ef62-119">See example below.</span></span>

- **`-ExcludeEmptyDirectories`**

  <span data-ttu-id="3ef62-120">Предотвращает включение пустых каталогов при сборке пакета.</span><span class="sxs-lookup"><span data-stu-id="3ef62-120">Prevents inclusion of empty directories when building the package.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="3ef62-121">*(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="3ef62-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="3ef62-122">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="3ef62-122">Displays help information for the command.</span></span>

- **`-IncludeReferencedProjects`**

  <span data-ttu-id="3ef62-123">Указывает, что построенный пакет должен включать проекты, на которые указывают ссылки, либо как зависимости, либо как часть пакета.</span><span class="sxs-lookup"><span data-stu-id="3ef62-123">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="3ef62-124">Если проект, на который указывает ссылка, имеет соответствующий `.nuspec` файл, имя которого совпадает с именем проекта, то указанный проект добавляется как зависимость.</span><span class="sxs-lookup"><span data-stu-id="3ef62-124">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="3ef62-125">В противном случае проект, на который указывает ссылка, добавляется как часть пакета.</span><span class="sxs-lookup"><span data-stu-id="3ef62-125">Otherwise, the referenced project is added as part of the package.</span></span>

- **`-InstallPackageToOutputPath`**

  <span data-ttu-id="3ef62-126">Укажите, должна ли команда подготовить выходной каталог пакета для поддержки общего доступа к веб-каналу.</span><span class="sxs-lookup"><span data-stu-id="3ef62-126">Specify if the command should prepare the package output directory to support share as feed.</span></span>

- **`-MinClientVersion`**

  <span data-ttu-id="3ef62-127">Задайте атрибут *minClientVersion* для созданного пакета.</span><span class="sxs-lookup"><span data-stu-id="3ef62-127">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="3ef62-128">Это значение переопределит значение существующего атрибута *minClientVersion* (если он есть) в `.nuspec` файле.</span><span class="sxs-lookup"><span data-stu-id="3ef62-128">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="3ef62-129">*(4.0 +)* Указывает путь MSBuild для использования с командой, который имеет приоритет над `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="3ef62-129">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="3ef62-130">*(3.2 +)* Указывает версию MSBuild, которая будет использоваться с этой командой.</span><span class="sxs-lookup"><span data-stu-id="3ef62-130">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="3ef62-131">Поддерживаемые значения: 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="3ef62-131">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="3ef62-132">По умолчанию в пути выбирается MSBuild, в противном случае — по умолчанию — самая высокая установленная версия MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3ef62-132">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoDefaultExcludes`**

  <span data-ttu-id="3ef62-133">Предотвращает исключение по умолчанию для файлов пакетов NuGet и файлов и папок, начинающихся с точки, например `.svn` и `.gitignore` .</span><span class="sxs-lookup"><span data-stu-id="3ef62-133">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="3ef62-134">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="3ef62-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoPackageAnalysis`**

  <span data-ttu-id="3ef62-135">Указывает, что пакету не нужно запускать анализ пакета после его сборки.</span><span class="sxs-lookup"><span data-stu-id="3ef62-135">Specifies that pack should not run package analysis after building the package.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="3ef62-136">Указывает папку, в которой хранится созданный пакет.</span><span class="sxs-lookup"><span data-stu-id="3ef62-136">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="3ef62-137">Если папка не указана, используется текущая папка.</span><span class="sxs-lookup"><span data-stu-id="3ef62-137">If no folder is specified, the current folder is used.</span></span>

- **`-OutputFileNamesWithoutVersion`**

  <span data-ttu-id="3ef62-138">Укажите, должна ли команда подготовить имя выхода пакета без версии.</span><span class="sxs-lookup"><span data-stu-id="3ef62-138">Specify if the command should prepare the package output name without the version.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="3ef62-139">Указывает папку Packages.</span><span class="sxs-lookup"><span data-stu-id="3ef62-139">Specifies the packages folder.</span></span>

- **`-p|-Properties`**

  <span data-ttu-id="3ef62-140">Должно отобразиться в командной строке в последнюю очередь после других параметров.</span><span class="sxs-lookup"><span data-stu-id="3ef62-140">Should appear last on the command line after other options.</span></span> <span data-ttu-id="3ef62-141">Указывает список свойств, переопределяющих значения в файле проекта. см. раздел [Общие свойства проекта MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) для имен свойств.</span><span class="sxs-lookup"><span data-stu-id="3ef62-141">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="3ef62-142">Аргумент Properties здесь представляет собой список пар token = значение, разделенных точкой с запятой, где каждое вхождение `$token$` в `.nuspec` файле будет заменено заданным значением.</span><span class="sxs-lookup"><span data-stu-id="3ef62-142">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="3ef62-143">Значения могут быть строками в кавычках.</span><span class="sxs-lookup"><span data-stu-id="3ef62-143">Values can be strings in quotation marks.</span></span> <span data-ttu-id="3ef62-144">Обратите внимание, что для свойства "Configuration" значение по умолчанию — "Debug".</span><span class="sxs-lookup"><span data-stu-id="3ef62-144">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="3ef62-145">Чтобы изменить конфигурацию выпуска, используйте `-Properties Configuration=Release` .</span><span class="sxs-lookup"><span data-stu-id="3ef62-145">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> <span data-ttu-id="3ef62-146">Как **правило**, свойства должны быть теми же, которые использовались во время соответствующей сборки проекта, чтобы избежать потенциально странного поведения.</span><span class="sxs-lookup"><span data-stu-id="3ef62-146">**In general**, Properties should be the same that were used during the corresponding project build, in order to avoid potentially strange behavior.</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="3ef62-147">Указывает каталог решения.</span><span class="sxs-lookup"><span data-stu-id="3ef62-147">Specifies the solution directory.</span></span>

- **`-Suffix`**

  <span data-ttu-id="3ef62-148">*(3.4.4 +)* Добавляет суффикс ко внутреннему номеру версии, который обычно используется для присоединения сборки или других идентификаторов предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="3ef62-148">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="3ef62-149">Например, при использовании `-suffix nightly` будет создан пакет с номером версии, например `1.2.3-nightly` .</span><span class="sxs-lookup"><span data-stu-id="3ef62-149">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="3ef62-150">Суффиксы должны начинаться с буквы, чтобы избежать предупреждений, ошибок и потенциальных несовместимости с различными версиями NuGet и диспетчером пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="3ef62-150">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span>

- **`-SymbolPackageFormat`**

  <span data-ttu-id="3ef62-151">При создании пакета символов позволяет выбрать `snupkg` `symbols.nupkg` Формат и.</span><span class="sxs-lookup"><span data-stu-id="3ef62-151">When creating a symbols package, allows to choose between the `snupkg` and `symbols.nupkg` format.</span></span>

- **`-Symbols`**

  <span data-ttu-id="3ef62-152">Указывает, что пакет содержит источники и символы.</span><span class="sxs-lookup"><span data-stu-id="3ef62-152">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="3ef62-153">При использовании с `.nuspec` файлом он создает обычный файл пакета NuGet и соответствующий пакет символов.</span><span class="sxs-lookup"><span data-stu-id="3ef62-153">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="3ef62-154">По умолчанию он создает [устаревший пакет символов](../../create-packages/Symbol-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="3ef62-154">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="3ef62-155">Новый рекомендуемый формат для пакетов символов — .snupkg.</span><span class="sxs-lookup"><span data-stu-id="3ef62-155">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="3ef62-156">См. раздел [Создание пакетов символов (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="3ef62-156">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span>

- **`-Tool`**

   <span data-ttu-id="3ef62-157">Указывает, что выходные файлы проекта должны быть помещены в `tool` папку.</span><span class="sxs-lookup"><span data-stu-id="3ef62-157">Specifies that the output files of the project should be placed in the `tool` folder.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="3ef62-158">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="3ef62-158">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="3ef62-159">Переопределяет номер версии из `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="3ef62-159">Overrides the version number from the `.nuspec` file.</span></span>

<span data-ttu-id="3ef62-160">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3ef62-160">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="3ef62-161">Исключение зависимостей разработки</span><span class="sxs-lookup"><span data-stu-id="3ef62-161">Excluding development dependencies</span></span>

<span data-ttu-id="3ef62-162">Некоторые пакеты NuGet полезны в качестве зависимостей разработки, которые помогают создавать собственные библиотеки, но не обязательно должны быть реальными зависимостями пакетов.</span><span class="sxs-lookup"><span data-stu-id="3ef62-162">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="3ef62-163">`pack`Команда будет игнорировать `package` записи в `packages.config` , для которых `developmentDependency` атрибуту присвоено значение `true` .</span><span class="sxs-lookup"><span data-stu-id="3ef62-163">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="3ef62-164">Эти записи не будут включены в качестве зависимостей в созданный пакет.</span><span class="sxs-lookup"><span data-stu-id="3ef62-164">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="3ef62-165">Например, рассмотрим следующий `packages.config` файл в исходном проекте:</span><span class="sxs-lookup"><span data-stu-id="3ef62-165">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="3ef62-166">Для этого проекта пакет, созданный, `nuget pack` будет иметь зависимость от `jQuery` и, `microsoft-web-helpers` но не `netfx-Guard` .</span><span class="sxs-lookup"><span data-stu-id="3ef62-166">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="suppressing-pack-warnings"></a><span data-ttu-id="3ef62-167">Подавление предупреждений о пакете</span><span class="sxs-lookup"><span data-stu-id="3ef62-167">Suppressing pack warnings</span></span>

<span data-ttu-id="3ef62-168">Хотя рекомендуется разрешать все предупреждения NuGet во время операций с пакетами, в некоторых ситуациях их подавление не гарантируется.</span><span class="sxs-lookup"><span data-stu-id="3ef62-168">While it is recommended that you resolve all NuGet warnings during your pack operations, in certain situations suppressing them is warranted.</span></span>

<span data-ttu-id="3ef62-169">Это можно сделать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3ef62-169">You can achieve that in the following way:</span></span> 

> <span data-ttu-id="3ef62-170">Пакет nuget.exe пакета. nuspec-Properties не warn = NU5104</span><span class="sxs-lookup"><span data-stu-id="3ef62-170">nuget.exe pack package.nuspec -Properties NoWarn=NU5104</span></span>

## <a name="examples"></a><span data-ttu-id="3ef62-171">Примеры</span><span class="sxs-lookup"><span data-stu-id="3ef62-171">Examples</span></span>

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
