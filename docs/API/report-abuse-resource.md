---
title: URL-адрес шаблона отчета о нарушении NuGet интерфейса API
description: Шаблон URL-адреса отчета о нарушении позволяет клиентам отображать ссылку на отчет о нарушении в их пользовательского интерфейса.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 15cf0953391489d9dd9b5d609c3f4c8f66748f19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="fc2c5-103">Шаблон URL-адреса отчета о нарушении</span><span class="sxs-lookup"><span data-stu-id="fc2c5-103">Report abuse URL template</span></span>

<span data-ttu-id="fc2c5-104">Существует возможность для клиента для построения URL-адрес, который может использоваться пользователем для сообщения о нарушении о определенного пакета.</span><span class="sxs-lookup"><span data-stu-id="fc2c5-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="fc2c5-105">Это полезно в том случае, когда источник пакета хочет обеспечить всех клиентов (даже третьих сторон) для делегирования отчетов о нарушении в исходную папку пакета.</span><span class="sxs-lookup"><span data-stu-id="fc2c5-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="fc2c5-106">Ресурс, используемый для получения содержимого пакета — `ReportAbuseUriTemplate` найти ресурс в [служба индекс](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="fc2c5-106">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="fc2c5-107">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="fc2c5-107">Versioning</span></span>

<span data-ttu-id="fc2c5-108">Следующие `@type` используются значения:</span><span class="sxs-lookup"><span data-stu-id="fc2c5-108">The following `@type` values are used:</span></span>

<span data-ttu-id="fc2c5-109">Значение @type</span><span class="sxs-lookup"><span data-stu-id="fc2c5-109">@type value</span></span>                       | <span data-ttu-id="fc2c5-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="fc2c5-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="fc2c5-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="fc2c5-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="fc2c5-112">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="fc2c5-112">The initial release</span></span>
<span data-ttu-id="fc2c5-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="fc2c5-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="fc2c5-114">Псевдоним `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="fc2c5-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="fc2c5-115">Шаблон URL-адреса</span><span class="sxs-lookup"><span data-stu-id="fc2c5-115">URL template</span></span>

<span data-ttu-id="fc2c5-116">URL-адрес для следующего API — это значение `@id` свойства, связанные с одной из упомянутых выше ресурсов `@type` значения.</span><span class="sxs-lookup"><span data-stu-id="fc2c5-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="fc2c5-117">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="fc2c5-117">HTTP methods</span></span>

<span data-ttu-id="fc2c5-118">Несмотря на то, что клиент не предназначен для выполнения запросов по URL-адресу отчетов о нарушении от имени пользователя, веб-страницы должны поддерживать `GET` метод, чтобы легко открыть в браузере пользователь щелкнул URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="fc2c5-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="fc2c5-119">Создать URL-адрес</span><span class="sxs-lookup"><span data-stu-id="fc2c5-119">Construct the URL</span></span>

<span data-ttu-id="fc2c5-120">Имея известные ИД и версию пакета, реализация клиента позволяет создавать URL-адрес, используемый для доступа к веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="fc2c5-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="fc2c5-121">Реализация клиента должно отображаться это сконструированный URL-адрес (или активную ссылку) для пользователей, позволяя им, чтобы откройте веб-браузер на URL-адрес и внесите любые необходимые о нарушении отчета.</span><span class="sxs-lookup"><span data-stu-id="fc2c5-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="fc2c5-122">Реализация формы отчетов о нарушении определяется реализация сервера.</span><span class="sxs-lookup"><span data-stu-id="fc2c5-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="fc2c5-123">Значение `@id` представляет собой строку URL-адрес содержит любые из следующих токенов заполнитель:</span><span class="sxs-lookup"><span data-stu-id="fc2c5-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="fc2c5-124">Местозаполнители URL-адресов</span><span class="sxs-lookup"><span data-stu-id="fc2c5-124">URL placeholders</span></span>

<span data-ttu-id="fc2c5-125">name</span><span class="sxs-lookup"><span data-stu-id="fc2c5-125">Name</span></span>        | <span data-ttu-id="fc2c5-126">Тип</span><span class="sxs-lookup"><span data-stu-id="fc2c5-126">Type</span></span>    | <span data-ttu-id="fc2c5-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="fc2c5-127">Required</span></span> | <span data-ttu-id="fc2c5-128">Примечания</span><span class="sxs-lookup"><span data-stu-id="fc2c5-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="fc2c5-129">string</span><span class="sxs-lookup"><span data-stu-id="fc2c5-129">string</span></span>  | <span data-ttu-id="fc2c5-130">Нет</span><span class="sxs-lookup"><span data-stu-id="fc2c5-130">no</span></span>       | <span data-ttu-id="fc2c5-131">Идентификатор пакета для сообщения о нарушении для</span><span class="sxs-lookup"><span data-stu-id="fc2c5-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="fc2c5-132">string</span><span class="sxs-lookup"><span data-stu-id="fc2c5-132">string</span></span>  | <span data-ttu-id="fc2c5-133">Нет</span><span class="sxs-lookup"><span data-stu-id="fc2c5-133">no</span></span>       | <span data-ttu-id="fc2c5-134">Версия пакета для сообщения о нарушении для</span><span class="sxs-lookup"><span data-stu-id="fc2c5-134">The package version to report abuse for</span></span>

<span data-ttu-id="fc2c5-135">`{id}` И `{version}` значения, интерпретируются реализация сервера должны быть без учета регистра и не подвержены ли Нормализованная версия.</span><span class="sxs-lookup"><span data-stu-id="fc2c5-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="fc2c5-136">Например nuget.org отчетов о нарушении шаблона выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fc2c5-136">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="fc2c5-137">Если реализация клиента должна отображать ссылку на форму отчета о нарушении для NuGet.Versioning 4.3.0, он бы привести следующий URL-адрес и предоставить его для пользователя:</span><span class="sxs-lookup"><span data-stu-id="fc2c5-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
