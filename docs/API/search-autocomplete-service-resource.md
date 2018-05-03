---
title: Функция автозаполнения, NuGet интерфейса API
description: Автозаполнение службы поиска поддерживает интерактивный обнаружения пакета идентификаторы и версии.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d5e1936c6c5406a1a376c16b2bad5351320dfb4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="autocomplete"></a><span data-ttu-id="68fc1-103">Автозавершение</span><span class="sxs-lookup"><span data-stu-id="68fc1-103">Autocomplete</span></span>

<span data-ttu-id="68fc1-104">Существует возможность создания пакета идентификатор и версия Автозаполнение опыт работы с V3 API.</span><span class="sxs-lookup"><span data-stu-id="68fc1-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="68fc1-105">Ресурс, используемый для автозаполнения запросов является `SearchAutocompleteService` найти ресурс в [служба индекс](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="68fc1-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="68fc1-106">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="68fc1-106">Versioning</span></span>

<span data-ttu-id="68fc1-107">Следующие `@type` используются значения:</span><span class="sxs-lookup"><span data-stu-id="68fc1-107">The following `@type` values are used:</span></span>

<span data-ttu-id="68fc1-108">Значение @type</span><span class="sxs-lookup"><span data-stu-id="68fc1-108">@type value</span></span>                          | <span data-ttu-id="68fc1-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="68fc1-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="68fc1-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="68fc1-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="68fc1-111">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="68fc1-111">The initial release</span></span>
<span data-ttu-id="68fc1-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="68fc1-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="68fc1-113">Псевдоним `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="68fc1-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="68fc1-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="68fc1-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="68fc1-115">Псевдоним `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="68fc1-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="68fc1-116">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="68fc1-116">Base URL</span></span>

<span data-ttu-id="68fc1-117">Базовый URL-адрес для следующих API-интерфейсов — это значение `@id` свойства, связанные с одной из упомянутых выше ресурсов `@type` значения.</span><span class="sxs-lookup"><span data-stu-id="68fc1-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="68fc1-118">В следующем документе заполнитель базовый URL-адрес `{@id}` будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="68fc1-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="68fc1-119">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="68fc1-119">HTTP Methods</span></span>

