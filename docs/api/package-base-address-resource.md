---
title: Содержимое пакета, API NuGet
description: Базовый адрес пакета — это простой интерфейс для выборки самого пакета.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 5ec6c0e17a3e8b9a3f156a48685bcaafe42c744b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488224"
---
# <a name="package-content"></a><span data-ttu-id="bc819-103">Содержимое пакета</span><span class="sxs-lookup"><span data-stu-id="bc819-103">Package Content</span></span>

<span data-ttu-id="bc819-104">Можно создать URL-адрес для выборки содержимого произвольного пакета (nupkg-файла) с помощью API V3.</span><span class="sxs-lookup"><span data-stu-id="bc819-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="bc819-105">Ресурс, используемый для выборки содержимого пакета, — `PackageBaseAddress` это ресурс, найденный в [индексе службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="bc819-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="bc819-106">Этот ресурс также включает обнаружение всех версий пакета, перечисленных или отсутствующих в списке.</span><span class="sxs-lookup"><span data-stu-id="bc819-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="bc819-107">Этот ресурс обычно называется "базовым адресом пакета" или "плоским контейнером".</span><span class="sxs-lookup"><span data-stu-id="bc819-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="bc819-108">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="bc819-108">Versioning</span></span>

<span data-ttu-id="bc819-109">Используется следующее `@type` значение:</span><span class="sxs-lookup"><span data-stu-id="bc819-109">The following `@type` value is used:</span></span>

<span data-ttu-id="bc819-110">Значение@type</span><span class="sxs-lookup"><span data-stu-id="bc819-110">@type value</span></span>              | <span data-ttu-id="bc819-111">Примечания</span><span class="sxs-lookup"><span data-stu-id="bc819-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="bc819-112">Паккажебасеаддресс/3.0.0</span><span class="sxs-lookup"><span data-stu-id="bc819-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="bc819-113">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="bc819-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="bc819-114">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="bc819-114">Base URL</span></span>

<span data-ttu-id="bc819-115">Базовый URL-адрес для следующих интерфейсов API — это значение `@id` свойства, связанного с вышеупомянутым значением `@type` ресурса.</span><span class="sxs-lookup"><span data-stu-id="bc819-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="bc819-116">В следующем документе будет использоваться базовый URL-адрес `{@id}` заполнителя.</span><span class="sxs-lookup"><span data-stu-id="bc819-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="bc819-117">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="bc819-117">HTTP methods</span></span>

<span data-ttu-id="bc819-118">Все URL-адреса, найденные в ресурсе регистрации `GET` , `HEAD`поддерживают методы HTTP и.</span><span class="sxs-lookup"><span data-stu-id="bc819-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="bc819-119">Перечислить версии пакета</span><span class="sxs-lookup"><span data-stu-id="bc819-119">Enumerate package versions</span></span>

<span data-ttu-id="bc819-120">Если клиент знает идентификатор пакета и хочет определить, какие версии пакетов доступны в источнике пакета, клиент может создать прогнозируемый URL-адрес для перечисления всех версий пакета.</span><span class="sxs-lookup"><span data-stu-id="bc819-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="bc819-121">Этот список должен быть списком каталогов для API содержимого пакета, упомянутого ниже.</span><span class="sxs-lookup"><span data-stu-id="bc819-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="bc819-122">Этот список содержит как перечисленные, так и невключенные версии пакетов.</span><span class="sxs-lookup"><span data-stu-id="bc819-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="bc819-123">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="bc819-123">Request parameters</span></span>

<span data-ttu-id="bc819-124">name</span><span class="sxs-lookup"><span data-stu-id="bc819-124">Name</span></span>     | <span data-ttu-id="bc819-125">In</span><span class="sxs-lookup"><span data-stu-id="bc819-125">In</span></span>     | <span data-ttu-id="bc819-126">Тип</span><span class="sxs-lookup"><span data-stu-id="bc819-126">Type</span></span>    | <span data-ttu-id="bc819-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="bc819-127">Required</span></span> | <span data-ttu-id="bc819-128">Примечания</span><span class="sxs-lookup"><span data-stu-id="bc819-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="bc819-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="bc819-129">LOWER_ID</span></span> | <span data-ttu-id="bc819-130">URL</span><span class="sxs-lookup"><span data-stu-id="bc819-130">URL</span></span>    | <span data-ttu-id="bc819-131">string</span><span class="sxs-lookup"><span data-stu-id="bc819-131">string</span></span>  | <span data-ttu-id="bc819-132">да</span><span class="sxs-lookup"><span data-stu-id="bc819-132">yes</span></span>      | <span data-ttu-id="bc819-133">Идентификатор пакета, нижний регистр</span><span class="sxs-lookup"><span data-stu-id="bc819-133">The package ID, lowercase</span></span>

<span data-ttu-id="bc819-134">`LOWER_ID` Значение представляет собой требуемый идентификатор пакета в нижнем регистре, используя правила, реализованные. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Метод NET.</span><span class="sxs-lookup"><span data-stu-id="bc819-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="bc819-135">Отклик</span><span class="sxs-lookup"><span data-stu-id="bc819-135">Response</span></span>

