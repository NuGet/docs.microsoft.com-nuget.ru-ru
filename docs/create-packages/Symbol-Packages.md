---
title: Создание пакетов символов прежних версий (.symbols.nupkg)
description: В этой статье описывается создание пакетов NuGet, которые содержат только символы, для поддержки отладки других пакетов NuGet в Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: d9a96986bf80aa15423d7dcee6ea3fe59255252b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774544"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a><span data-ttu-id="e5a9c-103">Создание пакетов символов прежних версий (.symbols.nupkg)</span><span class="sxs-lookup"><span data-stu-id="e5a9c-103">Creating legacy symbol packages (.symbols.nupkg)</span></span>

> [!Important]
> <span data-ttu-id="e5a9c-104">Новый рекомендуемый формат для пакетов символов — .snupkg.</span><span class="sxs-lookup"><span data-stu-id="e5a9c-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="e5a9c-105">См. раздел [Создание пакетов символов (.snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="e5a9c-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="e5a9c-106">Формат .symbols.nupkg все еще поддерживается, но только в целях совместимости.</span><span class="sxs-lookup"><span data-stu-id="e5a9c-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="e5a9c-107">Наряду с возможностью создания пакетов для веб-сайта nuget.org или других источников NuGet также позволяет создавать связанные пакеты символов, которые можно опубликовать на серверах символов.</span><span class="sxs-lookup"><span data-stu-id="e5a9c-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages that can be published to symbol servers.</span></span> <span data-ttu-id="e5a9c-108">Пакеты символов прежних версий в формате .symbols.nupkg можно отправить в репозиторий SymbolSource.</span><span class="sxs-lookup"><span data-stu-id="e5a9c-108">The legacy symbol package format, .symbols.nupkg, can be pushed to the SymbolSource repository.</span></span>

<span data-ttu-id="e5a9c-109">Потребители пакетов могут добавить `https://nuget.smbsrc.net` в соответствующие источники символов в Visual Studio, что позволяет осуществлять пошаговую отладку кода пакета в отладчике Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e5a9c-109">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="e5a9c-110">Дополнительные сведения об этом процессе см. в разделе [Указание файлов символов (.pdb) и файлов с исходным кодом в отладчике Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).</span><span class="sxs-lookup"><span data-stu-id="e5a9c-110">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-legacy-symbol-package"></a><span data-ttu-id="e5a9c-111">Создание пакета символов прежних версий</span><span class="sxs-lookup"><span data-stu-id="e5a9c-111">Creating a legacy symbol package</span></span>

<span data-ttu-id="e5a9c-112">При создании пакета символов прежних версий руководствуйтесь следующими соглашениями:</span><span class="sxs-lookup"><span data-stu-id="e5a9c-112">To create a legacy symbol package, follow these conventions:</span></span>

- <span data-ttu-id="e5a9c-113">Присвойте имя основному пакету (с кодом) `{identifier}.nupkg` и включите в него все файлы, за исключением файлов `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="e5a9c-113">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="e5a9c-114">Присвойте пакету имя `{identifier}.symbols.nupkg` и включите в него DLL-файл сборки, файлы `.pdb`, XMLDOC-файлы и файлы с исходным кодом (см. далее).</span><span class="sxs-lookup"><span data-stu-id="e5a9c-114">Name the legacy symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="e5a9c-115">Можно создать оба пакета с использованием параметра `-Symbols` на основе файла `.nuspec` или файла проекта:</span><span class="sxs-lookup"><span data-stu-id="e5a9c-115">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="e5a9c-116">Обратите внимание, что команда `pack` требует наличия Mono 4.4.2 в Mac OS X и не работает в системах Linux.</span><span class="sxs-lookup"><span data-stu-id="e5a9c-116">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="e5a9c-117">На компьютерах Mac также необходимо преобразовать пути в формате Windows, указанные в файле `.nuspec`, в формат Unix.</span><span class="sxs-lookup"><span data-stu-id="e5a9c-117">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="legacy-symbol-package-structure"></a><span data-ttu-id="e5a9c-118">Структура пакета символов прежних версий</span><span class="sxs-lookup"><span data-stu-id="e5a9c-118">Legacy symbol package structure</span></span>

<span data-ttu-id="e5a9c-119">Как и пакет библиотек, пакет символов прежних версий может предназначаться для нескольких целевых платформ, поэтому структура папки `lib` должна точно соответствовать основному пакету и включать файлы `.pdb` вместе с DLL.</span><span class="sxs-lookup"><span data-stu-id="e5a9c-119">A legacy symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="e5a9c-120">Например, пакет символов устаревших версий для .NET 4.0 и Silverlight 4 должен иметь следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="e5a9c-120">For example, a legacy symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

```
\lib
    \net40
        \MyAssembly.dll
        \MyAssembly.pdb
    \sl40
        \MyAssembly.dll
        \MyAssembly.pdb
