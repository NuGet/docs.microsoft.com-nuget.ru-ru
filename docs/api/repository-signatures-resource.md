---
title: Подписи репозитория, API NuGet | Документация Майкрософт
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: Ресурс "подписи репозитория" позволяет источникам пакетов клиентов объявлять свои возможности подписывания репозитория.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775330"
---
# <a name="repository-signatures"></a><span data-ttu-id="8ac9b-103">Подписи репозитория</span><span class="sxs-lookup"><span data-stu-id="8ac9b-103">Repository signatures</span></span>

<span data-ttu-id="8ac9b-104">Если источник пакета поддерживает добавление подписей репозитория в опубликованные пакеты, клиент может определить сертификаты подписи, используемые источником пакета.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="8ac9b-105">Этот ресурс позволяет клиентам определить, был ли подписанный в репозиторий пакет изменен или имеет непредвиденный сертификат подписи.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="8ac9b-106">Ресурс, используемый для получения сведений о подписи репозитория, — это `RepositorySignatures` ресурс, найденный в [индексе службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="8ac9b-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="8ac9b-107">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="8ac9b-107">Versioning</span></span>

<span data-ttu-id="8ac9b-108">Используется следующее `@type` значение:</span><span class="sxs-lookup"><span data-stu-id="8ac9b-108">The following `@type` value is used:</span></span>

<span data-ttu-id="8ac9b-109">Значение @type</span><span class="sxs-lookup"><span data-stu-id="8ac9b-109">@type value</span></span>                | <span data-ttu-id="8ac9b-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="8ac9b-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="8ac9b-111">Репоситорисигнатурес/4.7.0</span><span class="sxs-lookup"><span data-stu-id="8ac9b-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="8ac9b-112">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="8ac9b-112">The initial release</span></span>
<span data-ttu-id="8ac9b-113">Репоситорисигнатурес/4.9.0</span><span class="sxs-lookup"><span data-stu-id="8ac9b-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="8ac9b-114">Поддерживается клиентами NuGet v 4.9 +</span><span class="sxs-lookup"><span data-stu-id="8ac9b-114">Supported by NuGet v4.9+ clients</span></span>
<span data-ttu-id="8ac9b-115">Репоситорисигнатурес/5.0.0</span><span class="sxs-lookup"><span data-stu-id="8ac9b-115">RepositorySignatures/5.0.0</span></span> | <span data-ttu-id="8ac9b-116">Позволяет включить `allRepositorySigned` .</span><span class="sxs-lookup"><span data-stu-id="8ac9b-116">Allows enabling `allRepositorySigned`.</span></span> <span data-ttu-id="8ac9b-117">Поддерживается клиентами NuGet версии 5.0 и более поздних версий</span><span class="sxs-lookup"><span data-stu-id="8ac9b-117">Supported by NuGet v5.0+ clients</span></span>

## <a name="base-url"></a><span data-ttu-id="8ac9b-118">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="8ac9b-118">Base URL</span></span>

<span data-ttu-id="8ac9b-119">URL-адрес точки входа для следующих API-интерфейсов — это значение `@id` свойства, связанного с вышеупомянутым `@type` значением ресурса.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-119">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="8ac9b-120">В этом разделе используется URL-адрес заполнителя `{@id}` .</span><span class="sxs-lookup"><span data-stu-id="8ac9b-120">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="8ac9b-121">Обратите внимание, что, в отличие от других ресурсов, `{@id}` URL-адрес должен обрабатываться по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-121">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="8ac9b-122">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="8ac9b-122">HTTP methods</span></span>

<span data-ttu-id="8ac9b-123">Все URL-адреса, найденные в ресурсе сигнатур репозитория, поддерживают только методы HTTP `GET` и `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="8ac9b-123">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="8ac9b-124">Индекс подписей репозитория</span><span class="sxs-lookup"><span data-stu-id="8ac9b-124">Repository signatures index</span></span>

<span data-ttu-id="8ac9b-125">Индекс подписей репозитория содержит два фрагмента информации:</span><span class="sxs-lookup"><span data-stu-id="8ac9b-125">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="8ac9b-126">Являются ли все пакеты, найденные в источнике, подписанными этим источником пакетов.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-126">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="8ac9b-127">Список сертификатов, используемых источником пакета для подписи пакетов.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-127">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="8ac9b-128">В большинстве случаев список сертификатов будет добавляться к.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-128">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="8ac9b-129">Новые сертификаты добавляются в список, когда истечет срок действия предыдущего сертификата для подписи, и источнику пакета необходимо начать использовать новый сертификат подписи.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-129">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="8ac9b-130">Если сертификат удален из списка, это означает, что все подписи пакетов, созданные с помощью удаленного сертификата подписи, больше не должны считаться действительными для клиента.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-130">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="8ac9b-131">В этом случае подпись пакета (но не обязательно пакет) является недопустимой.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-131">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="8ac9b-132">Политика клиента может разрешить установку пакета без знака.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-132">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="8ac9b-133">В случае отзыва сертификата (например, Компрометация ключа) предполагается, что источник пакета повторно подписывает все пакеты, подписанные затронутым сертификатом.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-133">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="8ac9b-134">Кроме того, источник пакета должен удалить затронутый сертификат из списка сертификатов для подписи.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-134">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="8ac9b-135">Следующий запрос извлекает индекс подписей репозитория.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-135">The following request fetches the repository signatures index.</span></span>

```
GET {@id}
```

<span data-ttu-id="8ac9b-136">Индекс подписи репозитория — это документ JSON, содержащий объект со следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="8ac9b-136">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="8ac9b-137">Имя</span><span class="sxs-lookup"><span data-stu-id="8ac9b-137">Name</span></span>                | <span data-ttu-id="8ac9b-138">Тип</span><span class="sxs-lookup"><span data-stu-id="8ac9b-138">Type</span></span>             | <span data-ttu-id="8ac9b-139">Обязательно</span><span class="sxs-lookup"><span data-stu-id="8ac9b-139">Required</span></span> | <span data-ttu-id="8ac9b-140">Примечания</span><span class="sxs-lookup"><span data-stu-id="8ac9b-140">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="8ac9b-141">аллрепоситорисигнед</span><span class="sxs-lookup"><span data-stu-id="8ac9b-141">allRepositorySigned</span></span> | <span data-ttu-id="8ac9b-142">Логическое</span><span class="sxs-lookup"><span data-stu-id="8ac9b-142">boolean</span></span>          | <span data-ttu-id="8ac9b-143">yes</span><span class="sxs-lookup"><span data-stu-id="8ac9b-143">yes</span></span>      | <span data-ttu-id="8ac9b-144">Должен быть `false` для ресурсов 4.7.0 и 4.9.0</span><span class="sxs-lookup"><span data-stu-id="8ac9b-144">Must be `false` on 4.7.0 and 4.9.0 resources</span></span>
<span data-ttu-id="8ac9b-145">сигнингцертификатес</span><span class="sxs-lookup"><span data-stu-id="8ac9b-145">signingCertificates</span></span> | <span data-ttu-id="8ac9b-146">массив объектов</span><span class="sxs-lookup"><span data-stu-id="8ac9b-146">array of objects</span></span> | <span data-ttu-id="8ac9b-147">yes</span><span class="sxs-lookup"><span data-stu-id="8ac9b-147">yes</span></span>      | 

<span data-ttu-id="8ac9b-148">`allRepositorySigned`Логическое значение равно false, если источник пакета содержит пакеты, не имеющие подписи репозитория.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-148">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="8ac9b-149">Если для логического свойства задано значение true, то все пакеты, доступные в источнике, должны иметь подпись репозитория, созданную одним из сертификатов подписи, упомянутых в `signingCertificates` .</span><span class="sxs-lookup"><span data-stu-id="8ac9b-149">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="8ac9b-150">`allRepositorySigned`Для ресурсов 4.7.0 и 4.9.0 логическое значение должно быть равно false.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-150">The `allRepositorySigned` boolean must be false on the 4.7.0 and 4.9.0 resources.</span></span> <span data-ttu-id="8ac9b-151">Клиенты NuGet v 4.7, v 4.8 и v 4.9 не могут устанавливать пакеты из источников, `allRepositorySigned` для которых задано значение true.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-151">NuGet v4.7, v4.8, and v4.9 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="8ac9b-152">Если логическое значение равно true, в массиве должен быть один или несколько сертификатов для подписи `signingCertificates` `allRepositorySigned` .</span><span class="sxs-lookup"><span data-stu-id="8ac9b-152">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="8ac9b-153">Если массив пуст и `allRepositorySigned` имеет значение true, все пакеты из источника должны рассматриваться как недопустимые, хотя политика клиента может по-прежнему разрешать использование пакетов.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-153">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="8ac9b-154">Каждый элемент в этом массиве является объектом JSON со следующими свойствами.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-154">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="8ac9b-155">Имя</span><span class="sxs-lookup"><span data-stu-id="8ac9b-155">Name</span></span>         | <span data-ttu-id="8ac9b-156">Тип</span><span class="sxs-lookup"><span data-stu-id="8ac9b-156">Type</span></span>   | <span data-ttu-id="8ac9b-157">Обязательно</span><span class="sxs-lookup"><span data-stu-id="8ac9b-157">Required</span></span> | <span data-ttu-id="8ac9b-158">Примечания</span><span class="sxs-lookup"><span data-stu-id="8ac9b-158">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="8ac9b-159">contentUrl</span><span class="sxs-lookup"><span data-stu-id="8ac9b-159">contentUrl</span></span>   | <span data-ttu-id="8ac9b-160">строка</span><span class="sxs-lookup"><span data-stu-id="8ac9b-160">string</span></span> | <span data-ttu-id="8ac9b-161">yes</span><span class="sxs-lookup"><span data-stu-id="8ac9b-161">yes</span></span>      | <span data-ttu-id="8ac9b-162">Абсолютный URL-адрес общедоступного сертификата в формате DER</span><span class="sxs-lookup"><span data-stu-id="8ac9b-162">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="8ac9b-163">отпечатков</span><span class="sxs-lookup"><span data-stu-id="8ac9b-163">fingerprints</span></span> | <span data-ttu-id="8ac9b-164">object</span><span class="sxs-lookup"><span data-stu-id="8ac9b-164">object</span></span> | <span data-ttu-id="8ac9b-165">yes</span><span class="sxs-lookup"><span data-stu-id="8ac9b-165">yes</span></span>      |
<span data-ttu-id="8ac9b-166">subject</span><span class="sxs-lookup"><span data-stu-id="8ac9b-166">subject</span></span>      | <span data-ttu-id="8ac9b-167">строка</span><span class="sxs-lookup"><span data-stu-id="8ac9b-167">string</span></span> | <span data-ttu-id="8ac9b-168">yes</span><span class="sxs-lookup"><span data-stu-id="8ac9b-168">yes</span></span>      | <span data-ttu-id="8ac9b-169">Различающееся имя субъекта из сертификата</span><span class="sxs-lookup"><span data-stu-id="8ac9b-169">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="8ac9b-170">issuer</span><span class="sxs-lookup"><span data-stu-id="8ac9b-170">issuer</span></span>       | <span data-ttu-id="8ac9b-171">строка</span><span class="sxs-lookup"><span data-stu-id="8ac9b-171">string</span></span> | <span data-ttu-id="8ac9b-172">yes</span><span class="sxs-lookup"><span data-stu-id="8ac9b-172">yes</span></span>      | <span data-ttu-id="8ac9b-173">Различающееся имя издателя сертификата</span><span class="sxs-lookup"><span data-stu-id="8ac9b-173">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="8ac9b-174">notBefore</span><span class="sxs-lookup"><span data-stu-id="8ac9b-174">notBefore</span></span>    | <span data-ttu-id="8ac9b-175">строка</span><span class="sxs-lookup"><span data-stu-id="8ac9b-175">string</span></span> | <span data-ttu-id="8ac9b-176">yes</span><span class="sxs-lookup"><span data-stu-id="8ac9b-176">yes</span></span>      | <span data-ttu-id="8ac9b-177">Метка времени начала срока действия сертификата</span><span class="sxs-lookup"><span data-stu-id="8ac9b-177">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="8ac9b-178">notAfter</span><span class="sxs-lookup"><span data-stu-id="8ac9b-178">notAfter</span></span>     | <span data-ttu-id="8ac9b-179">строка</span><span class="sxs-lookup"><span data-stu-id="8ac9b-179">string</span></span> | <span data-ttu-id="8ac9b-180">yes</span><span class="sxs-lookup"><span data-stu-id="8ac9b-180">yes</span></span>      | <span data-ttu-id="8ac9b-181">Конечная метка времени периода действия сертификата</span><span class="sxs-lookup"><span data-stu-id="8ac9b-181">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="8ac9b-182">Обратите внимание, что объект должен обрабатываться `contentUrl` по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-182">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="8ac9b-183">Этот URL-адрес не имеет конкретного шаблона URL-адреса и должен быть динамически обнаружен с помощью этого документа индекса подписей репозитория.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-183">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="8ac9b-184">Все свойства в этом объекте (помимо `contentUrl` ) должны быть производными от сертификата, найденного в `contentUrl` .</span><span class="sxs-lookup"><span data-stu-id="8ac9b-184">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="8ac9b-185">Эти производные свойства предоставляются в качестве удобства для снижения круговых путей.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-185">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="8ac9b-186">Объект `fingerprints` имеет следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-186">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="8ac9b-187">Имя</span><span class="sxs-lookup"><span data-stu-id="8ac9b-187">Name</span></span>                   | <span data-ttu-id="8ac9b-188">Тип</span><span class="sxs-lookup"><span data-stu-id="8ac9b-188">Type</span></span>   | <span data-ttu-id="8ac9b-189">Обязательно</span><span class="sxs-lookup"><span data-stu-id="8ac9b-189">Required</span></span> | <span data-ttu-id="8ac9b-190">Примечания</span><span class="sxs-lookup"><span data-stu-id="8ac9b-190">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="8ac9b-191">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="8ac9b-191">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="8ac9b-192">строка</span><span class="sxs-lookup"><span data-stu-id="8ac9b-192">string</span></span> | <span data-ttu-id="8ac9b-193">yes</span><span class="sxs-lookup"><span data-stu-id="8ac9b-193">yes</span></span>      | <span data-ttu-id="8ac9b-194">Отпечаток SHA-256</span><span class="sxs-lookup"><span data-stu-id="8ac9b-194">The SHA-256 fingerprint</span></span>

<span data-ttu-id="8ac9b-195">Имя ключа `2.16.840.1.101.3.4.2.1` — OID алгоритма хеширования SHA-256.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-195">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="8ac9b-196">Все хэш-значения должны быть строчными и строковыми, закодированными шестнадцатеричным форматом хэш-хэша.</span><span class="sxs-lookup"><span data-stu-id="8ac9b-196">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="8ac9b-197">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="8ac9b-197">Sample request</span></span>

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a><span data-ttu-id="8ac9b-198">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="8ac9b-198">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
