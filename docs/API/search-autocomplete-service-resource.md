---
title: "Автозаполнение, NuGet API | Документы Microsoft"
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
description: "Автозаполнение службы поиска поддерживает интерактивный обнаружения пакета идентификаторы и версии."
keywords: "API автозаполнения NuGet, идентификатор пакета NuGet поиска, идентификатор пакета подстроки"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7c984ca61799293d7832851b80cf3fefc4734288
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2018
---
# <a name="autocomplete"></a><span data-ttu-id="9d24e-104">Автозавершение</span><span class="sxs-lookup"><span data-stu-id="9d24e-104">Autocomplete</span></span>

<span data-ttu-id="9d24e-105">Существует возможность создания пакета идентификатор и версия Автозаполнение опыт работы с V3 API.</span><span class="sxs-lookup"><span data-stu-id="9d24e-105">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="9d24e-106">Ресурс, используемый для автозаполнения запросов является `SearchAutocompleteService` найти ресурс в [служба индекс](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="9d24e-106">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="9d24e-107">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="9d24e-107">Versioning</span></span>

<span data-ttu-id="9d24e-108">Следующие `@type` используются значения:</span><span class="sxs-lookup"><span data-stu-id="9d24e-108">The following `@type` values are used:</span></span>

<span data-ttu-id="9d24e-109">Значение @type</span><span class="sxs-lookup"><span data-stu-id="9d24e-109">@type value</span></span>                          | <span data-ttu-id="9d24e-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="9d24e-110">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="9d24e-111">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="9d24e-111">SearchAutocompleteService</span></span>            | <span data-ttu-id="9d24e-112">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="9d24e-112">The initial release</span></span>
<span data-ttu-id="9d24e-113">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="9d24e-113">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="9d24e-114">Псевдоним`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="9d24e-114">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="9d24e-115">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="9d24e-115">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="9d24e-116">Псевдоним`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="9d24e-116">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="9d24e-117">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="9d24e-117">Base URL</span></span>

<span data-ttu-id="9d24e-118">Базовый URL-адрес для следующих API-интерфейсов — это значение `@id` свойства, связанные с одной из упомянутых выше ресурсов `@type` значения.</span><span class="sxs-lookup"><span data-stu-id="9d24e-118">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="9d24e-119">В следующем документе заполнитель базовый URL-адрес `{@id}` будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="9d24e-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="9d24e-120">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="9d24e-120">HTTP Methods</span></span>

<span data-ttu-id="9d24e-121">Все URL-адреса, найден в поддержку ресурсов регистрации методов HTTP `GET` и `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="9d24e-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="9d24e-122">Выполните поиск пакета идентификаторы</span><span class="sxs-lookup"><span data-stu-id="9d24e-122">Search for package IDs</span></span>

<span data-ttu-id="9d24e-123">Первый автозаполнения API поддерживает поиск строки идентификатор пакета.</span><span class="sxs-lookup"><span data-stu-id="9d24e-123">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="9d24e-124">Это очень полезно, если вы хотите предоставляют функцию typeahead пакета в пользовательском интерфейсе интегрирован с источника пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="9d24e-124">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="9d24e-125">Пакет, содержащий только версии, отсутствующие в списке не будет отображаться в результатах.</span><span class="sxs-lookup"><span data-stu-id="9d24e-125">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="9d24e-126">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="9d24e-126">Request parameters</span></span>

<span data-ttu-id="9d24e-127">name</span><span class="sxs-lookup"><span data-stu-id="9d24e-127">Name</span></span>        | <span data-ttu-id="9d24e-128">Увеличение</span><span class="sxs-lookup"><span data-stu-id="9d24e-128">In</span></span>     | <span data-ttu-id="9d24e-129">Тип</span><span class="sxs-lookup"><span data-stu-id="9d24e-129">Type</span></span>    | <span data-ttu-id="9d24e-130">Обязательно</span><span class="sxs-lookup"><span data-stu-id="9d24e-130">Required</span></span> | <span data-ttu-id="9d24e-131">Примечания</span><span class="sxs-lookup"><span data-stu-id="9d24e-131">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="9d24e-132">q</span><span class="sxs-lookup"><span data-stu-id="9d24e-132">q</span></span>           | <span data-ttu-id="9d24e-133">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="9d24e-133">URL</span></span>    | <span data-ttu-id="9d24e-134">string</span><span class="sxs-lookup"><span data-stu-id="9d24e-134">string</span></span>  | <span data-ttu-id="9d24e-135">Нет</span><span class="sxs-lookup"><span data-stu-id="9d24e-135">no</span></span>       | <span data-ttu-id="9d24e-136">Строка для сравнения с идентификаторами пакетов</span><span class="sxs-lookup"><span data-stu-id="9d24e-136">The string to compare against package IDs</span></span>
<span data-ttu-id="9d24e-137">skip</span><span class="sxs-lookup"><span data-stu-id="9d24e-137">skip</span></span>        | <span data-ttu-id="9d24e-138">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="9d24e-138">URL</span></span>    | <span data-ttu-id="9d24e-139">целочисленный</span><span class="sxs-lookup"><span data-stu-id="9d24e-139">integer</span></span> | <span data-ttu-id="9d24e-140">Нет</span><span class="sxs-lookup"><span data-stu-id="9d24e-140">no</span></span>       | <span data-ttu-id="9d24e-141">Количество пропускаемых для разбиения на страницы результатов</span><span class="sxs-lookup"><span data-stu-id="9d24e-141">The number of results to skip, for pagination</span></span>
<span data-ttu-id="9d24e-142">Take</span><span class="sxs-lookup"><span data-stu-id="9d24e-142">take</span></span>        | <span data-ttu-id="9d24e-143">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="9d24e-143">URL</span></span>    | <span data-ttu-id="9d24e-144">целочисленный</span><span class="sxs-lookup"><span data-stu-id="9d24e-144">integer</span></span> | <span data-ttu-id="9d24e-145">Нет</span><span class="sxs-lookup"><span data-stu-id="9d24e-145">no</span></span>       | <span data-ttu-id="9d24e-146">Число результатов, возвращаемых для разбиения на страницы</span><span class="sxs-lookup"><span data-stu-id="9d24e-146">The number of results to return, for pagination</span></span>
<span data-ttu-id="9d24e-147">Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="9d24e-147">prerelease</span></span>  | <span data-ttu-id="9d24e-148">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="9d24e-148">URL</span></span>    | <span data-ttu-id="9d24e-149">boolean</span><span class="sxs-lookup"><span data-stu-id="9d24e-149">boolean</span></span> | <span data-ttu-id="9d24e-150">Нет</span><span class="sxs-lookup"><span data-stu-id="9d24e-150">no</span></span>       | <span data-ttu-id="9d24e-151">`true`или `false` определения, следует ли включать [пакеты предварительного выпуска](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="9d24e-151">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="9d24e-152">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="9d24e-152">semVerLevel</span></span> | <span data-ttu-id="9d24e-153">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="9d24e-153">URL</span></span>    | <span data-ttu-id="9d24e-154">string</span><span class="sxs-lookup"><span data-stu-id="9d24e-154">string</span></span>  | <span data-ttu-id="9d24e-155">Нет</span><span class="sxs-lookup"><span data-stu-id="9d24e-155">no</span></span>       | <span data-ttu-id="9d24e-156">Строка версии 1.0.0 SemVer</span><span class="sxs-lookup"><span data-stu-id="9d24e-156">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="9d24e-157">Запрос автозаполнения `q` анализируется таким способом, который определен с помощью реализации сервера.</span><span class="sxs-lookup"><span data-stu-id="9d24e-157">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="9d24e-158">NuGet.org поддерживает выполнение запросов для префикса маркеров идентификатор пакета, которые — это идентификатор, созданный spliting исходный счет camel регистр и символы.</span><span class="sxs-lookup"><span data-stu-id="9d24e-158">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="9d24e-159">`skip` Параметра по умолчанию равно 0.</span><span class="sxs-lookup"><span data-stu-id="9d24e-159">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="9d24e-160">`take` Параметра должно быть целое число больше нуля.</span><span class="sxs-lookup"><span data-stu-id="9d24e-160">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="9d24e-161">Реализация сервера может наложить максимальное значение.</span><span class="sxs-lookup"><span data-stu-id="9d24e-161">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="9d24e-162">Если `prerelease` не указан, исключаются пакеты предварительного выпуска.</span><span class="sxs-lookup"><span data-stu-id="9d24e-162">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="9d24e-163">`semVerLevel` Параметра запроса используется для согласиться на [SemVer 2.0.0 пакетов](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="9d24e-163">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="9d24e-164">Если этот параметр запроса не исключается, будут возвращены только идентификаторы пакета с SemVer 1.0.0 совместимые версии (с [стандартные управление версиями NuGet](../reference/package-versioning.md) предупреждения, такие как строки версии 4 частей целое число).</span><span class="sxs-lookup"><span data-stu-id="9d24e-164">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="9d24e-165">Если `semVerLevel=2.0.0` указан, будут возвращены SemVer 1.0.0 и совместимые пакеты SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="9d24e-165">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="9d24e-166">В разделе [SemVer 2.0.0 поддержка nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="9d24e-166">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="9d24e-167">Ответ</span><span class="sxs-lookup"><span data-stu-id="9d24e-167">Response</span></span>

<span data-ttu-id="9d24e-168">Ответ представляет документ JSON, содержащий до `take` результаты автозаполнения.</span><span class="sxs-lookup"><span data-stu-id="9d24e-168">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="9d24e-169">Корневой объект JSON имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="9d24e-169">The root JSON object has the following properties:</span></span>

<span data-ttu-id="9d24e-170">name</span><span class="sxs-lookup"><span data-stu-id="9d24e-170">Name</span></span>      | <span data-ttu-id="9d24e-171">Тип</span><span class="sxs-lookup"><span data-stu-id="9d24e-171">Type</span></span>             | <span data-ttu-id="9d24e-172">Обязательно</span><span class="sxs-lookup"><span data-stu-id="9d24e-172">Required</span></span> | <span data-ttu-id="9d24e-173">Примечания</span><span class="sxs-lookup"><span data-stu-id="9d24e-173">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="9d24e-174">totalHits</span><span class="sxs-lookup"><span data-stu-id="9d24e-174">totalHits</span></span> | <span data-ttu-id="9d24e-175">целочисленный</span><span class="sxs-lookup"><span data-stu-id="9d24e-175">integer</span></span>          | <span data-ttu-id="9d24e-176">да</span><span class="sxs-lookup"><span data-stu-id="9d24e-176">yes</span></span>      | <span data-ttu-id="9d24e-177">Общее количество совпадений, без учета `skip` и`take`</span><span class="sxs-lookup"><span data-stu-id="9d24e-177">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="9d24e-178">Данные</span><span class="sxs-lookup"><span data-stu-id="9d24e-178">data</span></span>      | <span data-ttu-id="9d24e-179">Массив строк</span><span class="sxs-lookup"><span data-stu-id="9d24e-179">array of strings</span></span> | <span data-ttu-id="9d24e-180">да</span><span class="sxs-lookup"><span data-stu-id="9d24e-180">yes</span></span>      | <span data-ttu-id="9d24e-181">Запрос соответствует ИД пакета</span><span class="sxs-lookup"><span data-stu-id="9d24e-181">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="9d24e-182">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="9d24e-182">Sample request</span></span>

<span data-ttu-id="9d24e-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="9d24e-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="9d24e-184">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="9d24e-184">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="9d24e-185">Перечисление версий пакета</span><span class="sxs-lookup"><span data-stu-id="9d24e-185">Enumerate package versions</span></span>

<span data-ttu-id="9d24e-186">После обнаружения идентификатор пакета с помощью предыдущего API клиента можно использовать автозаполнение API для перечисления версии пакета для идентификатора указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="9d24e-186">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="9d24e-187">Версия пакета, отсутствующие в списке не будет отображаться в результатах.</span><span class="sxs-lookup"><span data-stu-id="9d24e-187">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="9d24e-188">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="9d24e-188">Request parameters</span></span>

<span data-ttu-id="9d24e-189">name</span><span class="sxs-lookup"><span data-stu-id="9d24e-189">Name</span></span>        | <span data-ttu-id="9d24e-190">Увеличение</span><span class="sxs-lookup"><span data-stu-id="9d24e-190">In</span></span>     | <span data-ttu-id="9d24e-191">Тип</span><span class="sxs-lookup"><span data-stu-id="9d24e-191">Type</span></span>    | <span data-ttu-id="9d24e-192">Обязательно</span><span class="sxs-lookup"><span data-stu-id="9d24e-192">Required</span></span> | <span data-ttu-id="9d24e-193">Примечания</span><span class="sxs-lookup"><span data-stu-id="9d24e-193">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="9d24e-194">id</span><span class="sxs-lookup"><span data-stu-id="9d24e-194">id</span></span>          | <span data-ttu-id="9d24e-195">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="9d24e-195">URL</span></span>    | <span data-ttu-id="9d24e-196">string</span><span class="sxs-lookup"><span data-stu-id="9d24e-196">string</span></span>  | <span data-ttu-id="9d24e-197">да</span><span class="sxs-lookup"><span data-stu-id="9d24e-197">yes</span></span>      | <span data-ttu-id="9d24e-198">Идентификатор пакета для версии для выборки</span><span class="sxs-lookup"><span data-stu-id="9d24e-198">The package ID to fetch versions for</span></span>
<span data-ttu-id="9d24e-199">Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="9d24e-199">prerelease</span></span>  | <span data-ttu-id="9d24e-200">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="9d24e-200">URL</span></span>    | <span data-ttu-id="9d24e-201">boolean</span><span class="sxs-lookup"><span data-stu-id="9d24e-201">boolean</span></span> | <span data-ttu-id="9d24e-202">Нет</span><span class="sxs-lookup"><span data-stu-id="9d24e-202">no</span></span>       | <span data-ttu-id="9d24e-203">`true`или `false` определения, следует ли включать [пакеты предварительного выпуска](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="9d24e-203">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="9d24e-204">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="9d24e-204">semVerLevel</span></span> | <span data-ttu-id="9d24e-205">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="9d24e-205">URL</span></span>    | <span data-ttu-id="9d24e-206">string</span><span class="sxs-lookup"><span data-stu-id="9d24e-206">string</span></span>  | <span data-ttu-id="9d24e-207">Нет</span><span class="sxs-lookup"><span data-stu-id="9d24e-207">no</span></span>       | <span data-ttu-id="9d24e-208">Строка версии SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="9d24e-208">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="9d24e-209">Если `prerelease` не указан, исключаются пакеты предварительного выпуска.</span><span class="sxs-lookup"><span data-stu-id="9d24e-209">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="9d24e-210">`semVerLevel` Параметра запроса используется для согласиться на пакеты SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="9d24e-210">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="9d24e-211">Если этот параметр запроса не исключается, будут возвращены только версии SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="9d24e-211">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="9d24e-212">Если `semVerLevel=2.0.0` указан, будут возвращены SemVer 1.0.0 и версии SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="9d24e-212">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="9d24e-213">В разделе [SemVer 2.0.0 поддержка nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="9d24e-213">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="9d24e-214">Ответ</span><span class="sxs-lookup"><span data-stu-id="9d24e-214">Response</span></span>

<span data-ttu-id="9d24e-215">Ответ — документ JSON, содержащий все версии пакета идентификатор предоставленного пакета, фильтрация на основе параметров данного запроса.</span><span class="sxs-lookup"><span data-stu-id="9d24e-215">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="9d24e-216">Корневой объект JSON имеет следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="9d24e-216">The root JSON object has the following property:</span></span>

<span data-ttu-id="9d24e-217">name</span><span class="sxs-lookup"><span data-stu-id="9d24e-217">Name</span></span>      | <span data-ttu-id="9d24e-218">Тип</span><span class="sxs-lookup"><span data-stu-id="9d24e-218">Type</span></span>             | <span data-ttu-id="9d24e-219">Обязательно</span><span class="sxs-lookup"><span data-stu-id="9d24e-219">Required</span></span> | <span data-ttu-id="9d24e-220">Примечания</span><span class="sxs-lookup"><span data-stu-id="9d24e-220">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="9d24e-221">Данные</span><span class="sxs-lookup"><span data-stu-id="9d24e-221">data</span></span>      | <span data-ttu-id="9d24e-222">Массив строк</span><span class="sxs-lookup"><span data-stu-id="9d24e-222">array of strings</span></span> | <span data-ttu-id="9d24e-223">да</span><span class="sxs-lookup"><span data-stu-id="9d24e-223">yes</span></span>      | <span data-ttu-id="9d24e-224">Запрос на соответствует версии пакета</span><span class="sxs-lookup"><span data-stu-id="9d24e-224">The package versions matched by the request</span></span>

<span data-ttu-id="9d24e-225">Версии пакетов в `data` массив может содержать метаданные сборки SemVer 2.0.0 (например `1.0.0+metadata`) Если `semVerLevel=2.0.0` был представлен в строке запроса.</span><span class="sxs-lookup"><span data-stu-id="9d24e-225">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="9d24e-226">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="9d24e-226">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="9d24e-227">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="9d24e-227">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
