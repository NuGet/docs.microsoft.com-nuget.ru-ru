---
title: Tools.JSON для обнаружения версии nuget.exe
description: Конечная точка для
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 003139abac7808dbdaef4aa66119e09772db2b4f
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852537"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="0b082-103">Tools.JSON для обнаружения версии nuget.exe</span><span class="sxs-lookup"><span data-stu-id="0b082-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="0b082-104">В настоящее время существует несколько способов получить последнюю версию nuget.exe на компьютере, допускающий применение сценариев образом.</span><span class="sxs-lookup"><span data-stu-id="0b082-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="0b082-105">Например, можно загрузить и извлечь [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) пакет с сайта nuget.org. Это имеет некоторые сложности, поскольку он либо требует, что у вас есть nuget.exe (для `nuget.exe install`) или необходимо распаковать с помощью средства основные unzip файла nupkg и найти двоичные внутренние.</span><span class="sxs-lookup"><span data-stu-id="0b082-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="0b082-106">Если у вас уже есть nuget.exe, можно также использовать `nuget.exe update -self`, однако для этого также требуется наличие копия nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="0b082-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="0b082-107">Этот подход можно также обновляет до последней версии.</span><span class="sxs-lookup"><span data-stu-id="0b082-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="0b082-108">Он не поддерживает использование конкретной версии.</span><span class="sxs-lookup"><span data-stu-id="0b082-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="0b082-109">`tools.json` Конечная точка будет доступна оба устранены начальной загрузки и передать управление версии nuget.exe загруженный.</span><span class="sxs-lookup"><span data-stu-id="0b082-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="0b082-110">Это можно использовать в средах непрерывной Интеграции и Развертывания или в пользовательских сценариев для поиска и скачивания любой версии nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="0b082-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="0b082-111">`tools.json` Конечной точки можно извлечь с помощью HTTP-запроса без проверки подлинности (например `Invoke-WebRequest` в PowerShell или `wget`).</span><span class="sxs-lookup"><span data-stu-id="0b082-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="0b082-112">Он может быть проанализирована с использованием десериализатор JSON и последующих nuget.exe продукты, которые URL-адреса можно также выбрать с помощью HTTP-запросы, не прошедшие проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="0b082-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="0b082-113">Конечную точку можно извлечь с помощью `GET` метод:</span><span class="sxs-lookup"><span data-stu-id="0b082-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="0b082-114">[Схему JSON](http://json-schema.org/) для конечной точки можно найти здесь:</span><span class="sxs-lookup"><span data-stu-id="0b082-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="0b082-115">Ответ</span><span class="sxs-lookup"><span data-stu-id="0b082-115">Response</span></span>

<span data-ttu-id="0b082-116">Ответ представляет собой документ JSON, содержащий все доступные версии nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="0b082-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="0b082-117">Корневой объект JSON имеет следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="0b082-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="0b082-118">name</span><span class="sxs-lookup"><span data-stu-id="0b082-118">Name</span></span>      | <span data-ttu-id="0b082-119">Тип</span><span class="sxs-lookup"><span data-stu-id="0b082-119">Type</span></span>             | <span data-ttu-id="0b082-120">Обязательно</span><span class="sxs-lookup"><span data-stu-id="0b082-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="0b082-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="0b082-121">nuget.exe</span></span> | <span data-ttu-id="0b082-122">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="0b082-122">array of objects</span></span> | <span data-ttu-id="0b082-123">да</span><span class="sxs-lookup"><span data-stu-id="0b082-123">yes</span></span>

<span data-ttu-id="0b082-124">Каждый объект в `nuget.exe` массива имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="0b082-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="0b082-125">name</span><span class="sxs-lookup"><span data-stu-id="0b082-125">Name</span></span>     | <span data-ttu-id="0b082-126">Тип</span><span class="sxs-lookup"><span data-stu-id="0b082-126">Type</span></span>   | <span data-ttu-id="0b082-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="0b082-127">Required</span></span> | <span data-ttu-id="0b082-128">Примечания</span><span class="sxs-lookup"><span data-stu-id="0b082-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="0b082-129">version</span><span class="sxs-lookup"><span data-stu-id="0b082-129">version</span></span>  | <span data-ttu-id="0b082-130">string</span><span class="sxs-lookup"><span data-stu-id="0b082-130">string</span></span> | <span data-ttu-id="0b082-131">да</span><span class="sxs-lookup"><span data-stu-id="0b082-131">yes</span></span>      | <span data-ttu-id="0b082-132">Строка SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="0b082-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="0b082-133">url</span><span class="sxs-lookup"><span data-stu-id="0b082-133">url</span></span>      | <span data-ttu-id="0b082-134">string</span><span class="sxs-lookup"><span data-stu-id="0b082-134">string</span></span> | <span data-ttu-id="0b082-135">да</span><span class="sxs-lookup"><span data-stu-id="0b082-135">yes</span></span>      | <span data-ttu-id="0b082-136">Абсолютный URL-адрес для загрузки этой версии nuget.exe</span><span class="sxs-lookup"><span data-stu-id="0b082-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="0b082-137">рабочей области</span><span class="sxs-lookup"><span data-stu-id="0b082-137">stage</span></span>    | <span data-ttu-id="0b082-138">string</span><span class="sxs-lookup"><span data-stu-id="0b082-138">string</span></span> | <span data-ttu-id="0b082-139">да</span><span class="sxs-lookup"><span data-stu-id="0b082-139">yes</span></span>      | <span data-ttu-id="0b082-140">Содержит строку перечисления</span><span class="sxs-lookup"><span data-stu-id="0b082-140">An enum string</span></span>
<span data-ttu-id="0b082-141">Отправить</span><span class="sxs-lookup"><span data-stu-id="0b082-141">uploaded</span></span> | <span data-ttu-id="0b082-142">string</span><span class="sxs-lookup"><span data-stu-id="0b082-142">string</span></span> | <span data-ttu-id="0b082-143">да</span><span class="sxs-lookup"><span data-stu-id="0b082-143">yes</span></span>      | <span data-ttu-id="0b082-144">Приблизительное ISO 8601 отметка времени после версии были сделаны доступными</span><span class="sxs-lookup"><span data-stu-id="0b082-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="0b082-145">Элементы массива сортируются по убыванию, SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="0b082-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="0b082-146">Эта гарантия призвана уменьшить нагрузку клиента, который заинтересовано в наибольший номер версии.</span><span class="sxs-lookup"><span data-stu-id="0b082-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="0b082-147">Однако это означает, что список не отсортированы в хронологическом порядке.</span><span class="sxs-lookup"><span data-stu-id="0b082-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="0b082-148">Например при обслуживании более ранней версии основных на дату позже выше основной номер версии, эта версия служб не появится в верхней части списка.</span><span class="sxs-lookup"><span data-stu-id="0b082-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="0b082-149">Если требуется последняя версия, выпускаемых корпорацией *timestamp*, достаточно отсортировать массив с `uploaded` строка.</span><span class="sxs-lookup"><span data-stu-id="0b082-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="0b082-150">Это работает, поскольку `uploaded` отметки времени находится в [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) формат, в которой могут быть отсортированы в хронологическом порядке с помощью лексикографических сортировки (т. е. простая строка сортировки).</span><span class="sxs-lookup"><span data-stu-id="0b082-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="0b082-151">`stage` Свойство указывает, как цельные проверенные — эта версия средства.</span><span class="sxs-lookup"><span data-stu-id="0b082-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="0b082-152">Этап</span><span class="sxs-lookup"><span data-stu-id="0b082-152">Stage</span></span>              | <span data-ttu-id="0b082-153">Значение</span><span class="sxs-lookup"><span data-stu-id="0b082-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="0b082-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="0b082-154">EarlyAccessPreview</span></span> | <span data-ttu-id="0b082-155">Не отображается на [загрузить веб-страницу](https://www.nuget.org/downloads) и должны быть проверены для партнеров</span><span class="sxs-lookup"><span data-stu-id="0b082-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="0b082-156">Выпущено</span><span class="sxs-lookup"><span data-stu-id="0b082-156">Released</span></span>           | <span data-ttu-id="0b082-157">Доступно на сайте загрузок но еще не рекомендуется к использованию широкое распространение</span><span class="sxs-lookup"><span data-stu-id="0b082-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="0b082-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="0b082-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="0b082-159">Доступные на сайте загрузок и рекомендуется для потребления</span><span class="sxs-lookup"><span data-stu-id="0b082-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="0b082-160">Один из простых подходов для наличия последней рекомендуемой версии должна стать первой версии в списке, который имеет `stage` значение `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="0b082-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="0b082-161">Это работает, поскольку версии сортируются в порядке SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="0b082-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="0b082-162">`NuGet.CommandLine` Пакета на сайте nuget.org обычно обновляется только с `ReleasedAndBlessed` версий.</span><span class="sxs-lookup"><span data-stu-id="0b082-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="0b082-163">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="0b082-163">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="0b082-164">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="0b082-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
