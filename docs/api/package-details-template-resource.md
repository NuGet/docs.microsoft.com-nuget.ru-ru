---
title: Шаблон URL-адреса сведений о пакете, API NuGet
description: Шаблон URL сведений о пакете позволяет клиентам отображать в пользовательском интерфейсе веб-ссылку на дополнительные сведения о пакете.
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: aaeedea9750c11099b34e927bd8442656839d784
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773954"
---
# <a name="package-details-url-template"></a><span data-ttu-id="770a0-103">Шаблон URL-адреса сведений о пакете</span><span class="sxs-lookup"><span data-stu-id="770a0-103">Package details URL template</span></span>

<span data-ttu-id="770a0-104">Клиент может создать URL-адрес, который будет использоваться пользователем для просмотра дополнительных сведений о пакете в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="770a0-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="770a0-105">Это полезно, когда источник пакета хочет показать дополнительные сведения о пакете, который может не попадать в область действия клиентского приложения NuGet.</span><span class="sxs-lookup"><span data-stu-id="770a0-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="770a0-106">Ресурс, используемый для создания этого URL-адреса, — это `PackageDetailsUriTemplate` ресурс, найденный в [индексе службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="770a0-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="770a0-107">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="770a0-107">Versioning</span></span>

<span data-ttu-id="770a0-108">Используются следующие `@type` значения:</span><span class="sxs-lookup"><span data-stu-id="770a0-108">The following `@type` values are used:</span></span>

<span data-ttu-id="770a0-109">Значение @type</span><span class="sxs-lookup"><span data-stu-id="770a0-109">@type value</span></span>                     | <span data-ttu-id="770a0-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="770a0-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="770a0-111">Паккажедетаилсуритемплате/5.1.0</span><span class="sxs-lookup"><span data-stu-id="770a0-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="770a0-112">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="770a0-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="770a0-113">Шаблон URL-адреса</span><span class="sxs-lookup"><span data-stu-id="770a0-113">URL template</span></span>

<span data-ttu-id="770a0-114">URL-адрес следующего API — это значение `@id` свойства, связанное с одним из вышеупомянутых `@type` значений ресурсов.</span><span class="sxs-lookup"><span data-stu-id="770a0-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="770a0-115">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="770a0-115">HTTP methods</span></span>

<span data-ttu-id="770a0-116">Хотя клиент не предназначен для выполнения запросов к URL-адресу сведений о пакете от имени пользователя, веб-страница должна поддерживать метод, `GET` позволяющий легко открывать URL-адреса, открытые в браузере.</span><span class="sxs-lookup"><span data-stu-id="770a0-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="770a0-117">Создание URL-адреса</span><span class="sxs-lookup"><span data-stu-id="770a0-117">Construct the URL</span></span>

<span data-ttu-id="770a0-118">При наличии известного идентификатора и версии пакета реализация клиента может создать URL-адрес, используемый для доступа к веб-интерфейсу.</span><span class="sxs-lookup"><span data-stu-id="770a0-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="770a0-119">Реализация клиента должна отображать этот сконструированный URL-адрес (или щелкнув ссылку) для пользователя, который позволяет ему открыть веб-браузер с URL-адресом и получить дополнительные сведения о пакете.</span><span class="sxs-lookup"><span data-stu-id="770a0-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="770a0-120">Содержимое страницы сведений о пакете определяется реализацией сервера.</span><span class="sxs-lookup"><span data-stu-id="770a0-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="770a0-121">URL-адрес должен быть абсолютным URL-адресом, а схема (протокол) должна быть HTTPS.</span><span class="sxs-lookup"><span data-stu-id="770a0-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="770a0-122">Значение `@id` в индексе службы является строкой URL-адреса, содержащей любой из следующих маркеров заполнителя:</span><span class="sxs-lookup"><span data-stu-id="770a0-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="770a0-123">Заполнители URL-адресов</span><span class="sxs-lookup"><span data-stu-id="770a0-123">URL placeholders</span></span>

<span data-ttu-id="770a0-124">Имя</span><span class="sxs-lookup"><span data-stu-id="770a0-124">Name</span></span>        | <span data-ttu-id="770a0-125">Тип</span><span class="sxs-lookup"><span data-stu-id="770a0-125">Type</span></span>    | <span data-ttu-id="770a0-126">Обязательно</span><span class="sxs-lookup"><span data-stu-id="770a0-126">Required</span></span> | <span data-ttu-id="770a0-127">Примечания</span><span class="sxs-lookup"><span data-stu-id="770a0-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="770a0-128">строка</span><span class="sxs-lookup"><span data-stu-id="770a0-128">string</span></span>  | <span data-ttu-id="770a0-129">нет</span><span class="sxs-lookup"><span data-stu-id="770a0-129">no</span></span>       | <span data-ttu-id="770a0-130">Идентификатор пакета для получения сведений</span><span class="sxs-lookup"><span data-stu-id="770a0-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="770a0-131">строка</span><span class="sxs-lookup"><span data-stu-id="770a0-131">string</span></span>  | <span data-ttu-id="770a0-132">нет</span><span class="sxs-lookup"><span data-stu-id="770a0-132">no</span></span>       | <span data-ttu-id="770a0-133">Версия пакета для получения сведений</span><span class="sxs-lookup"><span data-stu-id="770a0-133">The package version to get details for</span></span>

<span data-ttu-id="770a0-134">Сервер должен принимать `{id}` значения и `{version}` с любым регистром.</span><span class="sxs-lookup"><span data-stu-id="770a0-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="770a0-135">Кроме того, сервер не должен быть чувствительным к [нормализации](../concepts/package-versioning.md#normalized-version-numbers)версии.</span><span class="sxs-lookup"><span data-stu-id="770a0-135">In addition, the server should not be sensitive to whether the version is [normalized](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="770a0-136">Другими словами, сервер должен принять также и ненормализованные версии.</span><span class="sxs-lookup"><span data-stu-id="770a0-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="770a0-137">Например, шаблон сведений о пакете NuGet. org выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="770a0-137">For example, nuget.org's package details template looks like this:</span></span>

```http
https://www.nuget.org/packages/{id}/{version}
```

<span data-ttu-id="770a0-138">Если клиентская реализация должна отобразить ссылку на сведения о пакете для NuGet. Управление версиями 4.3.0, он создаст следующий URL-адрес и предоставит его пользователю:</span><span class="sxs-lookup"><span data-stu-id="770a0-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```http
https://www.nuget.org/packages/NuGet.Versioning/4.3.0
```
