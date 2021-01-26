---
title: Отправка пакетов символов, API NuGet | Документация Майкрософт
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Служба публикации позволяет клиентам публиковать новые пакеты символов.
keywords: Пакет символов push-уведомлений API NuGet
ms.reviewer: karann
ms.openlocfilehash: 91bb4c9ca77fd7f1ff35831e02eb4f9d65d641c5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773899"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="4cba3-104">Отправка пакетов символов</span><span class="sxs-lookup"><span data-stu-id="4cba3-104">Push Symbol Packages</span></span>

<span data-ttu-id="4cba3-105">Пакеты символов ([снупкг](../create-packages/Symbol-Packages-snupkg.md)) можно отправить с помощью API-интерфейса NuGet v3.</span><span class="sxs-lookup"><span data-stu-id="4cba3-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="4cba3-106">Эти операции основаны на `SymbolPackagePublish` ресурсе, найденном в [индексе службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="4cba3-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="4cba3-107">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="4cba3-107">Versioning</span></span>

<span data-ttu-id="4cba3-108">Используется следующее `@type` значение:</span><span class="sxs-lookup"><span data-stu-id="4cba3-108">The following `@type` value is used:</span></span>

<span data-ttu-id="4cba3-109">Значение @type</span><span class="sxs-lookup"><span data-stu-id="4cba3-109">@type value</span></span>                 | <span data-ttu-id="4cba3-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="4cba3-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="4cba3-111">Симболпаккажепублиш/4.9.0</span><span class="sxs-lookup"><span data-stu-id="4cba3-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="4cba3-112">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="4cba3-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="4cba3-113">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="4cba3-113">Base URL</span></span>

<span data-ttu-id="4cba3-114">Базовый URL-адрес для следующих API-интерфейсов — это значение `@id` свойства `SymbolPackagePublish/4.9.0` ресурса в [индексе службы](service-index.md)источника пакета.</span><span class="sxs-lookup"><span data-stu-id="4cba3-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="4cba3-115">В приведенной ниже документации используется URL-адрес NuGet. org.</span><span class="sxs-lookup"><span data-stu-id="4cba3-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="4cba3-116">Рассмотрите в `https://www.nuget.org/api/v2/symbolpackage` качестве заполнителя для `@id` значения, найденного в индексе службы.</span><span class="sxs-lookup"><span data-stu-id="4cba3-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="4cba3-117">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="4cba3-117">HTTP methods</span></span>

<span data-ttu-id="4cba3-118">`PUT`Этот ресурс поддерживает метод HTTP.</span><span class="sxs-lookup"><span data-stu-id="4cba3-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="4cba3-119">Отправка пакета символов</span><span class="sxs-lookup"><span data-stu-id="4cba3-119">Push a symbol package</span></span>

<span data-ttu-id="4cba3-120">nuget.org поддерживает принудительную отправку нового формата пакетов символов ([снупкг](../create-packages/Symbol-Packages-snupkg.md)) с помощью следующего API.</span><span class="sxs-lookup"><span data-stu-id="4cba3-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

```
PUT https://www.nuget.org/api/v2/symbolpackage
```

