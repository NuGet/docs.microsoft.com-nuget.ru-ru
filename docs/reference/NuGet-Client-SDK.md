---
title: Пакет SDK клиента NuGet
description: API развивается и еще не документирован, но примеры доступны в блоге Дейв Гликк.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 873bde467a39653b818b49173d53bc983e99d1b9
ms.sourcegitcommit: f9645fc5f49c18978e12a292a3f832e162e069d5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2019
ms.locfileid: "72924605"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="e757d-103">Пакет SDK клиента NuGet</span><span class="sxs-lookup"><span data-stu-id="e757d-103">NuGet Client SDK</span></span>

<span data-ttu-id="e757d-104">*Клиентский пакет SDK для NuGet* ссылается на группу пакетов NuGet, которые находятся в центре по отношению к [NuGet. Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet. Packaging](https://www.nuget.org/packages/NuGet.Packaging)и [NuGet. Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="e757d-104">The *NuGet Client SDK* refers to a group of NuGet packages centered around [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="e757d-105">Эти пакеты заменяют предыдущую библиотеку [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/) .</span><span class="sxs-lookup"><span data-stu-id="e757d-105">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

> [!Note]
>  <span data-ttu-id="e757d-106">Документацию по протоколу сервера NuGet см. в [API сервера NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="e757d-106">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="source-code"></a><span data-ttu-id="e757d-107">Исходный код</span><span class="sxs-lookup"><span data-stu-id="e757d-107">Source code</span></span>

<span data-ttu-id="e757d-108">Исходный код публикуется на сайте GitHub в проекте [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client).</span><span class="sxs-lookup"><span data-stu-id="e757d-108">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="e757d-109">Документация по сторонним производителям</span><span class="sxs-lookup"><span data-stu-id="e757d-109">Third-party documentation</span></span>

<span data-ttu-id="e757d-110">Примеры и документацию для некоторых API-интерфейсов можно найти в следующем ряде блогов: Дейв Гликк, Опубликовано 2016.</span><span class="sxs-lookup"><span data-stu-id="e757d-110">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="e757d-111">Изучение библиотек NuGet версии 3, часть 1. Введение и основные понятия</span><span class="sxs-lookup"><span data-stu-id="e757d-111">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="e757d-112">Изучение библиотек NuGet версии 3. часть 2. Поиск пакетов</span><span class="sxs-lookup"><span data-stu-id="e757d-112">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="e757d-113">Изучение библиотек NuGet v3, часть 3. Установка пакетов</span><span class="sxs-lookup"><span data-stu-id="e757d-113">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="e757d-114">Эти записи блога были написаны вскоре после выпуска **3.4.3** версии пакетов SDK клиента NuGet.</span><span class="sxs-lookup"><span data-stu-id="e757d-114">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="e757d-115">Более новые версии пакетов могут быть несовместимы с данными в записях блога.</span><span class="sxs-lookup"><span data-stu-id="e757d-115">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="e757d-116">"Мартен Бжöркстрöм" выполнил следующую запись блога в серии блогов Дейв Гликк, где он вводит другой подход к использованию пакета SDK клиента NuGet для установки пакетов NuGet:</span><span class="sxs-lookup"><span data-stu-id="e757d-116">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="e757d-117">Повторное посещение библиотек NuGet v3</span><span class="sxs-lookup"><span data-stu-id="e757d-117">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
