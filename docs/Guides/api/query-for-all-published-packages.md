---
title: "Запрос всех пакетов, опубликованных на сайте nuget.org | Документы Майкрософт"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 11/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "С помощью API NuGet вы можете запросить все пакеты, опубликованные на сайте nuget.org, и быть в курсе последних событий."
keywords: "перечисление всех пакетов API NuGet, репликация пакетов API NuGet, самые новые пакеты на сайте nuget.org"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: ce25680f3b591e9c6b0234b6ac30b82205d10ad3
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/20/2018
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="844ad-104">Запрос всех пакетов, опубликованных на сайте nuget.org</span><span class="sxs-lookup"><span data-stu-id="844ad-104">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="844ad-105">Типичным шаблоном запроса для устаревшего OData V2 API было перечисление всех пакетов, опубликованных на сайте nuget.org, с сортировкой по времени публикации.</span><span class="sxs-lookup"><span data-stu-id="844ad-105">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="844ad-106">Подобный запрос к сайту nuget.org может потребоваться в самых разных ситуациях:</span><span class="sxs-lookup"><span data-stu-id="844ad-106">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="844ad-107">Репликация всего сайта nuget.org</span><span class="sxs-lookup"><span data-stu-id="844ad-107">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="844ad-108">Проверка на наличие новых версий для пакетов</span><span class="sxs-lookup"><span data-stu-id="844ad-108">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="844ad-109">Поиск пакетов, зависящих от вашего пакета</span><span class="sxs-lookup"><span data-stu-id="844ad-109">Finding packages that depend on your package</span></span>

<span data-ttu-id="844ad-110">Ранее для этого обычно выполнялась сортировка сущности пакета OData по метке времени и просмотр огромного результирующего набора с помощью параметров `skip` и `top` (размер страницы).</span><span class="sxs-lookup"><span data-stu-id="844ad-110">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="844ad-111">К сожалению, у этого способа есть несколько недостатков:</span><span class="sxs-lookup"><span data-stu-id="844ad-111">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="844ad-112">Возможность отсутствия пакетов, так как запросы выполняются для данных, которые часто меняют порядок.</span><span class="sxs-lookup"><span data-stu-id="844ad-112">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="844ad-113">Большое время отклика запроса, так как запросы не оптимизируются (лучше всего оптимизированы запросы, поддерживающие основной сценарий для официального клиента NuGet).</span><span class="sxs-lookup"><span data-stu-id="844ad-113">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="844ad-114">Использование нерекомендуемого и незадокументированного API, из-за чего не гарантируется поддержка этих запросов в будущем.</span><span class="sxs-lookup"><span data-stu-id="844ad-114">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="844ad-115">Неспособность воспроизвести журнал в том порядке, в котором он формировался.</span><span class="sxs-lookup"><span data-stu-id="844ad-115">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="844ad-116">По этой причине можно воспользоваться приведенным ниже руководством, чтобы обеспечить более надежную и прогнозируемую работу в вышеупомянутых сценариях.</span><span class="sxs-lookup"><span data-stu-id="844ad-116">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="844ad-117">Обзор</span><span class="sxs-lookup"><span data-stu-id="844ad-117">Overview</span></span>

