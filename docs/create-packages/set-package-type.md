---
title: Установка типа пакета NuGet
description: Здесь описаны типы пакетов для определения их назначения.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1d869f616ce0291cf1c0a17b7ff20fc61e6a3bd5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230828"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="65cf3-103">Установка типа пакета NuGet</span><span class="sxs-lookup"><span data-stu-id="65cf3-103">Set a NuGet package type</span></span>

<span data-ttu-id="65cf3-104">В NuGet 3.5 и более поздних версиях пакету можно присвоить определенный *тип пакета*, указывающий на его предполагаемое назначение.</span><span class="sxs-lookup"><span data-stu-id="65cf3-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="65cf3-105">Пакеты, которым не назначен тип, включая все пакеты, созданные в более ранних версиях NuGet, по умолчанию имеют тип `Dependency`.</span><span class="sxs-lookup"><span data-stu-id="65cf3-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="65cf3-106">Пакеты типа `Dependency` добавляют ресурсы времени сборки или времени выполнения в библиотеки и приложения, и их можно устанавливать в проектах любого типа (при условии, что они совместимы).</span><span class="sxs-lookup"><span data-stu-id="65cf3-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="65cf3-107">Пакеты типа `DotnetTool` — это расширения [CLI dotnet](/dotnet/articles/core/tools/index), вызываемые из командной строки.</span><span class="sxs-lookup"><span data-stu-id="65cf3-107">`DotnetTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="65cf3-108">Такие пакеты можно устанавливать только в проектах .NET Core, и они не влияют на операции восстановления.</span><span class="sxs-lookup"><span data-stu-id="65cf3-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="65cf3-109">Дополнительные сведения об этих расширениях проекта можно найти в документации по [расширяемости .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).</span><span class="sxs-lookup"><span data-stu-id="65cf3-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="65cf3-110">Пакеты типов `Template` предоставляют [пользовательские шаблоны](/dotnet/core/tools/custom-templates), которые можно использовать для создания файлов или проектов, таких как приложение, служба, средство или библиотека классов.</span><span class="sxs-lookup"><span data-stu-id="65cf3-110">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

- <span data-ttu-id="65cf3-111">Для пакетов пользовательского типа применяются произвольные идентификаторы, в которых соблюдаются те же правила формата, что и в идентификаторах пакетов.</span><span class="sxs-lookup"><span data-stu-id="65cf3-111">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="65cf3-112">Типы, отличные от `Dependency` и `DotnetTool`, однако, не распознаются диспетчером пакетов NuGet в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="65cf3-112">Any type other than `Dependency` and `DotnetTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="65cf3-113">Типы пакетов задаются в файле `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="65cf3-113">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="65cf3-114">В целях обратной совместимости лучше *не* задавать тип `Dependency` явным образом, позволив диспетчеру NuGet определить его автоматически, что происходит, если тип не указан.</span><span class="sxs-lookup"><span data-stu-id="65cf3-114">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="65cf3-115">`.nuspec`: укажите тип пакета в узле `packageTypes\packageType` элемента `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="65cf3-115">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