<span data-ttu-id="bc819-136">Если источник пакета не имеет версий указанного идентификатора пакета, возвращается код состояния 404.</span><span class="sxs-lookup"><span data-stu-id="bc819-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="bc819-137">Если источник пакета имеет одну или несколько версий, возвращается код состояния 200.</span><span class="sxs-lookup"><span data-stu-id="bc819-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="bc819-138">Текст ответа — это объект JSON со следующим свойством:</span><span class="sxs-lookup"><span data-stu-id="bc819-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="bc819-139">name</span><span class="sxs-lookup"><span data-stu-id="bc819-139">Name</span></span>     | <span data-ttu-id="bc819-140">Тип</span><span class="sxs-lookup"><span data-stu-id="bc819-140">Type</span></span>             | <span data-ttu-id="bc819-141">Обязательно</span><span class="sxs-lookup"><span data-stu-id="bc819-141">Required</span></span> | <span data-ttu-id="bc819-142">Примечания</span><span class="sxs-lookup"><span data-stu-id="bc819-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="bc819-143">версии</span><span class="sxs-lookup"><span data-stu-id="bc819-143">versions</span></span> | <span data-ttu-id="bc819-144">Массив строк</span><span class="sxs-lookup"><span data-stu-id="bc819-144">array of strings</span></span> | <span data-ttu-id="bc819-145">да</span><span class="sxs-lookup"><span data-stu-id="bc819-145">yes</span></span>      | <span data-ttu-id="bc819-146">Идентификаторы пакетов доступны</span><span class="sxs-lookup"><span data-stu-id="bc819-146">The package IDs available</span></span>

