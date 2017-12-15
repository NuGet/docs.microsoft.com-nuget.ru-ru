---
title: "Поставщики учетных данных NuGet для Visual Studio | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 9c7f6d16-f437-47c4-82d4-6c996e0b18ec
description: "NuGet поставщиков учетных данных проверки подлинности с каналами, реализовав интерфейс IVsCredentialProvider в расширение Visual Studio."
keywords: "NuGet поставщиков учетных данных, проверку подлинности с веб-канала, проверку подлинности с помощью коллекции NuGet расширение visual studio"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2b2fac23102865a08509acc1cc3d09f0cd375f26
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="51662-104">Проверка подлинности веб-каналов в Visual Studio с помощью NuGet поставщиков учетных данных</span><span class="sxs-lookup"><span data-stu-id="51662-104">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="51662-105">Расширение NuGet Visual Studio 3.6 + поддерживает поставщиков учетных данных, которые позволяют NuGet для работы с проверкой подлинности веб-каналов.</span><span class="sxs-lookup"><span data-stu-id="51662-105">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="51662-106">После установки поставщика учетных данных NuGet для Visual Studio, расширение NuGet для Visual Studio автоматически получить и обновите учетные данные для прошедших проверку подлинности веб-каналы, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="51662-106">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="51662-107">Образец реализации можно найти в [пример VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="51662-107">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

> [!Note]
> <span data-ttu-id="51662-108">Поставщики учетных данных NuGet для Visual Studio, должен быть установлен как регулярное расширение Visual Studio и потребует [2017 г. Visual Studio](https://aka.ms/vs/15/preview/vs_enterprise) (в настоящее время в предварительной версии) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="51662-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (currently in preview) or above.</span></span>
>
> <span data-ttu-id="51662-109">Поставщики учетных данных NuGet для Visual Studio работает только в Visual Studio (не в dotnet восстановления или nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="51662-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="51662-110">Поставщики учетных данных с nuget.exe, в разделе [nuget.exe поставщиков учетных данных](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="51662-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="51662-111">Доступные поставщики учетных данных NuGet для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="51662-111">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="51662-112">Отсутствует поставщик учетных данных, встроенные в расширение Visual Studio NuGet поддержки Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="51662-112">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="51662-113">Расширение NuGet Visual Studio использует внутреннюю `VsCredentialProviderImporter` которого также проверяет наличие поставщиков учетных данных подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="51662-113">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="51662-114">Эти поставщики учетных данных подключаемого модуля должно быть включено обнаружение как MEF экспорта типа `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="51662-114">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="51662-115">Поставщики доступных подключаемых модулей учетных данных:</span><span class="sxs-lookup"><span data-stu-id="51662-115">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="51662-116">Поставщик учетных данных MyGet для Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="51662-116">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="51662-117">Создание учетных данных поставщика NuGet для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="51662-117">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="51662-118">Расширение NuGet Visual Studio 3.6 + реализует внутренней CredentialService, который используется для получения учетных данных.</span><span class="sxs-lookup"><span data-stu-id="51662-118">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="51662-119">CredentialService имеет список поставщиков учетных данных встроенной и подключаемый модуль.</span><span class="sxs-lookup"><span data-stu-id="51662-119">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="51662-120">Каждый поставщик предпринимается попытка последовательно, пока полученные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="51662-120">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="51662-121">Во время получения учетных данных службы учетных данных попытается поставщиков учетных данных в следующем порядке, остановка, а полученные учетные данные:</span><span class="sxs-lookup"><span data-stu-id="51662-121">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="51662-122">Учетные данные будут получены из файлов конфигурации NuGet (с помощью встроенной `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="51662-122">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="51662-123">Если источник пакета находится на Visual Studio Team Services `VisualStudioAccountProvider` будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="51662-123">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="51662-124">Все другие поставщики учетных данных подключаемый модуль будет предпринята последовательно.</span><span class="sxs-lookup"><span data-stu-id="51662-124">All other plug-in credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="51662-125">Если учетные данные не получены, пока пользователя будут запрашиваться учетные данные, используя диалоговое окно стандартных обычной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="51662-125">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="51662-126">Реализация IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="51662-126">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="51662-127">Чтобы создать учетные данные поставщика NuGet для Visual Studio, создайте расширения Visual Studio, предоставляющий открытый MEF-Экспорт реализации `IVsCredentialProvider` введите, а также придерживается перечисленным ниже.</span><span class="sxs-lookup"><span data-stu-id="51662-127">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="51662-128">Образец реализации можно найти в [пример VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="51662-128">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="51662-129">Каждый поставщик учетных данных NuGet для Visual Studio необходимо:</span><span class="sxs-lookup"><span data-stu-id="51662-129">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="51662-130">Определите ли его можно указать учетные данные для целевого URI перед запуском процесса получения учетных данных.</span><span class="sxs-lookup"><span data-stu-id="51662-130">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="51662-131">Если поставщик не может предоставить учетные данные для источника, то он должен возвращать `null`.</span><span class="sxs-lookup"><span data-stu-id="51662-131">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="51662-132">Если поставщик обрабатывать запросы для целевой URI, но не может предоставить учетные данные, должно создаваться исключение.</span><span class="sxs-lookup"><span data-stu-id="51662-132">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="51662-133">Необходимо реализовать пользовательский поставщик учетных данных NuGet для Visual Studio `IVsCredentialProvider` интерфейса, доступные в [NuGet.VisualStudio пакета](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="51662-133">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="51662-134">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="51662-134">GetCredentialAsync</span></span>

| <span data-ttu-id="51662-135">Входной параметр</span><span class="sxs-lookup"><span data-stu-id="51662-135">Input Parameter</span></span> |<span data-ttu-id="51662-136">Описание</span><span class="sxs-lookup"><span data-stu-id="51662-136">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="51662-137">Uri, URI</span><span class="sxs-lookup"><span data-stu-id="51662-137">Uri uri</span></span> | <span data-ttu-id="51662-138">Uri исходного пакета, для которого запрашиваются учетные данные.</span><span class="sxs-lookup"><span data-stu-id="51662-138">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="51662-139">IWebProxy прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="51662-139">IWebProxy proxy</span></span> | <span data-ttu-id="51662-140">Веб-прокси, который используется для связи по сети.</span><span class="sxs-lookup"><span data-stu-id="51662-140">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="51662-141">Значение NULL, если проверка подлинности прокси-сервер не настроен.</span><span class="sxs-lookup"><span data-stu-id="51662-141">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="51662-142">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="51662-142">bool isProxyRequest</span></span> | <span data-ttu-id="51662-143">Значение true, если этот запрос для получения учетных данных проверки подлинности прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="51662-143">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="51662-144">Если реализация не является допустимым для получения учетных данных прокси-сервера, должно быть возвращено значение null.</span><span class="sxs-lookup"><span data-stu-id="51662-144">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="51662-145">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="51662-145">bool isRetry</span></span> | <span data-ttu-id="51662-146">Значение true, если для данного Uri ранее запрошенные учетные данные, но предоставленные учетные данные не позволяли авторизованный доступ.</span><span class="sxs-lookup"><span data-stu-id="51662-146">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="51662-147">Неинтерактивные bool</span><span class="sxs-lookup"><span data-stu-id="51662-147">bool nonInteractive</span></span> | <span data-ttu-id="51662-148">Значение true, если поставщик учетных данных необходимо отключить все запросы пользователю и вместо этого используйте значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="51662-148">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="51662-149">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="51662-149">CancellationToken cancellationToken</span></span> | <span data-ttu-id="51662-150">Этот токен отмены должен проверяться для определения того, если с запросом учетных данных операция была отменена.</span><span class="sxs-lookup"><span data-stu-id="51662-150">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |
  
<span data-ttu-id="51662-151">**Возвращаемое значение**: объект учетных данных, реализующий [ `System.Net.ICredentials` интерфейс](https://msdn.microsoft.com/library/system.net.icredentials.aspx).</span><span class="sxs-lookup"><span data-stu-id="51662-151">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](https://msdn.microsoft.com/library/system.net.icredentials.aspx).</span></span>
