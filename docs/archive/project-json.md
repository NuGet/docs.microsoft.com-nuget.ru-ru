---
title: Справочник по файлу project.json для NuGet | Документы Майкрософт
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/27/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: В проектах некоторых типов в файле project.json содержится список пакетов NuGet, используемых в проекте.
keywords: NuGet project.json, ссылки на пакеты NuGet, зависимости NuGet, project.lock.json
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 21542a219faa3d1fa0c32a838645d4471c5aa935
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="projectjson-reference"></a><span data-ttu-id="bd758-104">Справочник по файлу project.json</span><span class="sxs-lookup"><span data-stu-id="bd758-104">project.json reference</span></span>

<span data-ttu-id="bd758-105">*NuGet 3.x или более поздней версии*</span><span class="sxs-lookup"><span data-stu-id="bd758-105">*NuGet 3.x+*</span></span>

<span data-ttu-id="bd758-106">В файле `project.json` содержится список пакетов, используемых в проекте, в формате управления пакетами.</span><span class="sxs-lookup"><span data-stu-id="bd758-106">The `project.json` file maintains a list of packages used in a project, known as a package management format.</span></span> <span data-ttu-id="bd758-107">Этот формат пришел на смену `packages.config`, а в NuGet 4.0 и более поздних версиях ему, в свою очередь, пришел на смену формат [PackageReference](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="bd758-107">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="bd758-108">Файл [`project.lock.json`](#projectlockjson) (описанный ниже) также применяется в проектах, в которых используется файл `project.json`.</span><span class="sxs-lookup"><span data-stu-id="bd758-108">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="bd758-109">Файл `project.json` имеет следующую основную структуру, в которой каждый из четырех объектов верхнего уровня может иметь любое число дочерних объектов:</span><span class="sxs-lookup"><span data-stu-id="bd758-109">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a><span data-ttu-id="bd758-110">Зависимости</span><span class="sxs-lookup"><span data-stu-id="bd758-110">Dependencies</span></span>

<span data-ttu-id="bd758-111">Содержит список зависимостей пакетов NuGet в проекте в следующей форме:</span><span class="sxs-lookup"><span data-stu-id="bd758-111">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="bd758-112">Пример:</span><span class="sxs-lookup"><span data-stu-id="bd758-112">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="bd758-113">Именно в раздел `dependencies` добавляются зависимости пакетов в проект из диалогового окна "Диспетчер пакетов NuGet".</span><span class="sxs-lookup"><span data-stu-id="bd758-113">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="bd758-114">Идентификатор пакета соответствует его идентификатору в nuget.org и в консоли диспетчера пакетов: `Install-Package Microsoft.NETCore`.</span><span class="sxs-lookup"><span data-stu-id="bd758-114">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="bd758-115">При восстановлении пакетов ограничение версии `"5.0.0"` означает `>= 5.0.0`.</span><span class="sxs-lookup"><span data-stu-id="bd758-115">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="bd758-116">То есть если версия 5.0.0 недоступна на сервере, но версия 5.0.1 имеется, NuGet устанавливает версию 5.0.1 и предупреждает об обновлении.</span><span class="sxs-lookup"><span data-stu-id="bd758-116">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="bd758-117">NuGet выбирает самую раннюю доступную версию на сервере, соответствующую ограничению.</span><span class="sxs-lookup"><span data-stu-id="bd758-117">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="bd758-118">Дополнительные сведения о правилах разрешения см. в разделе [Разрешение зависимостей](../consume-packages/dependency-resolution.md).</span><span class="sxs-lookup"><span data-stu-id="bd758-118">See [Dependency resolution](../consume-packages/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="bd758-119">Управление ресурсами зависимостей</span><span class="sxs-lookup"><span data-stu-id="bd758-119">Managing dependency assets</span></span>

<span data-ttu-id="bd758-120">Ресурсы, которые передаются из зависимостей в проект верхнего уровня, определяются с помощью разделенного запятыми набора тегов в свойствах `include` и `exclude` ссылки на зависимость.</span><span class="sxs-lookup"><span data-stu-id="bd758-120">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="bd758-121">Эти теги перечислены в приведенной ниже таблице.</span><span class="sxs-lookup"><span data-stu-id="bd758-121">The tags are listed the table below:</span></span>

| <span data-ttu-id="bd758-122">Тег включения или исключения</span><span class="sxs-lookup"><span data-stu-id="bd758-122">Include/Exclude tag</span></span> | <span data-ttu-id="bd758-123">Затрагиваемые папки пакета</span><span class="sxs-lookup"><span data-stu-id="bd758-123">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="bd758-124">contentFiles</span><span class="sxs-lookup"><span data-stu-id="bd758-124">contentFiles</span></span> | <span data-ttu-id="bd758-125">Content</span><span class="sxs-lookup"><span data-stu-id="bd758-125">Content</span></span>  |
| <span data-ttu-id="bd758-126">исполняющая среда</span><span class="sxs-lookup"><span data-stu-id="bd758-126">runtime</span></span> | <span data-ttu-id="bd758-127">Runtime, Resources и FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="bd758-127">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="bd758-128">compile</span><span class="sxs-lookup"><span data-stu-id="bd758-128">compile</span></span> | <span data-ttu-id="bd758-129">lib</span><span class="sxs-lookup"><span data-stu-id="bd758-129">lib</span></span> |
| <span data-ttu-id="bd758-130">выполнить сборку</span><span class="sxs-lookup"><span data-stu-id="bd758-130">build</span></span> | <span data-ttu-id="bd758-131">build (свойства и цели MSBuild)</span><span class="sxs-lookup"><span data-stu-id="bd758-131">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="bd758-132">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="bd758-132">native</span></span> | <span data-ttu-id="bd758-133">в машинном коде</span><span class="sxs-lookup"><span data-stu-id="bd758-133">native</span></span> |
| <span data-ttu-id="bd758-134">Нет</span><span class="sxs-lookup"><span data-stu-id="bd758-134">none</span></span> | <span data-ttu-id="bd758-135">Нет</span><span class="sxs-lookup"><span data-stu-id="bd758-135">No folders</span></span> |
| <span data-ttu-id="bd758-136">все</span><span class="sxs-lookup"><span data-stu-id="bd758-136">all</span></span> | <span data-ttu-id="bd758-137">Все папки</span><span class="sxs-lookup"><span data-stu-id="bd758-137">All folders</span></span> |

<span data-ttu-id="bd758-138">Теги в свойстве `exclude` имеют приоритет перед тегами в свойстве `include`.</span><span class="sxs-lookup"><span data-stu-id="bd758-138">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="bd758-139">Например, `include="runtime, compile" exclude="compile"` равносильно `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="bd758-139">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="bd758-140">Например, чтобы включить папки `build` и `native` зависимости, используйте следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="bd758-140">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

<span data-ttu-id="bd758-141">Чтобы исключить папки `content` и `build` зависимости, используйте следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="bd758-141">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a><span data-ttu-id="bd758-142">Инфраструктуры</span><span class="sxs-lookup"><span data-stu-id="bd758-142">Frameworks</span></span>

<span data-ttu-id="bd758-143">Список платформ, на которых выполняется проект, например `net45`, `netcoreapp`, `netstandard`.</span><span class="sxs-lookup"><span data-stu-id="bd758-143">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="bd758-144">В разделе `frameworks` допускается только одна запись.</span><span class="sxs-lookup"><span data-stu-id="bd758-144">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="bd758-145">(Исключение составляют файлы `project.json` проектов ASP.NET, сборка которых выполняется с помощью нерекомендуемой цепочки инструментов DNX, допускающей несколько целевых платформ.)</span><span class="sxs-lookup"><span data-stu-id="bd758-145">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX tool chain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="bd758-146">Runtimes</span><span class="sxs-lookup"><span data-stu-id="bd758-146">Runtimes</span></span>

<span data-ttu-id="bd758-147">Содержит список операционных систем и архитектур, в которых выполняется приложение, например `win10-arm`, `win8-x64`, `win8-x86`.</span><span class="sxs-lookup"><span data-stu-id="bd758-147">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

<span data-ttu-id="bd758-148">Пакет, содержащий переносимую библиотеку классов, которая может работать в любой среде выполнения, не требует указания этой среды.</span><span class="sxs-lookup"><span data-stu-id="bd758-148">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="bd758-149">Это также должно быть верно в отношении всех зависимостей. В противном случае необходимо указывать среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="bd758-149">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="bd758-150">Supports</span><span class="sxs-lookup"><span data-stu-id="bd758-150">Supports</span></span>

<span data-ttu-id="bd758-151">Определяет набор проверок для зависимостей пакетов.</span><span class="sxs-lookup"><span data-stu-id="bd758-151">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="bd758-152">Вы можете определить, где предполагается выполнение переносимой библиотеки классов или приложения.</span><span class="sxs-lookup"><span data-stu-id="bd758-152">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="bd758-153">Определения не являются ограничивающими, то есть код может выполняться и в других средах.</span><span class="sxs-lookup"><span data-stu-id="bd758-153">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="bd758-154">Однако если вы указываете эти проверки, NuGet проверяет, все ли зависимости совместимы с перечисленными моникерами целевой версии x.</span><span class="sxs-lookup"><span data-stu-id="bd758-154">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="bd758-155">Примеры возможных значений: `net46.app`, `uwp.10.0.app` и т. д.</span><span class="sxs-lookup"><span data-stu-id="bd758-155">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="bd758-156">При выборе элемента в диалоговом окне целевых платформ для переносимой библиотеки классов этот раздел должен заполняться автоматически.</span><span class="sxs-lookup"><span data-stu-id="bd758-156">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="bd758-157">Imports</span><span class="sxs-lookup"><span data-stu-id="bd758-157">Imports</span></span>

<span data-ttu-id="bd758-158">Раздел Imports предназначен для того, чтобы разрешить пакетам, использующим моникер целевой версии x `dotnet`, взаимодействовать с пакетами, которые не объявляют моникер целевой версии x dotnet.</span><span class="sxs-lookup"><span data-stu-id="bd758-158">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="bd758-159">Если в проекте используется моникер целевой версии x `dotnet`, все пакеты, от которых вы зависите, должны также содержать моникер целевой версии x `dotnet`. В противном случае нужно добавить в файл `project.json` следующий элемент, чтобы обеспечить совместимость платформ, отличных от `dotnet`, с `dotnet`:</span><span class="sxs-lookup"><span data-stu-id="bd758-159">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="bd758-160">Если вы используете моникер целевой версии x `dotnet`, система проектов переносимой библиотеки классов добавляет оператор `imports`, соответствующий поддерживаемым целевым платформам.</span><span class="sxs-lookup"><span data-stu-id="bd758-160">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="bd758-161">Отличия от переносимых приложений и веб-проектов</span><span class="sxs-lookup"><span data-stu-id="bd758-161">Differences from portable apps and web projects</span></span>

<span data-ttu-id="bd758-162">Содержимое файла `project.json`, используемого NuGet, представляет собой подмножество данных аналогичного файла в проектах ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="bd758-162">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="bd758-163">В ASP.NET Core файл `project.json` содержит метаданные проекта, сведения о компиляции и зависимости.</span><span class="sxs-lookup"><span data-stu-id="bd758-163">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="bd758-164">При использовании в других системах проектов эти три типа данных разносятся по отдельным файлам, поэтому файл `project.json` содержит меньше информации.</span><span class="sxs-lookup"><span data-stu-id="bd758-164">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="bd758-165">Ниже представлены наиболее важные отличия.</span><span class="sxs-lookup"><span data-stu-id="bd758-165">Notable differences include:</span></span>

- <span data-ttu-id="bd758-166">В разделе `frameworks` может быть только одна платформа.</span><span class="sxs-lookup"><span data-stu-id="bd758-166">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="bd758-167">Файл не может содержать зависимости, параметры компиляции и другие данные, которые можно увидеть в файлах `project.json` DNX.</span><span class="sxs-lookup"><span data-stu-id="bd758-167">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="bd758-168">Так как платформа может быть только одна, нет смысла указывать зависимости для конкретных платформ.</span><span class="sxs-lookup"><span data-stu-id="bd758-168">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="bd758-169">Компиляция осуществляется платформой MSBuild, поэтому параметры компиляции, определения препроцессора и т. д. содержатся в файле проекта MSBuild, а не в файле `project.json`.</span><span class="sxs-lookup"><span data-stu-id="bd758-169">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="bd758-170">В NuGet 3 предполагается, что разработчики не редактируют файл `project.json` вручную, так как для работы с его содержимым предназначен пользовательский интерфейс диспетчера пакетов в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bd758-170">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="bd758-171">Вы, безусловно, можете редактировать его, однако сборку проекта для запуска восстановления пакетов необходимо выполнять иным способом.</span><span class="sxs-lookup"><span data-stu-id="bd758-171">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="bd758-172">См. раздел [Восстановление пакета](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="bd758-172">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="bd758-173">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="bd758-173">project.lock.json</span></span>

<span data-ttu-id="bd758-174">Файл `project.lock.json` создается в процессе восстановления пакетов NuGet в проектах, в которых применяется файл `project.json`.</span><span class="sxs-lookup"><span data-stu-id="bd758-174">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="bd758-175">Он содержит моментальный снимок всех данных, создаваемых в процессе обхода диспетчером NuGet графа пакетов, включая версию, содержимое и зависимости всех пакетов в проекте.</span><span class="sxs-lookup"><span data-stu-id="bd758-175">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="bd758-176">Система сборки использует эти данные для выбора пакетов, которые необходимы при сборке проекта, из глобального расположения вместо обращения к локальной папке пакетов в самом проекте.</span><span class="sxs-lookup"><span data-stu-id="bd758-176">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="bd758-177">Благодаря этому ускоряется процесс сборки, так как требуется прочитать только файл `project.lock.json` вместо нескольких отдельных файлов `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="bd758-177">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="bd758-178">Файл `project.lock.json` создается автоматически при восстановлении пакета, поэтому его можно исключить из системы управления версиями, добавив его в файлы `.gitignore` и `.tfignore` (см. раздел [Пакеты и система управления версиями](../consume-packages/packages-and-source-control.md)).</span><span class="sxs-lookup"><span data-stu-id="bd758-178">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="bd758-179">Однако если вы включите его в систему управления версиями, в журнале изменений будут показаны изменения в разрешении зависимостей с течением времени.</span><span class="sxs-lookup"><span data-stu-id="bd758-179">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
