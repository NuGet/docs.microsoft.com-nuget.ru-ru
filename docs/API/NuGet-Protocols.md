---
title: "Протоколы NuGet.org | Документы Microsoft"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba1d9742-9f1c-42ff-8c30-8e953e23c501
description: "Протоколы развивающейся nuget.org взаимодействовать с клиентами NuGet."
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 097b7a86d056b692c52d6de76bc2fb99d1b58c6f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="e3656-103">Протоколы NuGet.org</span><span class="sxs-lookup"><span data-stu-id="e3656-103">nuget.org Protocols</span></span>

<span data-ttu-id="e3656-104">Для взаимодействия с nuget.org, клиенты должны следовать определенным протоколам.</span><span class="sxs-lookup"><span data-stu-id="e3656-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="e3656-105">Так как эти протоколы сохранить развиваться, клиенты необходимо определить версию протокола, которые они используют при вызове конкретного nuget.org API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="e3656-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="e3656-106">Это позволяет nuget.org необходимо ввести изменения в виде неразрывные старые клиенты.</span><span class="sxs-lookup"><span data-stu-id="e3656-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="e3656-107">Интерфейсы API, описанных на этой странице относятся к nuget.org и нет никаких предположений относительного других реализациях серверов NuGet представить эти API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="e3656-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="e3656-108">Сведения об API NuGet, широко осуществляемая экосистема NuGet см. в разделе [Обзор интерфейса API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="e3656-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="e3656-109">В этом разделе перечислены различные протоколы, как и когда они поступают существование.</span><span class="sxs-lookup"><span data-stu-id="e3656-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="e3656-110">Версия протокола NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="e3656-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="e3656-111">4.1.0 протокола задает использование ключей проверки области для взаимодействия со службами, отличные от nuget.org, чтобы проверить пакет учетной записи nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e3656-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="e3656-112">Обратите внимание, что `4.1.0` версия номер непрозрачная строка, но происходит совпадать с первой версии официальный NuGet клиента, который поддерживает этот протокол.</span><span class="sxs-lookup"><span data-stu-id="e3656-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="e3656-113">Проверка гарантирует, что API ключей, созданных пользователем используются только вместе с nuget.org и этой проверки или проверки службы сторонних осуществляется при помощи ключей проверки области однократного использования.</span><span class="sxs-lookup"><span data-stu-id="e3656-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="e3656-114">Эти ключи проверки области можно использовать для проверки пакета принадлежит конкретного пользователя (учетная запись) в nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e3656-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="e3656-115">Требования клиента</span><span class="sxs-lookup"><span data-stu-id="e3656-115">Client requirement</span></span>

<span data-ttu-id="e3656-116">Клиентам требуется передать следующий заголовок при вызове API **принудительной** пакетов nuget.org:</span><span class="sxs-lookup"><span data-stu-id="e3656-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="e3656-117">Обратите внимание, что предварительно `X-NuGet-Client-Version` заголовок используется для той же цели, но теперь устарело и больше не может использоваться.</span><span class="sxs-lookup"><span data-stu-id="e3656-117">Note that the pre-existing `X-NuGet-Client-Version` header has the same purpose but is now deprecated and should no longer be used.</span></span>

<span data-ttu-id="e3656-118">**Принудительной** сам протокол описан в документации по [ `PackagePublish` ресурсов](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="e3656-118">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="e3656-119">Если клиент взаимодействует с внешних служб и потребностей для проверки принадлежности пакета для конкретного пользователя (учетная запись), необходимо использовать следующий протокол и использовать ключи Проверьте область и не ключи API из nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e3656-119">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="e3656-120">API для запроса ключа убедитесь области</span><span class="sxs-lookup"><span data-stu-id="e3656-120">API to request a verify-scope key</span></span>

<span data-ttu-id="e3656-121">Этот API используется для получения ключа Проверьте область для nuget.org автору, чтобы проверить правильность пакета, который владеет этим пользователем.</span><span class="sxs-lookup"><span data-stu-id="e3656-121">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="e3656-122">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="e3656-122">Request parameters</span></span>

<span data-ttu-id="e3656-123">Имя</span><span class="sxs-lookup"><span data-stu-id="e3656-123">Name</span></span>           | <span data-ttu-id="e3656-124">Увеличение</span><span class="sxs-lookup"><span data-stu-id="e3656-124">In</span></span>     | <span data-ttu-id="e3656-125">Тип</span><span class="sxs-lookup"><span data-stu-id="e3656-125">Type</span></span>   | <span data-ttu-id="e3656-126">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e3656-126">Required</span></span> | <span data-ttu-id="e3656-127">Примечания</span><span class="sxs-lookup"><span data-stu-id="e3656-127">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="e3656-128">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="e3656-128">ID</span></span>             | <span data-ttu-id="e3656-129">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="e3656-129">URL</span></span>    | <span data-ttu-id="e3656-130">string</span><span class="sxs-lookup"><span data-stu-id="e3656-130">string</span></span> | <span data-ttu-id="e3656-131">да</span><span class="sxs-lookup"><span data-stu-id="e3656-131">yes</span></span>      | <span data-ttu-id="e3656-132">Identidier пакета, для которого запрашивается ключ области проверьте</span><span class="sxs-lookup"><span data-stu-id="e3656-132">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="e3656-133">VERSION</span><span class="sxs-lookup"><span data-stu-id="e3656-133">VERSION</span></span>        | <span data-ttu-id="e3656-134">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="e3656-134">URL</span></span>    | <span data-ttu-id="e3656-135">string</span><span class="sxs-lookup"><span data-stu-id="e3656-135">string</span></span> | <span data-ttu-id="e3656-136">Нет</span><span class="sxs-lookup"><span data-stu-id="e3656-136">no</span></span>       | <span data-ttu-id="e3656-137">Версия пакета</span><span class="sxs-lookup"><span data-stu-id="e3656-137">The package version</span></span>
<span data-ttu-id="e3656-138">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="e3656-138">X-NuGet-ApiKey</span></span> | <span data-ttu-id="e3656-139">Header</span><span class="sxs-lookup"><span data-stu-id="e3656-139">Header</span></span> | <span data-ttu-id="e3656-140">string</span><span class="sxs-lookup"><span data-stu-id="e3656-140">string</span></span> | <span data-ttu-id="e3656-141">да</span><span class="sxs-lookup"><span data-stu-id="e3656-141">yes</span></span>      | <span data-ttu-id="e3656-142">Например `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="e3656-142">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="e3656-143">Ответ</span><span class="sxs-lookup"><span data-stu-id="e3656-143">Response</span></span>

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="e3656-144">API, чтобы убедиться, что ключ области проверьте</span><span class="sxs-lookup"><span data-stu-id="e3656-144">API to verify the verify scope key</span></span>

<span data-ttu-id="e3656-145">Этот API используется для проверки области Проверьте ключ для принадлежащих nuget.org автора пакета.</span><span class="sxs-lookup"><span data-stu-id="e3656-145">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="e3656-146">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="e3656-146">Request parameters</span></span>

<span data-ttu-id="e3656-147">Имя</span><span class="sxs-lookup"><span data-stu-id="e3656-147">Name</span></span>           | <span data-ttu-id="e3656-148">Увеличение</span><span class="sxs-lookup"><span data-stu-id="e3656-148">In</span></span>     | <span data-ttu-id="e3656-149">Тип</span><span class="sxs-lookup"><span data-stu-id="e3656-149">Type</span></span>   | <span data-ttu-id="e3656-150">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e3656-150">Required</span></span> | <span data-ttu-id="e3656-151">Примечания</span><span class="sxs-lookup"><span data-stu-id="e3656-151">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="e3656-152">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="e3656-152">ID</span></span>             | <span data-ttu-id="e3656-153">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="e3656-153">URL</span></span>    | <span data-ttu-id="e3656-154">string</span><span class="sxs-lookup"><span data-stu-id="e3656-154">string</span></span> | <span data-ttu-id="e3656-155">да</span><span class="sxs-lookup"><span data-stu-id="e3656-155">yes</span></span>      | <span data-ttu-id="e3656-156">Идентификатор пакета, для которого запрашивается ключ области проверьте</span><span class="sxs-lookup"><span data-stu-id="e3656-156">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="e3656-157">VERSION</span><span class="sxs-lookup"><span data-stu-id="e3656-157">VERSION</span></span>        | <span data-ttu-id="e3656-158">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="e3656-158">URL</span></span>    | <span data-ttu-id="e3656-159">string</span><span class="sxs-lookup"><span data-stu-id="e3656-159">string</span></span> | <span data-ttu-id="e3656-160">Нет</span><span class="sxs-lookup"><span data-stu-id="e3656-160">no</span></span>       | <span data-ttu-id="e3656-161">Версия пакета</span><span class="sxs-lookup"><span data-stu-id="e3656-161">The package version</span></span>
<span data-ttu-id="e3656-162">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="e3656-162">X-NuGet-ApiKey</span></span> | <span data-ttu-id="e3656-163">Header</span><span class="sxs-lookup"><span data-stu-id="e3656-163">Header</span></span> | <span data-ttu-id="e3656-164">string</span><span class="sxs-lookup"><span data-stu-id="e3656-164">string</span></span> | <span data-ttu-id="e3656-165">да</span><span class="sxs-lookup"><span data-stu-id="e3656-165">yes</span></span>      | <span data-ttu-id="e3656-166">Например `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="e3656-166">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="e3656-167">Этот ключ API области проверьте, в дневное время истечения срока действия или при первом использовании произойдет раньше.</span><span class="sxs-lookup"><span data-stu-id="e3656-167">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="e3656-168">Ответ</span><span class="sxs-lookup"><span data-stu-id="e3656-168">Response</span></span>

<span data-ttu-id="e3656-169">Код состояния</span><span class="sxs-lookup"><span data-stu-id="e3656-169">Status Code</span></span> | <span data-ttu-id="e3656-170">Значение</span><span class="sxs-lookup"><span data-stu-id="e3656-170">Meaning</span></span>
----------- | -------
<span data-ttu-id="e3656-171">200</span><span class="sxs-lookup"><span data-stu-id="e3656-171">200</span></span>         | <span data-ttu-id="e3656-172">Ключ API является допустимым</span><span class="sxs-lookup"><span data-stu-id="e3656-172">The API key is valid</span></span>
<span data-ttu-id="e3656-173">403</span><span class="sxs-lookup"><span data-stu-id="e3656-173">403</span></span>         | <span data-ttu-id="e3656-174">Ключ API является недопустимым или не авторизован для передачи для пакета</span><span class="sxs-lookup"><span data-stu-id="e3656-174">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="e3656-175">404</span><span class="sxs-lookup"><span data-stu-id="e3656-175">404</span></span>         | <span data-ttu-id="e3656-176">Пакет ссылается `ID` и `VERSION` (необязательно) не существует</span><span class="sxs-lookup"><span data-stu-id="e3656-176">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
