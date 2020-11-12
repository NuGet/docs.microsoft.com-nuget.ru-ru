---
title: Подписывание пакетов NuGet
description: Описание того, как подписанные пакеты можно использовать, чтобы включить проверку целостности содержимого.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 64b28c29ae3b533bde7c8f41dd38a4ab0a5afef7
ms.sourcegitcommit: 0cc6ac680c3202d0b036c0bed7910f6709215682
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/12/2020
ms.locfileid: "94550379"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="906d6-103">Подписывание пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="906d6-103">Signing NuGet Packages</span></span>

<span data-ttu-id="906d6-104">Подписанные пакеты позволяют проверить целостность содержимого и защитить его от подделки.</span><span class="sxs-lookup"><span data-stu-id="906d6-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="906d6-105">Подпись пакетов также предоставляет истинные сведения о фактическом источнике пакета и подтверждает его подлинность для клиента.</span><span class="sxs-lookup"><span data-stu-id="906d6-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="906d6-106">В этом руководстве предполагается, что вы уже [создали пакет](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="906d6-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="906d6-107">Получение сертификата для подписи кода</span><span class="sxs-lookup"><span data-stu-id="906d6-107">Get a code signing certificate</span></span>

<span data-ttu-id="906d6-108">Допустимые сертификаты можно получить в общедоступном центре сертификации, таком как [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) и т. д. Полный список центров сертификации, доверенных для Windows: [http://aka.ms/trustcertpartners](/security/trusted-root/participants-list).</span><span class="sxs-lookup"><span data-stu-id="906d6-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](/security/trusted-root/participants-list).</span></span>

<span data-ttu-id="906d6-109">Для тестирования можно использовать самовыданные сертификаты.</span><span class="sxs-lookup"><span data-stu-id="906d6-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="906d6-110">Однако NuGet.org не принимает пакеты, подписанные с помощью самовыданных сертификатов. Дополнительные сведения о [создании тестового сертификата](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="906d6-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="906d6-111">Экспорт файла сертификата</span><span class="sxs-lookup"><span data-stu-id="906d6-111">Export the certificate file</span></span>

* <span data-ttu-id="906d6-112">Вы можете экспортировать существующий сертификат в двоичный формат DER, используя мастер экспорта сертификатов.</span><span class="sxs-lookup"><span data-stu-id="906d6-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Мастер экспорта сертификатов](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="906d6-114">Вы можете также экспортировать сертификат с помощью [команды Export-Certificate PowerShell](/powershell/module/pkiclient/export-certificate).</span><span class="sxs-lookup"><span data-stu-id="906d6-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="906d6-115">Подписывание пакета</span><span class="sxs-lookup"><span data-stu-id="906d6-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="906d6-116">Требуется nuget.exe 4.6.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="906d6-116">Requires nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="906d6-117">Поддержка dotnet.exe ожидается в ближайшее время ([№ 7939](https://github.com/NuGet/Home/issues/7939)).</span><span class="sxs-lookup"><span data-stu-id="906d6-117">dotnet.exe support is coming soon - [#7939](https://github.com/NuGet/Home/issues/7939)</span></span>

<span data-ttu-id="906d6-118">Подпишите пакет с помощью команды [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="906d6-118">Sign the package using [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> <span data-ttu-id="906d6-119">Поставщик сертификатов также часто предоставляет URL-адрес сервера меток времени, который можно указать в качестве значения необязательного аргумента `Timestamper` выше.</span><span class="sxs-lookup"><span data-stu-id="906d6-119">The certificate provider often also provides a timestamping server URL which you can use for the `Timestamper` optional argument show above.</span></span> <span data-ttu-id="906d6-120">Чтобы получить URL-адрес этой службы, обратитесь к документации и (или) в службу поддержки своего поставщика.</span><span class="sxs-lookup"><span data-stu-id="906d6-120">Consult with your provider's documentation and/or support for that service URL.</span></span>

* <span data-ttu-id="906d6-121">Вы можете использовать сертификат, доступный в хранилище сертификатов, или сертификат из файла.</span><span class="sxs-lookup"><span data-stu-id="906d6-121">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="906d6-122">См. справочник по CLI для [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="906d6-122">See CLI reference for [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span></span>
* <span data-ttu-id="906d6-123">Подписанные пакеты должны включать метку времени, чтобы подпись оставалась действительной после истечения срока действия сертификата для подписывания.</span><span class="sxs-lookup"><span data-stu-id="906d6-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="906d6-124">В противном случае операция sign вызовет [предупреждение](../reference/errors-and-warnings/NU3002.md).</span><span class="sxs-lookup"><span data-stu-id="906d6-124">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="906d6-125">Просмотреть сведения о подписи заданного пакета можно с помощью [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="906d6-125">You can see the signature details of a given package using [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="906d6-126">Регистрация сертификата на сайте NuGet.org</span><span class="sxs-lookup"><span data-stu-id="906d6-126">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="906d6-127">Чтобы опубликовать подписанный пакет, сначала нужно зарегистрировать сертификат на сайте NuGet.org. Вам потребуется сертификат, так как файл `.cer` находится в двоичном формате DER.</span><span class="sxs-lookup"><span data-stu-id="906d6-127">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="906d6-128">[Войдите](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) на сайт NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="906d6-128">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="906d6-129">Перейдите в `Account settings` (или `Manage Organization` **>** `Edit Organization`, если вы хотите зарегистрировать сертификат в учетной записи организации).</span><span class="sxs-lookup"><span data-stu-id="906d6-129">Go to `Account settings` (or `Manage Organization` **>** `Edit Organization` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="906d6-130">Разверните раздел `Certificates` и выберите `Register new`.</span><span class="sxs-lookup"><span data-stu-id="906d6-130">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="906d6-131">Найдите и выберите файл сертификата, экспортированного ранее.</span><span class="sxs-lookup"><span data-stu-id="906d6-131">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="906d6-132">![Зарегистрированные сертификаты](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="906d6-132">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="906d6-133">**Примечание**</span><span class="sxs-lookup"><span data-stu-id="906d6-133">**Note**</span></span>
* <span data-ttu-id="906d6-134">Один пользователь может отправить несколько сертификатов. Один и тот же сертификат может быть зарегистрирован несколькими пользователями.</span><span class="sxs-lookup"><span data-stu-id="906d6-134">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="906d6-135">После регистрации сертификата все будущие отправки пакетов **должны** быть подписаны с помощью одного из сертификатов.</span><span class="sxs-lookup"><span data-stu-id="906d6-135">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="906d6-136">См. раздел [Управление требованиями к подписи для вашего пакета на сайте NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="906d6-136">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="906d6-137">Пользователи могут также удалить зарегистрированный сертификат из учетной записи.</span><span class="sxs-lookup"><span data-stu-id="906d6-137">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="906d6-138">После удаления сертификата новые пакеты, подписанные с его помощью, вызовут сбой при отправке.</span><span class="sxs-lookup"><span data-stu-id="906d6-138">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="906d6-139">Существующие пакеты не будут затронуты.</span><span class="sxs-lookup"><span data-stu-id="906d6-139">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="906d6-140">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="906d6-140">Publish the package</span></span>

<span data-ttu-id="906d6-141">Теперь вы готовы к публикации пакета на сайте NuGet.org. См. раздел [Публикация пакетов](../nuget-org/Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="906d6-141">You are now ready to publish the package to NuGet.org. See [Publishing packages](../nuget-org/Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="906d6-142">Создание тестового сертификата</span><span class="sxs-lookup"><span data-stu-id="906d6-142">Create a test certificate</span></span>

<span data-ttu-id="906d6-143">Для тестирования можно использовать самовыданные сертификаты.</span><span class="sxs-lookup"><span data-stu-id="906d6-143">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="906d6-144">Чтобы создать самовыданный сертификат, используйте [команду New-SelfSignedCertificate PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="906d6-144">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate).</span></span>

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

<span data-ttu-id="906d6-145">Эта команда создает тестовый сертификат, доступный в личном хранилище сертификатов текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="906d6-145">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="906d6-146">Вы можете открыть хранилище сертификатов, запустив `certmgr.msc`, чтобы просмотреть созданный сертификат.</span><span class="sxs-lookup"><span data-stu-id="906d6-146">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="906d6-147">NuGet.org не принимает пакеты, подписанные с помощью самовыданных сертификатов.</span><span class="sxs-lookup"><span data-stu-id="906d6-147">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="906d6-148">Управление требованиями к подписи для пакета на сайте NuGet.org</span><span class="sxs-lookup"><span data-stu-id="906d6-148">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="906d6-149">[Войдите](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) на сайт NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="906d6-149">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="906d6-150">Перейдите в раздел `Manage Packages` 
   ![Настройка подписывающих лиц пакета](../reference/media/configure-package-signers.png).</span><span class="sxs-lookup"><span data-stu-id="906d6-150">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="906d6-151">Если вы — единственный владелец пакета, вам нужно подписывающее лицо. То есть вы можете использовать любой из зарегистрированных сертификатов для подписи и публикации пакетов на сайте NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="906d6-151">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="906d6-152">Если у пакета несколько владельцев, по умолчанию для подписания можно использовать любые сертификаты владельца.</span><span class="sxs-lookup"><span data-stu-id="906d6-152">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="906d6-153">Как совладелец пакета, вы можете указать себя или совладельца вместо значения "Любой".</span><span class="sxs-lookup"><span data-stu-id="906d6-153">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="906d6-154">Если вы сделаете владельцем пользователя, у которого нет зарегистрированного сертификата, неподписанные пакеты будут запрещены.</span><span class="sxs-lookup"><span data-stu-id="906d6-154">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="906d6-155">Аналогично если по умолчанию для пакета, в котором у одного владельца зарегистрирован сертификат, а у другого — не зарегистрирован, выбран параметр "Любой", то в этом случае NuGet.org принимает подписанный пакет с подписью, зарегистрированной одним из владельцев, или неподписанный пакет (так как у одного из владельцев не зарегистрирован сертификат).</span><span class="sxs-lookup"><span data-stu-id="906d6-155">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="906d6-156">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="906d6-156">Related articles</span></span>

- [<span data-ttu-id="906d6-157">Управление границами доверия пакета</span><span class="sxs-lookup"><span data-stu-id="906d6-157">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="906d6-158">Справочник по подписанным пакетам</span><span class="sxs-lookup"><span data-stu-id="906d6-158">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)