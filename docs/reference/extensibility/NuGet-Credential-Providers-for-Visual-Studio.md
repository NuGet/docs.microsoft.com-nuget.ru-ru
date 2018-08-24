---
title: Поставщики учетных данных NuGet для Visual Studio
description: Поставщики учетных данных NuGet пройти проверку подлинности с веб-каналами путем реализации интерфейса IVsCredentialProvider в расширении Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e8d8ae22300b55b93badb65864163d959105dca2
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/23/2018
ms.locfileid: "42793907"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="220fe-103">Проверка подлинности веб-каналов в Visual Studio с помощью поставщиков учетных данных NuGet</span><span class="sxs-lookup"><span data-stu-id="220fe-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="220fe-104">Расширение NuGet Visual Studio 3.6 + поддерживает поставщиков учетных данных, которые позволяют NuGet для работы с каналы с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="220fe-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="220fe-105">После установки поставщика учетных данных NuGet для Visual Studio, расширение NuGet для Visual Studio автоматически получать и обновлять учетные данные для каналы с проверкой подлинности при необходимости.</span><span class="sxs-lookup"><span data-stu-id="220fe-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="220fe-106">Пример реализации можно найти в [пример VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="220fe-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="220fe-107">Начиная с 4.8 + NuGet в Visual Studio поддерживает новый кроссплатформенный проверки подлинности подключаемые модули также, но они не рекомендуемый подход для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="220fe-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="220fe-108">Поставщики учетных данных NuGet для Visual Studio должен быть установлен как регулярное расширение Visual Studio и потребует [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="220fe-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="220fe-109">Поставщики учетных данных NuGet для Visual Studio работает только в Visual Studio (не в команда dotnet restore или nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="220fe-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="220fe-110">Поставщики учетных данных с помощью nuget.exe, см. в разделе [поставщиков учетных данных nuget.exe](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="220fe-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="220fe-111">Учетные данные поставщиков в dotnet и msbuild см. в разделе [NuGet кросс-подключаемые модули платформы](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="220fe-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="220fe-112">Доступные поставщики учетных данных NuGet для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="220fe-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="220fe-113">Нет поставщика учетных данных, встроенные в расширение Visual Studio NuGet поддерживает Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="220fe-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="220fe-114">Расширение NuGet Visual Studio использует внутренний `VsCredentialProviderImporter` которой также начинает проверку поставщики подключаемый модуль учетных данных.</span><span class="sxs-lookup"><span data-stu-id="220fe-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="220fe-115">Эти поставщики подключаемый модуль учетных данных должны быть обнаруживаемыми как Экспорт MEF типа `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="220fe-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="220fe-116">Поставщики доступных подключаемый модуль учетных данных:</span><span class="sxs-lookup"><span data-stu-id="220fe-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="220fe-117">Поставщик учетных данных MyGet для Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="220fe-117">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="220fe-118">Создание поставщика учетных данных NuGet для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="220fe-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="220fe-119">Расширение NuGet Visual Studio 3.6 + реализует внутренний CredentialService, который используется для получения учетных данных.</span><span class="sxs-lookup"><span data-stu-id="220fe-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="220fe-120">CredentialService имеет список встроенных и подключаемый модуль учетных данных поставщиков.</span><span class="sxs-lookup"><span data-stu-id="220fe-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="220fe-121">Каждый поставщик применяется последовательно, пока не полученные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="220fe-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="220fe-122">При приобретении учетных данных учетных данных служба попробует поставщиков учетных данных в следующем порядке, остановка, как только полученные учетные данные:</span><span class="sxs-lookup"><span data-stu-id="220fe-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="220fe-123">Учетные данные будут получены из файлов конфигурации NuGet (с помощью встроенной `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="220fe-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="220fe-124">Если источник пакета в Visual Studio Team Services, `VisualStudioAccountProvider` будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="220fe-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="220fe-125">Все другие подключаемый модуль Visual Studio поставщики учетных данных будет выполнена последовательно.</span><span class="sxs-lookup"><span data-stu-id="220fe-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="220fe-126">Попробуйте использовать все NuGet кросс-поставщики учетных данных платформы последовательно.</span><span class="sxs-lookup"><span data-stu-id="220fe-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="220fe-127">Если учетные данные не получены, пользователю предлагается ввести учетные данные, используя диалоговое окно стандартных обычной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="220fe-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="220fe-128">Реализация IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="220fe-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="220fe-129">Чтобы создать поставщик удостоверений NuGet для Visual Studio, создать расширение Visual Studio, предоставляющий открытый MEF-Экспорт реализация `IVsCredentialProvider` введите и соответствуют принципам, описанным ниже.</span><span class="sxs-lookup"><span data-stu-id="220fe-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

<span data-ttu-id="220fe-130">Пример реализации можно найти в [пример VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="220fe-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="220fe-131">Каждый поставщик учетных данных NuGet для Visual Studio необходимо:</span><span class="sxs-lookup"><span data-stu-id="220fe-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="220fe-132">Определите, может ли его предоставлять учетные данные для целевого URI перед запуском получение учетных данных.</span><span class="sxs-lookup"><span data-stu-id="220fe-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="220fe-133">Если поставщик не может предоставить учетные данные для источника, то он должен вернуть `null`.</span><span class="sxs-lookup"><span data-stu-id="220fe-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="220fe-134">Если поставщик обрабатывать запросы для целевой URI, но не может предоставить учетные данные, должно вызываться исключение.</span><span class="sxs-lookup"><span data-stu-id="220fe-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="220fe-135">Необходимо реализовать пользовательский поставщик учетных данных NuGet для Visual Studio `IVsCredentialProvider` интерфейс, доступный в [NuGet.VisualStudio пакета](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="220fe-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="220fe-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="220fe-136">GetCredentialAsync</span></span>

| <span data-ttu-id="220fe-137">Входной параметр</span><span class="sxs-lookup"><span data-stu-id="220fe-137">Input Parameter</span></span> |<span data-ttu-id="220fe-138">Описание:</span><span class="sxs-lookup"><span data-stu-id="220fe-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="220fe-139">URI uri</span><span class="sxs-lookup"><span data-stu-id="220fe-139">Uri uri</span></span> | <span data-ttu-id="220fe-140">Uri источника пакета, для которого запрашиваются учетные данные.</span><span class="sxs-lookup"><span data-stu-id="220fe-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="220fe-141">IWebProxy прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="220fe-141">IWebProxy proxy</span></span> | <span data-ttu-id="220fe-142">Веб-прокси, который используется для связи в сети.</span><span class="sxs-lookup"><span data-stu-id="220fe-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="220fe-143">Значение NULL, если проверка подлинности прокси-сервер не настроен.</span><span class="sxs-lookup"><span data-stu-id="220fe-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="220fe-144">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="220fe-144">bool isProxyRequest</span></span> | <span data-ttu-id="220fe-145">Значение true, если этот запрос для получения учетных данных проверки подлинности прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="220fe-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="220fe-146">Если реализация не является допустимым для получения учетных данных прокси-сервера, должны быть возвращено значение null.</span><span class="sxs-lookup"><span data-stu-id="220fe-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="220fe-147">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="220fe-147">bool isRetry</span></span> | <span data-ttu-id="220fe-148">Значение true, если учетные данные ранее запрошенные для данного универсального кода ресурса, но предоставленные учетные данные не разрешает авторизованного доступа.</span><span class="sxs-lookup"><span data-stu-id="220fe-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="220fe-149">Неинтерактивная bool</span><span class="sxs-lookup"><span data-stu-id="220fe-149">bool nonInteractive</span></span> | <span data-ttu-id="220fe-150">Значение true, если поставщик учетных данных необходимо отключить все запросы пользователю и вместо этого используйте значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="220fe-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="220fe-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="220fe-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="220fe-152">Этот токен отмены должен проверить, чтобы определить, если учетные данные запрашивающего операция была отменена.</span><span class="sxs-lookup"><span data-stu-id="220fe-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="220fe-153">**Возвращаемое значение**: объект учетных данных, реализующий интерфейс [ `System.Net.ICredentials` интерфейс](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="220fe-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
