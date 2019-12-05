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
ms.openlocfilehash: 8528261f90e75e2dfac8cb746b396d227c3741f4
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825180"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="81ffc-104">Создание пакетов символов (SNUPKG)</span><span class="sxs-lookup"><span data-stu-id="81ffc-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="81ffc-105">Пакеты символов позволяют улучшить интерфейс отладки пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="81ffc-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81ffc-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="81ffc-106">Prerequisites</span></span>

<span data-ttu-id="81ffc-107">[nuget.exe 4.9.0 или более поздней версии](https://www.nuget.org/downloads) либо [dotnet.exe 2.2.0 или более поздней версии](https://www.microsoft.com/net/download/dotnet-core/2.2), которые реализуют необходимые [протоколы NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="81ffc-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="81ffc-108">Создание пакета символов</span><span class="sxs-lookup"><span data-stu-id="81ffc-108">Creating a symbol package</span></span>

<span data-ttu-id="81ffc-109">Если вы используете dotnet.exe или MSBuild, необходимо задать свойства `IncludeSymbols` и `SymbolPackageFormat`, чтобы создать SNUPKG-файл в дополнение к NUPKG-файлу.</span><span class="sxs-lookup"><span data-stu-id="81ffc-109">If you're using dotnet.exe or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="81ffc-110">Как вариант, добавьте следующие свойства в CSPROJ-файл.</span><span class="sxs-lookup"><span data-stu-id="81ffc-110">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols> 
      <SymbolPackageFormat>snupkg</SymbolPackageFormat> 
   </PropertyGroup>
   ```

* <span data-ttu-id="81ffc-111">Вы также можете указать эти свойства в командной строке.</span><span class="sxs-lookup"><span data-stu-id="81ffc-111">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="81ffc-112">or</span><span class="sxs-lookup"><span data-stu-id="81ffc-112">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="81ffc-113">Если вы используете NuGet.exe, вы можете с помощью следующих команд создать SNUPKG-файл в дополнение к NUPKG-файлу:</span><span class="sxs-lookup"><span data-stu-id="81ffc-113">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="81ffc-114">Свойство [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) может иметь одно из двух значений: `symbols.nupkg` (по умолчанию) или `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="81ffc-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="81ffc-115">Если значение этого свойства не указано, будет создан устаревший пакет символов.</span><span class="sxs-lookup"><span data-stu-id="81ffc-115">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="81ffc-116">Устаревший формат `.symbols.nupkg` все еще поддерживается, но только в целях совместимости (см. раздел [Устаревшие пакеты символов](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="81ffc-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="81ffc-117">Сервер символов NuGet.org принимает только новый формат пакетов символов: `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="81ffc-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="81ffc-118">Публикация пакета символов</span><span class="sxs-lookup"><span data-stu-id="81ffc-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="81ffc-119">Для удобства сначала сохраните ключ API с NuGet (см. раздел [Публикация пакета](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="81ffc-119">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="81ffc-120">После публикации основного пакета в nuget.org передайте пакет символов следующим образом.</span><span class="sxs-lookup"><span data-stu-id="81ffc-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="81ffc-121">Также можно выполнить принудительную отправку одновременно основного пакета и пакета символов, используя указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="81ffc-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="81ffc-122">Оба файла (.nupkg и .snupkg) должны находиться в текущей папке.</span><span class="sxs-lookup"><span data-stu-id="81ffc-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="81ffc-123">NuGet опубликует оба пакета на сайте nuget.org. Пакет `MyPackage.nupkg` будет опубликован первым, а `MyPackage.snupkg` — вторым.</span><span class="sxs-lookup"><span data-stu-id="81ffc-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="81ffc-124">Если пакет символов не опубликован, убедитесь, что вы настроили источник NuGet.org в виде `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="81ffc-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="81ffc-125">Публикация пакетов символов поддерживается только в [API NuGet версии 3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="81ffc-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="81ffc-126">Сервер символов NuGet.org</span><span class="sxs-lookup"><span data-stu-id="81ffc-126">NuGet.org symbol server</span></span>

<span data-ttu-id="81ffc-127">NuGet.org поддерживает собственный репозиторий сервера символов и принимает только новый формат пакетов символов: `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="81ffc-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="81ffc-128">Потребители пакетов могут добавить `https://symbols.nuget.org/download/symbols` в соответствующие источники символов в Visual Studio с помощью символов, опубликованных на сервер символов nuget.org, что позволяет осуществлять пошаговую отладку кода пакета в отладчике Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="81ffc-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="81ffc-129">Дополнительные сведения об этом процессе см. в разделе [Указание файлов символов (.pdb) и файлов с исходным кодом в отладчике Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).</span><span class="sxs-lookup"><span data-stu-id="81ffc-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="81ffc-130">Ограничения пакета символов NuGet.org</span><span class="sxs-lookup"><span data-stu-id="81ffc-130">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="81ffc-131">NuGet.org налагает на пакеты символов следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="81ffc-131">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="81ffc-132">В пакетах символов допускаются только следующие расширения файлов: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span><span class="sxs-lookup"><span data-stu-id="81ffc-132">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="81ffc-133">На сервере символов NuGet.org поддерживаются только управляемые [переносимые PDB-файлы](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md).</span><span class="sxs-lookup"><span data-stu-id="81ffc-133">Only managed [Portable PDBs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="81ffc-134">Нужно выполнить сборку PDB-файлов и связанных с ними библиотек DLL NUPKG в компиляторе в Visual Studio версии 15.9 или более поздней (см. раздел [Хэш шифрования PDB-файлов](https://github.com/dotnet/roslyn/issues/24429)).</span><span class="sxs-lookup"><span data-stu-id="81ffc-134">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="81ffc-135">Пакеты символов, опубликованные в NuGet.org, не пройдут проверку, если указанные ограничения не соблюдаются.</span><span class="sxs-lookup"><span data-stu-id="81ffc-135">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="81ffc-136">Проверка и индексирование пакета символов</span><span class="sxs-lookup"><span data-stu-id="81ffc-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="81ffc-137">Пакеты символов, опубликованные в [NuGet.org](https://www.nuget.org/), проходят несколько проверок, включая проверку на наличие вредоносных программ.</span><span class="sxs-lookup"><span data-stu-id="81ffc-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="81ffc-138">Если пакет не проходит проверку, на странице сведений о нем отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="81ffc-138">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="81ffc-139">Кроме того, владельцы пакета получат сообщение электронной почты с инструкциями по устранению выявленных проблем.</span><span class="sxs-lookup"><span data-stu-id="81ffc-139">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="81ffc-140">После того как пакет символов пройдет все проверки, символы будут проиндексированы серверами символов NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="81ffc-140">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers.</span></span> <span data-ttu-id="81ffc-141">После индексирования символ будет доступен для использования на серверах символов NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="81ffc-141">Once indexed, the symbol will be available for consumption from the NuGet.org symbol servers.</span></span>

<span data-ttu-id="81ffc-142">Проверка и индексирование пакета обычно занимает около 15 минут.</span><span class="sxs-lookup"><span data-stu-id="81ffc-142">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="81ffc-143">Если публикация пакета занимает больше времени, перейдите на веб-сайт [status.nuget.org](https://status.nuget.org/) и убедитесь, что портал NuGet.org работает.</span><span class="sxs-lookup"><span data-stu-id="81ffc-143">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="81ffc-144">Если все системы исправны, но пакет не был опубликован в течение часа, войдите на веб-сайт nuget.org и свяжитесь с нами по ссылке "Связаться со службой поддержки" на странице сведений о пакете.</span><span class="sxs-lookup"><span data-stu-id="81ffc-144">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="81ffc-145">Структура пакета символов</span><span class="sxs-lookup"><span data-stu-id="81ffc-145">Symbol package structure</span></span>

<span data-ttu-id="81ffc-146">NUPKG-файл не будет отличаться от текущего, а SNUPKG-файл будет обладать следующими характеристиками.</span><span class="sxs-lookup"><span data-stu-id="81ffc-146">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="81ffc-147">SNUPKG-файл будет иметь тот же идентификатор и ту же версию, что и соответствующий NUPKG-файл.</span><span class="sxs-lookup"><span data-stu-id="81ffc-147">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="81ffc-148">SNUPKG-файл будет иметь ту же структуру папок, что и NUPKG-файл, для всех DLL- и EXE-файлов за следующим исключением. Вместо DLL- и EXE-файлов в ту же иерархию папок будут включены соответствующие PDB-файлы.</span><span class="sxs-lookup"><span data-stu-id="81ffc-148">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="81ffc-149">Файлы и папки с расширениями, отличными от PDB, не войдут в пакет SNUPKG.</span><span class="sxs-lookup"><span data-stu-id="81ffc-149">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="81ffc-150">NUSPEC-файл в SNUPKG также укажет новый тип PackageType, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="81ffc-150">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="81ffc-151">Тип PackageType должен быть единственным указанным.</span><span class="sxs-lookup"><span data-stu-id="81ffc-151">This should the only one PackageType specified.</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="81ffc-152">Если автор решит создать пакеты NUPKG и SNUPKG с помощью пользовательского NUSPEC-файла, пакет SNUPKG должен иметь иерархию папок и файлы, указанные в пункте 2).</span><span class="sxs-lookup"><span data-stu-id="81ffc-152">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="81ffc-153">Поля ```authors``` и ```owners``` будут исключены из NUSPEC-файла пакета SNUPKG.</span><span class="sxs-lookup"><span data-stu-id="81ffc-153">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>
6) <span data-ttu-id="81ffc-154">Не используйте элемент ```<license>```.</span><span class="sxs-lookup"><span data-stu-id="81ffc-154">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="81ffc-155">SNUPKG-файл рассматривается в рамках той же лицензии, что и соответствующий NUPKG-файл.</span><span class="sxs-lookup"><span data-stu-id="81ffc-155">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="81ffc-156">См. также</span><span class="sxs-lookup"><span data-stu-id="81ffc-156">See also</span></span>

<span data-ttu-id="81ffc-157">Чтобы обеспечить возможность отладки исходного кода сборок .NET, рекомендуется использовать Source Link.</span><span class="sxs-lookup"><span data-stu-id="81ffc-157">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="81ffc-158">Дополнительные сведения см. в [руководстве по Source Link](/dotnet/standard/library-guidance/sourcelink).</span><span class="sxs-lookup"><span data-stu-id="81ffc-158">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="81ffc-159">Дополнительные сведения о пакетах символов см. в проектной спецификации по [Отладка пакетов NuGet и улучшение символов](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements).</span><span class="sxs-lookup"><span data-stu-id="81ffc-159">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
