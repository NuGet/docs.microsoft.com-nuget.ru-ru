---
title: Форматы анализатора платформы компилятора .NET для NuGet
description: Соглашения для анализаторов .NET, упакованных и распространяемых вместе с пакетами NuGet, которые реализуют API или библиотеку.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0a8db9f6c55b7e79f9b338119e0b3ac6cb7a1e35
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324803"
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="58ad3-103">Форматы анализаторов NuGet</span><span class="sxs-lookup"><span data-stu-id="58ad3-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="58ad3-104">.NET Compiler Platform (также называется «Roslyn») позволяет разработчикам создавать [анализаторы](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) , изучить дерево синтаксиса и семантику кода по мере его написания.</span><span class="sxs-lookup"><span data-stu-id="58ad3-104">The .NET Compiler Platform (also known as "Roslyn") allows developers to create [analyzers](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="58ad3-105">Это предоставляет разработчикам способ создания средства анализа для определенного домена, например те, которые могли бы помочь регулировать использование конкретного API или библиотеки.</span><span class="sxs-lookup"><span data-stu-id="58ad3-105">This provides developers with a way to create domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="58ad3-106">Дополнительные сведения см. на вики-сайте GitHub [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki).</span><span class="sxs-lookup"><span data-stu-id="58ad3-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="58ad3-107">Кроме того, см. статью [Использование Roslyn для создания динамического анализатора кода для своего API](https://msdn.microsoft.com/magazine/dn879356.aspx) в MSDN Magazine.</span><span class="sxs-lookup"><span data-stu-id="58ad3-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span></span>

<span data-ttu-id="58ad3-108">Анализаторы обычно упаковываются и распространяются в составе пакетов NuGet, реализующих соответствующий API или соответствующую библиотеку.</span><span class="sxs-lookup"><span data-stu-id="58ad3-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="58ad3-109">Хороший пример см. в пакете [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="58ad3-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="58ad3-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="58ad3-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="58ad3-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="58ad3-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="58ad3-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="58ad3-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="58ad3-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="58ad3-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="58ad3-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="58ad3-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="58ad3-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="58ad3-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="58ad3-116">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="58ad3-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="58ad3-117">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="58ad3-117">tools\install.ps1</span></span>
- <span data-ttu-id="58ad3-118">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="58ad3-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="58ad3-119">Как видите, вы помещаете библиотеки DLL анализатора в папку `analyzers` пакета.</span><span class="sxs-lookup"><span data-stu-id="58ad3-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="58ad3-120">Файлы PROPS, которые служат для отключения устаревших правил FxCop и использования вместо них реализации анализатора, помещаются в папку `build`.</span><span class="sxs-lookup"><span data-stu-id="58ad3-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="58ad3-121">Скрипты установки и удаления, которые поддерживают проекты, использующие `packages.config`, помещаются в `tools`.</span><span class="sxs-lookup"><span data-stu-id="58ad3-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="58ad3-122">Обратите внимание, что так как данный пакет не имеет требований для конкретной платформы, папка `platform` опускается.</span><span class="sxs-lookup"><span data-stu-id="58ad3-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="58ad3-123">Формат пути для анализаторов</span><span class="sxs-lookup"><span data-stu-id="58ad3-123">Analyzers path format</span></span>

<span data-ttu-id="58ad3-124">Работа с папкой `analyzers` осуществляется так же, как и с папкой, использовавшейся для [целевых платформ](../create-packages/supporting-multiple-target-frameworks.md), за исключением того, что описатели в пути описывают зависимости узла разработки, а не времени сборки.</span><span class="sxs-lookup"><span data-stu-id="58ad3-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="58ad3-125">Общий формат имеет следующий вид:</span><span class="sxs-lookup"><span data-stu-id="58ad3-125">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- <span data-ttu-id="58ad3-126">**framework_name**: *необязательная* контактная зона API платформы .NET Framework, которая нужна для выполнения содержащихся библиотек DLL.</span><span class="sxs-lookup"><span data-stu-id="58ad3-126">**framework_name**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="58ad3-127">Сейчас единственным допустимым значением является `dotnet`, так как запуск анализаторов возможен только на узле Roslyn.</span><span class="sxs-lookup"><span data-stu-id="58ad3-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="58ad3-128">Если целевой объект не указан, предполагается, что библиотеки DLL применяются ко *всем* целевым объектам.</span><span class="sxs-lookup"><span data-stu-id="58ad3-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="58ad3-129">**supported_language**: язык, для которого применяется библиотека DLL, один из `cs` (C#), `vb` (Visual Basic) и `fs` (F#).</span><span class="sxs-lookup"><span data-stu-id="58ad3-129">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="58ad3-130">Это значение указывает, что анализатор следует загружать только для проекта, использующего данный язык.</span><span class="sxs-lookup"><span data-stu-id="58ad3-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="58ad3-131">Если язык не указан, то предполагается, что библиотека DLL для применения к *все* языкам, поддерживающим анализаторы.</span><span class="sxs-lookup"><span data-stu-id="58ad3-131">If no language is specified then the DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="58ad3-132">**analyzer_name**: указывает библиотеки DLL анализатора.</span><span class="sxs-lookup"><span data-stu-id="58ad3-132">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="58ad3-133">Если нужны дополнительные файлы, кроме библиотек DLL, их следует включить с помощью файлов целевых объектов или свойств.</span><span class="sxs-lookup"><span data-stu-id="58ad3-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="58ad3-134">Скрипты установки и удаления</span><span class="sxs-lookup"><span data-stu-id="58ad3-134">Install and uninstall scripts</span></span>

<span data-ttu-id="58ad3-135">Если проект пользователя использует `packages.config`, сценарий MSBuild, который выбирает анализатор не запускается, поэтому следует поместить `install.ps1` и `uninstall.ps1` в `tools` папки с содержимым, которые описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="58ad3-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should place `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="58ad3-136">**Содержимое файла install.ps1**</span><span class="sxs-lookup"><span data-stu-id="58ad3-136">**install.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Install the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Install language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}
```


<span data-ttu-id="58ad3-137">**Содержимое файла uninstall.ps1**</span><span class="sxs-lookup"><span data-stu-id="58ad3-137">**uninstall.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                try
                {
                    $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
                }
                catch
                {

                }
            }
        }
    }
}
```