```

<span data-ttu-id="e5a9c-121">Файлы исходного кода размещаются в отдельной папке `src`, которая должна соответствовать относительной структуре репозитория исходного кода.</span><span class="sxs-lookup"><span data-stu-id="e5a9c-121">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="e5a9c-122">Это связано с тем, что PDB-файлы содержат абсолютные пути к файлам исходного кода, используемым для компиляции соответствующей библиотеки DLL, и должны быть доступны в процессе публикации.</span><span class="sxs-lookup"><span data-stu-id="e5a9c-122">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="e5a9c-123">Базовый путь (общий префикс пути) может быть опущен. Например, рассмотрим библиотеку, построенную на основе следующих файлов:</span><span class="sxs-lookup"><span data-stu-id="e5a9c-123">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

```
C:\Projects
    \MyProject
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
            \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs
            \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)
```

<span data-ttu-id="e5a9c-124">Кроме папки `lib`, пакет символов прежних версий должен содержать следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="e5a9c-124">Apart from the `lib` folder, a legacy symbol package would need to contain this layout:</span></span>

```
\src
    \Common
        \MyClass.cs
    \Full
        \Properties
            \AssemblyInfo.cs
    \Silverlight
        \Properties
            \AssemblyInfo.cs
        \MySilverlightExtensions.cs
```

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="e5a9c-125">Ссылки на файлы в nuspec</span><span class="sxs-lookup"><span data-stu-id="e5a9c-125">Referring to files in the nuspec</span></span>

<span data-ttu-id="e5a9c-126">Пакет символов прежних версий можно создать в соответствии с соглашениями на основе структуры папок, как описывается в предыдущем разделе, а также путем указания его содержимого в разделе `files` манифеста.</span><span class="sxs-lookup"><span data-stu-id="e5a9c-126">A legacy symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="e5a9c-127">Например, чтобы построить показанный в предыдущем разделе пакет, используйте следующий файл `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="e5a9c-127">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a><span data-ttu-id="e5a9c-128">Публикация пакета символов прежних версий</span><span class="sxs-lookup"><span data-stu-id="e5a9c-128">Publishing a legacy symbol package</span></span>

> [!Important]
> <span data-ttu-id="e5a9c-129">Для принудительной отправки пакетов на веб-сайт nuget.org необходимо использовать [nuget.exe версии 4.9.1 или более поздней](https://www.nuget.org/downloads), где реализуются требуемые [протоколы NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="e5a9c-129">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="e5a9c-130">Для удобства сначала следует сохранить ключ API с помощью NuGet (см. раздел [Публикация пакета](../nuget-org/publish-a-package.md)), который будет применяться и к nuget.org, и к symbolsource.org, поскольку веб-сайт symbolsource.org будет проверять информацию о том, что вы являетесь владельцем пакета, на веб-сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e5a9c-130">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="e5a9c-131">После публикации основного пакета на веб-сайте nuget.org выполните принудительную отправку пакета символов прежних версий, как показано ниже. При этом в качестве назначения будет автоматически использоваться веб-сайт symbolsource.org, так как в имени файла указано `.symbols`:</span><span class="sxs-lookup"><span data-stu-id="e5a9c-131">After publishing your primary package to nuget.org, push the legacy symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="e5a9c-132">Чтобы выполнить публикацию в другом репозитории символов или принудительную отправку пакета символов прежних версий, не соответствующего соглашениям об именовании, следует использовать параметр `-Source`:</span><span class="sxs-lookup"><span data-stu-id="e5a9c-132">To publish to a different symbol repository, or to push a legacy symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="e5a9c-133">Также можно выполнить принудительную отправку одновременно основного пакета и пакета символов в оба репозитория, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e5a9c-133">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="e5a9c-134">При работе с nuget.exe версии 4.5.0 или более поздней пакеты символов не передаются автоматически на веб-сайт symbolsource.org. В таком случае принудительную отправку пакетов символов необходимо осуществлять отдельно, как было описано ранее.</span><span class="sxs-lookup"><span data-stu-id="e5a9c-134">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="e5a9c-135">В этом случае NuGet опубликует файл `MyPackage.symbols.nupkg` (если он есть) на веб-сайте https://nuget.smbsrc.net/ (URL-адрес принудительной отправки для веб-сайта symbolsource.org) после публикации основного пакета на веб-сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e5a9c-135">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="e5a9c-136">См. также</span><span class="sxs-lookup"><span data-stu-id="e5a9c-136">See also</span></span>

* <span data-ttu-id="e5a9c-137">[Создание пакетов символов (.snupkg)](Symbol-Packages-snupkg.md) — новый рекомендуемый формат для пакетов символов</span><span class="sxs-lookup"><span data-stu-id="e5a9c-137">[Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md) - The new recommended format for symbol packages</span></span>
* <span data-ttu-id="e5a9c-138">[Сведения о переходе на новый модуль SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="e5a9c-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