<span data-ttu-id="68fc1-120">Все URL-адреса, найден в поддержку ресурсов регистрации методов HTTP `GET` и `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="68fc1-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="68fc1-121">Выполните поиск пакета идентификаторы</span><span class="sxs-lookup"><span data-stu-id="68fc1-121">Search for package IDs</span></span>

<span data-ttu-id="68fc1-122">Первый автозаполнения API поддерживает поиск строки идентификатор пакета.</span><span class="sxs-lookup"><span data-stu-id="68fc1-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="68fc1-123">Это очень полезно, если вы хотите предоставляют функцию typeahead пакета в пользовательском интерфейсе интегрирован с источника пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="68fc1-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="68fc1-124">Пакет, содержащий только версии, отсутствующие в списке не будет отображаться в результатах.</span><span class="sxs-lookup"><span data-stu-id="68fc1-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="68fc1-125">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="68fc1-125">Request parameters</span></span>

<span data-ttu-id="68fc1-126">name</span><span class="sxs-lookup"><span data-stu-id="68fc1-126">Name</span></span>        | <span data-ttu-id="68fc1-127">Увеличение</span><span class="sxs-lookup"><span data-stu-id="68fc1-127">In</span></span>     | <span data-ttu-id="68fc1-128">Тип</span><span class="sxs-lookup"><span data-stu-id="68fc1-128">Type</span></span>    | <span data-ttu-id="68fc1-129">Обязательно</span><span class="sxs-lookup"><span data-stu-id="68fc1-129">Required</span></span> | <span data-ttu-id="68fc1-130">Примечания</span><span class="sxs-lookup"><span data-stu-id="68fc1-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="68fc1-131">q</span><span class="sxs-lookup"><span data-stu-id="68fc1-131">q</span></span>           | <span data-ttu-id="68fc1-132">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="68fc1-132">URL</span></span>    | <span data-ttu-id="68fc1-133">string</span><span class="sxs-lookup"><span data-stu-id="68fc1-133">string</span></span>  | <span data-ttu-id="68fc1-134">Нет</span><span class="sxs-lookup"><span data-stu-id="68fc1-134">no</span></span>       | <span data-ttu-id="68fc1-135">Строка для сравнения с идентификаторами пакетов</span><span class="sxs-lookup"><span data-stu-id="68fc1-135">The string to compare against package IDs</span></span>
<span data-ttu-id="68fc1-136">skip</span><span class="sxs-lookup"><span data-stu-id="68fc1-136">skip</span></span>        | <span data-ttu-id="68fc1-137">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="68fc1-137">URL</span></span>    | <span data-ttu-id="68fc1-138">целочисленный</span><span class="sxs-lookup"><span data-stu-id="68fc1-138">integer</span></span> | <span data-ttu-id="68fc1-139">Нет</span><span class="sxs-lookup"><span data-stu-id="68fc1-139">no</span></span>       | <span data-ttu-id="68fc1-140">Количество пропускаемых для разбиения на страницы результатов</span><span class="sxs-lookup"><span data-stu-id="68fc1-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="68fc1-141">Take</span><span class="sxs-lookup"><span data-stu-id="68fc1-141">take</span></span>        | <span data-ttu-id="68fc1-142">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="68fc1-142">URL</span></span>    | <span data-ttu-id="68fc1-143">целочисленный</span><span class="sxs-lookup"><span data-stu-id="68fc1-143">integer</span></span> | <span data-ttu-id="68fc1-144">Нет</span><span class="sxs-lookup"><span data-stu-id="68fc1-144">no</span></span>       | <span data-ttu-id="68fc1-145">Число результатов, возвращаемых для разбиения на страницы</span><span class="sxs-lookup"><span data-stu-id="68fc1-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="68fc1-146">Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="68fc1-146">prerelease</span></span>  | <span data-ttu-id="68fc1-147">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="68fc1-147">URL</span></span>    | <span data-ttu-id="68fc1-148">boolean</span><span class="sxs-lookup"><span data-stu-id="68fc1-148">boolean</span></span> | <span data-ttu-id="68fc1-149">Нет</span><span class="sxs-lookup"><span data-stu-id="68fc1-149">no</span></span>       | <span data-ttu-id="68fc1-150">`true` или `false` определения, следует ли включать [пакеты предварительного выпуска](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="68fc1-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="68fc1-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="68fc1-151">semVerLevel</span></span> | <span data-ttu-id="68fc1-152">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="68fc1-152">URL</span></span>    | <span data-ttu-id="68fc1-153">string</span><span class="sxs-lookup"><span data-stu-id="68fc1-153">string</span></span>  | <span data-ttu-id="68fc1-154">Нет</span><span class="sxs-lookup"><span data-stu-id="68fc1-154">no</span></span>       | <span data-ttu-id="68fc1-155">Строка версии 1.0.0 SemVer</span><span class="sxs-lookup"><span data-stu-id="68fc1-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="68fc1-156">Запрос автозаполнения `q` анализируется таким способом, который определен с помощью реализации сервера.</span><span class="sxs-lookup"><span data-stu-id="68fc1-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="68fc1-157">NuGet.org поддерживает выполнение запросов для префикса маркеров идентификатор пакета, которые — это идентификатор, созданный spliting исходный счет camel регистр и символы.</span><span class="sxs-lookup"><span data-stu-id="68fc1-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="68fc1-158">`skip` Параметра по умолчанию равно 0.</span><span class="sxs-lookup"><span data-stu-id="68fc1-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="68fc1-159">`take` Параметра должно быть целое число больше нуля.</span><span class="sxs-lookup"><span data-stu-id="68fc1-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="68fc1-160">Реализация сервера может наложить максимальное значение.</span><span class="sxs-lookup"><span data-stu-id="68fc1-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="68fc1-161">Если `prerelease` не указан, исключаются пакеты предварительного выпуска.</span><span class="sxs-lookup"><span data-stu-id="68fc1-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="68fc1-162">`semVerLevel` Параметра запроса используется для согласиться на [SemVer 2.0.0 пакетов](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="68fc1-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="68fc1-163">Если этот параметр запроса не исключается, будут возвращены только идентификаторы пакета с SemVer 1.0.0 совместимые версии (с [стандартные управление версиями NuGet](../reference/package-versioning.md) предупреждения, такие как строки версии 4 частей целое число).</span><span class="sxs-lookup"><span data-stu-id="68fc1-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="68fc1-164">Если `semVerLevel=2.0.0` указан, будут возвращены SemVer 1.0.0 и совместимые пакеты SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="68fc1-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="68fc1-165">В разделе [SemVer 2.0.0 поддержка nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="68fc1-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="68fc1-166">Ответ</span><span class="sxs-lookup"><span data-stu-id="68fc1-166">Response</span></span>

<span data-ttu-id="68fc1-167">Ответ представляет документ JSON, содержащий до `take` результаты автозаполнения.</span><span class="sxs-lookup"><span data-stu-id="68fc1-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="68fc1-168">Корневой объект JSON имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="68fc1-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="68fc1-169">name</span><span class="sxs-lookup"><span data-stu-id="68fc1-169">Name</span></span>      | <span data-ttu-id="68fc1-170">Тип</span><span class="sxs-lookup"><span data-stu-id="68fc1-170">Type</span></span>             | <span data-ttu-id="68fc1-171">Обязательно</span><span class="sxs-lookup"><span data-stu-id="68fc1-171">Required</span></span> | <span data-ttu-id="68fc1-172">Примечания</span><span class="sxs-lookup"><span data-stu-id="68fc1-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="68fc1-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="68fc1-173">totalHits</span></span> | <span data-ttu-id="68fc1-174">целочисленный</span><span class="sxs-lookup"><span data-stu-id="68fc1-174">integer</span></span>          | <span data-ttu-id="68fc1-175">да</span><span class="sxs-lookup"><span data-stu-id="68fc1-175">yes</span></span>      | <span data-ttu-id="68fc1-176">Общее количество совпадений, без учета `skip` и `take`</span><span class="sxs-lookup"><span data-stu-id="68fc1-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="68fc1-177">Данные</span><span class="sxs-lookup"><span data-stu-id="68fc1-177">data</span></span>      | <span data-ttu-id="68fc1-178">Массив строк</span><span class="sxs-lookup"><span data-stu-id="68fc1-178">array of strings</span></span> | <span data-ttu-id="68fc1-179">да</span><span class="sxs-lookup"><span data-stu-id="68fc1-179">yes</span></span>      | <span data-ttu-id="68fc1-180">Запрос соответствует ИД пакета</span><span class="sxs-lookup"><span data-stu-id="68fc1-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="68fc1-181">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="68fc1-181">Sample request</span></span>

<span data-ttu-id="68fc1-182">ПОЛУЧИТЬ https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="68fc1-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="68fc1-183">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="68fc1-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="68fc1-184">Перечисление версий пакета</span><span class="sxs-lookup"><span data-stu-id="68fc1-184">Enumerate package versions</span></span>

<span data-ttu-id="68fc1-185">После обнаружения идентификатор пакета с помощью предыдущего API клиента можно использовать автозаполнение API для перечисления версии пакета для идентификатора указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="68fc1-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="68fc1-186">Версия пакета, отсутствующие в списке не будет отображаться в результатах.</span><span class="sxs-lookup"><span data-stu-id="68fc1-186">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="68fc1-187">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="68fc1-187">Request parameters</span></span>

<span data-ttu-id="68fc1-188">name</span><span class="sxs-lookup"><span data-stu-id="68fc1-188">Name</span></span>        | <span data-ttu-id="68fc1-189">Увеличение</span><span class="sxs-lookup"><span data-stu-id="68fc1-189">In</span></span>     | <span data-ttu-id="68fc1-190">Тип</span><span class="sxs-lookup"><span data-stu-id="68fc1-190">Type</span></span>    | <span data-ttu-id="68fc1-191">Обязательно</span><span class="sxs-lookup"><span data-stu-id="68fc1-191">Required</span></span> | <span data-ttu-id="68fc1-192">Примечания</span><span class="sxs-lookup"><span data-stu-id="68fc1-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="68fc1-193">id</span><span class="sxs-lookup"><span data-stu-id="68fc1-193">id</span></span>          | <span data-ttu-id="68fc1-194">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="68fc1-194">URL</span></span>    | <span data-ttu-id="68fc1-195">string</span><span class="sxs-lookup"><span data-stu-id="68fc1-195">string</span></span>  | <span data-ttu-id="68fc1-196">да</span><span class="sxs-lookup"><span data-stu-id="68fc1-196">yes</span></span>      | <span data-ttu-id="68fc1-197">Идентификатор пакета для версии для выборки</span><span class="sxs-lookup"><span data-stu-id="68fc1-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="68fc1-198">Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="68fc1-198">prerelease</span></span>  | <span data-ttu-id="68fc1-199">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="68fc1-199">URL</span></span>    | <span data-ttu-id="68fc1-200">boolean</span><span class="sxs-lookup"><span data-stu-id="68fc1-200">boolean</span></span> | <span data-ttu-id="68fc1-201">Нет</span><span class="sxs-lookup"><span data-stu-id="68fc1-201">no</span></span>       | <span data-ttu-id="68fc1-202">`true` или `false` определения, следует ли включать [пакеты предварительного выпуска](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="68fc1-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="68fc1-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="68fc1-203">semVerLevel</span></span> | <span data-ttu-id="68fc1-204">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="68fc1-204">URL</span></span>    | <span data-ttu-id="68fc1-205">string</span><span class="sxs-lookup"><span data-stu-id="68fc1-205">string</span></span>  | <span data-ttu-id="68fc1-206">Нет</span><span class="sxs-lookup"><span data-stu-id="68fc1-206">no</span></span>       | <span data-ttu-id="68fc1-207">Строка версии SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="68fc1-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="68fc1-208">Если `prerelease` не указан, исключаются пакеты предварительного выпуска.</span><span class="sxs-lookup"><span data-stu-id="68fc1-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="68fc1-209">`semVerLevel` Параметра запроса используется для согласиться на пакеты SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="68fc1-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="68fc1-210">Если этот параметр запроса не исключается, будут возвращены только версии SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="68fc1-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="68fc1-211">Если `semVerLevel=2.0.0` указан, будут возвращены SemVer 1.0.0 и версии SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="68fc1-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="68fc1-212">В разделе [SemVer 2.0.0 поддержка nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="68fc1-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="68fc1-213">Ответ</span><span class="sxs-lookup"><span data-stu-id="68fc1-213">Response</span></span>

<span data-ttu-id="68fc1-214">Ответ — документ JSON, содержащий все версии пакета идентификатор предоставленного пакета, фильтрация на основе параметров данного запроса.</span><span class="sxs-lookup"><span data-stu-id="68fc1-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="68fc1-215">Корневой объект JSON имеет следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="68fc1-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="68fc1-216">name</span><span class="sxs-lookup"><span data-stu-id="68fc1-216">Name</span></span>      | <span data-ttu-id="68fc1-217">Тип</span><span class="sxs-lookup"><span data-stu-id="68fc1-217">Type</span></span>             | <span data-ttu-id="68fc1-218">Обязательно</span><span class="sxs-lookup"><span data-stu-id="68fc1-218">Required</span></span> | <span data-ttu-id="68fc1-219">Примечания</span><span class="sxs-lookup"><span data-stu-id="68fc1-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="68fc1-220">Данные</span><span class="sxs-lookup"><span data-stu-id="68fc1-220">data</span></span>      | <span data-ttu-id="68fc1-221">Массив строк</span><span class="sxs-lookup"><span data-stu-id="68fc1-221">array of strings</span></span> | <span data-ttu-id="68fc1-222">да</span><span class="sxs-lookup"><span data-stu-id="68fc1-222">yes</span></span>      | <span data-ttu-id="68fc1-223">Запрос на соответствует версии пакета</span><span class="sxs-lookup"><span data-stu-id="68fc1-223">The package versions matched by the request</span></span>

<span data-ttu-id="68fc1-224">Версии пакетов в `data` массив может содержать метаданные сборки SemVer 2.0.0 (например `1.0.0+metadata`) Если `semVerLevel=2.0.0` был представлен в строке запроса.</span><span class="sxs-lookup"><span data-stu-id="68fc1-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="68fc1-225">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="68fc1-225">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="68fc1-226">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="68fc1-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
