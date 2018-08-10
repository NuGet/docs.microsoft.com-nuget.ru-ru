---
title: Подписанные пакеты
description: Требования для подписывания пакета NuGet.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 992097281e21cd8cf37edf67fb1968b70c2b359b
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020522"
---
# <a name="signed-packages"></a><span data-ttu-id="095ff-103">Подписанные пакеты</span><span class="sxs-lookup"><span data-stu-id="095ff-103">Signed packages</span></span>

<span data-ttu-id="095ff-104">*NuGet 4.6.0+ и Visual Studio 2017 версии 15.6 и более поздние версии*</span><span class="sxs-lookup"><span data-stu-id="095ff-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="095ff-105">Пакеты NuGet могут включать цифровую подпись, которая обеспечивает защиту от поддельных содержимого.</span><span class="sxs-lookup"><span data-stu-id="095ff-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="095ff-106">Эта подпись, созданного из сертификата X.509, который также добавляет подлинность экспериментов на фактический источник пакета.</span><span class="sxs-lookup"><span data-stu-id="095ff-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="095ff-107">Подписанные пакеты обеспечивают надежную проверку end-to-end.</span><span class="sxs-lookup"><span data-stu-id="095ff-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="095ff-108">Существует два вида подписи NuGet:</span><span class="sxs-lookup"><span data-stu-id="095ff-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="095ff-109">**Создание подписи**.</span><span class="sxs-lookup"><span data-stu-id="095ff-109">**Author Signature**.</span></span> <span data-ttu-id="095ff-110">Сигнатура автор гарантирует, что пакет не был изменен, так как автор подписи пакета, независимо от того, из которой репозиторий или что транспорта метод пакет доставляется.</span><span class="sxs-lookup"><span data-stu-id="095ff-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="095ff-111">Кроме того автор подписанные пакеты предоставляют механизм дополнительную проверку подлинности в конвейер публикации nuget.org, так как сертификат для подписи должны быть зарегистрированы заранее.</span><span class="sxs-lookup"><span data-stu-id="095ff-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="095ff-112">Дополнительные сведения см. в разделе [регистрации сертификатов,](#register-certificate-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="095ff-112">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>
- <span data-ttu-id="095ff-113">**Подпись репозитория**.</span><span class="sxs-lookup"><span data-stu-id="095ff-113">**Repository Signature**.</span></span> <span data-ttu-id="095ff-114">Репозиторий подписи гарантируется целостность для **все** пакетов в репозитории, являются ли они автор знаком или без, даже если эти пакеты извлекаются из исходного репозитория, где они находились в другое место со знаком.</span><span class="sxs-lookup"><span data-stu-id="095ff-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="095ff-115">Дополнительные сведения о создании подписанных пакетов автора, см. в разделе [подписи пакетов](../create-packages/Sign-a-package.md) и [команда nuget входа](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="095ff-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="095ff-116">Подписание пакета в настоящее время поддерживается только в том случае, при использовании nuget.exe на Windows.</span><span class="sxs-lookup"><span data-stu-id="095ff-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="095ff-117">Проверка подписанных пакетов в настоящее время поддерживается только в том случае, если с помощью Visual Studio или nuget.exe в Windows.</span><span class="sxs-lookup"><span data-stu-id="095ff-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="095ff-118">Требования к сертификатам</span><span class="sxs-lookup"><span data-stu-id="095ff-118">Certificate requirements</span></span>

