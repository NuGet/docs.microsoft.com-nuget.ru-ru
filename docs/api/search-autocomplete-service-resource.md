---
title: Функция автозаполнения, API NuGet
description: Служба поиска autocomplete поддерживает интерактивного поиска пакета, идентификаторы и версии.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fdc3ad8aa239a42d8a4c169a757715e856bdcb41
ms.sourcegitcommit: 9f94e00428d83aef4a7a87db679129eff7720c59
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/03/2019
ms.locfileid: "58911053"
---
# <a name="autocomplete"></a><span data-ttu-id="ee0f1-103">Автозавершение</span><span class="sxs-lookup"><span data-stu-id="ee0f1-103">Autocomplete</span></span>

<span data-ttu-id="ee0f1-104">Существует возможность пакета ИД и версию автозавершения работы с помощью V3 API.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="ee0f1-105">Ресурс, используемый для автозаполнения запросов является `SearchAutocompleteService` найти ресурс в [индекс службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="ee0f1-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="ee0f1-106">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="ee0f1-106">Versioning</span></span>

<span data-ttu-id="ee0f1-107">Следующие `@type` значения используются:</span><span class="sxs-lookup"><span data-stu-id="ee0f1-107">The following `@type` values are used:</span></span>

<span data-ttu-id="ee0f1-108">Значение@type </span><span class="sxs-lookup"><span data-stu-id="ee0f1-108">@type value</span></span>                          | <span data-ttu-id="ee0f1-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="ee0f1-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="ee0f1-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="ee0f1-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="ee0f1-111">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="ee0f1-111">The initial release</span></span>
<span data-ttu-id="ee0f1-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="ee0f1-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="ee0f1-113">Псевдоним</span><span class="sxs-lookup"><span data-stu-id="ee0f1-113">Alias of</span></span> `SearchAutocompleteService`
<span data-ttu-id="ee0f1-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="ee0f1-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="ee0f1-115">Псевдоним</span><span class="sxs-lookup"><span data-stu-id="ee0f1-115">Alias of</span></span> `SearchAutocompleteService`

## <a name="base-url"></a><span data-ttu-id="ee0f1-116">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="ee0f1-116">Base URL</span></span>

<span data-ttu-id="ee0f1-117">Базовый URL-адрес для следующих API-интерфейсов является значением `@id` свойства, связанные с одной из упомянутых выше ресурсов `@type` значения.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="ee0f1-118">В следующем документе заполнитель базовый URL-адрес `{@id}` будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="ee0f1-119">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="ee0f1-119">HTTP Methods</span></span>

<span data-ttu-id="ee0f1-120">Все URL-адреса, найден в регистрации ресурсов поддерживают методы HTTP `GET` и `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="ee0f1-121">Найдите пакет идентификаторы</span><span class="sxs-lookup"><span data-stu-id="ee0f1-121">Search for package IDs</span></span>

<span data-ttu-id="ee0f1-122">Первый API автозаполнения поддерживает поиск строки идентификатор пакета.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="ee0f1-123">Это очень удобно, если вы хотите предоставить функцию typeahead пакета в пользовательском интерфейсе, интегрированных с источником пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="ee0f1-124">Пакет, содержащий только версии, отсутствующие в списке не появится в результатах.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="ee0f1-125">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="ee0f1-125">Request parameters</span></span>

<span data-ttu-id="ee0f1-126">name</span><span class="sxs-lookup"><span data-stu-id="ee0f1-126">Name</span></span>        | <span data-ttu-id="ee0f1-127">Увеличение</span><span class="sxs-lookup"><span data-stu-id="ee0f1-127">In</span></span>     | <span data-ttu-id="ee0f1-128">Тип</span><span class="sxs-lookup"><span data-stu-id="ee0f1-128">Type</span></span>    | <span data-ttu-id="ee0f1-129">Обязательно</span><span class="sxs-lookup"><span data-stu-id="ee0f1-129">Required</span></span> | <span data-ttu-id="ee0f1-130">Примечания</span><span class="sxs-lookup"><span data-stu-id="ee0f1-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="ee0f1-131">q</span><span class="sxs-lookup"><span data-stu-id="ee0f1-131">q</span></span>           | <span data-ttu-id="ee0f1-132">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="ee0f1-132">URL</span></span>    | <span data-ttu-id="ee0f1-133">string</span><span class="sxs-lookup"><span data-stu-id="ee0f1-133">string</span></span>  | <span data-ttu-id="ee0f1-134">Нет</span><span class="sxs-lookup"><span data-stu-id="ee0f1-134">no</span></span>       | <span data-ttu-id="ee0f1-135">Строка, сравниваемая с идентификаторами пакетов</span><span class="sxs-lookup"><span data-stu-id="ee0f1-135">The string to compare against package IDs</span></span>
<span data-ttu-id="ee0f1-136">skip</span><span class="sxs-lookup"><span data-stu-id="ee0f1-136">skip</span></span>        | <span data-ttu-id="ee0f1-137">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="ee0f1-137">URL</span></span>    | <span data-ttu-id="ee0f1-138">целочисленный</span><span class="sxs-lookup"><span data-stu-id="ee0f1-138">integer</span></span> | <span data-ttu-id="ee0f1-139">Нет</span><span class="sxs-lookup"><span data-stu-id="ee0f1-139">no</span></span>       | <span data-ttu-id="ee0f1-140">Количество пропускаемых для разбиения на страницы результатов</span><span class="sxs-lookup"><span data-stu-id="ee0f1-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="ee0f1-141">Take</span><span class="sxs-lookup"><span data-stu-id="ee0f1-141">take</span></span>        | <span data-ttu-id="ee0f1-142">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="ee0f1-142">URL</span></span>    | <span data-ttu-id="ee0f1-143">целочисленный</span><span class="sxs-lookup"><span data-stu-id="ee0f1-143">integer</span></span> | <span data-ttu-id="ee0f1-144">Нет</span><span class="sxs-lookup"><span data-stu-id="ee0f1-144">no</span></span>       | <span data-ttu-id="ee0f1-145">Количество результатов, возвращаемых для разбиения на страницы</span><span class="sxs-lookup"><span data-stu-id="ee0f1-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="ee0f1-146">Предварительные выпуски</span><span class="sxs-lookup"><span data-stu-id="ee0f1-146">prerelease</span></span>  | <span data-ttu-id="ee0f1-147">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="ee0f1-147">URL</span></span>    | <span data-ttu-id="ee0f1-148">boolean</span><span class="sxs-lookup"><span data-stu-id="ee0f1-148">boolean</span></span> | <span data-ttu-id="ee0f1-149">Нет</span><span class="sxs-lookup"><span data-stu-id="ee0f1-149">no</span></span>       | `true` <span data-ttu-id="ee0f1-150">или `false` определения, следует ли включать [пакетов предварительных версий](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="ee0f1-150">or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="ee0f1-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="ee0f1-151">semVerLevel</span></span> | <span data-ttu-id="ee0f1-152">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="ee0f1-152">URL</span></span>    | <span data-ttu-id="ee0f1-153">string</span><span class="sxs-lookup"><span data-stu-id="ee0f1-153">string</span></span>  | <span data-ttu-id="ee0f1-154">Нет</span><span class="sxs-lookup"><span data-stu-id="ee0f1-154">no</span></span>       | <span data-ttu-id="ee0f1-155">Строка версии SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="ee0f1-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="ee0f1-156">Автозаполнение запроса `q` анализируется таким образом, определяется в реализации сервера.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="ee0f1-157">NuGet.org поддерживает выполнение запросов для префикса маркеров Идентификации пакета, которые являются элементами идентификатор созданного разделение исходного по camel знаков и символов.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="ee0f1-158">`skip` Параметр по умолчанию равен 0.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="ee0f1-159">`take` Параметр должен быть целым числом больше нуля.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="ee0f1-160">Реализация сервера может привести к повышению максимальное значение.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="ee0f1-161">Если `prerelease` не указан, исключаются пакеты предварительного выпуска.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="ee0f1-162">`semVerLevel` Параметра запроса используется для согласиться на [SemVer 2.0.0 пакетов](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="ee0f1-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="ee0f1-163">Если этот параметр запроса не исключается, будут возвращены только идентификаторы пакета с SemVer 1.0.0 совместимые версии (с [стандартный управления версиями NuGet](../reference/package-versioning.md) предупреждения, такие как строки версии с 4 частей целого числа).</span><span class="sxs-lookup"><span data-stu-id="ee0f1-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="ee0f1-164">Если `semVerLevel=2.0.0` не указан, будет возвращено SemVer 1.0.0 и совместимые пакеты SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="ee0f1-165">См. в разделе [поддержки SemVer 2.0.0 для nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="ee0f1-166">Ответ</span><span class="sxs-lookup"><span data-stu-id="ee0f1-166">Response</span></span>

<span data-ttu-id="ee0f1-167">Ответ является документ JSON, содержащий до `take` результаты автозаполнения.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="ee0f1-168">Корневой объект JSON имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="ee0f1-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="ee0f1-169">name</span><span class="sxs-lookup"><span data-stu-id="ee0f1-169">Name</span></span>      | <span data-ttu-id="ee0f1-170">Тип</span><span class="sxs-lookup"><span data-stu-id="ee0f1-170">Type</span></span>             | <span data-ttu-id="ee0f1-171">Обязательно</span><span class="sxs-lookup"><span data-stu-id="ee0f1-171">Required</span></span> | <span data-ttu-id="ee0f1-172">Примечания</span><span class="sxs-lookup"><span data-stu-id="ee0f1-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="ee0f1-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="ee0f1-173">totalHits</span></span> | <span data-ttu-id="ee0f1-174">целочисленный</span><span class="sxs-lookup"><span data-stu-id="ee0f1-174">integer</span></span>          | <span data-ttu-id="ee0f1-175">да</span><span class="sxs-lookup"><span data-stu-id="ee0f1-175">yes</span></span>      | <span data-ttu-id="ee0f1-176">Общее количество совпадений, без учета `skip` и</span><span class="sxs-lookup"><span data-stu-id="ee0f1-176">The total number of matches, disregarding `skip` and</span></span> `take`
<span data-ttu-id="ee0f1-177">Данные</span><span class="sxs-lookup"><span data-stu-id="ee0f1-177">data</span></span>      | <span data-ttu-id="ee0f1-178">Массив строк</span><span class="sxs-lookup"><span data-stu-id="ee0f1-178">array of strings</span></span> | <span data-ttu-id="ee0f1-179">да</span><span class="sxs-lookup"><span data-stu-id="ee0f1-179">yes</span></span>      | <span data-ttu-id="ee0f1-180">Пакет идентификаторы запрос соответствует</span><span class="sxs-lookup"><span data-stu-id="ee0f1-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="ee0f1-181">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="ee0f1-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="ee0f1-182">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="ee0f1-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="ee0f1-183">Перечисление версий пакета</span><span class="sxs-lookup"><span data-stu-id="ee0f1-183">Enumerate package versions</span></span>

<span data-ttu-id="ee0f1-184">После обнаружения идентификатор пакета с помощью предыдущего API, клиент может использовать API автозаполнения для перечисления версии пакетов для идентификатора указанный пакет.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="ee0f1-185">Версии пакета, отсутствующие в списке не появится в результатах.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="ee0f1-186">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="ee0f1-186">Request parameters</span></span>

<span data-ttu-id="ee0f1-187">name</span><span class="sxs-lookup"><span data-stu-id="ee0f1-187">Name</span></span>        | <span data-ttu-id="ee0f1-188">Увеличение</span><span class="sxs-lookup"><span data-stu-id="ee0f1-188">In</span></span>     | <span data-ttu-id="ee0f1-189">Тип</span><span class="sxs-lookup"><span data-stu-id="ee0f1-189">Type</span></span>    | <span data-ttu-id="ee0f1-190">Обязательно</span><span class="sxs-lookup"><span data-stu-id="ee0f1-190">Required</span></span> | <span data-ttu-id="ee0f1-191">Примечания</span><span class="sxs-lookup"><span data-stu-id="ee0f1-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="ee0f1-192">id</span><span class="sxs-lookup"><span data-stu-id="ee0f1-192">id</span></span>          | <span data-ttu-id="ee0f1-193">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="ee0f1-193">URL</span></span>    | <span data-ttu-id="ee0f1-194">string</span><span class="sxs-lookup"><span data-stu-id="ee0f1-194">string</span></span>  | <span data-ttu-id="ee0f1-195">да</span><span class="sxs-lookup"><span data-stu-id="ee0f1-195">yes</span></span>      | <span data-ttu-id="ee0f1-196">Идентификатор пакета для получения версии для</span><span class="sxs-lookup"><span data-stu-id="ee0f1-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="ee0f1-197">Предварительные выпуски</span><span class="sxs-lookup"><span data-stu-id="ee0f1-197">prerelease</span></span>  | <span data-ttu-id="ee0f1-198">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="ee0f1-198">URL</span></span>    | <span data-ttu-id="ee0f1-199">boolean</span><span class="sxs-lookup"><span data-stu-id="ee0f1-199">boolean</span></span> | <span data-ttu-id="ee0f1-200">Нет</span><span class="sxs-lookup"><span data-stu-id="ee0f1-200">no</span></span>       | `true` <span data-ttu-id="ee0f1-201">или `false` определения, следует ли включать [пакетов предварительных версий](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="ee0f1-201">or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="ee0f1-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="ee0f1-202">semVerLevel</span></span> | <span data-ttu-id="ee0f1-203">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="ee0f1-203">URL</span></span>    | <span data-ttu-id="ee0f1-204">string</span><span class="sxs-lookup"><span data-stu-id="ee0f1-204">string</span></span>  | <span data-ttu-id="ee0f1-205">Нет</span><span class="sxs-lookup"><span data-stu-id="ee0f1-205">no</span></span>       | <span data-ttu-id="ee0f1-206">Строка версии SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="ee0f1-207">Если `prerelease` не указан, исключаются пакеты предварительного выпуска.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="ee0f1-208">`semVerLevel` Параметра запроса используется для согласиться на пакеты SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="ee0f1-209">Если этот параметр запроса не исключается, будет возвращаться только версии SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="ee0f1-210">Если `semVerLevel=2.0.0` не указан, будет возвращено SemVer 1.0.0 и версии SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="ee0f1-211">См. в разделе [поддержки SemVer 2.0.0 для nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="ee0f1-212">Ответ</span><span class="sxs-lookup"><span data-stu-id="ee0f1-212">Response</span></span>

<span data-ttu-id="ee0f1-213">Ответом является документ JSON, содержащий все версии пакетов идентификатора указанный пакет, фильтрация по заданным параметрам запроса.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="ee0f1-214">Корневой объект JSON имеет следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="ee0f1-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="ee0f1-215">name</span><span class="sxs-lookup"><span data-stu-id="ee0f1-215">Name</span></span>      | <span data-ttu-id="ee0f1-216">Тип</span><span class="sxs-lookup"><span data-stu-id="ee0f1-216">Type</span></span>             | <span data-ttu-id="ee0f1-217">Обязательно</span><span class="sxs-lookup"><span data-stu-id="ee0f1-217">Required</span></span> | <span data-ttu-id="ee0f1-218">Примечания</span><span class="sxs-lookup"><span data-stu-id="ee0f1-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="ee0f1-219">Данные</span><span class="sxs-lookup"><span data-stu-id="ee0f1-219">data</span></span>      | <span data-ttu-id="ee0f1-220">Массив строк</span><span class="sxs-lookup"><span data-stu-id="ee0f1-220">array of strings</span></span> | <span data-ttu-id="ee0f1-221">да</span><span class="sxs-lookup"><span data-stu-id="ee0f1-221">yes</span></span>      | <span data-ttu-id="ee0f1-222">Версии пакетов, совпадающих с запроса</span><span class="sxs-lookup"><span data-stu-id="ee0f1-222">The package versions matched by the request</span></span>

<span data-ttu-id="ee0f1-223">Версии пакетов в `data` массива могут содержать метаданные сборки SemVer 2.0.0 (например `1.0.0+metadata`) Если `semVerLevel=2.0.0` предоставляется в строке запроса.</span><span class="sxs-lookup"><span data-stu-id="ee0f1-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="ee0f1-224">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="ee0f1-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="ee0f1-225">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="ee0f1-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
