---
title: Пределы NuGet API скорости
description: API-интерфейсы NuGet будет обязательные пределы скорости для предотвращения нарушений.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: c5d3cf68ac6a96a6c14eb5e652bcf72698b6a8e8
ms.sourcegitcommit: 8f0bb8bb9cb91d27d660963ed9b0f32642f420fe
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34225948"
---
# <a name="rate-limits"></a><span data-ttu-id="ffbfe-103">Ограничения скорости</span><span class="sxs-lookup"><span data-stu-id="ffbfe-103">Rate Limits</span></span>

<span data-ttu-id="ffbfe-104">NuGet.org API применяет ограничение скорости для предотвращения нарушений.</span><span class="sxs-lookup"><span data-stu-id="ffbfe-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="ffbfe-105">Запросы, превышающие ограничение частоты возвращает следующую ошибку:</span><span class="sxs-lookup"><span data-stu-id="ffbfe-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="ffbfe-106">В следующих таблицах перечислены ограничения скорости для NuGet.org API.</span><span class="sxs-lookup"><span data-stu-id="ffbfe-106">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="ffbfe-107">Поиск пакетов</span><span class="sxs-lookup"><span data-stu-id="ffbfe-107">Package search</span></span>

> [!Note]
> <span data-ttu-id="ffbfe-108">Мы рекомендуем использовать NuGet.org [API-интерфейсы V3](https://docs.microsoft.com/nuget/api/search-query-service-resource) для поиска, которые обращаются и не имеющие ограничить в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="ffbfe-108">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="ffbfe-109">Для V1 и V2 поиск интерфейсов API, followins ограничения относятся:</span><span class="sxs-lookup"><span data-stu-id="ffbfe-109">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="ffbfe-110">API</span><span class="sxs-lookup"><span data-stu-id="ffbfe-110">API</span></span> | <span data-ttu-id="ffbfe-111">Ограничение типа</span><span class="sxs-lookup"><span data-stu-id="ffbfe-111">Limit Type</span></span> | <span data-ttu-id="ffbfe-112">Предельное значение</span><span class="sxs-lookup"><span data-stu-id="ffbfe-112">Limit Value</span></span> | <span data-ttu-id="ffbfe-113">API usecase</span><span class="sxs-lookup"><span data-stu-id="ffbfe-113">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="ffbfe-114">**ПОЛУЧИТЬ** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="ffbfe-114">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="ffbfe-115">IP</span><span class="sxs-lookup"><span data-stu-id="ffbfe-115">IP</span></span> | <span data-ttu-id="ffbfe-116">1000 / мин</span><span class="sxs-lookup"><span data-stu-id="ffbfe-116">1000 / minute</span></span> | <span data-ttu-id="ffbfe-117">Запросить метаданные пакета NuGet через v1 OData `Packages` коллекции</span><span class="sxs-lookup"><span data-stu-id="ffbfe-117">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="ffbfe-118">**ПОЛУЧИТЬ** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="ffbfe-118">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="ffbfe-119">IP</span><span class="sxs-lookup"><span data-stu-id="ffbfe-119">IP</span></span> | <span data-ttu-id="ffbfe-120">3000 / мин</span><span class="sxs-lookup"><span data-stu-id="ffbfe-120">3000 / minute</span></span> | <span data-ttu-id="ffbfe-121">Поиск пакетов NuGet через конечную точку поиска v1</span><span class="sxs-lookup"><span data-stu-id="ffbfe-121">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="ffbfe-122">**ПОЛУЧИТЬ** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="ffbfe-122">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="ffbfe-123">IP</span><span class="sxs-lookup"><span data-stu-id="ffbfe-123">IP</span></span> | <span data-ttu-id="ffbfe-124">20000 / мин</span><span class="sxs-lookup"><span data-stu-id="ffbfe-124">20000 / minute</span></span> | <span data-ttu-id="ffbfe-125">Запросить метаданные пакета NuGet через v2 OData `Packages` коллекции</span><span class="sxs-lookup"><span data-stu-id="ffbfe-125">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="ffbfe-126">**ПОЛУЧИТЬ** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="ffbfe-126">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="ffbfe-127">IP</span><span class="sxs-lookup"><span data-stu-id="ffbfe-127">IP</span></span> | <span data-ttu-id="ffbfe-128">100 / мин</span><span class="sxs-lookup"><span data-stu-id="ffbfe-128">100 / minute</span></span> | <span data-ttu-id="ffbfe-129">Запросить число пакета NuGet через v2 OData `Packages` коллекции</span><span class="sxs-lookup"><span data-stu-id="ffbfe-129">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="ffbfe-130">Пакет Push и исключить</span><span class="sxs-lookup"><span data-stu-id="ffbfe-130">Package Push and Unlist</span></span>

| <span data-ttu-id="ffbfe-131">API</span><span class="sxs-lookup"><span data-stu-id="ffbfe-131">API</span></span> | <span data-ttu-id="ffbfe-132">Ограничение типа</span><span class="sxs-lookup"><span data-stu-id="ffbfe-132">Limit Type</span></span> | <span data-ttu-id="ffbfe-133">Предельное значение</span><span class="sxs-lookup"><span data-stu-id="ffbfe-133">Limit Value</span></span> | <span data-ttu-id="ffbfe-134">API usecase</span><span class="sxs-lookup"><span data-stu-id="ffbfe-134">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="ffbfe-135">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="ffbfe-135">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="ffbfe-136">Ключ API</span><span class="sxs-lookup"><span data-stu-id="ffbfe-136">API Key</span></span> | <span data-ttu-id="ffbfe-137">250 / час</span><span class="sxs-lookup"><span data-stu-id="ffbfe-137">250 / hour</span></span> | <span data-ttu-id="ffbfe-138">Отправьте новый пакет NuGet (версия) через конечную точку принудительной v2</span><span class="sxs-lookup"><span data-stu-id="ffbfe-138">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="ffbfe-139">**УДАЛИТЬ** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="ffbfe-139">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="ffbfe-140">Ключ API</span><span class="sxs-lookup"><span data-stu-id="ffbfe-140">API Key</span></span> | <span data-ttu-id="ffbfe-141">250 / час</span><span class="sxs-lookup"><span data-stu-id="ffbfe-141">250 / hour</span></span> | <span data-ttu-id="ffbfe-142">Исключить пакет NuGet (версия) через конечную точку v2</span><span class="sxs-lookup"><span data-stu-id="ffbfe-142">Unlist a NuGet package (version) via v2 endpoint</span></span> 
