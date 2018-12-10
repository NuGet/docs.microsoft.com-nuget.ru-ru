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
# <a name="install-a-signed-package"></a><span data-ttu-id="d272f-103">Установка подписанного пакета</span><span class="sxs-lookup"><span data-stu-id="d272f-103">Install a signed package</span></span>

<span data-ttu-id="d272f-104">Для установки подписанных пакетов не требуются какие-либо специальные действия. Но если содержимое было изменено с момента подписания, установка блокируется и выдается ошибка [NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="d272f-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="d272f-105">Пакеты, подписанные с использованием недоверенных сертификатов, считаются неподписанными и устанавливаются без предупреждений или ошибок, как и любой другой неподписанный пакет.</span><span class="sxs-lookup"><span data-stu-id="d272f-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="d272f-106">Требования к настройке подписания пакетов</span><span class="sxs-lookup"><span data-stu-id="d272f-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="d272f-107">Требуется NuGet 4.9.0 и выше и Visual Studio версии 15.9 и более поздней в Windows.</span><span class="sxs-lookup"><span data-stu-id="d272f-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="d272f-108">Вы можете настроить способ проверки подписей пакетов в клиентах NuGet, задав для `signatureValidationMode` значение `require` в файле [nuget.config](../reference/nuget-config-file) с помощью команды [`nuget config`](../tools/cli-ref-config).</span><span class="sxs-lookup"><span data-stu-id="d272f-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file) file using the [`nuget config`](../tools/cli-ref-config) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="d272f-109">В этом режиме проверяется, все ли пакеты подписаны с использованием любых доверенных сертификатов в файле `nuget.config`.</span><span class="sxs-lookup"><span data-stu-id="d272f-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="d272f-110">Этот файл позволяет указать доверенных авторов или репозитории на основе отпечатка сертификата.</span><span class="sxs-lookup"><span data-stu-id="d272f-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="d272f-111">Доверие к автору пакета</span><span class="sxs-lookup"><span data-stu-id="d272f-111">Trust package author</span></span>

<span data-ttu-id="d272f-112">Чтобы доверять пакету на основе подписи автора, используйте команду [`trusted-signers`](..tools/cli-ref-trusted-signers) для задания свойства `author` в файле nuget.config.</span><span class="sxs-lookup"><span data-stu-id="d272f-112">To trust packages based on the author signature use the [`trusted-signers`](..tools/cli-ref-trusted-signers) command to set the `author` property in the nuget.config.</span></span>

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
><span data-ttu-id="d272f-113">Используйте [команду проверки](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) `nuget.exe`, чтобы получить значение `SHA256` отпечатка сертификата.</span><span class="sxs-lookup"><span data-stu-id="d272f-113">Use the `nuget.exe` [verify command](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="d272f-114">Доверие ко всем пакетам в репозитории</span><span class="sxs-lookup"><span data-stu-id="d272f-114">Trust all packages from a repository</span></span>

<span data-ttu-id="d272f-115">Для доверия к пакетам на основе подписи репозитория используйте элемент `repository`:</span><span class="sxs-lookup"><span data-stu-id="d272f-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="d272f-116">Доверие к владельцам пакета</span><span class="sxs-lookup"><span data-stu-id="d272f-116">Trust Package Owners</span></span>

<span data-ttu-id="d272f-117">Подписи репозиториев включают дополнительные метаданные для определения владельцев пакета во время отправки.</span><span class="sxs-lookup"><span data-stu-id="d272f-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="d272f-118">Вы можете ограничить пакеты из репозитория на основе списка владельцев:</span><span class="sxs-lookup"><span data-stu-id="d272f-118">You can restrict packages from a repository based on a list of owners:</span></span>

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

<span data-ttu-id="d272f-119">Если у пакета несколько владельцев, и как минимум один из них находится в списке доверенных, пакет будет установлен.</span><span class="sxs-lookup"><span data-stu-id="d272f-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="d272f-120">Недоверенные корневые сертификаты</span><span class="sxs-lookup"><span data-stu-id="d272f-120">Untrusted Root certificates</span></span>

<span data-ttu-id="d272f-121">В некоторых случаях может потребоваться проверка с использованием сертификатов, которые не связаны цепочкой с доверенным корневым сертификатом на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="d272f-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="d272f-122">Для настройки этого поведения используйте атрибут `allowUntrustedRoot`.</span><span class="sxs-lookup"><span data-stu-id="d272f-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="d272f-123">Синхронизация сертификатов репозитория</span><span class="sxs-lookup"><span data-stu-id="d272f-123">Sync repository certificates</span></span>

<span data-ttu-id="d272f-124">Репозитории пакетов должны объявлять о сертификатах, используемых в [индексе службы](https://docs.microsoft.com/en-us/nuget/api/service-index).</span><span class="sxs-lookup"><span data-stu-id="d272f-124">Package repositories should announce the certificates they use in their [service index](https://docs.microsoft.com/en-us/nuget/api/service-index).</span></span> <span data-ttu-id="d272f-125">Со временем репозиторий обновит эти сертификаты, например, по истечении срока их действия.</span><span class="sxs-lookup"><span data-stu-id="d272f-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="d272f-126">При этом клиенты с определенными политиками потребуют обновления конфигурации, чтобы включить новый добавленный сертификат.</span><span class="sxs-lookup"><span data-stu-id="d272f-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="d272f-127">Вы можете легко обновить доверенных подписывающих лиц, связанных с репозиторием, с помощью [команды синхронизации доверенных подписывающих лиц](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-) `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="d272f-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="d272f-128">Справочник схем</span><span class="sxs-lookup"><span data-stu-id="d272f-128">Schema reference</span></span>

<span data-ttu-id="d272f-129">Полный справочник схем для политик клиентов см. в [справочнике nuget.config](/nuget/reference/nuget-config-file#trustedsigners-section)</span><span class="sxs-lookup"><span data-stu-id="d272f-129">The complete schema reference for the client policies can be found in the [nuget.config reference](/nuget/reference/nuget-config-file#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="d272f-130">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="d272f-130">Related articles</span></span>

- [<span data-ttu-id="d272f-131">Способы установки пакета NuGet</span><span class="sxs-lookup"><span data-stu-id="d272f-131">Different ways to install a NuGet Package</span></span>](ways-to-install-a-package.md)
- [<span data-ttu-id="d272f-132">Подписывание пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="d272f-132">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="d272f-133">Справочник по подписанным пакетам</span><span class="sxs-lookup"><span data-stu-id="d272f-133">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
