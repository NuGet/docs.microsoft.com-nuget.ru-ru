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
ms.openlocfilehash: 81d32a7011268e45136e00cdb7345a95070aae06
ms.sourcegitcommit: be9c51b4b095aea40ef41bbea7e12ef0a194ee74
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248446"
---
# <a name="repository-signatures"></a><span data-ttu-id="31fd0-103">Репозиторий подписи</span><span class="sxs-lookup"><span data-stu-id="31fd0-103">Repository signatures</span></span>

<span data-ttu-id="31fd0-104">Если источник пакета поддерживает добавление подписей репозитория для опубликованных пакетов, можно для клиента определить сертификаты для подписи, используемые в источнике пакета.</span><span class="sxs-lookup"><span data-stu-id="31fd0-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="31fd0-105">Этот ресурс позволяет клиентам обнаруживать репозиторием подписи пакета было изменено или имеет непредвиденный сертификат для подписи.</span><span class="sxs-lookup"><span data-stu-id="31fd0-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="31fd0-106">Ресурс, используемый для получения сведения о подписи этот репозиторий является `RepositorySignatures` найти ресурс в [индекс службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="31fd0-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="31fd0-107">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="31fd0-107">Versioning</span></span>

<span data-ttu-id="31fd0-108">Следующие `@type` используется значение:</span><span class="sxs-lookup"><span data-stu-id="31fd0-108">The following `@type` value is used:</span></span>

<span data-ttu-id="31fd0-109">Значение@type </span><span class="sxs-lookup"><span data-stu-id="31fd0-109">@type value</span></span>                | <span data-ttu-id="31fd0-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="31fd0-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="31fd0-111">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="31fd0-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="31fd0-112">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="31fd0-112">The initial release</span></span>
<span data-ttu-id="31fd0-113">RepositorySignatures/4.9.0</span><span class="sxs-lookup"><span data-stu-id="31fd0-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="31fd0-114">Разрешает включение `allRepositorySigned`</span><span class="sxs-lookup"><span data-stu-id="31fd0-114">Allows enabling `allRepositorySigned`</span></span>

## <a name="base-url"></a><span data-ttu-id="31fd0-115">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="31fd0-115">Base URL</span></span>

<span data-ttu-id="31fd0-116">URL-адрес точки входа для следующих API-интерфейсов является значением `@id` свойство, связанное с ресурсом, упомянутых выше `@type` значение.</span><span class="sxs-lookup"><span data-stu-id="31fd0-116">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="31fd0-117">В этом разделе используется заполнитель URL-адреса `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="31fd0-117">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="31fd0-118">Обратите внимание, что в отличие от других ресурсов, `{@id}` URL-адрес необходим обслуживаются по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="31fd0-118">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="31fd0-119">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="31fd0-119">HTTP methods</span></span>

<span data-ttu-id="31fd0-120">Все URL-адресов в ресурсов поддержки только HTTP репозитория сигнатур методов `GET` и `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="31fd0-120">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="31fd0-121">Индекс подписи репозитория</span><span class="sxs-lookup"><span data-stu-id="31fd0-121">Repository signatures index</span></span>

<span data-ttu-id="31fd0-122">Индекс подписи репозитория содержит два элемента информации:</span><span class="sxs-lookup"><span data-stu-id="31fd0-122">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="31fd0-123">Ли найти все пакеты в источнике, подписанные этого источника пакетов репозитория.</span><span class="sxs-lookup"><span data-stu-id="31fd0-123">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="31fd0-124">Список сертификатов, используемых источника пакета для подписания пакетов.</span><span class="sxs-lookup"><span data-stu-id="31fd0-124">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="31fd0-125">В большинстве случаев в списке сертификатов будут добавляться только на.</span><span class="sxs-lookup"><span data-stu-id="31fd0-125">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="31fd0-126">Новые сертификаты следует добавить в список при предыдущий сертификат для подписи истек, и источник пакета должен начать использовать новый сертификат подписи.</span><span class="sxs-lookup"><span data-stu-id="31fd0-126">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="31fd0-127">Если сертификат удаляется из списка, это означает, что все подписи пакетов, созданных с помощью удален сертификат для подписи больше не считается допустимым клиентом.</span><span class="sxs-lookup"><span data-stu-id="31fd0-127">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="31fd0-128">В этом случае подпись пакета (но не обязательно пакета) является недопустимым.</span><span class="sxs-lookup"><span data-stu-id="31fd0-128">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="31fd0-129">Политика клиента может разрешить установку пакета как число без знака.</span><span class="sxs-lookup"><span data-stu-id="31fd0-129">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="31fd0-130">В случае отзыва сертификатов (например клавиш) источник пакета должен повторно подписать все пакеты, подписанные сертификатом уязвимой.</span><span class="sxs-lookup"><span data-stu-id="31fd0-130">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="31fd0-131">Кроме того источник пакета следует удалить затронутых сертификат из списка сертификатов подписи.</span><span class="sxs-lookup"><span data-stu-id="31fd0-131">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="31fd0-132">Следующий запрос извлекает индекс сигнатуры репозитория.</span><span class="sxs-lookup"><span data-stu-id="31fd0-132">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="31fd0-133">Индекс подписи репозиторий является документ JSON, который содержит объект со следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="31fd0-133">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="31fd0-134">name</span><span class="sxs-lookup"><span data-stu-id="31fd0-134">Name</span></span>                | <span data-ttu-id="31fd0-135">Тип</span><span class="sxs-lookup"><span data-stu-id="31fd0-135">Type</span></span>             | <span data-ttu-id="31fd0-136">Обязательно</span><span class="sxs-lookup"><span data-stu-id="31fd0-136">Required</span></span> | <span data-ttu-id="31fd0-137">Примечания</span><span class="sxs-lookup"><span data-stu-id="31fd0-137">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="31fd0-138">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="31fd0-138">allRepositorySigned</span></span> | <span data-ttu-id="31fd0-139">boolean</span><span class="sxs-lookup"><span data-stu-id="31fd0-139">boolean</span></span>          | <span data-ttu-id="31fd0-140">да</span><span class="sxs-lookup"><span data-stu-id="31fd0-140">yes</span></span>      | <span data-ttu-id="31fd0-141">Должен быть `false` на 4.7.0 ресурсов</span><span class="sxs-lookup"><span data-stu-id="31fd0-141">Must be `false` on 4.7.0 resource</span></span>
<span data-ttu-id="31fd0-142">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="31fd0-142">signingCertificates</span></span> | <span data-ttu-id="31fd0-143">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="31fd0-143">array of objects</span></span> | <span data-ttu-id="31fd0-144">да</span><span class="sxs-lookup"><span data-stu-id="31fd0-144">yes</span></span>      | 

<span data-ttu-id="31fd0-145">`allRepositorySigned` Логическое значение присвоено значение false, если источник пакета имеет некоторые пакеты, имеющие подпись отсутствует репозиторий.</span><span class="sxs-lookup"><span data-stu-id="31fd0-145">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="31fd0-146">Если логическое выражение имеет значение true, все пакеты, доступные на источник должен иметь сигнатуре репозитория, которая создается по одному из сертификатов подписей, упомянутые в `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="31fd0-146">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="31fd0-147">`allRepositorySigned` Логическое должно иметь значение false, если на 4.7.0 ресурсов.</span><span class="sxs-lookup"><span data-stu-id="31fd0-147">The `allRepositorySigned` boolean must be false on the 4.7.0 resource.</span></span> <span data-ttu-id="31fd0-148">Клиенты NuGet v4.7 и v4.8 не могут устанавливать пакеты из источников, которые имеют `allRepositorySigned` задано значение true.</span><span class="sxs-lookup"><span data-stu-id="31fd0-148">NuGet v4.7 and v4.8 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="31fd0-149">Должен быть один или несколько сертификатов подписи в `signingCertificates` массив Если `allRepositorySigned` логическое выражение имеет значение в значение true.</span><span class="sxs-lookup"><span data-stu-id="31fd0-149">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="31fd0-150">Если массив пуст и `allRepositorySigned` имеет значение true, все пакеты из источника должно считаться недействительным, несмотря на то, что политику клиента по-прежнему может разрешить использование пакетов.</span><span class="sxs-lookup"><span data-stu-id="31fd0-150">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="31fd0-151">Каждый элемент этого массива представляет собой объект JSON со следующими свойствами.</span><span class="sxs-lookup"><span data-stu-id="31fd0-151">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="31fd0-152">name</span><span class="sxs-lookup"><span data-stu-id="31fd0-152">Name</span></span>         | <span data-ttu-id="31fd0-153">Тип</span><span class="sxs-lookup"><span data-stu-id="31fd0-153">Type</span></span>   | <span data-ttu-id="31fd0-154">Обязательно</span><span class="sxs-lookup"><span data-stu-id="31fd0-154">Required</span></span> | <span data-ttu-id="31fd0-155">Примечания</span><span class="sxs-lookup"><span data-stu-id="31fd0-155">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="31fd0-156">contentUrl</span><span class="sxs-lookup"><span data-stu-id="31fd0-156">contentUrl</span></span>   | <span data-ttu-id="31fd0-157">string</span><span class="sxs-lookup"><span data-stu-id="31fd0-157">string</span></span> | <span data-ttu-id="31fd0-158">да</span><span class="sxs-lookup"><span data-stu-id="31fd0-158">yes</span></span>      | <span data-ttu-id="31fd0-159">Абсолютный URL-адрес в кодировке DER открытый сертификат</span><span class="sxs-lookup"><span data-stu-id="31fd0-159">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="31fd0-160">отпечатки пальцев</span><span class="sxs-lookup"><span data-stu-id="31fd0-160">fingerprints</span></span> | <span data-ttu-id="31fd0-161">object</span><span class="sxs-lookup"><span data-stu-id="31fd0-161">object</span></span> | <span data-ttu-id="31fd0-162">да</span><span class="sxs-lookup"><span data-stu-id="31fd0-162">yes</span></span>      |
<span data-ttu-id="31fd0-163">Тема</span><span class="sxs-lookup"><span data-stu-id="31fd0-163">subject</span></span>      | <span data-ttu-id="31fd0-164">string</span><span class="sxs-lookup"><span data-stu-id="31fd0-164">string</span></span> | <span data-ttu-id="31fd0-165">да</span><span class="sxs-lookup"><span data-stu-id="31fd0-165">yes</span></span>      | <span data-ttu-id="31fd0-166">Различающееся имя субъекта из сертификата</span><span class="sxs-lookup"><span data-stu-id="31fd0-166">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="31fd0-167">issuer</span><span class="sxs-lookup"><span data-stu-id="31fd0-167">issuer</span></span>       | <span data-ttu-id="31fd0-168">string</span><span class="sxs-lookup"><span data-stu-id="31fd0-168">string</span></span> | <span data-ttu-id="31fd0-169">да</span><span class="sxs-lookup"><span data-stu-id="31fd0-169">yes</span></span>      | <span data-ttu-id="31fd0-170">Различающееся имя издателя сертификата</span><span class="sxs-lookup"><span data-stu-id="31fd0-170">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="31fd0-171">notBefore</span><span class="sxs-lookup"><span data-stu-id="31fd0-171">notBefore</span></span>    | <span data-ttu-id="31fd0-172">string</span><span class="sxs-lookup"><span data-stu-id="31fd0-172">string</span></span> | <span data-ttu-id="31fd0-173">да</span><span class="sxs-lookup"><span data-stu-id="31fd0-173">yes</span></span>      | <span data-ttu-id="31fd0-174">Метка времени начала срока действия сертификата</span><span class="sxs-lookup"><span data-stu-id="31fd0-174">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="31fd0-175">notAfter</span><span class="sxs-lookup"><span data-stu-id="31fd0-175">notAfter</span></span>     | <span data-ttu-id="31fd0-176">string</span><span class="sxs-lookup"><span data-stu-id="31fd0-176">string</span></span> | <span data-ttu-id="31fd0-177">да</span><span class="sxs-lookup"><span data-stu-id="31fd0-177">yes</span></span>      | <span data-ttu-id="31fd0-178">Отметка времени окончания срока действия сертификата</span><span class="sxs-lookup"><span data-stu-id="31fd0-178">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="31fd0-179">Обратите внимание, что `contentUrl` должен обслуживаться по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="31fd0-179">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="31fd0-180">Этот URL-адрес имеет не определенному шаблону URL-адрес и должны быть динамически обнаружены при с помощью этого документа репозитория сигнатуры индекса.</span><span class="sxs-lookup"><span data-stu-id="31fd0-180">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="31fd0-181">Все свойства в этом объекте (помимо `contentUrl`) должен быть производное от сертификата, расположенный `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="31fd0-181">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="31fd0-182">Эти производное свойства предоставляются для удобства, чтобы свести к минимуму циклами.</span><span class="sxs-lookup"><span data-stu-id="31fd0-182">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="31fd0-183">`fingerprints` Объект имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="31fd0-183">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="31fd0-184">name</span><span class="sxs-lookup"><span data-stu-id="31fd0-184">Name</span></span>                   | <span data-ttu-id="31fd0-185">Тип</span><span class="sxs-lookup"><span data-stu-id="31fd0-185">Type</span></span>   | <span data-ttu-id="31fd0-186">Обязательно</span><span class="sxs-lookup"><span data-stu-id="31fd0-186">Required</span></span> | <span data-ttu-id="31fd0-187">Примечания</span><span class="sxs-lookup"><span data-stu-id="31fd0-187">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="31fd0-188">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="31fd0-188">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="31fd0-189">string</span><span class="sxs-lookup"><span data-stu-id="31fd0-189">string</span></span> | <span data-ttu-id="31fd0-190">да</span><span class="sxs-lookup"><span data-stu-id="31fd0-190">yes</span></span>      | <span data-ttu-id="31fd0-191">Отпечаток SHA-256</span><span class="sxs-lookup"><span data-stu-id="31fd0-191">The SHA-256 fingerprint</span></span>

<span data-ttu-id="31fd0-192">Имя ключа `2.16.840.1.101.3.4.2.1` — это идентификатор Объекта хэш-алгоритма SHA-256.</span><span class="sxs-lookup"><span data-stu-id="31fd0-192">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="31fd0-193">Все значения хэша должны быть строчные буквы, шестнадцатеричной кодировке строковые представления дайджест хэша.</span><span class="sxs-lookup"><span data-stu-id="31fd0-193">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="31fd0-194">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="31fd0-194">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="31fd0-195">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="31fd0-195">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
