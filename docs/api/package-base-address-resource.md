---
title: Содержимое пакета, NuGet API
description: Базовый адрес пакета — это простой интерфейс для получения самого пакета.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2f0f93e0cee78ea03cbd53194cdc2a10871fd7e1
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426765"
---
# <a name="package-content"></a><span data-ttu-id="4ba56-103">Содержимое пакета</span><span class="sxs-lookup"><span data-stu-id="4ba56-103">Package Content</span></span>

<span data-ttu-id="4ba56-104">Это можно создать URL-адрес для получения содержимого произвольного пакета (nupkg-файл) с помощью V3 API.</span><span class="sxs-lookup"><span data-stu-id="4ba56-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="4ba56-105">Ресурс, используемый для извлечения содержимого пакета является `PackageBaseAddress` найти ресурс в [индекс службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="4ba56-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="4ba56-106">Этот ресурс также позволяет обнаружить все версии пакета, в списке или удалена из списка.</span><span class="sxs-lookup"><span data-stu-id="4ba56-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="4ba56-107">Этот ресурс называется как «пакет базовый адрес» или «неструктурированный контейнер».</span><span class="sxs-lookup"><span data-stu-id="4ba56-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="4ba56-108">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="4ba56-108">Versioning</span></span>

<span data-ttu-id="4ba56-109">Следующие `@type` используется значение:</span><span class="sxs-lookup"><span data-stu-id="4ba56-109">The following `@type` value is used:</span></span>

<span data-ttu-id="4ba56-110">Значение@type</span><span class="sxs-lookup"><span data-stu-id="4ba56-110">@type value</span></span>              | <span data-ttu-id="4ba56-111">Примечания</span><span class="sxs-lookup"><span data-stu-id="4ba56-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="4ba56-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="4ba56-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="4ba56-113">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="4ba56-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="4ba56-114">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="4ba56-114">Base URL</span></span>

<span data-ttu-id="4ba56-115">Базовый URL-адрес для следующих API-интерфейсов является значением `@id` свойство, связанное с ресурсом, упомянутых выше `@type` значение.</span><span class="sxs-lookup"><span data-stu-id="4ba56-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="4ba56-116">В следующем документе заполнитель базовый URL-адрес `{@id}` будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="4ba56-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="4ba56-117">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="4ba56-117">HTTP methods</span></span>

