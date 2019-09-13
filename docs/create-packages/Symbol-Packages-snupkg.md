---
title: Публикация пакетов символов NuGet с помощью нового формата, SNUPKG| Документация Майкрософт
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Создание пакетов символов NuGet (SNUPKG).
keywords: пакеты символов NuGet, отладка пакета NuGet, поддержка отладки NuGet, символы пакета, соглашения о пакетах символов
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 109df18bcfd3e6a3fbd3ef3da1707ffada585140
ms.sourcegitcommit: f4bfdbf62302c95f1f39e81ccf998f8bbc6d56b0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2019
ms.locfileid: "70749032"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="f0666-104">Создание пакетов символов (SNUPKG)</span><span class="sxs-lookup"><span data-stu-id="f0666-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="f0666-105">Пакеты символов позволяют улучшить интерфейс отладки пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="f0666-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0666-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f0666-106">Prerequisites</span></span>

<span data-ttu-id="f0666-107">[nuget.exe 4.9.0 или более поздней версии](https://www.nuget.org/downloads) либо [dotnet.exe 2.2.0 или более поздней версии](https://www.microsoft.com/net/download/dotnet-core/2.2), которые реализуют необходимые [протоколы NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="f0666-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="f0666-108">Создание пакета символов</span><span class="sxs-lookup"><span data-stu-id="f0666-108">Creating a symbol package</span></span>

<span data-ttu-id="f0666-109">Если вы используете dotnet.exe или MSBuild, необходимо задать свойства `IncludeSymbols` и `SymbolPackageFormat`, чтобы создать SNUPKG-файл в дополнение к NUPKG-файлу.</span><span class="sxs-lookup"><span data-stu-id="f0666-109">If you're using dotnet.exe or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="f0666-110">Как вариант, добавьте следующие свойства в CSPROJ-файл.</span><span class="sxs-lookup"><span data-stu-id="f0666-110">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols> 
      <SymbolPackageFormat>snupkg</SymbolPackageFormat> 
   </PropertyGroup>
   ```

* <span data-ttu-id="f0666-111">Вы также можете указать эти свойства в командной строке.</span><span class="sxs-lookup"><span data-stu-id="f0666-111">Or specify these properties on the command-line:</span></span>

     ```cli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="f0666-112">или</span><span class="sxs-lookup"><span data-stu-id="f0666-112">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="f0666-113">Если вы используете NuGet.exe, вы можете с помощью следующих команд создать SNUPKG-файл в дополнение к NUPKG-файлу:</span><span class="sxs-lookup"><span data-stu-id="f0666-113">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="f0666-114">Свойство [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) может иметь одно из двух значений: `symbols.nupkg` (по умолчанию) или `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="f0666-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="f0666-115">Если значение этого свойства не указано, будет создан устаревший пакет символов.</span><span class="sxs-lookup"><span data-stu-id="f0666-115">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="f0666-116">Устаревший формат `.symbols.nupkg` все еще поддерживается, но только в целях совместимости (см. раздел [Устаревшие пакеты символов](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="f0666-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="f0666-117">Сервер символов NuGet.org принимает только новый формат пакетов символов: `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="f0666-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="f0666-118">Публикация пакета символов</span><span class="sxs-lookup"><span data-stu-id="f0666-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="f0666-119">Для удобства сначала сохраните ключ API с NuGet (см. раздел [Публикация пакета](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="f0666-119">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="f0666-120">После публикации основного пакета в nuget.org передайте пакет символов следующим образом.</span><span class="sxs-lookup"><span data-stu-id="f0666-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="f0666-121">Также можно выполнить принудительную отправку одновременно основного пакета и пакета символов, используя указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="f0666-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="f0666-122">Оба файла (.nupkg и .snupkg) должны находиться в текущей папке.</span><span class="sxs-lookup"><span data-stu-id="f0666-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="f0666-123">NuGet опубликует оба пакета на сайте nuget.org. Пакет `MyPackage.nupkg` будет опубликован первым, а `MyPackage.snupkg` — вторым.</span><span class="sxs-lookup"><span data-stu-id="f0666-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="f0666-124">Если пакет символов не опубликован, убедитесь, что вы настроили источник NuGet.org в виде `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="f0666-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="f0666-125">Публикация пакетов символов поддерживается только в [API NuGet версии 3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="f0666-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="f0666-126">Сервер символов NuGet.org</span><span class="sxs-lookup"><span data-stu-id="f0666-126">NuGet.org symbol server</span></span>

<span data-ttu-id="f0666-127">NuGet.org поддерживает собственный репозиторий сервера символов и принимает только новый формат пакетов символов: `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="f0666-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="f0666-128">Потребители пакетов могут добавить `https://symbols.nuget.org/download/symbols` в соответствующие источники символов в Visual Studio с помощью символов, опубликованных на сервер символов nuget.org, что позволяет осуществлять пошаговую отладку кода пакета в отладчике Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f0666-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="f0666-129">Дополнительные сведения об этом процессе см. в разделе [Указание файлов символов (.pdb) и файлов с исходным кодом в отладчике Visual Studio](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017).</span><span class="sxs-lookup"><span data-stu-id="f0666-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="f0666-130">Ограничения пакета символов Nuget.org</span><span class="sxs-lookup"><span data-stu-id="f0666-130">Nuget.org symbol package constraints</span></span>

<span data-ttu-id="f0666-131">Пакеты символов, поддерживаемые в nuget.org, имеют следующие ограничения.</span><span class="sxs-lookup"><span data-stu-id="f0666-131">The symbol packages supported on nuget.org have the following contraints</span></span>

- <span data-ttu-id="f0666-132">В пакет символов можно добавлять только следующие расширения файлов.</span><span class="sxs-lookup"><span data-stu-id="f0666-132">Only the following file extensions are allowed to be added to a symbol package.</span></span> ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- <span data-ttu-id="f0666-133">Сейчас на сервере символов NuGet поддерживаются только управляемые [переносимые PDB-файлы](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md).</span><span class="sxs-lookup"><span data-stu-id="f0666-133">Only managed [Portable pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are currently supported on nuget symbol server.</span></span>
- <span data-ttu-id="f0666-134">Нужно выполнить сборку PDB-файлов и связанных библиотек DLL NUPKG в компиляторе в Visual Studio версии 15.9 или выше (см. раздел [Хэш шифрования PDB-файлов](https://github.com/dotnet/roslyn/issues/24429)).</span><span class="sxs-lookup"><span data-stu-id="f0666-134">The pdbs and associated nupkg dlls need to be built with the compiler in Visual Studio version 15.9 or above (see [pdb crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="f0666-135">Если в SNUPKG-файл включены любые другие типы файлов, произойдет сбой публикации в nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f0666-135">The symbol package publish on nuget.org will fail if any other file types are included in the .snupkg.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="f0666-136">Проверка и индексирование пакета символов</span><span class="sxs-lookup"><span data-stu-id="f0666-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="f0666-137">Пакеты символов, опубликованные в [NuGet.org](https://www.nuget.org/), проходят несколько проверок, например, проверку на вирусы.</span><span class="sxs-lookup"><span data-stu-id="f0666-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, such as virus checks.</span></span>

<span data-ttu-id="f0666-138">После прохождения пакетом всех проверок может пройти некоторое время, прежде чем символы будут проиндексированы и станут доступны для использования на серверах символов NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f0666-138">When the package has passed all validation checks, it might take a while for the symbols to index and be available for consumption from the NuGet.org symbol servers.</span></span> <span data-ttu-id="f0666-139">Если пакет не проходит проверку, на странице сведений о пакете NUPKG отображается соответствующее уведомление об ошибке и вы также получите сообщение электронной почты с уведомлением.</span><span class="sxs-lookup"><span data-stu-id="f0666-139">If the package fails a validation check, the package details page for the .nupkg will update to display the associated error and you will also receive an email notifying you about it.</span></span>

<span data-ttu-id="f0666-140">Проверка и индексирование пакета обычно занимает около 15 минут.</span><span class="sxs-lookup"><span data-stu-id="f0666-140">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="f0666-141">Если публикация пакета занимает больше времени, перейдите на веб-сайт [status.nuget.org](https://status.nuget.org/) и убедитесь, что портал nuget.org работает.</span><span class="sxs-lookup"><span data-stu-id="f0666-141">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="f0666-142">Если все системы исправны, но пакет не был опубликован в течение часа, войдите на веб-сайт nuget.org и свяжитесь с нами по ссылке "Связаться со службой поддержки" на странице сведений о пакете.</span><span class="sxs-lookup"><span data-stu-id="f0666-142">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="f0666-143">Структура пакета символов</span><span class="sxs-lookup"><span data-stu-id="f0666-143">Symbol package structure</span></span>

<span data-ttu-id="f0666-144">NUPKG-файл не будет отличаться от текущего, а SNUPKG-файл будет обладать следующими характеристиками.</span><span class="sxs-lookup"><span data-stu-id="f0666-144">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="f0666-145">SNUPKG-файл будет иметь тот же идентификатор и ту же версию, что и соответствующий NUPKG-файл.</span><span class="sxs-lookup"><span data-stu-id="f0666-145">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="f0666-146">SNUPKG-файл будет иметь ту же структуру папок, что и NUPKG-файл, для всех DLL- и EXE-файлов за следующим исключением. Вместо DLL- и EXE-файлов в ту же иерархию папок будут включены соответствующие PDB-файлы.</span><span class="sxs-lookup"><span data-stu-id="f0666-146">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="f0666-147">Файлы и папки с расширениями, отличными от PDB, не войдут в пакет SNUPKG.</span><span class="sxs-lookup"><span data-stu-id="f0666-147">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="f0666-148">NUSPEC-файл в SNUPKG также укажет новый тип PackageType, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="f0666-148">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="f0666-149">Тип PackageType должен быть единственным указанным.</span><span class="sxs-lookup"><span data-stu-id="f0666-149">This should the only one PackageType specified.</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="f0666-150">Если автор решит создать пакеты NUPKG и SNUPKG с помощью пользовательского NUSPEC-файла, пакет SNUPKG должен иметь иерархию папок и файлы, указанные в пункте 2).</span><span class="sxs-lookup"><span data-stu-id="f0666-150">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="f0666-151">Поля ```authors``` и ```owners``` будут исключены из NUSPEC-файла пакета SNUPKG.</span><span class="sxs-lookup"><span data-stu-id="f0666-151">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>
6) <span data-ttu-id="f0666-152">Не используйте элемент ```<license>```.</span><span class="sxs-lookup"><span data-stu-id="f0666-152">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="f0666-153">SNUPKG-файл рассматривается в рамках той же лицензии, что и соответствующий NUPKG-файл.</span><span class="sxs-lookup"><span data-stu-id="f0666-153">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="f0666-154">См. также</span><span class="sxs-lookup"><span data-stu-id="f0666-154">See Also</span></span>

[<span data-ttu-id="f0666-155">Отладка пакетов NuGet и улучшение символов</span><span class="sxs-lookup"><span data-stu-id="f0666-155">NuGet Package Debugging & Symbols Improvements</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
