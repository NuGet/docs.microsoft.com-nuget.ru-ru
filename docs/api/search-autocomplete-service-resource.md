---
title: Автозаполнение, API NuGet
description: Служба автозаполнения поиска поддерживает интерактивное обнаружение идентификаторов и версий пакетов.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488297"
---
# <a name="autocomplete"></a><span data-ttu-id="20d86-103">Автозавершение</span><span class="sxs-lookup"><span data-stu-id="20d86-103">Autocomplete</span></span>

<span data-ttu-id="20d86-104">Можно создать идентификатор пакета и Автозаполнение версий с помощью API V3.</span><span class="sxs-lookup"><span data-stu-id="20d86-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="20d86-105">Ресурс, используемый для выполнения запросов автозаполнения, — `SearchAutocompleteService` это ресурс, найденный в [индексе службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="20d86-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="20d86-106">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="20d86-106">Versioning</span></span>

<span data-ttu-id="20d86-107">Используются следующие `@type` значения:</span><span class="sxs-lookup"><span data-stu-id="20d86-107">The following `@type` values are used:</span></span>

<span data-ttu-id="20d86-108">Значение@type</span><span class="sxs-lookup"><span data-stu-id="20d86-108">@type value</span></span>                          | <span data-ttu-id="20d86-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="20d86-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="20d86-110">сеарчаутокомплетесервице</span><span class="sxs-lookup"><span data-stu-id="20d86-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="20d86-111">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="20d86-111">The initial release</span></span>
<span data-ttu-id="20d86-112">Сеарчаутокомплетесервице/3.0.0 — бета-версия</span><span class="sxs-lookup"><span data-stu-id="20d86-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="20d86-113">Псевдоним`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="20d86-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="20d86-114">Сеарчаутокомплетесервице/3.0.0-RC</span><span class="sxs-lookup"><span data-stu-id="20d86-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="20d86-115">Псевдоним`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="20d86-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="20d86-116">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="20d86-116">Base URL</span></span>

<span data-ttu-id="20d86-117">Базовый URL-адрес для следующих API-интерфейсов — это `@id` значение свойства, связанного с одним из вышеупомянутых `@type` значений ресурсов.</span><span class="sxs-lookup"><span data-stu-id="20d86-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="20d86-118">В следующем документе будет использоваться базовый URL-адрес `{@id}` заполнителя.</span><span class="sxs-lookup"><span data-stu-id="20d86-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="20d86-119">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="20d86-119">HTTP Methods</span></span>

<span data-ttu-id="20d86-120">Все URL-адреса, найденные в ресурсе регистрации `GET` , `HEAD`поддерживают методы HTTP и.</span><span class="sxs-lookup"><span data-stu-id="20d86-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="20d86-121">Поиск идентификаторов пакетов</span><span class="sxs-lookup"><span data-stu-id="20d86-121">Search for package IDs</span></span>

<span data-ttu-id="20d86-122">Первый API автозаполнения поддерживает поиск части строки идентификатора пакета.</span><span class="sxs-lookup"><span data-stu-id="20d86-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="20d86-123">Это очень удобно, если вы хотите предоставить typeahead пакета в пользовательском интерфейсе, интегрированном с источником пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="20d86-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="20d86-124">Пакет, содержащий только непоставленные версии, не будет отображаться в результатах.</span><span class="sxs-lookup"><span data-stu-id="20d86-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="20d86-125">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="20d86-125">Request parameters</span></span>