<span data-ttu-id="4cba3-121">Пакеты символов с одинаковым ИДЕНТИФИКАТОРом и версией можно отправлять несколько раз.</span><span class="sxs-lookup"><span data-stu-id="4cba3-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="4cba3-122">Пакет символов будет отклонен в следующих случаях.</span><span class="sxs-lookup"><span data-stu-id="4cba3-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="4cba3-123">Пакет с тем же ИДЕНТИФИКАТОРом и версией не существует.</span><span class="sxs-lookup"><span data-stu-id="4cba3-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="4cba3-124">Пакет символов с тем же ИДЕНТИФИКАТОРом и версией был отправлен, но еще не опубликован.</span><span class="sxs-lookup"><span data-stu-id="4cba3-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="4cba3-125">Недопустимый пакет символов ([снупкг](../create-packages/Symbol-Packages-snupkg.md)) (см. раздел [ограничения пакета символов](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="4cba3-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="4cba3-126">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="4cba3-126">Request parameters</span></span>

<span data-ttu-id="4cba3-127">Имя</span><span class="sxs-lookup"><span data-stu-id="4cba3-127">Name</span></span>           | <span data-ttu-id="4cba3-128">В</span><span class="sxs-lookup"><span data-stu-id="4cba3-128">In</span></span>     | <span data-ttu-id="4cba3-129">Тип</span><span class="sxs-lookup"><span data-stu-id="4cba3-129">Type</span></span>   | <span data-ttu-id="4cba3-130">Обязательно</span><span class="sxs-lookup"><span data-stu-id="4cba3-130">Required</span></span> | <span data-ttu-id="4cba3-131">Примечания</span><span class="sxs-lookup"><span data-stu-id="4cba3-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="4cba3-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="4cba3-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="4cba3-133">Header</span><span class="sxs-lookup"><span data-stu-id="4cba3-133">Header</span></span> | <span data-ttu-id="4cba3-134">строка</span><span class="sxs-lookup"><span data-stu-id="4cba3-134">string</span></span> | <span data-ttu-id="4cba3-135">yes</span><span class="sxs-lookup"><span data-stu-id="4cba3-135">yes</span></span>      | <span data-ttu-id="4cba3-136">Например: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="4cba3-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="4cba3-137">Ключ API — это непрозрачная строка, полученная пользователем из источника пакета и настроенная в клиенте.</span><span class="sxs-lookup"><span data-stu-id="4cba3-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="4cba3-138">Конкретный формат строки не задан, но длина ключа API не должна превышать приемлемый размер для значений заголовка HTTP.</span><span class="sxs-lookup"><span data-stu-id="4cba3-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="4cba3-139">Тело запроса</span><span class="sxs-lookup"><span data-stu-id="4cba3-139">Request body</span></span>

<span data-ttu-id="4cba3-140">Текст запроса для отправки символа аналогичен тексту запроса на принудительную отправку пакета (см. раздел [Отправка и удаление пакета](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="4cba3-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="4cba3-141">Ответ</span><span class="sxs-lookup"><span data-stu-id="4cba3-141">Response</span></span>

<span data-ttu-id="4cba3-142">Код состояния</span><span class="sxs-lookup"><span data-stu-id="4cba3-142">Status Code</span></span> | <span data-ttu-id="4cba3-143">Значение</span><span class="sxs-lookup"><span data-stu-id="4cba3-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="4cba3-144">201</span><span class="sxs-lookup"><span data-stu-id="4cba3-144">201</span></span>         | <span data-ttu-id="4cba3-145">Пакет символов успешно отправлен.</span><span class="sxs-lookup"><span data-stu-id="4cba3-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="4cba3-146">400</span><span class="sxs-lookup"><span data-stu-id="4cba3-146">400</span></span>         | <span data-ttu-id="4cba3-147">Указан недопустимый пакет символов.</span><span class="sxs-lookup"><span data-stu-id="4cba3-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="4cba3-148">401</span><span class="sxs-lookup"><span data-stu-id="4cba3-148">401</span></span>         | <span data-ttu-id="4cba3-149">У пользователя нет разрешений на выполнение этого действия.</span><span class="sxs-lookup"><span data-stu-id="4cba3-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="4cba3-150">404</span><span class="sxs-lookup"><span data-stu-id="4cba3-150">404</span></span>         | <span data-ttu-id="4cba3-151">Соответствующий пакет с указанным ИДЕНТИФИКАТОРом и версией не существует.</span><span class="sxs-lookup"><span data-stu-id="4cba3-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="4cba3-152">409</span><span class="sxs-lookup"><span data-stu-id="4cba3-152">409</span></span>         | <span data-ttu-id="4cba3-153">Пакет символов с указанным ИДЕНТИФИКАТОРом и версией был отправлен, но пока недоступен.</span><span class="sxs-lookup"><span data-stu-id="4cba3-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="4cba3-154">413</span><span class="sxs-lookup"><span data-stu-id="4cba3-154">413</span></span>         | <span data-ttu-id="4cba3-155">Пакет слишком велик.</span><span class="sxs-lookup"><span data-stu-id="4cba3-155">The package is too large.</span></span>

