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
ms.openlocfilehash: 9ee5dc87ea33b4419bcd9a09751c41b53ae2f70e
ms.sourcegitcommit: a40a6ce6897b2d9411397b2e29b1be234eb6e50c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="3de97-104">команда пакет (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3de97-104">pack command (NuGet CLI)</span></span>

<span data-ttu-id="3de97-105">**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="3de97-105">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="3de97-106">Создает пакет NuGet, на основе указанных `.nuspec` или файла проекта.</span><span class="sxs-lookup"><span data-stu-id="3de97-106">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="3de97-107">`dotnet pack` Команды (см. [dotnet команды](dotnet-Commands.md)) и `msbuild /t:pack` (см. [целевые объекты MSBuild](../reference/msbuild-targets.md)) может использоваться в качестве альтернативы.</span><span class="sxs-lookup"><span data-stu-id="3de97-107">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="3de97-108">В среде Mono создания пакета из файла проекта не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="3de97-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="3de97-109">Вам также потребуется изменить нелокальных путей в `.nuspec` файла в стиле Unix пути, что и для nuget.exe не преобразует имена путей Windows, сам.</span><span class="sxs-lookup"><span data-stu-id="3de97-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="3de97-110">Использование</span><span class="sxs-lookup"><span data-stu-id="3de97-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options]
```

<span data-ttu-id="3de97-111">где `<nuspecPath>` и `<projectPath>` укажите `.nuspec` или файла, проекта соответственно.</span><span class="sxs-lookup"><span data-stu-id="3de97-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="3de97-112">Параметры</span><span class="sxs-lookup"><span data-stu-id="3de97-112">Options</span></span>

| <span data-ttu-id="3de97-113">Параметр</span><span class="sxs-lookup"><span data-stu-id="3de97-113">Option</span></span> | <span data-ttu-id="3de97-114">Описание:</span><span class="sxs-lookup"><span data-stu-id="3de97-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3de97-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="3de97-115">BasePath</span></span> | <span data-ttu-id="3de97-116">Задает базовый путь к файлам, определенным в `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="3de97-116">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="3de97-117">Построить</span><span class="sxs-lookup"><span data-stu-id="3de97-117">Build</span></span> | <span data-ttu-id="3de97-118">Указывает, что проект должен быть создан до начала сборки пакета.</span><span class="sxs-lookup"><span data-stu-id="3de97-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="3de97-119">Исключить</span><span class="sxs-lookup"><span data-stu-id="3de97-119">Exclude</span></span> | <span data-ttu-id="3de97-120">Указывает один или несколько шаблонов подстановочный знак, исключаемый при создании пакета.</span><span class="sxs-lookup"><span data-stu-id="3de97-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="3de97-121">Чтобы указать несколько шаблонов, повторите флаг - исключения.</span><span class="sxs-lookup"><span data-stu-id="3de97-121">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="3de97-122">См. пример ниже.</span><span class="sxs-lookup"><span data-stu-id="3de97-122">See example below.</span></span> |
| <span data-ttu-id="3de97-123">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="3de97-123">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="3de97-124">Предотвращает включение пустых каталогов при построении пакета.</span><span class="sxs-lookup"><span data-stu-id="3de97-124">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="3de97-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3de97-125">ForceEnglishOutput</span></span> | <span data-ttu-id="3de97-126">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="3de97-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3de97-127">Справка</span><span class="sxs-lookup"><span data-stu-id="3de97-127">Help</span></span> | <span data-ttu-id="3de97-128">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="3de97-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="3de97-129">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="3de97-129">IncludeReferencedProjects</span></span> | <span data-ttu-id="3de97-130">Указывает, что встроенный пакет должен включать указанных проектов как зависимости или как часть пакета.</span><span class="sxs-lookup"><span data-stu-id="3de97-130">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="3de97-131">Если проект, на который указывает ссылка имеет соответствующий `.nuspec` файл, который имеет имя, совпадающее с именем проекта, на который указывает ссылка проекта добавляется как элемент dependency.</span><span class="sxs-lookup"><span data-stu-id="3de97-131">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="3de97-132">В противном случае указанный проект добавляется как часть пакета.</span><span class="sxs-lookup"><span data-stu-id="3de97-132">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="3de97-133">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="3de97-133">MinClientVersion</span></span> | <span data-ttu-id="3de97-134">Задать *minClientVersion* атрибут для созданного пакета.</span><span class="sxs-lookup"><span data-stu-id="3de97-134">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="3de97-135">Это значение переопределяет значение существующего *minClientVersion* атрибута (если таковые имеются) в `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="3de97-135">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="3de97-136">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="3de97-136">MSBuildPath</span></span> | <span data-ttu-id="3de97-137">*(4.0 +)*  Указывает путь к MSBuild для команды, переназначает `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="3de97-137">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="3de97-138">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="3de97-138">MSBuildVersion</span></span> | <span data-ttu-id="3de97-139">*(3.2 +)*  Указывает версию MSBuild для использования с помощью этой команды.</span><span class="sxs-lookup"><span data-stu-id="3de97-139">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="3de97-140">Поддерживаемые значения: 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="3de97-140">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="3de97-141">По умолчанию выбирается MSBuild в пути в противном случае по умолчанию наибольшую установленную версию MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3de97-141">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="3de97-142">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="3de97-142">NoDefaultExcludes</span></span> | <span data-ttu-id="3de97-143">По умолчанию при исключении NuGet не позволяет упаковать файлы и файлы и папки, начиная с точки, такие как `.svn` и `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="3de97-143">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="3de97-144">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="3de97-144">NoPackageAnalysis</span></span> | <span data-ttu-id="3de97-145">Указывает, что пакету не нужно запускать анализ пакета после его сборки.</span><span class="sxs-lookup"><span data-stu-id="3de97-145">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="3de97-146">Выходной каталог</span><span class="sxs-lookup"><span data-stu-id="3de97-146">OutputDirectory</span></span> | <span data-ttu-id="3de97-147">Указывает папку, в которой будет храниться созданный пакет.</span><span class="sxs-lookup"><span data-stu-id="3de97-147">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="3de97-148">Если папка не указана, используется текущая папка.</span><span class="sxs-lookup"><span data-stu-id="3de97-148">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="3de97-149">Свойства</span><span class="sxs-lookup"><span data-stu-id="3de97-149">Properties</span></span> | <span data-ttu-id="3de97-150">Указывает список свойств, которые переопределяют значения в файле проекта. в разделе [общие свойства проектов MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) имен свойств.</span><span class="sxs-lookup"><span data-stu-id="3de97-150">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="3de97-151">Аргумент свойства приведен список маркер = пар «значение», разделенных точкой с запятой, где каждое вхождение `$token$` в `.nuspec` заменить файл по заданному значению.</span><span class="sxs-lookup"><span data-stu-id="3de97-151">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="3de97-152">Значения могут быть строк в кавычки.</span><span class="sxs-lookup"><span data-stu-id="3de97-152">Values can be strings in quotation marks.</span></span> <span data-ttu-id="3de97-153">Обратите внимание, что для свойства «Конфигурация» значение по умолчанию — «Debug».</span><span class="sxs-lookup"><span data-stu-id="3de97-153">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="3de97-154">Чтобы изменить конфигурацию выпуска, используйте `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="3de97-154">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="3de97-155">Суффикс</span><span class="sxs-lookup"><span data-stu-id="3de97-155">Suffix</span></span> | <span data-ttu-id="3de97-156">*(3.4.4+)*  Добавляет суффикс для созданного внутреннего номер_версии, обычно используется для добавления сборки или другими идентификаторами предварительного выпуска.</span><span class="sxs-lookup"><span data-stu-id="3de97-156">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="3de97-157">Например, с помощью `-suffix nightly` создаст пакет like номера версии `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="3de97-157">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="3de97-158">Суффиксы должно начинаться с буквы, чтобы избежать предупреждения, ошибки и потенциальных несовместимость с различными версиями NuGet и диспетчер пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="3de97-158">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="3de97-159">Символы</span><span class="sxs-lookup"><span data-stu-id="3de97-159">Symbols</span></span> | <span data-ttu-id="3de97-160">Указывает, что пакет содержит источники и символы.</span><span class="sxs-lookup"><span data-stu-id="3de97-160">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="3de97-161">При использовании с `.nuspec` файла, эта команда создает файл регулярного пакета NuGet и соответствующего пакета символов.</span><span class="sxs-lookup"><span data-stu-id="3de97-161">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="3de97-162">Средство</span><span class="sxs-lookup"><span data-stu-id="3de97-162">Tool</span></span> | <span data-ttu-id="3de97-163">Указывает, что следует поместить выходные файлы проекта в `tool` папки.</span><span class="sxs-lookup"><span data-stu-id="3de97-163">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="3de97-164">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="3de97-164">Verbosity</span></span> | <span data-ttu-id="3de97-165">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="3de97-165">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="3de97-166">Версия</span><span class="sxs-lookup"><span data-stu-id="3de97-166">Version</span></span> | <span data-ttu-id="3de97-167">Переопределяет номером версии из `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="3de97-167">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="3de97-168">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3de97-168">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="3de97-169">Исключение зависимостей разработки</span><span class="sxs-lookup"><span data-stu-id="3de97-169">Excluding development dependencies</span></span>

<span data-ttu-id="3de97-170">Некоторые пакеты NuGet, полезны в качестве зависимости разработки, которые позволяют создавать собственные библиотеки, но не требуется обязательно как зависимости сам пакет.</span><span class="sxs-lookup"><span data-stu-id="3de97-170">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="3de97-171">`pack` Команда будет игнорировать `package` записей в `packages.config` , имеющих `developmentDependency` атрибуту присвоено значение `true`.</span><span class="sxs-lookup"><span data-stu-id="3de97-171">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="3de97-172">Эти записи не будут включены в качестве зависимостей в созданный пакет.</span><span class="sxs-lookup"><span data-stu-id="3de97-172">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="3de97-173">Например, рассмотрим следующие `packages.config` файла исходного проекта:</span><span class="sxs-lookup"><span data-stu-id="3de97-173">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="3de97-174">Для этого проекта путем создания пакета `nuget pack` , имеют зависимость `jQuery` и `microsoft-web-helpers` , но не `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="3de97-174">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="3de97-175">Примеры</span><span class="sxs-lookup"><span data-stu-id="3de97-175">Examples</span></span>

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
