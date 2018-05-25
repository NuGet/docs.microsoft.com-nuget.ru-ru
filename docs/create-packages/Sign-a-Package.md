---
title: Подписывание пакетов NuGet
description: Описание того, как подписанные пакеты можно использовать, чтобы включить проверку целостности содержимого.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 9900db1970a89de129d9074e5900e0aa048101de
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/22/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="95d8e-103">Подписывание пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="95d8e-103">Signing NuGet Packages</span></span>

<span data-ttu-id="95d8e-104">Подписывание пакета — это процесс, который гарантирует, что пакет не был изменен с момента создания.</span><span class="sxs-lookup"><span data-stu-id="95d8e-104">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95d8e-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="95d8e-105">Prerequisites</span></span>

1. <span data-ttu-id="95d8e-106">Пакет (файл `.nupkg`) для подписывания.</span><span class="sxs-lookup"><span data-stu-id="95d8e-106">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="95d8e-107">См. статью [Создание пакета](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="95d8e-107">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="95d8e-108">nuget.exe 4.6.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="95d8e-108">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="95d8e-109">См. статью [Установка интерфейса командной строки NuGet](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="95d8e-109">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="95d8e-110">[Сертификат подписывания кода](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="95d8e-110">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="95d8e-111">Подписывание пакета</span><span class="sxs-lookup"><span data-stu-id="95d8e-111">Sign a package</span></span>

<span data-ttu-id="95d8e-112">Чтобы подписать пакет, используйте [nuget sign](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="95d8e-112">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="95d8e-113">Как описано в справочнике по командам, можно использовать сертификат, доступный в хранилище сертификатов, или сертификат из файла.</span><span class="sxs-lookup"><span data-stu-id="95d8e-113">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="95d8e-114">Распространенные проблемы при подписывании пакета</span><span class="sxs-lookup"><span data-stu-id="95d8e-114">Common problems when signing a package</span></span>

- <span data-ttu-id="95d8e-115">Недопустимый сертификат для подписывания кода.</span><span class="sxs-lookup"><span data-stu-id="95d8e-115">The certificate is not valid for code signing.</span></span> <span data-ttu-id="95d8e-116">Убедитесь, что указанный сертификат имеет подходящее расширенное использование ключа (EKU 1.3.6.1.5.5.7.3.3).</span><span class="sxs-lookup"><span data-stu-id="95d8e-116">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="95d8e-117">Сертификат не удовлетворяет базовым требованиям, таким как алгоритм подписи RSA SHA-256 или открытый ключ размером 2048 бит или больше.</span><span class="sxs-lookup"><span data-stu-id="95d8e-117">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="95d8e-118">Сертификат устарел или отозван.</span><span class="sxs-lookup"><span data-stu-id="95d8e-118">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="95d8e-119">Сервера меток времени не удовлетворяет требованиям к сертификату.</span><span class="sxs-lookup"><span data-stu-id="95d8e-119">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="95d8e-120">Подписанные пакеты должны включать метку времени, чтобы подпись оставалась действительной после истечения срока действия сертификата для подписывания.</span><span class="sxs-lookup"><span data-stu-id="95d8e-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="95d8e-121">При подписывании без метки времени операция sign вызывает [предупреждение NU3002](../reference/Errors-and-Warnings.md#nu3002).</span><span class="sxs-lookup"><span data-stu-id="95d8e-121">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="95d8e-122">Проверка подписанного пакета</span><span class="sxs-lookup"><span data-stu-id="95d8e-122">Verify a signed package</span></span>

<span data-ttu-id="95d8e-123">Используйте [nuget verify](../tools/cli-ref-verify.md), чтобы просмотреть сведения о подписи заданного пакета.</span><span class="sxs-lookup"><span data-stu-id="95d8e-123">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="95d8e-124">Установка подписанного пакета</span><span class="sxs-lookup"><span data-stu-id="95d8e-124">Install a signed package</span></span>

<span data-ttu-id="95d8e-125">Для установки подписанных пакетов не требуются какие-либо специальные действия.Но если содержимое было изменено с момента подписания, установка блокируется и выдается [ошибка NU3008](../reference/Errors-and-Warnings.md#nu3008).</span><span class="sxs-lookup"><span data-stu-id="95d8e-125">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="95d8e-126">Пакеты, подписанные с использованием недоверенных сертификатов, считаются неподписанными и устанавливаются без предупреждений или ошибок, как и любой другой неподписанный пакет.</span><span class="sxs-lookup"><span data-stu-id="95d8e-126">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="95d8e-127">См. также</span><span class="sxs-lookup"><span data-stu-id="95d8e-127">See also</span></span>

[<span data-ttu-id="95d8e-128">Справочник по подписанным пакетам</span><span class="sxs-lookup"><span data-stu-id="95d8e-128">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
