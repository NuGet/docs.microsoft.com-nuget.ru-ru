---
title: Пределы скорости, API NuGet
description: Интерфейсы API NuGet применяют ограничения скорости для предотвращения нарушения.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813199"
---
# <a name="rate-limits"></a><span data-ttu-id="ac6e1-103">Ограничения скорости</span><span class="sxs-lookup"><span data-stu-id="ac6e1-103">Rate Limits</span></span>

<span data-ttu-id="ac6e1-104">API NuGet.org обеспечивает ограничение скорости для предотвращения нарушения.</span><span class="sxs-lookup"><span data-stu-id="ac6e1-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="ac6e1-105">Запросы, превышающие предел скорости, возвращают следующую ошибку:</span><span class="sxs-lookup"><span data-stu-id="ac6e1-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="ac6e1-106">Помимо регулирования запросов с использованием пределов скорости, некоторые API также применяют квоту.</span><span class="sxs-lookup"><span data-stu-id="ac6e1-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="ac6e1-107">Запросы, превышающие квоту, возвращают следующую ошибку:</span><span class="sxs-lookup"><span data-stu-id="ac6e1-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="ac6e1-108">В следующих таблицах перечислены ограничения скорости для API NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="ac6e1-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="ac6e1-109">Поиск пакета</span><span class="sxs-lookup"><span data-stu-id="ac6e1-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="ac6e1-110">Мы рекомендуем использовать API-интерфейсы для [поиска версии 3](search-query-service-resource.md) NuGet. org, так как в настоящее время это не слишком мало частоты.</span><span class="sxs-lookup"><span data-stu-id="ac6e1-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="ac6e1-111">Для API-интерфейсов поиска v1 и v2 применяются следующие ограничения.</span><span class="sxs-lookup"><span data-stu-id="ac6e1-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="ac6e1-112">API</span><span class="sxs-lookup"><span data-stu-id="ac6e1-112">API</span></span> | <span data-ttu-id="ac6e1-113">Тип ограничения</span><span class="sxs-lookup"><span data-stu-id="ac6e1-113">Limit Type</span></span> | <span data-ttu-id="ac6e1-114">Значение ограничения</span><span class="sxs-lookup"><span data-stu-id="ac6e1-114">Limit Value</span></span> | <span data-ttu-id="ac6e1-115">API UseCase</span><span class="sxs-lookup"><span data-stu-id="ac6e1-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="ac6e1-116">**Получить** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="ac6e1-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="ac6e1-117">IP</span><span class="sxs-lookup"><span data-stu-id="ac6e1-117">IP</span></span> | <span data-ttu-id="ac6e1-118">1000/мин</span><span class="sxs-lookup"><span data-stu-id="ac6e1-118">1000 / minute</span></span> | <span data-ttu-id="ac6e1-119">Запрос метаданных пакета NuGet через v1 `Packages` коллекция OData</span><span class="sxs-lookup"><span data-stu-id="ac6e1-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="ac6e1-120">**Получить** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="ac6e1-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="ac6e1-121">IP</span><span class="sxs-lookup"><span data-stu-id="ac6e1-121">IP</span></span> | <span data-ttu-id="ac6e1-122">3000/мин</span><span class="sxs-lookup"><span data-stu-id="ac6e1-122">3000 / minute</span></span> | <span data-ttu-id="ac6e1-123">Поиск пакетов NuGet с помощью конечной точки поиска v1</span><span class="sxs-lookup"><span data-stu-id="ac6e1-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="ac6e1-124">**Получить** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="ac6e1-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="ac6e1-125">IP</span><span class="sxs-lookup"><span data-stu-id="ac6e1-125">IP</span></span> | <span data-ttu-id="ac6e1-126">20000/мин</span><span class="sxs-lookup"><span data-stu-id="ac6e1-126">20000 / minute</span></span> | <span data-ttu-id="ac6e1-127">Запрос метаданных пакета NuGet через v2 `Packages` коллекция OData</span><span class="sxs-lookup"><span data-stu-id="ac6e1-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="ac6e1-128">**Получить** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="ac6e1-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="ac6e1-129">IP</span><span class="sxs-lookup"><span data-stu-id="ac6e1-129">IP</span></span> | <span data-ttu-id="ac6e1-130">100/мин</span><span class="sxs-lookup"><span data-stu-id="ac6e1-130">100 / minute</span></span> | <span data-ttu-id="ac6e1-131">Запрос числа пакетов NuGet через v2 `Packages` коллекция OData</span><span class="sxs-lookup"><span data-stu-id="ac6e1-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="ac6e1-132">Отправка и вывод пакетов</span><span class="sxs-lookup"><span data-stu-id="ac6e1-132">Package Push and Unlist</span></span>

| <span data-ttu-id="ac6e1-133">API</span><span class="sxs-lookup"><span data-stu-id="ac6e1-133">API</span></span> | <span data-ttu-id="ac6e1-134">Тип ограничения</span><span class="sxs-lookup"><span data-stu-id="ac6e1-134">Limit Type</span></span> | <span data-ttu-id="ac6e1-135">Значение ограничения</span><span class="sxs-lookup"><span data-stu-id="ac6e1-135">Limit Value</span></span> | <span data-ttu-id="ac6e1-136">API UseCase</span><span class="sxs-lookup"><span data-stu-id="ac6e1-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="ac6e1-137">**Разместить** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="ac6e1-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="ac6e1-138">Ключ API</span><span class="sxs-lookup"><span data-stu-id="ac6e1-138">API Key</span></span> | <span data-ttu-id="ac6e1-139">350 в час</span><span class="sxs-lookup"><span data-stu-id="ac6e1-139">350 / hour</span></span> | <span data-ttu-id="ac6e1-140">Отправка нового пакета NuGet с помощью конечной точки push-уведомлений версии 2</span><span class="sxs-lookup"><span data-stu-id="ac6e1-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="ac6e1-141">**Удалить** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="ac6e1-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="ac6e1-142">Ключ API</span><span class="sxs-lookup"><span data-stu-id="ac6e1-142">API Key</span></span> | <span data-ttu-id="ac6e1-143">250 в час</span><span class="sxs-lookup"><span data-stu-id="ac6e1-143">250 / hour</span></span> | <span data-ttu-id="ac6e1-144">Отменяет список пакетов NuGet (версии) с помощью конечной точки версии 2</span><span class="sxs-lookup"><span data-stu-id="ac6e1-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
