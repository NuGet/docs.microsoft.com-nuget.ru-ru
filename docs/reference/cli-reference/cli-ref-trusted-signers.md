---
title: Команда NuGet CLI Trusted-Signs
description: Справочник по команде nuget.exe Trusted-Signs
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: a5f3564af8b96dfa673d2252aea2e77a79c184a4
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323594"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="903ba-103">Команда Trusted-Signs (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="903ba-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="903ba-104">Область **применения:** &bullet; **Поддерживаемые версии** потребления пакетов: 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="903ba-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="903ba-105">Возвращает или задает доверенных подписывающих для конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="903ba-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="903ba-106">Дополнительные сведения об использовании см. в разделе [Общие конфигурации NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="903ba-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="903ba-107">Дополнительные сведения о том, как выглядит схема nuget.config, см. в [справочнике по файлу конфигурации NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="903ba-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="903ba-108">Использование</span><span class="sxs-lookup"><span data-stu-id="903ba-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="903ba-109">Если ни один из `list|add|remove|sync` не указан, команда будет по умолчанию иметь значение `list` .</span><span class="sxs-lookup"><span data-stu-id="903ba-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="903ba-110">список доверенных-подписывающихй NuGet</span><span class="sxs-lookup"><span data-stu-id="903ba-110">nuget trusted-signers list</span></span>

<span data-ttu-id="903ba-111">Список всех доверенных подписывающих удостоверений в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="903ba-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="903ba-112">Этот параметр будет включать все сертификаты (с использованием отпечатка пальца и алгоритма отпечатков пальцев) для каждого знака.</span><span class="sxs-lookup"><span data-stu-id="903ba-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="903ba-113">Если сертификат уже существует `[U]` , это означает, что запись сертификата имеет `allowUntrustedRoot` значение `true` .</span><span class="sxs-lookup"><span data-stu-id="903ba-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="903ba-114">Ниже приведен пример выходных данных этой команды:</span><span class="sxs-lookup"><span data-stu-id="903ba-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D
        SHA256 - 5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="903ba-115">NuGet Trusted-Signs Add [параметры]</span><span class="sxs-lookup"><span data-stu-id="903ba-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="903ba-116">Добавляет доверенный подписывающий с заданным именем в конфигурацию. Этот параметр имеет разные жесты для добавления доверенного автора или репозитория.</span><span class="sxs-lookup"><span data-stu-id="903ba-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="903ba-117">Параметры для добавления на основе пакета</span><span class="sxs-lookup"><span data-stu-id="903ba-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package> -Name <name> [options]
```

<span data-ttu-id="903ba-118">где `<package>` — один подписанный `.nupkg` файл.</span><span class="sxs-lookup"><span data-stu-id="903ba-118">where `<package>` is one signed `.nupkg` file.</span></span>

- **`-Author`**

  <span data-ttu-id="903ba-119">Указывает, что подпись автора подписанного пакета должна быть доверенной.</span><span class="sxs-lookup"><span data-stu-id="903ba-119">Specifies that the author signature of the signed package should be trusted.</span></span>

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="903ba-120">Указывает, следует ли разрешить сертификату доверенного пользователя связываться с корнем без доверия.</span><span class="sxs-lookup"><span data-stu-id="903ba-120">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="903ba-121">Разделенный точками с запятой список доверенных владельцев для дальнейшего ограничения доверия репозитория.</span><span class="sxs-lookup"><span data-stu-id="903ba-121">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="903ba-122">Допустимо только при использовании `-Repository` параметра.</span><span class="sxs-lookup"><span data-stu-id="903ba-122">Only valid when using the `-Repository` option.</span></span>

- **`-Repository`**

  <span data-ttu-id="903ba-123">Указывает, что подпись репозитория или подпись другой стороны подписанного пакета должны быть доверенными.</span><span class="sxs-lookup"><span data-stu-id="903ba-123">Specifies that the repository signature or countersignature of the signed package should be trusted.</span></span>

<span data-ttu-id="903ba-124">Одновременное предоставление обоих `-Author` и `-Repository` одновременно не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="903ba-124">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="903ba-125">Параметры для добавления на основе индекса службы</span><span class="sxs-lookup"><span data-stu-id="903ba-125">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="903ba-126">_Примечание_. при выборе этого варианта будут добавлены только доверенные репозитории.</span><span class="sxs-lookup"><span data-stu-id="903ba-126">_Note_: This option will only add trusted repositories.</span></span> 

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="903ba-127">Указывает, следует ли разрешить сертификату доверенного пользователя связываться с корнем без доверия.</span><span class="sxs-lookup"><span data-stu-id="903ba-127">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="903ba-128">Разделенный точками с запятой список доверенных владельцев для дальнейшего ограничения доверия репозитория.</span><span class="sxs-lookup"><span data-stu-id="903ba-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span>

- **`-ServiceIndex`**

  <span data-ttu-id="903ba-129">Указывает индекс службы для доверенного репозитория версии 3.</span><span class="sxs-lookup"><span data-stu-id="903ba-129">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="903ba-130">Этот репозиторий должен поддерживать ресурс подписей репозитория.</span><span class="sxs-lookup"><span data-stu-id="903ba-130">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="903ba-131">Если этот параметр не указан, команда будет искать источник пакета с тем же `-Name` и получить индекс службы.</span><span class="sxs-lookup"><span data-stu-id="903ba-131">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span>

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="903ba-132">Параметры для добавления на основе сведений о сертификате</span><span class="sxs-lookup"><span data-stu-id="903ba-132">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="903ba-133">_Примечание_. Если доверенный подписывающий с данным именем уже существует, элемент сертификата будет добавлен в этот подписывающий.</span><span class="sxs-lookup"><span data-stu-id="903ba-133">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="903ba-134">В противном случае доверенный автор будет создан с помощью элемента сертификата из указанных сведений о сертификате.</span><span class="sxs-lookup"><span data-stu-id="903ba-134">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>


- **`-AllowUntrustedRoot`**

  <span data-ttu-id="903ba-135">Указывает, следует ли разрешить сертификату доверенного пользователя связываться с корнем без доверия.</span><span class="sxs-lookup"><span data-stu-id="903ba-135">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="903ba-136">Указывает отпечатки сертификата сертификата, для которого подписанные пакеты должны быть подписаны.</span><span class="sxs-lookup"><span data-stu-id="903ba-136">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="903ba-137">Отпечаток сертификата — это хэш сертификата.</span><span class="sxs-lookup"><span data-stu-id="903ba-137">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="903ba-138">Хэш-алгоритм, используемый для вычисления этого хэша, должен быть указан в `FingerprintAlgorithm` параметре.</span><span class="sxs-lookup"><span data-stu-id="903ba-138">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span>

- **`-FingerprintAlgorithm`**

  <span data-ttu-id="903ba-139">Указывает хэш-алгоритм, используемый для вычисления отпечатка сертификата.</span><span class="sxs-lookup"><span data-stu-id="903ba-139">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="903ba-140">По умолчанию — `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="903ba-140">Defaults to `SHA256`.</span></span> <span data-ttu-id="903ba-141">Поддерживаются значения `SHA256` , `SHA384` и `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="903ba-141">Values supported are `SHA256`, `SHA384` and `SHA512`.</span></span>

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="903ba-142">список доверенных-подписывающихй NuGet Remove-Name \<name\></span><span class="sxs-lookup"><span data-stu-id="903ba-142">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="903ba-143">Удаляет все доверенные подписывающих, соответствующие заданному имени.</span><span class="sxs-lookup"><span data-stu-id="903ba-143">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="903ba-144">Синхронизация доверенных подписывающихй NuGet-имя \<name\></span><span class="sxs-lookup"><span data-stu-id="903ba-144">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="903ba-145">Запрашивает последний список сертификатов, используемых в доверенном репозитории, чтобы обновить существующий список сертификатов в доверенном подписавшем.</span><span class="sxs-lookup"><span data-stu-id="903ba-145">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="903ba-146">_Примечание_. Этот жест удалит текущий список сертификатов и заменит их актуальным списком из репозитория.</span><span class="sxs-lookup"><span data-stu-id="903ba-146">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="903ba-147">Параметры</span><span class="sxs-lookup"><span data-stu-id="903ba-147">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="903ba-148">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="903ba-148">The NuGet configuration file to apply.</span></span> <span data-ttu-id="903ba-149">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="903ba-149">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="903ba-150">Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="903ba-150">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="903ba-151">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="903ba-151">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="903ba-152">Имя доверенного подписывающий.</span><span class="sxs-lookup"><span data-stu-id="903ba-152">Name of the trusted signer.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="903ba-153">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="903ba-153">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="903ba-154">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="903ba-154">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


## <a name="examples"></a><span data-ttu-id="903ba-155">Примеры</span><span class="sxs-lookup"><span data-stu-id="903ba-155">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget trusted-signers Remove -Name TrustedRepo

nuget trusted-signers Sync -Name TrustedRepo
```
