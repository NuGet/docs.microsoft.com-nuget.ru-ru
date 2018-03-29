---
title: Подпись ссылки на пакеты | Документы Microsoft
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Подписанные пакеты описание компонента.
keywords: Знак пакета NuGet, подписи, сертификат
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: a2a338596f7d98ded11da6fb02bafba3521249ab
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="signed-packages"></a>Подписанные пакеты

*NuGet 4.6.0+ и Visual Studio 2017 г 15.6 и более поздних версий*

Пакеты NuGet можно включить цифровую подпись, которая обеспечивает защиту от поддельных содержимого. Эта подпись создается из сертификата X.509, который также добавляет экспериментов подлинность фактического источника пакета.

Подписанные пакеты обеспечивают надежную проверку начала до конца. Сигнатура автор гарантирует, что пакет не был изменен с момента автор подписи пакета, независимо от того, из которой репозитория или что транспорта метод доставки пакета.

Потребителей, которым требуется закрытой среде может потребоваться пакеты, подписанные сертификатом, определенных автором.

Кроме того автор подписи пакетов предоставляют механизм дополнительную проверку подлинности в конвейер публикации nuget.org из-за сертификата для подписи должны быть зарегистрированы заранее.

Дополнительные сведения о создании подписанного пакета см. в разделе [подписи пакетов](../create-packages/Sign-a-package.md) и [входа команды nuget](../tools/cli-ref-sign.md).

> [!Important]
> в настоящее время NuGet.org не принимает подписанных пакетов. Вы можете подписывать пакеты для публикации в пользовательских веб-каналах.

## <a name="certificate-requirements"></a>Требования к сертификатам

Подписание пакета требуется сертификат, который — это специальный тип сертификата, который является допустимым для подписи кода `id-kp-codeSigning` цель [[RFC 5280 раздел 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Кроме того сертификат должен иметь RSA длина открытого ключа 2048 бит или более поздней версии.

## <a name="get-a-code-signing-certificate"></a>Получить сертификат подписи кода

Действительные сертификаты могут быть получены из открытых сертификации, таких как:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Глобальные входа](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

Полный список центров сертификации, доверенным для Windows можно получить из [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Создание тестового сертификата

Самостоятельно выданные сертификаты можно использовать для тестирования. Чтобы создать самостоятельно выданный сертификат, используйте [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) команды PowerShell.

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

Эта команда создает сертификата тестирования в хранилище персональных сертификатов текущего пользователя. Можно открыть хранилище сертификатов, выполнив `certmgr.msc` для просмотра только что созданный сертификат.

## <a name="timestamp-requirements"></a>Требования к отметки времени

Подписанных пакетов должна включать отметок времени RFC 3161, чтобы обеспечить правильность подписи за пределы периода действия сертификата для подписи пакетов. Сертификат, используемый для подписи отметку времени должен быть допустимым для `id-kp-timeStamping` цель [[RFC 5280 раздел 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Кроме того сертификат должен иметь RSA длина открытого ключа 2048 бит или более поздней версии.

Дополнительные технические сведения можно найти в [пакет подпись технические спецификации](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).