<span data-ttu-id="20d86-126">name</span><span class="sxs-lookup"><span data-stu-id="20d86-126">Name</span></span>        | <span data-ttu-id="20d86-127">In</span><span class="sxs-lookup"><span data-stu-id="20d86-127">In</span></span>     | <span data-ttu-id="20d86-128">Тип</span><span class="sxs-lookup"><span data-stu-id="20d86-128">Type</span></span>    | <span data-ttu-id="20d86-129">Обязательно</span><span class="sxs-lookup"><span data-stu-id="20d86-129">Required</span></span> | <span data-ttu-id="20d86-130">Примечания</span><span class="sxs-lookup"><span data-stu-id="20d86-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="20d86-131">q</span><span class="sxs-lookup"><span data-stu-id="20d86-131">q</span></span>           | <span data-ttu-id="20d86-132">URL</span><span class="sxs-lookup"><span data-stu-id="20d86-132">URL</span></span>    | <span data-ttu-id="20d86-133">string</span><span class="sxs-lookup"><span data-stu-id="20d86-133">string</span></span>  | <span data-ttu-id="20d86-134">Нет</span><span class="sxs-lookup"><span data-stu-id="20d86-134">no</span></span>       | <span data-ttu-id="20d86-135">Строка для сравнения с идентификаторами пакета</span><span class="sxs-lookup"><span data-stu-id="20d86-135">The string to compare against package IDs</span></span>
<span data-ttu-id="20d86-136">skip</span><span class="sxs-lookup"><span data-stu-id="20d86-136">skip</span></span>        | <span data-ttu-id="20d86-137">URL</span><span class="sxs-lookup"><span data-stu-id="20d86-137">URL</span></span>    | <span data-ttu-id="20d86-138">целочисленный</span><span class="sxs-lookup"><span data-stu-id="20d86-138">integer</span></span> | <span data-ttu-id="20d86-139">Нет</span><span class="sxs-lookup"><span data-stu-id="20d86-139">no</span></span>       | <span data-ttu-id="20d86-140">Число пропускаемых результатов для разбивки на страницы</span><span class="sxs-lookup"><span data-stu-id="20d86-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="20d86-141">нимают</span><span class="sxs-lookup"><span data-stu-id="20d86-141">take</span></span>        | <span data-ttu-id="20d86-142">URL</span><span class="sxs-lookup"><span data-stu-id="20d86-142">URL</span></span>    | <span data-ttu-id="20d86-143">целочисленный</span><span class="sxs-lookup"><span data-stu-id="20d86-143">integer</span></span> | <span data-ttu-id="20d86-144">Нет</span><span class="sxs-lookup"><span data-stu-id="20d86-144">no</span></span>       | <span data-ttu-id="20d86-145">Число возвращаемых результатов для разбивки на страницы</span><span class="sxs-lookup"><span data-stu-id="20d86-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="20d86-146">предварительной</span><span class="sxs-lookup"><span data-stu-id="20d86-146">prerelease</span></span>  | <span data-ttu-id="20d86-147">URL</span><span class="sxs-lookup"><span data-stu-id="20d86-147">URL</span></span>    | <span data-ttu-id="20d86-148">boolean</span><span class="sxs-lookup"><span data-stu-id="20d86-148">boolean</span></span> | <span data-ttu-id="20d86-149">Нет</span><span class="sxs-lookup"><span data-stu-id="20d86-149">no</span></span>       | <span data-ttu-id="20d86-150">`true`или `false` определить, следует ли включать [пакеты предварительной версии](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="20d86-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="20d86-151">семверлевел</span><span class="sxs-lookup"><span data-stu-id="20d86-151">semVerLevel</span></span> | <span data-ttu-id="20d86-152">URL</span><span class="sxs-lookup"><span data-stu-id="20d86-152">URL</span></span>    | <span data-ttu-id="20d86-153">string</span><span class="sxs-lookup"><span data-stu-id="20d86-153">string</span></span>  | <span data-ttu-id="20d86-154">Нет</span><span class="sxs-lookup"><span data-stu-id="20d86-154">no</span></span>       | <span data-ttu-id="20d86-155">Строка версии SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="20d86-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="20d86-156">Запрос `q` автозаполнения анализируется способом, который определяется реализацией сервера.</span><span class="sxs-lookup"><span data-stu-id="20d86-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="20d86-157">nuget.org поддерживает запросы к префиксам токенов ИДЕНТИФИКАТОРов пакетов, которые представляют собой фрагменты идентификатора, созданного путем разделения оригинала на символы Camel и символов.</span><span class="sxs-lookup"><span data-stu-id="20d86-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="20d86-158">Значение `skip` параметра по умолчанию равно 0.</span><span class="sxs-lookup"><span data-stu-id="20d86-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="20d86-159">`take` Параметр должен быть целым числом больше нуля.</span><span class="sxs-lookup"><span data-stu-id="20d86-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="20d86-160">Реализация сервера может накладывать максимальное значение.</span><span class="sxs-lookup"><span data-stu-id="20d86-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="20d86-161">Если `prerelease` не указан, пакеты предварительной версии исключаются.</span><span class="sxs-lookup"><span data-stu-id="20d86-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="20d86-162">Параметр запроса используется для явного согласия на [пакеты 2.0.0 SemVer.](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages) `semVerLevel`</span><span class="sxs-lookup"><span data-stu-id="20d86-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="20d86-163">Если этот параметр запроса исключен, будут возвращены только идентификаторы пакетов с совместимыми версиями SemVer 1.0.0 (со стандартными предупреждениями [управления версиями NuGet](../concepts/package-versioning.md) , такими как строки версии с 4 целыми частями).</span><span class="sxs-lookup"><span data-stu-id="20d86-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="20d86-164">Если `semVerLevel=2.0.0` указан, будут возвращены совместимые пакеты SemVer 1.0.0 и SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="20d86-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="20d86-165">Дополнительные сведения см. в разделе [Поддержка SemVer 2.0.0 для NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .</span><span class="sxs-lookup"><span data-stu-id="20d86-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="20d86-166">Отклик</span><span class="sxs-lookup"><span data-stu-id="20d86-166">Response</span></span>

<span data-ttu-id="20d86-167">Ответ — это документ JSON, содержащий `take` результаты автозаполнения.</span><span class="sxs-lookup"><span data-stu-id="20d86-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="20d86-168">Корневой объект JSON имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="20d86-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="20d86-169">name</span><span class="sxs-lookup"><span data-stu-id="20d86-169">Name</span></span>      | <span data-ttu-id="20d86-170">Тип</span><span class="sxs-lookup"><span data-stu-id="20d86-170">Type</span></span>             | <span data-ttu-id="20d86-171">Обязательно</span><span class="sxs-lookup"><span data-stu-id="20d86-171">Required</span></span> | <span data-ttu-id="20d86-172">Примечания</span><span class="sxs-lookup"><span data-stu-id="20d86-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="20d86-173">тоталхитс</span><span class="sxs-lookup"><span data-stu-id="20d86-173">totalHits</span></span> | <span data-ttu-id="20d86-174">целочисленный</span><span class="sxs-lookup"><span data-stu-id="20d86-174">integer</span></span>          | <span data-ttu-id="20d86-175">да</span><span class="sxs-lookup"><span data-stu-id="20d86-175">yes</span></span>      | <span data-ttu-id="20d86-176">Общее число совпадений, неотношении `skip` и`take`</span><span class="sxs-lookup"><span data-stu-id="20d86-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="20d86-177">Данные</span><span class="sxs-lookup"><span data-stu-id="20d86-177">data</span></span>      | <span data-ttu-id="20d86-178">Массив строк</span><span class="sxs-lookup"><span data-stu-id="20d86-178">array of strings</span></span> | <span data-ttu-id="20d86-179">да</span><span class="sxs-lookup"><span data-stu-id="20d86-179">yes</span></span>      | <span data-ttu-id="20d86-180">Идентификаторы пакетов, совпадающие по запросу</span><span class="sxs-lookup"><span data-stu-id="20d86-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="20d86-181">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="20d86-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="20d86-182">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="20d86-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="20d86-183">Перечислить версии пакета</span><span class="sxs-lookup"><span data-stu-id="20d86-183">Enumerate package versions</span></span>

<span data-ttu-id="20d86-184">После того как идентификатор пакета будет обнаружен с помощью предыдущего API, клиент может использовать API автозаполнения для перечисления версий пакета для указанного идентификатора пакета.</span><span class="sxs-lookup"><span data-stu-id="20d86-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="20d86-185">Версия пакета, которая не указана в списке, не будет отображаться в результатах.</span><span class="sxs-lookup"><span data-stu-id="20d86-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="20d86-186">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="20d86-186">Request parameters</span></span>

<span data-ttu-id="20d86-187">name</span><span class="sxs-lookup"><span data-stu-id="20d86-187">Name</span></span>        | <span data-ttu-id="20d86-188">In</span><span class="sxs-lookup"><span data-stu-id="20d86-188">In</span></span>     | <span data-ttu-id="20d86-189">Тип</span><span class="sxs-lookup"><span data-stu-id="20d86-189">Type</span></span>    | <span data-ttu-id="20d86-190">Обязательно</span><span class="sxs-lookup"><span data-stu-id="20d86-190">Required</span></span> | <span data-ttu-id="20d86-191">Примечания</span><span class="sxs-lookup"><span data-stu-id="20d86-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="20d86-192">id</span><span class="sxs-lookup"><span data-stu-id="20d86-192">id</span></span>          | <span data-ttu-id="20d86-193">URL</span><span class="sxs-lookup"><span data-stu-id="20d86-193">URL</span></span>    | <span data-ttu-id="20d86-194">string</span><span class="sxs-lookup"><span data-stu-id="20d86-194">string</span></span>  | <span data-ttu-id="20d86-195">да</span><span class="sxs-lookup"><span data-stu-id="20d86-195">yes</span></span>      | <span data-ttu-id="20d86-196">Идентификатор пакета для выборки версий для</span><span class="sxs-lookup"><span data-stu-id="20d86-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="20d86-197">предварительной</span><span class="sxs-lookup"><span data-stu-id="20d86-197">prerelease</span></span>  | <span data-ttu-id="20d86-198">URL</span><span class="sxs-lookup"><span data-stu-id="20d86-198">URL</span></span>    | <span data-ttu-id="20d86-199">boolean</span><span class="sxs-lookup"><span data-stu-id="20d86-199">boolean</span></span> | <span data-ttu-id="20d86-200">Нет</span><span class="sxs-lookup"><span data-stu-id="20d86-200">no</span></span>       | <span data-ttu-id="20d86-201">`true`или `false` определить, следует ли включать [пакеты предварительной версии](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="20d86-201">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="20d86-202">семверлевел</span><span class="sxs-lookup"><span data-stu-id="20d86-202">semVerLevel</span></span> | <span data-ttu-id="20d86-203">URL</span><span class="sxs-lookup"><span data-stu-id="20d86-203">URL</span></span>    | <span data-ttu-id="20d86-204">string</span><span class="sxs-lookup"><span data-stu-id="20d86-204">string</span></span>  | <span data-ttu-id="20d86-205">Нет</span><span class="sxs-lookup"><span data-stu-id="20d86-205">no</span></span>       | <span data-ttu-id="20d86-206">Строка версии 2.0.0 SemVer</span><span class="sxs-lookup"><span data-stu-id="20d86-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="20d86-207">Если `prerelease` не указан, пакеты предварительной версии исключаются.</span><span class="sxs-lookup"><span data-stu-id="20d86-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="20d86-208">Параметр `semVerLevel` запроса используется для явного согласия на пакеты 2.0.0 SemVer.</span><span class="sxs-lookup"><span data-stu-id="20d86-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="20d86-209">Если этот параметр запроса исключен, будут возвращены только версии SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="20d86-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="20d86-210">Если `semVerLevel=2.0.0` указан, будут возвращены версии SemVer 1.0.0 и SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="20d86-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="20d86-211">Дополнительные сведения см. в разделе [Поддержка SemVer 2.0.0 для NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .</span><span class="sxs-lookup"><span data-stu-id="20d86-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="20d86-212">Отклик</span><span class="sxs-lookup"><span data-stu-id="20d86-212">Response</span></span>

<span data-ttu-id="20d86-213">Ответ — это документ JSON, содержащий все версии пакета указанного идентификатора пакета, который фильтрует по заданным параметрам запроса.</span><span class="sxs-lookup"><span data-stu-id="20d86-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="20d86-214">Корневой объект JSON имеет следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="20d86-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="20d86-215">name</span><span class="sxs-lookup"><span data-stu-id="20d86-215">Name</span></span>      | <span data-ttu-id="20d86-216">Тип</span><span class="sxs-lookup"><span data-stu-id="20d86-216">Type</span></span>             | <span data-ttu-id="20d86-217">Обязательно</span><span class="sxs-lookup"><span data-stu-id="20d86-217">Required</span></span> | <span data-ttu-id="20d86-218">Примечания</span><span class="sxs-lookup"><span data-stu-id="20d86-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="20d86-219">Данные</span><span class="sxs-lookup"><span data-stu-id="20d86-219">data</span></span>      | <span data-ttu-id="20d86-220">Массив строк</span><span class="sxs-lookup"><span data-stu-id="20d86-220">array of strings</span></span> | <span data-ttu-id="20d86-221">да</span><span class="sxs-lookup"><span data-stu-id="20d86-221">yes</span></span>      | <span data-ttu-id="20d86-222">Версии пакета, соответствующие запросу</span><span class="sxs-lookup"><span data-stu-id="20d86-222">The package versions matched by the request</span></span>

<span data-ttu-id="20d86-223">Версии пакета в `data` массиве могут содержать метаданные сборки SemVer 2.0.0 ( `1.0.0+metadata`например,), `semVerLevel=2.0.0` если в строке запроса содержится.</span><span class="sxs-lookup"><span data-stu-id="20d86-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="20d86-224">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="20d86-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="20d86-225">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="20d86-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
