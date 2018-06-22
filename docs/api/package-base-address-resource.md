---
title: Содержимое пакета, NuGet интерфейса API
description: Базовый адрес пакета — это простой интерфейс для выборки в самом пакете.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a6ac40368f30d33f35d4ca0b6cc18ce4bd6efee5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819181"
---
# <a name="package-content"></a><span data-ttu-id="b6c7b-103">Содержимое пакета</span><span class="sxs-lookup"><span data-stu-id="b6c7b-103">Package Content</span></span>

<span data-ttu-id="b6c7b-104">Можно создать URL-адрес для выборки произвольного пакета содержимого (nupkg-файла) с помощью V3 API.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="b6c7b-105">Ресурс, используемый для получения содержимого пакета — `PackageBaseAddress` найти ресурс в [служба индекс](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="b6c7b-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="b6c7b-106">Этот ресурс также включает обнаружение всех версий пакета, в списке или не включенных в список.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="b6c7b-107">Этот ресурс называется как либо» пакета базовый адрес» или «неструктурированный контейнер».</span><span class="sxs-lookup"><span data-stu-id="b6c7b-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="b6c7b-108">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="b6c7b-108">Versioning</span></span>

<span data-ttu-id="b6c7b-109">Следующие `@type` используется значение:</span><span class="sxs-lookup"><span data-stu-id="b6c7b-109">The following `@type` value is used:</span></span>

<span data-ttu-id="b6c7b-110">Значение @type</span><span class="sxs-lookup"><span data-stu-id="b6c7b-110">@type value</span></span>              | <span data-ttu-id="b6c7b-111">Примечания</span><span class="sxs-lookup"><span data-stu-id="b6c7b-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="b6c7b-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="b6c7b-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="b6c7b-113">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="b6c7b-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="b6c7b-114">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b6c7b-114">Base URL</span></span>

<span data-ttu-id="b6c7b-115">Базовый URL-адрес для следующих API-интерфейсов — это значение `@id` свойства, связанные с ресурсом упомянутой выше `@type` значение.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="b6c7b-116">В следующем документе заполнитель базовый URL-адрес `{@id}` будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="b6c7b-117">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="b6c7b-117">HTTP methods</span></span>

<span data-ttu-id="b6c7b-118">Все URL-адреса, найден в поддержку ресурсов регистрации методов HTTP `GET` и `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="b6c7b-119">Перечисление версий пакета</span><span class="sxs-lookup"><span data-stu-id="b6c7b-119">Enumerate package versions</span></span>

<span data-ttu-id="b6c7b-120">Если клиент знает, идентификатор пакета и хочет, чтобы обнаружить, что пакета версии пакета источник был доступен, клиент можно создать прогнозируемые URL-адрес для перечисления всех версий пакета.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="b6c7b-121">Этот список предназначена для «список каталогов» для упомянутых ниже API содержимого пакета.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="b6c7b-122">Этот список содержит обе версии указанные и неуказанные пакета.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="b6c7b-123">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="b6c7b-123">Request parameters</span></span>

<span data-ttu-id="b6c7b-124">name</span><span class="sxs-lookup"><span data-stu-id="b6c7b-124">Name</span></span>     | <span data-ttu-id="b6c7b-125">Увеличение</span><span class="sxs-lookup"><span data-stu-id="b6c7b-125">In</span></span>     | <span data-ttu-id="b6c7b-126">Тип</span><span class="sxs-lookup"><span data-stu-id="b6c7b-126">Type</span></span>    | <span data-ttu-id="b6c7b-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b6c7b-127">Required</span></span> | <span data-ttu-id="b6c7b-128">Примечания</span><span class="sxs-lookup"><span data-stu-id="b6c7b-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="b6c7b-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="b6c7b-129">LOWER_ID</span></span> | <span data-ttu-id="b6c7b-130">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b6c7b-130">URL</span></span>    | <span data-ttu-id="b6c7b-131">string</span><span class="sxs-lookup"><span data-stu-id="b6c7b-131">string</span></span>  | <span data-ttu-id="b6c7b-132">да</span><span class="sxs-lookup"><span data-stu-id="b6c7b-132">yes</span></span>      | <span data-ttu-id="b6c7b-133">Идентификатор пакета, нижний регистр</span><span class="sxs-lookup"><span data-stu-id="b6c7b-133">The package ID, lowercase</span></span>

<span data-ttu-id="b6c7b-134">`LOWER_ID` Значение является Идентификатором нужный пакет букв с помощью правил, реализуемый. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) метод.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="b6c7b-135">Ответ</span><span class="sxs-lookup"><span data-stu-id="b6c7b-135">Response</span></span>

<span data-ttu-id="b6c7b-136">Если источник пакета не установлены версии предоставленный идентификатор, возвращается код состояния 404.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="b6c7b-137">Если исходный пакет имеет одну или несколько версий, возвращается код состояния 200.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="b6c7b-138">Текст ответа — это объект JSON с использованием следующего свойства:</span><span class="sxs-lookup"><span data-stu-id="b6c7b-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="b6c7b-139">name</span><span class="sxs-lookup"><span data-stu-id="b6c7b-139">Name</span></span>     | <span data-ttu-id="b6c7b-140">Тип</span><span class="sxs-lookup"><span data-stu-id="b6c7b-140">Type</span></span>             | <span data-ttu-id="b6c7b-141">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b6c7b-141">Required</span></span> | <span data-ttu-id="b6c7b-142">Примечания</span><span class="sxs-lookup"><span data-stu-id="b6c7b-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="b6c7b-143">версии</span><span class="sxs-lookup"><span data-stu-id="b6c7b-143">versions</span></span> | <span data-ttu-id="b6c7b-144">Массив строк</span><span class="sxs-lookup"><span data-stu-id="b6c7b-144">array of strings</span></span> | <span data-ttu-id="b6c7b-145">да</span><span class="sxs-lookup"><span data-stu-id="b6c7b-145">yes</span></span>      | <span data-ttu-id="b6c7b-146">Идентификаторы, доступные пакета</span><span class="sxs-lookup"><span data-stu-id="b6c7b-146">The package IDs available</span></span>

<span data-ttu-id="b6c7b-147">Строки в `versions` массив всех букв, [нормализации строки NuGet версии](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="b6c7b-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="b6c7b-148">Все метаданные сборки SemVer 2.0.0 не содержат строки версии.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="b6c7b-149">Целью является то, что версии строк, найденных в этом массиве можно использовать без изменений для `LOWER_VERSION` токены, найденные в следующих конечных точек.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="b6c7b-150">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="b6c7b-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="b6c7b-151">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="b6c7b-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="b6c7b-152">Скачать содержимое пакета (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="b6c7b-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="b6c7b-153">Если клиент знает ИД пакета и версия и хочет скачать содержимое пакета, достаточно лишь создать следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="b6c7b-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="b6c7b-154">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="b6c7b-154">Request parameters</span></span>

<span data-ttu-id="b6c7b-155">name</span><span class="sxs-lookup"><span data-stu-id="b6c7b-155">Name</span></span>          | <span data-ttu-id="b6c7b-156">Увеличение</span><span class="sxs-lookup"><span data-stu-id="b6c7b-156">In</span></span>     | <span data-ttu-id="b6c7b-157">Тип</span><span class="sxs-lookup"><span data-stu-id="b6c7b-157">Type</span></span>   | <span data-ttu-id="b6c7b-158">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b6c7b-158">Required</span></span> | <span data-ttu-id="b6c7b-159">Примечания</span><span class="sxs-lookup"><span data-stu-id="b6c7b-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b6c7b-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="b6c7b-160">LOWER_ID</span></span>      | <span data-ttu-id="b6c7b-161">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b6c7b-161">URL</span></span>    | <span data-ttu-id="b6c7b-162">string</span><span class="sxs-lookup"><span data-stu-id="b6c7b-162">string</span></span> | <span data-ttu-id="b6c7b-163">да</span><span class="sxs-lookup"><span data-stu-id="b6c7b-163">yes</span></span>      | <span data-ttu-id="b6c7b-164">Идентификатор пакета, нижний регистр</span><span class="sxs-lookup"><span data-stu-id="b6c7b-164">The package ID, lowercase</span></span>
<span data-ttu-id="b6c7b-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="b6c7b-165">LOWER_VERSION</span></span> | <span data-ttu-id="b6c7b-166">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b6c7b-166">URL</span></span>    | <span data-ttu-id="b6c7b-167">string</span><span class="sxs-lookup"><span data-stu-id="b6c7b-167">string</span></span> | <span data-ttu-id="b6c7b-168">да</span><span class="sxs-lookup"><span data-stu-id="b6c7b-168">yes</span></span>      | <span data-ttu-id="b6c7b-169">Версия пакета, нормализованную и букв</span><span class="sxs-lookup"><span data-stu-id="b6c7b-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="b6c7b-170">Оба `LOWER_ID` и `LOWER_VERSION` являются букв с помощью правил, реализуемый. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) метод.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="b6c7b-171">`LOWER_VERSION` Версии пакета на нужное нормализуется с использованием NuGet версии [правила нормализации](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="b6c7b-171">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="b6c7b-172">Это означает, что в этом случае необходимо исключить эти метаданные сборки, который разрешен спецификацией SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-172">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="b6c7b-173">Текст ответа</span><span class="sxs-lookup"><span data-stu-id="b6c7b-173">Response body</span></span>

<span data-ttu-id="b6c7b-174">Если пакет существует в источнике пакета, возвращается код состояния 200.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-174">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="b6c7b-175">Текст ответа будет содержимое пакета.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-175">The response body will be the package content itself.</span></span>

<span data-ttu-id="b6c7b-176">Если пакет не существует в источнике пакета, возвращается код состояния 404.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-176">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="b6c7b-177">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="b6c7b-177">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="b6c7b-178">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="b6c7b-178">Sample response</span></span>

<span data-ttu-id="b6c7b-179">Двоичный поток, который является .nupkg для Newtonsoft.Json 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-179">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="b6c7b-180">Загрузить манифест пакета (.nuspec)</span><span class="sxs-lookup"><span data-stu-id="b6c7b-180">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="b6c7b-181">Если клиент знает ИД пакета и версия и хочет загрузить манифест пакета, достаточно лишь создать следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="b6c7b-181">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="b6c7b-182">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="b6c7b-182">Request parameters</span></span>

<span data-ttu-id="b6c7b-183">name</span><span class="sxs-lookup"><span data-stu-id="b6c7b-183">Name</span></span>          | <span data-ttu-id="b6c7b-184">Увеличение</span><span class="sxs-lookup"><span data-stu-id="b6c7b-184">In</span></span>     | <span data-ttu-id="b6c7b-185">Тип</span><span class="sxs-lookup"><span data-stu-id="b6c7b-185">Type</span></span>    | <span data-ttu-id="b6c7b-186">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b6c7b-186">Required</span></span> | <span data-ttu-id="b6c7b-187">Примечания</span><span class="sxs-lookup"><span data-stu-id="b6c7b-187">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="b6c7b-188">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="b6c7b-188">LOWER_ID</span></span>      | <span data-ttu-id="b6c7b-189">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b6c7b-189">URL</span></span>    | <span data-ttu-id="b6c7b-190">string</span><span class="sxs-lookup"><span data-stu-id="b6c7b-190">string</span></span>  | <span data-ttu-id="b6c7b-191">да</span><span class="sxs-lookup"><span data-stu-id="b6c7b-191">yes</span></span>      | <span data-ttu-id="b6c7b-192">Идентификатор пакета, нижний регистр</span><span class="sxs-lookup"><span data-stu-id="b6c7b-192">The package ID, lowercase</span></span>
<span data-ttu-id="b6c7b-193">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="b6c7b-193">LOWER_VERSION</span></span> | <span data-ttu-id="b6c7b-194">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b6c7b-194">URL</span></span>    | <span data-ttu-id="b6c7b-195">целочисленный</span><span class="sxs-lookup"><span data-stu-id="b6c7b-195">integer</span></span> | <span data-ttu-id="b6c7b-196">да</span><span class="sxs-lookup"><span data-stu-id="b6c7b-196">yes</span></span>      | <span data-ttu-id="b6c7b-197">Версия пакета, нормализованную и букв</span><span class="sxs-lookup"><span data-stu-id="b6c7b-197">The package version, normalized and lowercased</span></span>

<span data-ttu-id="b6c7b-198">Оба `LOWER_ID` и `LOWER_VERSION` являются букв с помощью правил, реализуемый. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) метод.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-198">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="b6c7b-199">`LOWER_VERSION` Версии пакета на нужное нормализуется с использованием NuGet версии [правила нормализации](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="b6c7b-199">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="b6c7b-200">Это означает, что в этом случае необходимо исключить эти метаданные сборки, который разрешен спецификацией SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-200">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="b6c7b-201">Текст ответа</span><span class="sxs-lookup"><span data-stu-id="b6c7b-201">Response body</span></span>

<span data-ttu-id="b6c7b-202">Если пакет существует в источнике пакета, возвращается код состояния 200.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-202">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="b6c7b-203">Текст ответа будет манифест пакета, который является .nuspec, содержащиеся в соответствующей .nupkg.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-203">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="b6c7b-204">.nuspec — это документ XML.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-204">The .nuspec is an XML document.</span></span>

<span data-ttu-id="b6c7b-205">Если пакет не существует в источнике пакета, возвращается код состояния 404.</span><span class="sxs-lookup"><span data-stu-id="b6c7b-205">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="b6c7b-206">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="b6c7b-206">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="b6c7b-207">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="b6c7b-207">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
