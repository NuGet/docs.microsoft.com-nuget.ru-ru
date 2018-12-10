---
title: Установка подписанного пакета NuGet
description: Описание процесса установки подписанных пакетов NuGet и настройки параметров доверия подписи пакетов.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 11ffaee96b6f6a9260f38c534328b6631cd96abf
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977838"
---
# <a name="install-a-signed-package"></a>Установка подписанного пакета

Для установки подписанных пакетов не требуются какие-либо специальные действия. Но если содержимое было изменено с момента подписания, установка блокируется и выдается ошибка [NU3008](../reference/errors-and-warnings/NU3008.md).

> [!Warning]
> Пакеты, подписанные с использованием недоверенных сертификатов, считаются неподписанными и устанавливаются без предупреждений или ошибок, как и любой другой неподписанный пакет.

## <a name="configure-package-signature-requirements"></a>Требования к настройке подписания пакетов

> [!Note]
> Требуется NuGet 4.9.0 и выше и Visual Studio версии 15.9 и более поздней в Windows.

Вы можете настроить способ проверки подписей пакетов в клиентах NuGet, задав для `signatureValidationMode` значение `require` в файле [nuget.config](../reference/nuget-config-file) с помощью команды [`nuget config`](../tools/cli-ref-config).

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

В этом режиме проверяется, все ли пакеты подписаны с использованием любых доверенных сертификатов в файле `nuget.config`. Этот файл позволяет указать доверенных авторов или репозитории на основе отпечатка сертификата.

### <a name="trust-package-author"></a>Доверие к автору пакета

Чтобы доверять пакету на основе подписи автора, используйте команду [`trusted-signers`](..tools/cli-ref-trusted-signers) для задания свойства `author` в файле nuget.config.

```cmd
nuget.exe  trusted-signers Add -Name MyCompanyCert -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256
```

```xml
<trustedSigners>
  <author name="MyCompanyCert">
    <certificate fingerprint="CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
  </author>
</trustedSigners>
```

>[!TIP]
>Используйте [команду проверки](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) `nuget.exe`, чтобы получить значение `SHA256` отпечатка сертификата.


### <a name="trust-all-packages-from-a-repository"></a>Доверие ко всем пакетам в репозитории

Для доверия к пакетам на основе подписи репозитория используйте элемент `repository`:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a>Доверие к владельцам пакета

Подписи репозиториев включают дополнительные метаданные для определения владельцев пакета во время отправки. Вы можете ограничить пакеты из репозитория на основе списка владельцев:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
      <owners>microsoft;nuget</owners>
  </repository>
</trustedSigners>
```

Если у пакета несколько владельцев, и как минимум один из них находится в списке доверенных, пакет будет установлен.

### <a name="untrusted-root-certificates"></a>Недоверенные корневые сертификаты

В некоторых случаях может потребоваться проверка с использованием сертификатов, которые не связаны цепочкой с доверенным корневым сертификатом на локальном компьютере. Для настройки этого поведения используйте атрибут `allowUntrustedRoot`.

### <a name="sync-repository-certificates"></a>Синхронизация сертификатов репозитория

Репозитории пакетов должны объявлять о сертификатах, используемых в [индексе службы](https://docs.microsoft.com/en-us/nuget/api/service-index). Со временем репозиторий обновит эти сертификаты, например, по истечении срока их действия. При этом клиенты с определенными политиками потребуют обновления конфигурации, чтобы включить новый добавленный сертификат. Вы можете легко обновить доверенных подписывающих лиц, связанных с репозиторием, с помощью [команды синхронизации доверенных подписывающих лиц](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-) `nuget.exe`.

### <a name="schema-reference"></a>Справочник схем

Полный справочник схем для политик клиентов см. в [справочнике nuget.config](/nuget/reference/nuget-config-file#trustedsigners-section)

## <a name="related-articles"></a>Связанные статьи

- [Способы установки пакета NuGet](ways-to-install-a-package.md)
- [Подписывание пакетов NuGet](../create-packages/Sign-a-Package.md)
- [Справочник по подписанным пакетам](../reference/Signed-Packages-Reference.md)
