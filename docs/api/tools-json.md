---
title: Tools.JSON для обнаружения версии nuget.exe
description: Конечная точка для
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 6184fe8e987e0637cb912999f2e3fa3a3dc9b4ba
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546939"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="4cf16-103">Tools.JSON для обнаружения версии nuget.exe</span><span class="sxs-lookup"><span data-stu-id="4cf16-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="4cf16-104">В настоящее время существует несколько способов получить последнюю версию nuget.exe на компьютере, допускающий применение сценариев образом.</span><span class="sxs-lookup"><span data-stu-id="4cf16-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="4cf16-105">Например, можно загрузить и извлечь [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) пакет с сайта nuget.org. Это имеет некоторые сложности, поскольку он либо требует, что у вас есть nuget.exe (для `nuget.exe install`) или необходимо распаковать с помощью средства основные unzip файла nupkg и найти двоичные внутренние.</span><span class="sxs-lookup"><span data-stu-id="4cf16-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="4cf16-106">Если у вас уже есть nuget.exe, можно также использовать `nuget.exe update -self`, однако для этого также требуется наличие копия nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="4cf16-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="4cf16-107">Этот подход можно также обновляет до последней версии.</span><span class="sxs-lookup"><span data-stu-id="4cf16-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="4cf16-108">Он не поддерживает использование конкретной версии.</span><span class="sxs-lookup"><span data-stu-id="4cf16-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="4cf16-109">`tools.json` Конечная точка будет доступна оба устранены начальной загрузки и передать управление версии nuget.exe загруженный.</span><span class="sxs-lookup"><span data-stu-id="4cf16-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="4cf16-110">Это можно использовать в средах непрерывной Интеграции и Развертывания или в пользовательских сценариев для поиска и скачивания любой версии nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="4cf16-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="4cf16-111">`tools.json` Конечной точки можно извлечь с помощью HTTP-запроса без проверки подлинности (например `Invoke-WebRequest` в PowerShell или `wget`).</span><span class="sxs-lookup"><span data-stu-id="4cf16-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="4cf16-112">Он может быть проанализирована с использованием десериализатор JSON и последующих nuget.exe продукты, которые URL-адреса можно также выбрать с помощью HTTP-запросы, не прошедшие проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="4cf16-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="4cf16-113">Конечную точку можно извлечь с помощью `GET` метод:</span><span class="sxs-lookup"><span data-stu-id="4cf16-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="4cf16-114">[Схему JSON](http://json-schema.org/) для конечной точки можно найти здесь:</span><span class="sxs-lookup"><span data-stu-id="4cf16-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="4cf16-115">Ответ</span><span class="sxs-lookup"><span data-stu-id="4cf16-115">Response</span></span>

<span data-ttu-id="4cf16-116">Ответ представляет собой документ JSON, содержащий все доступные версии nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="4cf16-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="4cf16-117">Корневой объект JSON имеет следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="4cf16-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="4cf16-118">name</span><span class="sxs-lookup"><span data-stu-id="4cf16-118">Name</span></span>      | <span data-ttu-id="4cf16-119">Тип</span><span class="sxs-lookup"><span data-stu-id="4cf16-119">Type</span></span>             | <span data-ttu-id="4cf16-120">Обязательно</span><span class="sxs-lookup"><span data-stu-id="4cf16-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="4cf16-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="4cf16-121">nuget.exe</span></span> | <span data-ttu-id="4cf16-122">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="4cf16-122">array of objects</span></span> | <span data-ttu-id="4cf16-123">да</span><span class="sxs-lookup"><span data-stu-id="4cf16-123">yes</span></span>

<span data-ttu-id="4cf16-124">Каждый объект в `nuget.exe` массива имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="4cf16-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="4cf16-125">name</span><span class="sxs-lookup"><span data-stu-id="4cf16-125">Name</span></span>     | <span data-ttu-id="4cf16-126">Тип</span><span class="sxs-lookup"><span data-stu-id="4cf16-126">Type</span></span>   | <span data-ttu-id="4cf16-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="4cf16-127">Required</span></span> | <span data-ttu-id="4cf16-128">Примечания</span><span class="sxs-lookup"><span data-stu-id="4cf16-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="4cf16-129">version</span><span class="sxs-lookup"><span data-stu-id="4cf16-129">version</span></span>  | <span data-ttu-id="4cf16-130">string</span><span class="sxs-lookup"><span data-stu-id="4cf16-130">string</span></span> | <span data-ttu-id="4cf16-131">да</span><span class="sxs-lookup"><span data-stu-id="4cf16-131">yes</span></span>      | <span data-ttu-id="4cf16-132">Строка SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="4cf16-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="4cf16-133">url</span><span class="sxs-lookup"><span data-stu-id="4cf16-133">url</span></span>      | <span data-ttu-id="4cf16-134">string</span><span class="sxs-lookup"><span data-stu-id="4cf16-134">string</span></span> | <span data-ttu-id="4cf16-135">да</span><span class="sxs-lookup"><span data-stu-id="4cf16-135">yes</span></span>      | <span data-ttu-id="4cf16-136">Абсолютный URL-адрес для загрузки этой версии nuget.exe</span><span class="sxs-lookup"><span data-stu-id="4cf16-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="4cf16-137">рабочей области</span><span class="sxs-lookup"><span data-stu-id="4cf16-137">stage</span></span>    | <span data-ttu-id="4cf16-138">string</span><span class="sxs-lookup"><span data-stu-id="4cf16-138">string</span></span> | <span data-ttu-id="4cf16-139">да</span><span class="sxs-lookup"><span data-stu-id="4cf16-139">yes</span></span>      | <span data-ttu-id="4cf16-140">Содержит строку перечисления</span><span class="sxs-lookup"><span data-stu-id="4cf16-140">An enum string</span></span>
<span data-ttu-id="4cf16-141">Отправить</span><span class="sxs-lookup"><span data-stu-id="4cf16-141">uploaded</span></span> | <span data-ttu-id="4cf16-142">string</span><span class="sxs-lookup"><span data-stu-id="4cf16-142">string</span></span> | <span data-ttu-id="4cf16-143">да</span><span class="sxs-lookup"><span data-stu-id="4cf16-143">yes</span></span>      | <span data-ttu-id="4cf16-144">Если версии были сделаны доступными приблизительное отметка времени</span><span class="sxs-lookup"><span data-stu-id="4cf16-144">An approximate timestamp of when the version was made available</span></span>

<span data-ttu-id="4cf16-145">Элементы массива сортируются по убыванию, SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="4cf16-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="4cf16-146">Эта гарантия призвана снизить нагрузку на клиент, поиск последней версии.</span><span class="sxs-lookup"><span data-stu-id="4cf16-146">This guarantee is meant to ease the burden on a client looking for the latest version.</span></span> 

<span data-ttu-id="4cf16-147">`stage` Свойство указывает, каким образом vettect эта версия средства предназначена.</span><span class="sxs-lookup"><span data-stu-id="4cf16-147">The `stage` property indicates how vettect this version of the tool is.</span></span> 

<span data-ttu-id="4cf16-148">Этап</span><span class="sxs-lookup"><span data-stu-id="4cf16-148">Stage</span></span>              | <span data-ttu-id="4cf16-149">Значение</span><span class="sxs-lookup"><span data-stu-id="4cf16-149">Meaning</span></span>
------------------ | ------
<span data-ttu-id="4cf16-150">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="4cf16-150">EarlyAccessPreview</span></span> | <span data-ttu-id="4cf16-151">Не отображается на [загрузить веб-страницу](https://www.nuget.org/downloads) и должны быть проверены для партнеров</span><span class="sxs-lookup"><span data-stu-id="4cf16-151">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="4cf16-152">Выпущено</span><span class="sxs-lookup"><span data-stu-id="4cf16-152">Released</span></span>           | <span data-ttu-id="4cf16-153">Доступно на сайте загрузок но еще не рекомендуется к использованию широкое распространение</span><span class="sxs-lookup"><span data-stu-id="4cf16-153">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="4cf16-154">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="4cf16-154">ReleasedAndBlessed</span></span> | <span data-ttu-id="4cf16-155">Доступные на сайте загрузок и рекомендуется для потребления</span><span class="sxs-lookup"><span data-stu-id="4cf16-155">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="4cf16-156">Один из простых подходов для наличия последней рекомендуемой версии должна стать первой версии в списке, который имеет `stage` значение `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="4cf16-156">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span>

<span data-ttu-id="4cf16-157">`NuGet.CommandLine` Пакета на сайте nuget.org обычно обновляется только с `ReleasedAndBlessed` версий.</span><span class="sxs-lookup"><span data-stu-id="4cf16-157">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="4cf16-158">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="4cf16-158">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="4cf16-159">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="4cf16-159">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
