---
title: Протоколы NuGet.org
description: Протоколы nuget.org развивающейся взаимодействовать с клиентами NuGet.
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547277"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="4fbc5-103">протоколы NuGet.org</span><span class="sxs-lookup"><span data-stu-id="4fbc5-103">nuget.org protocols</span></span>

<span data-ttu-id="4fbc5-104">Для взаимодействия с сайта nuget.org, клиенты должны следовать определенным протоколам.</span><span class="sxs-lookup"><span data-stu-id="4fbc5-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="4fbc5-105">Поскольку Предотвращайте все эти протоколы, клиентам необходимо определить версию протокола, которые они используют при вызове конкретного nuget.org API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="4fbc5-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="4fbc5-106">Это позволяет nuget.org, чтобы внести изменения в виде некритических для старых клиентов.</span><span class="sxs-lookup"><span data-stu-id="4fbc5-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="4fbc5-107">Интерфейсы API, описанные на этой странице относятся к nuget.org и не предполагает других реализаций сервера NuGet представить эти API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="4fbc5-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="4fbc5-108">Сведения об API NuGet, широко применяется во всех экосистеме NuGet см. в разделе [Обзор API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="4fbc5-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="4fbc5-109">В этом разделе перечислены различные протоколы, как и когда пользователи попросят существование.</span><span class="sxs-lookup"><span data-stu-id="4fbc5-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="4fbc5-110">Версия протокола NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="4fbc5-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="4fbc5-111">4.1.0 протокол определяет использование ключей проверки область для взаимодействия со службами, отличными от nuget.org, чтобы проверить пакет учетную запись nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4fbc5-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="4fbc5-112">Обратите внимание, что `4.1.0` версии число является непрозрачная строка, но совпадает с первой версии официального клиента NuGet, который поддерживает этот протокол.</span><span class="sxs-lookup"><span data-stu-id="4fbc5-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="4fbc5-113">Проверка гарантирует, что ключей API, созданных пользователем используются только с сайта nuget.org и этой проверки или проверки из сторонней службы осуществляется через ключи Проверьте область однократного использования.</span><span class="sxs-lookup"><span data-stu-id="4fbc5-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="4fbc5-114">Эти ключи для проверки области можно использовать для проверки того, что пакет принадлежит к определенному пользователю (учетная запись) на сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4fbc5-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="4fbc5-115">Требования клиента</span><span class="sxs-lookup"><span data-stu-id="4fbc5-115">Client requirement</span></span>

<span data-ttu-id="4fbc5-116">Клиенты должны передать следующий заголовок при вызове API **принудительной** пакетов на сайте nuget.org:</span><span class="sxs-lookup"><span data-stu-id="4fbc5-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

    X-NuGet-Protocol-Version: 4.1.0

<span data-ttu-id="4fbc5-117">Обратите внимание, что `X-NuGet-Client-Version` заголовок имеет похожую семантику, но зарезервировано только для использования с официального клиента NuGet.</span><span class="sxs-lookup"><span data-stu-id="4fbc5-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="4fbc5-118">Сторонние клиенты должны использовать `X-NuGet-Protocol-Version` заголовок и значение.</span><span class="sxs-lookup"><span data-stu-id="4fbc5-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="4fbc5-119">**Принудительной** сам протокол описан в документации по [ `PackagePublish` ресурсов](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="4fbc5-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="4fbc5-120">Если клиент взаимодействует с внешними службами и его необходимо проверить ли пакет принадлежит к определенному пользователю (учетная запись), его следует использовать следующий протокол и использовать ключи Проверьте область и не ключи API с сайта nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4fbc5-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="4fbc5-121">API для запроса ключа Проверьте область</span><span class="sxs-lookup"><span data-stu-id="4fbc5-121">API to request a verify-scope key</span></span>

<span data-ttu-id="4fbc5-122">Этот API используется для получения ключа Проверьте область для nuget.org автору, чтобы проверить пакет, принадлежащие ему.</span><span class="sxs-lookup"><span data-stu-id="4fbc5-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="4fbc5-123">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="4fbc5-123">Request parameters</span></span>

<span data-ttu-id="4fbc5-124">name</span><span class="sxs-lookup"><span data-stu-id="4fbc5-124">Name</span></span>           | <span data-ttu-id="4fbc5-125">Увеличение</span><span class="sxs-lookup"><span data-stu-id="4fbc5-125">In</span></span>     | <span data-ttu-id="4fbc5-126">Тип</span><span class="sxs-lookup"><span data-stu-id="4fbc5-126">Type</span></span>   | <span data-ttu-id="4fbc5-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="4fbc5-127">Required</span></span> | <span data-ttu-id="4fbc5-128">Примечания</span><span class="sxs-lookup"><span data-stu-id="4fbc5-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="4fbc5-129">ID</span><span class="sxs-lookup"><span data-stu-id="4fbc5-129">ID</span></span>             | <span data-ttu-id="4fbc5-130">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="4fbc5-130">URL</span></span>    | <span data-ttu-id="4fbc5-131">string</span><span class="sxs-lookup"><span data-stu-id="4fbc5-131">string</span></span> | <span data-ttu-id="4fbc5-132">да</span><span class="sxs-lookup"><span data-stu-id="4fbc5-132">yes</span></span>      | <span data-ttu-id="4fbc5-133">Identidier пакета, для которого запрашивается область подтверждения</span><span class="sxs-lookup"><span data-stu-id="4fbc5-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="4fbc5-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="4fbc5-134">VERSION</span></span>        | <span data-ttu-id="4fbc5-135">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="4fbc5-135">URL</span></span>    | <span data-ttu-id="4fbc5-136">string</span><span class="sxs-lookup"><span data-stu-id="4fbc5-136">string</span></span> | <span data-ttu-id="4fbc5-137">Нет</span><span class="sxs-lookup"><span data-stu-id="4fbc5-137">no</span></span>       | <span data-ttu-id="4fbc5-138">Версия пакета</span><span class="sxs-lookup"><span data-stu-id="4fbc5-138">The package version</span></span>
<span data-ttu-id="4fbc5-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="4fbc5-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="4fbc5-140">Header</span><span class="sxs-lookup"><span data-stu-id="4fbc5-140">Header</span></span> | <span data-ttu-id="4fbc5-141">string</span><span class="sxs-lookup"><span data-stu-id="4fbc5-141">string</span></span> | <span data-ttu-id="4fbc5-142">да</span><span class="sxs-lookup"><span data-stu-id="4fbc5-142">yes</span></span>      | <span data-ttu-id="4fbc5-143">Например `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="4fbc5-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="4fbc5-144">Ответ</span><span class="sxs-lookup"><span data-stu-id="4fbc5-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="4fbc5-145">API для проверки области подтверждения</span><span class="sxs-lookup"><span data-stu-id="4fbc5-145">API to verify the verify scope key</span></span>

<span data-ttu-id="4fbc5-146">Этот API используется для проверки области Проверьте ключ для пакет, принадлежащий автор nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4fbc5-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="4fbc5-147">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="4fbc5-147">Request parameters</span></span>

<span data-ttu-id="4fbc5-148">name</span><span class="sxs-lookup"><span data-stu-id="4fbc5-148">Name</span></span>           | <span data-ttu-id="4fbc5-149">Увеличение</span><span class="sxs-lookup"><span data-stu-id="4fbc5-149">In</span></span>     | <span data-ttu-id="4fbc5-150">Тип</span><span class="sxs-lookup"><span data-stu-id="4fbc5-150">Type</span></span>   | <span data-ttu-id="4fbc5-151">Обязательно</span><span class="sxs-lookup"><span data-stu-id="4fbc5-151">Required</span></span> | <span data-ttu-id="4fbc5-152">Примечания</span><span class="sxs-lookup"><span data-stu-id="4fbc5-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="4fbc5-153">ID</span><span class="sxs-lookup"><span data-stu-id="4fbc5-153">ID</span></span>             | <span data-ttu-id="4fbc5-154">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="4fbc5-154">URL</span></span>    | <span data-ttu-id="4fbc5-155">string</span><span class="sxs-lookup"><span data-stu-id="4fbc5-155">string</span></span> | <span data-ttu-id="4fbc5-156">да</span><span class="sxs-lookup"><span data-stu-id="4fbc5-156">yes</span></span>      | <span data-ttu-id="4fbc5-157">Идентификатор пакета, для которого запрашивается область подтверждения</span><span class="sxs-lookup"><span data-stu-id="4fbc5-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="4fbc5-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="4fbc5-158">VERSION</span></span>        | <span data-ttu-id="4fbc5-159">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="4fbc5-159">URL</span></span>    | <span data-ttu-id="4fbc5-160">string</span><span class="sxs-lookup"><span data-stu-id="4fbc5-160">string</span></span> | <span data-ttu-id="4fbc5-161">Нет</span><span class="sxs-lookup"><span data-stu-id="4fbc5-161">no</span></span>       | <span data-ttu-id="4fbc5-162">Версия пакета</span><span class="sxs-lookup"><span data-stu-id="4fbc5-162">The package version</span></span>
<span data-ttu-id="4fbc5-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="4fbc5-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="4fbc5-164">Header</span><span class="sxs-lookup"><span data-stu-id="4fbc5-164">Header</span></span> | <span data-ttu-id="4fbc5-165">string</span><span class="sxs-lookup"><span data-stu-id="4fbc5-165">string</span></span> | <span data-ttu-id="4fbc5-166">да</span><span class="sxs-lookup"><span data-stu-id="4fbc5-166">yes</span></span>      | <span data-ttu-id="4fbc5-167">Например `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="4fbc5-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="4fbc5-168">Этот ключ Проверьте область API, в дневное время истечения срока действия или при первом использовании, что произойдет раньше.</span><span class="sxs-lookup"><span data-stu-id="4fbc5-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="4fbc5-169">Ответ</span><span class="sxs-lookup"><span data-stu-id="4fbc5-169">Response</span></span>

<span data-ttu-id="4fbc5-170">Код состояния</span><span class="sxs-lookup"><span data-stu-id="4fbc5-170">Status Code</span></span> | <span data-ttu-id="4fbc5-171">Значение</span><span class="sxs-lookup"><span data-stu-id="4fbc5-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="4fbc5-172">200</span><span class="sxs-lookup"><span data-stu-id="4fbc5-172">200</span></span>         | <span data-ttu-id="4fbc5-173">Ключ API является допустимым</span><span class="sxs-lookup"><span data-stu-id="4fbc5-173">The API key is valid</span></span>
<span data-ttu-id="4fbc5-174">403</span><span class="sxs-lookup"><span data-stu-id="4fbc5-174">403</span></span>         | <span data-ttu-id="4fbc5-175">Ключ API является недопустимым или не авторизован для принудительной отправки для пакета</span><span class="sxs-lookup"><span data-stu-id="4fbc5-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="4fbc5-176">404</span><span class="sxs-lookup"><span data-stu-id="4fbc5-176">404</span></span>         | <span data-ttu-id="4fbc5-177">Пакет ссылается `ID` и `VERSION` (необязательно) не существует</span><span class="sxs-lookup"><span data-stu-id="4fbc5-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
