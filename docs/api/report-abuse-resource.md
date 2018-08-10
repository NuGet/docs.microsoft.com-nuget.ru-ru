---
title: Сообщить о нарушении URL-адрес шаблона, API NuGet
description: Шаблон URL-адрес отчета о нарушении позволяет клиентам отображать ссылку на отчет о нарушении в их пользовательском Интерфейсе.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b1fd65b12590a6c5eeb23d946eec6ca4a1c661bc
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020444"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="c1209-103">Шаблон URL-адрес отчета о нарушении</span><span class="sxs-lookup"><span data-stu-id="c1209-103">Report abuse URL template</span></span>

<span data-ttu-id="c1209-104">Вполне возможно, для клиента, чтобы сформировать URL-адрес, который может использоваться пользователем, чтобы сообщить о нарушении об определенном пакете.</span><span class="sxs-lookup"><span data-stu-id="c1209-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="c1209-105">Это полезно в тех случаях, когда источник пакета необходимо включить все клиентские приложения (даже сторонний) для делегирования отчеты о нарушении к источнику пакета.</span><span class="sxs-lookup"><span data-stu-id="c1209-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="c1209-106">Ресурс, используемый для сборки этот URL-адрес является `ReportAbuseUriTemplate` найти ресурс в [индекс службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="c1209-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="c1209-107">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="c1209-107">Versioning</span></span>

<span data-ttu-id="c1209-108">Следующие `@type` значения используются:</span><span class="sxs-lookup"><span data-stu-id="c1209-108">The following `@type` values are used:</span></span>

<span data-ttu-id="c1209-109">Значение @type</span><span class="sxs-lookup"><span data-stu-id="c1209-109">@type value</span></span>                       | <span data-ttu-id="c1209-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="c1209-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="c1209-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="c1209-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="c1209-112">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="c1209-112">The initial release</span></span>
<span data-ttu-id="c1209-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="c1209-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="c1209-114">Псевдоним `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="c1209-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="c1209-115">Шаблон URL-адреса</span><span class="sxs-lookup"><span data-stu-id="c1209-115">URL template</span></span>

<span data-ttu-id="c1209-116">URL-адрес для следующего API — это значение `@id` свойства, связанные с одной из упомянутых выше ресурсов `@type` значения.</span><span class="sxs-lookup"><span data-stu-id="c1209-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="c1209-117">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="c1209-117">HTTP methods</span></span>

<span data-ttu-id="c1209-118">Несмотря на то, что клиент не предназначен для выполнения запросов к URL-адрес отчета о нарушении от имени пользователя, веб-страницы должен поддерживать `GET` метод, чтобы легко открыть в веб-браузере щелкнули URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="c1209-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="c1209-119">Создать URL-адрес</span><span class="sxs-lookup"><span data-stu-id="c1209-119">Construct the URL</span></span>

<span data-ttu-id="c1209-120">Учитывая известные ИД и версию пакета, реализация клиента можно создать URL-адрес, используемый для доступа к веб-интерфейс.</span><span class="sxs-lookup"><span data-stu-id="c1209-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="c1209-121">Реализация клиента отображать этот построенный URL-адрес (или активную ссылку) для пользователя, позволяющий открыть веб-браузер на URL-адрес и любые необходимые о нарушении отчет.</span><span class="sxs-lookup"><span data-stu-id="c1209-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="c1209-122">Реализация формы о нарушении отчета определяется в реализации сервера.</span><span class="sxs-lookup"><span data-stu-id="c1209-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="c1209-123">Значение `@id` — это строка URL-адрес, с любой из следующих токенов заполнитель:</span><span class="sxs-lookup"><span data-stu-id="c1209-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="c1209-124">Местозаполнители URL-адресов</span><span class="sxs-lookup"><span data-stu-id="c1209-124">URL placeholders</span></span>

<span data-ttu-id="c1209-125">name</span><span class="sxs-lookup"><span data-stu-id="c1209-125">Name</span></span>        | <span data-ttu-id="c1209-126">Тип</span><span class="sxs-lookup"><span data-stu-id="c1209-126">Type</span></span>    | <span data-ttu-id="c1209-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c1209-127">Required</span></span> | <span data-ttu-id="c1209-128">Примечания</span><span class="sxs-lookup"><span data-stu-id="c1209-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="c1209-129">string</span><span class="sxs-lookup"><span data-stu-id="c1209-129">string</span></span>  | <span data-ttu-id="c1209-130">Нет</span><span class="sxs-lookup"><span data-stu-id="c1209-130">no</span></span>       | <span data-ttu-id="c1209-131">Идентификатор пакета, чтобы сообщить о нарушении</span><span class="sxs-lookup"><span data-stu-id="c1209-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="c1209-132">string</span><span class="sxs-lookup"><span data-stu-id="c1209-132">string</span></span>  | <span data-ttu-id="c1209-133">Нет</span><span class="sxs-lookup"><span data-stu-id="c1209-133">no</span></span>       | <span data-ttu-id="c1209-134">Версия пакета, чтобы сообщить о нарушении</span><span class="sxs-lookup"><span data-stu-id="c1209-134">The package version to report abuse for</span></span>

<span data-ttu-id="c1209-135">`{id}` И `{version}` значения, интерпретируется в реализации сервера должны быть без учета регистра и не чувствительны к ли нормализуется версии.</span><span class="sxs-lookup"><span data-stu-id="c1209-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="c1209-136">Например для nuget.org отчетов о нарушении шаблона выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c1209-136">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="c1209-137">Если реализация клиента должен отображать ссылку на форму отчета о нарушении для NuGet.Versioning 4.3.0, он бы привести следующий URL-адрес и предоставляют их пользователю:</span><span class="sxs-lookup"><span data-stu-id="c1209-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
