---
title: Подписанные пакеты
description: Требования для подписания пакета NuGet.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 72fb1a87c13160c53f632d2ef87a12a4e9bc02a3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/22/2018
---
# <a name="signed-packages"></a><span data-ttu-id="96045-103">Подписанные пакеты</span><span class="sxs-lookup"><span data-stu-id="96045-103">Signed packages</span></span>

<span data-ttu-id="96045-104">*NuGet 4.6.0+ и Visual Studio 2017 г 15.6 и более поздних версий*</span><span class="sxs-lookup"><span data-stu-id="96045-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="96045-105">Пакеты NuGet можно включить цифровую подпись, которая обеспечивает защиту от поддельных содержимого.</span><span class="sxs-lookup"><span data-stu-id="96045-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="96045-106">Эта подпись создается из сертификата X.509, который также добавляет экспериментов подлинность фактического источника пакета.</span><span class="sxs-lookup"><span data-stu-id="96045-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="96045-107">Подписанные пакеты обеспечивают надежную проверку начала до конца.</span><span class="sxs-lookup"><span data-stu-id="96045-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="96045-108">Сигнатура автор гарантирует, что пакет не был изменен с момента автор подписи пакета, независимо от того, из которой репозитория или что транспорта метод доставки пакета.</span><span class="sxs-lookup"><span data-stu-id="96045-108">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="96045-109">Кроме того автор подписи пакетов предоставляют механизм дополнительную проверку подлинности в конвейер публикации nuget.org из-за сертификата для подписи должны быть зарегистрированы заранее.</span><span class="sxs-lookup"><span data-stu-id="96045-109">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="96045-110">Дополнительные сведения см. в разделе [регистрация сертификатов](#register-certificate-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="96045-110">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>

<span data-ttu-id="96045-111">Дополнительные сведения о создании подписанного пакета см. в разделе [подписи пакетов](../create-packages/Sign-a-package.md) и [входа команды nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="96045-111">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="96045-112">Подписание пакета в настоящее время поддерживается только при использовании nuget.exe в Windows.</span><span class="sxs-lookup"><span data-stu-id="96045-112">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="96045-113">Проверка подписанных пакетов в настоящее время поддерживается только при использовании nuget.exe или Visual Studio в Windows.</span><span class="sxs-lookup"><span data-stu-id="96045-113">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="96045-114">Требования к сертификатам</span><span class="sxs-lookup"><span data-stu-id="96045-114">Certificate requirements</span></span>

<span data-ttu-id="96045-115">Подписание пакета требуется сертификат, который — это специальный тип сертификата, который является допустимым для подписи кода `id-kp-codeSigning` цель [[RFC 5280 раздел 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="96045-115">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="96045-116">Кроме того сертификат должен иметь RSA длина открытого ключа 2048 бит или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="96045-116">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="96045-117">Получить сертификат подписи кода</span><span class="sxs-lookup"><span data-stu-id="96045-117">Get a code signing certificate</span></span>

<span data-ttu-id="96045-118">Действительные сертификаты могут быть получены из центра сертификации, например:</span><span class="sxs-lookup"><span data-stu-id="96045-118">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="96045-119">Symantec</span><span class="sxs-lookup"><span data-stu-id="96045-119">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="96045-120">DigiCert</span><span class="sxs-lookup"><span data-stu-id="96045-120">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="96045-121">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="96045-121">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="96045-122">Глобальные входа</span><span class="sxs-lookup"><span data-stu-id="96045-122">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="96045-123">Comodo</span><span class="sxs-lookup"><span data-stu-id="96045-123">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="96045-124">Certum</span><span class="sxs-lookup"><span data-stu-id="96045-124">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="96045-125">Полный список центров сертификации, доверенным для Windows можно получить из [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="96045-125">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="96045-126">Создание тестового сертификата</span><span class="sxs-lookup"><span data-stu-id="96045-126">Create a test certificate</span></span>

<span data-ttu-id="96045-127">Самостоятельно выданные сертификаты можно использовать для тестирования.</span><span class="sxs-lookup"><span data-stu-id="96045-127">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="96045-128">Чтобы создать самостоятельно выданный сертификат, используйте [команду PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="96045-128">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="96045-129">Эта команда создает сертификата тестирования в хранилище персональных сертификатов текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="96045-129">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="96045-130">Можно открыть хранилище сертификатов, выполнив `certmgr.msc` для просмотра только что созданный сертификат.</span><span class="sxs-lookup"><span data-stu-id="96045-130">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="96045-131">NuGet.org не принимает пакеты подписана самостоятельно выданные сертификаты.</span><span class="sxs-lookup"><span data-stu-id="96045-131">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="96045-132">Требования к отметки времени</span><span class="sxs-lookup"><span data-stu-id="96045-132">Timestamp requirements</span></span>

<span data-ttu-id="96045-133">Подписанных пакетов должна включать отметок времени RFC 3161, чтобы обеспечить правильность подписи за пределы периода действия сертификата для подписи пакетов.</span><span class="sxs-lookup"><span data-stu-id="96045-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="96045-134">Сертификат, используемый для подписи отметку времени должен быть допустимым для `id-kp-timeStamping` цель [[RFC 5280 раздел 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="96045-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="96045-135">Кроме того сертификат должен иметь RSA длина открытого ключа 2048 бит или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="96045-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="96045-136">Дополнительные технические сведения можно найти в [пакет подпись технические спецификации](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="96045-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="96045-137">Требования к подписи nuget.org</span><span class="sxs-lookup"><span data-stu-id="96045-137">Signature requirements on nuget.org</span></span>

<span data-ttu-id="96045-138">NuGet.org предъявляет требования для принятия подписанных пакетов.</span><span class="sxs-lookup"><span data-stu-id="96045-138">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="96045-139">Основная подпись должно быть сигнатура автора.</span><span class="sxs-lookup"><span data-stu-id="96045-139">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="96045-140">Основная подпись должна иметь допустимую метку времени.</span><span class="sxs-lookup"><span data-stu-id="96045-140">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="96045-141">Сертификаты X.509 для подписи автора и его подпись отметка времени:</span><span class="sxs-lookup"><span data-stu-id="96045-141">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="96045-142">Должен иметь открытый ключ RSA 2048 бит или больше.</span><span class="sxs-lookup"><span data-stu-id="96045-142">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="96045-143">Должен быть действителен в настоящее время на текущее время UTC во время проверки пакета на nuget.org.</span><span class="sxs-lookup"><span data-stu-id="96045-143">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="96045-144">Должен связываться по цепочке доверенным корневым центром сертификации, который является доверенным по умолчанию в Windows.</span><span class="sxs-lookup"><span data-stu-id="96045-144">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="96045-145">Пакеты, подписанные с самостоятельно выданные сертификаты будут отклонены.</span><span class="sxs-lookup"><span data-stu-id="96045-145">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="96045-146">Должен быть допустимым для его цели:</span><span class="sxs-lookup"><span data-stu-id="96045-146">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="96045-147">Автор сертификат подписи должен быть допустимым для подписи кода.</span><span class="sxs-lookup"><span data-stu-id="96045-147">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="96045-148">Отметка времени сертификат должен быть непригоден для.</span><span class="sxs-lookup"><span data-stu-id="96045-148">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="96045-149">Не должны быть отозваны во время подписи.</span><span class="sxs-lookup"><span data-stu-id="96045-149">Must not be revoked at signing time.</span></span> <span data-ttu-id="96045-150">(Это может быть не knowable во время передачи, поэтому nuget.org периодически проверяет состояние отзыва).</span><span class="sxs-lookup"><span data-stu-id="96045-150">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="96045-151">Регистрация сертификата на nuget.org</span><span class="sxs-lookup"><span data-stu-id="96045-151">Register certificate on nuget.org</span></span>

<span data-ttu-id="96045-152">Для отправки подписанного пакета, необходимо сначала зарегистрировать сертификат с nuget.org. Вам понадобится сертификат как `.cer` файл в двоичном формате DER.</span><span class="sxs-lookup"><span data-stu-id="96045-152">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="96045-153">С помощью мастера экспорта сертификатов можно экспортировать существующий сертификат в двоичном формате DER.</span><span class="sxs-lookup"><span data-stu-id="96045-153">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![Мастер экспорта сертификатов](media/CertificateExportWizard.png)

<span data-ttu-id="96045-155">Опытные пользователи могут экспортировать сертификат с помощью [команды PowerShell для экспорта сертификата](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="96045-155">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="96045-156">Чтобы зарегистрировать сертификат в nuget.org, перейдите к `Certificates` статьи на `Account settings` (или организации на странице Параметры) и выберите `Register new certificate`.</span><span class="sxs-lookup"><span data-stu-id="96045-156">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![Зарегистрированных сертификатов](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="96045-158">Один пользователь может отправить несколько сертификатов и тот же сертификат можно зарегистрировать несколько пользователей.</span><span class="sxs-lookup"><span data-stu-id="96045-158">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="96045-159">Как только пользователь имеет сертификат регистрации передачу пакета будущих **должен** быть подписаны с помощью одного из сертификатов.</span><span class="sxs-lookup"><span data-stu-id="96045-159">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="96045-160">Пользователей можно также удалить сертификат, зарегистрированный из учетной записи.</span><span class="sxs-lookup"><span data-stu-id="96045-160">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="96045-161">После удаления сертификата во отправки сбой пакеты, подписанным этим сертификатом.</span><span class="sxs-lookup"><span data-stu-id="96045-161">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="96045-162">Не влияет на существующие пакеты.</span><span class="sxs-lookup"><span data-stu-id="96045-162">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="96045-163">Настройка требований для подписи пакетов</span><span class="sxs-lookup"><span data-stu-id="96045-163">Configure package signing requirements</span></span>

<span data-ttu-id="96045-164">Если вы являетесь единственным владельцем пакета, не требуется подписывающего лица.</span><span class="sxs-lookup"><span data-stu-id="96045-164">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="96045-165">То есть зарегистрированных сертификатов можно использовать для подписания пакетов и отправки в nuget.org.</span><span class="sxs-lookup"><span data-stu-id="96045-165">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="96045-166">Если пакет содержит несколько владельцев по умолчанию, «Любой» владельца сертификаты могут использоваться для подписывания пакета.</span><span class="sxs-lookup"><span data-stu-id="96045-166">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="96045-167">Как владелец пакета можно переопределить «Любой» с самостоятельно или любые другие совладелец быть обязательным подписывающего лица.</span><span class="sxs-lookup"><span data-stu-id="96045-167">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="96045-168">При внесении владельца, не имеет сертификата, зарегистрированного неподписанные пакеты будут запрещены.</span><span class="sxs-lookup"><span data-stu-id="96045-168">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="96045-169">Аналогичным образом, если выбран параметр «Любой» пакета, где один владелец имеет сертификат, зарегистрированный и другого владельца по умолчанию не имеет сертификата, зарегистрированного, затем nuget.org принимает подписанного пакета с подписью, зарегистрированные с одним из владельцев или Неподписанный пакет (из-за одного владельцам отсутствует сертификат, зарегистрированный).</span><span class="sxs-lookup"><span data-stu-id="96045-169">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![Настройка пакета авторов](media/configure-package-signers.png)
