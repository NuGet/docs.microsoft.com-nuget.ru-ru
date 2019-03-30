---
title: Шаблон URL-адреса сведения для пакета, NuGet API
description: Сведения о URL-адрес шаблона пакета позволяет клиентам для отображения в их пользовательского интерфейса, веб-ссылки на дополнительные сведения о пакете
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638081"
---
# <a name="package-details-url-template"></a><span data-ttu-id="5045d-103">Шаблона URL-адрес сведений о пакете</span><span class="sxs-lookup"><span data-stu-id="5045d-103">Package details URL template</span></span>

<span data-ttu-id="5045d-104">Вполне возможно, для клиента, чтобы сформировать URL-адрес, который может использоваться пользователем, чтобы просмотреть дополнительные сведения о пакете веб-обозревателя.</span><span class="sxs-lookup"><span data-stu-id="5045d-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="5045d-105">Это полезно при источник пакетов для отображения дополнительных сведений о пакете, который может не поместиться в пределах показывает NuGet клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="5045d-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="5045d-106">Ресурс, используемый для сборки этот URL-адрес является `PackageDetailsUriTemplate` найти ресурс в [индекс службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="5045d-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="5045d-107">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="5045d-107">Versioning</span></span>

<span data-ttu-id="5045d-108">Следующие `@type` значения используются:</span><span class="sxs-lookup"><span data-stu-id="5045d-108">The following `@type` values are used:</span></span>

<span data-ttu-id="5045d-109">Значение@type </span><span class="sxs-lookup"><span data-stu-id="5045d-109">@type value</span></span>                     | <span data-ttu-id="5045d-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="5045d-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="5045d-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="5045d-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="5045d-112">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="5045d-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="5045d-113">Шаблон URL-адреса</span><span class="sxs-lookup"><span data-stu-id="5045d-113">URL template</span></span>

<span data-ttu-id="5045d-114">URL-адрес для следующего API — это значение `@id` свойства, связанные с одной из упомянутых выше ресурсов `@type` значения.</span><span class="sxs-lookup"><span data-stu-id="5045d-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="5045d-115">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="5045d-115">HTTP methods</span></span>

<span data-ttu-id="5045d-116">Несмотря на то, что клиент не предназначен для выполнения запросов к URL-адрес пакета сведения от имени пользователя, веб-страницы должен поддерживать `GET` метод, чтобы легко открыть в веб-браузере щелкнули URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="5045d-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="5045d-117">Создать URL-адрес</span><span class="sxs-lookup"><span data-stu-id="5045d-117">Construct the URL</span></span>

<span data-ttu-id="5045d-118">Учитывая известные ИД и версию пакета, реализация клиента можно создать URL-адрес, используемый для доступа к веб-интерфейс.</span><span class="sxs-lookup"><span data-stu-id="5045d-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="5045d-119">Реализация клиента отображать этот построенный URL-адрес (или активную ссылку) для пользователя, позволяющий открыть веб-браузер на URL-адрес и Дополнительные сведения о пакете.</span><span class="sxs-lookup"><span data-stu-id="5045d-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="5045d-120">Содержимое странице сведений о пакете определяется в реализации сервера.</span><span class="sxs-lookup"><span data-stu-id="5045d-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="5045d-121">URL-адрес должен быть абсолютный URL-адрес и схема (протокол) должна быть HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5045d-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="5045d-122">Значение `@id` в службе индекса является URL-адрес строка, содержащая любой из следующих токенов заполнитель:</span><span class="sxs-lookup"><span data-stu-id="5045d-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="5045d-123">Местозаполнители URL-адресов</span><span class="sxs-lookup"><span data-stu-id="5045d-123">URL placeholders</span></span>

<span data-ttu-id="5045d-124">name</span><span class="sxs-lookup"><span data-stu-id="5045d-124">Name</span></span>        | <span data-ttu-id="5045d-125">Тип</span><span class="sxs-lookup"><span data-stu-id="5045d-125">Type</span></span>    | <span data-ttu-id="5045d-126">Обязательно</span><span class="sxs-lookup"><span data-stu-id="5045d-126">Required</span></span> | <span data-ttu-id="5045d-127">Примечания</span><span class="sxs-lookup"><span data-stu-id="5045d-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="5045d-128">string</span><span class="sxs-lookup"><span data-stu-id="5045d-128">string</span></span>  | <span data-ttu-id="5045d-129">Нет</span><span class="sxs-lookup"><span data-stu-id="5045d-129">no</span></span>       | <span data-ttu-id="5045d-130">Идентификатор пакета, чтобы получить подробные сведения о</span><span class="sxs-lookup"><span data-stu-id="5045d-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="5045d-131">string</span><span class="sxs-lookup"><span data-stu-id="5045d-131">string</span></span>  | <span data-ttu-id="5045d-132">Нет</span><span class="sxs-lookup"><span data-stu-id="5045d-132">no</span></span>       | <span data-ttu-id="5045d-133">Чтобы получить подробные сведения о версии пакета</span><span class="sxs-lookup"><span data-stu-id="5045d-133">The package version to get details for</span></span>

<span data-ttu-id="5045d-134">Сервер должен принимать `{id}` и `{version}` значения в любом регистре.</span><span class="sxs-lookup"><span data-stu-id="5045d-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="5045d-135">Кроме того, сервер не должен быть чувствительно к версиях [нормализованное](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="5045d-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="5045d-136">Другими словами, сервер должен принимать также принимают версии не было нормализовано.</span><span class="sxs-lookup"><span data-stu-id="5045d-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="5045d-137">Например шаблон сведения пакета nuget.org выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5045d-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="5045d-138">Если реализация клиента должен отображать ссылку на сведения о пакете для NuGet.Versioning 4.3.0, он бы привести следующий URL-адрес и предоставляют их пользователю:</span><span class="sxs-lookup"><span data-stu-id="5045d-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
