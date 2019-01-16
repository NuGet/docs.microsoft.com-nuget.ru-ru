---
title: Пакет SDK для клиента NuGet
description: API-Интерфейс является развивающейся и еще не рассматриваются, но примеры доступны в блоге Дэйв Глику.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 97ed3ec7d41d2847c0521af69373a1871eb585dd
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324686"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="1e912-103">Пакет SDK для клиента NuGet</span><span class="sxs-lookup"><span data-stu-id="1e912-103">NuGet Client SDK</span></span>

> [!Note]
> <span data-ttu-id="1e912-104">Не следует путать с [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span><span class="sxs-lookup"><span data-stu-id="1e912-104">Not to be confused with the [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span></span>

<span data-ttu-id="1e912-105">*Пакет SDK для клиента NuGet* относится к группе библиотек .NET вокруг [NuGet.Client](https://www.nuget.org/packages/NuGet.Client), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), и [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="1e912-105">The *NuGet Client SDK* refers to a group of .NET libraries centered around [NuGet.Client](https://www.nuget.org/packages/NuGet.Client), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="1e912-106">Эти пакеты замените раннюю [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) библиотеки.</span><span class="sxs-lookup"><span data-stu-id="1e912-106">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

<span data-ttu-id="1e912-107">Мы работаем над наличие стабильной контактную зону, который мы скоро документировать.</span><span class="sxs-lookup"><span data-stu-id="1e912-107">We are working on having a stable surface area that we can document soon.</span></span>

## <a name="source-code"></a><span data-ttu-id="1e912-108">Исходный код</span><span class="sxs-lookup"><span data-stu-id="1e912-108">Source code</span></span>

<span data-ttu-id="1e912-109">Исходный код публикуется на сайте GitHub в проекте [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span><span class="sxs-lookup"><span data-stu-id="1e912-109">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="1e912-110">Документацией</span><span class="sxs-lookup"><span data-stu-id="1e912-110">Third-party documentation</span></span>

<span data-ttu-id="1e912-111">Примеры и документация для некоторые API-Интерфейсы можно найти в следующей серии публикаций в блоге, Дэйв Глику, опубликованные 2016:</span><span class="sxs-lookup"><span data-stu-id="1e912-111">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="1e912-112">Изучение библиотек NuGet v3, часть 1: Введение и основные понятия</span><span class="sxs-lookup"><span data-stu-id="1e912-112">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="1e912-113">Изучение библиотек NuGet v3, часть 2: Поиск пакетов</span><span class="sxs-lookup"><span data-stu-id="1e912-113">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="1e912-114">Изучение библиотек NuGet v3, часть 3: Установка пакетов</span><span class="sxs-lookup"><span data-stu-id="1e912-114">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="1e912-115">Эти сообщения в блогах были написаны вскоре после **3.4.3** версию NuGet, выпущенные пакеты SDK для клиента.</span><span class="sxs-lookup"><span data-stu-id="1e912-115">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="1e912-116">Более новые версии пакетов могут быть несовместимы с информацией в записях блога.</span><span class="sxs-lookup"><span data-stu-id="1e912-116">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="1e912-117">Мартин Björkström сделали исполнению блога к серии публикаций в блоге Дэйв Глику, где он представляет другой подход по использованию клиентский пакет SDK NuGet для установки пакетов NuGet:</span><span class="sxs-lookup"><span data-stu-id="1e912-117">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="1e912-118">Возвращаясь к библиотек NuGet v3</span><span class="sxs-lookup"><span data-stu-id="1e912-118">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
