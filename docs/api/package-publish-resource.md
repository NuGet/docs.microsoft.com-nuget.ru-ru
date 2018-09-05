---
title: Принудительная отправка и удаление, API NuGet
description: Службы публикации позволяет клиентам публикации новых пакетов и удалить из списка или удалите существующие пакеты.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: ad66d8e0ffda13aaef744104c213863b0e111e0e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547525"
---
# <a name="push-and-delete"></a><span data-ttu-id="d1732-103">Принудительная отправка и удаление</span><span class="sxs-lookup"><span data-stu-id="d1732-103">Push and Delete</span></span>

<span data-ttu-id="d1732-104">Можно отправить, удалить (или удалить из списка, в зависимости от реализации сервера) и вернуть в список пакетов с помощью NuGet V3 API.</span><span class="sxs-lookup"><span data-stu-id="d1732-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="d1732-105">Эти операции расположенного за пределами класса `PackagePublish` найти ресурс в [индекс службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="d1732-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="d1732-106">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="d1732-106">Versioning</span></span>

<span data-ttu-id="d1732-107">Следующие `@type` используется значение:</span><span class="sxs-lookup"><span data-stu-id="d1732-107">The following `@type` value is used:</span></span>

<span data-ttu-id="d1732-108">Значение @type</span><span class="sxs-lookup"><span data-stu-id="d1732-108">@type value</span></span>          | <span data-ttu-id="d1732-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="d1732-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="d1732-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="d1732-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="d1732-111">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="d1732-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="d1732-112">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d1732-112">Base URL</span></span>

