---
title: Репозиторий Signatures, NuGet API | Документация Майкрософт
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: Ресурс подписи репозиторий позволяет клиентам источники пакетов рады сообщить о их репозитории, подписи возможности.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 50f309b99d4bf59e14f3e29b6b0421d8c3e8aa5a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547985"
---
# <a name="repository-signatures"></a><span data-ttu-id="4a1a0-103">Репозиторий подписи</span><span class="sxs-lookup"><span data-stu-id="4a1a0-103">Repository signatures</span></span>

<span data-ttu-id="4a1a0-104">Если источник пакета поддерживает добавление подписей репозитория для опубликованных пакетов, можно для клиента определить сертификаты для подписи, используемые в источнике пакета.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="4a1a0-105">Этот ресурс позволяет клиентам обнаруживать репозиторием подписи пакета было изменено или имеет непредвиденный сертификат для подписи.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="4a1a0-106">Ресурс, используемый для получения сведения о подписи этот репозиторий является `RepositorySignatures` найти ресурс в [индекс службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="4a1a0-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="4a1a0-107">Запускает NuGet.org объявляет о `RepositorySignatures` ресурсов в ближайшем будущем.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-107">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="4a1a0-108">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="4a1a0-108">Versioning</span></span>

<span data-ttu-id="4a1a0-109">Следующие `@type` используется значение:</span><span class="sxs-lookup"><span data-stu-id="4a1a0-109">The following `@type` value is used:</span></span>

<span data-ttu-id="4a1a0-110">Значение @type</span><span class="sxs-lookup"><span data-stu-id="4a1a0-110">@type value</span></span>                | <span data-ttu-id="4a1a0-111">Примечания</span><span class="sxs-lookup"><span data-stu-id="4a1a0-111">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="4a1a0-112">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="4a1a0-112">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="4a1a0-113">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="4a1a0-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="4a1a0-114">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="4a1a0-114">Base URL</span></span>

<span data-ttu-id="4a1a0-115">URL-адрес точки входа для следующих API-интерфейсов является значением `@id` свойство, связанное с ресурсом, упомянутых выше `@type` значение.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-115">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="4a1a0-116">В этом разделе используется заполнитель URL-адреса `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-116">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="4a1a0-117">Обратите внимание, что в отличие от других ресурсов, `{@id}` URL-адрес необходим обслуживаются по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-117">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="4a1a0-118">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="4a1a0-118">HTTP methods</span></span>

<span data-ttu-id="4a1a0-119">Все URL-адресов в ресурсов поддержки только HTTP репозитория сигнатур методов `GET` и `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-119">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="4a1a0-120">Индекс подписи репозитория</span><span class="sxs-lookup"><span data-stu-id="4a1a0-120">Repository signatures index</span></span>

<span data-ttu-id="4a1a0-121">Индекс подписи репозитория содержит два элемента информации:</span><span class="sxs-lookup"><span data-stu-id="4a1a0-121">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="4a1a0-122">Ли найти все пакеты в источнике, подписанные этого источника пакетов репозитория.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-122">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="4a1a0-123">Список сертификатов, используемых источника пакета для подписания пакетов.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-123">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="4a1a0-124">В большинстве случаев в списке сертификатов будут добавляться только на.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-124">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="4a1a0-125">Новые сертификаты следует добавить в список при предыдущий сертификат для подписи истек, и источник пакета должен начать использовать новый сертификат подписи.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-125">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="4a1a0-126">Если сертификат удаляется из списка, это означает, что все подписи пакетов, созданных с помощью удален сертификат для подписи больше не считается допустимым клиентом.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-126">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="4a1a0-127">В этом случае подпись пакета (но не обязательно пакета) является недопустимым.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-127">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="4a1a0-128">Политика клиента может разрешить установку пакета как число без знака.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-128">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="4a1a0-129">В случае отзыва сертификатов (например клавиш) источник пакета должен повторно подписать все пакеты, подписанные сертификатом уязвимой.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-129">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="4a1a0-130">Кроме того источник пакета следует удалить затронутых сертификат из списка сертификатов подписи.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-130">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="4a1a0-131">Следующий запрос извлекает индекс сигнатуры репозитория.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-131">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="4a1a0-132">Индекс подписи репозиторий является документ JSON, который содержит объект со следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="4a1a0-132">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="4a1a0-133">name</span><span class="sxs-lookup"><span data-stu-id="4a1a0-133">Name</span></span>                | <span data-ttu-id="4a1a0-134">Тип</span><span class="sxs-lookup"><span data-stu-id="4a1a0-134">Type</span></span>             | <span data-ttu-id="4a1a0-135">Обязательно</span><span class="sxs-lookup"><span data-stu-id="4a1a0-135">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="4a1a0-136">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="4a1a0-136">allRepositorySigned</span></span> | <span data-ttu-id="4a1a0-137">boolean</span><span class="sxs-lookup"><span data-stu-id="4a1a0-137">boolean</span></span>          | <span data-ttu-id="4a1a0-138">да</span><span class="sxs-lookup"><span data-stu-id="4a1a0-138">yes</span></span>
<span data-ttu-id="4a1a0-139">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="4a1a0-139">signingCertificates</span></span> | <span data-ttu-id="4a1a0-140">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="4a1a0-140">array of objects</span></span> | <span data-ttu-id="4a1a0-141">да</span><span class="sxs-lookup"><span data-stu-id="4a1a0-141">yes</span></span>

<span data-ttu-id="4a1a0-142">`allRepositorySigned` Логическое значение присвоено значение false, если источник пакета имеет некоторые пакеты, имеющие подпись отсутствует репозиторий.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-142">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="4a1a0-143">Если логическое выражение имеет значение true, все пакеты, доступные на источник должен иметь сигнатуре репозитория, которая создается по одному из сертификатов подписей, упомянутые в `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-143">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="4a1a0-144">Должен быть один или несколько сертификатов подписи в `signingCertificates` массив Если `allRepositorySigned` логическое выражение имеет значение в значение true.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-144">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="4a1a0-145">Если массив пуст и `allRepositorySigned` имеет значение true, все пакеты из источника должно считаться недействительным, несмотря на то, что политику клиента по-прежнему может разрешить использование пакетов.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-145">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="4a1a0-146">Каждый элемент этого массива представляет собой объект JSON со следующими свойствами.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-146">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="4a1a0-147">name</span><span class="sxs-lookup"><span data-stu-id="4a1a0-147">Name</span></span>         | <span data-ttu-id="4a1a0-148">Тип</span><span class="sxs-lookup"><span data-stu-id="4a1a0-148">Type</span></span>   | <span data-ttu-id="4a1a0-149">Обязательно</span><span class="sxs-lookup"><span data-stu-id="4a1a0-149">Required</span></span> | <span data-ttu-id="4a1a0-150">Примечания</span><span class="sxs-lookup"><span data-stu-id="4a1a0-150">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="4a1a0-151">contentUrl</span><span class="sxs-lookup"><span data-stu-id="4a1a0-151">contentUrl</span></span>   | <span data-ttu-id="4a1a0-152">string</span><span class="sxs-lookup"><span data-stu-id="4a1a0-152">string</span></span> | <span data-ttu-id="4a1a0-153">да</span><span class="sxs-lookup"><span data-stu-id="4a1a0-153">yes</span></span>      | <span data-ttu-id="4a1a0-154">Абсолютный URL-адрес в кодировке DER открытый сертификат</span><span class="sxs-lookup"><span data-stu-id="4a1a0-154">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="4a1a0-155">отпечатки пальцев</span><span class="sxs-lookup"><span data-stu-id="4a1a0-155">fingerprints</span></span> | <span data-ttu-id="4a1a0-156">object</span><span class="sxs-lookup"><span data-stu-id="4a1a0-156">object</span></span> | <span data-ttu-id="4a1a0-157">да</span><span class="sxs-lookup"><span data-stu-id="4a1a0-157">yes</span></span>      |
<span data-ttu-id="4a1a0-158">Тема</span><span class="sxs-lookup"><span data-stu-id="4a1a0-158">subject</span></span>      | <span data-ttu-id="4a1a0-159">string</span><span class="sxs-lookup"><span data-stu-id="4a1a0-159">string</span></span> | <span data-ttu-id="4a1a0-160">да</span><span class="sxs-lookup"><span data-stu-id="4a1a0-160">yes</span></span>      | <span data-ttu-id="4a1a0-161">Различающееся имя субъекта из сертификата</span><span class="sxs-lookup"><span data-stu-id="4a1a0-161">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="4a1a0-162">issuer</span><span class="sxs-lookup"><span data-stu-id="4a1a0-162">issuer</span></span>       | <span data-ttu-id="4a1a0-163">string</span><span class="sxs-lookup"><span data-stu-id="4a1a0-163">string</span></span> | <span data-ttu-id="4a1a0-164">да</span><span class="sxs-lookup"><span data-stu-id="4a1a0-164">yes</span></span>      | <span data-ttu-id="4a1a0-165">Различающееся имя издателя сертификата</span><span class="sxs-lookup"><span data-stu-id="4a1a0-165">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="4a1a0-166">notBefore</span><span class="sxs-lookup"><span data-stu-id="4a1a0-166">notBefore</span></span>    | <span data-ttu-id="4a1a0-167">string</span><span class="sxs-lookup"><span data-stu-id="4a1a0-167">string</span></span> | <span data-ttu-id="4a1a0-168">да</span><span class="sxs-lookup"><span data-stu-id="4a1a0-168">yes</span></span>      | <span data-ttu-id="4a1a0-169">Метка времени начала срока действия сертификата</span><span class="sxs-lookup"><span data-stu-id="4a1a0-169">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="4a1a0-170">notAfter</span><span class="sxs-lookup"><span data-stu-id="4a1a0-170">notAfter</span></span>     | <span data-ttu-id="4a1a0-171">string</span><span class="sxs-lookup"><span data-stu-id="4a1a0-171">string</span></span> | <span data-ttu-id="4a1a0-172">да</span><span class="sxs-lookup"><span data-stu-id="4a1a0-172">yes</span></span>      | <span data-ttu-id="4a1a0-173">Отметка времени окончания срока действия сертификата</span><span class="sxs-lookup"><span data-stu-id="4a1a0-173">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="4a1a0-174">Обратите внимание, что `contentUrl` должен обслуживаться по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-174">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="4a1a0-175">Этот URL-адрес имеет не определенному шаблону URL-адрес и должны быть динамически обнаружены при с помощью этого документа репозитория сигнатуры индекса.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-175">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="4a1a0-176">Все свойства в этом объекте (помимо `contentUrl`) должен быть производное от сертификата, расположенный `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-176">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="4a1a0-177">Эти производное свойства предоставляются для удобства, чтобы свести к минимуму циклами.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-177">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="4a1a0-178">`fingerprints` Объект имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="4a1a0-178">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="4a1a0-179">name</span><span class="sxs-lookup"><span data-stu-id="4a1a0-179">Name</span></span>                   | <span data-ttu-id="4a1a0-180">Тип</span><span class="sxs-lookup"><span data-stu-id="4a1a0-180">Type</span></span>   | <span data-ttu-id="4a1a0-181">Обязательно</span><span class="sxs-lookup"><span data-stu-id="4a1a0-181">Required</span></span> | <span data-ttu-id="4a1a0-182">Примечания</span><span class="sxs-lookup"><span data-stu-id="4a1a0-182">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="4a1a0-183">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="4a1a0-183">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="4a1a0-184">string</span><span class="sxs-lookup"><span data-stu-id="4a1a0-184">string</span></span> | <span data-ttu-id="4a1a0-185">да</span><span class="sxs-lookup"><span data-stu-id="4a1a0-185">yes</span></span>      | <span data-ttu-id="4a1a0-186">Отпечаток SHA-256</span><span class="sxs-lookup"><span data-stu-id="4a1a0-186">The SHA-256 fingerprint</span></span>

<span data-ttu-id="4a1a0-187">Имя ключа `2.16.840.1.101.3.4.2.1` — это идентификатор Объекта хэш-алгоритма SHA-256.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-187">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="4a1a0-188">Все значения хэша должны быть строчные буквы, шестнадцатеричной кодировке строковые представления дайджест хэша.</span><span class="sxs-lookup"><span data-stu-id="4a1a0-188">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="4a1a0-189">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="4a1a0-189">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="4a1a0-190">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="4a1a0-190">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
