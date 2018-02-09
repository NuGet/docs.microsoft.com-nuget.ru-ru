---
title: "Настройка локальных веб-каналов NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Сведения о создании локального веб-канала для пакетов NuGet с помощью папок в локальной сети"
keywords: "веб-канал NuGet, коллекция NuGet, локальный веб-канал пакетов"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0b8633db78b19fecddeb057a9f287ef971aef27a
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2018
---
# <a name="local-feeds"></a><span data-ttu-id="1959f-104">Локальные веб-каналы</span><span class="sxs-lookup"><span data-stu-id="1959f-104">Local feeds</span></span>

<span data-ttu-id="1959f-105">Локальные веб-каналы пакетов NuGet — это просто иерархические структуры папок в локальной сети (или даже просто на локальном компьютере), где размещаются пакеты.</span><span class="sxs-lookup"><span data-stu-id="1959f-105">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="1959f-106">Эти веб-каналы можно использовать в качестве источников пакетов во всех других операциях NuGet с использованием интерфейса командной строки, пользовательского интерфейса диспетчера пакетов и консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="1959f-106">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="1959f-107">Чтобы включить источник, добавьте путь к нему (например, `\\myserver\packages`) в список источников с помощью [пользовательского интерфейса диспетчера пакетов](../tools/package-manager-ui.md#package-sources) или команды [`nuget sources`](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="1959f-107">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../tools/package-manager-ui.md#package-sources) or the [`nuget sources`](../tools/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="1959f-108">Иерархические структуры папок поддерживаются в NuGet 3.3+.</span><span class="sxs-lookup"><span data-stu-id="1959f-108">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="1959f-109">Более старые версии NuGet используют лишь отдельную папку, содержащую пакеты, производительность которой значительно ниже, чем у иерархической структуры.</span><span class="sxs-lookup"><span data-stu-id="1959f-109">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="1959f-110">Инициализация и обслуживание иерархических папок</span><span class="sxs-lookup"><span data-stu-id="1959f-110">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="1959f-111">Дерево иерархических папок с версиями имеет следующую общую структуру:</span><span class="sxs-lookup"><span data-stu-id="1959f-111">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="1959f-112">NuGet автоматически создает эту структуру, когда вы используете команду [`nuget add`](../tools/cli-ref-add.md) для копирования пакета в веб-канал:</span><span class="sxs-lookup"><span data-stu-id="1959f-112">NuGet creates this structure automatically when you use the [`nuget add`](../tools/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="1959f-113">Команда `nuget add` работает с одним пакетом за раз, что может быть неудобно при настройке веб-канала с несколькими пакетами.</span><span class="sxs-lookup"><span data-stu-id="1959f-113">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="1959f-114">В таких случаях используйте команду [`nuget init`](../tools/cli-ref-init.md), чтобы скопировать все пакеты из папки в веб-канал, как если бы вы запустили `nuget add` для каждого из них по отдельности.</span><span class="sxs-lookup"><span data-stu-id="1959f-114">In such cases, use the [`nuget init`](../tools/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="1959f-115">Например, следующая команда копирует все пакеты из `c:\packages` в иерархическое дерево в `\\myserver\packages`:</span><span class="sxs-lookup"><span data-stu-id="1959f-115">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="1959f-116">Как и в случае с командой `add`, `init` создает папку для каждого идентификатора пакета, каждый из которых содержит папку номера версии, внутри которой располагается соответствующий пакет.</span><span class="sxs-lookup"><span data-stu-id="1959f-116">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
