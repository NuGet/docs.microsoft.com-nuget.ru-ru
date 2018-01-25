---
title: "Пакет содержимого NuGet API | Документы Microsoft"
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
description: "Базовый адрес пакета — это простой интерфейс для выборки в самом пакете."
keywords: "Контейнер, базовый адрес для пакета NuGet, nupkg NuGet API версии пакета NuGet API, NuGet API с плоскими NuGet не включенных в список пакетов, nuspec загрузки NuGet API"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c2e631dc0bba95ac849430d77142f27ef591f741
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="package-content"></a><span data-ttu-id="d54b8-104">Содержимое пакета</span><span class="sxs-lookup"><span data-stu-id="d54b8-104">Package Content</span></span>

<span data-ttu-id="d54b8-105">Можно создать URL-адрес для выборки произвольного пакета содержимого (nupkg-файла) с помощью V3 API.</span><span class="sxs-lookup"><span data-stu-id="d54b8-105">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="d54b8-106">Ресурс, используемый для получения содержимого пакета — `PackageBaseAddress` найти ресурс в [служба индекс](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="d54b8-106">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="d54b8-107">Этот ресурс также включает обнаружение всех версий пакета, в списке или не включенных в список.</span><span class="sxs-lookup"><span data-stu-id="d54b8-107">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="d54b8-108">Этот ресурс называется как либо» пакета базовый адрес» или «неструктурированный контейнер».</span><span class="sxs-lookup"><span data-stu-id="d54b8-108">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="d54b8-109">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="d54b8-109">Versioning</span></span>

<span data-ttu-id="d54b8-110">Следующие `@type` используется значение:</span><span class="sxs-lookup"><span data-stu-id="d54b8-110">The following `@type` value is used:</span></span>

<span data-ttu-id="d54b8-111">Значение @type</span><span class="sxs-lookup"><span data-stu-id="d54b8-111">@type value</span></span>              | <span data-ttu-id="d54b8-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="d54b8-112">Notes</span></span>
------------------------ | -----
<span data-ttu-id="d54b8-113">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="d54b8-113">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="d54b8-114">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="d54b8-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="d54b8-115">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d54b8-115">Base URL</span></span>

<span data-ttu-id="d54b8-116">Базовый URL-адрес для следующих API-интерфейсов — это значение `@id` свойства, связанные с ресурсом упомянутой выше `@type` значение.</span><span class="sxs-lookup"><span data-stu-id="d54b8-116">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="d54b8-117">В следующем документе заполнитель базовый URL-адрес `{@id}` будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="d54b8-117">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d54b8-118">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="d54b8-118">HTTP methods</span></span>

<span data-ttu-id="d54b8-119">Все URL-адреса, найден в поддержку ресурсов регистрации методов HTTP `GET` и `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="d54b8-119">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="d54b8-120">Перечисление версий пакета</span><span class="sxs-lookup"><span data-stu-id="d54b8-120">Enumerate package versions</span></span>

<span data-ttu-id="d54b8-121">Если клиент знает, идентификатор пакета и хочет, чтобы обнаружить, что пакета версии пакета источник был доступен, клиент можно создать прогнозируемые URL-адрес для перечисления всех версий пакета.</span><span class="sxs-lookup"><span data-stu-id="d54b8-121">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="d54b8-122">Этот список предназначена для «список каталогов» для упомянутых ниже API содержимого пакета.</span><span class="sxs-lookup"><span data-stu-id="d54b8-122">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="d54b8-123">Этот список содержит обе версии указанные и неуказанные пакета.</span><span class="sxs-lookup"><span data-stu-id="d54b8-123">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="d54b8-124">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="d54b8-124">Request parameters</span></span>

<span data-ttu-id="d54b8-125">name</span><span class="sxs-lookup"><span data-stu-id="d54b8-125">Name</span></span>     | <span data-ttu-id="d54b8-126">Увеличение</span><span class="sxs-lookup"><span data-stu-id="d54b8-126">In</span></span>     | <span data-ttu-id="d54b8-127">Тип</span><span class="sxs-lookup"><span data-stu-id="d54b8-127">Type</span></span>    | <span data-ttu-id="d54b8-128">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d54b8-128">Required</span></span> | <span data-ttu-id="d54b8-129">Примечания</span><span class="sxs-lookup"><span data-stu-id="d54b8-129">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="d54b8-130">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="d54b8-130">LOWER_ID</span></span> | <span data-ttu-id="d54b8-131">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d54b8-131">URL</span></span>    | <span data-ttu-id="d54b8-132">string</span><span class="sxs-lookup"><span data-stu-id="d54b8-132">string</span></span>  | <span data-ttu-id="d54b8-133">да</span><span class="sxs-lookup"><span data-stu-id="d54b8-133">yes</span></span>      | <span data-ttu-id="d54b8-134">Идентификатор пакета, нижний регистр</span><span class="sxs-lookup"><span data-stu-id="d54b8-134">The package ID, lowercase</span></span>

<span data-ttu-id="d54b8-135">`LOWER_ID` Значение является Идентификатором нужный пакет букв с помощью правил, реализуемый. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) метод.</span><span class="sxs-lookup"><span data-stu-id="d54b8-135">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="d54b8-136">Ответ</span><span class="sxs-lookup"><span data-stu-id="d54b8-136">Response</span></span>

<span data-ttu-id="d54b8-137">Если источник пакета не установлены версии предоставленный идентификатор, возвращается код состояния 404.</span><span class="sxs-lookup"><span data-stu-id="d54b8-137">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="d54b8-138">Если исходный пакет имеет одну или несколько версий, возвращается код состояния 200.</span><span class="sxs-lookup"><span data-stu-id="d54b8-138">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="d54b8-139">Текст ответа — это объект JSON с использованием следующего свойства:</span><span class="sxs-lookup"><span data-stu-id="d54b8-139">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="d54b8-140">name</span><span class="sxs-lookup"><span data-stu-id="d54b8-140">Name</span></span>     | <span data-ttu-id="d54b8-141">Тип</span><span class="sxs-lookup"><span data-stu-id="d54b8-141">Type</span></span>             | <span data-ttu-id="d54b8-142">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d54b8-142">Required</span></span> | <span data-ttu-id="d54b8-143">Примечания</span><span class="sxs-lookup"><span data-stu-id="d54b8-143">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="d54b8-144">версии</span><span class="sxs-lookup"><span data-stu-id="d54b8-144">versions</span></span> | <span data-ttu-id="d54b8-145">Массив строк</span><span class="sxs-lookup"><span data-stu-id="d54b8-145">array of strings</span></span> | <span data-ttu-id="d54b8-146">да</span><span class="sxs-lookup"><span data-stu-id="d54b8-146">yes</span></span>      | <span data-ttu-id="d54b8-147">Идентификаторы, доступные пакета</span><span class="sxs-lookup"><span data-stu-id="d54b8-147">The package IDs available</span></span>

<span data-ttu-id="d54b8-148">Строки в `versions` массив всех букв, [нормализации строки NuGet версии](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="d54b8-148">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="d54b8-149">Все метаданные сборки SemVer 2.0.0 не содержат строки версии.</span><span class="sxs-lookup"><span data-stu-id="d54b8-149">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="d54b8-150">Целью является то, что версии строк, найденных в этом массиве можно использовать без изменений для `LOWER_VERSION` токены, найденные в следующих конечных точек.</span><span class="sxs-lookup"><span data-stu-id="d54b8-150">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d54b8-151">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="d54b8-151">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="d54b8-152">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="d54b8-152">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="d54b8-153">Скачать содержимое пакета (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="d54b8-153">Download package content (.nupkg)</span></span>

<span data-ttu-id="d54b8-154">Если клиент знает ИД пакета и версия и хочет скачать содержимое пакета, достаточно лишь создать следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="d54b8-154">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="d54b8-155">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="d54b8-155">Request parameters</span></span>

<span data-ttu-id="d54b8-156">name</span><span class="sxs-lookup"><span data-stu-id="d54b8-156">Name</span></span>          | <span data-ttu-id="d54b8-157">Увеличение</span><span class="sxs-lookup"><span data-stu-id="d54b8-157">In</span></span>     | <span data-ttu-id="d54b8-158">Тип</span><span class="sxs-lookup"><span data-stu-id="d54b8-158">Type</span></span>   | <span data-ttu-id="d54b8-159">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d54b8-159">Required</span></span> | <span data-ttu-id="d54b8-160">Примечания</span><span class="sxs-lookup"><span data-stu-id="d54b8-160">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="d54b8-161">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="d54b8-161">LOWER_ID</span></span>      | <span data-ttu-id="d54b8-162">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d54b8-162">URL</span></span>    | <span data-ttu-id="d54b8-163">string</span><span class="sxs-lookup"><span data-stu-id="d54b8-163">string</span></span> | <span data-ttu-id="d54b8-164">да</span><span class="sxs-lookup"><span data-stu-id="d54b8-164">yes</span></span>      | <span data-ttu-id="d54b8-165">Идентификатор пакета, нижний регистр</span><span class="sxs-lookup"><span data-stu-id="d54b8-165">The package ID, lowercase</span></span>
<span data-ttu-id="d54b8-166">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="d54b8-166">LOWER_VERSION</span></span> | <span data-ttu-id="d54b8-167">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d54b8-167">URL</span></span>    | <span data-ttu-id="d54b8-168">string</span><span class="sxs-lookup"><span data-stu-id="d54b8-168">string</span></span> | <span data-ttu-id="d54b8-169">да</span><span class="sxs-lookup"><span data-stu-id="d54b8-169">yes</span></span>      | <span data-ttu-id="d54b8-170">Версия пакета, нормализованную и букв</span><span class="sxs-lookup"><span data-stu-id="d54b8-170">The package version, normalized and lowercased</span></span>

<span data-ttu-id="d54b8-171">Оба `LOWER_ID` и `LOWER_VERSION` являются букв с помощью правил, реализуемый. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) метод.</span><span class="sxs-lookup"><span data-stu-id="d54b8-171">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="d54b8-172">`LOWER_VERSION` Версии пакета на нужное нормализуется с использованием NuGet версии [правила нормализации](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="d54b8-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="d54b8-173">Это означает, что в этом случае необходимо исключить эти метаданные сборки, который разрешен спецификацией SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d54b8-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="d54b8-174">Текст ответа</span><span class="sxs-lookup"><span data-stu-id="d54b8-174">Response body</span></span>

<span data-ttu-id="d54b8-175">Если пакет существует в источнике пакета, возвращается код состояния 200.</span><span class="sxs-lookup"><span data-stu-id="d54b8-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="d54b8-176">Текст ответа будет содержимое пакета.</span><span class="sxs-lookup"><span data-stu-id="d54b8-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="d54b8-177">Если пакет не существует в источнике пакета, возвращается код состояния 404.</span><span class="sxs-lookup"><span data-stu-id="d54b8-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d54b8-178">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="d54b8-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="d54b8-179">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="d54b8-179">Sample response</span></span>

<span data-ttu-id="d54b8-180">Двоичный поток, который является .nupkg для Newtonsoft.Json 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="d54b8-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="d54b8-181">Загрузить манифест пакета (.nuspec)</span><span class="sxs-lookup"><span data-stu-id="d54b8-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="d54b8-182">Если клиент знает ИД пакета и версия и хочет загрузить манифест пакета, достаточно лишь создать следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="d54b8-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="d54b8-183">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="d54b8-183">Request parameters</span></span>

<span data-ttu-id="d54b8-184">name</span><span class="sxs-lookup"><span data-stu-id="d54b8-184">Name</span></span>          | <span data-ttu-id="d54b8-185">Увеличение</span><span class="sxs-lookup"><span data-stu-id="d54b8-185">In</span></span>     | <span data-ttu-id="d54b8-186">Тип</span><span class="sxs-lookup"><span data-stu-id="d54b8-186">Type</span></span>    | <span data-ttu-id="d54b8-187">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d54b8-187">Required</span></span> | <span data-ttu-id="d54b8-188">Примечания</span><span class="sxs-lookup"><span data-stu-id="d54b8-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="d54b8-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="d54b8-189">LOWER_ID</span></span>      | <span data-ttu-id="d54b8-190">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d54b8-190">URL</span></span>    | <span data-ttu-id="d54b8-191">string</span><span class="sxs-lookup"><span data-stu-id="d54b8-191">string</span></span>  | <span data-ttu-id="d54b8-192">да</span><span class="sxs-lookup"><span data-stu-id="d54b8-192">yes</span></span>      | <span data-ttu-id="d54b8-193">Идентификатор пакета, нижний регистр</span><span class="sxs-lookup"><span data-stu-id="d54b8-193">The package ID, lowercase</span></span>
<span data-ttu-id="d54b8-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="d54b8-194">LOWER_VERSION</span></span> | <span data-ttu-id="d54b8-195">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d54b8-195">URL</span></span>    | <span data-ttu-id="d54b8-196">целочисленный</span><span class="sxs-lookup"><span data-stu-id="d54b8-196">integer</span></span> | <span data-ttu-id="d54b8-197">да</span><span class="sxs-lookup"><span data-stu-id="d54b8-197">yes</span></span>      | <span data-ttu-id="d54b8-198">Версия пакета, нормализованную и букв</span><span class="sxs-lookup"><span data-stu-id="d54b8-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="d54b8-199">Оба `LOWER_ID` и `LOWER_VERSION` являются букв с помощью правил, реализуемый. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) метод.</span><span class="sxs-lookup"><span data-stu-id="d54b8-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="d54b8-200">`LOWER_VERSION` Версии пакета на нужное нормализуется с использованием NuGet версии [правила нормализации](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="d54b8-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="d54b8-201">Это означает, что в этом случае необходимо исключить эти метаданные сборки, который разрешен спецификацией SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d54b8-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="d54b8-202">Текст ответа</span><span class="sxs-lookup"><span data-stu-id="d54b8-202">Response body</span></span>

<span data-ttu-id="d54b8-203">Если пакет существует в источнике пакета, возвращается код состояния 200.</span><span class="sxs-lookup"><span data-stu-id="d54b8-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="d54b8-204">Текст ответа будет манифест пакета, который является .nuspec, содержащиеся в соответствующей .nupkg.</span><span class="sxs-lookup"><span data-stu-id="d54b8-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="d54b8-205">.nuspec — это документ XML.</span><span class="sxs-lookup"><span data-stu-id="d54b8-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="d54b8-206">Если пакет не существует в источнике пакета, возвращается код состояния 404.</span><span class="sxs-lookup"><span data-stu-id="d54b8-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d54b8-207">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="d54b8-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="d54b8-208">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="d54b8-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
