---
title: Команда интерфейса командной строки NuGet pack
description: Справочник по командам пакет nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: db236b0eaac34ca9f6f67fd15ca3ad6884f6a18d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549100"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="36a00-103">Команда pack (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="36a00-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="36a00-104">**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="36a00-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="36a00-105">Создает пакет NuGet на основе указанного `.nuspec` или файла проекта.</span><span class="sxs-lookup"><span data-stu-id="36a00-105">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="36a00-106">`dotnet pack` Команды (см. в разделе [команды dotnet](dotnet-Commands.md)) и `msbuild /t:pack` (см. в разделе [целевых объектов MSBuild](../reference/msbuild-targets.md)) может использоваться в качестве альтернативы.</span><span class="sxs-lookup"><span data-stu-id="36a00-106">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="36a00-107">В рамках проекта Mono Создание пакета из файла проекта не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="36a00-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="36a00-108">Необходимо также настроить пути не являющейся локальной в `.nuspec` файла в пути в формате Unix, а nuget.exe не преобразует пути Windows, сам.</span><span class="sxs-lookup"><span data-stu-id="36a00-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="36a00-109">Использование</span><span class="sxs-lookup"><span data-stu-id="36a00-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="36a00-110">где `<nuspecPath>` и `<projectPath>` укажите `.nuspec` или файла проекта соответственно.</span><span class="sxs-lookup"><span data-stu-id="36a00-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="36a00-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="36a00-111">Options</span></span>

