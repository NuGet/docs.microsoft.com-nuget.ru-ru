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
ms.assetid: ead5cf7a-e51e-4cbb-8798-58226f4c853f
description: "Автозаполнение службы поиска поддерживает интерактивный обнаружения пакета идентификаторы и версии."
keywords: "API автозаполнения NuGet, идентификатор пакета NuGet поиска, идентификатор пакета подстроки"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 313ceb630947b46c34b98e14044ecf121b725087
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="autocomplete"></a><span data-ttu-id="d5eab-104">Автозавершение</span><span class="sxs-lookup"><span data-stu-id="d5eab-104">Autocomplete</span></span>

<span data-ttu-id="d5eab-105">Существует возможность создания пакета идентификатор и версия Автозаполнение опыт работы с V3 API.</span><span class="sxs-lookup"><span data-stu-id="d5eab-105">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="d5eab-106">Ресурс, используемый для автозаполнения запросов является `SearchAutocompleteService` найти ресурс в [служба индекс](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="d5eab-106">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="d5eab-107">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="d5eab-107">Versioning</span></span>

<span data-ttu-id="d5eab-108">Следующие `@type` используются значения:</span><span class="sxs-lookup"><span data-stu-id="d5eab-108">The following `@type` values are used:</span></span>

<span data-ttu-id="d5eab-109">Значение @type</span><span class="sxs-lookup"><span data-stu-id="d5eab-109">@type value</span></span>                          | <span data-ttu-id="d5eab-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="d5eab-110">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="d5eab-111">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="d5eab-111">SearchAutocompleteService</span></span>            | <span data-ttu-id="d5eab-112">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="d5eab-112">The initial release</span></span>
<span data-ttu-id="d5eab-113">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="d5eab-113">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="d5eab-114">Псевдоним`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="d5eab-114">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="d5eab-115">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="d5eab-115">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="d5eab-116">Псевдоним`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="d5eab-116">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="d5eab-117">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d5eab-117">Base URL</span></span>

<span data-ttu-id="d5eab-118">Базовый URL-адрес для следующих API-интерфейсов — это значение `@id` свойства, связанные с одной из упомянутых выше ресурсов `@type` значения.</span><span class="sxs-lookup"><span data-stu-id="d5eab-118">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="d5eab-119">В следующем документе заполнитель базовый URL-адрес `{@id}` будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="d5eab-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d5eab-120">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="d5eab-120">HTTP Methods</span></span>

<span data-ttu-id="d5eab-121">Все URL-адреса, найден в поддержку ресурсов регистрации методов HTTP `GET` и `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="d5eab-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="d5eab-122">Выполните поиск пакета идентификаторы</span><span class="sxs-lookup"><span data-stu-id="d5eab-122">Search for package IDs</span></span>

<span data-ttu-id="d5eab-123">Первый автозаполнения API поддерживает поиск строки идентификатор пакета.</span><span class="sxs-lookup"><span data-stu-id="d5eab-123">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="d5eab-124">Это очень полезно, если вы хотите предоставляют функцию typeahead пакета в пользовательском интерфейсе интегрирован с источника пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="d5eab-124">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="d5eab-125">Пакет, содержащий только версии, отсутствующие в списке не будет отображаться в результатах.</span><span class="sxs-lookup"><span data-stu-id="d5eab-125">A package with only unlisted versions will not appear in the results.</span></span>

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="d5eab-126">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="d5eab-126">Request parameters</span></span>

<span data-ttu-id="d5eab-127">Имя</span><span class="sxs-lookup"><span data-stu-id="d5eab-127">Name</span></span>        | <span data-ttu-id="d5eab-128">Увеличение</span><span class="sxs-lookup"><span data-stu-id="d5eab-128">In</span></span>     | <span data-ttu-id="d5eab-129">Тип</span><span class="sxs-lookup"><span data-stu-id="d5eab-129">Type</span></span>    | <span data-ttu-id="d5eab-130">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5eab-130">Required</span></span> | <span data-ttu-id="d5eab-131">Примечания</span><span class="sxs-lookup"><span data-stu-id="d5eab-131">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="d5eab-132">q</span><span class="sxs-lookup"><span data-stu-id="d5eab-132">q</span></span>           | <span data-ttu-id="d5eab-133">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d5eab-133">URL</span></span>    | <span data-ttu-id="d5eab-134">string</span><span class="sxs-lookup"><span data-stu-id="d5eab-134">string</span></span>  | <span data-ttu-id="d5eab-135">Нет</span><span class="sxs-lookup"><span data-stu-id="d5eab-135">no</span></span>       | <span data-ttu-id="d5eab-136">Строка для сравнения с идентификаторами пакетов</span><span class="sxs-lookup"><span data-stu-id="d5eab-136">The string to compare against package IDs</span></span>
<span data-ttu-id="d5eab-137">skip</span><span class="sxs-lookup"><span data-stu-id="d5eab-137">skip</span></span>        | <span data-ttu-id="d5eab-138">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d5eab-138">URL</span></span>    | <span data-ttu-id="d5eab-139">целочисленный</span><span class="sxs-lookup"><span data-stu-id="d5eab-139">integer</span></span> | <span data-ttu-id="d5eab-140">Нет</span><span class="sxs-lookup"><span data-stu-id="d5eab-140">no</span></span>       | <span data-ttu-id="d5eab-141">Количество пропускаемых для разбиения на страницы результатов</span><span class="sxs-lookup"><span data-stu-id="d5eab-141">The number of results to skip, for pagination</span></span>
<span data-ttu-id="d5eab-142">Take</span><span class="sxs-lookup"><span data-stu-id="d5eab-142">take</span></span>        | <span data-ttu-id="d5eab-143">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d5eab-143">URL</span></span>    | <span data-ttu-id="d5eab-144">целочисленный</span><span class="sxs-lookup"><span data-stu-id="d5eab-144">integer</span></span> | <span data-ttu-id="d5eab-145">Нет</span><span class="sxs-lookup"><span data-stu-id="d5eab-145">no</span></span>       | <span data-ttu-id="d5eab-146">Число результатов, возвращаемых для разбиения на страницы</span><span class="sxs-lookup"><span data-stu-id="d5eab-146">The number of results to return, for pagination</span></span>
<span data-ttu-id="d5eab-147">Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="d5eab-147">prerelease</span></span>  | <span data-ttu-id="d5eab-148">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d5eab-148">URL</span></span>    | <span data-ttu-id="d5eab-149">boolean</span><span class="sxs-lookup"><span data-stu-id="d5eab-149">boolean</span></span> | <span data-ttu-id="d5eab-150">Нет</span><span class="sxs-lookup"><span data-stu-id="d5eab-150">no</span></span>       | <span data-ttu-id="d5eab-151">`true`или `false` определения, следует ли включать [пакеты предварительного выпуска](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d5eab-151">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="d5eab-152">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="d5eab-152">semVerLevel</span></span> | <span data-ttu-id="d5eab-153">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d5eab-153">URL</span></span>    | <span data-ttu-id="d5eab-154">string</span><span class="sxs-lookup"><span data-stu-id="d5eab-154">string</span></span>  | <span data-ttu-id="d5eab-155">Нет</span><span class="sxs-lookup"><span data-stu-id="d5eab-155">no</span></span>       | <span data-ttu-id="d5eab-156">Строка версии 1.0.0 SemVer</span><span class="sxs-lookup"><span data-stu-id="d5eab-156">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="d5eab-157">Запрос автозаполнения `q` анализируется таким способом, который определен с помощью реализации сервера.</span><span class="sxs-lookup"><span data-stu-id="d5eab-157">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="d5eab-158">NuGet.org поддерживает выполнение запросов для префикса маркеров идентификатор пакета, которые — это идентификатор, созданный spliting исходный счет camel регистр и символы.</span><span class="sxs-lookup"><span data-stu-id="d5eab-158">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="d5eab-159">`skip` Параметра по умолчанию равно 0.</span><span class="sxs-lookup"><span data-stu-id="d5eab-159">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="d5eab-160">`take` Параметра должно быть целое число больше нуля.</span><span class="sxs-lookup"><span data-stu-id="d5eab-160">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="d5eab-161">Реализация сервера может наложить максимальное значение.</span><span class="sxs-lookup"><span data-stu-id="d5eab-161">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="d5eab-162">Если `prerelease` не указан, исключаются пакеты предварительного выпуска.</span><span class="sxs-lookup"><span data-stu-id="d5eab-162">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="d5eab-163">`semVerLevel` Параметра запроса используется для согласиться на [SemVer 2.0.0 пакетов](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="d5eab-163">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="d5eab-164">Если этот параметр запроса не исключается, будут возвращены только идентификаторы пакета с SemVer 1.0.0 совместимые версии (с [стандартные управление версиями NuGet](../reference/package-versioning.md) предупреждения, такие как строки версии 4 частей целое число).</span><span class="sxs-lookup"><span data-stu-id="d5eab-164">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="d5eab-165">Если `semVerLevel=2.0.0` указан, будут возвращены SemVer 1.0.0 и совместимые пакеты SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d5eab-165">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="d5eab-166">В разделе [SemVer 2.0.0 поддержка nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="d5eab-166">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="d5eab-167">Ответ</span><span class="sxs-lookup"><span data-stu-id="d5eab-167">Response</span></span>

<span data-ttu-id="d5eab-168">Ответ представляет документ JSON, содержащий до `take` результаты автозаполнения.</span><span class="sxs-lookup"><span data-stu-id="d5eab-168">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="d5eab-169">Корневой объект JSON имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="d5eab-169">The root JSON object has the following properties:</span></span>

<span data-ttu-id="d5eab-170">Имя</span><span class="sxs-lookup"><span data-stu-id="d5eab-170">Name</span></span>      | <span data-ttu-id="d5eab-171">Тип</span><span class="sxs-lookup"><span data-stu-id="d5eab-171">Type</span></span>             | <span data-ttu-id="d5eab-172">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5eab-172">Required</span></span> | <span data-ttu-id="d5eab-173">Примечания</span><span class="sxs-lookup"><span data-stu-id="d5eab-173">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="d5eab-174">totalHits</span><span class="sxs-lookup"><span data-stu-id="d5eab-174">totalHits</span></span> | <span data-ttu-id="d5eab-175">целочисленный</span><span class="sxs-lookup"><span data-stu-id="d5eab-175">integer</span></span>          | <span data-ttu-id="d5eab-176">да</span><span class="sxs-lookup"><span data-stu-id="d5eab-176">yes</span></span>      | <span data-ttu-id="d5eab-177">Общее количество совпадений, без учета `skip` и`take`</span><span class="sxs-lookup"><span data-stu-id="d5eab-177">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="d5eab-178">Данные</span><span class="sxs-lookup"><span data-stu-id="d5eab-178">data</span></span>      | <span data-ttu-id="d5eab-179">Массив строк</span><span class="sxs-lookup"><span data-stu-id="d5eab-179">array of strings</span></span> | <span data-ttu-id="d5eab-180">да</span><span class="sxs-lookup"><span data-stu-id="d5eab-180">yes</span></span>      | <span data-ttu-id="d5eab-181">Запрос соответствует ИД пакета</span><span class="sxs-lookup"><span data-stu-id="d5eab-181">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="d5eab-182">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="d5eab-182">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="d5eab-183">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="d5eab-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="d5eab-184">Перечисление версий пакета</span><span class="sxs-lookup"><span data-stu-id="d5eab-184">Enumerate package versions</span></span>

<span data-ttu-id="d5eab-185">После обнаружения идентификатор пакета с помощью предыдущего API клиента можно использовать автозаполнение API для перечисления версии пакета для идентификатора указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="d5eab-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="d5eab-186">Версия пакета, отсутствующие в списке не будет отображаться в результатах.</span><span class="sxs-lookup"><span data-stu-id="d5eab-186">A package version that is unlisted will not appear in the results.</span></span>

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="d5eab-187">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="d5eab-187">Request parameters</span></span>

<span data-ttu-id="d5eab-188">Имя</span><span class="sxs-lookup"><span data-stu-id="d5eab-188">Name</span></span>        | <span data-ttu-id="d5eab-189">Увеличение</span><span class="sxs-lookup"><span data-stu-id="d5eab-189">In</span></span>     | <span data-ttu-id="d5eab-190">Тип</span><span class="sxs-lookup"><span data-stu-id="d5eab-190">Type</span></span>    | <span data-ttu-id="d5eab-191">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5eab-191">Required</span></span> | <span data-ttu-id="d5eab-192">Примечания</span><span class="sxs-lookup"><span data-stu-id="d5eab-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="d5eab-193">id</span><span class="sxs-lookup"><span data-stu-id="d5eab-193">id</span></span>          | <span data-ttu-id="d5eab-194">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d5eab-194">URL</span></span>    | <span data-ttu-id="d5eab-195">string</span><span class="sxs-lookup"><span data-stu-id="d5eab-195">string</span></span>  | <span data-ttu-id="d5eab-196">да</span><span class="sxs-lookup"><span data-stu-id="d5eab-196">yes</span></span>      | <span data-ttu-id="d5eab-197">Идентификатор пакета для версии для выборки</span><span class="sxs-lookup"><span data-stu-id="d5eab-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="d5eab-198">Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="d5eab-198">prerelease</span></span>  | <span data-ttu-id="d5eab-199">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d5eab-199">URL</span></span>    | <span data-ttu-id="d5eab-200">boolean</span><span class="sxs-lookup"><span data-stu-id="d5eab-200">boolean</span></span> | <span data-ttu-id="d5eab-201">Нет</span><span class="sxs-lookup"><span data-stu-id="d5eab-201">no</span></span>       | <span data-ttu-id="d5eab-202">`true`или `false` определения, следует ли включать [пакеты предварительного выпуска](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d5eab-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="d5eab-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="d5eab-203">semVerLevel</span></span> | <span data-ttu-id="d5eab-204">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d5eab-204">URL</span></span>    | <span data-ttu-id="d5eab-205">string</span><span class="sxs-lookup"><span data-stu-id="d5eab-205">string</span></span>  | <span data-ttu-id="d5eab-206">Нет</span><span class="sxs-lookup"><span data-stu-id="d5eab-206">no</span></span>       | <span data-ttu-id="d5eab-207">Строка версии SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="d5eab-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="d5eab-208">Если `prerelease` не указан, исключаются пакеты предварительного выпуска.</span><span class="sxs-lookup"><span data-stu-id="d5eab-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="d5eab-209">`semVerLevel` Параметра запроса используется для согласиться на пакеты SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d5eab-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="d5eab-210">Если этот параметр запроса не исключается, будут возвращены только версии SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="d5eab-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="d5eab-211">Если `semVerLevel=2.0.0` указан, будут возвращены SemVer 1.0.0 и версии SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d5eab-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="d5eab-212">В разделе [SemVer 2.0.0 поддержка nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="d5eab-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="d5eab-213">Ответ</span><span class="sxs-lookup"><span data-stu-id="d5eab-213">Response</span></span>

<span data-ttu-id="d5eab-214">Ответ — документ JSON, содержащий все версии пакета идентификатор предоставленного пакета, фильтрация на основе параметров данного запроса.</span><span class="sxs-lookup"><span data-stu-id="d5eab-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="d5eab-215">Корневой объект JSON имеет следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="d5eab-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="d5eab-216">Имя</span><span class="sxs-lookup"><span data-stu-id="d5eab-216">Name</span></span>      | <span data-ttu-id="d5eab-217">Тип</span><span class="sxs-lookup"><span data-stu-id="d5eab-217">Type</span></span>             | <span data-ttu-id="d5eab-218">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5eab-218">Required</span></span> | <span data-ttu-id="d5eab-219">Примечания</span><span class="sxs-lookup"><span data-stu-id="d5eab-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="d5eab-220">Данные</span><span class="sxs-lookup"><span data-stu-id="d5eab-220">data</span></span>      | <span data-ttu-id="d5eab-221">Массив строк</span><span class="sxs-lookup"><span data-stu-id="d5eab-221">array of strings</span></span> | <span data-ttu-id="d5eab-222">да</span><span class="sxs-lookup"><span data-stu-id="d5eab-222">yes</span></span>      | <span data-ttu-id="d5eab-223">Запрос на соответствует версии пакета</span><span class="sxs-lookup"><span data-stu-id="d5eab-223">The package versions matched by the request</span></span>

<span data-ttu-id="d5eab-224">Версии пакетов в `data` массив может содержать метаданные сборки SemVer 2.0.0 (например `1.0.0+metadata`) Если `semVerLevel=2.0.0` был представлен в строке запроса.</span><span class="sxs-lookup"><span data-stu-id="d5eab-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d5eab-225">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="d5eab-225">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="d5eab-226">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="d5eab-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
