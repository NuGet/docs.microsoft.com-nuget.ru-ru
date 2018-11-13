---
title: Отправка пакетов символов, NuGet API | Документация Майкрософт
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Службы публикации позволяет клиентам публиковать новые пакеты символов.
keywords: Пакет символов NuGet API push
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580417"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="3d8ab-104">Отправить пакеты символов</span><span class="sxs-lookup"><span data-stu-id="3d8ab-104">Push Symbol Packages</span></span>

<span data-ttu-id="3d8ab-105">Существует возможность принудительной отправки пакетов символов ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) с помощью NuGet V3 API.</span><span class="sxs-lookup"><span data-stu-id="3d8ab-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="3d8ab-106">Эти операции расположенного за пределами класса `SymbolPackagePublish` найти ресурс в [индекс службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="3d8ab-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="3d8ab-107">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="3d8ab-107">Versioning</span></span>

<span data-ttu-id="3d8ab-108">Следующие `@type` используется значение:</span><span class="sxs-lookup"><span data-stu-id="3d8ab-108">The following `@type` value is used:</span></span>

<span data-ttu-id="3d8ab-109">Значение@type </span><span class="sxs-lookup"><span data-stu-id="3d8ab-109">@type value</span></span>                 | <span data-ttu-id="3d8ab-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="3d8ab-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="3d8ab-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="3d8ab-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="3d8ab-112">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="3d8ab-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="3d8ab-113">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="3d8ab-113">Base URL</span></span>

<span data-ttu-id="3d8ab-114">Базовый URL-адрес для следующих API-интерфейсов является значением `@id` свойство `SymbolPackagePublish/4.9.0` ресурсов в источнике пакета [индекс службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="3d8ab-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="3d8ab-115">В приведенной ниже документации используется URL-адреса для nuget.org.</span><span class="sxs-lookup"><span data-stu-id="3d8ab-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="3d8ab-116">Рассмотрите возможность `https://www.nuget.org/api/v2/symbolpackage` как заполнитель для `@id` значение найдено в индекс службы.</span><span class="sxs-lookup"><span data-stu-id="3d8ab-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="3d8ab-117">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="3d8ab-117">HTTP methods</span></span>

<span data-ttu-id="3d8ab-118">`PUT` Метод HTTP поддерживается этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="3d8ab-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="3d8ab-119">Принудительную отправку пакета символов</span><span class="sxs-lookup"><span data-stu-id="3d8ab-119">Push a symbol package</span></span>

<span data-ttu-id="3d8ab-120">NuGet.org поддерживает помещает новый формат пакетов символов ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) с помощью следующего API.</span><span class="sxs-lookup"><span data-stu-id="3d8ab-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="3d8ab-121">Пакеты символов, с тем же Идентификатором и версией можно отправлять несколько раз.</span><span class="sxs-lookup"><span data-stu-id="3d8ab-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="3d8ab-122">Пакет символов будут отклонены в следующих случаях.</span><span class="sxs-lookup"><span data-stu-id="3d8ab-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="3d8ab-123">Пакет с тем же Идентификатором и версией не существует.</span><span class="sxs-lookup"><span data-stu-id="3d8ab-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="3d8ab-124">Пакет символов с тем же Идентификатором и версией был отправлен, но еще не опубликован.</span><span class="sxs-lookup"><span data-stu-id="3d8ab-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="3d8ab-125">Пакет символов ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) является недопустимым (см. в разделе [символов ограничения пакета](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="3d8ab-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="3d8ab-126">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="3d8ab-126">Request parameters</span></span>

