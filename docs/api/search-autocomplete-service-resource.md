---
title: Автозаполнение, API NuGet
description: Служба автозаполнения поиска поддерживает интерактивное обнаружение идентификаторов и версий пакетов.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2893e13ff7b070844a2bdd5722da3aa1f123538d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773962"
---
# <a name="autocomplete"></a><span data-ttu-id="b5bc5-103">Автозавершение</span><span class="sxs-lookup"><span data-stu-id="b5bc5-103">Autocomplete</span></span>

<span data-ttu-id="b5bc5-104">Можно создать идентификатор пакета и Автозаполнение версий с помощью API V3.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="b5bc5-105">Ресурс, используемый для выполнения запросов автозаполнения, — это `SearchAutocompleteService` ресурс, найденный в [индексе службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="b5bc5-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="b5bc5-106">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="b5bc5-106">Versioning</span></span>

<span data-ttu-id="b5bc5-107">Используются следующие `@type` значения:</span><span class="sxs-lookup"><span data-stu-id="b5bc5-107">The following `@type` values are used:</span></span>

<span data-ttu-id="b5bc5-108">Значение @type</span><span class="sxs-lookup"><span data-stu-id="b5bc5-108">@type value</span></span>                          | <span data-ttu-id="b5bc5-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="b5bc5-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="b5bc5-110">сеарчаутокомплетесервице</span><span class="sxs-lookup"><span data-stu-id="b5bc5-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="b5bc5-111">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="b5bc5-111">The initial release</span></span>
<span data-ttu-id="b5bc5-112">Сеарчаутокомплетесервице/3.0.0 — бета-версия</span><span class="sxs-lookup"><span data-stu-id="b5bc5-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="b5bc5-113">Псевдоним `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="b5bc5-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="b5bc5-114">Сеарчаутокомплетесервице/3.0.0-RC</span><span class="sxs-lookup"><span data-stu-id="b5bc5-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="b5bc5-115">Псевдоним `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="b5bc5-115">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="b5bc5-116">Сеарчаутокомплетесервице/3.5.0</span><span class="sxs-lookup"><span data-stu-id="b5bc5-116">SearchAutocompleteService/3.5.0</span></span>      | <span data-ttu-id="b5bc5-117">Включает поддержку `packageType` параметра запроса</span><span class="sxs-lookup"><span data-stu-id="b5bc5-117">Includes support for `packageType` query parameter</span></span>

### <a name="searchautocompleteservice350"></a><span data-ttu-id="b5bc5-118">Сеарчаутокомплетесервице/3.5.0</span><span class="sxs-lookup"><span data-stu-id="b5bc5-118">SearchAutocompleteService/3.5.0</span></span>
<span data-ttu-id="b5bc5-119">Эта версия предоставляет поддержку для `packageType` параметра запроса, что позволяет выполнять фильтрацию по определенным типам пакетов.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-119">This version introduces support for the `packageType` query parameter, allowing filtering by author defined package types.</span></span> <span data-ttu-id="b5bc5-120">Он полностью обратно совместим с запросами к `SearchAutocompleteService` .</span><span class="sxs-lookup"><span data-stu-id="b5bc5-120">It is fully backwards compatible with queries to `SearchAutocompleteService`.</span></span>

## <a name="base-url"></a><span data-ttu-id="b5bc5-121">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b5bc5-121">Base URL</span></span>

<span data-ttu-id="b5bc5-122">Базовый URL-адрес для следующих API-интерфейсов — это значение `@id` свойства, связанного с одним из вышеупомянутых `@type` значений ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-122">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="b5bc5-123">В следующем документе будет использоваться базовый URL-адрес заполнителя `{@id}` .</span><span class="sxs-lookup"><span data-stu-id="b5bc5-123">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="b5bc5-124">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="b5bc5-124">HTTP Methods</span></span>

<span data-ttu-id="b5bc5-125">Все URL-адреса, найденные в ресурсе регистрации, поддерживают методы HTTP `GET` и `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="b5bc5-125">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="b5bc5-126">Поиск идентификаторов пакетов</span><span class="sxs-lookup"><span data-stu-id="b5bc5-126">Search for package IDs</span></span>

<span data-ttu-id="b5bc5-127">Первый API автозаполнения поддерживает поиск части строки идентификатора пакета.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-127">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="b5bc5-128">Это очень удобно, если вы хотите предоставить typeahead пакета в пользовательском интерфейсе, интегрированном с источником пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-128">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="b5bc5-129">Пакет, содержащий только непоставленные версии, не будет отображаться в результатах.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-129">A package with only unlisted versions will not appear in the results.</span></span>

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}
```

### <a name="request-parameters"></a><span data-ttu-id="b5bc5-130">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="b5bc5-130">Request parameters</span></span>

<span data-ttu-id="b5bc5-131">Имя</span><span class="sxs-lookup"><span data-stu-id="b5bc5-131">Name</span></span>        | <span data-ttu-id="b5bc5-132">В</span><span class="sxs-lookup"><span data-stu-id="b5bc5-132">In</span></span>     | <span data-ttu-id="b5bc5-133">Тип</span><span class="sxs-lookup"><span data-stu-id="b5bc5-133">Type</span></span>    | <span data-ttu-id="b5bc5-134">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b5bc5-134">Required</span></span> | <span data-ttu-id="b5bc5-135">Примечания</span><span class="sxs-lookup"><span data-stu-id="b5bc5-135">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="b5bc5-136">q</span><span class="sxs-lookup"><span data-stu-id="b5bc5-136">q</span></span>           | <span data-ttu-id="b5bc5-137">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b5bc5-137">URL</span></span>    | <span data-ttu-id="b5bc5-138">строка</span><span class="sxs-lookup"><span data-stu-id="b5bc5-138">string</span></span>  | <span data-ttu-id="b5bc5-139">нет</span><span class="sxs-lookup"><span data-stu-id="b5bc5-139">no</span></span>       | <span data-ttu-id="b5bc5-140">Строка для сравнения с идентификаторами пакета</span><span class="sxs-lookup"><span data-stu-id="b5bc5-140">The string to compare against package IDs</span></span>
<span data-ttu-id="b5bc5-141">skip</span><span class="sxs-lookup"><span data-stu-id="b5bc5-141">skip</span></span>        | <span data-ttu-id="b5bc5-142">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b5bc5-142">URL</span></span>    | <span data-ttu-id="b5bc5-143">Целое число</span><span class="sxs-lookup"><span data-stu-id="b5bc5-143">integer</span></span> | <span data-ttu-id="b5bc5-144">нет</span><span class="sxs-lookup"><span data-stu-id="b5bc5-144">no</span></span>       | <span data-ttu-id="b5bc5-145">Число пропускаемых результатов для разбивки на страницы</span><span class="sxs-lookup"><span data-stu-id="b5bc5-145">The number of results to skip, for pagination</span></span>
<span data-ttu-id="b5bc5-146">take</span><span class="sxs-lookup"><span data-stu-id="b5bc5-146">take</span></span>        | <span data-ttu-id="b5bc5-147">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b5bc5-147">URL</span></span>    | <span data-ttu-id="b5bc5-148">Целое число</span><span class="sxs-lookup"><span data-stu-id="b5bc5-148">integer</span></span> | <span data-ttu-id="b5bc5-149">нет</span><span class="sxs-lookup"><span data-stu-id="b5bc5-149">no</span></span>       | <span data-ttu-id="b5bc5-150">Число возвращаемых результатов для разбивки на страницы</span><span class="sxs-lookup"><span data-stu-id="b5bc5-150">The number of results to return, for pagination</span></span>
<span data-ttu-id="b5bc5-151">prerelease</span><span class="sxs-lookup"><span data-stu-id="b5bc5-151">prerelease</span></span>  | <span data-ttu-id="b5bc5-152">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b5bc5-152">URL</span></span>    | <span data-ttu-id="b5bc5-153">Логическое</span><span class="sxs-lookup"><span data-stu-id="b5bc5-153">boolean</span></span> | <span data-ttu-id="b5bc5-154">нет</span><span class="sxs-lookup"><span data-stu-id="b5bc5-154">no</span></span>       | <span data-ttu-id="b5bc5-155">`true` или `false` определить, следует ли включать [пакеты предварительной версии](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="b5bc5-155">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="b5bc5-156">семверлевел</span><span class="sxs-lookup"><span data-stu-id="b5bc5-156">semVerLevel</span></span> | <span data-ttu-id="b5bc5-157">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b5bc5-157">URL</span></span>    | <span data-ttu-id="b5bc5-158">строка</span><span class="sxs-lookup"><span data-stu-id="b5bc5-158">string</span></span>  | <span data-ttu-id="b5bc5-159">нет</span><span class="sxs-lookup"><span data-stu-id="b5bc5-159">no</span></span>       | <span data-ttu-id="b5bc5-160">Строка версии SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="b5bc5-160">A SemVer 1.0.0 version string</span></span> 
<span data-ttu-id="b5bc5-161">packageType</span><span class="sxs-lookup"><span data-stu-id="b5bc5-161">packageType</span></span> | <span data-ttu-id="b5bc5-162">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b5bc5-162">URL</span></span>    | <span data-ttu-id="b5bc5-163">строка</span><span class="sxs-lookup"><span data-stu-id="b5bc5-163">string</span></span>  | <span data-ttu-id="b5bc5-164">нет</span><span class="sxs-lookup"><span data-stu-id="b5bc5-164">no</span></span>       | <span data-ttu-id="b5bc5-165">Тип пакета, используемый для фильтрации пакетов (добавляется в `SearchAutocompleteService/3.5.0` )</span><span class="sxs-lookup"><span data-stu-id="b5bc5-165">The package type to use to filter packages (added in `SearchAutocompleteService/3.5.0`)</span></span>

<span data-ttu-id="b5bc5-166">Запрос автозаполнения `q` анализируется способом, который определяется реализацией сервера.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-166">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="b5bc5-167">nuget.org поддерживает запросы к префиксам токенов ИДЕНТИФИКАТОРов пакетов, которые представляют собой фрагменты идентификатора, созданного путем разделения оригинала на символы Camel и символов.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-167">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="b5bc5-168">Значение `skip` параметра по умолчанию равно 0.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-168">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="b5bc5-169">`take`Параметр должен быть целым числом больше нуля.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-169">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="b5bc5-170">Реализация сервера может накладывать максимальное значение.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-170">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="b5bc5-171">Если `prerelease` не указан, пакеты предварительной версии исключаются.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-171">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="b5bc5-172">`semVerLevel`Параметр запроса используется для явного согласия на [пакеты 2.0.0 SemVer](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="b5bc5-172">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="b5bc5-173">Если этот параметр запроса исключен, будут возвращены только идентификаторы пакетов с совместимыми версиями SemVer 1.0.0 (со [стандартными предупреждениями управления версиями NuGet](../concepts/package-versioning.md) , такими как строки версии с 4 целыми частями).</span><span class="sxs-lookup"><span data-stu-id="b5bc5-173">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="b5bc5-174">Если указан `semVerLevel=2.0.0` , будут возвращены совместимые пакеты SemVer 1.0.0 и SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-174">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="b5bc5-175">Дополнительные сведения см. в разделе [Поддержка SemVer 2.0.0 для NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .</span><span class="sxs-lookup"><span data-stu-id="b5bc5-175">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

<span data-ttu-id="b5bc5-176">`packageType`Параметр используется для дальнейшей фильтрации результатов автозаполнения только в пакетах, имеющих по крайней мере один тип пакета, совпадающий с именем типа пакета.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-176">The `packageType` parameter is used to further filter the autocomplete results to only packages that have at least one package type matching the package type name.</span></span>
<span data-ttu-id="b5bc5-177">Если предоставленный тип пакета не является допустимым типом пакета, как определено в [документе типа пакета](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), будет возвращен пустой результат.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-177">If the provided package type is not a valid package type as defined by the [Package Type document](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), an empty result will returned.</span></span>
<span data-ttu-id="b5bc5-178">Если предоставленный тип пакета пуст, фильтр применяться не будет.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-178">If the provided package type is empty, no filter will be applied.</span></span> <span data-ttu-id="b5bc5-179">Иными словами, передача значения в `packageType` параметр будет вести себя так, как если бы параметр не был передан.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-179">In other words, passing no value to the `packageType` parameter will behave as if the parameter was not passed.</span></span>

### <a name="response"></a><span data-ttu-id="b5bc5-180">Ответ</span><span class="sxs-lookup"><span data-stu-id="b5bc5-180">Response</span></span>

<span data-ttu-id="b5bc5-181">Ответ — это документ JSON, содержащий `take` результаты автозаполнения.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-181">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="b5bc5-182">Корневой объект JSON имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="b5bc5-182">The root JSON object has the following properties:</span></span>

<span data-ttu-id="b5bc5-183">Имя</span><span class="sxs-lookup"><span data-stu-id="b5bc5-183">Name</span></span>      | <span data-ttu-id="b5bc5-184">Тип</span><span class="sxs-lookup"><span data-stu-id="b5bc5-184">Type</span></span>             | <span data-ttu-id="b5bc5-185">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b5bc5-185">Required</span></span> | <span data-ttu-id="b5bc5-186">Примечания</span><span class="sxs-lookup"><span data-stu-id="b5bc5-186">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="b5bc5-187">тоталхитс</span><span class="sxs-lookup"><span data-stu-id="b5bc5-187">totalHits</span></span> | <span data-ttu-id="b5bc5-188">Целое число</span><span class="sxs-lookup"><span data-stu-id="b5bc5-188">integer</span></span>          | <span data-ttu-id="b5bc5-189">yes</span><span class="sxs-lookup"><span data-stu-id="b5bc5-189">yes</span></span>      | <span data-ttu-id="b5bc5-190">Общее число совпадений, неотношении `skip` и `take`</span><span class="sxs-lookup"><span data-stu-id="b5bc5-190">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="b5bc5-191">.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-191">data</span></span>      | <span data-ttu-id="b5bc5-192">Массив строк</span><span class="sxs-lookup"><span data-stu-id="b5bc5-192">array of strings</span></span> | <span data-ttu-id="b5bc5-193">yes</span><span class="sxs-lookup"><span data-stu-id="b5bc5-193">yes</span></span>      | <span data-ttu-id="b5bc5-194">Идентификаторы пакетов, совпадающие по запросу</span><span class="sxs-lookup"><span data-stu-id="b5bc5-194">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="b5bc5-195">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="b5bc5-195">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="b5bc5-196">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="b5bc5-196">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="b5bc5-197">Перечислить версии пакета</span><span class="sxs-lookup"><span data-stu-id="b5bc5-197">Enumerate package versions</span></span>

<span data-ttu-id="b5bc5-198">После того как идентификатор пакета будет обнаружен с помощью предыдущего API, клиент может использовать API автозаполнения для перечисления версий пакета для указанного идентификатора пакета.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-198">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="b5bc5-199">Версия пакета, которая не указана в списке, не будет отображаться в результатах.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-199">A package version that is unlisted will not appear in the results.</span></span>

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="b5bc5-200">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="b5bc5-200">Request parameters</span></span>

<span data-ttu-id="b5bc5-201">Имя</span><span class="sxs-lookup"><span data-stu-id="b5bc5-201">Name</span></span>        | <span data-ttu-id="b5bc5-202">В</span><span class="sxs-lookup"><span data-stu-id="b5bc5-202">In</span></span>     | <span data-ttu-id="b5bc5-203">Тип</span><span class="sxs-lookup"><span data-stu-id="b5bc5-203">Type</span></span>    | <span data-ttu-id="b5bc5-204">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b5bc5-204">Required</span></span> | <span data-ttu-id="b5bc5-205">Примечания</span><span class="sxs-lookup"><span data-stu-id="b5bc5-205">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="b5bc5-206">идентификатор</span><span class="sxs-lookup"><span data-stu-id="b5bc5-206">id</span></span>          | <span data-ttu-id="b5bc5-207">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b5bc5-207">URL</span></span>    | <span data-ttu-id="b5bc5-208">строка</span><span class="sxs-lookup"><span data-stu-id="b5bc5-208">string</span></span>  | <span data-ttu-id="b5bc5-209">yes</span><span class="sxs-lookup"><span data-stu-id="b5bc5-209">yes</span></span>      | <span data-ttu-id="b5bc5-210">Идентификатор пакета для выборки версий для</span><span class="sxs-lookup"><span data-stu-id="b5bc5-210">The package ID to fetch versions for</span></span>
<span data-ttu-id="b5bc5-211">prerelease</span><span class="sxs-lookup"><span data-stu-id="b5bc5-211">prerelease</span></span>  | <span data-ttu-id="b5bc5-212">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b5bc5-212">URL</span></span>    | <span data-ttu-id="b5bc5-213">Логическое</span><span class="sxs-lookup"><span data-stu-id="b5bc5-213">boolean</span></span> | <span data-ttu-id="b5bc5-214">нет</span><span class="sxs-lookup"><span data-stu-id="b5bc5-214">no</span></span>       | <span data-ttu-id="b5bc5-215">`true` или `false` определить, следует ли включать [пакеты предварительной версии](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="b5bc5-215">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="b5bc5-216">семверлевел</span><span class="sxs-lookup"><span data-stu-id="b5bc5-216">semVerLevel</span></span> | <span data-ttu-id="b5bc5-217">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b5bc5-217">URL</span></span>    | <span data-ttu-id="b5bc5-218">строка</span><span class="sxs-lookup"><span data-stu-id="b5bc5-218">string</span></span>  | <span data-ttu-id="b5bc5-219">нет</span><span class="sxs-lookup"><span data-stu-id="b5bc5-219">no</span></span>       | <span data-ttu-id="b5bc5-220">Строка версии 2.0.0 SemVer</span><span class="sxs-lookup"><span data-stu-id="b5bc5-220">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="b5bc5-221">Если `prerelease` не указан, пакеты предварительной версии исключаются.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-221">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="b5bc5-222">`semVerLevel`Параметр запроса используется для явного согласия на пакеты 2.0.0 SemVer.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-222">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="b5bc5-223">Если этот параметр запроса исключен, будут возвращены только версии SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-223">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="b5bc5-224">Если указан `semVerLevel=2.0.0` , будут возвращены версии SemVer 1.0.0 и SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-224">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="b5bc5-225">Дополнительные сведения см. в разделе [Поддержка SemVer 2.0.0 для NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .</span><span class="sxs-lookup"><span data-stu-id="b5bc5-225">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="b5bc5-226">Ответ</span><span class="sxs-lookup"><span data-stu-id="b5bc5-226">Response</span></span>

<span data-ttu-id="b5bc5-227">Ответ — это документ JSON, содержащий все версии пакета указанного идентификатора пакета, который фильтрует по заданным параметрам запроса.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-227">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="b5bc5-228">Корневой объект JSON имеет следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="b5bc5-228">The root JSON object has the following property:</span></span>

<span data-ttu-id="b5bc5-229">Имя</span><span class="sxs-lookup"><span data-stu-id="b5bc5-229">Name</span></span>      | <span data-ttu-id="b5bc5-230">Тип</span><span class="sxs-lookup"><span data-stu-id="b5bc5-230">Type</span></span>             | <span data-ttu-id="b5bc5-231">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b5bc5-231">Required</span></span> | <span data-ttu-id="b5bc5-232">Примечания</span><span class="sxs-lookup"><span data-stu-id="b5bc5-232">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="b5bc5-233">.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-233">data</span></span>      | <span data-ttu-id="b5bc5-234">Массив строк</span><span class="sxs-lookup"><span data-stu-id="b5bc5-234">array of strings</span></span> | <span data-ttu-id="b5bc5-235">yes</span><span class="sxs-lookup"><span data-stu-id="b5bc5-235">yes</span></span>      | <span data-ttu-id="b5bc5-236">Версии пакета, соответствующие запросу</span><span class="sxs-lookup"><span data-stu-id="b5bc5-236">The package versions matched by the request</span></span>

<span data-ttu-id="b5bc5-237">Версии пакета в `data` массиве могут содержать метаданные сборки SemVer 2.0.0 (например, `1.0.0+metadata` ), если в `semVerLevel=2.0.0` строке запроса содержится.</span><span class="sxs-lookup"><span data-stu-id="b5bc5-237">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="b5bc5-238">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="b5bc5-238">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="b5bc5-239">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="b5bc5-239">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
