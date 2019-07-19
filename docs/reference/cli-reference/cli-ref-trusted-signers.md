---
title: Команда NuGet CLI Trusted-Signs
description: Справочные сведения для команды NuGet. exe Trusted-Signs
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 197f2eaeed1a4a11f0f3ed426534807a0136271e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327541"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="ebdc6-103">Команда Trusted-Signs (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="ebdc6-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="ebdc6-104">Область **применения:** &bullet; **Поддерживаемые версии** потребления пакетов: 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="ebdc6-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="ebdc6-105">Возвращает или задает доверенных подписывающих для конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="ebdc6-106">Дополнительные сведения об использовании см. в разделе [Общие конфигурации NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ebdc6-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="ebdc6-107">Дополнительные сведения о том, как выглядит схема NuGet. config, см. в [справочнике по файлу конфигурации NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="ebdc6-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="ebdc6-108">Использование</span><span class="sxs-lookup"><span data-stu-id="ebdc6-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="ebdc6-109">Если ни один `list|add|remove|sync` из не указан, команда будет `list`по умолчанию иметь значение.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="ebdc6-110">список доверенных-подписывающихй NuGet</span><span class="sxs-lookup"><span data-stu-id="ebdc6-110">nuget trusted-signers list</span></span>

<span data-ttu-id="ebdc6-111">Список всех доверенных подписывающих удостоверений в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="ebdc6-112">Этот параметр будет включать все сертификаты (с использованием отпечатка пальца и алгоритма отпечатков пальцев) для каждого знака.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="ebdc6-113">Если сертификат уже существует `[U]`, это означает, что запись сертификата имеет `allowUntrustedRoot` значение `true`.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="ebdc6-114">Ниже приведен пример выходных данных этой команды:</span><span class="sxs-lookup"><span data-stu-id="ebdc6-114">Below is an example output from this command:</span></span>

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

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="ebdc6-115">NuGet Trusted-Signs Add [параметры]</span><span class="sxs-lookup"><span data-stu-id="ebdc6-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="ebdc6-116">Добавляет доверенный подписывающий с заданным именем в конфигурацию. Этот параметр имеет разные жесты для добавления доверенного автора или репозитория.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="ebdc6-117">Параметры для добавления на основе пакета</span><span class="sxs-lookup"><span data-stu-id="ebdc6-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="ebdc6-118">где `<package(s)>` — один или несколько `.nupkg` файлов.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="ebdc6-119">Параметр</span><span class="sxs-lookup"><span data-stu-id="ebdc6-119">Option</span></span> | <span data-ttu-id="ebdc6-120">Описание</span><span class="sxs-lookup"><span data-stu-id="ebdc6-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ebdc6-121">Дизайнер</span><span class="sxs-lookup"><span data-stu-id="ebdc6-121">Author</span></span> | <span data-ttu-id="ebdc6-122">Указывает, что подпись автора пакетов должна быть доверенной.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="ebdc6-123">WMI</span><span class="sxs-lookup"><span data-stu-id="ebdc6-123">Repository</span></span> | <span data-ttu-id="ebdc6-124">Указывает, что подпись репозитория или подпись другой стороны пакетов должны быть доверенными.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="ebdc6-125">алловунтрустедрут</span><span class="sxs-lookup"><span data-stu-id="ebdc6-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="ebdc6-126">Указывает, следует ли разрешить сертификату доверенного пользователя связываться с корнем без доверия.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="ebdc6-127">Владельцы</span><span class="sxs-lookup"><span data-stu-id="ebdc6-127">Owners</span></span> | <span data-ttu-id="ebdc6-128">Разделенный точками с запятой список доверенных владельцев для дальнейшего ограничения доверия репозитория.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="ebdc6-129">Допустимо только при использовании `-Repository` параметра.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="ebdc6-130">Одновременное `-Author` предоставление `-Repository` обоих и одновременно не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="ebdc6-131">Параметры для добавления на основе индекса службы</span><span class="sxs-lookup"><span data-stu-id="ebdc6-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="ebdc6-132">_Примечание_. При выборе этого варианта будут добавлены только доверенные репозитории.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="ebdc6-133">Параметр</span><span class="sxs-lookup"><span data-stu-id="ebdc6-133">Option</span></span> | <span data-ttu-id="ebdc6-134">Описание</span><span class="sxs-lookup"><span data-stu-id="ebdc6-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ebdc6-135">сервицеиндекс</span><span class="sxs-lookup"><span data-stu-id="ebdc6-135">ServiceIndex</span></span> | <span data-ttu-id="ebdc6-136">Указывает индекс службы для доверенного репозитория версии 3.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="ebdc6-137">Этот репозиторий должен поддерживать ресурс подписей репозитория.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="ebdc6-138">Если этот параметр не указан, команда будет искать источник пакета с тем же `-Name` и получить индекс службы.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="ebdc6-139">алловунтрустедрут</span><span class="sxs-lookup"><span data-stu-id="ebdc6-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="ebdc6-140">Указывает, следует ли разрешить сертификату доверенного пользователя связываться с корнем без доверия.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="ebdc6-141">Владельцы</span><span class="sxs-lookup"><span data-stu-id="ebdc6-141">Owners</span></span> | <span data-ttu-id="ebdc6-142">Разделенный точками с запятой список доверенных владельцев для дальнейшего ограничения доверия репозитория.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="ebdc6-143">Параметры для добавления на основе сведений о сертификате</span><span class="sxs-lookup"><span data-stu-id="ebdc6-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="ebdc6-144">_Примечание_. Если доверенный подписывающий с данным именем уже существует, элемент сертификата будет добавлен в этот подписывающий.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="ebdc6-145">В противном случае доверенный автор будет создан с помощью элемента сертификата из указанных сведений о сертификате.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="ebdc6-146">Параметр</span><span class="sxs-lookup"><span data-stu-id="ebdc6-146">Option</span></span> | <span data-ttu-id="ebdc6-147">Описание</span><span class="sxs-lookup"><span data-stu-id="ebdc6-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ebdc6-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="ebdc6-148">CertificateFingerprint</span></span> | <span data-ttu-id="ebdc6-149">Указывает отпечатки сертификата сертификата, для которого подписанные пакеты должны быть подписаны.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="ebdc6-150">Отпечаток сертификата — это хэш сертификата.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="ebdc6-151">Хэш-алгоритм, используемый для вычисления этого хэша, `FingerprintAlgorithm` должен быть указан в параметре.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="ebdc6-152">финжерпринталгорисм</span><span class="sxs-lookup"><span data-stu-id="ebdc6-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="ebdc6-153">Указывает хэш-алгоритм, используемый для вычисления отпечатка сертификата.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="ebdc6-154">По умолчанию — `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="ebdc6-155">Поддерживаются `SHA256`значения, `SHA384` и`SHA512`</span><span class="sxs-lookup"><span data-stu-id="ebdc6-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="ebdc6-156">алловунтрустедрут</span><span class="sxs-lookup"><span data-stu-id="ebdc6-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="ebdc6-157">Указывает, следует ли разрешить сертификату доверенного пользователя связываться с корнем без доверия.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="ebdc6-158">список доверенных-подписывающихй NuGet Remove-Name<name></span><span class="sxs-lookup"><span data-stu-id="ebdc6-158">nuget trusted-signers remove -Name <name></span></span>

<span data-ttu-id="ebdc6-159">Удаляет все доверенные подписывающих, соответствующие заданному имени.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="ebdc6-160">Синхронизация доверенных подписывающихй NuGet-имя<name></span><span class="sxs-lookup"><span data-stu-id="ebdc6-160">nuget trusted-signers sync -Name <name></span></span>

<span data-ttu-id="ebdc6-161">Запрашивает последний список сертификатов, используемых в доверенном репозитории, чтобы обновить существующий список сертификатов в доверенном подписавшем.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="ebdc6-162">_Примечание_. Этот жест удалит текущий список сертификатов и заменит их актуальным списком из репозитория.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="ebdc6-163">Параметры</span><span class="sxs-lookup"><span data-stu-id="ebdc6-163">Options</span></span>

| <span data-ttu-id="ebdc6-164">Параметр</span><span class="sxs-lookup"><span data-stu-id="ebdc6-164">Option</span></span> | <span data-ttu-id="ebdc6-165">Описание</span><span class="sxs-lookup"><span data-stu-id="ebdc6-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ebdc6-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ebdc6-166">ConfigFile</span></span> | <span data-ttu-id="ebdc6-167">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ebdc6-168">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="ebdc6-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ebdc6-169">форцеенглишаутпут</span><span class="sxs-lookup"><span data-stu-id="ebdc6-169">ForceEnglishOutput</span></span> | <span data-ttu-id="ebdc6-170">Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ebdc6-171">Help</span><span class="sxs-lookup"><span data-stu-id="ebdc6-171">Help</span></span> | <span data-ttu-id="ebdc6-172">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="ebdc6-173">Verbosity</span><span class="sxs-lookup"><span data-stu-id="ebdc6-173">Verbosity</span></span> | <span data-ttu-id="ebdc6-174">Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*.</span><span class="sxs-lookup"><span data-stu-id="ebdc6-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="ebdc6-175">Примеры</span><span class="sxs-lookup"><span data-stu-id="ebdc6-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
