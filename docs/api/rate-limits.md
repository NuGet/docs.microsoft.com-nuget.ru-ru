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
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367938"
---
# <a name="rate-limits"></a><span data-ttu-id="fa81e-103">Ограничения скорости</span><span class="sxs-lookup"><span data-stu-id="fa81e-103">Rate Limits</span></span>

<span data-ttu-id="fa81e-104">API NuGet.org обеспечивает ограничение скорости для предотвращения нарушения.</span><span class="sxs-lookup"><span data-stu-id="fa81e-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="fa81e-105">Запросы, превышающие предел скорости, возвращают следующую ошибку:</span><span class="sxs-lookup"><span data-stu-id="fa81e-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="fa81e-106">Помимо регулирования запросов с использованием пределов скорости, некоторые API также применяют квоту.</span><span class="sxs-lookup"><span data-stu-id="fa81e-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="fa81e-107">Запросы, превышающие квоту, возвращают следующую ошибку:</span><span class="sxs-lookup"><span data-stu-id="fa81e-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="fa81e-108">В следующих таблицах перечислены ограничения скорости для API NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="fa81e-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="fa81e-109">Поиск пакета</span><span class="sxs-lookup"><span data-stu-id="fa81e-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="fa81e-110">Мы рекомендуем использовать API-интерфейсы для [поиска версии 3](search-query-service-resource.md) NuGet. org, так как в настоящее время это не слишком мало частоты.</span><span class="sxs-lookup"><span data-stu-id="fa81e-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="fa81e-111">Для API-интерфейсов поиска v1 и v2 применяются следующие ограничения.</span><span class="sxs-lookup"><span data-stu-id="fa81e-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="fa81e-112">API</span><span class="sxs-lookup"><span data-stu-id="fa81e-112">API</span></span> | <span data-ttu-id="fa81e-113">Тип ограничения</span><span class="sxs-lookup"><span data-stu-id="fa81e-113">Limit Type</span></span> | <span data-ttu-id="fa81e-114">Значение ограничения</span><span class="sxs-lookup"><span data-stu-id="fa81e-114">Limit Value</span></span> | <span data-ttu-id="fa81e-115">Вариант использования API</span><span class="sxs-lookup"><span data-stu-id="fa81e-115">API Use Case</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="fa81e-116">**Получить**`/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="fa81e-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="fa81e-117">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="fa81e-117">IP</span></span> | <span data-ttu-id="fa81e-118">1000/мин</span><span class="sxs-lookup"><span data-stu-id="fa81e-118">1000 / minute</span></span> | <span data-ttu-id="fa81e-119">Запрос метаданных пакета NuGet через коллекцию OData v1 `Packages`</span><span class="sxs-lookup"><span data-stu-id="fa81e-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="fa81e-120">**Получить**`/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="fa81e-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="fa81e-121">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="fa81e-121">IP</span></span> | <span data-ttu-id="fa81e-122">3000/мин</span><span class="sxs-lookup"><span data-stu-id="fa81e-122">3000 / minute</span></span> | <span data-ttu-id="fa81e-123">Поиск пакетов NuGet с помощью конечной точки поиска v1</span><span class="sxs-lookup"><span data-stu-id="fa81e-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="fa81e-124">**Получить**`/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="fa81e-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="fa81e-125">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="fa81e-125">IP</span></span> | <span data-ttu-id="fa81e-126">20000/мин</span><span class="sxs-lookup"><span data-stu-id="fa81e-126">20000 / minute</span></span> | <span data-ttu-id="fa81e-127">Запрос метаданных пакета NuGet через v2 `Packages` коллекция OData</span><span class="sxs-lookup"><span data-stu-id="fa81e-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="fa81e-128">**Получить**`/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="fa81e-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="fa81e-129">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="fa81e-129">IP</span></span> | <span data-ttu-id="fa81e-130">100/мин</span><span class="sxs-lookup"><span data-stu-id="fa81e-130">100 / minute</span></span> | <span data-ttu-id="fa81e-131">Запрос числа пакетов NuGet через v2 `Packages` коллекция OData</span><span class="sxs-lookup"><span data-stu-id="fa81e-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="fa81e-132">Отправка и вывод пакетов</span><span class="sxs-lookup"><span data-stu-id="fa81e-132">Package Push and Unlist</span></span>

