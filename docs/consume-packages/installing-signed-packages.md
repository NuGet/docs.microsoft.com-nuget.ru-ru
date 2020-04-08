---
title: Управление границами доверия пакета
description: Описание процесса установки подписанных пакетов NuGet и настройки параметров доверия подписи пакетов.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 034b9dd9699af529e4d82d6ee5b1c42214673341
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428603"
---
# <a name="manage-package-trust-boundaries"></a><span data-ttu-id="a5cdd-103">Управление границами доверия пакета</span><span class="sxs-lookup"><span data-stu-id="a5cdd-103">Manage package trust boundaries</span></span>

<span data-ttu-id="a5cdd-104">Для установки подписанных пакетов не требуются какие-либо специальные действия. Но если содержимое было изменено с момента подписания, установка блокируется и выдается ошибка [NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="a5cdd-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="a5cdd-105">Пакеты, подписанные с использованием недоверенных сертификатов, считаются неподписанными и устанавливаются без предупреждений или ошибок, как и любой другой неподписанный пакет.</span><span class="sxs-lookup"><span data-stu-id="a5cdd-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="a5cdd-106">Требования к настройке подписания пакетов</span><span class="sxs-lookup"><span data-stu-id="a5cdd-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="a5cdd-107">Требуется NuGet 4.9.0 и выше и Visual Studio версии 15.9 и более поздней в Windows.</span><span class="sxs-lookup"><span data-stu-id="a5cdd-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="a5cdd-108">Вы можете настроить способ проверки подписей пакетов в клиентах NuGet, задав для `signatureValidationMode` значение `require` в файле [nuget.config](../reference/nuget-config-file.md) с помощью команды [`nuget config`](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="a5cdd-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file.md) file using the [`nuget config`](../reference/cli-reference/cli-ref-config.md) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="a5cdd-109">В этом режиме проверяется, все ли пакеты подписаны с использованием любых доверенных сертификатов в файле `nuget.config`.</span><span class="sxs-lookup"><span data-stu-id="a5cdd-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="a5cdd-110">Этот файл позволяет указать доверенных авторов или репозитории на основе отпечатка сертификата.</span><span class="sxs-lookup"><span data-stu-id="a5cdd-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="a5cdd-111">Доверие к автору пакета</span><span class="sxs-lookup"><span data-stu-id="a5cdd-111">Trust package author</span></span>

<span data-ttu-id="a5cdd-112">Чтобы доверять пакету на основе подписи автора, используйте команду [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) для задания свойства `author` в файле nuget.config.</span><span class="sxs-lookup"><span data-stu-id="a5cdd-112">To trust packages based on the author signature use the [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) command to set the `author` property in the nuget.config.</span></span>

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
><span data-ttu-id="a5cdd-113">Используйте [команду проверки](../reference/cli-reference/cli-ref-verify.md) `nuget.exe`, чтобы получить значение `SHA256` отпечатка сертификата.</span><span class="sxs-lookup"><span data-stu-id="a5cdd-113">Use the `nuget.exe` [verify command](../reference/cli-reference/cli-ref-verify.md) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="a5cdd-114">Доверие ко всем пакетам в репозитории</span><span class="sxs-lookup"><span data-stu-id="a5cdd-114">Trust all packages from a repository</span></span>

<span data-ttu-id="a5cdd-115">Для доверия к пакетам на основе подписи репозитория используйте элемент `repository`:</span><span class="sxs-lookup"><span data-stu-id="a5cdd-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="a5cdd-116">Доверие к владельцам пакета</span><span class="sxs-lookup"><span data-stu-id="a5cdd-116">Trust Package Owners</span></span>

<span data-ttu-id="a5cdd-117">Подписи репозиториев включают дополнительные метаданные для определения владельцев пакета во время отправки.</span><span class="sxs-lookup"><span data-stu-id="a5cdd-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="a5cdd-118">Вы можете ограничить пакеты из репозитория на основе списка владельцев:</span><span class="sxs-lookup"><span data-stu-id="a5cdd-118">You can restrict packages from a repository based on a list of owners:</span></span>

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

<span data-ttu-id="a5cdd-119">Если у пакета несколько владельцев, и как минимум один из них находится в списке доверенных, пакет будет установлен.</span><span class="sxs-lookup"><span data-stu-id="a5cdd-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="a5cdd-120">Недоверенные корневые сертификаты</span><span class="sxs-lookup"><span data-stu-id="a5cdd-120">Untrusted Root certificates</span></span>

<span data-ttu-id="a5cdd-121">В некоторых случаях может потребоваться проверка с использованием сертификатов, которые не связаны цепочкой с доверенным корневым сертификатом на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="a5cdd-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="a5cdd-122">Для настройки этого поведения используйте атрибут `allowUntrustedRoot`.</span><span class="sxs-lookup"><span data-stu-id="a5cdd-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="a5cdd-123">Синхронизация сертификатов репозитория</span><span class="sxs-lookup"><span data-stu-id="a5cdd-123">Sync repository certificates</span></span>

<span data-ttu-id="a5cdd-124">Репозитории пакетов должны объявлять о сертификатах, используемых в [индексе службы](../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="a5cdd-124">Package repositories should announce the certificates they use in their [service index](../api/service-index.md).</span></span> <span data-ttu-id="a5cdd-125">Со временем репозиторий обновит эти сертификаты, например, по истечении срока их действия.</span><span class="sxs-lookup"><span data-stu-id="a5cdd-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="a5cdd-126">При этом клиенты с определенными политиками потребуют обновления конфигурации, чтобы включить новый добавленный сертификат.</span><span class="sxs-lookup"><span data-stu-id="a5cdd-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="a5cdd-127">Вы можете легко обновить доверенных подписывающих лиц, связанных с репозиторием, с помощью [команды синхронизации доверенных подписывающих лиц](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name) `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="a5cdd-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="a5cdd-128">Справочник схем</span><span class="sxs-lookup"><span data-stu-id="a5cdd-128">Schema reference</span></span>

<span data-ttu-id="a5cdd-129">Полный справочник схем для политик клиентов см. в [справочнике nuget.config](../reference/nuget-config-file.md#trustedsigners-section)</span><span class="sxs-lookup"><span data-stu-id="a5cdd-129">The complete schema reference for the client policies can be found in the [nuget.config reference](../reference/nuget-config-file.md#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="a5cdd-130">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="a5cdd-130">Related articles</span></span>

- [<span data-ttu-id="a5cdd-131">Подписывание пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="a5cdd-131">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="a5cdd-132">Справочник по подписанным пакетам</span><span class="sxs-lookup"><span data-stu-id="a5cdd-132">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
