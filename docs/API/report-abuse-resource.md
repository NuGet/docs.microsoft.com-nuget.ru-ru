---
title: "Отчет о нарушении URL-адрес шаблона NuGet интерфейса API | Документы Microsoft"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 148d743a-09e5-4539-8454-675be11902db
description: "Шаблон URL-адреса отчета о нарушении позволяет клиентам отображать ссылку на отчет о нарушении в их пользовательского интерфейса."
keywords: "Сообщить о нарушении NuGet интерфейса API, NuGet API файл политикам, NuGet.org шаблон URL-адреса отчета"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7b3413297f5a7fcf0e2c7757036b1f240ed0058a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="dd271-104">Шаблон URL-адреса отчета о нарушении</span><span class="sxs-lookup"><span data-stu-id="dd271-104">Report Abuse URL Template</span></span>

<span data-ttu-id="dd271-105">Существует возможность для клиента для построения URL-адрес, который может использоваться пользователем для сообщения о нарушении о определенного пакета.</span><span class="sxs-lookup"><span data-stu-id="dd271-105">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="dd271-106">Это полезно в том случае, когда источник пакета хочет обеспечить всех клиентов (даже третьих сторон) для делегирования отчетов о нарушении в исходную папку пакета.</span><span class="sxs-lookup"><span data-stu-id="dd271-106">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="dd271-107">Ресурс, используемый для получения содержимого пакета — `ReportAbuseUriTemplate` найти ресурс в [служба индекс](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="dd271-107">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="dd271-108">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="dd271-108">Versioning</span></span>

<span data-ttu-id="dd271-109">Следующие `@type` используются значения:</span><span class="sxs-lookup"><span data-stu-id="dd271-109">The following `@type` values are used:</span></span>

<span data-ttu-id="dd271-110">Значение @type</span><span class="sxs-lookup"><span data-stu-id="dd271-110">@type value</span></span>                       | <span data-ttu-id="dd271-111">Примечания</span><span class="sxs-lookup"><span data-stu-id="dd271-111">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="dd271-112">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="dd271-112">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="dd271-113">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="dd271-113">The initial release</span></span>
<span data-ttu-id="dd271-114">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="dd271-114">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="dd271-115">Псевдоним`ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="dd271-115">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="dd271-116">Шаблон URL-адреса</span><span class="sxs-lookup"><span data-stu-id="dd271-116">URL template</span></span>

<span data-ttu-id="dd271-117">URL-адрес для следующего API — это значение `@id` свойства, связанные с одной из упомянутых выше ресурсов `@type` значения.</span><span class="sxs-lookup"><span data-stu-id="dd271-117">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="dd271-118">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="dd271-118">HTTP methods</span></span>

<span data-ttu-id="dd271-119">Несмотря на то, что клиент не предназначен для выполнения запросов по URL-адресу отчетов о нарушении от имени пользователя, веб-страницы должны поддерживать `GET` метод, чтобы легко открыть в браузере пользователь щелкнул URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="dd271-119">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="dd271-120">Создать URL-адрес</span><span class="sxs-lookup"><span data-stu-id="dd271-120">Construct the URL</span></span>

<span data-ttu-id="dd271-121">Имея известные ИД и версию пакета, реализация клиента позволяет создавать URL-адрес, используемый для доступа к веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="dd271-121">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="dd271-122">Реализация клиента должно отображаться это сконструированный URL-адрес (или активную ссылку) для пользователей, позволяя им, чтобы откройте веб-браузер на URL-адрес и внесите любые необходимые о нарушении отчета.</span><span class="sxs-lookup"><span data-stu-id="dd271-122">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="dd271-123">Реализация формы отчетов о нарушении определяется реализация сервера.</span><span class="sxs-lookup"><span data-stu-id="dd271-123">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="dd271-124">Значение `@id` представляет собой строку URL-адрес содержит любые из следующих токенов заполнитель:</span><span class="sxs-lookup"><span data-stu-id="dd271-124">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="dd271-125">Местозаполнители URL-адресов</span><span class="sxs-lookup"><span data-stu-id="dd271-125">URL placeholders</span></span>

<span data-ttu-id="dd271-126">Имя</span><span class="sxs-lookup"><span data-stu-id="dd271-126">Name</span></span>        | <span data-ttu-id="dd271-127">Тип</span><span class="sxs-lookup"><span data-stu-id="dd271-127">Type</span></span>    | <span data-ttu-id="dd271-128">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dd271-128">Required</span></span> | <span data-ttu-id="dd271-129">Примечания</span><span class="sxs-lookup"><span data-stu-id="dd271-129">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="dd271-130">string</span><span class="sxs-lookup"><span data-stu-id="dd271-130">string</span></span>  | <span data-ttu-id="dd271-131">Нет</span><span class="sxs-lookup"><span data-stu-id="dd271-131">no</span></span>       | <span data-ttu-id="dd271-132">Идентификатор пакета для сообщения о нарушении для</span><span class="sxs-lookup"><span data-stu-id="dd271-132">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="dd271-133">string</span><span class="sxs-lookup"><span data-stu-id="dd271-133">string</span></span>  | <span data-ttu-id="dd271-134">Нет</span><span class="sxs-lookup"><span data-stu-id="dd271-134">no</span></span>       | <span data-ttu-id="dd271-135">Версия пакета для сообщения о нарушении для</span><span class="sxs-lookup"><span data-stu-id="dd271-135">The package version to report abuse for</span></span>

<span data-ttu-id="dd271-136">`{id}` И `{version}` значения интерпретируются реализация сервера должен быть регистра без учета регистра и не подвержены ли Нормализованная версия.</span><span class="sxs-lookup"><span data-stu-id="dd271-136">The `{id}` and `{version}` values interpreted by the server implementation must be case insenstive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="dd271-137">Например nuget.org отчетов о нарушении шаблона выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="dd271-137">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="dd271-138">Если реализация клиента должна отображать ссылку на форму отчета о нарушении для NuGet.Versioning 4.3.0, он бы привести следующий URL-адрес и предоставить его для пользователя:</span><span class="sxs-lookup"><span data-stu-id="dd271-138">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```