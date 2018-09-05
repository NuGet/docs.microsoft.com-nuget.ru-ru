---
title: Ограничения, NuGet API скорости
description: API-интерфейсы NuGet будет обязательные ограничения скорости, чтобы избежать злонамеренного использования.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548681"
---
# <a name="rate-limits"></a><span data-ttu-id="49c48-103">Ограничения скорости</span><span class="sxs-lookup"><span data-stu-id="49c48-103">Rate Limits</span></span>

<span data-ttu-id="49c48-104">NuGet.org API применяет ограничение скорости, чтобы избежать злонамеренного использования.</span><span class="sxs-lookup"><span data-stu-id="49c48-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="49c48-105">Запросы, которые превышают ограничение частоты возвращает следующую ошибку:</span><span class="sxs-lookup"><span data-stu-id="49c48-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="49c48-106">В дополнение к регулирование с помощью ограничений скорости запросов некоторые API-интерфейсы также обеспечивают квоты.</span><span class="sxs-lookup"><span data-stu-id="49c48-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="49c48-107">Запросы, которые превышают квоту возвращает следующую ошибку:</span><span class="sxs-lookup"><span data-stu-id="49c48-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="49c48-108">В следующих таблицах перечислены ограничения скорости для NuGet.org API.</span><span class="sxs-lookup"><span data-stu-id="49c48-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="49c48-109">Поиск пакетов</span><span class="sxs-lookup"><span data-stu-id="49c48-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="49c48-110">Мы рекомендуем использовать для NuGet.org [API-интерфейсы V3](https://docs.microsoft.com/nuget/api/search-query-service-resource) для поиска, который обладает низкой производительностью и каких-либо ограничения в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="49c48-110">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="49c48-111">Для версий 1 и 2 поиска API-интерфейсы, followins ограничения относятся:</span><span class="sxs-lookup"><span data-stu-id="49c48-111">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="49c48-112">API</span><span class="sxs-lookup"><span data-stu-id="49c48-112">API</span></span> | <span data-ttu-id="49c48-113">Тип ограничения</span><span class="sxs-lookup"><span data-stu-id="49c48-113">Limit Type</span></span> | <span data-ttu-id="49c48-114">Предельное значение</span><span class="sxs-lookup"><span data-stu-id="49c48-114">Limit Value</span></span> | <span data-ttu-id="49c48-115">API usecase</span><span class="sxs-lookup"><span data-stu-id="49c48-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="49c48-116">**ПОЛУЧИТЬ** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="49c48-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="49c48-117">IP</span><span class="sxs-lookup"><span data-stu-id="49c48-117">IP</span></span> | <span data-ttu-id="49c48-118">1000 / мин</span><span class="sxs-lookup"><span data-stu-id="49c48-118">1000 / minute</span></span> | <span data-ttu-id="49c48-119">Запросить метаданные пакета NuGet с помощью v1 OData `Packages` коллекции</span><span class="sxs-lookup"><span data-stu-id="49c48-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="49c48-120">**ПОЛУЧИТЬ** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="49c48-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="49c48-121">IP</span><span class="sxs-lookup"><span data-stu-id="49c48-121">IP</span></span> | <span data-ttu-id="49c48-122">3000 / мин</span><span class="sxs-lookup"><span data-stu-id="49c48-122">3000 / minute</span></span> | <span data-ttu-id="49c48-123">Поиск пакетов NuGet через конечную точку версии 1 поиска</span><span class="sxs-lookup"><span data-stu-id="49c48-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="49c48-124">**ПОЛУЧИТЬ** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="49c48-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="49c48-125">IP</span><span class="sxs-lookup"><span data-stu-id="49c48-125">IP</span></span> | <span data-ttu-id="49c48-126">20000 / мин</span><span class="sxs-lookup"><span data-stu-id="49c48-126">20000 / minute</span></span> | <span data-ttu-id="49c48-127">Запросить метаданные пакета NuGet с помощью v2 OData `Packages` коллекции</span><span class="sxs-lookup"><span data-stu-id="49c48-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="49c48-128">**ПОЛУЧИТЬ** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="49c48-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="49c48-129">IP</span><span class="sxs-lookup"><span data-stu-id="49c48-129">IP</span></span> | <span data-ttu-id="49c48-130">100 / мин</span><span class="sxs-lookup"><span data-stu-id="49c48-130">100 / minute</span></span> | <span data-ttu-id="49c48-131">Запрос количества пакетов NuGet с помощью v2 OData `Packages` коллекции</span><span class="sxs-lookup"><span data-stu-id="49c48-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="49c48-132">Пакет Push-уведомлений и удалить из списка</span><span class="sxs-lookup"><span data-stu-id="49c48-132">Package Push and Unlist</span></span>

| <span data-ttu-id="49c48-133">API</span><span class="sxs-lookup"><span data-stu-id="49c48-133">API</span></span> | <span data-ttu-id="49c48-134">Тип ограничения</span><span class="sxs-lookup"><span data-stu-id="49c48-134">Limit Type</span></span> | <span data-ttu-id="49c48-135">Предельное значение</span><span class="sxs-lookup"><span data-stu-id="49c48-135">Limit Value</span></span> | <span data-ttu-id="49c48-136">API usecase</span><span class="sxs-lookup"><span data-stu-id="49c48-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="49c48-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="49c48-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="49c48-138">Ключ API</span><span class="sxs-lookup"><span data-stu-id="49c48-138">API Key</span></span> | <span data-ttu-id="49c48-139">250 / час</span><span class="sxs-lookup"><span data-stu-id="49c48-139">250 / hour</span></span> | <span data-ttu-id="49c48-140">Отправьте новый пакет NuGet (версии) с помощью конечной точки версии 2 Push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="49c48-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="49c48-141">**УДАЛЕНИЕ** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="49c48-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="49c48-142">Ключ API</span><span class="sxs-lookup"><span data-stu-id="49c48-142">API Key</span></span> | <span data-ttu-id="49c48-143">250 / час</span><span class="sxs-lookup"><span data-stu-id="49c48-143">250 / hour</span></span> | <span data-ttu-id="49c48-144">Удалить из списка пакет NuGet (версии) с помощью конечной точки версии 2</span><span class="sxs-lookup"><span data-stu-id="49c48-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
