---
title: Отправка и удаление, API NuGet
description: Служба публикации позволяет клиентам публиковать новые пакеты и удалять существующие.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773917"
---
# <a name="push-and-delete"></a><span data-ttu-id="d884d-103">Принудительная отправка и удаление</span><span class="sxs-lookup"><span data-stu-id="d884d-103">Push and Delete</span></span>

<span data-ttu-id="d884d-104">Можно выполнить принудительную отправку, удаление (или вывод из списка) в зависимости от реализации сервера, а также перечислить пакеты с помощью API NuGet v3.</span><span class="sxs-lookup"><span data-stu-id="d884d-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="d884d-105">Эти операции основаны на `PackagePublish` ресурсе, найденном в [индексе службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="d884d-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="d884d-106">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="d884d-106">Versioning</span></span>

<span data-ttu-id="d884d-107">Используется следующее `@type` значение:</span><span class="sxs-lookup"><span data-stu-id="d884d-107">The following `@type` value is used:</span></span>

<span data-ttu-id="d884d-108">Значение @type</span><span class="sxs-lookup"><span data-stu-id="d884d-108">@type value</span></span>          | <span data-ttu-id="d884d-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="d884d-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="d884d-110">Паккажепублиш/2.0.0</span><span class="sxs-lookup"><span data-stu-id="d884d-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="d884d-111">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="d884d-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="d884d-112">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d884d-112">Base URL</span></span>

<span data-ttu-id="d884d-113">Базовый URL-адрес для следующих API-интерфейсов — это значение `@id` свойства `PackagePublish/2.0.0` ресурса в [индексе службы](service-index.md)источника пакета.</span><span class="sxs-lookup"><span data-stu-id="d884d-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="d884d-114">В приведенной ниже документации используется URL-адрес NuGet. org.</span><span class="sxs-lookup"><span data-stu-id="d884d-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="d884d-115">Рассмотрите в `https://www.nuget.org/api/v2/package` качестве заполнителя для `@id` значения, найденного в индексе службы.</span><span class="sxs-lookup"><span data-stu-id="d884d-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="d884d-116">Обратите внимание, что этот URL-адрес указывает на то же расположение, что и конечная точка Push предыдущей версии v2, так как этот протокол совпадает.</span><span class="sxs-lookup"><span data-stu-id="d884d-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d884d-117">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="d884d-117">HTTP methods</span></span>

<span data-ttu-id="d884d-118">В `PUT` `POST` `DELETE` этом ресурсе поддерживаются методы, и HTTP.</span><span class="sxs-lookup"><span data-stu-id="d884d-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="d884d-119">Сведения о том, какие методы поддерживаются в каждой конечной точке, см. ниже.</span><span class="sxs-lookup"><span data-stu-id="d884d-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="d884d-120">Отправка пакета</span><span class="sxs-lookup"><span data-stu-id="d884d-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="d884d-121">nuget.org имеет [Дополнительные требования](NuGet-Protocols.md) для взаимодействия с конечной точкой принудительной отправки.</span><span class="sxs-lookup"><span data-stu-id="d884d-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="d884d-122">nuget.org поддерживает принудительную отправку новых пакетов с помощью следующего API.</span><span class="sxs-lookup"><span data-stu-id="d884d-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="d884d-123">Если пакет с указанным ИДЕНТИФИКАТОРом и версией уже существует, nuget.org отклонит push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="d884d-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="d884d-124">Другие источники пакетов могут поддерживать замену существующего пакета.</span><span class="sxs-lookup"><span data-stu-id="d884d-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="d884d-125">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="d884d-125">Request parameters</span></span>

