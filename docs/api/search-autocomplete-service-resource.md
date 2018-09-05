---
title: Функция автозаполнения, API NuGet
description: Служба поиска autocomplete поддерживает интерактивного поиска пакета, идентификаторы и версии.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 01f919dc3bbfb6752c8f8e055a3cd473ad194e75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549087"
---
# <a name="autocomplete"></a><span data-ttu-id="fe402-103">Автозавершение</span><span class="sxs-lookup"><span data-stu-id="fe402-103">Autocomplete</span></span>

<span data-ttu-id="fe402-104">Существует возможность пакета ИД и версию автозавершения работы с помощью V3 API.</span><span class="sxs-lookup"><span data-stu-id="fe402-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="fe402-105">Ресурс, используемый для автозаполнения запросов является `SearchAutocompleteService` найти ресурс в [индекс службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="fe402-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="fe402-106">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="fe402-106">Versioning</span></span>

<span data-ttu-id="fe402-107">Следующие `@type` значения используются:</span><span class="sxs-lookup"><span data-stu-id="fe402-107">The following `@type` values are used:</span></span>

<span data-ttu-id="fe402-108">Значение @type</span><span class="sxs-lookup"><span data-stu-id="fe402-108">@type value</span></span>                          | <span data-ttu-id="fe402-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="fe402-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="fe402-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="fe402-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="fe402-111">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="fe402-111">The initial release</span></span>
<span data-ttu-id="fe402-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="fe402-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="fe402-113">Псевдоним `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="fe402-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="fe402-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="fe402-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="fe402-115">Псевдоним `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="fe402-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="fe402-116">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="fe402-116">Base URL</span></span>

<span data-ttu-id="fe402-117">Базовый URL-адрес для следующих API-интерфейсов является значением `@id` свойства, связанные с одной из упомянутых выше ресурсов `@type` значения.</span><span class="sxs-lookup"><span data-stu-id="fe402-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="fe402-118">В следующем документе заполнитель базовый URL-адрес `{@id}` будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="fe402-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="fe402-119">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="fe402-119">HTTP Methods</span></span>

