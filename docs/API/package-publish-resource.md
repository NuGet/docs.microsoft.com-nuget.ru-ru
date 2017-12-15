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
ms.openlocfilehash: 1fa3c0e1698a11208d9ef29fdf26a4980cb60cf5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="push-and-delete"></a><span data-ttu-id="bc05e-104">Принудительные и удалить</span><span class="sxs-lookup"><span data-stu-id="bc05e-104">Push and Delete</span></span>

<span data-ttu-id="bc05e-105">Это возможно, push и удалять (или исключить, в зависимости от реализации сервера) пакетов с помощью NuGet V3 API.</span><span class="sxs-lookup"><span data-stu-id="bc05e-105">It is possible to push and delete (or unlist, depending on the server implementation) packages using the NuGet V3 API.</span></span>
<span data-ttu-id="bc05e-106">Обе операции расположенного за пределами `PackagePublish` найти ресурс в [служба индекс](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="bc05e-106">Both operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="bc05e-107">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="bc05e-107">Versioning</span></span>

<span data-ttu-id="bc05e-108">Следующие `@type` используется значение:</span><span class="sxs-lookup"><span data-stu-id="bc05e-108">The following `@type` value is used:</span></span>

<span data-ttu-id="bc05e-109">Значение @type</span><span class="sxs-lookup"><span data-stu-id="bc05e-109">@type value</span></span>          | <span data-ttu-id="bc05e-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="bc05e-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="bc05e-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="bc05e-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="bc05e-112">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="bc05e-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="bc05e-113">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="bc05e-113">Base URL</span></span>

<span data-ttu-id="bc05e-114">Базовый URL-адрес для следующих API-интерфейсов — это значение `@id` свойство `PackagePublish/2.0.0` ресурсов в источнике пакетов [служба индекс](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="bc05e-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="bc05e-115">В следующих документах используется nuget.org URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="bc05e-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="bc05e-116">Рассмотрим `https://www.nuget.org/api/v2/package` как заполнитель для `@id` значение найдено в индексе службы.</span><span class="sxs-lookup"><span data-stu-id="bc05e-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="bc05e-117">Обратите внимание, на который этот URL-адрес указывает же расположении, что конечная точка устаревших V2 push, так как использует тот же протокол.</span><span class="sxs-lookup"><span data-stu-id="bc05e-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="bc05e-118">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="bc05e-118">HTTP methods</span></span>

<span data-ttu-id="bc05e-119">`PUT` И `DELETE` этот ресурс поддерживаемых методов HTTP.</span><span class="sxs-lookup"><span data-stu-id="bc05e-119">The `PUT` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="bc05e-120">Какие методы поддерживаются для каждой конечной точки см. ниже.</span><span class="sxs-lookup"><span data-stu-id="bc05e-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="bc05e-121">Пакет Push</span><span class="sxs-lookup"><span data-stu-id="bc05e-121">Push a package</span></span>

<span data-ttu-id="bc05e-122">NuGet.org поддерживает принудительную отправку новых пакетов с помощью следующих API.</span><span class="sxs-lookup"><span data-stu-id="bc05e-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="bc05e-123">Если пакет с предоставленным Идентификатором и версией уже существует, nuget.org отклонит принудительной отправки.</span><span class="sxs-lookup"><span data-stu-id="bc05e-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="bc05e-124">Другие источники пакетов могут поддерживать замены существующего пакета.</span><span class="sxs-lookup"><span data-stu-id="bc05e-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="bc05e-125">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="bc05e-125">Request parameters</span></span>

<span data-ttu-id="bc05e-126">Имя</span><span class="sxs-lookup"><span data-stu-id="bc05e-126">Name</span></span>           | <span data-ttu-id="bc05e-127">Увеличение</span><span class="sxs-lookup"><span data-stu-id="bc05e-127">In</span></span>     | <span data-ttu-id="bc05e-128">Тип</span><span class="sxs-lookup"><span data-stu-id="bc05e-128">Type</span></span>   | <span data-ttu-id="bc05e-129">Обязательно</span><span class="sxs-lookup"><span data-stu-id="bc05e-129">Required</span></span> | <span data-ttu-id="bc05e-130">Примечания</span><span class="sxs-lookup"><span data-stu-id="bc05e-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="bc05e-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="bc05e-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="bc05e-132">Header</span><span class="sxs-lookup"><span data-stu-id="bc05e-132">Header</span></span> | <span data-ttu-id="bc05e-133">string</span><span class="sxs-lookup"><span data-stu-id="bc05e-133">string</span></span> | <span data-ttu-id="bc05e-134">да</span><span class="sxs-lookup"><span data-stu-id="bc05e-134">yes</span></span>      | <span data-ttu-id="bc05e-135">Например `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="bc05e-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="bc05e-136">Ключ API — непрозрачная строка получения из источника пакета пользователем и настроены в клиент.</span><span class="sxs-lookup"><span data-stu-id="bc05e-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="bc05e-137">Формат строки не является обязательной, но длина ключа API не должно превышать разумный размер для значения заголовка HTTP.</span><span class="sxs-lookup"><span data-stu-id="bc05e-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="bc05e-138">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="bc05e-138">Request body</span></span>

<span data-ttu-id="bc05e-139">Текст запроса должен указываться в следующей форме:</span><span class="sxs-lookup"><span data-stu-id="bc05e-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="bc05e-140">Данных составной формы</span><span class="sxs-lookup"><span data-stu-id="bc05e-140">Multipart form data</span></span>

<span data-ttu-id="bc05e-141">Заголовок запроса `Content-Type` — `multipart/form-data` и необработанные байты .nupkg нажимают является первый элемент в тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="bc05e-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="bc05e-142">Последующих элементов составного текста учитываются.</span><span class="sxs-lookup"><span data-stu-id="bc05e-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="bc05e-143">Имя файла или другие заголовки составных элементов учитываются.</span><span class="sxs-lookup"><span data-stu-id="bc05e-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="bc05e-144">Ответ</span><span class="sxs-lookup"><span data-stu-id="bc05e-144">Response</span></span>

<span data-ttu-id="bc05e-145">Код состояния</span><span class="sxs-lookup"><span data-stu-id="bc05e-145">Status Code</span></span> | <span data-ttu-id="bc05e-146">Значение</span><span class="sxs-lookup"><span data-stu-id="bc05e-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="bc05e-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="bc05e-147">201, 202</span></span>    | <span data-ttu-id="bc05e-148">Пакет был успешно отправлен</span><span class="sxs-lookup"><span data-stu-id="bc05e-148">The package was successfully pushed</span></span>
<span data-ttu-id="bc05e-149">400</span><span class="sxs-lookup"><span data-stu-id="bc05e-149">400</span></span>         | <span data-ttu-id="bc05e-150">Предоставленный пакет является недопустимым</span><span class="sxs-lookup"><span data-stu-id="bc05e-150">The provided package is invalid</span></span>
<span data-ttu-id="bc05e-151">409</span><span class="sxs-lookup"><span data-stu-id="bc05e-151">409</span></span>         | <span data-ttu-id="bc05e-152">Пакет с предоставленным Идентификатором и версией уже существует</span><span class="sxs-lookup"><span data-stu-id="bc05e-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="bc05e-153">Код состояния успеха возвращается, если пакет успешно отправлена по-разному реализаций серверов.</span><span class="sxs-lookup"><span data-stu-id="bc05e-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="bc05e-154">Удаление пакета</span><span class="sxs-lookup"><span data-stu-id="bc05e-154">Delete a package</span></span>

<span data-ttu-id="bc05e-155">NuGet.org интерпретирует запроса на удаление пакета как объект «исключить».</span><span class="sxs-lookup"><span data-stu-id="bc05e-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="bc05e-156">Это означает, что пакет по-прежнему доступен для существующих потребителей пакета, но пакета больше не отображается в результатах поиска или веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="bc05e-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="bc05e-157">Дополнительные сведения об этом практическом см. в разделе [удалить пакеты](../policies/deleting-packages.md) политики.</span><span class="sxs-lookup"><span data-stu-id="bc05e-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="bc05e-158">Реализации других серверов могут интерпретировать этот сигнал как окончательного удаления, возможностью удаления или исключить.</span><span class="sxs-lookup"><span data-stu-id="bc05e-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="bc05e-159">Например [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (реализация сервера только поддержка более старых API V2) поддерживает обработка данного запроса в качестве unlist или окончательного удаления зависимости от параметра конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bc05e-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="bc05e-160">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="bc05e-160">Request parameters</span></span>

<span data-ttu-id="bc05e-161">Имя</span><span class="sxs-lookup"><span data-stu-id="bc05e-161">Name</span></span>           | <span data-ttu-id="bc05e-162">Увеличение</span><span class="sxs-lookup"><span data-stu-id="bc05e-162">In</span></span>     | <span data-ttu-id="bc05e-163">Тип</span><span class="sxs-lookup"><span data-stu-id="bc05e-163">Type</span></span>   | <span data-ttu-id="bc05e-164">Обязательно</span><span class="sxs-lookup"><span data-stu-id="bc05e-164">Required</span></span> | <span data-ttu-id="bc05e-165">Примечания</span><span class="sxs-lookup"><span data-stu-id="bc05e-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="bc05e-166">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="bc05e-166">ID</span></span>             | <span data-ttu-id="bc05e-167">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="bc05e-167">URL</span></span>    | <span data-ttu-id="bc05e-168">string</span><span class="sxs-lookup"><span data-stu-id="bc05e-168">string</span></span> | <span data-ttu-id="bc05e-169">да</span><span class="sxs-lookup"><span data-stu-id="bc05e-169">yes</span></span>      | <span data-ttu-id="bc05e-170">Идентификатор пакета для удаления</span><span class="sxs-lookup"><span data-stu-id="bc05e-170">The ID of the package to delete</span></span>
<span data-ttu-id="bc05e-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="bc05e-171">VERSION</span></span>        | <span data-ttu-id="bc05e-172">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="bc05e-172">URL</span></span>    | <span data-ttu-id="bc05e-173">string</span><span class="sxs-lookup"><span data-stu-id="bc05e-173">string</span></span> | <span data-ttu-id="bc05e-174">да</span><span class="sxs-lookup"><span data-stu-id="bc05e-174">yes</span></span>      | <span data-ttu-id="bc05e-175">Версия пакета для удаления</span><span class="sxs-lookup"><span data-stu-id="bc05e-175">The version of the package to delete</span></span>
<span data-ttu-id="bc05e-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="bc05e-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="bc05e-177">Header</span><span class="sxs-lookup"><span data-stu-id="bc05e-177">Header</span></span> | <span data-ttu-id="bc05e-178">string</span><span class="sxs-lookup"><span data-stu-id="bc05e-178">string</span></span> | <span data-ttu-id="bc05e-179">да</span><span class="sxs-lookup"><span data-stu-id="bc05e-179">yes</span></span>      | <span data-ttu-id="bc05e-180">Например `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="bc05e-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="bc05e-181">Ответ</span><span class="sxs-lookup"><span data-stu-id="bc05e-181">Response</span></span>

<span data-ttu-id="bc05e-182">Код состояния</span><span class="sxs-lookup"><span data-stu-id="bc05e-182">Status Code</span></span> | <span data-ttu-id="bc05e-183">Значение</span><span class="sxs-lookup"><span data-stu-id="bc05e-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="bc05e-184">204</span><span class="sxs-lookup"><span data-stu-id="bc05e-184">204</span></span>         | <span data-ttu-id="bc05e-185">Пакет был удален.</span><span class="sxs-lookup"><span data-stu-id="bc05e-185">The package was deleted</span></span>
<span data-ttu-id="bc05e-186">404</span><span class="sxs-lookup"><span data-stu-id="bc05e-186">404</span></span>         | <span data-ttu-id="bc05e-187">Без пакета с использованием указанного `ID` и `VERSION` существует</span><span class="sxs-lookup"><span data-stu-id="bc05e-187">No package with the provided `ID` and `VERSION` exists</span></span>
