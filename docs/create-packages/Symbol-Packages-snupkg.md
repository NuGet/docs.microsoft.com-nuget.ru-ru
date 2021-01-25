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
ms.openlocfilehash: fbcc035a6b800617f995d3bcebd7e1764aa467b0
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235728"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="063b0-104">Создание пакетов символов (SNUPKG)</span><span class="sxs-lookup"><span data-stu-id="063b0-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="063b0-105">Хороший опыт отладки полагается на наличие отладочных символов, так как они предоставляют важную информацию, такую как связь между скомпилированным и исходным кодом, имена локальных переменных, трассировки стека и многое другое.</span><span class="sxs-lookup"><span data-stu-id="063b0-105">A good debugging experience relies on the presence of debug symbols as they provide critical information like the association between the compiled and the source code, names of local variables, stack traces, and more.</span></span> <span data-ttu-id="063b0-106">Пакеты символов (SNUPKG) можно использовать для распространения этих символов и улучшения возможностей отладки пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="063b0-106">You can use symbol packages (.snupkg) to distribute these symbols and improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="063b0-107">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="063b0-107">Prerequisites</span></span>

<span data-ttu-id="063b0-108">[nuget.exe 4.9.0 или более поздней версии](https://www.nuget.org/downloads) либо [dotnet CLI 2.2.0 или более поздней версии](https://www.microsoft.com/net/download/dotnet-core/2.2), которые реализуют необходимые [протоколы NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="063b0-108">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet CLI v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="063b0-109">Создание пакета символов</span><span class="sxs-lookup"><span data-stu-id="063b0-109">Creating a symbol package</span></span>

<span data-ttu-id="063b0-110">Если вы используете dotnet CLI или MSBuild, необходимо задать свойства `IncludeSymbols` и `SymbolPackageFormat`, чтобы создать SNUPKG-файл в дополнение к NUPKG-файлу.</span><span class="sxs-lookup"><span data-stu-id="063b0-110">If you're using dotnet CLI or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="063b0-111">Как вариант, добавьте следующие свойства в CSPROJ-файл.</span><span class="sxs-lookup"><span data-stu-id="063b0-111">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* <span data-ttu-id="063b0-112">Вы также можете указать эти свойства в командной строке.</span><span class="sxs-lookup"><span data-stu-id="063b0-112">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="063b0-113">или диспетчер конфигурации служб</span><span class="sxs-lookup"><span data-stu-id="063b0-113">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="063b0-114">Если вы используете NuGet.exe, вы можете с помощью следующих команд создать SNUPKG-файл в дополнение к NUPKG-файлу:</span><span class="sxs-lookup"><span data-stu-id="063b0-114">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="063b0-115">Свойство [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) может иметь одно из двух значений: `symbols.nupkg` (по умолчанию) или `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="063b0-115">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="063b0-116">Если значение этого свойства не указано, будет создан устаревший пакет символов.</span><span class="sxs-lookup"><span data-stu-id="063b0-116">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="063b0-117">Устаревший формат `.symbols.nupkg` все еще поддерживается, но только в целях совместимости как собственные пакеты (см. раздел [Устаревшие пакеты символов](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="063b0-117">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons like native packages (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="063b0-118">Сервер символов NuGet.org принимает только новый формат пакетов символов: `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="063b0-118">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="063b0-119">Публикация пакета символов</span><span class="sxs-lookup"><span data-stu-id="063b0-119">Publishing a symbol package</span></span>

1. <span data-ttu-id="063b0-120">Для удобства сначала сохраните ключ API с NuGet (см. раздел [Публикация пакета](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="063b0-120">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="063b0-121">После публикации основного пакета в nuget.org передайте пакет символов следующим образом.</span><span class="sxs-lookup"><span data-stu-id="063b0-121">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="063b0-122">Также можно выполнить принудительную отправку одновременно основного пакета и пакета символов, используя указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="063b0-122">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="063b0-123">Оба файла (.nupkg и .snupkg) должны находиться в текущей папке.</span><span class="sxs-lookup"><span data-stu-id="063b0-123">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="063b0-124">NuGet опубликует оба пакета на сайте nuget.org. Пакет `MyPackage.nupkg` будет опубликован первым, а `MyPackage.snupkg` — вторым.</span><span class="sxs-lookup"><span data-stu-id="063b0-124">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="063b0-125">Если пакет символов не опубликован, убедитесь, что вы настроили источник NuGet.org в виде `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="063b0-125">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="063b0-126">Публикация пакетов символов поддерживается только в [API NuGet версии 3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="063b0-126">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="063b0-127">Сервер символов NuGet.org</span><span class="sxs-lookup"><span data-stu-id="063b0-127">NuGet.org symbol server</span></span>

<span data-ttu-id="063b0-128">NuGet.org поддерживает собственный репозиторий сервера символов и принимает только новый формат пакетов символов: `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="063b0-128">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="063b0-129">Потребители пакетов могут добавить `https://symbols.nuget.org/download/symbols` в соответствующие источники символов в Visual Studio с помощью символов, опубликованных на сервер символов nuget.org, что позволяет осуществлять пошаговую отладку кода пакета в отладчике Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="063b0-129">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="063b0-130">Дополнительные сведения об этом процессе см. в разделе [Указание файлов символов (.pdb) и файлов с исходным кодом в отладчике Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).</span><span class="sxs-lookup"><span data-stu-id="063b0-130">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="063b0-131">Ограничения пакета символов NuGet.org</span><span class="sxs-lookup"><span data-stu-id="063b0-131">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="063b0-132">NuGet.org налагает на пакеты символов следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="063b0-132">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="063b0-133">В пакетах символов допускаются только следующие расширения файлов: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span><span class="sxs-lookup"><span data-stu-id="063b0-133">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="063b0-134">На сервере символов NuGet.org поддерживаются только управляемые [переносимые PDB-файлы](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md).</span><span class="sxs-lookup"><span data-stu-id="063b0-134">Only managed [Portable PDBs](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="063b0-135">Нужно выполнить сборку PDB-файлов и связанных с ними библиотек DLL NUPKG в компиляторе в Visual Studio версии 15.9 или более поздней (см. раздел [Хэш шифрования PDB-файлов](https://github.com/dotnet/roslyn/issues/24429)).</span><span class="sxs-lookup"><span data-stu-id="063b0-135">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="063b0-136">Пакеты символов, опубликованные в NuGet.org, не пройдут проверку, если указанные ограничения не соблюдаются.</span><span class="sxs-lookup"><span data-stu-id="063b0-136">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

> [!NOTE]
> <span data-ttu-id="063b0-137">Собственные проекты, например проекты C++, создают PDB-файлы Windows вместо переносимых PDB-файлов.</span><span class="sxs-lookup"><span data-stu-id="063b0-137">Native projects, such as C++ projects, produce Windows PDBs instead of Portable PDBs.</span></span> <span data-ttu-id="063b0-138">Сервер символов NuGet.org не поддерживает такие файлы.</span><span class="sxs-lookup"><span data-stu-id="063b0-138">These are not supported by NuGet.org's symbol server.</span></span> <span data-ttu-id="063b0-139">Вместо них следует использовать [устаревшие пакеты символов](Symbol-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="063b0-139">Please use [Legacy Symbol Packages](Symbol-Packages.md) instead.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="063b0-140">Проверка и индексирование пакета символов</span><span class="sxs-lookup"><span data-stu-id="063b0-140">Symbol package validation and indexing</span></span>

<span data-ttu-id="063b0-141">Пакеты символов, опубликованные в [NuGet.org](https://www.nuget.org/), проходят несколько проверок, включая проверку на наличие вредоносных программ.</span><span class="sxs-lookup"><span data-stu-id="063b0-141">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="063b0-142">Если пакет не проходит проверку, на странице сведений о нем отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="063b0-142">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="063b0-143">Кроме того, владельцы пакета получат сообщение электронной почты с инструкциями по устранению выявленных проблем.</span><span class="sxs-lookup"><span data-stu-id="063b0-143">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="063b0-144">После того как пакет символов пройдет все проверки, символы будут проиндексированы серверами символов NuGet.org и доступны для использования.</span><span class="sxs-lookup"><span data-stu-id="063b0-144">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers and will be available for consumption.</span></span>

<span data-ttu-id="063b0-145">Проверка и индексирование пакета обычно занимает около 15 минут.</span><span class="sxs-lookup"><span data-stu-id="063b0-145">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="063b0-146">Если публикация пакета занимает больше времени, перейдите на веб-сайт [status.nuget.org](https://status.nuget.org/) и убедитесь, что портал NuGet.org работает.</span><span class="sxs-lookup"><span data-stu-id="063b0-146">If the package publishing takes longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="063b0-147">Если все системы исправны, но пакет не был опубликован в течение часа, войдите на веб-сайт nuget.org и свяжитесь с нами по ссылке "Связаться со службой поддержки" на странице сведений о пакете.</span><span class="sxs-lookup"><span data-stu-id="063b0-147">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="063b0-148">Структура пакета символов</span><span class="sxs-lookup"><span data-stu-id="063b0-148">Symbol package structure</span></span>

<span data-ttu-id="063b0-149">Пакет символов (SNUPKG) имеет следующие характеристики:</span><span class="sxs-lookup"><span data-stu-id="063b0-149">The symbol package (.snupkg) has the following characteristics:</span></span>

1) <span data-ttu-id="063b0-150">SNUPKG-файл имеет тот же идентификатор и ту же версию, что и соответствующий пакет NuGet (NUPKG).</span><span class="sxs-lookup"><span data-stu-id="063b0-150">The .snupkg has the same id and version as its corresponding NuGet package (.nupkg).</span></span>
2) <span data-ttu-id="063b0-151">SNUPKG-файл имеет ту же структуру папок, что и соответствующий NUPKG-файл для всех DLL- и EXE-файлов, но вместо DLL- и EXE-файлов в ту же иерархию папок будут включены соответствующие PDB-файлы.</span><span class="sxs-lookup"><span data-stu-id="063b0-151">The .snupkg has the same folder structure as its corresponding .nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="063b0-152">Файлы и папки с расширениями, отличными от PDB, не войдут в пакет SNUPKG.</span><span class="sxs-lookup"><span data-stu-id="063b0-152">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="063b0-153">Файл пакета символов NUSPEC имеет тип пакета `SymbolsPackage`:</span><span class="sxs-lookup"><span data-stu-id="063b0-153">The symbol package's .nuspec file has the `SymbolsPackage` package type:</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="063b0-154">Если автор решит создать пакеты NUPKG и SNUPKG с помощью пользовательского NUSPEC-файла, пакет SNUPKG должен иметь иерархию папок и файлы, указанные в пункте 2).</span><span class="sxs-lookup"><span data-stu-id="063b0-154">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="063b0-155">Следующие поля будут исключены из NUSPEC-файла пакета SNUPKG: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl``` и ```icon```.</span><span class="sxs-lookup"><span data-stu-id="063b0-155">The following fields will be excluded from the snupkg's nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```, and  ```icon```.</span></span>
6) <span data-ttu-id="063b0-156">Не используйте элемент ```<license>```.</span><span class="sxs-lookup"><span data-stu-id="063b0-156">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="063b0-157">SNUPKG-файл рассматривается в рамках той же лицензии, что и соответствующий NUPKG-файл.</span><span class="sxs-lookup"><span data-stu-id="063b0-157">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="063b0-158">См. также статью</span><span class="sxs-lookup"><span data-stu-id="063b0-158">See also</span></span>

<span data-ttu-id="063b0-159">Чтобы обеспечить возможность отладки исходного кода сборок .NET, рекомендуется использовать Source Link.</span><span class="sxs-lookup"><span data-stu-id="063b0-159">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="063b0-160">Дополнительные сведения см. в [руководстве по Source Link](/dotnet/standard/library-guidance/sourcelink).</span><span class="sxs-lookup"><span data-stu-id="063b0-160">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="063b0-161">Дополнительные сведения о пакетах символов см. в проектной спецификации по [Отладка пакетов NuGet и улучшение символов](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements).</span><span class="sxs-lookup"><span data-stu-id="063b0-161">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
