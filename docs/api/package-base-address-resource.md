---
title: Содержимое пакета, API NuGet
description: Базовый адрес пакета — это простой интерфейс для выборки самого пакета.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 7aea28d6224a89149aa33be035c82a45db3058f0
ms.sourcegitcommit: 1eda83ab537c86cc27316e7bc67f95a358766e63
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/18/2019
ms.locfileid: "71094126"
---
# <a name="package-content"></a><span data-ttu-id="6bf9b-103">Содержимое пакета</span><span class="sxs-lookup"><span data-stu-id="6bf9b-103">Package Content</span></span>

<span data-ttu-id="6bf9b-104">Можно создать URL-адрес для выборки содержимого произвольного пакета (nupkg-файла) с помощью API V3.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="6bf9b-105">Ресурс, используемый для выборки содержимого пакета, — `PackageBaseAddress` это ресурс, найденный в [индексе службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="6bf9b-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="6bf9b-106">Этот ресурс также включает обнаружение всех версий пакета, перечисленных или отсутствующих в списке.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="6bf9b-107">Этот ресурс обычно называется "базовым адресом пакета" или "плоским контейнером".</span><span class="sxs-lookup"><span data-stu-id="6bf9b-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="6bf9b-108">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="6bf9b-108">Versioning</span></span>

<span data-ttu-id="6bf9b-109">Используется следующее `@type` значение:</span><span class="sxs-lookup"><span data-stu-id="6bf9b-109">The following `@type` value is used:</span></span>

<span data-ttu-id="6bf9b-110">Значение@type</span><span class="sxs-lookup"><span data-stu-id="6bf9b-110">@type value</span></span>              | <span data-ttu-id="6bf9b-111">Примечания</span><span class="sxs-lookup"><span data-stu-id="6bf9b-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="6bf9b-112">Паккажебасеаддресс/3.0.0</span><span class="sxs-lookup"><span data-stu-id="6bf9b-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="6bf9b-113">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="6bf9b-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="6bf9b-114">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="6bf9b-114">Base URL</span></span>

<span data-ttu-id="6bf9b-115">Базовый URL-адрес для следующих интерфейсов API — это значение `@id` свойства, связанного с вышеупомянутым значением `@type` ресурса.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="6bf9b-116">В следующем документе будет использоваться базовый URL-адрес `{@id}` заполнителя.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="6bf9b-117">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="6bf9b-117">HTTP methods</span></span>

<span data-ttu-id="6bf9b-118">Все URL-адреса, найденные в ресурсе регистрации `GET` , `HEAD`поддерживают методы HTTP и.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="6bf9b-119">Перечислить версии пакета</span><span class="sxs-lookup"><span data-stu-id="6bf9b-119">Enumerate package versions</span></span>

<span data-ttu-id="6bf9b-120">Если клиент знает идентификатор пакета и хочет определить, какие версии пакетов доступны в источнике пакета, клиент может создать прогнозируемый URL-адрес для перечисления всех версий пакета.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="6bf9b-121">Этот список должен быть списком каталогов для API содержимого пакета, упомянутого ниже.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="6bf9b-122">Этот список содержит как перечисленные, так и невключенные версии пакетов.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="6bf9b-123">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="6bf9b-123">Request parameters</span></span>

<span data-ttu-id="6bf9b-124">name</span><span class="sxs-lookup"><span data-stu-id="6bf9b-124">Name</span></span>     | <span data-ttu-id="6bf9b-125">In</span><span class="sxs-lookup"><span data-stu-id="6bf9b-125">In</span></span>     | <span data-ttu-id="6bf9b-126">Тип</span><span class="sxs-lookup"><span data-stu-id="6bf9b-126">Type</span></span>    | <span data-ttu-id="6bf9b-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6bf9b-127">Required</span></span> | <span data-ttu-id="6bf9b-128">Примечания</span><span class="sxs-lookup"><span data-stu-id="6bf9b-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="6bf9b-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="6bf9b-129">LOWER_ID</span></span> | <span data-ttu-id="6bf9b-130">URL</span><span class="sxs-lookup"><span data-stu-id="6bf9b-130">URL</span></span>    | <span data-ttu-id="6bf9b-131">string</span><span class="sxs-lookup"><span data-stu-id="6bf9b-131">string</span></span>  | <span data-ttu-id="6bf9b-132">да</span><span class="sxs-lookup"><span data-stu-id="6bf9b-132">yes</span></span>      | <span data-ttu-id="6bf9b-133">Идентификатор пакета, в нижнем регистре</span><span class="sxs-lookup"><span data-stu-id="6bf9b-133">The package ID, lowercased</span></span>

<span data-ttu-id="6bf9b-134">`LOWER_ID` Значение представляет собой требуемый идентификатор пакета в нижнем регистре, используя правила, реализованные. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Метод NET.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="6bf9b-135">Отклик</span><span class="sxs-lookup"><span data-stu-id="6bf9b-135">Response</span></span>

<span data-ttu-id="6bf9b-136">Если источник пакета не имеет версий указанного идентификатора пакета, возвращается код состояния 404.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="6bf9b-137">Если источник пакета имеет одну или несколько версий, возвращается код состояния 200.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="6bf9b-138">Текст ответа — это объект JSON со следующим свойством:</span><span class="sxs-lookup"><span data-stu-id="6bf9b-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="6bf9b-139">name</span><span class="sxs-lookup"><span data-stu-id="6bf9b-139">Name</span></span>     | <span data-ttu-id="6bf9b-140">Тип</span><span class="sxs-lookup"><span data-stu-id="6bf9b-140">Type</span></span>             | <span data-ttu-id="6bf9b-141">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6bf9b-141">Required</span></span> | <span data-ttu-id="6bf9b-142">Примечания</span><span class="sxs-lookup"><span data-stu-id="6bf9b-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="6bf9b-143">версии</span><span class="sxs-lookup"><span data-stu-id="6bf9b-143">versions</span></span> | <span data-ttu-id="6bf9b-144">Массив строк</span><span class="sxs-lookup"><span data-stu-id="6bf9b-144">array of strings</span></span> | <span data-ttu-id="6bf9b-145">да</span><span class="sxs-lookup"><span data-stu-id="6bf9b-145">yes</span></span>      | <span data-ttu-id="6bf9b-146">Доступные версии</span><span class="sxs-lookup"><span data-stu-id="6bf9b-146">The versions available</span></span>

<span data-ttu-id="6bf9b-147">Строки в `versions` массиве — это все строки [нормализованных строк версии NuGet](../concepts/package-versioning.md#normalized-version-numbers)в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="6bf9b-148">Строки версии не содержат метаданные сборки SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="6bf9b-149">Цель состоит в том, что строки версии, найденные в этом массиве, можно `LOWER_VERSION` использовать буквально для маркеров, найденных в следующих конечных точках.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="6bf9b-150">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="6bf9b-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="6bf9b-151">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="6bf9b-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="6bf9b-152">Скачать содержимое пакета (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="6bf9b-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="6bf9b-153">Если клиент знает идентификатор и версию пакета и хочет загрузить содержимое пакета, необходимо создать только следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="6bf9b-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="6bf9b-154">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="6bf9b-154">Request parameters</span></span>

<span data-ttu-id="6bf9b-155">name</span><span class="sxs-lookup"><span data-stu-id="6bf9b-155">Name</span></span>          | <span data-ttu-id="6bf9b-156">In</span><span class="sxs-lookup"><span data-stu-id="6bf9b-156">In</span></span>     | <span data-ttu-id="6bf9b-157">Тип</span><span class="sxs-lookup"><span data-stu-id="6bf9b-157">Type</span></span>   | <span data-ttu-id="6bf9b-158">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6bf9b-158">Required</span></span> | <span data-ttu-id="6bf9b-159">Примечания</span><span class="sxs-lookup"><span data-stu-id="6bf9b-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="6bf9b-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="6bf9b-160">LOWER_ID</span></span>      | <span data-ttu-id="6bf9b-161">URL</span><span class="sxs-lookup"><span data-stu-id="6bf9b-161">URL</span></span>    | <span data-ttu-id="6bf9b-162">string</span><span class="sxs-lookup"><span data-stu-id="6bf9b-162">string</span></span> | <span data-ttu-id="6bf9b-163">да</span><span class="sxs-lookup"><span data-stu-id="6bf9b-163">yes</span></span>      | <span data-ttu-id="6bf9b-164">Идентификатор пакета, нижний регистр</span><span class="sxs-lookup"><span data-stu-id="6bf9b-164">The package ID, lowercase</span></span>
<span data-ttu-id="6bf9b-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="6bf9b-165">LOWER_VERSION</span></span> | <span data-ttu-id="6bf9b-166">URL</span><span class="sxs-lookup"><span data-stu-id="6bf9b-166">URL</span></span>    | <span data-ttu-id="6bf9b-167">string</span><span class="sxs-lookup"><span data-stu-id="6bf9b-167">string</span></span> | <span data-ttu-id="6bf9b-168">да</span><span class="sxs-lookup"><span data-stu-id="6bf9b-168">yes</span></span>      | <span data-ttu-id="6bf9b-169">Версия пакета, нормализованная и строчная</span><span class="sxs-lookup"><span data-stu-id="6bf9b-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="6bf9b-170">И, `LOWER_VERSION` и являются строчными, используя правила, реализованные. `LOWER_ID` СЕТЬ[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="6bf9b-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="6bf9b-171">метод.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-171">method.</span></span>

<span data-ttu-id="6bf9b-172">— Это требуемая версия пакета, нормализованная с помощью [правил нормализации](../concepts/package-versioning.md#normalized-version-numbers)версий NuGet. `LOWER_VERSION`</span><span class="sxs-lookup"><span data-stu-id="6bf9b-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="6bf9b-173">Это означает, что в этом случае необходимо исключить метаданные сборки, которые допускаются спецификацией SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="6bf9b-174">Текст ответа</span><span class="sxs-lookup"><span data-stu-id="6bf9b-174">Response body</span></span>

<span data-ttu-id="6bf9b-175">Если пакет существует в источнике пакета, возвращается код состояния 200.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="6bf9b-176">Текст ответа будет самим содержимым пакета.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="6bf9b-177">Если пакет не существует в источнике пакета, возвращается код состояния 404.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="6bf9b-178">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="6bf9b-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="6bf9b-179">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="6bf9b-179">Sample response</span></span>

<span data-ttu-id="6bf9b-180">Двоичный поток, который является файлом. nupkg для Newtonsoft. JSON 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="6bf9b-181">Скачать манифест пакета (. nuspec)</span><span class="sxs-lookup"><span data-stu-id="6bf9b-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="6bf9b-182">Если клиент знает идентификатор и версию пакета и хочет скачать манифест пакета, ему нужно только создать следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="6bf9b-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="6bf9b-183">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="6bf9b-183">Request parameters</span></span>

<span data-ttu-id="6bf9b-184">name</span><span class="sxs-lookup"><span data-stu-id="6bf9b-184">Name</span></span>          | <span data-ttu-id="6bf9b-185">In</span><span class="sxs-lookup"><span data-stu-id="6bf9b-185">In</span></span>     | <span data-ttu-id="6bf9b-186">Тип</span><span class="sxs-lookup"><span data-stu-id="6bf9b-186">Type</span></span>   | <span data-ttu-id="6bf9b-187">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6bf9b-187">Required</span></span> | <span data-ttu-id="6bf9b-188">Примечания</span><span class="sxs-lookup"><span data-stu-id="6bf9b-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="6bf9b-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="6bf9b-189">LOWER_ID</span></span>      | <span data-ttu-id="6bf9b-190">URL</span><span class="sxs-lookup"><span data-stu-id="6bf9b-190">URL</span></span>    | <span data-ttu-id="6bf9b-191">string</span><span class="sxs-lookup"><span data-stu-id="6bf9b-191">string</span></span> | <span data-ttu-id="6bf9b-192">да</span><span class="sxs-lookup"><span data-stu-id="6bf9b-192">yes</span></span>      | <span data-ttu-id="6bf9b-193">Идентификатор пакета, нижний регистр</span><span class="sxs-lookup"><span data-stu-id="6bf9b-193">The package ID, lowercase</span></span>
<span data-ttu-id="6bf9b-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="6bf9b-194">LOWER_VERSION</span></span> | <span data-ttu-id="6bf9b-195">URL</span><span class="sxs-lookup"><span data-stu-id="6bf9b-195">URL</span></span>    | <span data-ttu-id="6bf9b-196">string</span><span class="sxs-lookup"><span data-stu-id="6bf9b-196">string</span></span> | <span data-ttu-id="6bf9b-197">да</span><span class="sxs-lookup"><span data-stu-id="6bf9b-197">yes</span></span>      | <span data-ttu-id="6bf9b-198">Версия пакета, нормализованная и строчная</span><span class="sxs-lookup"><span data-stu-id="6bf9b-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="6bf9b-199">И, `LOWER_VERSION` и являются строчными, используя правила, реализованные. `LOWER_ID` [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Метод NET.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="6bf9b-200">— Это требуемая версия пакета, нормализованная с помощью [правил нормализации](../concepts/package-versioning.md#normalized-version-numbers)версий NuGet. `LOWER_VERSION`</span><span class="sxs-lookup"><span data-stu-id="6bf9b-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="6bf9b-201">Это означает, что в этом случае необходимо исключить метаданные сборки, которые допускаются спецификацией SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="6bf9b-202">Текст ответа</span><span class="sxs-lookup"><span data-stu-id="6bf9b-202">Response body</span></span>

<span data-ttu-id="6bf9b-203">Если пакет существует в источнике пакета, возвращается код состояния 200.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="6bf9b-204">Текст ответа будет манифестом пакета, который является. nuspec, содержащимся в соответствующем nupkg.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="6bf9b-205">Nuspec — это XML-документ.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="6bf9b-206">Если пакет не существует в источнике пакета, возвращается код состояния 404.</span><span class="sxs-lookup"><span data-stu-id="6bf9b-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="6bf9b-207">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="6bf9b-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="6bf9b-208">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="6bf9b-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
