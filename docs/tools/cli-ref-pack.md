---
title: Команда пакет NuGet CLI
description: Справочник по командной пакет nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a2468b099a822e69298ea78c80cfd1d5d5c09938
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="4eaf8-103">Команда pack (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4eaf8-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="4eaf8-104">**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="4eaf8-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="4eaf8-105">Создает пакет NuGet, на основе указанных `.nuspec` или файла проекта.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-105">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="4eaf8-106">`dotnet pack` Команды (см. [dotnet команды](dotnet-Commands.md)) и `msbuild /t:pack` (см. [целевые объекты MSBuild](../reference/msbuild-targets.md)) может использоваться в качестве альтернативы.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-106">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="4eaf8-107">В среде Mono создания пакета из файла проекта не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="4eaf8-108">Вам также потребуется изменить нелокальных путей в `.nuspec` файла в стиле Unix пути, что и для nuget.exe не преобразует имена путей Windows, сам.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="4eaf8-109">Использование</span><span class="sxs-lookup"><span data-stu-id="4eaf8-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="4eaf8-110">где `<nuspecPath>` и `<projectPath>` укажите `.nuspec` или файла, проекта соответственно.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="4eaf8-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="4eaf8-111">Options</span></span>

| <span data-ttu-id="4eaf8-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="4eaf8-112">Option</span></span> | <span data-ttu-id="4eaf8-113">Описание</span><span class="sxs-lookup"><span data-stu-id="4eaf8-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4eaf8-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="4eaf8-114">BasePath</span></span> | <span data-ttu-id="4eaf8-115">Задает базовый путь к файлам, определенным в `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-115">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="4eaf8-116">Построить</span><span class="sxs-lookup"><span data-stu-id="4eaf8-116">Build</span></span> | <span data-ttu-id="4eaf8-117">Указывает, что проект должен быть создан до начала сборки пакета.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="4eaf8-118">Исключить</span><span class="sxs-lookup"><span data-stu-id="4eaf8-118">Exclude</span></span> | <span data-ttu-id="4eaf8-119">Указывает один или несколько шаблонов подстановочный знак, исключаемый при создании пакета.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="4eaf8-120">Чтобы указать несколько шаблонов, повторите флаг - исключения.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="4eaf8-121">См. пример ниже.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-121">See example below.</span></span> |
| <span data-ttu-id="4eaf8-122">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="4eaf8-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="4eaf8-123">Предотвращает включение пустых каталогов при построении пакета.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="4eaf8-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4eaf8-124">ForceEnglishOutput</span></span> | <span data-ttu-id="4eaf8-125">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4eaf8-126">Справка</span><span class="sxs-lookup"><span data-stu-id="4eaf8-126">Help</span></span> | <span data-ttu-id="4eaf8-127">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-127">Displays help information for the command.</span></span> |
| <span data-ttu-id="4eaf8-128">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="4eaf8-128">IncludeReferencedProjects</span></span> | <span data-ttu-id="4eaf8-129">Указывает, что встроенный пакет должен включать указанных проектов как зависимости или как часть пакета.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-129">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="4eaf8-130">Если проект, на который указывает ссылка имеет соответствующий `.nuspec` файл, который имеет имя, совпадающее с именем проекта, на который указывает ссылка проекта добавляется как элемент dependency.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-130">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="4eaf8-131">В противном случае указанный проект добавляется как часть пакета.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-131">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="4eaf8-132">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="4eaf8-132">MinClientVersion</span></span> | <span data-ttu-id="4eaf8-133">Задать *minClientVersion* атрибут для созданного пакета.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-133">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="4eaf8-134">Это значение переопределяет значение существующего *minClientVersion* атрибута (если таковые имеются) в `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-134">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="4eaf8-135">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="4eaf8-135">MSBuildPath</span></span> | <span data-ttu-id="4eaf8-136">*(4.0 +)*  Указывает путь к MSBuild для команды, переназначает `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-136">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="4eaf8-137">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="4eaf8-137">MSBuildVersion</span></span> | <span data-ttu-id="4eaf8-138">*(3.2 +)*  Указывает версию MSBuild для использования с помощью этой команды.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-138">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="4eaf8-139">Поддерживаемые значения: 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-139">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="4eaf8-140">По умолчанию выбирается MSBuild в пути в противном случае по умолчанию наибольшую установленную версию MSBuild.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-140">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="4eaf8-141">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="4eaf8-141">NoDefaultExcludes</span></span> | <span data-ttu-id="4eaf8-142">По умолчанию при исключении NuGet не позволяет упаковать файлы и файлы и папки, начиная с точки, такие как `.svn` и `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-142">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="4eaf8-143">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="4eaf8-143">NoPackageAnalysis</span></span> | <span data-ttu-id="4eaf8-144">Указывает, что пакету не нужно запускать анализ пакета после его сборки.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-144">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="4eaf8-145">Выходной каталог</span><span class="sxs-lookup"><span data-stu-id="4eaf8-145">OutputDirectory</span></span> | <span data-ttu-id="4eaf8-146">Указывает папку, в которой будет храниться созданный пакет.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-146">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="4eaf8-147">Если папка не указана, используется текущая папка.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-147">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="4eaf8-148">Свойства</span><span class="sxs-lookup"><span data-stu-id="4eaf8-148">Properties</span></span> | <span data-ttu-id="4eaf8-149">Должны появиться последнего в командной строке после других параметров.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-149">Should appear last on the command line after other options.</span></span> <span data-ttu-id="4eaf8-150">Указывает список свойств, которые переопределяют значения в файле проекта. в разделе [общие свойства проектов MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) имен свойств.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-150">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="4eaf8-151">Аргумент свойства приведен список маркер = пар «значение», разделенных точкой с запятой, где каждое вхождение `$token$` в `.nuspec` заменить файл по заданному значению.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-151">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="4eaf8-152">Значения могут быть строк в кавычки.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-152">Values can be strings in quotation marks.</span></span> <span data-ttu-id="4eaf8-153">Обратите внимание, что для свойства «Конфигурация» значение по умолчанию — «Debug».</span><span class="sxs-lookup"><span data-stu-id="4eaf8-153">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="4eaf8-154">Чтобы изменить конфигурацию выпуска, используйте `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-154">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="4eaf8-155">Суффикс</span><span class="sxs-lookup"><span data-stu-id="4eaf8-155">Suffix</span></span> | <span data-ttu-id="4eaf8-156">*(3.4.4+)*  Добавляет суффикс для созданного внутреннего номер_версии, обычно используется для добавления сборки или другими идентификаторами предварительного выпуска.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-156">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="4eaf8-157">Например, с помощью `-suffix nightly` создаст пакет like номера версии `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-157">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="4eaf8-158">Суффиксы должно начинаться с буквы, чтобы избежать предупреждения, ошибки и потенциальных несовместимость с различными версиями NuGet и диспетчер пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-158">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="4eaf8-159">Символы</span><span class="sxs-lookup"><span data-stu-id="4eaf8-159">Symbols</span></span> | <span data-ttu-id="4eaf8-160">Указывает, что пакет содержит источники и символы.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-160">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="4eaf8-161">При использовании с `.nuspec` файла, эта команда создает файл регулярного пакета NuGet и соответствующего пакета символов.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-161">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="4eaf8-162">Средство</span><span class="sxs-lookup"><span data-stu-id="4eaf8-162">Tool</span></span> | <span data-ttu-id="4eaf8-163">Указывает, что следует поместить выходные файлы проекта в `tool` папки.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-163">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="4eaf8-164">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="4eaf8-164">Verbosity</span></span> | <span data-ttu-id="4eaf8-165">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-165">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="4eaf8-166">Версия</span><span class="sxs-lookup"><span data-stu-id="4eaf8-166">Version</span></span> | <span data-ttu-id="4eaf8-167">Переопределяет номером версии из `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-167">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="4eaf8-168">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4eaf8-168">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="4eaf8-169">Исключение зависимостей разработки</span><span class="sxs-lookup"><span data-stu-id="4eaf8-169">Excluding development dependencies</span></span>

<span data-ttu-id="4eaf8-170">Некоторые пакеты NuGet, полезны в качестве зависимости разработки, которые позволяют создавать собственные библиотеки, но не требуется обязательно как зависимости сам пакет.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-170">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="4eaf8-171">`pack` Команда будет игнорировать `package` записей в `packages.config` , имеющих `developmentDependency` атрибуту присвоено значение `true`.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-171">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="4eaf8-172">Эти записи не будут включены в качестве зависимостей в созданный пакет.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-172">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="4eaf8-173">Например, рассмотрим следующие `packages.config` файла исходного проекта:</span><span class="sxs-lookup"><span data-stu-id="4eaf8-173">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="4eaf8-174">Для этого проекта путем создания пакета `nuget pack` , имеют зависимость `jQuery` и `microsoft-web-helpers` , но не `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="4eaf8-174">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="4eaf8-175">Примеры</span><span class="sxs-lookup"><span data-stu-id="4eaf8-175">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```