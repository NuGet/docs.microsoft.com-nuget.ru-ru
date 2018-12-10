---
title: Подписывание пакетов NuGet
description: Описание того, как подписанные пакеты можно использовать, чтобы включить проверку целостности содержимого.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e8955f9d46bab235c8755d5654814a4291d542d6
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977567"
---
# <a name="signing-nuget-packages"></a>Подписывание пакетов NuGet

Подписанные пакеты позволяют проверить целостность содержимого и защитить его от подделки. Подпись пакетов также предоставляет истинные сведения о фактическом источнике пакета и подтверждает его подлинность для клиента. В этом руководстве предполагается, что вы уже [создали пакет](creating-a-package.md).

## <a name="get-a-code-signing-certificate"></a>Получение сертификата для подписи кода

Допустимые сертификаты можно получить в общедоступном центре сертификации, таком как [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) и т. д. Полный список центров сертификации, доверенных для Windows: [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).

Для тестирования можно использовать самовыданные сертификаты. Однако NuGet.org не принимает пакеты, подписанные с помощью самовыданных сертификатов. Дополнительные сведения о [создании тестового сертификата](#create-a-test-certificate)

## <a name="export-the-certificate-file"></a>Экспорт файла сертификата

* Вы можете экспортировать существующий сертификат в двоичный формат DER, используя мастер экспорта сертификатов.

  ![Мастер экспорта сертификатов](../reference/media/CertificateExportWizard.png)

* Вы можете также экспортировать сертификат с помощью [команды Export-Certificate PowerShell](/powershell/module/pkiclient/export-certificate.md).

## <a name="sign-the-package"></a>Подписывание пакета

> [!note]
> Требуется nuget.exe 4.6.0 или более поздней версии.

Подпишите пакет с помощью команды [nuget sign](../tools/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificateFilePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

* Вы можете использовать сертификат, доступный в хранилище сертификатов, или сертификат из файла. См. справочник по CLI для [nuget sign](../tools/cli-ref-sign.md).
* Подписанные пакеты должны включать метку времени, чтобы подпись оставалась действительной после истечения срока действия сертификата для подписывания. В противном случае операция sign вызовет [предупреждение](../reference/errors-and-warnings/NU3002.md).
* Просмотреть сведения о подписи заданного пакета можно с помощью [nuget verify](../tools/cli-ref-verify.md).

## <a name="register-the-certificate-on-nugetorg"></a>Регистрация сертификата на сайте NuGet.org

Чтобы опубликовать подписанный пакет, сначала нужно зарегистрировать сертификат на сайте NuGet.org. Вам потребуется сертификат, так как файл `.cer` находится в двоичном формате DER.

1. [Войдите](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) на сайт NuGet.org.
1. Перейдите в `Account settings` (или `Manage Organization` **>** `Edit Organziation`, если вы хотите зарегистрировать сертификат в учетной записи организации).
1. Разверните раздел `Certificates` и выберите `Register new`.
1. Найдите и выберите файл сертификата, экспортированного ранее.
  ![Зарегистрированные сертификаты](../reference/media/registered-certs.png)

**Примечание**
* Один пользователь может отправить несколько сертификатов. Один и тот же сертификат может быть зарегистрирован несколькими пользователями.
* После регистрации сертификата все будущие отправки пакетов **должны** быть подписаны с помощью одного из сертификатов. См. раздел [Управление требованиями к подписи для вашего пакета на сайте NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)
* Пользователи могут также удалить зарегистрированный сертификат из учетной записи. После удаления сертификата новые пакеты, подписанные с его помощью, вызовут сбой при отправке. Существующие пакеты не будут затронуты.

## <a name="publish-the-package"></a>Публикация пакета

Теперь вы готовы к публикации пакета на сайте NuGet.org. См. раздел [Публикация пакетов](Publish-a-package.md).

## <a name="create-a-test-certificate"></a>Создание тестового сертификата

Для тестирования можно использовать самовыданные сертификаты. Чтобы создать самовыданный сертификат, используйте [команду New-SelfSignedCertificate PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate.md).

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

Эта команда создает тестовый сертификат, доступный в личном хранилище сертификатов текущего пользователя. Вы можете открыть хранилище сертификатов, запустив `certmgr.msc`, чтобы просмотреть созданный сертификат.

> [!Warning]
> NuGet.org не принимает пакеты, подписанные с помощью самовыданных сертификатов.

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>Управление требованиями к подписи для пакета на сайте NuGet.org
1. [Войдите](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) на сайт NuGet.org.

1. Перейдите в раздел `Manage Packages` 
   ![Настройка подписывающих лиц пакета](../reference/media/configure-package-signers.png).

* Если вы — единственный владелец пакета, вам нужно подписывающее лицо. То есть вы можете использовать любой из зарегистрированных сертификатов для подписи и публикации пакетов на сайте NuGet.org.

* Если у пакета несколько владельцев, по умолчанию для подписания можно использовать любые сертификаты владельца. Как совладелец пакета, вы можете указать себя или совладельца вместо значения "Любой". Если вы сделаете владельцем пользователя, у которого нет зарегистрированного сертификата, неподписанные пакеты будут запрещены. 

* Аналогично если по умолчанию для пакета, в котором у одного владельца зарегистрирован сертификат, а у другого — не зарегистрирован, выбран параметр "Любой", то в этом случае NuGet.org принимает подписанный пакет с подписью, зарегистрированной одним из владельцев, или неподписанный пакет (так как у одного из владельцев не зарегистрирован сертификат).

## <a name="related-articles"></a>Связанные статьи

- [Установка подписанных пакетов](../consume-packages/installing-signed-packages.md)
- [Справочник по подписанным пакетам](../reference/Signed-Packages-Reference.md)
