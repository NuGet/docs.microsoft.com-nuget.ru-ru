---
title: tools.jsдля обнаружения версий nuget.exe
description: Конечная точка для
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773822"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="f58ed-103">tools.jsдля обнаружения версий nuget.exe</span><span class="sxs-lookup"><span data-stu-id="f58ed-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="f58ed-104">Сегодня существует несколько способов получить последнюю версию nuget.exe на компьютере в сценарии.</span><span class="sxs-lookup"><span data-stu-id="f58ed-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="f58ed-105">Например, можно скачать и извлечь [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) пакет из NuGet.org. Это требует некоторой сложности, так как требуется наличие nuget.exe (для `nuget.exe install` ) или необходимости распаковать nupkg с помощью базового средства распаковки и найти двоичный файл внутри.</span><span class="sxs-lookup"><span data-stu-id="f58ed-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="f58ed-106">Если у вас уже есть nuget.exe, можно также использовать `nuget.exe update -self` , но для этого также требуется существующая копия nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="f58ed-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="f58ed-107">Этот подход также приводит к обновлению до последней версии.</span><span class="sxs-lookup"><span data-stu-id="f58ed-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="f58ed-108">Он не позволяет использовать определенную версию.</span><span class="sxs-lookup"><span data-stu-id="f58ed-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="f58ed-109">`tools.json`Конечная точка доступна как для решения проблемы начальной загрузки, так и для предоставления контроля версий загружаемых nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="f58ed-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="f58ed-110">Это можно использовать в средах CI/CD или в пользовательских скриптах для обнаружения и загрузки любой выпущенной версии nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="f58ed-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="f58ed-111">`tools.json`Конечную точку можно получить с помощью HTTP-запроса без проверки подлинности (например, `Invoke-WebRequest` в PowerShell или `wget` ).</span><span class="sxs-lookup"><span data-stu-id="f58ed-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="f58ed-112">Его можно проанализировать с помощью десериализатора JSON, и последующие nuget.exe URL-адреса загрузки также можно получить с помощью HTTP-запросов без проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f58ed-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="f58ed-113">Получить конечную точку можно с помощью `GET` метода:</span><span class="sxs-lookup"><span data-stu-id="f58ed-113">The endpoint can be fetched using the `GET` method:</span></span>

```
GET https://dist.nuget.org/tools.json
```

