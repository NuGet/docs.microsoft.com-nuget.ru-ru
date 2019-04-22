---
title: Пакет SDK для клиента NuGet
description: API-Интерфейс является развивающейся и еще не рассматриваются, но примеры доступны в блоге Дэйв Глику.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 8f96bf289e8121fd25262fb95c2f36dfc89045c5
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911040"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="2f35b-103">Пакет SDK для клиента NuGet</span><span class="sxs-lookup"><span data-stu-id="2f35b-103">NuGet Client SDK</span></span>

> [!Note]
> <span data-ttu-id="2f35b-104">Не следует путать с [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span><span class="sxs-lookup"><span data-stu-id="2f35b-104">Not to be confused with the [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span></span>

<span data-ttu-id="2f35b-105">*Пакет SDK для клиента NuGet* относится к группе библиотек .NET вокруг [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), и [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="2f35b-105">The *NuGet Client SDK* refers to a group of .NET libraries centered around [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="2f35b-106">Эти пакеты замените раннюю [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) библиотеки.</span><span class="sxs-lookup"><span data-stu-id="2f35b-106">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

<span data-ttu-id="2f35b-107">Мы работаем над наличие стабильной контактную зону, который мы скоро документировать.</span><span class="sxs-lookup"><span data-stu-id="2f35b-107">We are working on having a stable surface area that we can document soon.</span></span>

## <a name="source-code"></a><span data-ttu-id="2f35b-108">Исходный код</span><span class="sxs-lookup"><span data-stu-id="2f35b-108">Source code</span></span>

<span data-ttu-id="2f35b-109">Исходный код публикуется на сайте GitHub в проекте [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span><span class="sxs-lookup"><span data-stu-id="2f35b-109">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="2f35b-110">Документацией</span><span class="sxs-lookup"><span data-stu-id="2f35b-110">Third-party documentation</span></span>

<span data-ttu-id="2f35b-111">Примеры и документация для некоторые API-Интерфейсы можно найти в следующей серии публикаций в блоге, Дэйв Глику, опубликованные 2016:</span><span class="sxs-lookup"><span data-stu-id="2f35b-111">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="2f35b-112">Изучение библиотек NuGet v3, часть 1: Введение и основные понятия</span><span class="sxs-lookup"><span data-stu-id="2f35b-112">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="2f35b-113">Изучение библиотек NuGet v3, часть 2: Поиск пакетов</span><span class="sxs-lookup"><span data-stu-id="2f35b-113">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="2f35b-114">Изучение библиотек NuGet v3, часть 3: Установка пакетов</span><span class="sxs-lookup"><span data-stu-id="2f35b-114">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="2f35b-115">Эти сообщения в блогах были написаны вскоре после **3.4.3** версию NuGet, выпущенные пакеты SDK для клиента.</span><span class="sxs-lookup"><span data-stu-id="2f35b-115">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="2f35b-116">Более новые версии пакетов могут быть несовместимы с информацией в записях блога.</span><span class="sxs-lookup"><span data-stu-id="2f35b-116">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="2f35b-117">Мартин Björkström сделали исполнению блога к серии публикаций в блоге Дэйв Глику, где он представляет другой подход по использованию клиентский пакет SDK NuGet для установки пакетов NuGet:</span><span class="sxs-lookup"><span data-stu-id="2f35b-117">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="2f35b-118">Возвращаясь к библиотек NuGet v3</span><span class="sxs-lookup"><span data-stu-id="2f35b-118">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
