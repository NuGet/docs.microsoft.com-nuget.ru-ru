---
title: Общие сведения о сайте NuGet.org
description: Общие сведения о сайте NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 2dac6ebd6367f3ed1a5ef9e81d843867a4a22f62
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901880"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="724af-103">Общие сведения о сайте NuGet.org</span><span class="sxs-lookup"><span data-stu-id="724af-103">Overview of NuGet.org</span></span>

<span data-ttu-id="724af-104">NuGet.org — это общедоступный центр для размещения пакетов NuGet, который ежедневно посещают миллионы разработчиков приложений на платформах .NET и .NET Core.</span><span class="sxs-lookup"><span data-stu-id="724af-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="724af-105">Роль сайта NuGet.org в экосистеме NuGet</span><span class="sxs-lookup"><span data-stu-id="724af-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="724af-106">Как общедоступный центр NuGet.org содержит центральный репозиторий с более 100 000 уникальных пакетов, доступными по адресу [nuget.org](https://www.nuget.org). NuGet.org — это не единственный центр для размещения пакетов.</span><span class="sxs-lookup"><span data-stu-id="724af-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="724af-107">Благодаря технологии NuGet вы можете хранить пакеты в частном облаке (например, в Azure DevOps), частной сети или даже локальной файловой системе.</span><span class="sxs-lookup"><span data-stu-id="724af-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="724af-108">Если вы хотите использовать другой центр или способ размещения, ознакомьтесь со статьей [Размещение своих веб-каналов NuGet](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="724af-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="724af-109">NuGet.org, как и любой другой центр размещения пакетов NuGet, выступает в качестве точки подключения между *создателями* и *потребителями* пакета.</span><span class="sxs-lookup"><span data-stu-id="724af-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="724af-110">Создатели разрабатывают полезные пакеты NuGet и публикуют их.</span><span class="sxs-lookup"><span data-stu-id="724af-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="724af-111">Потребители ищут полезные и совместимые пакеты на доступных узлах, скачивая эти пакеты и включая их в свои проекты.</span><span class="sxs-lookup"><span data-stu-id="724af-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="724af-112">После установки в проекте API пакеты становятся доступны остальной части кода проекта.</span><span class="sxs-lookup"><span data-stu-id="724af-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![Связь между создателями, узлами и потребителями пакета](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="724af-114">Учетные записи</span><span class="sxs-lookup"><span data-stu-id="724af-114">Accounts</span></span>

<span data-ttu-id="724af-115">Чтобы публиковать пакеты на сайте NuGet.org, сначала вам необходимо создать [индивидуальную (пользовательскую) учетную запись](individual-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="724af-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="724af-116">Она будет использоваться в качестве вашего удостоверения на сайте NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="724af-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="724af-117">Кроме того, на сайте NuGet.org можно создать [учетную запись организации](organizations-on-nuget-org.md).</span><span class="sxs-lookup"><span data-stu-id="724af-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="724af-118">В учетную запись организации могут входить в качестве членов одна или несколько индивидуальных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="724af-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="724af-119">Эти члены могут управлять набором пакетов, используя для этого единое удостоверение владельца.</span><span class="sxs-lookup"><span data-stu-id="724af-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="724af-120">Ваша индивидуальная учетная запись может являться членом любого количества учетных записей организации.</span><span class="sxs-lookup"><span data-stu-id="724af-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="724af-121">Пакет может принадлежать учетной записи организации так же, как и индивидуальной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="724af-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="724af-122">Для потребителей пакета нет никаких различий между индивидуальной учетной записью и учетной записью организации. Обе они отображаются как объекты `owners` для пакета.</span><span class="sxs-lookup"><span data-stu-id="724af-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="724af-123">Ключи API</span><span class="sxs-lookup"><span data-stu-id="724af-123">API keys</span></span>

<span data-ttu-id="724af-124">Получив пакет NuGet (файл *.nupkg*) для публикации, вы можете опубликовать его на сайте NuGet.org с помощью средства CLI nuget.exe или dotnet.exe, используя [ключ API](scoped-api-keys.md), полученный на этом сайте.</span><span class="sxs-lookup"><span data-stu-id="724af-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="724af-125">При [публикации пакета](../create-packages/creating-a-package.md) значение ключа API указывается в команде CLI.</span><span class="sxs-lookup"><span data-stu-id="724af-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="724af-126">Префиксы идентификаторов</span><span class="sxs-lookup"><span data-stu-id="724af-126">ID prefixes</span></span>

<span data-ttu-id="724af-127">Чтобы сохранить и защитить собственное удостоверение при публикации пакетов, вы можете [зарезервировать префиксы идентификаторов](id-prefix-reservation.md).</span><span class="sxs-lookup"><span data-stu-id="724af-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="724af-128">При установке пакета его потребители получают дополнительную информацию о том, что в идентифицирующих свойствах пакета содержатся соответствующие действительности данные.</span><span class="sxs-lookup"><span data-stu-id="724af-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="724af-129">Конечная точка API для сайта NuGet.org</span><span class="sxs-lookup"><span data-stu-id="724af-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="724af-130">Чтобы использовать NuGet.org в качестве репозитория пакетов в клиентах NuGet, вам нужна следующая конечная точка API версии 3:</span><span class="sxs-lookup"><span data-stu-id="724af-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="724af-131">Клиенты более старых версий могут по-прежнему использовать протокол версии 2 для доступа к NuGet.org. Однако обратите внимание, что клиенты NuGet версии 3.0 и выше будут работать с протоколом версии 2 медленнее и с меньшей надежностью.</span><span class="sxs-lookup"><span data-stu-id="724af-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="724af-132">`https://www.nuget.org/api/v2` (**Протокол версии 2 является нерекомендуемым!** )</span><span class="sxs-lookup"><span data-stu-id="724af-132">`https://www.nuget.org/api/v2` (**The V2 protocol is deprecated!**)</span></span>
