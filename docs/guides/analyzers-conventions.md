---
title: Форматы анализаторов .NET Compiler Platform для NuGet
description: Соглашения для анализаторов .NET, упакованных и распространяемых вместе с пакетами NuGet, которые реализуют API или библиотеку.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 63880b6b9bbfe6aac9cc6419d6a972062eea3495
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774133"
---
# <a name="analyzer-nuget-formats"></a>Форматы анализаторов NuGet

.NET Compiler Platform (также называется Roslyn) позволяет разработчикам создавать [анализаторы](https://github.com/dotnet/roslyn/blob/master/docs/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix.md), которые проверяют дерево синтаксиса и семантику кода по мере его написания. Благодаря этому разработчики могут создавать средства анализа для определенного домена, например, способные регулировать использование конкретного API или конкретной библиотеки. Дополнительные сведения см. на вики-сайте GitHub [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki). Кроме того, см. статью [Использование Roslyn для создания динамического анализатора кода для своего API](/archive/msdn-magazine/2014/special-issue/csharp-and-visual-basic-use-roslyn-to-write-a-live-code-analyzer-for-your-api) в MSDN Magazine.

Анализаторы обычно упаковываются и распространяются в составе пакетов NuGet, реализующих соответствующий API или соответствующую библиотеку.

Хороший пример см. в пакете [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) со следующим содержимым:

- analyzers\dotnet\System.Runtime.Analyzers.dll
- analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- tools\install.ps1
- tools\uninstall.ps1

Как видите, вы помещаете библиотеки DLL анализатора в папку `analyzers` пакета.

Файлы PROPS, которые служат для отключения устаревших правил FxCop и использования вместо них реализации анализатора, помещаются в папку `build`.

Скрипты установки и удаления, которые поддерживают проекты, использующие `packages.config`, помещаются в `tools`.

Обратите внимание, что так как данный пакет не имеет требований для конкретной платформы, папка `platform` опускается.


## <a name="analyzers-path-format"></a>Формат пути для анализаторов

Работа с папкой `analyzers` осуществляется так же, как и с папкой, использовавшейся для [целевых платформ](../create-packages/supporting-multiple-target-frameworks.md), за исключением того, что описатели в пути описывают зависимости узла разработки, а не времени сборки. Общий формат имеет следующий вид:

```
$/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll
```

- **framework_name** и **version**: *необязательная* контактная зона API платформы .NET Framework, которая нужна для выполнения содержащихся библиотек DLL. Сейчас единственным допустимым значением является `dotnet`, так как запуск анализаторов возможен только на узле Roslyn. Если целевой объект не указан, предполагается, что библиотеки DLL применяются ко *всем* целевым объектам.
- **supported_language**: язык, для которого применяется библиотека DLL, один из `cs` (C#), `vb` (Visual Basic) и `fs` (F#). Это значение указывает, что анализатор следует загружать только для проекта, использующего данный язык. Если язык не указан, предполагается, что библиотека DLL применяется ко *всем* языкам, поддерживающим анализаторы.
- **analyzer_name**: указывает библиотеки DLL анализатора. Если нужны дополнительные файлы, кроме библиотек DLL, их следует включить с помощью файлов целевых объектов или свойств.


## <a name="install-and-uninstall-scripts"></a>Скрипты установки и удаления

Если проект пользователя использует `packages.config`, скрипт MSBuild, который выбирает анализатор, не запускается, поэтому вам нужно использовать `install.ps1` и `uninstall.ps1` в папке `tools` с содержимым, описанным ниже.

**Содержимое файла install.ps1**

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


**Содержимое файла uninstall.ps1**

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
