---
title: "Подписывание пакетов NuGet | Документы Майкрософт"
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Описание того, как подписанные пакеты можно использовать, чтобы включить проверку целостности содержимого."
keywords: "Подписывание пакетов NuGet, безопасность NuGet, создание подписанных пакетов"
ms.reviewer:
- karann-msft
- anangaur
ms.openlocfilehash: aaf6ab7d7a9e66d4d9519d8aa79f0d0fac646d3a
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="c7220-104">Подписывание пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="c7220-104">Signing NuGet Packages</span></span>

<span data-ttu-id="c7220-105">Подписывание пакета — это процесс, который гарантирует, что пакет не был изменен с момента создания.</span><span class="sxs-lookup"><span data-stu-id="c7220-105">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7220-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c7220-106">Prerequisites</span></span>

1. <span data-ttu-id="c7220-107">Пакет (файл `.nupkg`) для подписывания.</span><span class="sxs-lookup"><span data-stu-id="c7220-107">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="c7220-108">См. статью [Создание пакета](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="c7220-108">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="c7220-109">nuget.exe 4.6.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="c7220-109">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="c7220-110">См. статью [Установка интерфейса командной строки NuGet](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="c7220-110">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="c7220-111">[Сертификат подписывания кода](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="c7220-111">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

> [!Warning]
> <span data-ttu-id="c7220-112">Сейчас nuget.org не принимает подписанные пакеты.</span><span class="sxs-lookup"><span data-stu-id="c7220-112">nuget.org does not currently accept signed packages.</span></span> <span data-ttu-id="c7220-113">Вы можете подписывать пакеты для публикации в пользовательских веб-каналах.</span><span class="sxs-lookup"><span data-stu-id="c7220-113">You can sign packages for publishing to custom feeds.</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="c7220-114">Подписывание пакета</span><span class="sxs-lookup"><span data-stu-id="c7220-114">Sign a package</span></span>

<span data-ttu-id="c7220-115">Чтобы подписать пакет, используйте [nuget sign](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="c7220-115">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="c7220-116">Как описано в справочнике по командам, можно использовать сертификат, доступный в хранилище сертификатов, или сертификат из файла.</span><span class="sxs-lookup"><span data-stu-id="c7220-116">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="c7220-117">Распространенные проблемы при подписывании пакета</span><span class="sxs-lookup"><span data-stu-id="c7220-117">Common problems when signing a package</span></span>

- <span data-ttu-id="c7220-118">Недопустимый сертификат для подписывания кода.</span><span class="sxs-lookup"><span data-stu-id="c7220-118">The certificate is not valid for code signing.</span></span> <span data-ttu-id="c7220-119">Убедитесь, что указанный сертификат имеет подходящее расширенное использование ключа (EKU 1.3.6.1.5.5.7.3.3).</span><span class="sxs-lookup"><span data-stu-id="c7220-119">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="c7220-120">Сертификат не удовлетворяет базовым требованиям, таким как алгоритм подписи RSA SHA-256 или открытый ключ размером 2048 бит или больше.</span><span class="sxs-lookup"><span data-stu-id="c7220-120">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="c7220-121">Сертификат устарел или отозван.</span><span class="sxs-lookup"><span data-stu-id="c7220-121">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="c7220-122">Сервера меток времени не удовлетворяет требованиям к сертификату.</span><span class="sxs-lookup"><span data-stu-id="c7220-122">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="c7220-123">Подписанные пакеты должны включать метку времени, чтобы подпись оставалась действительной после истечения срока действия сертификата для подписывания.</span><span class="sxs-lookup"><span data-stu-id="c7220-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="c7220-124">При подписывании без метки времени операция sign вызывает [предупреждение NU3002](../reference/Errors-and-Warnings.md#nu3002).</span><span class="sxs-lookup"><span data-stu-id="c7220-124">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="c7220-125">Проверка подписанного пакета</span><span class="sxs-lookup"><span data-stu-id="c7220-125">Verify a signed package</span></span>

<span data-ttu-id="c7220-126">Используйте [nuget verify](../tools/cli-ref-verify.md), чтобы просмотреть сведения о подписи заданного пакета.</span><span class="sxs-lookup"><span data-stu-id="c7220-126">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="c7220-127">Установка подписанного пакета</span><span class="sxs-lookup"><span data-stu-id="c7220-127">Install a signed package</span></span>

<span data-ttu-id="c7220-128">Для установки подписанных пакетов не требуются какие-либо специальные действия.Но если содержимое было изменено с момента подписания, установка блокируется и выдается [ошибка NU3008](../reference/Errors-and-Warnings.md#nu3008).</span><span class="sxs-lookup"><span data-stu-id="c7220-128">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="c7220-129">Пакеты, подписанные с использованием недоверенных сертификатов, считаются неподписанными и устанавливаются без предупреждений или ошибок, как и любой другой неподписанный пакет.</span><span class="sxs-lookup"><span data-stu-id="c7220-129">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="c7220-130">См. также</span><span class="sxs-lookup"><span data-stu-id="c7220-130">See also</span></span>

[<span data-ttu-id="c7220-131">Справочник по подписанным пакетам</span><span class="sxs-lookup"><span data-stu-id="c7220-131">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
