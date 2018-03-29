---
title: Форматы анализаторов .NET Compiler Platform для NuGet | Документы Майкрософт
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Соглашения для анализаторов .NET, упакованных и распространяемых вместе с пакетами NuGet, которые реализуют API или библиотеку.
keywords: соглашения для анализаторов NuGet, анализаторы .NET, NuGet и .NET Compiler Platform, NuGet и Roslyn
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 26e40346b1d76d2f4f0e4177dbe0670f10db164c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="analyzer-nuget-formats"></a>Форматы анализаторов NuGet

Платформой компилятора .NET (также называется «Roslyn») дает разработчикам возможность создавать [анализаторы] (https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) , просмотреть дерево синтаксиса и семантики кода, как выполняется запись. Благодаря этому разработчики могут создавать средства анализа для определенного домена, например, способные регулировать использование конкретного API или конкретной библиотеки. Дополнительные сведения см. на вики-сайте GitHub [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki). Кроме того, см. статью [Использование Roslyn для создания динамического анализатора кода для своего API](https://msdn.microsoft.com/magazine/dn879356.aspx) в MSDN Magazine.

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

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}}/{analyzer_name}.dll

- **framework_name**: *необязательная* контактная зона API платформы .NET Framework, которая нужна для выполнения содержащихся библиотек DLL. Сейчас единственным допустимым значением является `dotnet`, так как запуск анализаторов возможен только на узле Roslyn. Если целевой объект не указан, предполагается, что библиотеки DLL применяются ко *всем* целевым объектам.
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