<span data-ttu-id="fe402-120">Все URL-адреса, найден в регистрации ресурсов поддерживают методы HTTP `GET` и `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="fe402-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="fe402-121">Найдите пакет идентификаторы</span><span class="sxs-lookup"><span data-stu-id="fe402-121">Search for package IDs</span></span>

<span data-ttu-id="fe402-122">Первый API автозаполнения поддерживает поиск строки идентификатор пакета.</span><span class="sxs-lookup"><span data-stu-id="fe402-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="fe402-123">Это очень удобно, если вы хотите предоставить функцию typeahead пакета в пользовательском интерфейсе, интегрированных с источником пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="fe402-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="fe402-124">Пакет, содержащий только версии, отсутствующие в списке не появится в результатах.</span><span class="sxs-lookup"><span data-stu-id="fe402-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="fe402-125">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="fe402-125">Request parameters</span></span>

<span data-ttu-id="fe402-126">name</span><span class="sxs-lookup"><span data-stu-id="fe402-126">Name</span></span>        | <span data-ttu-id="fe402-127">Увеличение</span><span class="sxs-lookup"><span data-stu-id="fe402-127">In</span></span>     | <span data-ttu-id="fe402-128">Тип</span><span class="sxs-lookup"><span data-stu-id="fe402-128">Type</span></span>    | <span data-ttu-id="fe402-129">Обязательно</span><span class="sxs-lookup"><span data-stu-id="fe402-129">Required</span></span> | <span data-ttu-id="fe402-130">Примечания</span><span class="sxs-lookup"><span data-stu-id="fe402-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="fe402-131">q</span><span class="sxs-lookup"><span data-stu-id="fe402-131">q</span></span>           | <span data-ttu-id="fe402-132">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="fe402-132">URL</span></span>    | <span data-ttu-id="fe402-133">string</span><span class="sxs-lookup"><span data-stu-id="fe402-133">string</span></span>  | <span data-ttu-id="fe402-134">Нет</span><span class="sxs-lookup"><span data-stu-id="fe402-134">no</span></span>       | <span data-ttu-id="fe402-135">Строка, сравниваемая с идентификаторами пакетов</span><span class="sxs-lookup"><span data-stu-id="fe402-135">The string to compare against package IDs</span></span>
<span data-ttu-id="fe402-136">skip</span><span class="sxs-lookup"><span data-stu-id="fe402-136">skip</span></span>        | <span data-ttu-id="fe402-137">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="fe402-137">URL</span></span>    | <span data-ttu-id="fe402-138">целочисленный</span><span class="sxs-lookup"><span data-stu-id="fe402-138">integer</span></span> | <span data-ttu-id="fe402-139">Нет</span><span class="sxs-lookup"><span data-stu-id="fe402-139">no</span></span>       | <span data-ttu-id="fe402-140">Количество пропускаемых для разбиения на страницы результатов</span><span class="sxs-lookup"><span data-stu-id="fe402-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="fe402-141">Take</span><span class="sxs-lookup"><span data-stu-id="fe402-141">take</span></span>        | <span data-ttu-id="fe402-142">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="fe402-142">URL</span></span>    | <span data-ttu-id="fe402-143">целочисленный</span><span class="sxs-lookup"><span data-stu-id="fe402-143">integer</span></span> | <span data-ttu-id="fe402-144">Нет</span><span class="sxs-lookup"><span data-stu-id="fe402-144">no</span></span>       | <span data-ttu-id="fe402-145">Количество результатов, возвращаемых для разбиения на страницы</span><span class="sxs-lookup"><span data-stu-id="fe402-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="fe402-146">Предварительные выпуски</span><span class="sxs-lookup"><span data-stu-id="fe402-146">prerelease</span></span>  | <span data-ttu-id="fe402-147">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="fe402-147">URL</span></span>    | <span data-ttu-id="fe402-148">boolean</span><span class="sxs-lookup"><span data-stu-id="fe402-148">boolean</span></span> | <span data-ttu-id="fe402-149">Нет</span><span class="sxs-lookup"><span data-stu-id="fe402-149">no</span></span>       | <span data-ttu-id="fe402-150">`true` или `false` определения, следует ли включать [пакетов предварительных версий](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="fe402-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="fe402-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="fe402-151">semVerLevel</span></span> | <span data-ttu-id="fe402-152">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="fe402-152">URL</span></span>    | <span data-ttu-id="fe402-153">string</span><span class="sxs-lookup"><span data-stu-id="fe402-153">string</span></span>  | <span data-ttu-id="fe402-154">Нет</span><span class="sxs-lookup"><span data-stu-id="fe402-154">no</span></span>       | <span data-ttu-id="fe402-155">Строка версии SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="fe402-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="fe402-156">Автозаполнение запроса `q` анализируется таким образом, определяется в реализации сервера.</span><span class="sxs-lookup"><span data-stu-id="fe402-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="fe402-157">NuGet.org поддерживает выполнение запросов для префикса маркеров Идентификации пакета, которые являются элементами идентификатор созданного разделение исходного по camel знаков и символов.</span><span class="sxs-lookup"><span data-stu-id="fe402-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="fe402-158">`skip` Параметр по умолчанию равен 0.</span><span class="sxs-lookup"><span data-stu-id="fe402-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="fe402-159">`take` Параметр должен быть целым числом больше нуля.</span><span class="sxs-lookup"><span data-stu-id="fe402-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="fe402-160">Реализация сервера может привести к повышению максимальное значение.</span><span class="sxs-lookup"><span data-stu-id="fe402-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="fe402-161">Если `prerelease` не указан, исключаются пакеты предварительного выпуска.</span><span class="sxs-lookup"><span data-stu-id="fe402-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="fe402-162">`semVerLevel` Параметра запроса используется для согласиться на [SemVer 2.0.0 пакетов](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="fe402-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="fe402-163">Если этот параметр запроса не исключается, будут возвращены только идентификаторы пакета с SemVer 1.0.0 совместимые версии (с [стандартный управления версиями NuGet](../reference/package-versioning.md) предупреждения, такие как строки версии с 4 частей целого числа).</span><span class="sxs-lookup"><span data-stu-id="fe402-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="fe402-164">Если `semVerLevel=2.0.0` не указан, будет возвращено SemVer 1.0.0 и совместимые пакеты SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="fe402-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="fe402-165">См. в разделе [поддержки SemVer 2.0.0 для nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="fe402-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="fe402-166">Ответ</span><span class="sxs-lookup"><span data-stu-id="fe402-166">Response</span></span>

<span data-ttu-id="fe402-167">Ответ является документ JSON, содержащий до `take` результаты автозаполнения.</span><span class="sxs-lookup"><span data-stu-id="fe402-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="fe402-168">Корневой объект JSON имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="fe402-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="fe402-169">name</span><span class="sxs-lookup"><span data-stu-id="fe402-169">Name</span></span>      | <span data-ttu-id="fe402-170">Тип</span><span class="sxs-lookup"><span data-stu-id="fe402-170">Type</span></span>             | <span data-ttu-id="fe402-171">Обязательно</span><span class="sxs-lookup"><span data-stu-id="fe402-171">Required</span></span> | <span data-ttu-id="fe402-172">Примечания</span><span class="sxs-lookup"><span data-stu-id="fe402-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="fe402-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="fe402-173">totalHits</span></span> | <span data-ttu-id="fe402-174">целочисленный</span><span class="sxs-lookup"><span data-stu-id="fe402-174">integer</span></span>          | <span data-ttu-id="fe402-175">да</span><span class="sxs-lookup"><span data-stu-id="fe402-175">yes</span></span>      | <span data-ttu-id="fe402-176">Общее количество совпадений, без учета `skip` и `take`</span><span class="sxs-lookup"><span data-stu-id="fe402-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="fe402-177">Данные</span><span class="sxs-lookup"><span data-stu-id="fe402-177">data</span></span>      | <span data-ttu-id="fe402-178">Массив строк</span><span class="sxs-lookup"><span data-stu-id="fe402-178">array of strings</span></span> | <span data-ttu-id="fe402-179">да</span><span class="sxs-lookup"><span data-stu-id="fe402-179">yes</span></span>      | <span data-ttu-id="fe402-180">Пакет идентификаторы запрос соответствует</span><span class="sxs-lookup"><span data-stu-id="fe402-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="fe402-181">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="fe402-181">Sample request</span></span>

<span data-ttu-id="fe402-182">ПОЛУЧИТЬ https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="fe402-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="fe402-183">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="fe402-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="fe402-184">Перечисление версий пакета</span><span class="sxs-lookup"><span data-stu-id="fe402-184">Enumerate package versions</span></span>

<span data-ttu-id="fe402-185">После обнаружения идентификатор пакета с помощью предыдущего API, клиент может использовать API автозаполнения для перечисления версии пакетов для идентификатора указанный пакет.</span><span class="sxs-lookup"><span data-stu-id="fe402-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="fe402-186">Версии пакета, отсутствующие в списке не появится в результатах.</span><span class="sxs-lookup"><span data-stu-id="fe402-186">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="fe402-187">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="fe402-187">Request parameters</span></span>

<span data-ttu-id="fe402-188">name</span><span class="sxs-lookup"><span data-stu-id="fe402-188">Name</span></span>        | <span data-ttu-id="fe402-189">Увеличение</span><span class="sxs-lookup"><span data-stu-id="fe402-189">In</span></span>     | <span data-ttu-id="fe402-190">Тип</span><span class="sxs-lookup"><span data-stu-id="fe402-190">Type</span></span>    | <span data-ttu-id="fe402-191">Обязательно</span><span class="sxs-lookup"><span data-stu-id="fe402-191">Required</span></span> | <span data-ttu-id="fe402-192">Примечания</span><span class="sxs-lookup"><span data-stu-id="fe402-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="fe402-193">id</span><span class="sxs-lookup"><span data-stu-id="fe402-193">id</span></span>          | <span data-ttu-id="fe402-194">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="fe402-194">URL</span></span>    | <span data-ttu-id="fe402-195">string</span><span class="sxs-lookup"><span data-stu-id="fe402-195">string</span></span>  | <span data-ttu-id="fe402-196">да</span><span class="sxs-lookup"><span data-stu-id="fe402-196">yes</span></span>      | <span data-ttu-id="fe402-197">Идентификатор пакета для получения версии для</span><span class="sxs-lookup"><span data-stu-id="fe402-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="fe402-198">Предварительные выпуски</span><span class="sxs-lookup"><span data-stu-id="fe402-198">prerelease</span></span>  | <span data-ttu-id="fe402-199">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="fe402-199">URL</span></span>    | <span data-ttu-id="fe402-200">boolean</span><span class="sxs-lookup"><span data-stu-id="fe402-200">boolean</span></span> | <span data-ttu-id="fe402-201">Нет</span><span class="sxs-lookup"><span data-stu-id="fe402-201">no</span></span>       | <span data-ttu-id="fe402-202">`true` или `false` определения, следует ли включать [пакетов предварительных версий](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="fe402-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="fe402-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="fe402-203">semVerLevel</span></span> | <span data-ttu-id="fe402-204">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="fe402-204">URL</span></span>    | <span data-ttu-id="fe402-205">string</span><span class="sxs-lookup"><span data-stu-id="fe402-205">string</span></span>  | <span data-ttu-id="fe402-206">Нет</span><span class="sxs-lookup"><span data-stu-id="fe402-206">no</span></span>       | <span data-ttu-id="fe402-207">Строка версии SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="fe402-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="fe402-208">Если `prerelease` не указан, исключаются пакеты предварительного выпуска.</span><span class="sxs-lookup"><span data-stu-id="fe402-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="fe402-209">`semVerLevel` Параметра запроса используется для согласиться на пакеты SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="fe402-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="fe402-210">Если этот параметр запроса не исключается, будет возвращаться только версии SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="fe402-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="fe402-211">Если `semVerLevel=2.0.0` не указан, будет возвращено SemVer 1.0.0 и версии SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="fe402-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="fe402-212">См. в разделе [поддержки SemVer 2.0.0 для nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="fe402-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="fe402-213">Ответ</span><span class="sxs-lookup"><span data-stu-id="fe402-213">Response</span></span>

<span data-ttu-id="fe402-214">Ответом является документ JSON, содержащий все версии пакетов идентификатора указанный пакет, фильтрация по заданным параметрам запроса.</span><span class="sxs-lookup"><span data-stu-id="fe402-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="fe402-215">Корневой объект JSON имеет следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="fe402-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="fe402-216">name</span><span class="sxs-lookup"><span data-stu-id="fe402-216">Name</span></span>      | <span data-ttu-id="fe402-217">Тип</span><span class="sxs-lookup"><span data-stu-id="fe402-217">Type</span></span>             | <span data-ttu-id="fe402-218">Обязательно</span><span class="sxs-lookup"><span data-stu-id="fe402-218">Required</span></span> | <span data-ttu-id="fe402-219">Примечания</span><span class="sxs-lookup"><span data-stu-id="fe402-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="fe402-220">Данные</span><span class="sxs-lookup"><span data-stu-id="fe402-220">data</span></span>      | <span data-ttu-id="fe402-221">Массив строк</span><span class="sxs-lookup"><span data-stu-id="fe402-221">array of strings</span></span> | <span data-ttu-id="fe402-222">да</span><span class="sxs-lookup"><span data-stu-id="fe402-222">yes</span></span>      | <span data-ttu-id="fe402-223">Версии пакетов, совпадающих с запроса</span><span class="sxs-lookup"><span data-stu-id="fe402-223">The package versions matched by the request</span></span>

<span data-ttu-id="fe402-224">Версии пакетов в `data` массив может содержать метаданные сборки SemVer 2.0.0 (например `1.0.0+metadata`) Если `semVerLevel=2.0.0` был представлен в строке запроса.</span><span class="sxs-lookup"><span data-stu-id="fe402-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="fe402-225">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="fe402-225">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="fe402-226">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="fe402-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
