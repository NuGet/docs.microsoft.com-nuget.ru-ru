---
title: Установка типа пакета NuGet
description: Здесь описаны типы пакетов для определения их назначения.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 990ac580f4031615566d78e359a24eaedaaf3e07
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774365"
---
# <a name="set-a-nuget-package-type"></a>Установка типа пакета NuGet

В NuGet 3.5 и более поздних версиях пакету можно присвоить определенный *тип пакета*, указывающий на его предполагаемое назначение. Пакеты, которым не назначен тип, включая все пакеты, созданные в более ранних версиях NuGet, по умолчанию имеют тип `Dependency`.

- Пакеты типа `Dependency` добавляют ресурсы времени сборки или времени выполнения в библиотеки и приложения, и их можно устанавливать в проектах любого типа (при условии, что они совместимы).

- Пакеты типа `DotnetTool` — это расширения [CLI dotnet](/dotnet/articles/core/tools/index), вызываемые из командной строки. Такие пакеты можно устанавливать только в проектах .NET Core, и они не влияют на операции восстановления. Дополнительные сведения об этих расширениях проекта можно найти в документации по [расширяемости .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).

- Пакеты типов `Template` предоставляют [пользовательские шаблоны](/dotnet/core/tools/custom-templates), которые можно использовать для создания файлов или проектов, таких как приложение, служба, средство или библиотека классов.

- Для пакетов пользовательского типа применяются произвольные идентификаторы, в которых соблюдаются те же правила формата, что и в идентификаторах пакетов. Типы, отличные от `Dependency` и `DotnetTool`, однако, не распознаются диспетчером пакетов NuGet в Visual Studio.

Типы пакетов задаются в файле `.nuspec`. В целях обратной совместимости лучше *не* задавать тип `Dependency` явным образом, позволив диспетчеру NuGet определить его автоматически, что происходит, если тип не указан.

- `.nuspec`: укажите тип пакета в узле `packageTypes\packageType` элемента `<metadata>`:

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