<span data-ttu-id="d884d-126">Имя</span><span class="sxs-lookup"><span data-stu-id="d884d-126">Name</span></span>           | <span data-ttu-id="d884d-127">В</span><span class="sxs-lookup"><span data-stu-id="d884d-127">In</span></span>     | <span data-ttu-id="d884d-128">Тип</span><span class="sxs-lookup"><span data-stu-id="d884d-128">Type</span></span>   | <span data-ttu-id="d884d-129">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d884d-129">Required</span></span> | <span data-ttu-id="d884d-130">Примечания</span><span class="sxs-lookup"><span data-stu-id="d884d-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="d884d-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="d884d-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="d884d-132">Header</span><span class="sxs-lookup"><span data-stu-id="d884d-132">Header</span></span> | <span data-ttu-id="d884d-133">строка</span><span class="sxs-lookup"><span data-stu-id="d884d-133">string</span></span> | <span data-ttu-id="d884d-134">yes</span><span class="sxs-lookup"><span data-stu-id="d884d-134">yes</span></span>      | <span data-ttu-id="d884d-135">Например: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="d884d-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="d884d-136">Ключ API — это непрозрачная строка, полученная пользователем из источника пакета и настроенная в клиенте.</span><span class="sxs-lookup"><span data-stu-id="d884d-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="d884d-137">Конкретный формат строки не задан, но длина ключа API не должна превышать приемлемый размер для значений заголовка HTTP.</span><span class="sxs-lookup"><span data-stu-id="d884d-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="d884d-138">Тело запроса</span><span class="sxs-lookup"><span data-stu-id="d884d-138">Request body</span></span>

<span data-ttu-id="d884d-139">Текст запроса должен быть в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="d884d-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="d884d-140">Составные данные форм</span><span class="sxs-lookup"><span data-stu-id="d884d-140">Multipart form data</span></span>

<span data-ttu-id="d884d-141">Заголовок запроса `Content-Type` — `multipart/form-data` , а первый элемент в тексте запроса — это необработанные байты nupkg.</span><span class="sxs-lookup"><span data-stu-id="d884d-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="d884d-142">Последующие элементы в составном тексте не учитываются.</span><span class="sxs-lookup"><span data-stu-id="d884d-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="d884d-143">Имя файла или любые другие заголовки составных элементов игнорируются.</span><span class="sxs-lookup"><span data-stu-id="d884d-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="d884d-144">Ответ</span><span class="sxs-lookup"><span data-stu-id="d884d-144">Response</span></span>

<span data-ttu-id="d884d-145">Код состояния</span><span class="sxs-lookup"><span data-stu-id="d884d-145">Status Code</span></span> | <span data-ttu-id="d884d-146">Значение</span><span class="sxs-lookup"><span data-stu-id="d884d-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="d884d-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="d884d-147">201, 202</span></span>    | <span data-ttu-id="d884d-148">Пакет успешно отправлен</span><span class="sxs-lookup"><span data-stu-id="d884d-148">The package was successfully pushed</span></span>
<span data-ttu-id="d884d-149">400</span><span class="sxs-lookup"><span data-stu-id="d884d-149">400</span></span>         | <span data-ttu-id="d884d-150">Указан недопустимый пакет</span><span class="sxs-lookup"><span data-stu-id="d884d-150">The provided package is invalid</span></span>
<span data-ttu-id="d884d-151">409</span><span class="sxs-lookup"><span data-stu-id="d884d-151">409</span></span>         | <span data-ttu-id="d884d-152">Пакет с указанным ИДЕНТИФИКАТОРом и версией уже существует</span><span class="sxs-lookup"><span data-stu-id="d884d-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="d884d-153">Серверные реализации зависят от кода состояния успеха, возвращаемого при успешной отправке пакета.</span><span class="sxs-lookup"><span data-stu-id="d884d-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="d884d-154">Удаление пакета</span><span class="sxs-lookup"><span data-stu-id="d884d-154">Delete a package</span></span>

