---
title: Протоколы nuget.org
description: Развивающиеся протоколы nuget.org для взаимодействия с клиентами NuGet.
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773969"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="62e48-103">Протоколы nuget.org</span><span class="sxs-lookup"><span data-stu-id="62e48-103">nuget.org protocols</span></span>

<span data-ttu-id="62e48-104">Для взаимодействия с nuget.org клиентам необходимо соблюдать определенные протоколы.</span><span class="sxs-lookup"><span data-stu-id="62e48-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="62e48-105">Так как эти протоколы продолжают развиваться, клиенты должны указать используемую версию протокола при вызове конкретных API-интерфейсов nuget.org.</span><span class="sxs-lookup"><span data-stu-id="62e48-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="62e48-106">Это позволяет nuget.org внести изменения в некритический способ для старых клиентов.</span><span class="sxs-lookup"><span data-stu-id="62e48-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="62e48-107">API-интерфейсы, описанные на этой странице, относятся только к nuget.org и не предполагают, что другие реализации сервера NuGet могут ввести эти API.</span><span class="sxs-lookup"><span data-stu-id="62e48-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="62e48-108">Дополнительные сведения об API NuGet, реализованном в экосистеме NuGet, см. в [обзоре API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="62e48-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="62e48-109">В этом разделе перечислены различные протоколы как и, когда они бывают.</span><span class="sxs-lookup"><span data-stu-id="62e48-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="62e48-110">Версия протокола NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="62e48-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="62e48-111">Протокол 4.1.0 задает использование ключей проверки области для взаимодействия со службами, отличными от nuget.org, для проверки пакета на соответствие учетной записи nuget.org.</span><span class="sxs-lookup"><span data-stu-id="62e48-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="62e48-112">Обратите внимание, что `4.1.0` номер версии является непрозрачной строкой, но совпадает с первой версией официального клиента NuGet, который поддерживал этот протокол.</span><span class="sxs-lookup"><span data-stu-id="62e48-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="62e48-113">Проверка гарантирует, что создаваемые пользователем ключи API будут использоваться только с nuget.org, а другие проверки или проверки из сторонней службы обрабатываются посредством однократного использования ключей проверки области.</span><span class="sxs-lookup"><span data-stu-id="62e48-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="62e48-114">Эти ключи проверки можно использовать для проверки принадлежности пакета определенному пользователю (учетной записи) в nuget.org.</span><span class="sxs-lookup"><span data-stu-id="62e48-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="62e48-115">Требование клиента</span><span class="sxs-lookup"><span data-stu-id="62e48-115">Client requirement</span></span>

<span data-ttu-id="62e48-116">Клиентам необходимо передать следующий заголовок, если они выполняют вызовы API для **отправки** пакетов в NuGet.org:</span><span class="sxs-lookup"><span data-stu-id="62e48-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="62e48-117">Обратите внимание, что `X-NuGet-Client-Version` заголовок имеет подобную семантику, но зарезервировано только официальным клиентом NuGet.</span><span class="sxs-lookup"><span data-stu-id="62e48-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="62e48-118">Сторонние клиенты должны использовать `X-NuGet-Protocol-Version` заголовок и значение.</span><span class="sxs-lookup"><span data-stu-id="62e48-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="62e48-119">Сам протокол **push-уведомлений** описан в документации по [ `PackagePublish` ресурсу](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="62e48-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="62e48-120">Если клиент взаимодействует с внешними службами и должен проверить, принадлежит ли пакет определенному пользователю (учетная запись), он должен использовать следующий протокол и использовать ключи проверки области, а не ключи API из nuget.org.</span><span class="sxs-lookup"><span data-stu-id="62e48-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="62e48-121">API для запроса ключа проверки</span><span class="sxs-lookup"><span data-stu-id="62e48-121">API to request a verify-scope key</span></span>

<span data-ttu-id="62e48-122">Этот API используется для получения ключа проверки области действия для автора nuget.org для проверки пакета, принадлежащего ему.</span><span class="sxs-lookup"><span data-stu-id="62e48-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="62e48-123">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="62e48-123">Request parameters</span></span>

<span data-ttu-id="62e48-124">Имя</span><span class="sxs-lookup"><span data-stu-id="62e48-124">Name</span></span>           | <span data-ttu-id="62e48-125">В</span><span class="sxs-lookup"><span data-stu-id="62e48-125">In</span></span>     | <span data-ttu-id="62e48-126">Тип</span><span class="sxs-lookup"><span data-stu-id="62e48-126">Type</span></span>   | <span data-ttu-id="62e48-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="62e48-127">Required</span></span> | <span data-ttu-id="62e48-128">Примечания</span><span class="sxs-lookup"><span data-stu-id="62e48-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="62e48-129">ID</span><span class="sxs-lookup"><span data-stu-id="62e48-129">ID</span></span>             | <span data-ttu-id="62e48-130">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="62e48-130">URL</span></span>    | <span data-ttu-id="62e48-131">строка</span><span class="sxs-lookup"><span data-stu-id="62e48-131">string</span></span> | <span data-ttu-id="62e48-132">yes</span><span class="sxs-lookup"><span data-stu-id="62e48-132">yes</span></span>      | <span data-ttu-id="62e48-133">Пакет идентидиер, для которого запрашивается ключ области проверки</span><span class="sxs-lookup"><span data-stu-id="62e48-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="62e48-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="62e48-134">VERSION</span></span>        | <span data-ttu-id="62e48-135">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="62e48-135">URL</span></span>    | <span data-ttu-id="62e48-136">строка</span><span class="sxs-lookup"><span data-stu-id="62e48-136">string</span></span> | <span data-ttu-id="62e48-137">нет</span><span class="sxs-lookup"><span data-stu-id="62e48-137">no</span></span>       | <span data-ttu-id="62e48-138">Версия пакета</span><span class="sxs-lookup"><span data-stu-id="62e48-138">The package version</span></span>
<span data-ttu-id="62e48-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="62e48-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="62e48-140">Header</span><span class="sxs-lookup"><span data-stu-id="62e48-140">Header</span></span> | <span data-ttu-id="62e48-141">строка</span><span class="sxs-lookup"><span data-stu-id="62e48-141">string</span></span> | <span data-ttu-id="62e48-142">yes</span><span class="sxs-lookup"><span data-stu-id="62e48-142">yes</span></span>      | <span data-ttu-id="62e48-143">Например: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="62e48-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="62e48-144">Ответ</span><span class="sxs-lookup"><span data-stu-id="62e48-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="62e48-145">API для проверки ключа области проверки</span><span class="sxs-lookup"><span data-stu-id="62e48-145">API to verify the verify scope key</span></span>

<span data-ttu-id="62e48-146">Этот API используется для проверки ключа проверки области действия для пакета, принадлежащего автору nuget.org.</span><span class="sxs-lookup"><span data-stu-id="62e48-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="62e48-147">Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="62e48-147">Request parameters</span></span>

<span data-ttu-id="62e48-148">Имя</span><span class="sxs-lookup"><span data-stu-id="62e48-148">Name</span></span>           | <span data-ttu-id="62e48-149">В</span><span class="sxs-lookup"><span data-stu-id="62e48-149">In</span></span>     | <span data-ttu-id="62e48-150">Тип</span><span class="sxs-lookup"><span data-stu-id="62e48-150">Type</span></span>   | <span data-ttu-id="62e48-151">Обязательно</span><span class="sxs-lookup"><span data-stu-id="62e48-151">Required</span></span> | <span data-ttu-id="62e48-152">Примечания</span><span class="sxs-lookup"><span data-stu-id="62e48-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="62e48-153">ID</span><span class="sxs-lookup"><span data-stu-id="62e48-153">ID</span></span>             | <span data-ttu-id="62e48-154">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="62e48-154">URL</span></span>    | <span data-ttu-id="62e48-155">строка</span><span class="sxs-lookup"><span data-stu-id="62e48-155">string</span></span> | <span data-ttu-id="62e48-156">yes</span><span class="sxs-lookup"><span data-stu-id="62e48-156">yes</span></span>      | <span data-ttu-id="62e48-157">Идентификатор пакета, для которого запрашивается ключ области проверки</span><span class="sxs-lookup"><span data-stu-id="62e48-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="62e48-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="62e48-158">VERSION</span></span>        | <span data-ttu-id="62e48-159">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="62e48-159">URL</span></span>    | <span data-ttu-id="62e48-160">строка</span><span class="sxs-lookup"><span data-stu-id="62e48-160">string</span></span> | <span data-ttu-id="62e48-161">нет</span><span class="sxs-lookup"><span data-stu-id="62e48-161">no</span></span>       | <span data-ttu-id="62e48-162">Версия пакета</span><span class="sxs-lookup"><span data-stu-id="62e48-162">The package version</span></span>
<span data-ttu-id="62e48-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="62e48-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="62e48-164">Header</span><span class="sxs-lookup"><span data-stu-id="62e48-164">Header</span></span> | <span data-ttu-id="62e48-165">строка</span><span class="sxs-lookup"><span data-stu-id="62e48-165">string</span></span> | <span data-ttu-id="62e48-166">yes</span><span class="sxs-lookup"><span data-stu-id="62e48-166">yes</span></span>      | <span data-ttu-id="62e48-167">Например: `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="62e48-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="62e48-168">Срок действия ключа API области проверки истекает через день или при первом использовании, в зависимости от того, что происходит раньше.</span><span class="sxs-lookup"><span data-stu-id="62e48-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="62e48-169">Ответ</span><span class="sxs-lookup"><span data-stu-id="62e48-169">Response</span></span>

<span data-ttu-id="62e48-170">Код состояния</span><span class="sxs-lookup"><span data-stu-id="62e48-170">Status Code</span></span> | <span data-ttu-id="62e48-171">Значение</span><span class="sxs-lookup"><span data-stu-id="62e48-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="62e48-172">200</span><span class="sxs-lookup"><span data-stu-id="62e48-172">200</span></span>         | <span data-ttu-id="62e48-173">Ключ API является допустимым</span><span class="sxs-lookup"><span data-stu-id="62e48-173">The API key is valid</span></span>
<span data-ttu-id="62e48-174">403</span><span class="sxs-lookup"><span data-stu-id="62e48-174">403</span></span>         | <span data-ttu-id="62e48-175">Ключ API является недопустимым или не разрешен для отправки в пакет</span><span class="sxs-lookup"><span data-stu-id="62e48-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="62e48-176">404</span><span class="sxs-lookup"><span data-stu-id="62e48-176">404</span></span>         | <span data-ttu-id="62e48-177">Пакет, на который ссылается, `ID` и `VERSION` (необязательно) не существует</span><span class="sxs-lookup"><span data-stu-id="62e48-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