<span data-ttu-id="f58ed-114">[Схема JSON](https://json-schema.org/) для конечной точки доступна здесь:</span><span class="sxs-lookup"><span data-stu-id="f58ed-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a><span data-ttu-id="f58ed-115">Ответ</span><span class="sxs-lookup"><span data-stu-id="f58ed-115">Response</span></span>

<span data-ttu-id="f58ed-116">Ответ — это документ JSON, содержащий все доступные версии nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="f58ed-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="f58ed-117">Корневой объект JSON имеет следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="f58ed-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="f58ed-118">Имя</span><span class="sxs-lookup"><span data-stu-id="f58ed-118">Name</span></span>      | <span data-ttu-id="f58ed-119">Тип</span><span class="sxs-lookup"><span data-stu-id="f58ed-119">Type</span></span>             | <span data-ttu-id="f58ed-120">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f58ed-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="f58ed-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="f58ed-121">nuget.exe</span></span> | <span data-ttu-id="f58ed-122">массив объектов</span><span class="sxs-lookup"><span data-stu-id="f58ed-122">array of objects</span></span> | <span data-ttu-id="f58ed-123">yes</span><span class="sxs-lookup"><span data-stu-id="f58ed-123">yes</span></span>

<span data-ttu-id="f58ed-124">Каждый объект в `nuget.exe` массиве имеет следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="f58ed-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="f58ed-125">Имя</span><span class="sxs-lookup"><span data-stu-id="f58ed-125">Name</span></span>     | <span data-ttu-id="f58ed-126">Тип</span><span class="sxs-lookup"><span data-stu-id="f58ed-126">Type</span></span>   | <span data-ttu-id="f58ed-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f58ed-127">Required</span></span> | <span data-ttu-id="f58ed-128">Примечания</span><span class="sxs-lookup"><span data-stu-id="f58ed-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="f58ed-129">version</span><span class="sxs-lookup"><span data-stu-id="f58ed-129">version</span></span>  | <span data-ttu-id="f58ed-130">строка</span><span class="sxs-lookup"><span data-stu-id="f58ed-130">string</span></span> | <span data-ttu-id="f58ed-131">yes</span><span class="sxs-lookup"><span data-stu-id="f58ed-131">yes</span></span>      | <span data-ttu-id="f58ed-132">Строка 2.0.0 SemVer</span><span class="sxs-lookup"><span data-stu-id="f58ed-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="f58ed-133">url</span><span class="sxs-lookup"><span data-stu-id="f58ed-133">url</span></span>      | <span data-ttu-id="f58ed-134">строка</span><span class="sxs-lookup"><span data-stu-id="f58ed-134">string</span></span> | <span data-ttu-id="f58ed-135">yes</span><span class="sxs-lookup"><span data-stu-id="f58ed-135">yes</span></span>      | <span data-ttu-id="f58ed-136">Абсолютный URL-адрес для загрузки этой версии nuget.exe</span><span class="sxs-lookup"><span data-stu-id="f58ed-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="f58ed-137">разместить</span><span class="sxs-lookup"><span data-stu-id="f58ed-137">stage</span></span>    | <span data-ttu-id="f58ed-138">строка</span><span class="sxs-lookup"><span data-stu-id="f58ed-138">string</span></span> | <span data-ttu-id="f58ed-139">yes</span><span class="sxs-lookup"><span data-stu-id="f58ed-139">yes</span></span>      | <span data-ttu-id="f58ed-140">Строка перечисления</span><span class="sxs-lookup"><span data-stu-id="f58ed-140">An enum string</span></span>
<span data-ttu-id="f58ed-141">дано</span><span class="sxs-lookup"><span data-stu-id="f58ed-141">uploaded</span></span> | <span data-ttu-id="f58ed-142">строка</span><span class="sxs-lookup"><span data-stu-id="f58ed-142">string</span></span> | <span data-ttu-id="f58ed-143">yes</span><span class="sxs-lookup"><span data-stu-id="f58ed-143">yes</span></span>      | <span data-ttu-id="f58ed-144">Приблизительная метка времени ISO 8601, когда была сделана доступная версия</span><span class="sxs-lookup"><span data-stu-id="f58ed-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="f58ed-145">Элементы в массиве будут отсортированы в порядке убывания, SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="f58ed-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="f58ed-146">Эта гарантия призвана снизить нагрузку клиента, которому требуется наибольший номер версии.</span><span class="sxs-lookup"><span data-stu-id="f58ed-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="f58ed-147">Однако это означает, что список не сортируется в хронологическом порядке.</span><span class="sxs-lookup"><span data-stu-id="f58ed-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="f58ed-148">Например, если более низкая основная версия обслуживается в день позже, чем старшая старшая версия, эта обслуживаемая версия не будет отображаться в верхней части списка.</span><span class="sxs-lookup"><span data-stu-id="f58ed-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="f58ed-149">Если вы хотите, чтобы последняя версия была отпущена по *метке времени*, просто отсортируйте массив по `uploaded` строке.</span><span class="sxs-lookup"><span data-stu-id="f58ed-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="f58ed-150">Это работает потому, что `uploaded` Метка времени имеет формат [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) , который можно сортировать в хронологическом порядке с помощью лексикографическом сортировки (т. е. простой сортировки строк).</span><span class="sxs-lookup"><span data-stu-id="f58ed-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="f58ed-151">`stage`Свойство показывает, как проверены эту версию средства.</span><span class="sxs-lookup"><span data-stu-id="f58ed-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="f58ed-152">Этап</span><span class="sxs-lookup"><span data-stu-id="f58ed-152">Stage</span></span>              | <span data-ttu-id="f58ed-153">Значение</span><span class="sxs-lookup"><span data-stu-id="f58ed-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="f58ed-154">еарлякцесспревиев</span><span class="sxs-lookup"><span data-stu-id="f58ed-154">EarlyAccessPreview</span></span> | <span data-ttu-id="f58ed-155">Еще не отображается на [веб-странице загрузки](https://www.nuget.org/downloads) и должна быть проверена партнерами</span><span class="sxs-lookup"><span data-stu-id="f58ed-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="f58ed-156">Выпущено</span><span class="sxs-lookup"><span data-stu-id="f58ed-156">Released</span></span>           | <span data-ttu-id="f58ed-157">Доступно на сайте загрузки, но еще не рекомендовано для широкого использования.</span><span class="sxs-lookup"><span data-stu-id="f58ed-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="f58ed-158">релеаседандблессед</span><span class="sxs-lookup"><span data-stu-id="f58ed-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="f58ed-159">Доступно на сайте загрузки и рекомендуется для использования</span><span class="sxs-lookup"><span data-stu-id="f58ed-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="f58ed-160">Одним из простых подходов к обновлению последней рекомендованной версии является получение первой версии в списке, имеющей `stage` значение `ReleasedAndBlessed` .</span><span class="sxs-lookup"><span data-stu-id="f58ed-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="f58ed-161">Это работает потому, что версии сортируются в SemVer 2.0.0 Order.</span><span class="sxs-lookup"><span data-stu-id="f58ed-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="f58ed-162">`NuGet.CommandLine`Пакет в NuGet.org обычно обновляется только с использованием `ReleasedAndBlessed` версий.</span><span class="sxs-lookup"><span data-stu-id="f58ed-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="f58ed-163">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="f58ed-163">Sample request</span></span>

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a><span data-ttu-id="f58ed-164">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="f58ed-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
