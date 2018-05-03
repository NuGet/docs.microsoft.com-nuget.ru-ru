---
title: Принудительные и удалить NuGet интерфейса API
description: Служба публикации позволяет клиентам публикации новых пакетов и исключить или удалите существующие пакеты.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 911c8238624f806b1fbb5c7938d02b6bdfbd8614
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="29ada-103">Принудительные и удалить</span><span class="sxs-lookup"><span data-stu-id="29ada-103">Push and Delete</span></span>

<span data-ttu-id="29ada-104">Существует возможность push, удалить (или исключить, в зависимости от реализации сервера) и relist пакетов с помощью NuGet V3 API.</span><span class="sxs-lookup"><span data-stu-id="29ada-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="29ada-105">Эти операции расположенного за пределами `PackagePublish` найти ресурс в [служба индекс](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="29ada-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="29ada-106">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="29ada-106">Versioning</span></span>

<span data-ttu-id="29ada-107">Следующие `@type` используется значение:</span><span class="sxs-lookup"><span data-stu-id="29ada-107">The following `@type` value is used:</span></span>

<span data-ttu-id="29ada-108">Значение @type</span><span class="sxs-lookup"><span data-stu-id="29ada-108">@type value</span></span>          | <span data-ttu-id="29ada-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="29ada-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="29ada-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="29ada-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="29ada-111">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="29ada-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="29ada-112">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="29ada-112">Base URL</span></span>

