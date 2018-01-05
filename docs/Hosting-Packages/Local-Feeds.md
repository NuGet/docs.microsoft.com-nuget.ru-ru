---
title: "Настройка локальных веб-каналов NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 1354a527-d988-43d1-8dcf-6ce46ec5d3d4
description: "Сведения о создании локального веб-канала для пакетов NuGet с помощью папок в локальной сети"
keywords: "веб-канал NuGet, коллекция NuGet, локальный веб-канал пакетов"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 32217622077ff983abaf00b2e6e5baf3064fff56
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="local-feeds"></a>Локальные веб-каналы

Локальные веб-каналы пакетов NuGet — это просто иерархические структуры папок в локальной сети (или даже просто на локальном компьютере), где размещаются пакеты. Эти веб-каналы можно использовать в качестве источников пакетов во всех других операциях NuGet с использованием интерфейса командной строки, пользовательского интерфейса диспетчера пакетов и консоли диспетчера пакетов.

Чтобы включить источник, добавьте путь к нему (например, `\\myserver\packages`) в список источников с помощью [пользовательского интерфейса диспетчера пакетов](../tools/package-manager-ui.md#package-sources) или команды [`nuget sources`](../tools/cli-ref-sources.md).

> [!Note]
> Иерархические структуры папок поддерживаются в NuGet 3.3+. Более старые версии NuGet используют лишь отдельную папку, содержащую пакеты, производительность которой значительно ниже, чем у иерархической структуры.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Инициализация и обслуживание иерархических папок

Дерево иерархических папок с версиями имеет следующую общую структуру:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

NuGet автоматически создает эту структуру, когда вы используете команду [`nuget add`](../tools/cli-ref-add.md) для копирования пакета в веб-канал:

```
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

Команда `nuget add` работает с одним пакетом за раз, что может быть неудобно при настройке веб-канала с несколькими пакетами.

В таких случаях используйте команду [`nuget init`](../tools/cli-ref-init.md), чтобы скопировать все пакеты из папки в веб-канал, как если бы вы запустили `nuget add` для каждого из них по отдельности. Например, следующая команда копирует все пакеты из `c:\packages` в иерархическое дерево в `\\myserver\packages`:

```
nuget init c:\packages \\myserver\packages
```

Как и в случае с командой `add`, `init` создает папку для каждого идентификатора пакета, каждый из которых содержит папку номера версии, внутри которой располагается соответствующий пакет.