<span data-ttu-id="d884d-155">nuget.org интерпретирует запрос на удаление пакета как "unlist".</span><span class="sxs-lookup"><span data-stu-id="d884d-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="d884d-156">Это означает, что пакет по-прежнему доступен для существующих потребителей пакета, но пакет больше не отображается в результатах поиска или в веб-интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="d884d-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="d884d-157">Дополнительные сведения об этом практическом занятии см. в разделе Политика [удаленных пакетов](../nuget-org/policies/deleting-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="d884d-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="d884d-158">Другие серверные реализации могут интерпретировать этот сигнал как жесткое удаление, обратимое удаление или удалить из списка.</span><span class="sxs-lookup"><span data-stu-id="d884d-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="d884d-159">Например, [NuGet. Server](https://www.nuget.org/packages/NuGet.Server) (Серверная реализация, поддерживающая более старый API версии 2) поддерживает обработку этого запроса в виде несписка или жесткого удаления на основе параметра конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d884d-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="d884d-160">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="d884d-160">Request parameters</span></span>

<span data-ttu-id="d884d-161">Имя</span><span class="sxs-lookup"><span data-stu-id="d884d-161">Name</span></span>           | <span data-ttu-id="d884d-162">В</span><span class="sxs-lookup"><span data-stu-id="d884d-162">In</span></span>     | <span data-ttu-id="d884d-163">Тип</span><span class="sxs-lookup"><span data-stu-id="d884d-163">Type</span></span>   | <span data-ttu-id="d884d-164">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d884d-164">Required</span></span> | <span data-ttu-id="d884d-165">Примечания</span><span class="sxs-lookup"><span data-stu-id="d884d-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="d884d-166">ID</span><span class="sxs-lookup"><span data-stu-id="d884d-166">ID</span></span>             | <span data-ttu-id="d884d-167">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d884d-167">URL</span></span>    | <span data-ttu-id="d884d-168">строка</span><span class="sxs-lookup"><span data-stu-id="d884d-168">string</span></span> | <span data-ttu-id="d884d-169">yes</span><span class="sxs-lookup"><span data-stu-id="d884d-169">yes</span></span>      | <span data-ttu-id="d884d-170">Идентификатор удаляемого пакета</span><span class="sxs-lookup"><span data-stu-id="d884d-170">The ID of the package to delete</span></span>
<span data-ttu-id="d884d-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="d884d-171">VERSION</span></span>        | <span data-ttu-id="d884d-172">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d884d-172">URL</span></span>    | <span data-ttu-id="d884d-173">строка</span><span class="sxs-lookup"><span data-stu-id="d884d-173">string</span></span> | <span data-ttu-id="d884d-174">yes</span><span class="sxs-lookup"><span data-stu-id="d884d-174">yes</span></span>      | <span data-ttu-id="d884d-175">Версия удаляемого пакета</span><span class="sxs-lookup"><span data-stu-id="d884d-175">The version of the package to delete</span></span>
<span data-ttu-id="d884d-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="d884d-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="d884d-177">Header</span><span class="sxs-lookup"><span data-stu-id="d884d-177">Header</span></span> | <span data-ttu-id="d884d-178">строка</span><span class="sxs-lookup"><span data-stu-id="d884d-178">string</span></span> | <span data-ttu-id="d884d-179">yes</span><span class="sxs-lookup"><span data-stu-id="d884d-179">yes</span></span>      | <span data-ttu-id="d884d-180">Например: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="d884d-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="d884d-181">Ответ</span><span class="sxs-lookup"><span data-stu-id="d884d-181">Response</span></span>

<span data-ttu-id="d884d-182">Код состояния</span><span class="sxs-lookup"><span data-stu-id="d884d-182">Status Code</span></span> | <span data-ttu-id="d884d-183">Значение</span><span class="sxs-lookup"><span data-stu-id="d884d-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="d884d-184">204</span><span class="sxs-lookup"><span data-stu-id="d884d-184">204</span></span>         | <span data-ttu-id="d884d-185">Пакет был удален</span><span class="sxs-lookup"><span data-stu-id="d884d-185">The package was deleted</span></span>
<span data-ttu-id="d884d-186">404</span><span class="sxs-lookup"><span data-stu-id="d884d-186">404</span></span>         | <span data-ttu-id="d884d-187">Нет пакета с указанным `ID` и не `VERSION` существует</span><span class="sxs-lookup"><span data-stu-id="d884d-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="d884d-188">Повторное перечисление пакета</span><span class="sxs-lookup"><span data-stu-id="d884d-188">Relist a package</span></span>

<span data-ttu-id="d884d-189">Если пакет не включен в список, можно сделать этот пакет снова видимым в результатах поиска, используя конечную точку "перечисление".</span><span class="sxs-lookup"><span data-stu-id="d884d-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="d884d-190">Эта конечная точка имеет ту же форму, что и [Конечная точка Delete (удалить из списка)](#delete-a-package) , но использует `POST` метод HTTP вместо `DELETE` метода.</span><span class="sxs-lookup"><span data-stu-id="d884d-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="d884d-191">Если пакет уже указан, запрос все равно будет выполнен.</span><span class="sxs-lookup"><span data-stu-id="d884d-191">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="d884d-192">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="d884d-192">Request parameters</span></span>

<span data-ttu-id="d884d-193">Имя</span><span class="sxs-lookup"><span data-stu-id="d884d-193">Name</span></span>           | <span data-ttu-id="d884d-194">В</span><span class="sxs-lookup"><span data-stu-id="d884d-194">In</span></span>     | <span data-ttu-id="d884d-195">Тип</span><span class="sxs-lookup"><span data-stu-id="d884d-195">Type</span></span>   | <span data-ttu-id="d884d-196">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d884d-196">Required</span></span> | <span data-ttu-id="d884d-197">Примечания</span><span class="sxs-lookup"><span data-stu-id="d884d-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="d884d-198">ID</span><span class="sxs-lookup"><span data-stu-id="d884d-198">ID</span></span>             | <span data-ttu-id="d884d-199">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d884d-199">URL</span></span>    | <span data-ttu-id="d884d-200">строка</span><span class="sxs-lookup"><span data-stu-id="d884d-200">string</span></span> | <span data-ttu-id="d884d-201">yes</span><span class="sxs-lookup"><span data-stu-id="d884d-201">yes</span></span>      | <span data-ttu-id="d884d-202">Идентификатор пакета для повторного перечисления</span><span class="sxs-lookup"><span data-stu-id="d884d-202">The ID of the package to relist</span></span>
<span data-ttu-id="d884d-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="d884d-203">VERSION</span></span>        | <span data-ttu-id="d884d-204">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d884d-204">URL</span></span>    | <span data-ttu-id="d884d-205">строка</span><span class="sxs-lookup"><span data-stu-id="d884d-205">string</span></span> | <span data-ttu-id="d884d-206">yes</span><span class="sxs-lookup"><span data-stu-id="d884d-206">yes</span></span>      | <span data-ttu-id="d884d-207">Версия пакета для повторного перечисления</span><span class="sxs-lookup"><span data-stu-id="d884d-207">The version of the package to relist</span></span>
<span data-ttu-id="d884d-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="d884d-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="d884d-209">Header</span><span class="sxs-lookup"><span data-stu-id="d884d-209">Header</span></span> | <span data-ttu-id="d884d-210">строка</span><span class="sxs-lookup"><span data-stu-id="d884d-210">string</span></span> | <span data-ttu-id="d884d-211">yes</span><span class="sxs-lookup"><span data-stu-id="d884d-211">yes</span></span>      | <span data-ttu-id="d884d-212">Например: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="d884d-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="d884d-213">Ответ</span><span class="sxs-lookup"><span data-stu-id="d884d-213">Response</span></span>

<span data-ttu-id="d884d-214">Код состояния</span><span class="sxs-lookup"><span data-stu-id="d884d-214">Status Code</span></span> | <span data-ttu-id="d884d-215">Значение</span><span class="sxs-lookup"><span data-stu-id="d884d-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="d884d-216">200</span><span class="sxs-lookup"><span data-stu-id="d884d-216">200</span></span>         | <span data-ttu-id="d884d-217">Пакет теперь указан</span><span class="sxs-lookup"><span data-stu-id="d884d-217">The package is now listed</span></span>
<span data-ttu-id="d884d-218">404</span><span class="sxs-lookup"><span data-stu-id="d884d-218">404</span></span>         | <span data-ttu-id="d884d-219">Нет пакета с указанным `ID` и не `VERSION` существует</span><span class="sxs-lookup"><span data-stu-id="d884d-219">No package with the provided `ID` and `VERSION` exists</span></span>