<span data-ttu-id="3d8ab-127">name</span><span class="sxs-lookup"><span data-stu-id="3d8ab-127">Name</span></span>           | <span data-ttu-id="3d8ab-128">Увеличение</span><span class="sxs-lookup"><span data-stu-id="3d8ab-128">In</span></span>     | <span data-ttu-id="3d8ab-129">Тип</span><span class="sxs-lookup"><span data-stu-id="3d8ab-129">Type</span></span>   | <span data-ttu-id="3d8ab-130">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3d8ab-130">Required</span></span> | <span data-ttu-id="3d8ab-131">Примечания</span><span class="sxs-lookup"><span data-stu-id="3d8ab-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="3d8ab-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="3d8ab-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="3d8ab-133">Header</span><span class="sxs-lookup"><span data-stu-id="3d8ab-133">Header</span></span> | <span data-ttu-id="3d8ab-134">string</span><span class="sxs-lookup"><span data-stu-id="3d8ab-134">string</span></span> | <span data-ttu-id="3d8ab-135">да</span><span class="sxs-lookup"><span data-stu-id="3d8ab-135">yes</span></span>      | <span data-ttu-id="3d8ab-136">Например `X-NuGet-ApiKey: {USER_API_KEY}` </span><span class="sxs-lookup"><span data-stu-id="3d8ab-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="3d8ab-137">Ключ API — непрозрачная строка получить из источника пакета пользователем и настроены в клиент.</span><span class="sxs-lookup"><span data-stu-id="3d8ab-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="3d8ab-138">Нет определенного формата строки является обязательной, но длина ключа API не должен превышать размер для значения заголовка HTTP.</span><span class="sxs-lookup"><span data-stu-id="3d8ab-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="3d8ab-139">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="3d8ab-139">Request body</span></span>

<span data-ttu-id="3d8ab-140">Текст запроса для Push-уведомления символ совпадает с текстом запроса пакета запроса Push-уведомлений (см. в разделе [упаковки Push-уведомлений и удалить](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="3d8ab-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="3d8ab-141">Ответ</span><span class="sxs-lookup"><span data-stu-id="3d8ab-141">Response</span></span>

<span data-ttu-id="3d8ab-142">Код состояния</span><span class="sxs-lookup"><span data-stu-id="3d8ab-142">Status Code</span></span> | <span data-ttu-id="3d8ab-143">Значение</span><span class="sxs-lookup"><span data-stu-id="3d8ab-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="3d8ab-144">201</span><span class="sxs-lookup"><span data-stu-id="3d8ab-144">201</span></span>         | <span data-ttu-id="3d8ab-145">Пакет символов был успешно отправлен.</span><span class="sxs-lookup"><span data-stu-id="3d8ab-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="3d8ab-146">400</span><span class="sxs-lookup"><span data-stu-id="3d8ab-146">400</span></span>         | <span data-ttu-id="3d8ab-147">Недопустимый пакет указанный символ.</span><span class="sxs-lookup"><span data-stu-id="3d8ab-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="3d8ab-148">401</span><span class="sxs-lookup"><span data-stu-id="3d8ab-148">401</span></span>         | <span data-ttu-id="3d8ab-149">Пользователь не авторизован для выполнения этого действия.</span><span class="sxs-lookup"><span data-stu-id="3d8ab-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="3d8ab-150">404</span><span class="sxs-lookup"><span data-stu-id="3d8ab-150">404</span></span>         | <span data-ttu-id="3d8ab-151">Соответствующего пакета с помощью предоставленного идентификатора и версии не существует.</span><span class="sxs-lookup"><span data-stu-id="3d8ab-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="3d8ab-152">409</span><span class="sxs-lookup"><span data-stu-id="3d8ab-152">409</span></span>         | <span data-ttu-id="3d8ab-153">Был отправлен пакет символов с предоставленным Идентификатором и версией, но он еще не доступны.</span><span class="sxs-lookup"><span data-stu-id="3d8ab-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="3d8ab-154">413</span><span class="sxs-lookup"><span data-stu-id="3d8ab-154">413</span></span>         | <span data-ttu-id="3d8ab-155">Пакет слишком велик.</span><span class="sxs-lookup"><span data-stu-id="3d8ab-155">The package is too large.</span></span>

