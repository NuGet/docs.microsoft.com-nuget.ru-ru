---
title: Пределы скорости | Документы Microsoft
author:
- cmanu
- anangaur
ms.author:
- cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: API-интерфейсы NuGet будет обязательные пределы скорости для предотвращения нарушений.
keywords: Интенсивность NuGet интерфейса API, ограничение
ms.reviewer:
- skofman
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f7891d5e4c008219d9f4808f223f3e5e7ae06ced
ms.sourcegitcommit: fa40be739d093a37d5f7072b62ebdb4f595f4110
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/30/2018
---
# <a name="rate-limits"></a><span data-ttu-id="8831d-104">Ограничения скорости</span><span class="sxs-lookup"><span data-stu-id="8831d-104">Rate Limits</span></span>

<span data-ttu-id="8831d-105">NuGet.org API применяет ограничение скорости для предотвращения нарушений.</span><span class="sxs-lookup"><span data-stu-id="8831d-105">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="8831d-106">Запросы, превышающие ограничение частоты возвращает следующую ошибку:</span><span class="sxs-lookup"><span data-stu-id="8831d-106">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="8831d-107">В следующих таблицах перечислены ограничения скорости для NuGet.org API.</span><span class="sxs-lookup"><span data-stu-id="8831d-107">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="8831d-108">Поиск пакетов</span><span class="sxs-lookup"><span data-stu-id="8831d-108">Package search</span></span>

> [!Note]
> <span data-ttu-id="8831d-109">Мы рекомендуем использовать NuGet.org [API-интерфейсы V3](https://docs.microsoft.com/nuget/api/search-query-service-resource) для поиска, которые обращаются и не имеющие ограничить в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="8831d-109">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="8831d-110">Для V1 и V2 поиск интерфейсов API, followins ограничения относятся:</span><span class="sxs-lookup"><span data-stu-id="8831d-110">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="8831d-111">API</span><span class="sxs-lookup"><span data-stu-id="8831d-111">API</span></span> | <span data-ttu-id="8831d-112">Ограничение типа</span><span class="sxs-lookup"><span data-stu-id="8831d-112">Limit Type</span></span> | <span data-ttu-id="8831d-113">Предельное значение</span><span class="sxs-lookup"><span data-stu-id="8831d-113">Limit Value</span></span> | <span data-ttu-id="8831d-114">API usecase</span><span class="sxs-lookup"><span data-stu-id="8831d-114">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="8831d-115">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="8831d-115">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="8831d-116">IP</span><span class="sxs-lookup"><span data-stu-id="8831d-116">IP</span></span> | <span data-ttu-id="8831d-117">1000 / мин</span><span class="sxs-lookup"><span data-stu-id="8831d-117">1000 / minute</span></span> | <span data-ttu-id="8831d-118">Запросить метаданные пакета NuGet через v1 OData `Packages` коллекции</span><span class="sxs-lookup"><span data-stu-id="8831d-118">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="8831d-119">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="8831d-119">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="8831d-120">IP</span><span class="sxs-lookup"><span data-stu-id="8831d-120">IP</span></span> | <span data-ttu-id="8831d-121">3000 / мин</span><span class="sxs-lookup"><span data-stu-id="8831d-121">3000 / minute</span></span> | <span data-ttu-id="8831d-122">Поиск пакетов NuGet через конечную точку поиска v1</span><span class="sxs-lookup"><span data-stu-id="8831d-122">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="8831d-123">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="8831d-123">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="8831d-124">IP</span><span class="sxs-lookup"><span data-stu-id="8831d-124">IP</span></span> | <span data-ttu-id="8831d-125">20000 / мин</span><span class="sxs-lookup"><span data-stu-id="8831d-125">20000 / minute</span></span> | <span data-ttu-id="8831d-126">Запросить метаданные пакета NuGet через v2 OData `Packages` коллекции</span><span class="sxs-lookup"><span data-stu-id="8831d-126">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="8831d-127">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="8831d-127">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="8831d-128">IP</span><span class="sxs-lookup"><span data-stu-id="8831d-128">IP</span></span> | <span data-ttu-id="8831d-129">100 / мин</span><span class="sxs-lookup"><span data-stu-id="8831d-129">100 / minute</span></span> | <span data-ttu-id="8831d-130">Запросить число пакета NuGet через v2 OData `Packages` коллекции</span><span class="sxs-lookup"><span data-stu-id="8831d-130">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="8831d-131">Пакет Push и исключить</span><span class="sxs-lookup"><span data-stu-id="8831d-131">Package Push and Unlist</span></span>

| <span data-ttu-id="8831d-132">API</span><span class="sxs-lookup"><span data-stu-id="8831d-132">API</span></span> | <span data-ttu-id="8831d-133">Ограничение типа</span><span class="sxs-lookup"><span data-stu-id="8831d-133">Limit Type</span></span> | <span data-ttu-id="8831d-134">Предельное значение</span><span class="sxs-lookup"><span data-stu-id="8831d-134">Limit Value</span></span> | <span data-ttu-id="8831d-135">APU usecase</span><span class="sxs-lookup"><span data-stu-id="8831d-135">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="8831d-136">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="8831d-136">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="8831d-137">Ключ API</span><span class="sxs-lookup"><span data-stu-id="8831d-137">API Key</span></span> | <span data-ttu-id="8831d-138">100 / мин</span><span class="sxs-lookup"><span data-stu-id="8831d-138">100 / minute</span></span> | <span data-ttu-id="8831d-139">Отправьте новый пакет NuGet (версия) через конечную точку принудительной v2</span><span class="sxs-lookup"><span data-stu-id="8831d-139">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="8831d-140">**УДАЛИТЬ** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="8831d-140">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="8831d-141">Ключ API</span><span class="sxs-lookup"><span data-stu-id="8831d-141">API Key</span></span> | <span data-ttu-id="8831d-142">100 / мин</span><span class="sxs-lookup"><span data-stu-id="8831d-142">100 / minute</span></span> | <span data-ttu-id="8831d-143">Исключить пакет NuGet (версия) через конечную точку v2</span><span class="sxs-lookup"><span data-stu-id="8831d-143">Unlist a NuGet package (version) via v2 endpoint</span></span> 