<span data-ttu-id="bc819-147">Строки в `versions` массиве — это все строки нормализованных [строк версии NuGet](../concepts/package-versioning.md#normalized-version-numbers)в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="bc819-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="bc819-148">Строки версии не содержат метаданные сборки SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="bc819-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="bc819-149">Цель состоит в том, что строки версии, найденные в этом массиве, можно `LOWER_VERSION` использовать буквально для маркеров, найденных в следующих конечных точках.</span><span class="sxs-lookup"><span data-stu-id="bc819-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="bc819-150">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="bc819-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="bc819-151">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="bc819-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="bc819-152">Скачать содержимое пакета (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="bc819-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="bc819-153">Если клиент знает идентификатор и версию пакета и хочет загрузить содержимое пакета, необходимо создать только следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="bc819-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="bc819-154">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="bc819-154">Request parameters</span></span>

<span data-ttu-id="bc819-155">name</span><span class="sxs-lookup"><span data-stu-id="bc819-155">Name</span></span>          | <span data-ttu-id="bc819-156">In</span><span class="sxs-lookup"><span data-stu-id="bc819-156">In</span></span>     | <span data-ttu-id="bc819-157">Тип</span><span class="sxs-lookup"><span data-stu-id="bc819-157">Type</span></span>   | <span data-ttu-id="bc819-158">Обязательно</span><span class="sxs-lookup"><span data-stu-id="bc819-158">Required</span></span> | <span data-ttu-id="bc819-159">Примечания</span><span class="sxs-lookup"><span data-stu-id="bc819-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="bc819-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="bc819-160">LOWER_ID</span></span>      | <span data-ttu-id="bc819-161">URL</span><span class="sxs-lookup"><span data-stu-id="bc819-161">URL</span></span>    | <span data-ttu-id="bc819-162">string</span><span class="sxs-lookup"><span data-stu-id="bc819-162">string</span></span> | <span data-ttu-id="bc819-163">да</span><span class="sxs-lookup"><span data-stu-id="bc819-163">yes</span></span>      | <span data-ttu-id="bc819-164">Идентификатор пакета, нижний регистр</span><span class="sxs-lookup"><span data-stu-id="bc819-164">The package ID, lowercase</span></span>
<span data-ttu-id="bc819-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="bc819-165">LOWER_VERSION</span></span> | <span data-ttu-id="bc819-166">URL</span><span class="sxs-lookup"><span data-stu-id="bc819-166">URL</span></span>    | <span data-ttu-id="bc819-167">string</span><span class="sxs-lookup"><span data-stu-id="bc819-167">string</span></span> | <span data-ttu-id="bc819-168">да</span><span class="sxs-lookup"><span data-stu-id="bc819-168">yes</span></span>      | <span data-ttu-id="bc819-169">Версия пакета, нормализованная и строчная</span><span class="sxs-lookup"><span data-stu-id="bc819-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="bc819-170">И, `LOWER_VERSION` и являются строчными, используя правила, реализованные. `LOWER_ID` СЕТЬ[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="bc819-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="bc819-171">метод.</span><span class="sxs-lookup"><span data-stu-id="bc819-171">method.</span></span>

<span data-ttu-id="bc819-172">— Это требуемая версия пакета, нормализованная с помощью [правил нормализации](../concepts/package-versioning.md#normalized-version-numbers)версий NuGet. `LOWER_VERSION`</span><span class="sxs-lookup"><span data-stu-id="bc819-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="bc819-173">Это означает, что в этом случае необходимо исключить метаданные сборки, которые допускаются спецификацией SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="bc819-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="bc819-174">Текст ответа</span><span class="sxs-lookup"><span data-stu-id="bc819-174">Response body</span></span>

<span data-ttu-id="bc819-175">Если пакет существует в источнике пакета, возвращается код состояния 200.</span><span class="sxs-lookup"><span data-stu-id="bc819-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="bc819-176">Текст ответа будет самим содержимым пакета.</span><span class="sxs-lookup"><span data-stu-id="bc819-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="bc819-177">Если пакет не существует в источнике пакета, возвращается код состояния 404.</span><span class="sxs-lookup"><span data-stu-id="bc819-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="bc819-178">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="bc819-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="bc819-179">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="bc819-179">Sample response</span></span>

<span data-ttu-id="bc819-180">Двоичный поток, который является файлом. nupkg для Newtonsoft. JSON 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="bc819-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="bc819-181">Скачать манифест пакета (. nuspec)</span><span class="sxs-lookup"><span data-stu-id="bc819-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="bc819-182">Если клиент знает идентификатор и версию пакета и хочет скачать манифест пакета, ему нужно только создать следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="bc819-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="bc819-183">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="bc819-183">Request parameters</span></span>

<span data-ttu-id="bc819-184">name</span><span class="sxs-lookup"><span data-stu-id="bc819-184">Name</span></span>          | <span data-ttu-id="bc819-185">In</span><span class="sxs-lookup"><span data-stu-id="bc819-185">In</span></span>     | <span data-ttu-id="bc819-186">Тип</span><span class="sxs-lookup"><span data-stu-id="bc819-186">Type</span></span>   | <span data-ttu-id="bc819-187">Обязательно</span><span class="sxs-lookup"><span data-stu-id="bc819-187">Required</span></span> | <span data-ttu-id="bc819-188">Примечания</span><span class="sxs-lookup"><span data-stu-id="bc819-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="bc819-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="bc819-189">LOWER_ID</span></span>      | <span data-ttu-id="bc819-190">URL</span><span class="sxs-lookup"><span data-stu-id="bc819-190">URL</span></span>    | <span data-ttu-id="bc819-191">string</span><span class="sxs-lookup"><span data-stu-id="bc819-191">string</span></span> | <span data-ttu-id="bc819-192">да</span><span class="sxs-lookup"><span data-stu-id="bc819-192">yes</span></span>      | <span data-ttu-id="bc819-193">Идентификатор пакета, нижний регистр</span><span class="sxs-lookup"><span data-stu-id="bc819-193">The package ID, lowercase</span></span>
<span data-ttu-id="bc819-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="bc819-194">LOWER_VERSION</span></span> | <span data-ttu-id="bc819-195">URL</span><span class="sxs-lookup"><span data-stu-id="bc819-195">URL</span></span>    | <span data-ttu-id="bc819-196">string</span><span class="sxs-lookup"><span data-stu-id="bc819-196">string</span></span> | <span data-ttu-id="bc819-197">да</span><span class="sxs-lookup"><span data-stu-id="bc819-197">yes</span></span>      | <span data-ttu-id="bc819-198">Версия пакета, нормализованная и строчная</span><span class="sxs-lookup"><span data-stu-id="bc819-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="bc819-199">И, `LOWER_VERSION` и являются строчными, используя правила, реализованные. `LOWER_ID` [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Метод NET.</span><span class="sxs-lookup"><span data-stu-id="bc819-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="bc819-200">— Это требуемая версия пакета, нормализованная с помощью [правил нормализации](../concepts/package-versioning.md#normalized-version-numbers)версий NuGet. `LOWER_VERSION`</span><span class="sxs-lookup"><span data-stu-id="bc819-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="bc819-201">Это означает, что в этом случае необходимо исключить метаданные сборки, которые допускаются спецификацией SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="bc819-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="bc819-202">Текст ответа</span><span class="sxs-lookup"><span data-stu-id="bc819-202">Response body</span></span>

<span data-ttu-id="bc819-203">Если пакет существует в источнике пакета, возвращается код состояния 200.</span><span class="sxs-lookup"><span data-stu-id="bc819-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="bc819-204">Текст ответа будет манифестом пакета, который является. nuspec, содержащимся в соответствующем nupkg.</span><span class="sxs-lookup"><span data-stu-id="bc819-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="bc819-205">Nuspec — это XML-документ.</span><span class="sxs-lookup"><span data-stu-id="bc819-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="bc819-206">Если пакет не существует в источнике пакета, возвращается код состояния 404.</span><span class="sxs-lookup"><span data-stu-id="bc819-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="bc819-207">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="bc819-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="bc819-208">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="bc819-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