| <span data-ttu-id="36a00-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="36a00-112">Option</span></span> | <span data-ttu-id="36a00-113">Описание</span><span class="sxs-lookup"><span data-stu-id="36a00-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="36a00-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="36a00-114">BasePath</span></span> | <span data-ttu-id="36a00-115">Задает базовый путь к файлам, определенным в `.nuspec` файл.</span><span class="sxs-lookup"><span data-stu-id="36a00-115">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="36a00-116">Построить</span><span class="sxs-lookup"><span data-stu-id="36a00-116">Build</span></span> | <span data-ttu-id="36a00-117">Указывает, что проект должен быть создан перед созданием пакета.</span><span class="sxs-lookup"><span data-stu-id="36a00-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="36a00-118">Исключить</span><span class="sxs-lookup"><span data-stu-id="36a00-118">Exclude</span></span> | <span data-ttu-id="36a00-119">Указывает один или несколько шаблонов с подстановочными знаками для исключения при создании пакета.</span><span class="sxs-lookup"><span data-stu-id="36a00-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="36a00-120">Чтобы указать несколько шаблонов, повторите флаг - исключения.</span><span class="sxs-lookup"><span data-stu-id="36a00-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="36a00-121">См. пример ниже.</span><span class="sxs-lookup"><span data-stu-id="36a00-121">See example below.</span></span> |
| <span data-ttu-id="36a00-122">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="36a00-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="36a00-123">Предотвращает включение пустые каталоги, при сборке пакета.</span><span class="sxs-lookup"><span data-stu-id="36a00-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="36a00-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="36a00-124">ForceEnglishOutput</span></span> | <span data-ttu-id="36a00-125">*(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры.</span><span class="sxs-lookup"><span data-stu-id="36a00-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="36a00-126">Справка</span><span class="sxs-lookup"><span data-stu-id="36a00-126">Help</span></span> | <span data-ttu-id="36a00-127">Отображает справку для команды.</span><span class="sxs-lookup"><span data-stu-id="36a00-127">Displays help information for the command.</span></span> |
| <span data-ttu-id="36a00-128">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="36a00-128">IncludeReferencedProjects</span></span> | <span data-ttu-id="36a00-129">Указывает, что встроенный пакет должен включать упоминаемые проекты как зависимости или как часть пакета.</span><span class="sxs-lookup"><span data-stu-id="36a00-129">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="36a00-130">Если у упоминаемого проекта есть соответствующий `.nuspec` файл, который имеет имя, совпадающее с именем проекта, а затем этот проект добавляется в качестве зависимости.</span><span class="sxs-lookup"><span data-stu-id="36a00-130">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="36a00-131">В противном случае проект добавляется как часть пакета.</span><span class="sxs-lookup"><span data-stu-id="36a00-131">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="36a00-132">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="36a00-132">MinClientVersion</span></span> | <span data-ttu-id="36a00-133">Задайте *minClientVersion* атрибут для созданного пакета.</span><span class="sxs-lookup"><span data-stu-id="36a00-133">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="36a00-134">Это значение будет переопределять значение существующего *minClientVersion* атрибута (если таковые имеются) в `.nuspec` файл.</span><span class="sxs-lookup"><span data-stu-id="36a00-134">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="36a00-135">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="36a00-135">MSBuildPath</span></span> | <span data-ttu-id="36a00-136">*(4.0 и более поздние)*  Указывает путь к MSBuild для использования с командой, имеют приоритет перед `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="36a00-136">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="36a00-137">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="36a00-137">MSBuildVersion</span></span> | <span data-ttu-id="36a00-138">*(3.2 и более поздние)*  Указывает версию MSBuild для использования с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="36a00-138">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="36a00-139">Поддерживаемые значения: 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="36a00-139">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="36a00-140">По умолчанию выбирается MSBuild в пути в противном случае по умолчанию установленных самую новую версию MSBuild.</span><span class="sxs-lookup"><span data-stu-id="36a00-140">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="36a00-141">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="36a00-141">NoDefaultExcludes</span></span> | <span data-ttu-id="36a00-142">Предотвращает исключения по умолчанию NuGet упаковать файлы и файлы и папки, начиная с точки, такие как `.svn` и `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="36a00-142">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="36a00-143">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="36a00-143">NoPackageAnalysis</span></span> | <span data-ttu-id="36a00-144">Указывает, что пакету не нужно запускать анализ пакета после его сборки.</span><span class="sxs-lookup"><span data-stu-id="36a00-144">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="36a00-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="36a00-145">OutputDirectory</span></span> | <span data-ttu-id="36a00-146">Указывает папку, в которой будет храниться созданный пакет.</span><span class="sxs-lookup"><span data-stu-id="36a00-146">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="36a00-147">Если папка не указана, используется текущая папка.</span><span class="sxs-lookup"><span data-stu-id="36a00-147">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="36a00-148">Свойства</span><span class="sxs-lookup"><span data-stu-id="36a00-148">Properties</span></span> | <span data-ttu-id="36a00-149">Последний в командной строке через появятся другие параметры.</span><span class="sxs-lookup"><span data-stu-id="36a00-149">Should appear last on the command line after other options.</span></span> <span data-ttu-id="36a00-150">Указывает список свойств, которые переопределяют значения в файле проекта; см. в разделе [общие свойства проектов MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) для имен свойств.</span><span class="sxs-lookup"><span data-stu-id="36a00-150">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="36a00-151">Аргументе свойств приведен список маркер = пар "значение", разделенных точкой с запятой, где каждое вхождение `$token$` в `.nuspec` файл будет заменен на заданное значение.</span><span class="sxs-lookup"><span data-stu-id="36a00-151">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="36a00-152">Значения могут быть строки в кавычках.</span><span class="sxs-lookup"><span data-stu-id="36a00-152">Values can be strings in quotation marks.</span></span> <span data-ttu-id="36a00-153">Обратите внимание, что для свойства «Конфигурация», значение по умолчанию «Debug».</span><span class="sxs-lookup"><span data-stu-id="36a00-153">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="36a00-154">Чтобы изменить конфигурацию выпуска, используйте `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="36a00-154">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="36a00-155">Суффикс</span><span class="sxs-lookup"><span data-stu-id="36a00-155">Suffix</span></span> | <span data-ttu-id="36a00-156">*(3.4.4+)*  Добавляет суффикс для созданного внутреннего номер_версии, обычно используется для добавления сборки или другие идентификаторы предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="36a00-156">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="36a00-157">Например, с помощью `-suffix nightly` создаст пакет с like номера версии `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="36a00-157">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="36a00-158">Суффиксы должны начинаться с буквы, чтобы избежать предупреждения, ошибки и потенциальных несовместимости с различными версиями NuGet и диспетчер пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="36a00-158">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="36a00-159">Символы</span><span class="sxs-lookup"><span data-stu-id="36a00-159">Symbols</span></span> | <span data-ttu-id="36a00-160">Указывает, что пакет содержит источники и символы.</span><span class="sxs-lookup"><span data-stu-id="36a00-160">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="36a00-161">При использовании с `.nuspec` файл, это создает обычный файл пакета NuGet и соответствующий пакет символов.</span><span class="sxs-lookup"><span data-stu-id="36a00-161">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="36a00-162">Средство</span><span class="sxs-lookup"><span data-stu-id="36a00-162">Tool</span></span> | <span data-ttu-id="36a00-163">Указывает, что следует поместить выходные файлы проекта в `tool` папку.</span><span class="sxs-lookup"><span data-stu-id="36a00-163">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="36a00-164">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="36a00-164">Verbosity</span></span> | <span data-ttu-id="36a00-165">Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="36a00-165">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="36a00-166">Версия</span><span class="sxs-lookup"><span data-stu-id="36a00-166">Version</span></span> | <span data-ttu-id="36a00-167">Переопределяет номер версии из `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="36a00-167">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="36a00-168">Также см. в разделе [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="36a00-168">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="36a00-169">За исключением зависимости разработки</span><span class="sxs-lookup"><span data-stu-id="36a00-169">Excluding development dependencies</span></span>

<span data-ttu-id="36a00-170">Некоторые пакеты NuGet полезны в качестве зависимости разработки, которые помогут вам создать свою собственную библиотеку, но не обязательно нужны как зависимости самого пакета.</span><span class="sxs-lookup"><span data-stu-id="36a00-170">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="36a00-171">`pack` Команда будет игнорировать `package` записей в `packages.config` , имеющих `developmentDependency` атрибут `true`.</span><span class="sxs-lookup"><span data-stu-id="36a00-171">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="36a00-172">Эти записи не будут включены в качестве зависимостей в созданный пакет.</span><span class="sxs-lookup"><span data-stu-id="36a00-172">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="36a00-173">Например, рассмотрим следующие `packages.config` файл в исходном проекте:</span><span class="sxs-lookup"><span data-stu-id="36a00-173">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="36a00-174">Для этого проекта, пакет создан `nuget pack` будет зависят от `jQuery` и `microsoft-web-helpers` , но не `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="36a00-174">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="36a00-175">Примеры</span><span class="sxs-lookup"><span data-stu-id="36a00-175">Examples</span></span>

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
