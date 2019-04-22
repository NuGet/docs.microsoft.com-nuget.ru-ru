---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 4a40cc1f7d333e8d35a721f3eed2e6b9365faf7b
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/18/2019
ms.locfileid: "58921563"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="a524d-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="a524d-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="a524d-103">Обоснование</span><span class="sxs-lookup"><span data-stu-id="a524d-103">Rationale</span></span>

<span data-ttu-id="a524d-104">С появлением [лицензии выражения](nuspec.md#license), появилось является обязательным для надежной службы, которая могла бы предоставить текст ссылки для выражений лицензии, идентификаторы исключение или идентификаторы отдельных лицензий.</span><span class="sxs-lookup"><span data-stu-id="a524d-104">With the introduction of the [license expressions](nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="a524d-105">Еще одно требование для этой службы является стабильной схему URL-адрес, который не подвержена воздействию связать rot, таким образом, можно безопасно использовать их для обеспечения обратной совместимости для старых клиентов.</span><span class="sxs-lookup"><span data-stu-id="a524d-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="a524d-106">Licenses.NuGet.org выполняет эту роль.</span><span class="sxs-lookup"><span data-stu-id="a524d-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="a524d-107">NuGet.org использует ее для предоставления данная текстовая ссылка лицензии для пакетов, которые указывают лицензии с помощью выражения лицензии.</span><span class="sxs-lookup"><span data-stu-id="a524d-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="a524d-108">`nuget pack` или упаковки с другими [клиентские средства](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) задать [ `licenseUrl` ](nuspec.md#licenseurl) указывающий licenses.nuget.org для обеспечения обратной совместимости со старыми клиентами, которые не поддерживают `license` элемент.</span><span class="sxs-lookup"><span data-stu-id="a524d-108">`nuget pack` or packing with other [client tools](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) set the [`licenseUrl`](nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="a524d-109">Протокол</span><span class="sxs-lookup"><span data-stu-id="a524d-109">Protocol</span></span>

<span data-ttu-id="a524d-110">Licenses.NuGet.org предназначена для просмотра пользователями в своих браузерах, предоставляются машиночитаемый ответов.</span><span class="sxs-lookup"><span data-stu-id="a524d-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="a524d-111">Необходимо использовать протокол HTTPS, и запросы должны создаваться определенным образом.</span><span class="sxs-lookup"><span data-stu-id="a524d-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="a524d-112">Он поддерживает только `GET` запросов.</span><span class="sxs-lookup"><span data-stu-id="a524d-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="a524d-113">Он принимает выражения лицензии или лицензии исключение идентификаторов в качестве входных данных в виде указанных ниже.</span><span class="sxs-lookup"><span data-stu-id="a524d-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="a524d-114">Обратите внимание, что все элементы выражений лицензии чувствительны к регистру, и таким образом все входные данные для licenses.nuget.org учитывается регистр символов также.</span><span class="sxs-lookup"><span data-stu-id="a524d-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="a524d-115">Выражения лицензии</span><span class="sxs-lookup"><span data-stu-id="a524d-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="a524d-116">Запрос</span><span class="sxs-lookup"><span data-stu-id="a524d-116">Request</span></span>

<span data-ttu-id="a524d-117">Выражения лицензии (включая тривиальные случаев, когда выражение состоит из одной лицензией) должны быть [URL-адреса](https://tools.ietf.org/html/rfc3986#section-2.1) и использоваться в качестве пути в запросе к licenses.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a524d-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="a524d-118">Выражение лицензии</span><span class="sxs-lookup"><span data-stu-id="a524d-118">License expression</span></span> | <span data-ttu-id="a524d-119">URL-адрес для использования</span><span class="sxs-lookup"><span data-stu-id="a524d-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="a524d-120">MIT</span><span class="sxs-lookup"><span data-stu-id="a524d-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="a524d-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="a524d-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="a524d-122">(LGPL 2.0 — только с помощью Apache или исключение FLTK-2.0+)</span><span class="sxs-lookup"><span data-stu-id="a524d-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="a524d-123">Служба поддерживает только идентификаторы лицензии и лицензии исключение идентификаторы, которые может принимать nuget.org. Все выражения лицензии, содержащие неподдерживаемые лицензии идентификаторов или идентификаторов исключение лицензии или, которые не соответствуют синтаксис выражений лицензии, считаются недействительными.</span><span class="sxs-lookup"><span data-stu-id="a524d-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="a524d-124">Ответ</span><span class="sxs-lookup"><span data-stu-id="a524d-124">Response</span></span>

<span data-ttu-id="a524d-125">Licenses.NuGet.org отвечает на запросы, содержащие выражения действительной лицензии с кодом состояния HTTP 200 и веб-страницы, содержащая описание выражения лицензии:</span><span class="sxs-lookup"><span data-stu-id="a524d-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="a524d-126">Если указано выражение лицензии содержит идентификатор одну лицензию возврата веб-страницы, содержащий текст ссылки лицензии;</span><span class="sxs-lookup"><span data-stu-id="a524d-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="a524d-127">Если лицензии выражение является выражением составного лицензии, возвращаются веб-страницы, содержащее выражение лицензии со ссылками на отдельные лицензии или лицензии исключение ссылки.</span><span class="sxs-lookup"><span data-stu-id="a524d-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="a524d-128">Любые запросы, содержащие результат выражения недействительную лицензию в ответ HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="a524d-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="a524d-129">Исключения лицензии</span><span class="sxs-lookup"><span data-stu-id="a524d-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="a524d-130">Запрос</span><span class="sxs-lookup"><span data-stu-id="a524d-130">Request</span></span>

<span data-ttu-id="a524d-131">Идентификаторы исключение лицензии должны быть URL-адреса и напрямую используются как пути в запросе к licenses.nuget.org. В одном запросе может быть предоставлен идентификатор исключения только одну лицензию.</span><span class="sxs-lookup"><span data-stu-id="a524d-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="a524d-132">Нет дополнительные символы помимо идентификатор лицензии исключения могут присутствовать в часть пути URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="a524d-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="a524d-133">Идентификатор исключения лицензии</span><span class="sxs-lookup"><span data-stu-id="a524d-133">License exception identifier</span></span> | <span data-ttu-id="a524d-134">URL-адрес для использования</span><span class="sxs-lookup"><span data-stu-id="a524d-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="a524d-135">FLTK-исключение</span><span class="sxs-lookup"><span data-stu-id="a524d-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="a524d-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="a524d-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="a524d-137">Ответ</span><span class="sxs-lookup"><span data-stu-id="a524d-137">Response</span></span>

<span data-ttu-id="a524d-138">Licenses.NuGet.org отвечает на запрос с идентификатором исключения известных лицензии с ответ HTTP 200 и веб-страницы, содержащий текст ссылки для исключения Указанная лицензия.</span><span class="sxs-lookup"><span data-stu-id="a524d-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="a524d-139">Любой запрос, содержащий идентификатор исключения неподдерживаемый лицензии приводит ответ HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="a524d-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>