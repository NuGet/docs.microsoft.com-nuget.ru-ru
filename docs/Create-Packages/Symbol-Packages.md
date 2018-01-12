---
title: "Создание пакетов символов NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 9/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 4667a70d-5a17-4f1e-b2f2-b8d0c6af3882
description: "В этой статье описывается создание пакетов NuGet, которые содержат только символы, для поддержки отладки других пакетов NuGet в Visual Studio."
keywords: "пакеты символов NuGet, отладка пакета NuGet, поддержка отладки NuGet, символы пакета, соглашения о пакетах символов"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2bdb8a2c946618b0c297c70bf7fcf6a9038b2a02
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="creating-symbol-packages"></a><span data-ttu-id="8d457-104">Создание пакетов символов</span><span class="sxs-lookup"><span data-stu-id="8d457-104">Creating symbol packages</span></span>

<span data-ttu-id="8d457-105">Помимо построения пакетов для веб-сайта nuget.org или других источников, NuGet также поддерживает создание связанных пакетов символов и их публикацию в [репозитории SymbolSource](http://www.symbolsource.org/Public).</span><span class="sxs-lookup"><span data-stu-id="8d457-105">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the [SymbolSource repository](http://www.symbolsource.org/Public).</span></span>

<span data-ttu-id="8d457-106">Потребители пакетов могут добавить `http://srv.symbolsource.org/pdb/Public` в соответствующие источники символов в Visual Studio, что позволяет осуществлять пошаговую отладку кода пакета в отладчике Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8d457-106">Package consumers can then add `http://srv.symbolsource.org/pdb/Public` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="8d457-107">Дополнительные сведения об этом процессе см. в разделе [Указание файлов символов (.pdb) и файлов с исходным кодом в отладчике Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).</span><span class="sxs-lookup"><span data-stu-id="8d457-107">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>


## <a name="creating-a-symbol-package"></a><span data-ttu-id="8d457-108">Создание пакета символов</span><span class="sxs-lookup"><span data-stu-id="8d457-108">Creating a symbol package</span></span>

<span data-ttu-id="8d457-109">При создании пакета символов руководствуйтесь следующими соглашениями:</span><span class="sxs-lookup"><span data-stu-id="8d457-109">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="8d457-110">Присвойте имя основному пакету (с кодом) `{identifier}.nupkg` и включите в него все файлы, за исключением файлов `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="8d457-110">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="8d457-111">Присвойте имя пакету символов `{identifier}.symbols.nupkg` и включите в него DLL-файл сборки, файлы `.pdb`, XMLDOC-файлы и файлы с исходным кодом (см. далее).</span><span class="sxs-lookup"><span data-stu-id="8d457-111">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="8d457-112">Можно создать оба пакета с использованием параметра `-Symbols` на основе файла `.nuspec` или файла проекта:</span><span class="sxs-lookup"><span data-stu-id="8d457-112">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="8d457-113">Обратите внимание, что команда `pack` требует наличия Mono 4.4.2 в Mac OS X и не работает в системах Linux.</span><span class="sxs-lookup"><span data-stu-id="8d457-113">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="8d457-114">На компьютерах Mac также необходимо преобразовать пути в формате Windows, указанные в файле `.nuspec`, в формат Unix.</span><span class="sxs-lookup"><span data-stu-id="8d457-114">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="8d457-115">Структура пакета символов</span><span class="sxs-lookup"><span data-stu-id="8d457-115">Symbol package structure</span></span>

<span data-ttu-id="8d457-116">Пакет символов, так же как и пакет библиотек, может предназначаться для нескольких целевых платформ, поэтому структура папки `lib` должна в точности совпадать с основным пакетом и включать файлы `.pdb` наряду с DLL.</span><span class="sxs-lookup"><span data-stu-id="8d457-116">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="8d457-117">Например, пакет символов для платформы .NET 4.0 и Silverlight 4 должен иметь следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="8d457-117">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="8d457-118">Файлы исходного кода размещаются в отдельной папке `src`, которая должна соответствовать относительной структуре репозитория исходного кода.</span><span class="sxs-lookup"><span data-stu-id="8d457-118">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="8d457-119">Это связано с тем, что PDB-файлы содержат абсолютные пути к файлам исходного кода, используемым для компиляции соответствующей библиотеки DLL, и должны быть доступны в процессе публикации.</span><span class="sxs-lookup"><span data-stu-id="8d457-119">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="8d457-120">Базовый путь (общий префикс пути) может быть опущен. Например, рассмотрим библиотеку, построенную на основе следующих файлов:</span><span class="sxs-lookup"><span data-stu-id="8d457-120">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="8d457-121">Помимо папки `lib`, пакет символов должен содержать следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="8d457-121">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="8d457-122">Ссылки на файлы в nuspec</span><span class="sxs-lookup"><span data-stu-id="8d457-122">Referring to files in the nuspec</span></span>

<span data-ttu-id="8d457-123">Пакет символов может быть построен в соответствии с соглашениями на основе структуры папок, как описывается в предыдущем разделе, а также путем указания его содержимого в разделе `files` манифеста.</span><span class="sxs-lookup"><span data-stu-id="8d457-123">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="8d457-124">Например, чтобы построить показанный в предыдущем разделе пакет, используйте следующий файл `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="8d457-124">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="8d457-125">Публикация пакета символов</span><span class="sxs-lookup"><span data-stu-id="8d457-125">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="8d457-126">Для принудительной отправки пакетов на веб-сайт nuget.org необходимо использовать [nuget.exe версии 4.1.0 или более поздней](https://www.nuget.org/downloads), где реализуются требуемые [протоколы NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="8d457-126">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="8d457-127">Для удобства сначала следует сохранить ключ API с помощью NuGet (см. раздел [Публикация пакета](../create-packages/publish-a-package.md)), который будет применяться и к nuget.org, и к symbolsource.org, поскольку веб-сайт symbolsource.org будет проверять информацию о том, что вы являетесь владельцем пакета, на веб-сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8d457-127">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="8d457-128">После публикации основного пакета на веб-сайте nuget.org выполните принудительную отправку пакета символов, как показано ниже. При этом в качестве назначения будет автоматически использоваться веб-сайт symbolsource.org, поскольку в имени файла указано `.symbols`:</span><span class="sxs-lookup"><span data-stu-id="8d457-128">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```
    nuget push MyPackage.symbols.nupkg
    ```
> [!Note]
> <span data-ttu-id="8d457-129">При работе с nuget.exe версии 4.5.0 или более поздней пакеты символов не передаются автоматически на веб-сайт symbolsource.org. В таком случае принудительную отправку пакетов символов необходимо осуществлять отдельно, как описывается на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="8d457-129">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the next step.</span></span>

1. <span data-ttu-id="8d457-130">Чтобы выполнить публикацию в другом репозитории символов или принудительную отправку пакета символов, не соответствующего соглашениям об именовании, следует использовать параметр `-Source`:</span><span class="sxs-lookup"><span data-stu-id="8d457-130">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

1. <span data-ttu-id="8d457-131">Также можно выполнить принудительную отправку одновременно основного пакета и пакета символов в оба репозитория, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8d457-131">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="8d457-132">В этом случае NuGet опубликует файл `MyPackage.symbols.nupkg` (если он есть) на веб-сайте https://nuget.smbsrc.net/ (URL-адрес принудительной отправки для веб-сайта symbolsource.org) после публикации основного пакета на веб-сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8d457-132">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="8d457-133">См. также</span><span class="sxs-lookup"><span data-stu-id="8d457-133">See Also</span></span>

 - <span data-ttu-id="8d457-134"><a href="https://www.symbolsource.org/Public/Wiki/Using" target="_blank">Использование веб-сайта SymbolSource</a> (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="8d457-134"><a href="https://www.symbolsource.org/Public/Wiki/Using" target="_blank">Using SymbolSource</a> (symbolsource.org)</span></span>
