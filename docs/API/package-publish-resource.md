---
title: "Принудительные и удалить NuGet API | Документы Microsoft"
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
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "Служба публикации позволяет клиентам публикации новых пакетов и исключить или удалите существующие пакеты."
keywords: "Пакет NuGet API push, NuGet API удалить пакет, NuGet API исключить пакета пакет NuGet интерфейса API передачи, NuGet API создания пакета"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 5fbcd82b09ebd56ae21103640e7c39b482059525
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/10/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="77863-104">Принудительные и удалить</span><span class="sxs-lookup"><span data-stu-id="77863-104">Push and Delete</span></span>

<span data-ttu-id="77863-105">Существует возможность push, удалить (или исключить, в зависимости от реализации сервера) и relist пакетов с помощью NuGet V3 API.</span><span class="sxs-lookup"><span data-stu-id="77863-105">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="77863-106">Эти операции расположенного за пределами `PackagePublish` найти ресурс в [служба индекс](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="77863-106">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="77863-107">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="77863-107">Versioning</span></span>

<span data-ttu-id="77863-108">Следующие `@type` используется значение:</span><span class="sxs-lookup"><span data-stu-id="77863-108">The following `@type` value is used:</span></span>

<span data-ttu-id="77863-109">Значение @type</span><span class="sxs-lookup"><span data-stu-id="77863-109">@type value</span></span>          | <span data-ttu-id="77863-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="77863-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="77863-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="77863-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="77863-112">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="77863-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="77863-113">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="77863-113">Base URL</span></span>

<span data-ttu-id="77863-114">Базовый URL-адрес для следующих API-интерфейсов — это значение `@id` свойство `PackagePublish/2.0.0` ресурсов в источнике пакетов [служба индекс](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="77863-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="77863-115">В следующих документах используется nuget.org URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="77863-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="77863-116">Рассмотрим `https://www.nuget.org/api/v2/package` как заполнитель для `@id` значение найдено в индексе службы.</span><span class="sxs-lookup"><span data-stu-id="77863-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="77863-117">Обратите внимание, на который этот URL-адрес указывает же расположении, что конечная точка устаревших V2 push, так как использует тот же протокол.</span><span class="sxs-lookup"><span data-stu-id="77863-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="77863-118">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="77863-118">HTTP methods</span></span>

<span data-ttu-id="77863-119">`PUT`, `POST` И `DELETE` этот ресурс поддерживаемых методов HTTP.</span><span class="sxs-lookup"><span data-stu-id="77863-119">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="77863-120">Какие методы поддерживаются для каждой конечной точки см. ниже.</span><span class="sxs-lookup"><span data-stu-id="77863-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="77863-121">Пакет Push</span><span class="sxs-lookup"><span data-stu-id="77863-121">Push a package</span></span>

> [!Note]
> <span data-ttu-id="77863-122">имеет NuGet.org [Дополнительные требования](NuGet-Protocols.md) для взаимодействия с конечной точкой push.</span><span class="sxs-lookup"><span data-stu-id="77863-122">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="77863-123">NuGet.org поддерживает принудительную отправку новых пакетов с помощью следующих API.</span><span class="sxs-lookup"><span data-stu-id="77863-123">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="77863-124">Если пакет с предоставленным Идентификатором и версией уже существует, nuget.org отклонит принудительной отправки.</span><span class="sxs-lookup"><span data-stu-id="77863-124">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="77863-125">Другие источники пакетов могут поддерживать замены существующего пакета.</span><span class="sxs-lookup"><span data-stu-id="77863-125">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="77863-126">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="77863-126">Request parameters</span></span>

<span data-ttu-id="77863-127">name</span><span class="sxs-lookup"><span data-stu-id="77863-127">Name</span></span>           | <span data-ttu-id="77863-128">Увеличение</span><span class="sxs-lookup"><span data-stu-id="77863-128">In</span></span>     | <span data-ttu-id="77863-129">Тип</span><span class="sxs-lookup"><span data-stu-id="77863-129">Type</span></span>   | <span data-ttu-id="77863-130">Обязательно</span><span class="sxs-lookup"><span data-stu-id="77863-130">Required</span></span> | <span data-ttu-id="77863-131">Примечания</span><span class="sxs-lookup"><span data-stu-id="77863-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="77863-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="77863-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="77863-133">Header</span><span class="sxs-lookup"><span data-stu-id="77863-133">Header</span></span> | <span data-ttu-id="77863-134">string</span><span class="sxs-lookup"><span data-stu-id="77863-134">string</span></span> | <span data-ttu-id="77863-135">да</span><span class="sxs-lookup"><span data-stu-id="77863-135">yes</span></span>      | <span data-ttu-id="77863-136">Например `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="77863-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="77863-137">Ключ API — непрозрачная строка получения из источника пакета пользователем и настроены в клиент.</span><span class="sxs-lookup"><span data-stu-id="77863-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="77863-138">Формат строки не является обязательной, но длина ключа API не должно превышать разумный размер для значения заголовка HTTP.</span><span class="sxs-lookup"><span data-stu-id="77863-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="77863-139">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="77863-139">Request body</span></span>

<span data-ttu-id="77863-140">Текст запроса должен указываться в следующей форме:</span><span class="sxs-lookup"><span data-stu-id="77863-140">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="77863-141">Данных составной формы</span><span class="sxs-lookup"><span data-stu-id="77863-141">Multipart form data</span></span>

<span data-ttu-id="77863-142">Заголовок запроса `Content-Type` — `multipart/form-data` и необработанные байты .nupkg нажимают является первый элемент в тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="77863-142">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="77863-143">Последующих элементов составного текста учитываются.</span><span class="sxs-lookup"><span data-stu-id="77863-143">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="77863-144">Имя файла или другие заголовки составных элементов учитываются.</span><span class="sxs-lookup"><span data-stu-id="77863-144">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="77863-145">Ответ</span><span class="sxs-lookup"><span data-stu-id="77863-145">Response</span></span>

<span data-ttu-id="77863-146">Код состояния</span><span class="sxs-lookup"><span data-stu-id="77863-146">Status Code</span></span> | <span data-ttu-id="77863-147">Значение</span><span class="sxs-lookup"><span data-stu-id="77863-147">Meaning</span></span>
----------- | -------
<span data-ttu-id="77863-148">201, 202</span><span class="sxs-lookup"><span data-stu-id="77863-148">201, 202</span></span>    | <span data-ttu-id="77863-149">Пакет был успешно отправлен</span><span class="sxs-lookup"><span data-stu-id="77863-149">The package was successfully pushed</span></span>
<span data-ttu-id="77863-150">400</span><span class="sxs-lookup"><span data-stu-id="77863-150">400</span></span>         | <span data-ttu-id="77863-151">Предоставленный пакет является недопустимым</span><span class="sxs-lookup"><span data-stu-id="77863-151">The provided package is invalid</span></span>
<span data-ttu-id="77863-152">409</span><span class="sxs-lookup"><span data-stu-id="77863-152">409</span></span>         | <span data-ttu-id="77863-153">Пакет с предоставленным Идентификатором и версией уже существует</span><span class="sxs-lookup"><span data-stu-id="77863-153">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="77863-154">Код состояния успеха возвращается, если пакет успешно отправлена по-разному реализаций серверов.</span><span class="sxs-lookup"><span data-stu-id="77863-154">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="77863-155">Удаление пакета</span><span class="sxs-lookup"><span data-stu-id="77863-155">Delete a package</span></span>

<span data-ttu-id="77863-156">NuGet.org интерпретирует запроса на удаление пакета как объект «исключить».</span><span class="sxs-lookup"><span data-stu-id="77863-156">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="77863-157">Это означает, что пакет по-прежнему доступен для существующих потребителей пакета, но пакета больше не отображается в результатах поиска или веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="77863-157">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="77863-158">Дополнительные сведения об этом практическом см. в разделе [удалить пакеты](../policies/deleting-packages.md) политики.</span><span class="sxs-lookup"><span data-stu-id="77863-158">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="77863-159">Реализации других серверов могут интерпретировать этот сигнал как окончательного удаления, возможностью удаления или исключить.</span><span class="sxs-lookup"><span data-stu-id="77863-159">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="77863-160">Например [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (реализация сервера только поддержка более старых API V2) поддерживает обработка данного запроса в качестве unlist или окончательного удаления зависимости от параметра конфигурации.</span><span class="sxs-lookup"><span data-stu-id="77863-160">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="77863-161">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="77863-161">Request parameters</span></span>

<span data-ttu-id="77863-162">name</span><span class="sxs-lookup"><span data-stu-id="77863-162">Name</span></span>           | <span data-ttu-id="77863-163">Увеличение</span><span class="sxs-lookup"><span data-stu-id="77863-163">In</span></span>     | <span data-ttu-id="77863-164">Тип</span><span class="sxs-lookup"><span data-stu-id="77863-164">Type</span></span>   | <span data-ttu-id="77863-165">Обязательно</span><span class="sxs-lookup"><span data-stu-id="77863-165">Required</span></span> | <span data-ttu-id="77863-166">Примечания</span><span class="sxs-lookup"><span data-stu-id="77863-166">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="77863-167">ID</span><span class="sxs-lookup"><span data-stu-id="77863-167">ID</span></span>             | <span data-ttu-id="77863-168">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="77863-168">URL</span></span>    | <span data-ttu-id="77863-169">string</span><span class="sxs-lookup"><span data-stu-id="77863-169">string</span></span> | <span data-ttu-id="77863-170">да</span><span class="sxs-lookup"><span data-stu-id="77863-170">yes</span></span>      | <span data-ttu-id="77863-171">Идентификатор пакета для удаления</span><span class="sxs-lookup"><span data-stu-id="77863-171">The ID of the package to delete</span></span>
<span data-ttu-id="77863-172">VERSION</span><span class="sxs-lookup"><span data-stu-id="77863-172">VERSION</span></span>        | <span data-ttu-id="77863-173">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="77863-173">URL</span></span>    | <span data-ttu-id="77863-174">string</span><span class="sxs-lookup"><span data-stu-id="77863-174">string</span></span> | <span data-ttu-id="77863-175">да</span><span class="sxs-lookup"><span data-stu-id="77863-175">yes</span></span>      | <span data-ttu-id="77863-176">Версия пакета для удаления</span><span class="sxs-lookup"><span data-stu-id="77863-176">The version of the package to delete</span></span>
<span data-ttu-id="77863-177">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="77863-177">X-NuGet-ApiKey</span></span> | <span data-ttu-id="77863-178">Header</span><span class="sxs-lookup"><span data-stu-id="77863-178">Header</span></span> | <span data-ttu-id="77863-179">string</span><span class="sxs-lookup"><span data-stu-id="77863-179">string</span></span> | <span data-ttu-id="77863-180">да</span><span class="sxs-lookup"><span data-stu-id="77863-180">yes</span></span>      | <span data-ttu-id="77863-181">Например `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="77863-181">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="77863-182">Ответ</span><span class="sxs-lookup"><span data-stu-id="77863-182">Response</span></span>

<span data-ttu-id="77863-183">Код состояния</span><span class="sxs-lookup"><span data-stu-id="77863-183">Status Code</span></span> | <span data-ttu-id="77863-184">Значение</span><span class="sxs-lookup"><span data-stu-id="77863-184">Meaning</span></span>
----------- | -------
<span data-ttu-id="77863-185">204</span><span class="sxs-lookup"><span data-stu-id="77863-185">204</span></span>         | <span data-ttu-id="77863-186">Пакет был удален.</span><span class="sxs-lookup"><span data-stu-id="77863-186">The package was deleted</span></span>
<span data-ttu-id="77863-187">404</span><span class="sxs-lookup"><span data-stu-id="77863-187">404</span></span>         | <span data-ttu-id="77863-188">Без пакета с использованием указанного `ID` и `VERSION` существует</span><span class="sxs-lookup"><span data-stu-id="77863-188">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="77863-189">Relist пакета</span><span class="sxs-lookup"><span data-stu-id="77863-189">Relist a package</span></span>

<span data-ttu-id="77863-190">Если пакет, отсутствующие в списке, можно обеспечить еще раз отображается в результатах поиска, используя конечную точку «relist» этого пакета.</span><span class="sxs-lookup"><span data-stu-id="77863-190">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="77863-191">Эта конечная точка имеет так же, как [удалить (исключить) конечной точки](#delete-a-package) , но использует `POST` HTTP вместо метода `DELETE` метод.</span><span class="sxs-lookup"><span data-stu-id="77863-191">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="77863-192">Если пакет уже присутствует в списке, запрос по-прежнему выполняется успешно.</span><span class="sxs-lookup"><span data-stu-id="77863-192">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="77863-193">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="77863-193">Request parameters</span></span>

<span data-ttu-id="77863-194">name</span><span class="sxs-lookup"><span data-stu-id="77863-194">Name</span></span>           | <span data-ttu-id="77863-195">Увеличение</span><span class="sxs-lookup"><span data-stu-id="77863-195">In</span></span>     | <span data-ttu-id="77863-196">Тип</span><span class="sxs-lookup"><span data-stu-id="77863-196">Type</span></span>   | <span data-ttu-id="77863-197">Обязательно</span><span class="sxs-lookup"><span data-stu-id="77863-197">Required</span></span> | <span data-ttu-id="77863-198">Примечания</span><span class="sxs-lookup"><span data-stu-id="77863-198">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="77863-199">ID</span><span class="sxs-lookup"><span data-stu-id="77863-199">ID</span></span>             | <span data-ttu-id="77863-200">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="77863-200">URL</span></span>    | <span data-ttu-id="77863-201">string</span><span class="sxs-lookup"><span data-stu-id="77863-201">string</span></span> | <span data-ttu-id="77863-202">да</span><span class="sxs-lookup"><span data-stu-id="77863-202">yes</span></span>      | <span data-ttu-id="77863-203">Идентификатор пакета для relist</span><span class="sxs-lookup"><span data-stu-id="77863-203">The ID of the package to relist</span></span>
<span data-ttu-id="77863-204">VERSION</span><span class="sxs-lookup"><span data-stu-id="77863-204">VERSION</span></span>        | <span data-ttu-id="77863-205">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="77863-205">URL</span></span>    | <span data-ttu-id="77863-206">string</span><span class="sxs-lookup"><span data-stu-id="77863-206">string</span></span> | <span data-ttu-id="77863-207">да</span><span class="sxs-lookup"><span data-stu-id="77863-207">yes</span></span>      | <span data-ttu-id="77863-208">Версия пакета для relist</span><span class="sxs-lookup"><span data-stu-id="77863-208">The version of the package to relist</span></span>
<span data-ttu-id="77863-209">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="77863-209">X-NuGet-ApiKey</span></span> | <span data-ttu-id="77863-210">Header</span><span class="sxs-lookup"><span data-stu-id="77863-210">Header</span></span> | <span data-ttu-id="77863-211">string</span><span class="sxs-lookup"><span data-stu-id="77863-211">string</span></span> | <span data-ttu-id="77863-212">да</span><span class="sxs-lookup"><span data-stu-id="77863-212">yes</span></span>      | <span data-ttu-id="77863-213">Например `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="77863-213">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="77863-214">Ответ</span><span class="sxs-lookup"><span data-stu-id="77863-214">Response</span></span>

<span data-ttu-id="77863-215">Код состояния</span><span class="sxs-lookup"><span data-stu-id="77863-215">Status Code</span></span> | <span data-ttu-id="77863-216">Значение</span><span class="sxs-lookup"><span data-stu-id="77863-216">Meaning</span></span>
----------- | -------
<span data-ttu-id="77863-217">200</span><span class="sxs-lookup"><span data-stu-id="77863-217">200</span></span>         | <span data-ttu-id="77863-218">Пакет сейчас отобразится</span><span class="sxs-lookup"><span data-stu-id="77863-218">The package is now listed</span></span>
<span data-ttu-id="77863-219">404</span><span class="sxs-lookup"><span data-stu-id="77863-219">404</span></span>         | <span data-ttu-id="77863-220">Без пакета с использованием указанного `ID` и `VERSION` существует</span><span class="sxs-lookup"><span data-stu-id="77863-220">No package with the provided `ID` and `VERSION` exists</span></span>
