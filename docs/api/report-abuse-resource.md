---
title: Шаблон URL-адреса сообщения о нарушении, API NuGet
description: Шаблон URL-адреса отчета о нарушении позволяет клиентам отображать ссылку на сообщение о нарушении в пользовательском интерфейсе.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775229"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="e9d98-103">Шаблон URL-адреса сообщения о нарушении</span><span class="sxs-lookup"><span data-stu-id="e9d98-103">Report abuse URL template</span></span>

<span data-ttu-id="e9d98-104">Клиент может создать URL-адрес, который будет использоваться пользователем для сообщения о нарушении конкретного пакета.</span><span class="sxs-lookup"><span data-stu-id="e9d98-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="e9d98-105">Это полезно, когда источник пакета хочет включить все клиентские возможности (даже сторонние) для делегирования отчетов о нарушении в источник пакета.</span><span class="sxs-lookup"><span data-stu-id="e9d98-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="e9d98-106">Ресурс, используемый для создания этого URL-адреса, — это `ReportAbuseUriTemplate` ресурс, найденный в [индексе службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="e9d98-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="e9d98-107">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="e9d98-107">Versioning</span></span>

<span data-ttu-id="e9d98-108">Используются следующие `@type` значения:</span><span class="sxs-lookup"><span data-stu-id="e9d98-108">The following `@type` values are used:</span></span>

<span data-ttu-id="e9d98-109">Значение @type</span><span class="sxs-lookup"><span data-stu-id="e9d98-109">@type value</span></span>                       | <span data-ttu-id="e9d98-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="e9d98-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="e9d98-111">Репортабусеуритемплате/3.0.0 — бета-версия</span><span class="sxs-lookup"><span data-stu-id="e9d98-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="e9d98-112">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="e9d98-112">The initial release</span></span>
<span data-ttu-id="e9d98-113">Репортабусеуритемплате/3.0.0-RC</span><span class="sxs-lookup"><span data-stu-id="e9d98-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="e9d98-114">Псевдоним `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="e9d98-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="e9d98-115">Шаблон URL-адреса</span><span class="sxs-lookup"><span data-stu-id="e9d98-115">URL template</span></span>

<span data-ttu-id="e9d98-116">URL-адрес следующего API — это значение `@id` свойства, связанное с одним из вышеупомянутых `@type` значений ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e9d98-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e9d98-117">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="e9d98-117">HTTP methods</span></span>

<span data-ttu-id="e9d98-118">Хотя клиент не предназначен для выполнения запросов к URL-адресу сообщения о нарушении по имени пользователя, веб-страница должна поддерживать `GET` метод, позволяющий легко открывать URL-адреса, открытые в браузере.</span><span class="sxs-lookup"><span data-stu-id="e9d98-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="e9d98-119">Создание URL-адреса</span><span class="sxs-lookup"><span data-stu-id="e9d98-119">Construct the URL</span></span>

<span data-ttu-id="e9d98-120">При наличии известного идентификатора и версии пакета реализация клиента может создать URL-адрес, используемый для доступа к веб-интерфейсу.</span><span class="sxs-lookup"><span data-stu-id="e9d98-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="e9d98-121">Реализация клиента должна отображать этот сконструированный URL-адрес (или щелчок ссылки) для пользователя, который позволяет открывать веб-браузер по URL-адресу и создавать все необходимые отчеты о нарушениях.</span><span class="sxs-lookup"><span data-stu-id="e9d98-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="e9d98-122">Реализация формы отчета о нарушении определяется реализацией сервера.</span><span class="sxs-lookup"><span data-stu-id="e9d98-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="e9d98-123">Значение `@id` является строкой URL-адреса, содержащей любой из следующих маркеров заполнителя:</span><span class="sxs-lookup"><span data-stu-id="e9d98-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="e9d98-124">Заполнители URL-адресов</span><span class="sxs-lookup"><span data-stu-id="e9d98-124">URL placeholders</span></span>

<span data-ttu-id="e9d98-125">Имя</span><span class="sxs-lookup"><span data-stu-id="e9d98-125">Name</span></span>        | <span data-ttu-id="e9d98-126">Тип</span><span class="sxs-lookup"><span data-stu-id="e9d98-126">Type</span></span>    | <span data-ttu-id="e9d98-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e9d98-127">Required</span></span> | <span data-ttu-id="e9d98-128">Примечания</span><span class="sxs-lookup"><span data-stu-id="e9d98-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="e9d98-129">строка</span><span class="sxs-lookup"><span data-stu-id="e9d98-129">string</span></span>  | <span data-ttu-id="e9d98-130">нет</span><span class="sxs-lookup"><span data-stu-id="e9d98-130">no</span></span>       | <span data-ttu-id="e9d98-131">Идентификатор пакета для сообщения о нарушении</span><span class="sxs-lookup"><span data-stu-id="e9d98-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="e9d98-132">строка</span><span class="sxs-lookup"><span data-stu-id="e9d98-132">string</span></span>  | <span data-ttu-id="e9d98-133">нет</span><span class="sxs-lookup"><span data-stu-id="e9d98-133">no</span></span>       | <span data-ttu-id="e9d98-134">Версия пакета для сообщения о нарушении</span><span class="sxs-lookup"><span data-stu-id="e9d98-134">The package version to report abuse for</span></span>

<span data-ttu-id="e9d98-135">`{id}`Значения и, `{version}` интерпретируемые реализацией сервера, должны учитывать регистр и не учитывать, является ли версия нормализованной.</span><span class="sxs-lookup"><span data-stu-id="e9d98-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="e9d98-136">Например, шаблон "отчет о нарушении" в NuGet. org выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e9d98-136">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="e9d98-137">Если клиентская реализация должна отобразить ссылку на форму сообщения о нарушении для NuGet. Управление версиями 4.3.0, он выдаст следующий URL-адрес и предоставит его пользователю:</span><span class="sxs-lookup"><span data-stu-id="e9d98-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