<span data-ttu-id="4ba56-118">Все URL-адреса, найден в регистрации ресурсов поддерживают методы HTTP `GET` и `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="4ba56-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="4ba56-119">Перечисление версий пакета</span><span class="sxs-lookup"><span data-stu-id="4ba56-119">Enumerate package versions</span></span>

<span data-ttu-id="4ba56-120">Если клиент знает идентификатор пакета и хочет обнаружение также пакеты версии пакета источник имеет доступен, клиент можно создать прогнозируемые URL-адрес для перечисления всех версий пакета.</span><span class="sxs-lookup"><span data-stu-id="4ba56-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="4ba56-121">Этот список предназначен быть «список каталогов» для API содержимого пакета, указанный ниже.</span><span class="sxs-lookup"><span data-stu-id="4ba56-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="4ba56-122">Этот список содержит обе версии перечисленных и отсутствующие в списке пакетов.</span><span class="sxs-lookup"><span data-stu-id="4ba56-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="4ba56-123">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="4ba56-123">Request parameters</span></span>

<span data-ttu-id="4ba56-124">name</span><span class="sxs-lookup"><span data-stu-id="4ba56-124">Name</span></span>     | <span data-ttu-id="4ba56-125">Увеличение</span><span class="sxs-lookup"><span data-stu-id="4ba56-125">In</span></span>     | <span data-ttu-id="4ba56-126">Тип</span><span class="sxs-lookup"><span data-stu-id="4ba56-126">Type</span></span>    | <span data-ttu-id="4ba56-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="4ba56-127">Required</span></span> | <span data-ttu-id="4ba56-128">Примечания</span><span class="sxs-lookup"><span data-stu-id="4ba56-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="4ba56-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="4ba56-129">LOWER_ID</span></span> | <span data-ttu-id="4ba56-130">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="4ba56-130">URL</span></span>    | <span data-ttu-id="4ba56-131">string</span><span class="sxs-lookup"><span data-stu-id="4ba56-131">string</span></span>  | <span data-ttu-id="4ba56-132">да</span><span class="sxs-lookup"><span data-stu-id="4ba56-132">yes</span></span>      | <span data-ttu-id="4ba56-133">Идентификатор пакета, нижний регистр</span><span class="sxs-lookup"><span data-stu-id="4ba56-133">The package ID, lowercase</span></span>

<span data-ttu-id="4ba56-134">`LOWER_ID` Значение является Идентификатором нужного пакета букв с помощью правил, реализованных по. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) метод.</span><span class="sxs-lookup"><span data-stu-id="4ba56-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="4ba56-135">Ответ</span><span class="sxs-lookup"><span data-stu-id="4ba56-135">Response</span></span>

<span data-ttu-id="4ba56-136">Если источник пакета не установлены версии идентификатор предоставленного пакета, возвращается код состояния 404.</span><span class="sxs-lookup"><span data-stu-id="4ba56-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="4ba56-137">Если источник имеет один или несколько версий, возвращается код состояния 200.</span><span class="sxs-lookup"><span data-stu-id="4ba56-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="4ba56-138">Текст ответа представляет собой объект JSON со следующим свойством:</span><span class="sxs-lookup"><span data-stu-id="4ba56-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="4ba56-139">name</span><span class="sxs-lookup"><span data-stu-id="4ba56-139">Name</span></span>     | <span data-ttu-id="4ba56-140">Тип</span><span class="sxs-lookup"><span data-stu-id="4ba56-140">Type</span></span>             | <span data-ttu-id="4ba56-141">Обязательно</span><span class="sxs-lookup"><span data-stu-id="4ba56-141">Required</span></span> | <span data-ttu-id="4ba56-142">Примечания</span><span class="sxs-lookup"><span data-stu-id="4ba56-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="4ba56-143">версии</span><span class="sxs-lookup"><span data-stu-id="4ba56-143">versions</span></span> | <span data-ttu-id="4ba56-144">Массив строк</span><span class="sxs-lookup"><span data-stu-id="4ba56-144">array of strings</span></span> | <span data-ttu-id="4ba56-145">да</span><span class="sxs-lookup"><span data-stu-id="4ba56-145">yes</span></span>      | <span data-ttu-id="4ba56-146">Идентификаторы, доступные пакета</span><span class="sxs-lookup"><span data-stu-id="4ba56-146">The package IDs available</span></span>

<span data-ttu-id="4ba56-147">Строки в `versions` массив всех букв, [нормализовать строки версии NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="4ba56-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="4ba56-148">Строки версии не содержат все метаданные сборки SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="4ba56-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="4ba56-149">Цель состоит в том, что версии строк, найденных в этот массив может использоваться непосредственно для `LOWER_VERSION` токенов см. в следующих конечных точек.</span><span class="sxs-lookup"><span data-stu-id="4ba56-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="4ba56-150">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="4ba56-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="4ba56-151">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="4ba56-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="4ba56-152">Скачать содержимое пакета (файла nupkg)</span><span class="sxs-lookup"><span data-stu-id="4ba56-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="4ba56-153">Если клиент знает ИД пакета и версии и хочет загрузить содержимое пакета, они достаточно создать следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="4ba56-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="4ba56-154">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="4ba56-154">Request parameters</span></span>

<span data-ttu-id="4ba56-155">name</span><span class="sxs-lookup"><span data-stu-id="4ba56-155">Name</span></span>          | <span data-ttu-id="4ba56-156">Увеличение</span><span class="sxs-lookup"><span data-stu-id="4ba56-156">In</span></span>     | <span data-ttu-id="4ba56-157">Тип</span><span class="sxs-lookup"><span data-stu-id="4ba56-157">Type</span></span>   | <span data-ttu-id="4ba56-158">Обязательно</span><span class="sxs-lookup"><span data-stu-id="4ba56-158">Required</span></span> | <span data-ttu-id="4ba56-159">Примечания</span><span class="sxs-lookup"><span data-stu-id="4ba56-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="4ba56-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="4ba56-160">LOWER_ID</span></span>      | <span data-ttu-id="4ba56-161">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="4ba56-161">URL</span></span>    | <span data-ttu-id="4ba56-162">string</span><span class="sxs-lookup"><span data-stu-id="4ba56-162">string</span></span> | <span data-ttu-id="4ba56-163">да</span><span class="sxs-lookup"><span data-stu-id="4ba56-163">yes</span></span>      | <span data-ttu-id="4ba56-164">Идентификатор пакета, нижний регистр</span><span class="sxs-lookup"><span data-stu-id="4ba56-164">The package ID, lowercase</span></span>
<span data-ttu-id="4ba56-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="4ba56-165">LOWER_VERSION</span></span> | <span data-ttu-id="4ba56-166">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="4ba56-166">URL</span></span>    | <span data-ttu-id="4ba56-167">string</span><span class="sxs-lookup"><span data-stu-id="4ba56-167">string</span></span> | <span data-ttu-id="4ba56-168">да</span><span class="sxs-lookup"><span data-stu-id="4ba56-168">yes</span></span>      | <span data-ttu-id="4ba56-169">Версия пакета, нормализованную и букв</span><span class="sxs-lookup"><span data-stu-id="4ba56-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="4ba56-170">Оба `LOWER_ID` и `LOWER_VERSION` являются букв с помощью правил, реализованных по. NET [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="4ba56-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="4ba56-171">метод.</span><span class="sxs-lookup"><span data-stu-id="4ba56-171">method.</span></span>

<span data-ttu-id="4ba56-172">`LOWER_VERSION` Нужного пакета версии нормализуется с использованием NuGet версии [правила нормализации](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="4ba56-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="4ba56-173">Это означает, что в этом случае необходимо исключить эти метаданные сборки, для которых разрешено в спецификации SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="4ba56-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="4ba56-174">Текст ответа</span><span class="sxs-lookup"><span data-stu-id="4ba56-174">Response body</span></span>

<span data-ttu-id="4ba56-175">Если пакет существует в источнике пакета, возвращается код состояния 200.</span><span class="sxs-lookup"><span data-stu-id="4ba56-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="4ba56-176">Текст ответа будет само содержимое пакета.</span><span class="sxs-lookup"><span data-stu-id="4ba56-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="4ba56-177">Если пакет не существует в источнике пакета, возвращается код состояния 404.</span><span class="sxs-lookup"><span data-stu-id="4ba56-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="4ba56-178">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="4ba56-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="4ba56-179">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="4ba56-179">Sample response</span></span>

<span data-ttu-id="4ba56-180">Двоичный поток, который является файл nupkg для Newtonsoft.Json 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="4ba56-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="4ba56-181">Загрузить манифест пакета (файлу nuspec)</span><span class="sxs-lookup"><span data-stu-id="4ba56-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="4ba56-182">Если клиент знает ИД пакета и версии и хочет загрузить манифест пакета, они достаточно создать следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="4ba56-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="4ba56-183">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="4ba56-183">Request parameters</span></span>

<span data-ttu-id="4ba56-184">name</span><span class="sxs-lookup"><span data-stu-id="4ba56-184">Name</span></span>          | <span data-ttu-id="4ba56-185">Увеличение</span><span class="sxs-lookup"><span data-stu-id="4ba56-185">In</span></span>     | <span data-ttu-id="4ba56-186">Тип</span><span class="sxs-lookup"><span data-stu-id="4ba56-186">Type</span></span>   | <span data-ttu-id="4ba56-187">Обязательно</span><span class="sxs-lookup"><span data-stu-id="4ba56-187">Required</span></span> | <span data-ttu-id="4ba56-188">Примечания</span><span class="sxs-lookup"><span data-stu-id="4ba56-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="4ba56-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="4ba56-189">LOWER_ID</span></span>      | <span data-ttu-id="4ba56-190">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="4ba56-190">URL</span></span>    | <span data-ttu-id="4ba56-191">string</span><span class="sxs-lookup"><span data-stu-id="4ba56-191">string</span></span> | <span data-ttu-id="4ba56-192">да</span><span class="sxs-lookup"><span data-stu-id="4ba56-192">yes</span></span>      | <span data-ttu-id="4ba56-193">Идентификатор пакета, нижний регистр</span><span class="sxs-lookup"><span data-stu-id="4ba56-193">The package ID, lowercase</span></span>
<span data-ttu-id="4ba56-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="4ba56-194">LOWER_VERSION</span></span> | <span data-ttu-id="4ba56-195">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="4ba56-195">URL</span></span>    | <span data-ttu-id="4ba56-196">string</span><span class="sxs-lookup"><span data-stu-id="4ba56-196">string</span></span> | <span data-ttu-id="4ba56-197">да</span><span class="sxs-lookup"><span data-stu-id="4ba56-197">yes</span></span>      | <span data-ttu-id="4ba56-198">Версия пакета, нормализованную и букв</span><span class="sxs-lookup"><span data-stu-id="4ba56-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="4ba56-199">Оба `LOWER_ID` и `LOWER_VERSION` являются букв с помощью правил, реализованных по. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) метод.</span><span class="sxs-lookup"><span data-stu-id="4ba56-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="4ba56-200">`LOWER_VERSION` Нужного пакета версии нормализуется с использованием NuGet версии [правила нормализации](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="4ba56-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="4ba56-201">Это означает, что в этом случае необходимо исключить эти метаданные сборки, для которых разрешено в спецификации SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="4ba56-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="4ba56-202">Текст ответа</span><span class="sxs-lookup"><span data-stu-id="4ba56-202">Response body</span></span>

<span data-ttu-id="4ba56-203">Если пакет существует в источнике пакета, возвращается код состояния 200.</span><span class="sxs-lookup"><span data-stu-id="4ba56-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="4ba56-204">Текст ответа будет манифест пакета, который является файла nuspec, из соответствующего файла nupkg.</span><span class="sxs-lookup"><span data-stu-id="4ba56-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="4ba56-205">Файла nuspec — это документ XML.</span><span class="sxs-lookup"><span data-stu-id="4ba56-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="4ba56-206">Если пакет не существует в источнике пакета, возвращается код состояния 404.</span><span class="sxs-lookup"><span data-stu-id="4ba56-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="4ba56-207">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="4ba56-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="4ba56-208">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="4ba56-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