<span data-ttu-id="29ada-113">Базовый URL-адрес для следующих API-интерфейсов — это значение `@id` свойство `PackagePublish/2.0.0` ресурсов в источнике пакетов [служба индекс](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="29ada-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="29ada-114">В следующих документах используется nuget.org URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="29ada-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="29ada-115">Рассмотрим `https://www.nuget.org/api/v2/package` как заполнитель для `@id` значение найдено в индексе службы.</span><span class="sxs-lookup"><span data-stu-id="29ada-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="29ada-116">Обратите внимание, на который этот URL-адрес указывает же расположении, что конечная точка устаревших V2 push, так как использует тот же протокол.</span><span class="sxs-lookup"><span data-stu-id="29ada-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="29ada-117">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="29ada-117">HTTP methods</span></span>

<span data-ttu-id="29ada-118">`PUT`, `POST` И `DELETE` этот ресурс поддерживаемых методов HTTP.</span><span class="sxs-lookup"><span data-stu-id="29ada-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="29ada-119">Какие методы поддерживаются для каждой конечной точки см. ниже.</span><span class="sxs-lookup"><span data-stu-id="29ada-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="29ada-120">Пакет Push</span><span class="sxs-lookup"><span data-stu-id="29ada-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="29ada-121">имеет NuGet.org [Дополнительные требования](NuGet-Protocols.md) для взаимодействия с конечной точкой push.</span><span class="sxs-lookup"><span data-stu-id="29ada-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="29ada-122">NuGet.org поддерживает принудительную отправку новых пакетов с помощью следующих API.</span><span class="sxs-lookup"><span data-stu-id="29ada-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="29ada-123">Если пакет с предоставленным Идентификатором и версией уже существует, nuget.org отклонит принудительной отправки.</span><span class="sxs-lookup"><span data-stu-id="29ada-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="29ada-124">Другие источники пакетов могут поддерживать замены существующего пакета.</span><span class="sxs-lookup"><span data-stu-id="29ada-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="29ada-125">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="29ada-125">Request parameters</span></span>

<span data-ttu-id="29ada-126">name</span><span class="sxs-lookup"><span data-stu-id="29ada-126">Name</span></span>           | <span data-ttu-id="29ada-127">Увеличение</span><span class="sxs-lookup"><span data-stu-id="29ada-127">In</span></span>     | <span data-ttu-id="29ada-128">Тип</span><span class="sxs-lookup"><span data-stu-id="29ada-128">Type</span></span>   | <span data-ttu-id="29ada-129">Обязательно</span><span class="sxs-lookup"><span data-stu-id="29ada-129">Required</span></span> | <span data-ttu-id="29ada-130">Примечания</span><span class="sxs-lookup"><span data-stu-id="29ada-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="29ada-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="29ada-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="29ada-132">Header</span><span class="sxs-lookup"><span data-stu-id="29ada-132">Header</span></span> | <span data-ttu-id="29ada-133">string</span><span class="sxs-lookup"><span data-stu-id="29ada-133">string</span></span> | <span data-ttu-id="29ada-134">да</span><span class="sxs-lookup"><span data-stu-id="29ada-134">yes</span></span>      | <span data-ttu-id="29ada-135">Например `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="29ada-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="29ada-136">Ключ API — непрозрачная строка получения из источника пакета пользователем и настроены в клиент.</span><span class="sxs-lookup"><span data-stu-id="29ada-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="29ada-137">Формат строки не является обязательной, но длина ключа API не должно превышать разумный размер для значения заголовка HTTP.</span><span class="sxs-lookup"><span data-stu-id="29ada-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="29ada-138">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="29ada-138">Request body</span></span>

<span data-ttu-id="29ada-139">Текст запроса должен указываться в следующей форме:</span><span class="sxs-lookup"><span data-stu-id="29ada-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="29ada-140">Данных составной формы</span><span class="sxs-lookup"><span data-stu-id="29ada-140">Multipart form data</span></span>

<span data-ttu-id="29ada-141">Заголовок запроса `Content-Type` — `multipart/form-data` и необработанные байты .nupkg нажимают является первый элемент в тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="29ada-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="29ada-142">Последующих элементов составного текста учитываются.</span><span class="sxs-lookup"><span data-stu-id="29ada-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="29ada-143">Имя файла или другие заголовки составных элементов учитываются.</span><span class="sxs-lookup"><span data-stu-id="29ada-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="29ada-144">Ответ</span><span class="sxs-lookup"><span data-stu-id="29ada-144">Response</span></span>

<span data-ttu-id="29ada-145">Код состояния</span><span class="sxs-lookup"><span data-stu-id="29ada-145">Status Code</span></span> | <span data-ttu-id="29ada-146">Значение</span><span class="sxs-lookup"><span data-stu-id="29ada-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="29ada-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="29ada-147">201, 202</span></span>    | <span data-ttu-id="29ada-148">Пакет был успешно отправлен</span><span class="sxs-lookup"><span data-stu-id="29ada-148">The package was successfully pushed</span></span>
<span data-ttu-id="29ada-149">400</span><span class="sxs-lookup"><span data-stu-id="29ada-149">400</span></span>         | <span data-ttu-id="29ada-150">Предоставленный пакет является недопустимым</span><span class="sxs-lookup"><span data-stu-id="29ada-150">The provided package is invalid</span></span>
<span data-ttu-id="29ada-151">409</span><span class="sxs-lookup"><span data-stu-id="29ada-151">409</span></span>         | <span data-ttu-id="29ada-152">Пакет с предоставленным Идентификатором и версией уже существует</span><span class="sxs-lookup"><span data-stu-id="29ada-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="29ada-153">Код состояния успеха возвращается, если пакет успешно отправлена по-разному реализаций серверов.</span><span class="sxs-lookup"><span data-stu-id="29ada-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="29ada-154">Удаление пакета</span><span class="sxs-lookup"><span data-stu-id="29ada-154">Delete a package</span></span>

<span data-ttu-id="29ada-155">NuGet.org интерпретирует запроса на удаление пакета как объект «исключить».</span><span class="sxs-lookup"><span data-stu-id="29ada-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="29ada-156">Это означает, что пакет по-прежнему доступен для существующих потребителей пакета, но пакета больше не отображается в результатах поиска или веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="29ada-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="29ada-157">Дополнительные сведения об этом практическом см. в разделе [удалить пакеты](../policies/deleting-packages.md) политики.</span><span class="sxs-lookup"><span data-stu-id="29ada-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="29ada-158">Реализации других серверов могут интерпретировать этот сигнал как окончательного удаления, возможностью удаления или исключить.</span><span class="sxs-lookup"><span data-stu-id="29ada-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="29ada-159">Например [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (реализация сервера только поддержка более старых API V2) поддерживает обработка данного запроса в качестве unlist или окончательного удаления зависимости от параметра конфигурации.</span><span class="sxs-lookup"><span data-stu-id="29ada-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="29ada-160">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="29ada-160">Request parameters</span></span>

<span data-ttu-id="29ada-161">name</span><span class="sxs-lookup"><span data-stu-id="29ada-161">Name</span></span>           | <span data-ttu-id="29ada-162">Увеличение</span><span class="sxs-lookup"><span data-stu-id="29ada-162">In</span></span>     | <span data-ttu-id="29ada-163">Тип</span><span class="sxs-lookup"><span data-stu-id="29ada-163">Type</span></span>   | <span data-ttu-id="29ada-164">Обязательно</span><span class="sxs-lookup"><span data-stu-id="29ada-164">Required</span></span> | <span data-ttu-id="29ada-165">Примечания</span><span class="sxs-lookup"><span data-stu-id="29ada-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="29ada-166">ID</span><span class="sxs-lookup"><span data-stu-id="29ada-166">ID</span></span>             | <span data-ttu-id="29ada-167">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="29ada-167">URL</span></span>    | <span data-ttu-id="29ada-168">string</span><span class="sxs-lookup"><span data-stu-id="29ada-168">string</span></span> | <span data-ttu-id="29ada-169">да</span><span class="sxs-lookup"><span data-stu-id="29ada-169">yes</span></span>      | <span data-ttu-id="29ada-170">Идентификатор пакета для удаления</span><span class="sxs-lookup"><span data-stu-id="29ada-170">The ID of the package to delete</span></span>
<span data-ttu-id="29ada-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="29ada-171">VERSION</span></span>        | <span data-ttu-id="29ada-172">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="29ada-172">URL</span></span>    | <span data-ttu-id="29ada-173">string</span><span class="sxs-lookup"><span data-stu-id="29ada-173">string</span></span> | <span data-ttu-id="29ada-174">да</span><span class="sxs-lookup"><span data-stu-id="29ada-174">yes</span></span>      | <span data-ttu-id="29ada-175">Версия пакета для удаления</span><span class="sxs-lookup"><span data-stu-id="29ada-175">The version of the package to delete</span></span>
<span data-ttu-id="29ada-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="29ada-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="29ada-177">Header</span><span class="sxs-lookup"><span data-stu-id="29ada-177">Header</span></span> | <span data-ttu-id="29ada-178">string</span><span class="sxs-lookup"><span data-stu-id="29ada-178">string</span></span> | <span data-ttu-id="29ada-179">да</span><span class="sxs-lookup"><span data-stu-id="29ada-179">yes</span></span>      | <span data-ttu-id="29ada-180">Например `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="29ada-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="29ada-181">Ответ</span><span class="sxs-lookup"><span data-stu-id="29ada-181">Response</span></span>

<span data-ttu-id="29ada-182">Код состояния</span><span class="sxs-lookup"><span data-stu-id="29ada-182">Status Code</span></span> | <span data-ttu-id="29ada-183">Значение</span><span class="sxs-lookup"><span data-stu-id="29ada-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="29ada-184">204</span><span class="sxs-lookup"><span data-stu-id="29ada-184">204</span></span>         | <span data-ttu-id="29ada-185">Пакет был удален.</span><span class="sxs-lookup"><span data-stu-id="29ada-185">The package was deleted</span></span>
<span data-ttu-id="29ada-186">404</span><span class="sxs-lookup"><span data-stu-id="29ada-186">404</span></span>         | <span data-ttu-id="29ada-187">Без пакета с использованием указанного `ID` и `VERSION` существует</span><span class="sxs-lookup"><span data-stu-id="29ada-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="29ada-188">Relist пакета</span><span class="sxs-lookup"><span data-stu-id="29ada-188">Relist a package</span></span>

<span data-ttu-id="29ada-189">Если пакет, отсутствующие в списке, можно обеспечить еще раз отображается в результатах поиска, используя конечную точку «relist» этого пакета.</span><span class="sxs-lookup"><span data-stu-id="29ada-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="29ada-190">Эта конечная точка имеет так же, как [удалить (исключить) конечной точки](#delete-a-package) , но использует `POST` HTTP вместо метода `DELETE` метод.</span><span class="sxs-lookup"><span data-stu-id="29ada-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="29ada-191">Если пакет уже присутствует в списке, запрос по-прежнему выполняется успешно.</span><span class="sxs-lookup"><span data-stu-id="29ada-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="29ada-192">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="29ada-192">Request parameters</span></span>

<span data-ttu-id="29ada-193">name</span><span class="sxs-lookup"><span data-stu-id="29ada-193">Name</span></span>           | <span data-ttu-id="29ada-194">Увеличение</span><span class="sxs-lookup"><span data-stu-id="29ada-194">In</span></span>     | <span data-ttu-id="29ada-195">Тип</span><span class="sxs-lookup"><span data-stu-id="29ada-195">Type</span></span>   | <span data-ttu-id="29ada-196">Обязательно</span><span class="sxs-lookup"><span data-stu-id="29ada-196">Required</span></span> | <span data-ttu-id="29ada-197">Примечания</span><span class="sxs-lookup"><span data-stu-id="29ada-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="29ada-198">ID</span><span class="sxs-lookup"><span data-stu-id="29ada-198">ID</span></span>             | <span data-ttu-id="29ada-199">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="29ada-199">URL</span></span>    | <span data-ttu-id="29ada-200">string</span><span class="sxs-lookup"><span data-stu-id="29ada-200">string</span></span> | <span data-ttu-id="29ada-201">да</span><span class="sxs-lookup"><span data-stu-id="29ada-201">yes</span></span>      | <span data-ttu-id="29ada-202">Идентификатор пакета для relist</span><span class="sxs-lookup"><span data-stu-id="29ada-202">The ID of the package to relist</span></span>
<span data-ttu-id="29ada-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="29ada-203">VERSION</span></span>        | <span data-ttu-id="29ada-204">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="29ada-204">URL</span></span>    | <span data-ttu-id="29ada-205">string</span><span class="sxs-lookup"><span data-stu-id="29ada-205">string</span></span> | <span data-ttu-id="29ada-206">да</span><span class="sxs-lookup"><span data-stu-id="29ada-206">yes</span></span>      | <span data-ttu-id="29ada-207">Версия пакета для relist</span><span class="sxs-lookup"><span data-stu-id="29ada-207">The version of the package to relist</span></span>
<span data-ttu-id="29ada-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="29ada-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="29ada-209">Header</span><span class="sxs-lookup"><span data-stu-id="29ada-209">Header</span></span> | <span data-ttu-id="29ada-210">string</span><span class="sxs-lookup"><span data-stu-id="29ada-210">string</span></span> | <span data-ttu-id="29ada-211">да</span><span class="sxs-lookup"><span data-stu-id="29ada-211">yes</span></span>      | <span data-ttu-id="29ada-212">Например `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="29ada-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="29ada-213">Ответ</span><span class="sxs-lookup"><span data-stu-id="29ada-213">Response</span></span>

<span data-ttu-id="29ada-214">Код состояния</span><span class="sxs-lookup"><span data-stu-id="29ada-214">Status Code</span></span> | <span data-ttu-id="29ada-215">Значение</span><span class="sxs-lookup"><span data-stu-id="29ada-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="29ada-216">200</span><span class="sxs-lookup"><span data-stu-id="29ada-216">200</span></span>         | <span data-ttu-id="29ada-217">Пакет сейчас отобразится</span><span class="sxs-lookup"><span data-stu-id="29ada-217">The package is now listed</span></span>
<span data-ttu-id="29ada-218">404</span><span class="sxs-lookup"><span data-stu-id="29ada-218">404</span></span>         | <span data-ttu-id="29ada-219">Без пакета с использованием указанного `ID` и `VERSION` существует</span><span class="sxs-lookup"><span data-stu-id="29ada-219">No package with the provided `ID` and `VERSION` exists</span></span>
