---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427119"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="05a15-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="05a15-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="05a15-103">Обоснование</span><span class="sxs-lookup"><span data-stu-id="05a15-103">Rationale</span></span>

<span data-ttu-id="05a15-104">С появлением [выражений лицензии](../reference/nuspec.md#license) были определены требования, подразумевающие реализацию надежной службы, которая могла бы предоставлять справочный текст для отдельных идентификаторов лицензий и исключений, а также для выражений лицензии.</span><span class="sxs-lookup"><span data-stu-id="05a15-104">With the introduction of the [license expressions](../reference/nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="05a15-105">Кроме того, такая служба должна иметь надежную схему URL-адресов, которая может обеспечить обработку устаревающих ссылок и гарантировать обратную совместимость для более старых версий клиента.</span><span class="sxs-lookup"><span data-stu-id="05a15-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="05a15-106">Эту роль играет раздел licenses.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="05a15-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="05a15-107">Этот раздел сайта Nuget.org представляет текст лицензии для ссылок на пакеты, в котором с помощью выражений лицензии определяются условия лицензирования.</span><span class="sxs-lookup"><span data-stu-id="05a15-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="05a15-108">Команда `nuget pack` или упаковка вместе с другими [клиентскими средствами](../install-nuget-client-tools.md) позволяют задать для элемента [`licenseUrl`](../reference/nuspec.md#licenseurl) указатель на раздел licenses.nuget.org, который обеспечивает обратную совместимость с клиентами более старых версий, не поддерживающими элемент `license`.</span><span class="sxs-lookup"><span data-stu-id="05a15-108">`nuget pack` or packing with other [client tools](../install-nuget-client-tools.md) set the [`licenseUrl`](../reference/nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="05a15-109">Протокол</span><span class="sxs-lookup"><span data-stu-id="05a15-109">Protocol</span></span>

<span data-ttu-id="05a15-110">Раздел licenses.nuget.org предназначен для пользователей, работающих в браузере, и не генерирует ответов в распознаваемом компьютером виде.</span><span class="sxs-lookup"><span data-stu-id="05a15-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="05a15-111">Для работы используется протокол HTTPS, а запросы должны иметь определенную конструкцию.</span><span class="sxs-lookup"><span data-stu-id="05a15-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="05a15-112">Поддерживаются только запросы `GET`.</span><span class="sxs-lookup"><span data-stu-id="05a15-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="05a15-113">В качестве входных данных принимаются выражения лицензии или идентификаторы исключений, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="05a15-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="05a15-114">Обратите внимание, что все элементы выражений лицензии задаются с учетом регистра символов. Таким образом, это ограничение применяется ко всем входным данным для раздела licenses.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="05a15-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="05a15-115">Выражения лицензии</span><span class="sxs-lookup"><span data-stu-id="05a15-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="05a15-116">Запрос</span><span class="sxs-lookup"><span data-stu-id="05a15-116">Request</span></span>

<span data-ttu-id="05a15-117">Выражения лицензии (включая простейшие случаи, когда выражения состоят из одной лицензии), должны [кодироваться как URL-адреса](https://tools.ietf.org/html/rfc3986#section-2.1) и использоваться в качестве пути в запросе к разделу licenses.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="05a15-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="05a15-118">Выражение лицензии</span><span class="sxs-lookup"><span data-stu-id="05a15-118">License expression</span></span> | <span data-ttu-id="05a15-119">Используемый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="05a15-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="05a15-120">MIT</span><span class="sxs-lookup"><span data-stu-id="05a15-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="05a15-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="05a15-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="05a15-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span><span class="sxs-lookup"><span data-stu-id="05a15-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="05a15-123">Эта служба поддерживает только идентификаторы лицензий и исключений лицензий, которые принимаются сайтом nuget.org. Все выражения лицензии, которые содержат неподдерживаемые идентификаторы лицензий или исключений лицензий, либо не соответствуют синтаксису выражения лицензии, считаются недопустимыми.</span><span class="sxs-lookup"><span data-stu-id="05a15-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="05a15-124">Ответ</span><span class="sxs-lookup"><span data-stu-id="05a15-124">Response</span></span>

<span data-ttu-id="05a15-125">Раздел licenses.nuget.org в ответ на запросы, содержащие допустимые выражения лицензии, отправляет код состояния HTTP 200 и веб-страницу с описанием выражения лицензии:</span><span class="sxs-lookup"><span data-stu-id="05a15-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="05a15-126">если предоставленное выражение лицензии содержит один идентификатор лицензии, возвращается веб-страница, которая содержит соответствующий справочный текст лицензии;</span><span class="sxs-lookup"><span data-stu-id="05a15-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="05a15-127">если предоставленное выражение описывает составное выражение лицензии, возвращается веб-страница с выражением лицензии и ссылками на отдельные лицензии или исключения лицензии.</span><span class="sxs-lookup"><span data-stu-id="05a15-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="05a15-128">При получении любых запросов, содержащих недопустимые выражения лицензии, возвращается ответ HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="05a15-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="05a15-129">Исключения лицензии</span><span class="sxs-lookup"><span data-stu-id="05a15-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="05a15-130">Запрос</span><span class="sxs-lookup"><span data-stu-id="05a15-130">Request</span></span>

<span data-ttu-id="05a15-131">Идентификаторы исключений лицензии должны кодироваться как URL-адреса и использоваться в качестве пути в запросе к разделу licenses.nuget.org. В одном запросе может быть предоставлен только один идентификатор исключения лицензии.</span><span class="sxs-lookup"><span data-stu-id="05a15-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="05a15-132">В части пути URL-адреса не допускаются никакие дополнительные символы, за исключением идентификатора исключения лицензии.</span><span class="sxs-lookup"><span data-stu-id="05a15-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="05a15-133">Идентификатор исключения лицензии</span><span class="sxs-lookup"><span data-stu-id="05a15-133">License exception identifier</span></span> | <span data-ttu-id="05a15-134">Используемый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="05a15-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="05a15-135">FLTK-exception</span><span class="sxs-lookup"><span data-stu-id="05a15-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="05a15-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="05a15-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="05a15-137">Ответ</span><span class="sxs-lookup"><span data-stu-id="05a15-137">Response</span></span>

<span data-ttu-id="05a15-138">Раздел licenses.nuget.org в ответ на запрос, содержащий известный идентификатор исключения лицензии, возвращает ответ HTTP 200 и веб-страницу, содержащую справочный текст для указанного исключения лицензии.</span><span class="sxs-lookup"><span data-stu-id="05a15-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="05a15-139">При получении любого запроса, содержащего неподдерживаемый идентификатор исключения лицензии, возвращается ответ HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="05a15-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>