<span data-ttu-id="d1732-113">Базовый URL-адрес для следующих API-интерфейсов является значением `@id` свойство `PackagePublish/2.0.0` ресурсов в источнике пакета [индекс службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="d1732-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="d1732-114">В приведенной ниже документации используется URL-адреса для nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d1732-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="d1732-115">Рассмотрите возможность `https://www.nuget.org/api/v2/package` как заполнитель для `@id` значение найдено в индекс службы.</span><span class="sxs-lookup"><span data-stu-id="d1732-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="d1732-116">Обратите внимание на то, что этот URL-адрес указывает в том же расположении, как устаревшие принудительной конечных точек версии 2, поскольку протокол одинаковы.</span><span class="sxs-lookup"><span data-stu-id="d1732-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d1732-117">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="d1732-117">HTTP methods</span></span>

<span data-ttu-id="d1732-118">`PUT`, `POST` И `DELETE` поддерживаемых методов HTTP этот ресурс.</span><span class="sxs-lookup"><span data-stu-id="d1732-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="d1732-119">Какие методы поддерживаются на каждой конечной точки см. в разделе ниже.</span><span class="sxs-lookup"><span data-stu-id="d1732-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="d1732-120">Отправьте пакет</span><span class="sxs-lookup"><span data-stu-id="d1732-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="d1732-121">имеет NuGet.org [Дополнительные требования](NuGet-Protocols.md) для взаимодействия с конечной точкой Push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="d1732-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="d1732-122">NuGet.org поддерживает принудительную отправку новых пакетов, с помощью следующего API.</span><span class="sxs-lookup"><span data-stu-id="d1732-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="d1732-123">Если пакет с предоставленным Идентификатором и версией уже существует, nuget.org будет отклонять Push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="d1732-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="d1732-124">Другие источники пакета может поддерживать, заменив существующий пакет.</span><span class="sxs-lookup"><span data-stu-id="d1732-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="d1732-125">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="d1732-125">Request parameters</span></span>

<span data-ttu-id="d1732-126">name</span><span class="sxs-lookup"><span data-stu-id="d1732-126">Name</span></span>           | <span data-ttu-id="d1732-127">Увеличение</span><span class="sxs-lookup"><span data-stu-id="d1732-127">In</span></span>     | <span data-ttu-id="d1732-128">Тип</span><span class="sxs-lookup"><span data-stu-id="d1732-128">Type</span></span>   | <span data-ttu-id="d1732-129">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d1732-129">Required</span></span> | <span data-ttu-id="d1732-130">Примечания</span><span class="sxs-lookup"><span data-stu-id="d1732-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="d1732-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="d1732-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="d1732-132">Header</span><span class="sxs-lookup"><span data-stu-id="d1732-132">Header</span></span> | <span data-ttu-id="d1732-133">string</span><span class="sxs-lookup"><span data-stu-id="d1732-133">string</span></span> | <span data-ttu-id="d1732-134">да</span><span class="sxs-lookup"><span data-stu-id="d1732-134">yes</span></span>      | <span data-ttu-id="d1732-135">Например `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="d1732-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="d1732-136">Ключ API — непрозрачная строка получить из источника пакета пользователем и настроены в клиент.</span><span class="sxs-lookup"><span data-stu-id="d1732-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="d1732-137">Нет определенного формата строки является обязательной, но длина ключа API не должен превышать размер для значения заголовка HTTP.</span><span class="sxs-lookup"><span data-stu-id="d1732-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="d1732-138">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="d1732-138">Request body</span></span>

<span data-ttu-id="d1732-139">Текст запроса должна иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="d1732-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="d1732-140">Данных составной формы</span><span class="sxs-lookup"><span data-stu-id="d1732-140">Multipart form data</span></span>

<span data-ttu-id="d1732-141">Заголовок запроса `Content-Type` является `multipart/form-data` и первый элемент в тексте запроса — необработанные байты файла nupkg принудительно.</span><span class="sxs-lookup"><span data-stu-id="d1732-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="d1732-142">Последующих элементов составного текста учитываются.</span><span class="sxs-lookup"><span data-stu-id="d1732-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="d1732-143">Имя файла или любые другие заголовки составных элементов учитываются.</span><span class="sxs-lookup"><span data-stu-id="d1732-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="d1732-144">Ответ</span><span class="sxs-lookup"><span data-stu-id="d1732-144">Response</span></span>

<span data-ttu-id="d1732-145">Код состояния</span><span class="sxs-lookup"><span data-stu-id="d1732-145">Status Code</span></span> | <span data-ttu-id="d1732-146">Значение</span><span class="sxs-lookup"><span data-stu-id="d1732-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="d1732-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="d1732-147">201, 202</span></span>    | <span data-ttu-id="d1732-148">Пакет был успешно отправлен</span><span class="sxs-lookup"><span data-stu-id="d1732-148">The package was successfully pushed</span></span>
<span data-ttu-id="d1732-149">400</span><span class="sxs-lookup"><span data-stu-id="d1732-149">400</span></span>         | <span data-ttu-id="d1732-150">Предоставленный пакет является недопустимым</span><span class="sxs-lookup"><span data-stu-id="d1732-150">The provided package is invalid</span></span>
<span data-ttu-id="d1732-151">409</span><span class="sxs-lookup"><span data-stu-id="d1732-151">409</span></span>         | <span data-ttu-id="d1732-152">Пакет с предоставленным Идентификатором и версией уже существует</span><span class="sxs-lookup"><span data-stu-id="d1732-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="d1732-153">Реализации сервера зависят от код состояния успеха, возвращается, если пакет успешно отправлена.</span><span class="sxs-lookup"><span data-stu-id="d1732-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="d1732-154">Удаление пакета</span><span class="sxs-lookup"><span data-stu-id="d1732-154">Delete a package</span></span>

<span data-ttu-id="d1732-155">NuGet.org интерпретирует запроса на удаление пакета как значение «удалить из списка».</span><span class="sxs-lookup"><span data-stu-id="d1732-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="d1732-156">Это означает, что пакет будет по-прежнему доступен для существующих потребителей пакета, но пакет больше не отображается в результатах поиска или веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d1732-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="d1732-157">Дополнительные сведения о такой подход, см. в разделе [удалить пакеты](../policies/deleting-packages.md) политики.</span><span class="sxs-lookup"><span data-stu-id="d1732-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="d1732-158">Другие реализации серверов могут интерпретировать этот сигнал как окончательного удаления, обратимое удаление или удалить из списка.</span><span class="sxs-lookup"><span data-stu-id="d1732-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="d1732-159">Например [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (серверную реализацию только вспомогательные API более старые версии 2) поддерживает, обрабатывающего этот запрос как окончательного удаления зависимости от параметра конфигурации или удаления из списка.</span><span class="sxs-lookup"><span data-stu-id="d1732-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="d1732-160">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="d1732-160">Request parameters</span></span>

<span data-ttu-id="d1732-161">name</span><span class="sxs-lookup"><span data-stu-id="d1732-161">Name</span></span>           | <span data-ttu-id="d1732-162">Увеличение</span><span class="sxs-lookup"><span data-stu-id="d1732-162">In</span></span>     | <span data-ttu-id="d1732-163">Тип</span><span class="sxs-lookup"><span data-stu-id="d1732-163">Type</span></span>   | <span data-ttu-id="d1732-164">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d1732-164">Required</span></span> | <span data-ttu-id="d1732-165">Примечания</span><span class="sxs-lookup"><span data-stu-id="d1732-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="d1732-166">ID</span><span class="sxs-lookup"><span data-stu-id="d1732-166">ID</span></span>             | <span data-ttu-id="d1732-167">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d1732-167">URL</span></span>    | <span data-ttu-id="d1732-168">string</span><span class="sxs-lookup"><span data-stu-id="d1732-168">string</span></span> | <span data-ttu-id="d1732-169">да</span><span class="sxs-lookup"><span data-stu-id="d1732-169">yes</span></span>      | <span data-ttu-id="d1732-170">Идентификатор пакета для удаления</span><span class="sxs-lookup"><span data-stu-id="d1732-170">The ID of the package to delete</span></span>
<span data-ttu-id="d1732-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="d1732-171">VERSION</span></span>        | <span data-ttu-id="d1732-172">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d1732-172">URL</span></span>    | <span data-ttu-id="d1732-173">string</span><span class="sxs-lookup"><span data-stu-id="d1732-173">string</span></span> | <span data-ttu-id="d1732-174">да</span><span class="sxs-lookup"><span data-stu-id="d1732-174">yes</span></span>      | <span data-ttu-id="d1732-175">Версия пакета для удаления</span><span class="sxs-lookup"><span data-stu-id="d1732-175">The version of the package to delete</span></span>
<span data-ttu-id="d1732-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="d1732-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="d1732-177">Header</span><span class="sxs-lookup"><span data-stu-id="d1732-177">Header</span></span> | <span data-ttu-id="d1732-178">string</span><span class="sxs-lookup"><span data-stu-id="d1732-178">string</span></span> | <span data-ttu-id="d1732-179">да</span><span class="sxs-lookup"><span data-stu-id="d1732-179">yes</span></span>      | <span data-ttu-id="d1732-180">Например `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="d1732-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="d1732-181">Ответ</span><span class="sxs-lookup"><span data-stu-id="d1732-181">Response</span></span>

<span data-ttu-id="d1732-182">Код состояния</span><span class="sxs-lookup"><span data-stu-id="d1732-182">Status Code</span></span> | <span data-ttu-id="d1732-183">Значение</span><span class="sxs-lookup"><span data-stu-id="d1732-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="d1732-184">204</span><span class="sxs-lookup"><span data-stu-id="d1732-184">204</span></span>         | <span data-ttu-id="d1732-185">Пакет был удален</span><span class="sxs-lookup"><span data-stu-id="d1732-185">The package was deleted</span></span>
<span data-ttu-id="d1732-186">404</span><span class="sxs-lookup"><span data-stu-id="d1732-186">404</span></span>         | <span data-ttu-id="d1732-187">Нет пакета с предоставленным `ID` и `VERSION` существует</span><span class="sxs-lookup"><span data-stu-id="d1732-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="d1732-188">Вернуть в список пакета</span><span class="sxs-lookup"><span data-stu-id="d1732-188">Relist a package</span></span>

<span data-ttu-id="d1732-189">Если пакет будет удалена из списка, это можно делать этот пакет снова отображается в результатах поиска, используя конечную точку «вернуть в список».</span><span class="sxs-lookup"><span data-stu-id="d1732-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="d1732-190">Эта конечная точка поддерживает же форму, что [удалить (исключить) конечной точки](#delete-a-package) , но использует `POST` метод HTTP, а не `DELETE` метод.</span><span class="sxs-lookup"><span data-stu-id="d1732-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="d1732-191">Если пакет уже присутствует в списке, запрос по-прежнему выполняется успешно.</span><span class="sxs-lookup"><span data-stu-id="d1732-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="d1732-192">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="d1732-192">Request parameters</span></span>

<span data-ttu-id="d1732-193">name</span><span class="sxs-lookup"><span data-stu-id="d1732-193">Name</span></span>           | <span data-ttu-id="d1732-194">Увеличение</span><span class="sxs-lookup"><span data-stu-id="d1732-194">In</span></span>     | <span data-ttu-id="d1732-195">Тип</span><span class="sxs-lookup"><span data-stu-id="d1732-195">Type</span></span>   | <span data-ttu-id="d1732-196">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d1732-196">Required</span></span> | <span data-ttu-id="d1732-197">Примечания</span><span class="sxs-lookup"><span data-stu-id="d1732-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="d1732-198">ID</span><span class="sxs-lookup"><span data-stu-id="d1732-198">ID</span></span>             | <span data-ttu-id="d1732-199">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d1732-199">URL</span></span>    | <span data-ttu-id="d1732-200">string</span><span class="sxs-lookup"><span data-stu-id="d1732-200">string</span></span> | <span data-ttu-id="d1732-201">да</span><span class="sxs-lookup"><span data-stu-id="d1732-201">yes</span></span>      | <span data-ttu-id="d1732-202">Идентификатор пакета, чтобы вернуть в список</span><span class="sxs-lookup"><span data-stu-id="d1732-202">The ID of the package to relist</span></span>
<span data-ttu-id="d1732-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="d1732-203">VERSION</span></span>        | <span data-ttu-id="d1732-204">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d1732-204">URL</span></span>    | <span data-ttu-id="d1732-205">string</span><span class="sxs-lookup"><span data-stu-id="d1732-205">string</span></span> | <span data-ttu-id="d1732-206">да</span><span class="sxs-lookup"><span data-stu-id="d1732-206">yes</span></span>      | <span data-ttu-id="d1732-207">Версия пакета, чтобы вернуть в список</span><span class="sxs-lookup"><span data-stu-id="d1732-207">The version of the package to relist</span></span>
<span data-ttu-id="d1732-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="d1732-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="d1732-209">Header</span><span class="sxs-lookup"><span data-stu-id="d1732-209">Header</span></span> | <span data-ttu-id="d1732-210">string</span><span class="sxs-lookup"><span data-stu-id="d1732-210">string</span></span> | <span data-ttu-id="d1732-211">да</span><span class="sxs-lookup"><span data-stu-id="d1732-211">yes</span></span>      | <span data-ttu-id="d1732-212">Например `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="d1732-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="d1732-213">Ответ</span><span class="sxs-lookup"><span data-stu-id="d1732-213">Response</span></span>

<span data-ttu-id="d1732-214">Код состояния</span><span class="sxs-lookup"><span data-stu-id="d1732-214">Status Code</span></span> | <span data-ttu-id="d1732-215">Значение</span><span class="sxs-lookup"><span data-stu-id="d1732-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="d1732-216">200</span><span class="sxs-lookup"><span data-stu-id="d1732-216">200</span></span>         | <span data-ttu-id="d1732-217">Пакет сейчас отобразится</span><span class="sxs-lookup"><span data-stu-id="d1732-217">The package is now listed</span></span>
<span data-ttu-id="d1732-218">404</span><span class="sxs-lookup"><span data-stu-id="d1732-218">404</span></span>         | <span data-ttu-id="d1732-219">Нет пакета с предоставленным `ID` и `VERSION` существует</span><span class="sxs-lookup"><span data-stu-id="d1732-219">No package with the provided `ID` and `VERSION` exists</span></span>
