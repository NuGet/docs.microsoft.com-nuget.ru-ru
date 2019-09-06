---
title: Поставщики учетных данных NuGet для Visual Studio
description: Поставщики учетных данных NuGet проходят проверку подлинности с помощью веб-каналов, реализовав интерфейс Ивскредентиалпровидер в расширении Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 4e781a2462871bceeb1c7f02220320daabdab98a
ms.sourcegitcommit: a0807671386782021acb7588741390e6f07e94e1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/05/2019
ms.locfileid: "70384431"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="148c3-103">Проверка подлинности веб-каналов в Visual Studio с помощью поставщиков учетных данных NuGet</span><span class="sxs-lookup"><span data-stu-id="148c3-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="148c3-104">Расширение NuGet Visual Studio 3.6 + поддерживает поставщиков учетных данных, которые позволяют NuGet работать с веб-каналами с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="148c3-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="148c3-105">После установки поставщика учетных данных NuGet для Visual Studio расширение NuGet для Visual Studio будет автоматически получать и обновлять учетные данные для веб-каналов, прошедших проверку подлинности, по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="148c3-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="148c3-106">Пример реализации можно найти в [примере вскредентиалпровидер](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="148c3-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="148c3-107">Начиная с 4.8 + NuGet в Visual Studio, поддерживаются также новые подключаемые модули многоплатформенной проверки подлинности, но они не являются рекомендуемым подходом для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="148c3-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="148c3-108">Поставщики учетных данных NuGet для Visual Studio должны быть установлены как обычные расширения Visual Studio, и для них потребуется [Visual studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="148c3-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="148c3-109">Поставщики учетных данных NuGet для Visual Studio работают только в Visual Studio (не в dotnet restore или NuGet. exe).</span><span class="sxs-lookup"><span data-stu-id="148c3-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="148c3-110">Сведения о поставщиках учетных данных с помощью NuGet. exe см. в разделе [поставщики учетных данных NuGet. exe](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="148c3-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="148c3-111">Для поставщиков учетных данных в DotNet и MSBuild см. Дополнительные сведения о [подключаемых](nuget-cross-platform-authentication-plugin.md) модулях NuGet.</span><span class="sxs-lookup"><span data-stu-id="148c3-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="148c3-112">Доступные поставщики учетных данных NuGet для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="148c3-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="148c3-113">Существует поставщик учетных данных, встроенный в расширение NuGet Visual Studio для поддержки Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="148c3-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="148c3-114">Расширение NuGet для Visual Studio использует внутренний `VsCredentialProviderImporter` объект, который также сканирует поставщики учетных данных подключаемых модулей.</span><span class="sxs-lookup"><span data-stu-id="148c3-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="148c3-115">Эти поставщики учетных данных подключаемых модулей должны быть обнаруживаемыми в качестве экспорта MEF типа `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="148c3-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="148c3-116">Доступные поставщики учетных данных подключаемых модулей включают:</span><span class="sxs-lookup"><span data-stu-id="148c3-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="148c3-117">Поставщик учетных данных MyGet для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="148c3-117">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="148c3-118">Создание поставщика учетных данных NuGet для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="148c3-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="148c3-119">Расширение NuGet Visual Studio 3.6 и реализует внутренний Кредентиалсервице, используемый для получения учетных данных.</span><span class="sxs-lookup"><span data-stu-id="148c3-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="148c3-120">Кредентиалсервице имеет список встроенных поставщиков учетных данных и подключаемых модулей.</span><span class="sxs-lookup"><span data-stu-id="148c3-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="148c3-121">Каждый поставщик попытается последовательно, пока не будут получены учетные данные.</span><span class="sxs-lookup"><span data-stu-id="148c3-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="148c3-122">При получении учетных данных служба учетных данных попытается использовать поставщики учетных данных в следующем порядке, останавливаясь, как только будут получены учетные данные:</span><span class="sxs-lookup"><span data-stu-id="148c3-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="148c3-123">Учетные данные будут получены из файлов конфигурации NuGet (с помощью встроенной `SettingsCredentialProvider`функции).</span><span class="sxs-lookup"><span data-stu-id="148c3-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="148c3-124">Если источник пакета находится в Visual Studio Team Services, `VisualStudioAccountProvider` будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="148c3-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="148c3-125">Все другие поставщики учетных данных подключаемых модулей Visual Studio будут последовательной попытки.</span><span class="sxs-lookup"><span data-stu-id="148c3-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="148c3-126">Постарайтесь использовать все межплатформенные поставщики учетных данных NuGet последовательно.</span><span class="sxs-lookup"><span data-stu-id="148c3-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="148c3-127">Если учетные данные еще не получены, пользователь получит запрос на ввод учетных данных, используя стандартное диалоговое окно обычной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="148c3-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="148c3-128">Реализация Ивскредентиалпровидер. Жеткредентиалсасинк</span><span class="sxs-lookup"><span data-stu-id="148c3-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="148c3-129">Чтобы создать поставщик учетных данных NuGet для Visual Studio, создайте расширение Visual Studio, которое предоставляет открытый экспорт MEF, реализующий `IVsCredentialProvider` тип, и соответствует описанным ниже принципам.</span><span class="sxs-lookup"><span data-stu-id="148c3-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="148c3-130">Пример реализации можно найти в [примере вскредентиалпровидер](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="148c3-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="148c3-131">Каждый поставщик учетных данных NuGet для Visual Studio должен:</span><span class="sxs-lookup"><span data-stu-id="148c3-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="148c3-132">Определите, может ли он предоставлять учетные данные для целевого URI перед инициацией получения учетных данных.</span><span class="sxs-lookup"><span data-stu-id="148c3-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="148c3-133">Если поставщик не может предоставить учетные данные для целевого источника, он должен вернуть `null`.</span><span class="sxs-lookup"><span data-stu-id="148c3-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="148c3-134">Если поставщик обрабатывает запросы для целевого URI, но не может предоставить учетные данные, должно быть выдано исключение.</span><span class="sxs-lookup"><span data-stu-id="148c3-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="148c3-135">Пользовательский поставщик учетных данных NuGet для Visual Studio должен реализовывать `IVsCredentialProvider` интерфейс, доступный в [пакете NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="148c3-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="148c3-136">жеткредентиаласинк</span><span class="sxs-lookup"><span data-stu-id="148c3-136">GetCredentialAsync</span></span>

| <span data-ttu-id="148c3-137">Входной параметр</span><span class="sxs-lookup"><span data-stu-id="148c3-137">Input Parameter</span></span> |<span data-ttu-id="148c3-138">Описание</span><span class="sxs-lookup"><span data-stu-id="148c3-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="148c3-139">URI URI</span><span class="sxs-lookup"><span data-stu-id="148c3-139">Uri uri</span></span> | <span data-ttu-id="148c3-140">URI источника пакета, для которого запрашиваются учетные данные.</span><span class="sxs-lookup"><span data-stu-id="148c3-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="148c3-141">Прокси-сервер IWebProxy</span><span class="sxs-lookup"><span data-stu-id="148c3-141">IWebProxy proxy</span></span> | <span data-ttu-id="148c3-142">Веб-прокси для использования при обмене данными по сети.</span><span class="sxs-lookup"><span data-stu-id="148c3-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="148c3-143">Значение null, если проверка подлинности прокси-сервера не настроена.</span><span class="sxs-lookup"><span data-stu-id="148c3-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="148c3-144">bool Испроксирекуест</span><span class="sxs-lookup"><span data-stu-id="148c3-144">bool isProxyRequest</span></span> | <span data-ttu-id="148c3-145">Значение true, если этот запрос должен получать учетные данные проверки подлинности прокси.</span><span class="sxs-lookup"><span data-stu-id="148c3-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="148c3-146">Если реализация не является допустимой для получения учетных данных прокси-сервера, то должно возвращаться значение null.</span><span class="sxs-lookup"><span data-stu-id="148c3-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="148c3-147">bool, повтор</span><span class="sxs-lookup"><span data-stu-id="148c3-147">bool isRetry</span></span> | <span data-ttu-id="148c3-148">Значение true, если ранее были запрошены учетные данные для этого URI, но предоставленные учетные данные не позволяли авторизовать доступ.</span><span class="sxs-lookup"><span data-stu-id="148c3-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="148c3-149">bool Неинтерактивный</span><span class="sxs-lookup"><span data-stu-id="148c3-149">bool nonInteractive</span></span> | <span data-ttu-id="148c3-150">Если значение — true, поставщик учетных данных должен отключить все запросы пользователя и использовать вместо них значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="148c3-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="148c3-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="148c3-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="148c3-152">Этот токен отмены должен быть проверен, чтобы определить, была ли отменена операция, запрашивающая учетные данные.</span><span class="sxs-lookup"><span data-stu-id="148c3-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="148c3-153">**Возвращаемое значение**: Объект учетных данных, реализующий [ `System.Net.ICredentials` интерфейс](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="148c3-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
