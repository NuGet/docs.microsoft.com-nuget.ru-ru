---
title: Пакет SDK клиента NuGet
description: API развивается и еще не документирован, но примеры доступны в блоге Дейв Гликк.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: a5c542379318f24ee35ccf25651d0e8de91253ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231244"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="c2884-103">Пакет SDK клиента NuGet</span><span class="sxs-lookup"><span data-stu-id="c2884-103">NuGet Client SDK</span></span>

<span data-ttu-id="c2884-104">*Пакет SDK клиента NuGet* ссылается на группу пакетов NuGet:</span><span class="sxs-lookup"><span data-stu-id="c2884-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="c2884-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) — используется для взаимодействия с веб-каналами NuGet и файлов на основе HTTP</span><span class="sxs-lookup"><span data-stu-id="c2884-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="c2884-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) — используется для взаимодействия с пакетами NuGet.</span><span class="sxs-lookup"><span data-stu-id="c2884-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="c2884-107">`NuGet.Protocol` зависит от этого пакета</span><span class="sxs-lookup"><span data-stu-id="c2884-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="c2884-108">Исходный код для этих пакетов можно найти в репозитории GitHub для [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) .</span><span class="sxs-lookup"><span data-stu-id="c2884-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="c2884-109">Документацию по протоколу сервера NuGet см. в [API сервера NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="c2884-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="c2884-110">Начало работы</span><span class="sxs-lookup"><span data-stu-id="c2884-110">Getting started</span></span>

### <a name="install-the-package"></a><span data-ttu-id="c2884-111">Установка пакета</span><span class="sxs-lookup"><span data-stu-id="c2884-111">Install the package</span></span>

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a><span data-ttu-id="c2884-112">Примеры</span><span class="sxs-lookup"><span data-stu-id="c2884-112">Examples</span></span>

<span data-ttu-id="c2884-113">Эти примеры можно найти в проекте [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="c2884-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="c2884-114">Список версий пакета</span><span class="sxs-lookup"><span data-stu-id="c2884-114">List package versions</span></span>

<span data-ttu-id="c2884-115">Найдите все версии Newtonsoft. JSON с помощью [API содержимого пакета NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="c2884-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="c2884-116">Скачать пакет</span><span class="sxs-lookup"><span data-stu-id="c2884-116">Download a package</span></span>

<span data-ttu-id="c2884-117">Скачайте Newtonsoft. JSON v 12.0.1 с помощью [API содержимого пакета NuGet v3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="c2884-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="c2884-118">Получение метаданных пакета</span><span class="sxs-lookup"><span data-stu-id="c2884-118">Get package metadata</span></span>

<span data-ttu-id="c2884-119">Получите метаданные для пакета "Newtonsoft. JSON" с помощью [API метаданных пакета NuGet v3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="c2884-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="c2884-120">Поиск пакетов</span><span class="sxs-lookup"><span data-stu-id="c2884-120">Search packages</span></span>

<span data-ttu-id="c2884-121">Поиск пакетов "JSON" с помощью [API поиска NuGet v3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="c2884-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a><span data-ttu-id="c2884-122">Документация по сторонним производителям</span><span class="sxs-lookup"><span data-stu-id="c2884-122">Third-party documentation</span></span>

<span data-ttu-id="c2884-123">Примеры и документацию для некоторых API-интерфейсов можно найти в следующем ряде блогов: Дейв Гликк, Опубликовано 2016.</span><span class="sxs-lookup"><span data-stu-id="c2884-123">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="c2884-124">Изучение библиотек NuGet версии 3, часть 1. Введение и основные понятия</span><span class="sxs-lookup"><span data-stu-id="c2884-124">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="c2884-125">Изучение библиотек NuGet версии 3. часть 2. Поиск пакетов</span><span class="sxs-lookup"><span data-stu-id="c2884-125">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="c2884-126">Изучение библиотек NuGet v3, часть 3. Установка пакетов</span><span class="sxs-lookup"><span data-stu-id="c2884-126">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="c2884-127">Эти записи блога были написаны вскоре после выпуска **3.4.3** версии пакетов SDK клиента NuGet.</span><span class="sxs-lookup"><span data-stu-id="c2884-127">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="c2884-128">Более новые версии пакетов могут быть несовместимы с данными в записях блога.</span><span class="sxs-lookup"><span data-stu-id="c2884-128">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="c2884-129">Бжöркстрöм в блоге Дейв Гликк, где появился другой подход к использованию пакета SDK клиента NuGet для установки пакетов NuGet:</span><span class="sxs-lookup"><span data-stu-id="c2884-129">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="c2884-130">Повторное посещение библиотек NuGet v3</span><span class="sxs-lookup"><span data-stu-id="c2884-130">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