| <span data-ttu-id="fa81e-133">API</span><span class="sxs-lookup"><span data-stu-id="fa81e-133">API</span></span> | <span data-ttu-id="fa81e-134">Тип ограничения</span><span class="sxs-lookup"><span data-stu-id="fa81e-134">Limit Type</span></span> | <span data-ttu-id="fa81e-135">Значение ограничения</span><span class="sxs-lookup"><span data-stu-id="fa81e-135">Limit Value</span></span> | <span data-ttu-id="fa81e-136">Вариант использования API</span><span class="sxs-lookup"><span data-stu-id="fa81e-136">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="fa81e-137">**Размещение**`/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="fa81e-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="fa81e-138">Ключ API</span><span class="sxs-lookup"><span data-stu-id="fa81e-138">API Key</span></span> | <span data-ttu-id="fa81e-139">350 в час</span><span class="sxs-lookup"><span data-stu-id="fa81e-139">350 / hour</span></span> | <span data-ttu-id="fa81e-140">Отправка нового пакета NuGet с помощью конечной точки push-уведомлений версии 2</span><span class="sxs-lookup"><span data-stu-id="fa81e-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="fa81e-141">**Удаление**`/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="fa81e-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="fa81e-142">Ключ API</span><span class="sxs-lookup"><span data-stu-id="fa81e-142">API Key</span></span> | <span data-ttu-id="fa81e-143">250 в час</span><span class="sxs-lookup"><span data-stu-id="fa81e-143">250 / hour</span></span> | <span data-ttu-id="fa81e-144">Отменяет список пакетов NuGet (версии) с помощью конечной точки версии 2</span><span class="sxs-lookup"><span data-stu-id="fa81e-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 

## <a name="nugetorg-website-page-views"></a><span data-ttu-id="fa81e-145">Просмотры страниц веб-сайта nuget.org</span><span class="sxs-lookup"><span data-stu-id="fa81e-145">nuget.org website page views</span></span>

<span data-ttu-id="fa81e-146">Если вы обращаетесь к веб-страницам nuget.org программным способом, рассмотрите возможность изучения документированных [API V3](overview.md).</span><span class="sxs-lookup"><span data-stu-id="fa81e-146">If you are accessing the nuget.org web pages programmatically, consider investigating our documented [V3 APIs](overview.md).</span></span> <span data-ttu-id="fa81e-147">Эти конечные точки обеспечивают более простой доступ к метаданным и содержимому пакета.</span><span class="sxs-lookup"><span data-stu-id="fa81e-147">These endpoints allow for simpler access to package metadata and content.</span></span> <span data-ttu-id="fa81e-148">API V3 обеспечивает лучшую доступность и имеет более высокую производительность, чем доступ к веб-страницам коллекции NuGet, которые предназначены для взаимодействия веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="fa81e-148">The V3 API has better availability and has higher performance than accessing the NuGet Gallery web pages, which are designed for web browser interaction.</span></span>

| <span data-ttu-id="fa81e-149">API</span><span class="sxs-lookup"><span data-stu-id="fa81e-149">API</span></span> | <span data-ttu-id="fa81e-150">Тип ограничения</span><span class="sxs-lookup"><span data-stu-id="fa81e-150">Limit Type</span></span> | <span data-ttu-id="fa81e-151">Значение ограничения</span><span class="sxs-lookup"><span data-stu-id="fa81e-151">Limit Value</span></span> | <span data-ttu-id="fa81e-152">Вариант использования API</span><span class="sxs-lookup"><span data-stu-id="fa81e-152">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="fa81e-153">**Получить**`/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="fa81e-153">**GET** `/package/{id}/{version}`</span></span> | <span data-ttu-id="fa81e-154">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="fa81e-154">IP</span></span> | <span data-ttu-id="fa81e-155">50/мин</span><span class="sxs-lookup"><span data-stu-id="fa81e-155">50 / minute</span></span> | <span data-ttu-id="fa81e-156">Отображение страницы сведений о пакете (версии).</span><span class="sxs-lookup"><span data-stu-id="fa81e-156">Display package (version) details page.</span></span> 
