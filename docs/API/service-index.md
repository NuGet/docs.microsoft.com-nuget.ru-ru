---
title: "Служба индекс, NuGet API | Документы Microsoft"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Служба индекс является точкой входа NuGet HTTP API и перечисляет возможности сервера."
keywords: "Точка входа NuGet API, NuGetA PI обнаружения конечной точки"
ms.reviewer:
- karann
- unnir
ms.openlocfilehash: 8de0bc15edc358d091d84da54b8b67c085f29645
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/08/2018
---
# <a name="service-index"></a><span data-ttu-id="994bb-104">Служба индекс.</span><span class="sxs-lookup"><span data-stu-id="994bb-104">Service index</span></span>

<span data-ttu-id="994bb-105">Индекс службы является документом JSON, — это точка входа для источника пакета NuGet и позволяет ознакомиться с возможностями источника пакета реализации клиента.</span><span class="sxs-lookup"><span data-stu-id="994bb-105">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="994bb-106">Служба индекс — это объект JSON со два обязательных свойства: `version` (версия схемы индекса службы) и `resources` (конечные точки или возможностях исходного пакета).</span><span class="sxs-lookup"><span data-stu-id="994bb-106">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="994bb-107">Индекс службы NuGet.org находится в каталоге `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="994bb-107">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="994bb-108">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="994bb-108">Versioning</span></span>

<span data-ttu-id="994bb-109">`version` Значение представляет собой строку непригодными для синтаксического анализа версии SemVer 2.0.0, который указывает версию схемы индекса службы.</span><span class="sxs-lookup"><span data-stu-id="994bb-109">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="994bb-110">API требует, что строка версии имеет номер основной версии `3`.</span><span class="sxs-lookup"><span data-stu-id="994bb-110">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="994bb-111">Некритических изменений, выполненных в схеме индекса службы, строку версии, дополнительный номер версии увеличивается.</span><span class="sxs-lookup"><span data-stu-id="994bb-111">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="994bb-112">Каждый ресурс в индексе службы с версиями, независимо от версии службы индекса схемы.</span><span class="sxs-lookup"><span data-stu-id="994bb-112">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="994bb-113">Текущая версия схемы `3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="994bb-113">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="994bb-114">`3.0.0` Версии функционально эквивалентен старые `3.0.0-beta.1` версии, но должен быть предпочтительным, как он более точно обменивается схемы стабильной, определенный.</span><span class="sxs-lookup"><span data-stu-id="994bb-114">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="994bb-115">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="994bb-115">HTTP methods</span></span>

<span data-ttu-id="994bb-116">Индекс службы можно получить через HTTP-методов `GET` и `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="994bb-116">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="994bb-117">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="994bb-117">Resources</span></span>

<span data-ttu-id="994bb-118">`resources` Свойство содержит массив ресурсов, поддерживаемые источником этого пакета.</span><span class="sxs-lookup"><span data-stu-id="994bb-118">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="994bb-119">Ресурс</span><span class="sxs-lookup"><span data-stu-id="994bb-119">Resource</span></span>

<span data-ttu-id="994bb-120">Ресурс — это объект в `resources` массива.</span><span class="sxs-lookup"><span data-stu-id="994bb-120">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="994bb-121">Он представляет функцию с версиями источника пакета.</span><span class="sxs-lookup"><span data-stu-id="994bb-121">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="994bb-122">Ресурс имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="994bb-122">A resource has the following properties:</span></span>

<span data-ttu-id="994bb-123">name</span><span class="sxs-lookup"><span data-stu-id="994bb-123">Name</span></span>          | <span data-ttu-id="994bb-124">Тип</span><span class="sxs-lookup"><span data-stu-id="994bb-124">Type</span></span>   | <span data-ttu-id="994bb-125">Обязательно</span><span class="sxs-lookup"><span data-stu-id="994bb-125">Required</span></span> | <span data-ttu-id="994bb-126">Примечания</span><span class="sxs-lookup"><span data-stu-id="994bb-126">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="994bb-127">string</span><span class="sxs-lookup"><span data-stu-id="994bb-127">string</span></span> | <span data-ttu-id="994bb-128">да</span><span class="sxs-lookup"><span data-stu-id="994bb-128">yes</span></span>      | <span data-ttu-id="994bb-129">URL-адрес ресурса</span><span class="sxs-lookup"><span data-stu-id="994bb-129">The URL to the resource</span></span>
@type         | <span data-ttu-id="994bb-130">string</span><span class="sxs-lookup"><span data-stu-id="994bb-130">string</span></span> | <span data-ttu-id="994bb-131">да</span><span class="sxs-lookup"><span data-stu-id="994bb-131">yes</span></span>      | <span data-ttu-id="994bb-132">Строковая константа, представляющая тип ресурса</span><span class="sxs-lookup"><span data-stu-id="994bb-132">A string constant representing the resource type</span></span>
<span data-ttu-id="994bb-133">комментарий</span><span class="sxs-lookup"><span data-stu-id="994bb-133">comment</span></span>       | <span data-ttu-id="994bb-134">string</span><span class="sxs-lookup"><span data-stu-id="994bb-134">string</span></span> | <span data-ttu-id="994bb-135">Нет</span><span class="sxs-lookup"><span data-stu-id="994bb-135">no</span></span>       | <span data-ttu-id="994bb-136">Понятное описание ресурса</span><span class="sxs-lookup"><span data-stu-id="994bb-136">A human readable description of the resource</span></span>

<span data-ttu-id="994bb-137">`@id` : URL-адрес, который должен быть абсолютным и должен либо иметь схемы HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="994bb-137">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="994bb-138">`@type` Используется для идентификации конкретного протокола для использования при взаимодействии с ресурсом.</span><span class="sxs-lookup"><span data-stu-id="994bb-138">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="994bb-139">Тип ресурса непрозрачная строка, но обычно имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="994bb-139">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="994bb-140">Клиенты должны жестко `@type` значения их понимания и находить их в индексе источник пакета службы.</span><span class="sxs-lookup"><span data-stu-id="994bb-140">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="994bb-141">Точное `@type` значения в настоящее время выполняется перечисление на конкретный ресурс справочные документы, перечисленные в [Обзор интерфейса API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="994bb-141">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="994bb-142">Для обеспечения этой документации, документацию по различным ресурсам по существу группируются по `{RESOURCE_NAME}` найден в индексе службы, который является аналогом группирования по сценарию.</span><span class="sxs-lookup"><span data-stu-id="994bb-142">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="994bb-143">Не требуется, чтобы каждый ресурс имеет уникальный `@id` или `@type`.</span><span class="sxs-lookup"><span data-stu-id="994bb-143">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="994bb-144">Это зависит от реализации клиента, чтобы определить, какие ресурсы предпочитают на другое.</span><span class="sxs-lookup"><span data-stu-id="994bb-144">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="994bb-145">Является одной из возможных реализаций, ресурсы одинаковые или совместимые `@type` может использоваться в циклического перебора, в случае сбоя или сервера ошибка подключения.</span><span class="sxs-lookup"><span data-stu-id="994bb-145">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="994bb-146">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="994bb-146">Sample request</span></span>

<span data-ttu-id="994bb-147">GET https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="994bb-147">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="994bb-148">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="994bb-148">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
