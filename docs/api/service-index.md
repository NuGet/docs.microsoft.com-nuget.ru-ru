---
title: Индекс службы, API NuGet
description: Индекс службы является точкой входа API HTTP NuGet и перечисляет возможности сервера.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775364"
---
# <a name="service-index"></a><span data-ttu-id="2a2fe-103">Индекс службы</span><span class="sxs-lookup"><span data-stu-id="2a2fe-103">Service index</span></span>

<span data-ttu-id="2a2fe-104">Индекс службы — это документ JSON, который является точкой входа для источника пакета NuGet и позволяет клиентской реализации обнаруживать возможности источника пакета.</span><span class="sxs-lookup"><span data-stu-id="2a2fe-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="2a2fe-105">Индекс службы — это объект JSON с двумя обязательными свойствами: `version` (версия схемы индекса службы) и `resources`  (конечные точки или возможности источника пакета).</span><span class="sxs-lookup"><span data-stu-id="2a2fe-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="2a2fe-106">индекс службы NuGet. org расположен по адресу `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="2a2fe-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="2a2fe-107">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="2a2fe-107">Versioning</span></span>

<span data-ttu-id="2a2fe-108">`version`Значение является строкой версии SemVer 2.0.0, которая указывает версию схемы индекса службы.</span><span class="sxs-lookup"><span data-stu-id="2a2fe-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="2a2fe-109">API требует, чтобы строка версии была основным номером версии `3` .</span><span class="sxs-lookup"><span data-stu-id="2a2fe-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="2a2fe-110">Так как в схему индекса службы вносятся некритические изменения, дополнительный номер версии строки версии увеличится.</span><span class="sxs-lookup"><span data-stu-id="2a2fe-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="2a2fe-111">Каждый ресурс в индексе службы обновляется независимо от версии схемы индекса службы.</span><span class="sxs-lookup"><span data-stu-id="2a2fe-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="2a2fe-112">Текущая версия схемы — `3.0.0` .</span><span class="sxs-lookup"><span data-stu-id="2a2fe-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="2a2fe-113">`3.0.0`Версия функционально эквивалентна старой `3.0.0-beta.1` версии, но должна быть предпочтительнее, так как она более четко передает устойчивую, определенную схему.</span><span class="sxs-lookup"><span data-stu-id="2a2fe-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="2a2fe-114">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="2a2fe-114">HTTP methods</span></span>

<span data-ttu-id="2a2fe-115">Индекс службы доступен с помощью методов HTTP `GET` и `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="2a2fe-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="2a2fe-116">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="2a2fe-116">Resources</span></span>

<span data-ttu-id="2a2fe-117">`resources`Свойство содержит массив ресурсов, поддерживаемых этим источником пакета.</span><span class="sxs-lookup"><span data-stu-id="2a2fe-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="2a2fe-118">Ресурс</span><span class="sxs-lookup"><span data-stu-id="2a2fe-118">Resource</span></span>

<span data-ttu-id="2a2fe-119">Ресурс — это объект в `resources` массиве.</span><span class="sxs-lookup"><span data-stu-id="2a2fe-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="2a2fe-120">Он представляет возможность версии источника пакета.</span><span class="sxs-lookup"><span data-stu-id="2a2fe-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="2a2fe-121">Ресурс имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="2a2fe-121">A resource has the following properties:</span></span>

<span data-ttu-id="2a2fe-122">Имя</span><span class="sxs-lookup"><span data-stu-id="2a2fe-122">Name</span></span>          | <span data-ttu-id="2a2fe-123">Тип</span><span class="sxs-lookup"><span data-stu-id="2a2fe-123">Type</span></span>   | <span data-ttu-id="2a2fe-124">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2a2fe-124">Required</span></span> | <span data-ttu-id="2a2fe-125">Примечания</span><span class="sxs-lookup"><span data-stu-id="2a2fe-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="2a2fe-126">строка</span><span class="sxs-lookup"><span data-stu-id="2a2fe-126">string</span></span> | <span data-ttu-id="2a2fe-127">yes</span><span class="sxs-lookup"><span data-stu-id="2a2fe-127">yes</span></span>      | <span data-ttu-id="2a2fe-128">URL-адрес ресурса</span><span class="sxs-lookup"><span data-stu-id="2a2fe-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="2a2fe-129">строка</span><span class="sxs-lookup"><span data-stu-id="2a2fe-129">string</span></span> | <span data-ttu-id="2a2fe-130">yes</span><span class="sxs-lookup"><span data-stu-id="2a2fe-130">yes</span></span>      | <span data-ttu-id="2a2fe-131">Строковая константа, представляющая тип ресурса</span><span class="sxs-lookup"><span data-stu-id="2a2fe-131">A string constant representing the resource type</span></span>
<span data-ttu-id="2a2fe-132">comment</span><span class="sxs-lookup"><span data-stu-id="2a2fe-132">comment</span></span>       | <span data-ttu-id="2a2fe-133">строка</span><span class="sxs-lookup"><span data-stu-id="2a2fe-133">string</span></span> | <span data-ttu-id="2a2fe-134">нет</span><span class="sxs-lookup"><span data-stu-id="2a2fe-134">no</span></span>       | <span data-ttu-id="2a2fe-135">Понятное описание ресурса</span><span class="sxs-lookup"><span data-stu-id="2a2fe-135">A human readable description of the resource</span></span>

<span data-ttu-id="2a2fe-136">`@id`— Это URL-адрес, который должен быть абсолютным и должен иметь схему HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2a2fe-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="2a2fe-137">`@type`Используется для задания конкретного протокола, используемого при взаимодействии с ресурсом.</span><span class="sxs-lookup"><span data-stu-id="2a2fe-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="2a2fe-138">Тип ресурса является непрозрачной строкой, но обычно имеет формат:</span><span class="sxs-lookup"><span data-stu-id="2a2fe-138">The type of the resource is an opaque string but generally has the format:</span></span>

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

<span data-ttu-id="2a2fe-139">Клиенты должны жестко кодировать `@type` значения, которые они понимают, и найти их в индексе службы источника пакета.</span><span class="sxs-lookup"><span data-stu-id="2a2fe-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="2a2fe-140">Точные `@type` значения, используемые сегодня, перечислены в документах ссылок на отдельные ресурсы, перечисленные в [обзоре API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="2a2fe-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="2a2fe-141">В этой документации документация по различным ресурсам будет сгруппирована по `{RESOURCE_NAME}` найденному в индексе службы, что аналогично группированию по сценарию.</span><span class="sxs-lookup"><span data-stu-id="2a2fe-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="2a2fe-142">Требования к каждому ресурсу уникальны `@id` или отсутствуют `@type` .</span><span class="sxs-lookup"><span data-stu-id="2a2fe-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="2a2fe-143">Чтобы определить, какой ресурс предпочтительнее другого, необходимо реализовать клиент.</span><span class="sxs-lookup"><span data-stu-id="2a2fe-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="2a2fe-144">Одной из возможных реализаций является то, что ресурсы с одинаковыми или совместимыми `@type` могут использоваться в циклической перебора в случае сбоя соединения или ошибки сервера.</span><span class="sxs-lookup"><span data-stu-id="2a2fe-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="2a2fe-145">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="2a2fe-145">Sample request</span></span>

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a><span data-ttu-id="2a2fe-146">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="2a2fe-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