<span data-ttu-id="844ad-118">Центральной точкой этого руководства является ресурс в [API NuGet](../../api/overview.md), называемый **каталогом**.</span><span class="sxs-lookup"><span data-stu-id="844ad-118">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="844ad-119">Каталог — это доступный только для добавления API, который позволяет вызывающему объекту просмотреть полный журнал пакетов, добавленных, измененных и удаленных на сайте nuget.org. Если вас интересуют все пакеты, опубликованные на сайте nuget.org, или их подмножество, каталог отлично подходит для того, чтобы оставаться в курсе актуального набора доступных пакетов.</span><span class="sxs-lookup"><span data-stu-id="844ad-119">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="844ad-120">Это руководство имеет общий характер. Если вы хотите получить более подробные сведения о каталоге, см. соответствующий [справочник по API](../../api/catalog-resource.md).</span><span class="sxs-lookup"><span data-stu-id="844ad-120">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="844ad-121">Приведенные ниже шаги можно реализовать на любом языке программирования.</span><span class="sxs-lookup"><span data-stu-id="844ad-121">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="844ad-122">Если вам нужен полноценный рабочий пример, обратите внимание на указанный ниже [пример на C#](#c-sample-code).</span><span class="sxs-lookup"><span data-stu-id="844ad-122">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="844ad-123">В противном случае выполните приведенные ниже инструкции, чтобы создать надежное средство чтения каталога.</span><span class="sxs-lookup"><span data-stu-id="844ad-123">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="844ad-124">Инициализация курсора</span><span class="sxs-lookup"><span data-stu-id="844ad-124">Initialize a cursor</span></span>

<span data-ttu-id="844ad-125">Первым шагом в создании надежного средства чтения каталога является реализация курсора.</span><span class="sxs-lookup"><span data-stu-id="844ad-125">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="844ad-126">Полные сведения о проектировании курсора каталога см. в [справочном документе по каталогу](../../api/catalog-resource.md#cursor).</span><span class="sxs-lookup"><span data-stu-id="844ad-126">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="844ad-127">Если кратко, курсор является точкой во времени, до которой вы обработали события в каталоге.</span><span class="sxs-lookup"><span data-stu-id="844ad-127">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="844ad-128">События в каталоге представляют публикации пакетов и другие их изменения.</span><span class="sxs-lookup"><span data-stu-id="844ad-128">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="844ad-129">Если вас интересуют все пакеты, когда-либо опубликованные в NuGet (с самого его появления), нужно инициализировать курсор с минимальной меткой времени (например, `DateTime.MinValue` в .NET).</span><span class="sxs-lookup"><span data-stu-id="844ad-129">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="844ad-130">Если вам нужны только пакеты, опубликованные с текущего момента, нужно использовать текущую метку времени в качестве начального значения курсора.</span><span class="sxs-lookup"><span data-stu-id="844ad-130">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="844ad-131">В этом руководстве мы инициализируем курсор с меткой времени на час раньше текущего момента.</span><span class="sxs-lookup"><span data-stu-id="844ad-131">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="844ad-132">Пока просто сохраните метку времени в памяти.</span><span class="sxs-lookup"><span data-stu-id="844ad-132">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="844ad-133">Определение URL-адреса индекса каталога</span><span class="sxs-lookup"><span data-stu-id="844ad-133">Determine catalog index URL</span></span>

<span data-ttu-id="844ad-134">Нужно определить расположение каждого ресурса (конечная точка) в API NuGet с помощью [индекса службы](../../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="844ad-134">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="844ad-135">Так как это руководство ориентировано на сайт nuget.org, мы будем использовать индекс службы для nuget.org.</span><span class="sxs-lookup"><span data-stu-id="844ad-135">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

    GET https://api.nuget.org/v3/index.json

<span data-ttu-id="844ad-136">Документ службы представляет собой документ JSON, содержащий все ресурсы на сайте nuget.org. Выполните поиск ресурса, у которого свойство `@type` имеет значение `Catalog/3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="844ad-136">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="844ad-137">Соответствующее значение свойства `@id` является URL-адресом для самого индекса каталога.</span><span class="sxs-lookup"><span data-stu-id="844ad-137">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="844ad-138">Поиск новых конечных объектов каталога</span><span class="sxs-lookup"><span data-stu-id="844ad-138">Find new catalog leaves</span></span>

<span data-ttu-id="844ad-139">Используя значение свойства `@id`, найденное на предыдущем шаге, скачайте индекс каталога:</span><span class="sxs-lookup"><span data-stu-id="844ad-139">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

    GET https://api.nuget.org/v3/catalog0/index.json

<span data-ttu-id="844ad-140">Десериализуйте [индекс каталога](../../api/catalog-resource.md#catalog-index).</span><span class="sxs-lookup"><span data-stu-id="844ad-140">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="844ad-141">Отфильтруйте все [объекты страниц каталога](../../api/catalog-resource.md#catalog-page-object-in-the-index), у которых `commitTimeStamp` меньше или равен текущему значению курсора.</span><span class="sxs-lookup"><span data-stu-id="844ad-141">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="844ad-142">Для каждой из оставшихся страниц каталога скачайте полный документ, используя свойство `@id`.</span><span class="sxs-lookup"><span data-stu-id="844ad-142">For each remaining catalog page, download the full document using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/page2926.json

<span data-ttu-id="844ad-143">Десериализуйте [страницу каталога](../../api/catalog-resource.md#catalog-page).</span><span class="sxs-lookup"><span data-stu-id="844ad-143">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="844ad-144">Отфильтруйте все [конечные объекты каталога](../../api/catalog-resource.md#catalog-item-object-in-a-page), у которых `commitTimeStamp` меньше или равен текущему значению курсора.</span><span class="sxs-lookup"><span data-stu-id="844ad-144">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="844ad-145">Скачав все неотфильтрованные страницы каталога, вы получите набор конечных объектов каталога, представляющих пакеты, которые были опубликованы, исключены из списка, добавлены в список или удалены за период между меткой времени вашего курсора и текущим моментом.</span><span class="sxs-lookup"><span data-stu-id="844ad-145">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="844ad-146">Обработка конечных объектов каталога</span><span class="sxs-lookup"><span data-stu-id="844ad-146">Process catalog leaves</span></span>

<span data-ttu-id="844ad-147">На этом этапе вы можете выполнить любую пользовательскую обработку элементов каталога.</span><span class="sxs-lookup"><span data-stu-id="844ad-147">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="844ad-148">Если вам нужны только идентификатор и версия пакета, можно просмотреть свойства `nuget:id` и `nuget:version` для объектов элементов каталога, найденных на этих страницах.</span><span class="sxs-lookup"><span data-stu-id="844ad-148">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="844ad-149">Обязательно просмотрите свойство `@type`, чтобы узнать, касается ли элемент каталога существующего или удаленного пакета.</span><span class="sxs-lookup"><span data-stu-id="844ad-149">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="844ad-150">Если вас интересуют метаданные о пакете (например, описание, зависимости, размер, файла NUPKG и т. д), можно извлечь [документ конечного объекта каталога](../../api/catalog-resource.md#catalog-leaf) с помощью свойства `@id`.</span><span class="sxs-lookup"><span data-stu-id="844ad-150">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

<span data-ttu-id="844ad-151">Этот документ содержит все метаданные, входящие в [ресурс метаданных пакета](../../api/registration-base-url-resource.md), и многое другое.</span><span class="sxs-lookup"><span data-stu-id="844ad-151">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="844ad-152">На этом этапе вы реализуете настраиваемую логику.</span><span class="sxs-lookup"><span data-stu-id="844ad-152">This step is where you implement your custom logic.</span></span> <span data-ttu-id="844ad-153">Другие действия в этом руководстве реализуются аналогичным образом, независимо от конкретных действий с конечными объектами каталога.</span><span class="sxs-lookup"><span data-stu-id="844ad-153">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="844ad-154">Скачивание файла NUPKG</span><span class="sxs-lookup"><span data-stu-id="844ad-154">Downloading the .nupkg</span></span>

<span data-ttu-id="844ad-155">Если вы хотите скачать файл NUPKG для найденных в каталоге пакетов, можно использовать [ресурс содержимого пакета](../../api/package-base-address-resource.md).</span><span class="sxs-lookup"><span data-stu-id="844ad-155">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="844ad-156">Но нужно учитывать, что при обнаружении пакета в каталоге он станет доступен в ресурсе содержимого пакета с небольшой задержкой.</span><span class="sxs-lookup"><span data-stu-id="844ad-156">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="844ad-157">Поэтому если при попытке скачать файл NUPKG для найденного в каталоге пакета возникает `404 Not Found`, просто повторите попытку немного позднее.</span><span class="sxs-lookup"><span data-stu-id="844ad-157">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="844ad-158">Исправлению этой задержки посвящен вопрос GitHub [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span><span class="sxs-lookup"><span data-stu-id="844ad-158">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="844ad-159">Перемещение курсора вперед</span><span class="sxs-lookup"><span data-stu-id="844ad-159">Move the cursor forward</span></span>

<span data-ttu-id="844ad-160">После успешной обработки элементов каталога нужно определить новое значение курсора.</span><span class="sxs-lookup"><span data-stu-id="844ad-160">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="844ad-161">Для этого найдите максимальное значение (последнее в хронологическом порядке) `commitTimeStamp` для всех обработанных элементов каталога.</span><span class="sxs-lookup"><span data-stu-id="844ad-161">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="844ad-162">Это и есть новое значение курсора.</span><span class="sxs-lookup"><span data-stu-id="844ad-162">This is your new cursor value.</span></span> <span data-ttu-id="844ad-163">Сохраните его в постоянном хранилище, таком как база данных, файловая система или хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="844ad-163">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="844ad-164">Если вам нужно получить дополнительные элементы каталога, просто начните с [первого шага](#initialize-a-cursor), инициализировав значение курсора из этого постоянного хранилища.</span><span class="sxs-lookup"><span data-stu-id="844ad-164">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="844ad-165">Если приложение вызывает исключения или завершается со сбоем, не перемещайте курсор вперед.</span><span class="sxs-lookup"><span data-stu-id="844ad-165">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="844ad-166">Перемещение курсора вперед означает, что вам больше никогда не потребуется снова обработать элементы каталога, предшествующие курсору.</span><span class="sxs-lookup"><span data-stu-id="844ad-166">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="844ad-167">Если по некоторым причинам у вас возникает ошибка при обработке конечных объектов каталога, можете просто переместить курсор назад и позволить коду повторно обработать старые элементы каталога.</span><span class="sxs-lookup"><span data-stu-id="844ad-167">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="844ad-168">Пример кода на C#</span><span class="sxs-lookup"><span data-stu-id="844ad-168">C# sample code</span></span>

<span data-ttu-id="844ad-169">Так как каталог представляет собой набор документов JSON, доступных по протоколу HTTP, с ним можно взаимодействовать с помощью любого языка программирования, имеющего HTTP-клиент и десериализатор JSON.</span><span class="sxs-lookup"><span data-stu-id="844ad-169">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="844ad-170">Примеры на C# доступны в [репозитории NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="844ad-170">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="844ad-171">Пакет SDK каталога</span><span class="sxs-lookup"><span data-stu-id="844ad-171">Catalog SDK</span></span>

<span data-ttu-id="844ad-172">Для работы с каталогом проще всего использовать предварительную версию пакета SDK для каталога .NET: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span><span class="sxs-lookup"><span data-stu-id="844ad-172">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span></span> <span data-ttu-id="844ad-173">Этот пакет доступен в веб-канале `nuget-build` MyGet, для которого используется URL-адрес источника пакетов NuGet `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="844ad-173">This package is available on the `nuget-build` MyGet feed, for which you use the NuGet package source URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span></span>

<span data-ttu-id="844ad-174">Вы можете установить этот пакет в проект, совместимый с `netstandard1.3` или более поздней версии (например, .NET Framework 4.6).</span><span class="sxs-lookup"><span data-stu-id="844ad-174">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="844ad-175">Пример использования этого пакета можно найти на сайте GitHub в [проекте NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span><span class="sxs-lookup"><span data-stu-id="844ad-175">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="844ad-176">Пример полученных результатов</span><span class="sxs-lookup"><span data-stu-id="844ad-176">Sample output</span></span>

```output
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a><span data-ttu-id="844ad-177">Минималистичный пример</span><span class="sxs-lookup"><span data-stu-id="844ad-177">Minimal sample</span></span>

<span data-ttu-id="844ad-178">Пример с меньшим числом зависимостей, более подробно демонстрирующий взаимодействие с каталогом, см. в [проекте примера CatalogReaderExample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="844ad-178">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="844ad-179">Этот проект ориентирован на `netcoreapp2.0` и зависит от [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (для разрешения индекса службы) и [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (для десериализации JSON).</span><span class="sxs-lookup"><span data-stu-id="844ad-179">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="844ad-180">Основная логика кода видна в [файле Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="844ad-180">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="844ad-181">Пример полученных результатов</span><span class="sxs-lookup"><span data-stu-id="844ad-181">Sample output</span></span>

```output
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