<span data-ttu-id="095ff-119">Подписание пакета требует сертификата, который — это специальный тип сертификата, который является допустимым для подписи кода `id-kp-codeSigning` назначения [[RFC 5280 разделе 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="095ff-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="095ff-120">Кроме того сертификат должен иметь RSA длина открытого ключа 2048 бит или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="095ff-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="095ff-121">Получение сертификата подписи кода</span><span class="sxs-lookup"><span data-stu-id="095ff-121">Get a code signing certificate</span></span>

<span data-ttu-id="095ff-122">Действительные сертификаты может быть получен из общедоступного ЦС, например:</span><span class="sxs-lookup"><span data-stu-id="095ff-122">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="095ff-123">Symantec</span><span class="sxs-lookup"><span data-stu-id="095ff-123">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="095ff-124">DigiCert</span><span class="sxs-lookup"><span data-stu-id="095ff-124">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="095ff-125">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="095ff-125">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="095ff-126">Глобальные входа</span><span class="sxs-lookup"><span data-stu-id="095ff-126">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="095ff-127">Comodo</span><span class="sxs-lookup"><span data-stu-id="095ff-127">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="095ff-128">Certum</span><span class="sxs-lookup"><span data-stu-id="095ff-128">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="095ff-129">Полный список центров сертификации, доверенным для Windows можно получить из [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="095ff-129">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="095ff-130">Создание тестового сертификата</span><span class="sxs-lookup"><span data-stu-id="095ff-130">Create a test certificate</span></span>

<span data-ttu-id="095ff-131">Для целей тестирования можно использовать самостоятельно выданные сертификаты.</span><span class="sxs-lookup"><span data-stu-id="095ff-131">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="095ff-132">Чтобы создать самостоятельно выданный сертификат, используйте [команду PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="095ff-132">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="095ff-133">Эта команда создает сертификат тестирования, доступный в хранилище личных сертификатов текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="095ff-133">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="095ff-134">Можно открыть хранилище сертификатов, выполнив `certmgr.msc` для просмотра только что созданный сертификат.</span><span class="sxs-lookup"><span data-stu-id="095ff-134">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="095ff-135">NuGet.org не принимает пакеты, подписанные самостоятельно выданные сертификаты.</span><span class="sxs-lookup"><span data-stu-id="095ff-135">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="095ff-136">Требования к отметки времени</span><span class="sxs-lookup"><span data-stu-id="095ff-136">Timestamp requirements</span></span>

<span data-ttu-id="095ff-137">Подписанные пакеты должны включать отметку времени RFC 3161 чтобы обеспечить достоверность подписи за пределы периода действия сертификата подписи пакета.</span><span class="sxs-lookup"><span data-stu-id="095ff-137">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="095ff-138">Сертификат, используемый для подписи отметку времени должен быть допустимым для `id-kp-timeStamping` назначения [[RFC 5280 разделе 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="095ff-138">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="095ff-139">Кроме того сертификат должен иметь RSA длина открытого ключа 2048 бит или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="095ff-139">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="095ff-140">Дополнительные технические сведения можно найти в [пакет подпись технические спецификации](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="095ff-140">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="095ff-141">Требования к подписи на сайте nuget.org</span><span class="sxs-lookup"><span data-stu-id="095ff-141">Signature requirements on nuget.org</span></span>

<span data-ttu-id="095ff-142">NuGet.org имеет дополнительные требования к выполнению подписанных пакетов:</span><span class="sxs-lookup"><span data-stu-id="095ff-142">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="095ff-143">Основная подпись должен быть подпись автора.</span><span class="sxs-lookup"><span data-stu-id="095ff-143">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="095ff-144">Основная подпись должны иметь допустимую метку времени.</span><span class="sxs-lookup"><span data-stu-id="095ff-144">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="095ff-145">Сертификаты X.509 для подписи автора и его подпись метка времени:</span><span class="sxs-lookup"><span data-stu-id="095ff-145">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="095ff-146">Должен иметь открытый ключ RSA 2048 бит или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="095ff-146">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="095ff-147">Должен находиться в пределах срока его действия на текущее время в формате UTC во время проверки пакета на сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="095ff-147">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="095ff-148">Необходимо объединить в цепочку с доверенным корневым центром сертификации, считается надежным по умолчанию в Windows.</span><span class="sxs-lookup"><span data-stu-id="095ff-148">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="095ff-149">Пакеты, подписанные с помощью самостоятельно выданные сертификаты отклоняются.</span><span class="sxs-lookup"><span data-stu-id="095ff-149">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="095ff-150">Должен быть допустимым для его цели:</span><span class="sxs-lookup"><span data-stu-id="095ff-150">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="095ff-151">Сертификат для подписи автор должен быть допустимым для подписывания кода.</span><span class="sxs-lookup"><span data-stu-id="095ff-151">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="095ff-152">Метка времени сертификат должен быть непригоден для.</span><span class="sxs-lookup"><span data-stu-id="095ff-152">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="095ff-153">Не должен быть отозван в времени подписи.</span><span class="sxs-lookup"><span data-stu-id="095ff-153">Must not be revoked at signing time.</span></span> <span data-ttu-id="095ff-154">(Это может не быть knowable во время отправки, поэтому nuget.org периодически проверяет состояние отзыва).</span><span class="sxs-lookup"><span data-stu-id="095ff-154">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="095ff-155">Регистрация сертификата на сайте nuget.org</span><span class="sxs-lookup"><span data-stu-id="095ff-155">Register certificate on nuget.org</span></span>

<span data-ttu-id="095ff-156">Для отправки подписанных пакетов, необходимо сначала зарегистрировать сертификат с сайта nuget.org. Вам потребуется сертификат как `.cer` файл в двоичном DER-формате.</span><span class="sxs-lookup"><span data-stu-id="095ff-156">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="095ff-157">Существующий сертификат можно экспортировать в двоичном DER-формате с помощью мастера экспорта сертификатов.</span><span class="sxs-lookup"><span data-stu-id="095ff-157">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![Мастер экспорта сертификатов](media/CertificateExportWizard.png)

<span data-ttu-id="095ff-159">Опытные пользователи могут экспортировать сертификат с помощью [команду PowerShell для экспорта сертификата](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="095ff-159">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="095ff-160">Чтобы зарегистрировать сертификат с сайта nuget.org, перейдите к статье `Certificates` разделе `Account settings` страницы (или организации на странице "Параметры") и выберите `Register new certificate`.</span><span class="sxs-lookup"><span data-stu-id="095ff-160">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![Зарегистрированных сертификатов](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="095ff-162">Один пользователь может отправить несколько сертификатов и тот же сертификат можно зарегистрировать несколько пользователей.</span><span class="sxs-lookup"><span data-stu-id="095ff-162">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="095ff-163">Имеющийся у пользователя сертификат зарегистрирован, пакет будущих передачу **необходимо** быть подписаны с помощью одного из сертификатов.</span><span class="sxs-lookup"><span data-stu-id="095ff-163">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="095ff-164">Пользователи также могут удалять зарегистрированный сертификат из учетной записи.</span><span class="sxs-lookup"><span data-stu-id="095ff-164">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="095ff-165">После удаления сертификата во отправки сбой пакеты, подписанные этим сертификатом.</span><span class="sxs-lookup"><span data-stu-id="095ff-165">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="095ff-166">Существующие пакеты не затрагиваются.</span><span class="sxs-lookup"><span data-stu-id="095ff-166">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="095ff-167">Настройка требований для подписи пакета</span><span class="sxs-lookup"><span data-stu-id="095ff-167">Configure package signing requirements</span></span>

<span data-ttu-id="095ff-168">Если вы являетесь единственным владельцем пакета, не требуется подписавшего.</span><span class="sxs-lookup"><span data-stu-id="095ff-168">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="095ff-169">То есть можно использовать любой из зарегистрированных сертификатов для подписывания пакетов и отправки на сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="095ff-169">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="095ff-170">Если пакет содержит несколько владельцев по умолчанию, «Любой» владелец сертификаты могут использоваться для подписи пакета.</span><span class="sxs-lookup"><span data-stu-id="095ff-170">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="095ff-171">Как владелец пакета можно переопределить «Любой» с самостоятельно или любые другие совладелец быть требуется подписавшего.</span><span class="sxs-lookup"><span data-stu-id="095ff-171">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="095ff-172">Если владелец, который не поддерживает любой сертификат, зарегистрированный, неподписанных пакетов разрешается.</span><span class="sxs-lookup"><span data-stu-id="095ff-172">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="095ff-173">Аналогичным образом, если для пакета, где один владелец имеет сертификат, зарегистрированный и другого владельца выбран «Any» параметр по умолчанию не имеет любой сертификат, зарегистрированный, затем nuget.org принимает подписанных пакетов с сигнатурой, зарегистрированные с одним из владельцев или Неподписанный пакет (так как один из владельцев имеет любой сертификат, зарегистрированный).</span><span class="sxs-lookup"><span data-stu-id="095ff-173">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![Настройка пакета подписавших](media/configure-package-signers.png)
