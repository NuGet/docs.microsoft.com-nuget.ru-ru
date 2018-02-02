---
title: "Общие сведения о размещении своих веб-каналов NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Общие сведения о локальном или удаленном размещении своих веб-каналов пакетов NuGet или коллекций."
keywords: "веб-канал NuGet, коллекция NuGet, настраиваемый веб-канал пакетов, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 738190e20603046d075faa3f50402601890583c1
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2018
---
# <a name="hosting-your-own-nuget-feeds"></a><span data-ttu-id="042bc-104">Размещение своих веб-каналов NuGet</span><span class="sxs-lookup"><span data-stu-id="042bc-104">Hosting your own NuGet feeds</span></span>

<span data-ttu-id="042bc-105">Вместо того, чтобы делать пакеты общедоступными, вам может потребоваться выпустить их лишь для ограниченного круга пользователей, например вашей организации или рабочей группы.</span><span class="sxs-lookup"><span data-stu-id="042bc-105">Instead of making packages publicly available, you might want to release packages to only a limited audience, such as your organization or workgroup.</span></span> <span data-ttu-id="042bc-106">Кроме того, некоторым организациям может потребоваться ограничить доступные их разработчикам сторонние библиотеки, то есть предоставить в их распоряжение ограниченный источник пакетов, а не весь сайт nuget.org.</span><span class="sxs-lookup"><span data-stu-id="042bc-106">In addition, some companies may want to restrict which third-party libraries their developers may use, and thus direct those developers to draw from a limited package source rather than nuget.org.</span></span>

<span data-ttu-id="042bc-107">Для этого NuGet позволяет настроить частные источники пакетов одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="042bc-107">For all such purposes, NuGet supports setting up private package sources in the following ways:</span></span>

- <span data-ttu-id="042bc-108">Локальный веб-канал: пакеты просто помещаются в подходящую сетевую общую папку. Оптимальнее всего для этого использовать `nuget init` и `nuget add`, чтобы создать иерархическую структуру папок (NuGet 3.3+).</span><span class="sxs-lookup"><span data-stu-id="042bc-108">Local feed: Packages are simply placed on a suitable network file share, ideally using `nuget init` and `nuget add` to create a hierarchical folder structure (NuGet 3.3+).</span></span> <span data-ttu-id="042bc-109">Дополнительные сведения см. в разделе [Локальные веб-каналы](../hosting-packages/local-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="042bc-109">For details, see [Local Feeds](../hosting-packages/local-feeds.md).</span></span>
- <span data-ttu-id="042bc-110">NuGet.Server: пакеты предоставляются через локальный HTTP-сервер.</span><span class="sxs-lookup"><span data-stu-id="042bc-110">NuGet.Server: Packages are made available through a local HTTP server.</span></span> <span data-ttu-id="042bc-111">Дополнительные сведения см. в разделе [NuGet.Server](../hosting-packages/nuget-server.md).</span><span class="sxs-lookup"><span data-stu-id="042bc-111">For details, see [NuGet.Server](../hosting-packages/nuget-server.md).</span></span>
- <span data-ttu-id="042bc-112">Коллекция NuGet: пакеты размещаются на интернет-сервере с помощью [проекта коллекции NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span><span class="sxs-lookup"><span data-stu-id="042bc-112">NuGet Gallery: Packages are hosted on an Internet server using the [NuGet Gallery Project](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span></span> <span data-ttu-id="042bc-113">Коллекция NuGet позволяет управлять пользователями и предоставляет такие функции, как расширенный пользовательский веб-интерфейс, позволяющий искать и просматривать пакеты с помощью браузера, аналогично nuget.org.</span><span class="sxs-lookup"><span data-stu-id="042bc-113">NuGet Gallery provides user management and features such as an extensive web UI that allows searching and exploring packages from within the browser, similar to nuget.org.</span></span>

<span data-ttu-id="042bc-114">Существует несколько других продуктов для размещения NuGet, которые поддерживают удаленные закрытые веб-каналы, включая следующие:</span><span class="sxs-lookup"><span data-stu-id="042bc-114">There are also several other NuGet hosting products that support remote private feeds, including the following:</span></span>

- <span data-ttu-id="042bc-115">[Управление пакетами Visual Studio Team Services](https://www.visualstudio.com/docs/package/nuget/publish), которое также доступно в Team Foundation Server 2017 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="042bc-115">[Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), which is also available on Team Foundation Server 2017 and later.</span></span>
- [<span data-ttu-id="042bc-116">MyGet</span><span class="sxs-lookup"><span data-stu-id="042bc-116">MyGet</span></span>](http://myget.org)
- <span data-ttu-id="042bc-117">[ProGet](http://inedo.com/proget) от Inedo</span><span class="sxs-lookup"><span data-stu-id="042bc-117">[ProGet](http://inedo.com/proget) from Inedo</span></span>
- <span data-ttu-id="042bc-118">[Сервер NuGet](http://nugetserver.net/) — проект сообщества от Inedo</span><span class="sxs-lookup"><span data-stu-id="042bc-118">[NuGet Server](http://nugetserver.net/), a community project from Inedo</span></span>
- <span data-ttu-id="042bc-119">[Сервер NuGet (открытый исходный код)](http://nuget-server.net) — реализация, аналогичная серверу NuGet от Inedo, с открытым исходным кодом</span><span class="sxs-lookup"><span data-stu-id="042bc-119">[NuGet Server (Open Source)](http://nuget-server.net), an open-source implementation similar to Inedo's NuGet Server</span></span>
- <span data-ttu-id="042bc-120">[Artifactory](https://www.jfrog.com/artifactory/) от JFrog.</span><span class="sxs-lookup"><span data-stu-id="042bc-120">[Artifactory](https://www.jfrog.com/artifactory/) from JFrog.</span></span>
- <span data-ttu-id="042bc-121">[Nexus](http://www.sonatype.org/nexus/) от Sonatype.</span><span class="sxs-lookup"><span data-stu-id="042bc-121">[Nexus](http://www.sonatype.org/nexus/) from Sonatype.</span></span>
- <span data-ttu-id="042bc-122">[TeamCity](https://www.jetbrains.com/teamcity/) от JetBrains.</span><span class="sxs-lookup"><span data-stu-id="042bc-122">[TeamCity](https://www.jetbrains.com/teamcity/) from JetBrains.</span></span>

<span data-ttu-id="042bc-123">Независимо от способа размещения пакетов доступ к ним осуществляется путем добавления их в список доступных источников в `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="042bc-123">Regardless of how packages are hosted, you access them by adding them to the list of available sources in `NuGet.Config`.</span></span> <span data-ttu-id="042bc-124">Это можно сделать в Visual Studio, как описано в разделе [Источники пакетов](../tools/package-manager-ui.md#package-sources), или из командной строки с помощью [`nuget sources`](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="042bc-124">This can be done in Visual Studio as described in [Package Sources](../tools/package-manager-ui.md#package-sources), or from the command line using [`nuget sources`](../tools/cli-ref-sources.md).</span></span> <span data-ttu-id="042bc-125">Путь к источнику может быть путем к локальной папке, сетевым именем или URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="042bc-125">The path to a source can be a local folder pathname, a network name, or a URL.</span></span>
