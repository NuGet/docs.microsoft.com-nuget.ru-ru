---
title: Установка типа пакета NuGet
description: Здесь описаны типы пакетов для определения их назначения.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 22e8ac2e9e2086a1280c5b0c3be8a032b7998b36
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036920"
---
# <a name="set-a-nuget-package-type"></a>Установка типа пакета NuGet

В NuGet 3.5 и более поздних версиях пакету можно присвоить определенный *тип пакета*, указывающий на его предполагаемое назначение. Пакеты, которым не назначен тип, включая все пакеты, созданные в более ранних версиях NuGet, по умолчанию имеют тип `Dependency`.

- Пакеты типа `Dependency` добавляют ресурсы времени сборки или времени выполнения в библиотеки и приложения, и их можно устанавливать в проектах любого типа (при условии, что они совместимы).

- Пакеты типа `DotnetTool` — это расширения [CLI dotnet](/dotnet/articles/core/tools/index), вызываемые из командной строки. Такие пакеты можно устанавливать только в проектах .NET Core, и они не влияют на операции восстановления. Дополнительные сведения об этих расширениях проекта можно найти в документации по [расширяемости .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).

- Пакеты типов `Template` предоставляют [пользовательские шаблоны](/dotnet/core/tools/custom-templates), которые можно использовать для создания файлов или проектов, таких как приложение, служба, средство или библиотека классов.

- Для пакетов пользовательского типа применяются произвольные идентификаторы, в которых соблюдаются те же правила формата, что и в идентификаторах пакетов. Типы, отличные от `Dependency` и `DotnetTool`, однако, не распознаются диспетчером пакетов NuGet в Visual Studio.

Типы пакетов задаются в файле `.nuspec`. В целях обратной совместимости лучше *не* задавать тип `Dependency` явным образом, позволив диспетчеру NuGet определить его автоматически, что происходит, если тип не указан.

- `.nuspec`. укажите тип пакета в узле `packageTypes\packageType` элемента `<metadata>`.

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
