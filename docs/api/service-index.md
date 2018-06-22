---
title: Служба индекса NuGet интерфейса API
description: Служба индекс является точкой входа NuGet HTTP API и перечисляет возможности сервера.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 84e623e8480e4d17edad2ec3b2da6dcb6e53d21b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822098"
---
# <a name="service-index"></a><span data-ttu-id="a6e90-103">Служба индекс.</span><span class="sxs-lookup"><span data-stu-id="a6e90-103">Service index</span></span>

<span data-ttu-id="a6e90-104">Индекс службы является документом JSON, — это точка входа для источника пакета NuGet и позволяет ознакомиться с возможностями источника пакета реализации клиента.</span><span class="sxs-lookup"><span data-stu-id="a6e90-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="a6e90-105">Служба индекс — это объект JSON со два обязательных свойства: `version` (версия схемы индекса службы) и `resources` (конечные точки или возможностях исходного пакета).</span><span class="sxs-lookup"><span data-stu-id="a6e90-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="a6e90-106">Индекс службы NuGet.org находится в каталоге `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="a6e90-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="a6e90-107">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="a6e90-107">Versioning</span></span>

<span data-ttu-id="a6e90-108">`version` Значение представляет собой строку непригодными для синтаксического анализа версии SemVer 2.0.0, который указывает версию схемы индекса службы.</span><span class="sxs-lookup"><span data-stu-id="a6e90-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="a6e90-109">API требует, что строка версии имеет номер основной версии `3`.</span><span class="sxs-lookup"><span data-stu-id="a6e90-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="a6e90-110">Некритических изменений, выполненных в схеме индекса службы, строку версии, дополнительный номер версии увеличивается.</span><span class="sxs-lookup"><span data-stu-id="a6e90-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="a6e90-111">Каждый ресурс в индексе службы с версиями, независимо от версии службы индекса схемы.</span><span class="sxs-lookup"><span data-stu-id="a6e90-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="a6e90-112">Текущая версия схемы `3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="a6e90-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="a6e90-113">`3.0.0` Версии функционально эквивалентен старые `3.0.0-beta.1` версии, но должен быть предпочтительным, как он более точно обменивается схемы стабильной, определенный.</span><span class="sxs-lookup"><span data-stu-id="a6e90-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="a6e90-114">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="a6e90-114">HTTP methods</span></span>

<span data-ttu-id="a6e90-115">Индекс службы можно получить через HTTP-методов `GET` и `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="a6e90-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="a6e90-116">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="a6e90-116">Resources</span></span>

<span data-ttu-id="a6e90-117">`resources` Свойство содержит массив ресурсов, поддерживаемые источником этого пакета.</span><span class="sxs-lookup"><span data-stu-id="a6e90-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="a6e90-118">Ресурс</span><span class="sxs-lookup"><span data-stu-id="a6e90-118">Resource</span></span>

<span data-ttu-id="a6e90-119">Ресурс — это объект в `resources` массива.</span><span class="sxs-lookup"><span data-stu-id="a6e90-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="a6e90-120">Он представляет функцию с версиями источника пакета.</span><span class="sxs-lookup"><span data-stu-id="a6e90-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="a6e90-121">Ресурс имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="a6e90-121">A resource has the following properties:</span></span>

<span data-ttu-id="a6e90-122">name</span><span class="sxs-lookup"><span data-stu-id="a6e90-122">Name</span></span>          | <span data-ttu-id="a6e90-123">Тип</span><span class="sxs-lookup"><span data-stu-id="a6e90-123">Type</span></span>   | <span data-ttu-id="a6e90-124">Обязательно</span><span class="sxs-lookup"><span data-stu-id="a6e90-124">Required</span></span> | <span data-ttu-id="a6e90-125">Примечания</span><span class="sxs-lookup"><span data-stu-id="a6e90-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="a6e90-126">string</span><span class="sxs-lookup"><span data-stu-id="a6e90-126">string</span></span> | <span data-ttu-id="a6e90-127">да</span><span class="sxs-lookup"><span data-stu-id="a6e90-127">yes</span></span>      | <span data-ttu-id="a6e90-128">URL-адрес ресурса</span><span class="sxs-lookup"><span data-stu-id="a6e90-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="a6e90-129">string</span><span class="sxs-lookup"><span data-stu-id="a6e90-129">string</span></span> | <span data-ttu-id="a6e90-130">да</span><span class="sxs-lookup"><span data-stu-id="a6e90-130">yes</span></span>      | <span data-ttu-id="a6e90-131">Строковая константа, представляющая тип ресурса</span><span class="sxs-lookup"><span data-stu-id="a6e90-131">A string constant representing the resource type</span></span>
<span data-ttu-id="a6e90-132">комментарий</span><span class="sxs-lookup"><span data-stu-id="a6e90-132">comment</span></span>       | <span data-ttu-id="a6e90-133">string</span><span class="sxs-lookup"><span data-stu-id="a6e90-133">string</span></span> | <span data-ttu-id="a6e90-134">Нет</span><span class="sxs-lookup"><span data-stu-id="a6e90-134">no</span></span>       | <span data-ttu-id="a6e90-135">Понятное описание ресурса</span><span class="sxs-lookup"><span data-stu-id="a6e90-135">A human readable description of the resource</span></span>

<span data-ttu-id="a6e90-136">`@id` : URL-адрес, который должен быть абсолютным и должен либо иметь схемы HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a6e90-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="a6e90-137">`@type` Используется для идентификации конкретного протокола для использования при взаимодействии с ресурсом.</span><span class="sxs-lookup"><span data-stu-id="a6e90-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="a6e90-138">Тип ресурса непрозрачная строка, но обычно имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="a6e90-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="a6e90-139">Клиенты должны жестко `@type` значения их понимания и находить их в индексе источник пакета службы.</span><span class="sxs-lookup"><span data-stu-id="a6e90-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="a6e90-140">Точное `@type` значения в настоящее время выполняется перечисление на конкретный ресурс справочные документы, перечисленные в [Обзор интерфейса API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="a6e90-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="a6e90-141">Для обеспечения этой документации, документацию по различным ресурсам по существу группируются по `{RESOURCE_NAME}` найден в индексе службы, который является аналогом группирования по сценарию.</span><span class="sxs-lookup"><span data-stu-id="a6e90-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="a6e90-142">Не требуется, чтобы каждый ресурс имеет уникальный `@id` или `@type`.</span><span class="sxs-lookup"><span data-stu-id="a6e90-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="a6e90-143">Это зависит от реализации клиента, чтобы определить, какие ресурсы предпочитают на другое.</span><span class="sxs-lookup"><span data-stu-id="a6e90-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="a6e90-144">Является одной из возможных реализаций, ресурсы одинаковые или совместимые `@type` может использоваться в циклического перебора, в случае сбоя или сервера ошибка подключения.</span><span class="sxs-lookup"><span data-stu-id="a6e90-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a6e90-145">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="a6e90-145">Sample request</span></span>

<span data-ttu-id="a6e90-146">ПОЛУЧИТЬ https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="a6e90-146">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="a6e90-147">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="a6e90-147">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
