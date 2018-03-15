---
title: "Подпись ссылки на пакеты | Документы Microsoft"
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Подписанные пакеты описание компонента."
keywords: "Знак пакета NuGet, подписи, сертификат"
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9bf9885aaf42bedb681a5d916202fa8b26749a0c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="signed-packages"></a><span data-ttu-id="22c30-104">Подписанные пакеты</span><span class="sxs-lookup"><span data-stu-id="22c30-104">Signed packages</span></span>

<span data-ttu-id="22c30-105">*NuGet 4.6.0+ и Visual Studio 2017 г 15.6 и более поздних версий*</span><span class="sxs-lookup"><span data-stu-id="22c30-105">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="22c30-106">Пакеты NuGet можно включить цифровую подпись, которая обеспечивает защиту от поддельных содержимого.</span><span class="sxs-lookup"><span data-stu-id="22c30-106">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="22c30-107">Эта подпись создается из сертификата X.509, который также добавляет экспериментов подлинность фактического источника пакета.</span><span class="sxs-lookup"><span data-stu-id="22c30-107">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="22c30-108">Подписанные пакеты обеспечивают надежную проверку начала до конца.</span><span class="sxs-lookup"><span data-stu-id="22c30-108">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="22c30-109">Сигнатура автор гарантирует, что пакет не был изменен с момента автор подписи пакета, независимо от того, из которой репозитория или что транспорта метод доставки пакета.</span><span class="sxs-lookup"><span data-stu-id="22c30-109">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="22c30-110">Потребителей, которым требуется закрытой среде может потребоваться пакеты, подписанные сертификатом, определенных автором.</span><span class="sxs-lookup"><span data-stu-id="22c30-110">Consumers who demand a locked-down environment can require packages signed with a specific author certificate.</span></span>

<span data-ttu-id="22c30-111">Кроме того автор подписи пакетов предоставляют механизм дополнительную проверку подлинности в конвейер публикации nuget.org из-за сертификата для подписи должны быть зарегистрированы заранее.</span><span class="sxs-lookup"><span data-stu-id="22c30-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span>

<span data-ttu-id="22c30-112">Дополнительные сведения о создании подписанного пакета см. в разделе [подписи пакетов](../create-packages/Sign-a-package.md) и [входа команды nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="22c30-112">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="22c30-113">в настоящее время NuGet.org не принимает подписанных пакетов.</span><span class="sxs-lookup"><span data-stu-id="22c30-113">nuget.org does not presently accept signed packages.</span></span> <span data-ttu-id="22c30-114">Можно подписывать пакеты для публикации в пользовательских каналов.</span><span class="sxs-lookup"><span data-stu-id="22c30-114">You can sign packages for publishing to custom feeds.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="22c30-115">Требования к сертификатам</span><span class="sxs-lookup"><span data-stu-id="22c30-115">Certificate requirements</span></span>

<span data-ttu-id="22c30-116">Подписание пакета требуется сертификат, который — это специальный тип сертификата, который является допустимым для подписи кода `id-kp-codeSigning` цель [[RFC 5280 раздел 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="22c30-116">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="22c30-117">Кроме того сертификат должен иметь RSA длина открытого ключа 2048 бит или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="22c30-117">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="22c30-118">Получить сертификат подписи кода</span><span class="sxs-lookup"><span data-stu-id="22c30-118">Get a code signing certificate</span></span>

<span data-ttu-id="22c30-119">Действительные сертификаты могут быть получены из открытых сертификации, таких как:</span><span class="sxs-lookup"><span data-stu-id="22c30-119">Valid certificates may be obtained from public certificate authorities like:</span></span>

- [<span data-ttu-id="22c30-120">Symantec</span><span class="sxs-lookup"><span data-stu-id="22c30-120">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="22c30-121">DigiCert</span><span class="sxs-lookup"><span data-stu-id="22c30-121">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="22c30-122">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="22c30-122">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="22c30-123">Глобальные входа</span><span class="sxs-lookup"><span data-stu-id="22c30-123">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="22c30-124">Comodo</span><span class="sxs-lookup"><span data-stu-id="22c30-124">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="22c30-125">Certum</span><span class="sxs-lookup"><span data-stu-id="22c30-125">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="22c30-126">Полный список центров сертификации, доверенным для Windows можно получить из [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="22c30-126">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="22c30-127">Создание тестового сертификата</span><span class="sxs-lookup"><span data-stu-id="22c30-127">Create a test certificate</span></span>

<span data-ttu-id="22c30-128">Самостоятельно выданные сертификаты можно использовать для тестирования.</span><span class="sxs-lookup"><span data-stu-id="22c30-128">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="22c30-129">Чтобы создать самостоятельно выданный сертификат, используйте [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22c30-129">To create a self-issued certificate, use the [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell command.</span></span>

```ps
New-SelfSignedCertificate -Subject "CN=NuGet Test Developer, OU=Use for testing purposes ONLY" `
                          -FriendlyName "NuGetTestDeveloper" `
                          -Type CodeSigning `
                          -KeyUsage DigitalSignature `
                          -KeyLength 2048 `
                          -KeyAlgorithm RSA `
                          -HashAlgorithm SHA256 `
                          -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
                          -CertStoreLocation "Cert:\CurrentUser\My" 
```

<span data-ttu-id="22c30-130">Эта команда создает сертификата тестирования в хранилище персональных сертификатов текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="22c30-130">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="22c30-131">Можно открыть хранилище сертификатов, выполнив `certmgr.msc` для просмотра только что созданный сертификат.</span><span class="sxs-lookup"><span data-stu-id="22c30-131">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="22c30-132">Требования к отметки времени</span><span class="sxs-lookup"><span data-stu-id="22c30-132">Timestamp requirements</span></span>

<span data-ttu-id="22c30-133">Подписанных пакетов должна включать отметок времени RFC 3161, чтобы обеспечить правильность подписи за пределы периода действия сертификата для подписи пакетов.</span><span class="sxs-lookup"><span data-stu-id="22c30-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="22c30-134">Сертификат, используемый для подписи отметку времени должен быть допустимым для `id-kp-timeStamping` цель [[RFC 5280 раздел 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="22c30-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="22c30-135">Кроме того сертификат должен иметь RSA длина открытого ключа 2048 бит или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="22c30-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="22c30-136">Дополнительные технические сведения можно найти в [пакет подпись технические спецификации](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="22c30-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>
