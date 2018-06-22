---
title: Протоколы NuGet.org
description: Протоколы развивающейся nuget.org взаимодействовать с клиентами NuGet.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: cc6d52617ea8b69d5b18b831ddf8a1a85dd6798f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822582"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="34cef-103">протоколы NuGet.org</span><span class="sxs-lookup"><span data-stu-id="34cef-103">nuget.org protocols</span></span>

<span data-ttu-id="34cef-104">Для взаимодействия с nuget.org, клиенты должны следовать определенным протоколам.</span><span class="sxs-lookup"><span data-stu-id="34cef-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="34cef-105">Так как эти протоколы сохранить развиваться, клиенты необходимо определить версию протокола, которые они используют при вызове конкретного nuget.org API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="34cef-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="34cef-106">Это позволяет nuget.org необходимо ввести изменения в виде неразрывные старые клиенты.</span><span class="sxs-lookup"><span data-stu-id="34cef-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="34cef-107">Интерфейсы API, описанных на этой странице относятся к nuget.org и нет никаких предположений относительного других реализациях серверов NuGet представить эти API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="34cef-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="34cef-108">Сведения об API NuGet, широко осуществляемая экосистема NuGet см. в разделе [Обзор интерфейса API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="34cef-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="34cef-109">В этом разделе перечислены различные протоколы, как и когда они поступают существование.</span><span class="sxs-lookup"><span data-stu-id="34cef-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="34cef-110">Версия протокола NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="34cef-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="34cef-111">4.1.0 протокола задает использование ключей проверки области для взаимодействия со службами, отличные от nuget.org, чтобы проверить пакет учетной записи nuget.org.</span><span class="sxs-lookup"><span data-stu-id="34cef-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="34cef-112">Обратите внимание, что `4.1.0` версия номер непрозрачная строка, но происходит совпадать с первой версии официальный NuGet клиента, который поддерживает этот протокол.</span><span class="sxs-lookup"><span data-stu-id="34cef-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="34cef-113">Проверка гарантирует, что API ключей, созданных пользователем используются только вместе с nuget.org и этой проверки или проверки службы сторонних осуществляется при помощи ключей проверки области однократного использования.</span><span class="sxs-lookup"><span data-stu-id="34cef-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="34cef-114">Эти ключи проверки области можно использовать для проверки пакета принадлежит конкретного пользователя (учетная запись) в nuget.org.</span><span class="sxs-lookup"><span data-stu-id="34cef-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="34cef-115">Требования клиента</span><span class="sxs-lookup"><span data-stu-id="34cef-115">Client requirement</span></span>

<span data-ttu-id="34cef-116">Клиентам требуется передать следующий заголовок при вызове API **принудительной** пакетов nuget.org:</span><span class="sxs-lookup"><span data-stu-id="34cef-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

    X-NuGet-Protocol-Version: 4.1.0

<span data-ttu-id="34cef-117">Обратите внимание, что `X-NuGet-Client-Version` заголовок имеет похожую семантику, но зарезервировано только для использования клиентом официальный NuGet.</span><span class="sxs-lookup"><span data-stu-id="34cef-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="34cef-118">Сторонние клиенты должны использовать `X-NuGet-Protocol-Version` заголовка и значения.</span><span class="sxs-lookup"><span data-stu-id="34cef-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="34cef-119">**Принудительной** сам протокол описан в документации по [ `PackagePublish` ресурсов](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="34cef-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="34cef-120">Если клиент взаимодействует с внешних служб и потребностей для проверки принадлежности пакета для конкретного пользователя (учетная запись), необходимо использовать следующий протокол и использовать ключи Проверьте область и не ключи API из nuget.org.</span><span class="sxs-lookup"><span data-stu-id="34cef-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="34cef-121">API для запроса ключа убедитесь области</span><span class="sxs-lookup"><span data-stu-id="34cef-121">API to request a verify-scope key</span></span>

<span data-ttu-id="34cef-122">Этот API используется для получения ключа Проверьте область для nuget.org автору, чтобы проверить правильность пакета, который владеет этим пользователем.</span><span class="sxs-lookup"><span data-stu-id="34cef-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="34cef-123">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="34cef-123">Request parameters</span></span>

<span data-ttu-id="34cef-124">name</span><span class="sxs-lookup"><span data-stu-id="34cef-124">Name</span></span>           | <span data-ttu-id="34cef-125">Увеличение</span><span class="sxs-lookup"><span data-stu-id="34cef-125">In</span></span>     | <span data-ttu-id="34cef-126">Тип</span><span class="sxs-lookup"><span data-stu-id="34cef-126">Type</span></span>   | <span data-ttu-id="34cef-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="34cef-127">Required</span></span> | <span data-ttu-id="34cef-128">Примечания</span><span class="sxs-lookup"><span data-stu-id="34cef-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="34cef-129">ID</span><span class="sxs-lookup"><span data-stu-id="34cef-129">ID</span></span>             | <span data-ttu-id="34cef-130">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="34cef-130">URL</span></span>    | <span data-ttu-id="34cef-131">string</span><span class="sxs-lookup"><span data-stu-id="34cef-131">string</span></span> | <span data-ttu-id="34cef-132">да</span><span class="sxs-lookup"><span data-stu-id="34cef-132">yes</span></span>      | <span data-ttu-id="34cef-133">Identidier пакета, для которого запрашивается ключ области проверьте</span><span class="sxs-lookup"><span data-stu-id="34cef-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="34cef-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="34cef-134">VERSION</span></span>        | <span data-ttu-id="34cef-135">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="34cef-135">URL</span></span>    | <span data-ttu-id="34cef-136">string</span><span class="sxs-lookup"><span data-stu-id="34cef-136">string</span></span> | <span data-ttu-id="34cef-137">Нет</span><span class="sxs-lookup"><span data-stu-id="34cef-137">no</span></span>       | <span data-ttu-id="34cef-138">Версия пакета</span><span class="sxs-lookup"><span data-stu-id="34cef-138">The package version</span></span>
<span data-ttu-id="34cef-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="34cef-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="34cef-140">Header</span><span class="sxs-lookup"><span data-stu-id="34cef-140">Header</span></span> | <span data-ttu-id="34cef-141">string</span><span class="sxs-lookup"><span data-stu-id="34cef-141">string</span></span> | <span data-ttu-id="34cef-142">да</span><span class="sxs-lookup"><span data-stu-id="34cef-142">yes</span></span>      | <span data-ttu-id="34cef-143">Например `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="34cef-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="34cef-144">Ответ</span><span class="sxs-lookup"><span data-stu-id="34cef-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="34cef-145">API, чтобы убедиться, что ключ области проверьте</span><span class="sxs-lookup"><span data-stu-id="34cef-145">API to verify the verify scope key</span></span>

<span data-ttu-id="34cef-146">Этот API используется для проверки области Проверьте ключ для принадлежащих nuget.org автора пакета.</span><span class="sxs-lookup"><span data-stu-id="34cef-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="34cef-147">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="34cef-147">Request parameters</span></span>

<span data-ttu-id="34cef-148">name</span><span class="sxs-lookup"><span data-stu-id="34cef-148">Name</span></span>           | <span data-ttu-id="34cef-149">Увеличение</span><span class="sxs-lookup"><span data-stu-id="34cef-149">In</span></span>     | <span data-ttu-id="34cef-150">Тип</span><span class="sxs-lookup"><span data-stu-id="34cef-150">Type</span></span>   | <span data-ttu-id="34cef-151">Обязательно</span><span class="sxs-lookup"><span data-stu-id="34cef-151">Required</span></span> | <span data-ttu-id="34cef-152">Примечания</span><span class="sxs-lookup"><span data-stu-id="34cef-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="34cef-153">ID</span><span class="sxs-lookup"><span data-stu-id="34cef-153">ID</span></span>             | <span data-ttu-id="34cef-154">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="34cef-154">URL</span></span>    | <span data-ttu-id="34cef-155">string</span><span class="sxs-lookup"><span data-stu-id="34cef-155">string</span></span> | <span data-ttu-id="34cef-156">да</span><span class="sxs-lookup"><span data-stu-id="34cef-156">yes</span></span>      | <span data-ttu-id="34cef-157">Идентификатор пакета, для которого запрашивается ключ области проверьте</span><span class="sxs-lookup"><span data-stu-id="34cef-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="34cef-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="34cef-158">VERSION</span></span>        | <span data-ttu-id="34cef-159">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="34cef-159">URL</span></span>    | <span data-ttu-id="34cef-160">string</span><span class="sxs-lookup"><span data-stu-id="34cef-160">string</span></span> | <span data-ttu-id="34cef-161">Нет</span><span class="sxs-lookup"><span data-stu-id="34cef-161">no</span></span>       | <span data-ttu-id="34cef-162">Версия пакета</span><span class="sxs-lookup"><span data-stu-id="34cef-162">The package version</span></span>
<span data-ttu-id="34cef-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="34cef-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="34cef-164">Header</span><span class="sxs-lookup"><span data-stu-id="34cef-164">Header</span></span> | <span data-ttu-id="34cef-165">string</span><span class="sxs-lookup"><span data-stu-id="34cef-165">string</span></span> | <span data-ttu-id="34cef-166">да</span><span class="sxs-lookup"><span data-stu-id="34cef-166">yes</span></span>      | <span data-ttu-id="34cef-167">Например `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="34cef-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="34cef-168">Этот ключ API области проверьте, в дневное время истечения срока действия или при первом использовании произойдет раньше.</span><span class="sxs-lookup"><span data-stu-id="34cef-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="34cef-169">Ответ</span><span class="sxs-lookup"><span data-stu-id="34cef-169">Response</span></span>

<span data-ttu-id="34cef-170">Код состояния</span><span class="sxs-lookup"><span data-stu-id="34cef-170">Status Code</span></span> | <span data-ttu-id="34cef-171">Значение</span><span class="sxs-lookup"><span data-stu-id="34cef-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="34cef-172">200</span><span class="sxs-lookup"><span data-stu-id="34cef-172">200</span></span>         | <span data-ttu-id="34cef-173">Ключ API является допустимым</span><span class="sxs-lookup"><span data-stu-id="34cef-173">The API key is valid</span></span>
<span data-ttu-id="34cef-174">403</span><span class="sxs-lookup"><span data-stu-id="34cef-174">403</span></span>         | <span data-ttu-id="34cef-175">Ключ API является недопустимым или не авторизован для передачи для пакета</span><span class="sxs-lookup"><span data-stu-id="34cef-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="34cef-176">404</span><span class="sxs-lookup"><span data-stu-id="34cef-176">404</span></span>         | <span data-ttu-id="34cef-177">Пакет ссылается `ID` и `VERSION` (необязательно) не существует</span><span class="sxs-lookup"><span data-stu-id="34cef-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
