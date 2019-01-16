---
title: Обновления индекса, API NuGet
description: Индекс службы представляет собой точку входа интерфейса API HTTP NuGet и перечисляет возможности сервера.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1dcfb87690b728280b494d4434f9c1d7ee7a7e74
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324725"
---
# <a name="service-index"></a><span data-ttu-id="59227-103">Индекс службы</span><span class="sxs-lookup"><span data-stu-id="59227-103">Service index</span></span>

<span data-ttu-id="59227-104">Индекс службы — это документ JSON, который представляет собой точку входа для источника пакетов NuGet и позволяет обнаружить источник пакета возможности реализации клиента.</span><span class="sxs-lookup"><span data-stu-id="59227-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="59227-105">Индекс службы представляет собой объект JSON с два обязательных свойства: `version` (версия схемы для индекса службы) и `resources` (конечные точки или возможности источника пакета).</span><span class="sxs-lookup"><span data-stu-id="59227-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="59227-106">Индекс службы для NuGet.org находится в каталоге `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="59227-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="59227-107">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="59227-107">Versioning</span></span>

<span data-ttu-id="59227-108">`version` Значением является строка непригодными для синтаксического анализа версии SemVer 2.0.0, который указывает версию схемы индекса службы.</span><span class="sxs-lookup"><span data-stu-id="59227-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="59227-109">API требует, что строка версии имеет номер основной версии `3`.</span><span class="sxs-lookup"><span data-stu-id="59227-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="59227-110">Как некритических изменений со схемой индекса службы, строку версии дополнительный номер версии увеличивается.</span><span class="sxs-lookup"><span data-stu-id="59227-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="59227-111">Каждый ресурс в индекс службы включено управление версиями, независимо от версии схемы индекса службы.</span><span class="sxs-lookup"><span data-stu-id="59227-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="59227-112">Текущая версия схемы `3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="59227-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="59227-113">`3.0.0` Функционально эквивалентен более ранние версии `3.0.0-beta.1` версии, но лучше использовать, поскольку он более точно взаимодействует схемы стабильной, определенный.</span><span class="sxs-lookup"><span data-stu-id="59227-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="59227-114">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="59227-114">HTTP methods</span></span>

<span data-ttu-id="59227-115">Индекс службы доступен, с помощью HTTP-методов `GET` и `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="59227-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="59227-116">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="59227-116">Resources</span></span>

<span data-ttu-id="59227-117">`resources` Свойство содержит набор ресурсов, поддерживаемых источником этого пакета.</span><span class="sxs-lookup"><span data-stu-id="59227-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="59227-118">Ресурс</span><span class="sxs-lookup"><span data-stu-id="59227-118">Resource</span></span>

<span data-ttu-id="59227-119">Ресурс — это объект в `resources` массива.</span><span class="sxs-lookup"><span data-stu-id="59227-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="59227-120">Он представляет функцию с версиями источника пакета.</span><span class="sxs-lookup"><span data-stu-id="59227-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="59227-121">Ресурс имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="59227-121">A resource has the following properties:</span></span>

<span data-ttu-id="59227-122">name</span><span class="sxs-lookup"><span data-stu-id="59227-122">Name</span></span>          | <span data-ttu-id="59227-123">Тип</span><span class="sxs-lookup"><span data-stu-id="59227-123">Type</span></span>   | <span data-ttu-id="59227-124">Обязательно</span><span class="sxs-lookup"><span data-stu-id="59227-124">Required</span></span> | <span data-ttu-id="59227-125">Примечания</span><span class="sxs-lookup"><span data-stu-id="59227-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="59227-126">string</span><span class="sxs-lookup"><span data-stu-id="59227-126">string</span></span> | <span data-ttu-id="59227-127">да</span><span class="sxs-lookup"><span data-stu-id="59227-127">yes</span></span>      | <span data-ttu-id="59227-128">URL-адрес ресурса</span><span class="sxs-lookup"><span data-stu-id="59227-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="59227-129">string</span><span class="sxs-lookup"><span data-stu-id="59227-129">string</span></span> | <span data-ttu-id="59227-130">да</span><span class="sxs-lookup"><span data-stu-id="59227-130">yes</span></span>      | <span data-ttu-id="59227-131">Строковая константа, представляющая тип ресурса</span><span class="sxs-lookup"><span data-stu-id="59227-131">A string constant representing the resource type</span></span>
<span data-ttu-id="59227-132">комментарий</span><span class="sxs-lookup"><span data-stu-id="59227-132">comment</span></span>       | <span data-ttu-id="59227-133">string</span><span class="sxs-lookup"><span data-stu-id="59227-133">string</span></span> | <span data-ttu-id="59227-134">Нет</span><span class="sxs-lookup"><span data-stu-id="59227-134">no</span></span>       | <span data-ttu-id="59227-135">Понятное описание ресурса</span><span class="sxs-lookup"><span data-stu-id="59227-135">A human readable description of the resource</span></span>

<span data-ttu-id="59227-136">`@id` Является URL-адрес, который должен быть абсолютным и должен либо иметь схему HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="59227-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="59227-137">`@type` Используется для идентификации конкретного протокола, используемые для обмена с ресурсом.</span><span class="sxs-lookup"><span data-stu-id="59227-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="59227-138">Тип ресурса непрозрачная строка, но обычно имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="59227-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="59227-139">Клиентам следует жестко `@type` значения, что они понимают и находить их в индекс службы источника пакета.</span><span class="sxs-lookup"><span data-stu-id="59227-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="59227-140">Точное `@type` значения в настоящее время перечисляются в справочных документах отдельного ресурса, перечисленные в [Обзор API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="59227-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="59227-141">Ради этой документации документации о различных ресурсах по сути группируются по `{RESOURCE_NAME}` найден в индекс службы, который является аналогом группирование по сценарию.</span><span class="sxs-lookup"><span data-stu-id="59227-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="59227-142">Нет необходимости, что каждый ресурс имеет уникальное `@id` или `@type`.</span><span class="sxs-lookup"><span data-stu-id="59227-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="59227-143">Это зависит от реализации клиента, чтобы определить, какой ресурс следует по возможности отдавайте предпочтение другой.</span><span class="sxs-lookup"><span data-stu-id="59227-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="59227-144">Одна возможная реализация том, что ресурсы из той же или совместимый `@type` может использоваться в циклического перебора в случае сбоя или сервер ошибка подключения.</span><span class="sxs-lookup"><span data-stu-id="59227-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="59227-145">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="59227-145">Sample request</span></span>

    GET https://api.nuget.org/v3/index.json

### <a name="sample-response"></a><span data-ttu-id="59227-146">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="59227-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
