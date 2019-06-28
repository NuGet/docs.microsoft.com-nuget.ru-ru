---
title: Доверенные подписавших команды интерфейса командной строки NuGet
description: Справочник по командам доверенные подписавших nuget.exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c22c7f0a6b6878bec4f8396e02e2d97998170455
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425985"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="6ad6c-103">Команда доверенного подписавших (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6ad6c-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="6ad6c-104">**Применяется к:** упаковать потребления &bullet; **поддерживаемые версии:** 4.9.1+</span><span class="sxs-lookup"><span data-stu-id="6ad6c-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="6ad6c-105">Возвращает или задает доверенных подписавших конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="6ad6c-106">Избыточное использование см. в разделе [NuGet распространенных конфигураций](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="6ad6c-106">For additional usage, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="6ad6c-107">Дополнительные сведения о как схема nuget.config, как выглядит, см. [ссылку на файл конфигурации NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="6ad6c-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="6ad6c-108">Использование</span><span class="sxs-lookup"><span data-stu-id="6ad6c-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="6ad6c-109">Если ни один из `list|add|remove|sync` указан, команда по умолчанию будет `list`.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="6ad6c-110">список доверенных подписавших NuGet</span><span class="sxs-lookup"><span data-stu-id="6ad6c-110">nuget trusted-signers list</span></span>

<span data-ttu-id="6ad6c-111">Список всех доверенных авторов в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="6ad6c-112">Этот параметр будет включать все сертификаты (с помощью отпечатков пальцев и алгоритм отпечатков пальцев) у каждого подписывающего.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="6ad6c-113">Если сертификат имеет предшествующий `[U]`, это означает, что запись сертификат имеет `allowUntrustedRoot` задать в качестве `true`.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="6ad6c-114">Ниже приведен пример выходных данных этой команды:</span><span class="sxs-lookup"><span data-stu-id="6ad6c-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="6ad6c-115">доверенные подписавших NuGet add [параметры]</span><span class="sxs-lookup"><span data-stu-id="6ad6c-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="6ad6c-116">Добавляет доверенным лицом, с заданным именем в файле конфигурации. Этот параметр может иметь разные жесты Добавление доверенных автора или репозитория.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="6ad6c-117">Параметры установки, на основе пакета</span><span class="sxs-lookup"><span data-stu-id="6ad6c-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="6ad6c-118">где `<package(s)>` — это один или несколько `.nupkg` файлов.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="6ad6c-119">Параметр</span><span class="sxs-lookup"><span data-stu-id="6ad6c-119">Option</span></span> | <span data-ttu-id="6ad6c-120">Описание</span><span class="sxs-lookup"><span data-stu-id="6ad6c-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6ad6c-121">Дизайнер</span><span class="sxs-lookup"><span data-stu-id="6ad6c-121">Author</span></span> | <span data-ttu-id="6ad6c-122">Указывает, что автор подписи пакетов должен быть доверенным.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="6ad6c-123">WMI</span><span class="sxs-lookup"><span data-stu-id="6ad6c-123">Repository</span></span> | <span data-ttu-id="6ad6c-124">Указывает, что репозиторий подпись или скрепляющая подпись из пакетов должен быть доверенным.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="6ad6c-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="6ad6c-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="6ad6c-126">Указывает, если сертификат доверенным лицом должны создать недоверенный корневой цепочку.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="6ad6c-127">Владельцы</span><span class="sxs-lookup"><span data-stu-id="6ad6c-127">Owners</span></span> | <span data-ttu-id="6ad6c-128">Разделенный точками с запятой список доверенных владельцев для дальнейшего ограничения доверительные отношения с репозиторием.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="6ad6c-129">Допустимо только при использовании `-Repository` параметр.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="6ad6c-130">Одновременное предоставление `-Author` и `-Repository` в то же время не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="6ad6c-131">Параметры установки, на основе индекса службы</span><span class="sxs-lookup"><span data-stu-id="6ad6c-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="6ad6c-132">_Примечание_. Этот параметр будет добавлять только доверенных репозиториев.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="6ad6c-133">Параметр</span><span class="sxs-lookup"><span data-stu-id="6ad6c-133">Option</span></span> | <span data-ttu-id="6ad6c-134">Описание</span><span class="sxs-lookup"><span data-stu-id="6ad6c-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6ad6c-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="6ad6c-135">ServiceIndex</span></span> | <span data-ttu-id="6ad6c-136">Указывает индекс службы V3 репозитория доверенными.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="6ad6c-137">Этот репозиторий содержит для поддержки ресурса подписи репозитория.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="6ad6c-138">Если не указано, команда будет искать источник пакета с тем же `-Name` и получить индекс службы оттуда.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="6ad6c-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="6ad6c-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="6ad6c-140">Указывает, если сертификат доверенным лицом должны создать недоверенный корневой цепочку.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="6ad6c-141">Владельцы</span><span class="sxs-lookup"><span data-stu-id="6ad6c-141">Owners</span></span> | <span data-ttu-id="6ad6c-142">Разделенный точками с запятой список доверенных владельцев для дальнейшего ограничения доверительные отношения с репозиторием.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="6ad6c-143">Параметры установки, в зависимости от сведений о сертификате</span><span class="sxs-lookup"><span data-stu-id="6ad6c-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="6ad6c-144">_Примечание_. Если доверенным лицом, с заданным именем уже существует, будет добавлен элемент сертификат для этого подписавшего.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="6ad6c-145">В противном случае будет создан доверенным автора с элементом сертификата из определенных сведений о сертификате.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="6ad6c-146">Параметр</span><span class="sxs-lookup"><span data-stu-id="6ad6c-146">Option</span></span> | <span data-ttu-id="6ad6c-147">Описание</span><span class="sxs-lookup"><span data-stu-id="6ad6c-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6ad6c-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="6ad6c-148">CertificateFingerprint</span></span> | <span data-ttu-id="6ad6c-149">Указывает сертификат, который должен быть подписан отпечатков сертификата, который подписанных пакетов.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="6ad6c-150">Отпечаток сертификата — это хэш сертификата.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="6ad6c-151">Задает алгоритм хэширования, используемый для вычисления этого хэш-кода должен быть в `FingerprintAlgorithm` параметр.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="6ad6c-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="6ad6c-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="6ad6c-153">Задает алгоритм хэширования, используемый для вычисления отпечаток сертификата.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="6ad6c-154">По умолчанию — `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="6ad6c-155">Поддерживаемые значения `SHA256`, `SHA384` и `SHA512`</span><span class="sxs-lookup"><span data-stu-id="6ad6c-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="6ad6c-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="6ad6c-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="6ad6c-157">Указывает, если сертификат доверенным лицом должны создать недоверенный корневой цепочку.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="6ad6c-158">удалить доверенный подписавших NuGet - имя <name></span><span class="sxs-lookup"><span data-stu-id="6ad6c-158">nuget trusted-signers remove -Name <name></span></span>

<span data-ttu-id="6ad6c-159">Удаляет все доверенных авторов, которые соответствуют заданному имени.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="6ad6c-160">синхронизировать доверенные подписавших NuGet - имя <name></span><span class="sxs-lookup"><span data-stu-id="6ad6c-160">nuget trusted-signers sync -Name <name></span></span>

<span data-ttu-id="6ad6c-161">Запрашивает обновленный список сертификатов, используемых в настоящее время доверенного хранилища для обновления существующего списка сертификатов в доверенным лицом.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="6ad6c-162">_Примечание_. Этот жест будет удалить текущий список сертификатов и замените их список актуальных из репозитория.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="6ad6c-163">Параметры</span><span class="sxs-lookup"><span data-stu-id="6ad6c-163">Options</span></span>

| <span data-ttu-id="6ad6c-164">Параметр</span><span class="sxs-lookup"><span data-stu-id="6ad6c-164">Option</span></span> | <span data-ttu-id="6ad6c-165">Описание</span><span class="sxs-lookup"><span data-stu-id="6ad6c-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6ad6c-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6ad6c-166">ConfigFile</span></span> | <span data-ttu-id="6ad6c-167">Чтобы применить файл конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6ad6c-168">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="6ad6c-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="6ad6c-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6ad6c-169">ForceEnglishOutput</span></span> | <span data-ttu-id="6ad6c-170">Nuget.exe силы для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6ad6c-171">Help</span><span class="sxs-lookup"><span data-stu-id="6ad6c-171">Help</span></span> | <span data-ttu-id="6ad6c-172">Отображает справку для команды.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="6ad6c-173">Verbosity</span><span class="sxs-lookup"><span data-stu-id="6ad6c-173">Verbosity</span></span> | <span data-ttu-id="6ad6c-174">Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="6ad6c-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="6ad6c-175">Примеры</span><span class="sxs-lookup"><span data-stu-id="6ad6c-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
