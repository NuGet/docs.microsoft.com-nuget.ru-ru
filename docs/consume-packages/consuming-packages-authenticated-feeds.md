---
title: Использование пакетов из веб-каналов, прошедших проверку подлинности
description: Использование пакетов из веб-каналов, прошедших проверку подлинности, во всех сценариях клиента NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: e76fefaf4d3c86aa15cf279090c0adb8ed779aab
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901516"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="f31b8-103">Использование пакетов из веб-каналов, прошедших проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="f31b8-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="f31b8-104">Кроме [общедоступного веб-канала](https://api.nuget.org/v3/index.json) nuget.org клиенты NuGet могут взаимодействовать с веб-каналами файлов и частными веб-каналами HTTP.</span><span class="sxs-lookup"><span data-stu-id="f31b8-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="f31b8-105">Для проверки подлинности с использованием частных веб-каналов HTTP применяются два подхода:</span><span class="sxs-lookup"><span data-stu-id="f31b8-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="f31b8-106">Добавление учетных данных в [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span><span class="sxs-lookup"><span data-stu-id="f31b8-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="f31b8-107">Проверка подлинности с использованием одной из многих моделей расширяемости в зависимости от применяемого клиента.</span><span class="sxs-lookup"><span data-stu-id="f31b8-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="f31b8-108">Расширяемость проверки подлинности клиентов NuGet</span><span class="sxs-lookup"><span data-stu-id="f31b8-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="f31b8-109">Для различных клиентов NuGet за проверку подлинности отвечает сам поставщик частных веб-каналов.</span><span class="sxs-lookup"><span data-stu-id="f31b8-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="f31b8-110">Все клиенты NuGet имеют методы расширения для поддержки этой возможности.</span><span class="sxs-lookup"><span data-stu-id="f31b8-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="f31b8-111">Это либо расширение Visual Studio, либо подключаемый модуль, которые могут взаимодействовать с NuGet для получения учетных данных.</span><span class="sxs-lookup"><span data-stu-id="f31b8-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="f31b8-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f31b8-112">Visual Studio</span></span>

<span data-ttu-id="f31b8-113">В Visual Studio NuGet предоставляет интерфейс, который поставщики веб-каналов могут реализовывать и предоставлять своим клиентам.</span><span class="sxs-lookup"><span data-stu-id="f31b8-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="f31b8-114">Дополнительные сведения см. в документации по [созданию поставщика учетных данных Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span><span class="sxs-lookup"><span data-stu-id="f31b8-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="f31b8-115">Доступные поставщики учетных данных NuGet для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f31b8-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="f31b8-116">Существует поставщик учетных данных, встроенный в Visual Studio для поддержки Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="f31b8-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="f31b8-117">Доступные поставщики учетных данных подключаемых модулей:</span><span class="sxs-lookup"><span data-stu-id="f31b8-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="f31b8-118">Поставщик учетных данных MyGet для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f31b8-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="f31b8-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="f31b8-119">nuget.exe</span></span>

<span data-ttu-id="f31b8-120">Когда средству `nuget.exe` требуются учетные данные для проверки подлинности в веб-канале, оно ищет их следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f31b8-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="f31b8-121">Поиск учетных данных в файлах `NuGet.config`.</span><span class="sxs-lookup"><span data-stu-id="f31b8-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="f31b8-122">Использование поставщиков учетных данных подключаемых модулей версии 2.</span><span class="sxs-lookup"><span data-stu-id="f31b8-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="f31b8-123">Использование поставщиков учетных данных подключаемых модулей версии 1.</span><span class="sxs-lookup"><span data-stu-id="f31b8-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="f31b8-124">Затем NuGet запрашивает у пользователя учетные данные в командной строке.</span><span class="sxs-lookup"><span data-stu-id="f31b8-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="f31b8-125">Поставщики учетных данных nuget.exe и версии 2</span><span class="sxs-lookup"><span data-stu-id="f31b8-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="f31b8-126">В версии `4.8` NuGet определяет новый механизм подключаемого модуля проверки подлинности, который далее называется поставщиками учетных данных версии 2.</span><span class="sxs-lookup"><span data-stu-id="f31b8-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="f31b8-127">Сведения об установке и обнаружении этих поставщиков см. в разделе [Кроссплатформенные подключаемые модули NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="f31b8-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="f31b8-128">Поставщики учетных данных nuget.exe и версии 1</span><span class="sxs-lookup"><span data-stu-id="f31b8-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="f31b8-129">В версии `3.3` NuGet представляет первую версию подключаемых модулей проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f31b8-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="f31b8-130">Сведения об установке и обнаружении этих поставщиков см. в разделе [Поставщики учетных данных nuget.exe](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery).</span><span class="sxs-lookup"><span data-stu-id="f31b8-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="f31b8-131">Доступные поставщики учетных данных для nuget.exe</span><span class="sxs-lookup"><span data-stu-id="f31b8-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="f31b8-132">[Поставщики учетных данных версии 2 Azure DevOps](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) или [Поставщик учетных данных Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="f31b8-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="f31b8-133">В Visual Studio 2017 версии 15.9 и более поздней поставщик учетных данных Azure DevOps входит в состав Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f31b8-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="f31b8-134">Если `nuget.exe` использует MSBuild из этого конкретного набора инструментов Visual Studio, подключаемый модуль будет обнаружен автоматически.</span><span class="sxs-lookup"><span data-stu-id="f31b8-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="f31b8-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="f31b8-135">dotnet.exe</span></span>

<span data-ttu-id="f31b8-136">Когда средству `dotnet.exe` требуются учетные данные для проверки подлинности в веб-канале, оно ищет их следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f31b8-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="f31b8-137">Поиск учетных данных в файлах `NuGet.config`.</span><span class="sxs-lookup"><span data-stu-id="f31b8-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="f31b8-138">Использование поставщиков учетных данных подключаемых модулей версии 2.</span><span class="sxs-lookup"><span data-stu-id="f31b8-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="f31b8-139">По умолчанию `dotnet.exe` не является интерактивным, поэтому может потребоваться передать флаг `--interactive`, чтобы обеспечить блокировку для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f31b8-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="f31b8-140">Поставщики учетных данных dotnet.exe и версии 2</span><span class="sxs-lookup"><span data-stu-id="f31b8-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="f31b8-141">В версии `2.2.100` пакета SDK NuGet определяет механизм подключаемого модуля проверки подлинности, который работает во всех клиентах.</span><span class="sxs-lookup"><span data-stu-id="f31b8-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="f31b8-142">Сведения об установке и обнаружении этих поставщиков см. в разделе [Кроссплатформенные подключаемые модули NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="f31b8-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="f31b8-143">Доступные поставщики учетных данных для dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="f31b8-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="f31b8-144">Поставщик учетных данных Azure Artifacts</span><span class="sxs-lookup"><span data-stu-id="f31b8-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="f31b8-145">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="f31b8-145">MSBuild.exe</span></span>

<span data-ttu-id="f31b8-146">Когда средству `MSBuild.exe` требуются учетные данные для проверки подлинности в веб-канале, оно ищет их следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f31b8-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="f31b8-147">Поиск учетных данных в файлах `NuGet.config`.</span><span class="sxs-lookup"><span data-stu-id="f31b8-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="f31b8-148">Использование поставщиков учетных данных подключаемых модулей версии 2.</span><span class="sxs-lookup"><span data-stu-id="f31b8-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="f31b8-149">По умолчанию `MSBuild.exe` не является интерактивным, поэтому может потребоваться задать свойство `/p:NuGetInteractive=true`, чтобы обеспечить блокировку для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f31b8-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="f31b8-150">Поставщики учетных данных MSBuild.exe и версии 2</span><span class="sxs-lookup"><span data-stu-id="f31b8-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="f31b8-151">В Visual Studio 2019 с обновлением 9 NuGet определяет механизм подключаемого модуля проверки подлинности, который работает во всех клиентах.</span><span class="sxs-lookup"><span data-stu-id="f31b8-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="f31b8-152">Сведения об установке и обнаружении этих поставщиков см. в разделе [Кроссплатформенные подключаемые модули NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="f31b8-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="f31b8-153">Доступные поставщики учетных данных для MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="f31b8-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="f31b8-154">Поставщик учетных данных Azure Artifacts</span><span class="sxs-lookup"><span data-stu-id="f31b8-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="f31b8-155">В Visual Studio 2017 с обновлением 9 и более поздней поставщик учетных данных Azure DevOps входит в состав Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f31b8-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="f31b8-156">Дополнительные действия не требуются.</span><span class="sxs-lookup"><span data-stu-id="f31b8-156">No additional steps are required.</span></span>
