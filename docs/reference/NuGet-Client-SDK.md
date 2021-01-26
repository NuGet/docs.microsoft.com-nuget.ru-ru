---
title: Пакет SDK для клиента NuGet
description: API развивается и еще не документирован, но примеры доступны в блоге Дейв Гликк.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: e89b50601deb204892536406b4ddabf7005e0642
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776131"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="e360d-103">Пакет SDK для клиента NuGet</span><span class="sxs-lookup"><span data-stu-id="e360d-103">NuGet Client SDK</span></span>

<span data-ttu-id="e360d-104">*Пакет SDK клиента NuGet* ссылается на группу пакетов NuGet:</span><span class="sxs-lookup"><span data-stu-id="e360d-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="e360d-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) — Используется для взаимодействия с веб-каналами NuGet и на основе файлов.</span><span class="sxs-lookup"><span data-stu-id="e360d-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="e360d-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) — Используется для взаимодействия с пакетами NuGet.</span><span class="sxs-lookup"><span data-stu-id="e360d-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="e360d-107">`NuGet.Protocol` зависит от этого пакета</span><span class="sxs-lookup"><span data-stu-id="e360d-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="e360d-108">Исходный код для этих пакетов можно найти в репозитории GitHub для [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) .</span><span class="sxs-lookup"><span data-stu-id="e360d-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>
<span data-ttu-id="e360d-109">Исходный код для этих примеров можно найти в проекте [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="e360d-109">You can find the source code for these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

> [!Note]
> <span data-ttu-id="e360d-110">Документацию по протоколу сервера NuGet см. в [API сервера NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="e360d-110">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="nugetprotocol"></a><span data-ttu-id="e360d-111">NuGet. Protocol</span><span class="sxs-lookup"><span data-stu-id="e360d-111">NuGet.Protocol</span></span>

<span data-ttu-id="e360d-112">Установите `NuGet.Protocol` пакет для взаимодействия с веб-каналами пакетов NuGet на основе HTTP и папок.</span><span class="sxs-lookup"><span data-stu-id="e360d-112">Install the `NuGet.Protocol` package to interact with HTTP and folder-based NuGet package feeds:</span></span>

```ps1
dotnet add package NuGet.Protocol
```

### <a name="list-package-versions"></a><span data-ttu-id="e360d-113">Список версий пакета</span><span class="sxs-lookup"><span data-stu-id="e360d-113">List package versions</span></span>

<span data-ttu-id="e360d-114">Найдите все версии Newtonsoft.Jsс помощью [API содержимого пакета NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="e360d-114">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="e360d-115">Скачать пакет</span><span class="sxs-lookup"><span data-stu-id="e360d-115">Download a package</span></span>

<span data-ttu-id="e360d-116">Скачайте Newtonsoft.Jsна v 12.0.1 с помощью [API содержимого пакета NuGet v3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="e360d-116">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="e360d-117">Получение метаданных пакета</span><span class="sxs-lookup"><span data-stu-id="e360d-117">Get package metadata</span></span>

<span data-ttu-id="e360d-118">Получите метаданные для пакета "Newtonsoft.Jsдля" с помощью [API метаданных пакета NuGet v3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="e360d-118">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="e360d-119">Поиск пакетов</span><span class="sxs-lookup"><span data-stu-id="e360d-119">Search packages</span></span>

<span data-ttu-id="e360d-120">Поиск пакетов "JSON" с помощью [API поиска NuGet v3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="e360d-120">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a><span data-ttu-id="e360d-121">Отправка пакета</span><span class="sxs-lookup"><span data-stu-id="e360d-121">Push a package</span></span>

<span data-ttu-id="e360d-122">Отправка пакета с помощью [API-интерфейса NuGet v3 Push and Delete](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="e360d-122">Push a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a><span data-ttu-id="e360d-123">Удаление пакета</span><span class="sxs-lookup"><span data-stu-id="e360d-123">Delete a package</span></span>

<span data-ttu-id="e360d-124">Удаление пакета с помощью [API-интерфейса NuGet v3 Push and Delete](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="e360d-124">Delete a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

> [!Note]
> <span data-ttu-id="e360d-125">Серверы NuGet могут интерпретировать запрос на удаление пакета как «жесткое удаление», «обратимое удаление» или «удалить список».</span><span class="sxs-lookup"><span data-stu-id="e360d-125">NuGet servers are free to interpret a package delete request as a "hard delete", "soft delete", or "unlist".</span></span>
> <span data-ttu-id="e360d-126">Например, nuget.org интерпретирует запрос на удаление пакета как "unlist".</span><span class="sxs-lookup"><span data-stu-id="e360d-126">For example, nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="e360d-127">Дополнительные сведения об этом практическом занятии см. в разделе [Удаление политик пакетов](../nuget-org/policies/deleting-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="e360d-127">For more information about this practice, see the [Deleting Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span>

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a><span data-ttu-id="e360d-128">Работа с веб-каналами с проверкой подлинности</span><span class="sxs-lookup"><span data-stu-id="e360d-128">Work with authenticated feeds</span></span>

<span data-ttu-id="e360d-129">Используется [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) для работы с веб-каналами с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="e360d-129">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) to work with authenticated feeds.</span></span>

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a><span data-ttu-id="e360d-130">NuGet. Упаковка</span><span class="sxs-lookup"><span data-stu-id="e360d-130">NuGet.Packaging</span></span>

<span data-ttu-id="e360d-131">Установите `NuGet.Packaging` пакет для взаимодействия с `.nupkg` файлами и `.nuspec` из потока:</span><span class="sxs-lookup"><span data-stu-id="e360d-131">Install the `NuGet.Packaging` package to interact with `.nupkg` and `.nuspec` files from a stream:</span></span>

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a><span data-ttu-id="e360d-132">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="e360d-132">Create a package</span></span>

<span data-ttu-id="e360d-133">Создание пакета, Установка метаданных и Добавление зависимостей с помощью [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="e360d-133">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e360d-134">Настоятельно рекомендуется создавать пакеты NuGet с помощью официального инструментария NuGet, а **не** использовать этот низкоуровневый API.</span><span class="sxs-lookup"><span data-stu-id="e360d-134">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="e360d-135">Существует множество характеристик, важных для правильно сформированного пакета, и последняя версия инструментов помогает реализовать эти рекомендации.</span><span class="sxs-lookup"><span data-stu-id="e360d-135">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="e360d-136">Дополнительные сведения о создании пакетов NuGet см. в обзоре [рабочего процесса создания пакета](../create-packages/overview-and-workflow.md) и документации по официальному набору средств для работы с пакетами (например, [с помощью DotNet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="e360d-136">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="e360d-137">Чтение пакета</span><span class="sxs-lookup"><span data-stu-id="e360d-137">Read a package</span></span>

<span data-ttu-id="e360d-138">Чтение пакета из файлового потока с помощью [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="e360d-138">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="e360d-139">Документация по сторонним производителям</span><span class="sxs-lookup"><span data-stu-id="e360d-139">Third-party documentation</span></span>

<span data-ttu-id="e360d-140">Примеры и документацию для некоторых API-интерфейсов можно найти в следующем ряде блогов: Дейв Гликк, Опубликовано 2016.</span><span class="sxs-lookup"><span data-stu-id="e360d-140">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="e360d-141">Изучение библиотек NuGet версии 3, часть 1. Введение и основные понятия</span><span class="sxs-lookup"><span data-stu-id="e360d-141">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="e360d-142">Изучение библиотек NuGet версии 3. часть 2. Поиск пакетов</span><span class="sxs-lookup"><span data-stu-id="e360d-142">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="e360d-143">Изучение библиотек NuGet v3, часть 3. Установка пакетов</span><span class="sxs-lookup"><span data-stu-id="e360d-143">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="e360d-144">Эти записи блога были написаны вскоре после выпуска **3.4.3** версии пакетов SDK клиента NuGet.</span><span class="sxs-lookup"><span data-stu-id="e360d-144">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="e360d-145">Более новые версии пакетов могут быть несовместимы с данными в записях блога.</span><span class="sxs-lookup"><span data-stu-id="e360d-145">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="e360d-146">Бжöркстрöм в блоге Дейв Гликк, где появился другой подход к использованию пакета SDK клиента NuGet для установки пакетов NuGet:</span><span class="sxs-lookup"><span data-stu-id="e360d-146">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="e360d-147">Повторное посещение библиотек NuGet v3</span><span class="sxs-lookup"><span data-stu-id="e360d-147">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
