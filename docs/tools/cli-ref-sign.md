---
title: Команда входа NuGet CLI
description: Ссылку для входа команду nuget.exe
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7e84d794b802cfd69c785f720280fd5c022a46f6
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="a16ad-103">Команда sign (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a16ad-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="a16ad-104">**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="a16ad-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="a16ad-105">Подписывает все пакеты, соответствующие первого аргумента, с помощью сертификата.</span><span class="sxs-lookup"><span data-stu-id="a16ad-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="a16ad-106">Можно получить сертификат с закрытым ключом, из файла или сертификат, установленный в хранилище сертификатов, указав имя субъекта или отпечатка.</span><span class="sxs-lookup"><span data-stu-id="a16ad-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

<span data-ttu-id="a16ad-107">Подписание пакета еще не поддерживается в .NET Core в Mono, так и на платформах, отличных от Windows.</span><span class="sxs-lookup"><span data-stu-id="a16ad-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="a16ad-108">Использование</span><span class="sxs-lookup"><span data-stu-id="a16ad-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="a16ad-109">где `<package(s)>` одной или нескольких `.nupkg` файлов.</span><span class="sxs-lookup"><span data-stu-id="a16ad-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="a16ad-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="a16ad-110">Options</span></span>

| <span data-ttu-id="a16ad-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="a16ad-111">Option</span></span> | <span data-ttu-id="a16ad-112">Описание</span><span class="sxs-lookup"><span data-stu-id="a16ad-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a16ad-113">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="a16ad-113">CertificateFingerprint</span></span> | <span data-ttu-id="a16ad-114">Указывает отпечаток сертификата, используемого для поиска в локальном хранилище сертификатов для сертификата SHA-1.</span><span class="sxs-lookup"><span data-stu-id="a16ad-114">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span> |
| <span data-ttu-id="a16ad-115">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="a16ad-115">CertificatePassword</span></span> | <span data-ttu-id="a16ad-116">Указывает пароль для сертификата, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="a16ad-116">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="a16ad-117">Если сертификат защищен паролем, но пароль не указан, команда предложит ввести пароль во время выполнения, если передается неинтерактивных параметр.</span><span class="sxs-lookup"><span data-stu-id="a16ad-117">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the -NonInteractive option is passed.</span></span> |
| <span data-ttu-id="a16ad-118">CertificatePath</span><span class="sxs-lookup"><span data-stu-id="a16ad-118">CertificatePath</span></span> | <span data-ttu-id="a16ad-119">Указывает путь к файлу, чтобы сертификат, используемый для подписи пакета.</span><span class="sxs-lookup"><span data-stu-id="a16ad-119">Specifies the file path to the certificate to be used in signing the package.</span></span> |
| <span data-ttu-id="a16ad-120">CertificateStoreLocation</span><span class="sxs-lookup"><span data-stu-id="a16ad-120">CertificateStoreLocation</span></span> | <span data-ttu-id="a16ad-121">Задает имя хранилища сертификатов X.509, используемый для поиска сертификата.</span><span class="sxs-lookup"><span data-stu-id="a16ad-121">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="a16ad-122">По умолчанию используется «CurrentUser», хранилища сертификатов X.509, используемый текущим пользователем.</span><span class="sxs-lookup"><span data-stu-id="a16ad-122">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="a16ad-123">Этот параметр следует использовать при указании сертификата - CertificateSubjectName или - CertificateFingerprint параметры.</span><span class="sxs-lookup"><span data-stu-id="a16ad-123">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="a16ad-124">CertificateStoreName</span><span class="sxs-lookup"><span data-stu-id="a16ad-124">CertificateStoreName</span></span> | <span data-ttu-id="a16ad-125">Задает имя хранилища сертификатов X.509 для поиска сертификата.</span><span class="sxs-lookup"><span data-stu-id="a16ad-125">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="a16ad-126">Значение по умолчанию «My», хранилище сертификатов X.509 для личных сертификатов.</span><span class="sxs-lookup"><span data-stu-id="a16ad-126">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="a16ad-127">Этот параметр следует использовать при указании сертификата - CertificateSubjectName или - CertificateFingerprint параметры.</span><span class="sxs-lookup"><span data-stu-id="a16ad-127">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="a16ad-128">CertificateSubjectName</span><span class="sxs-lookup"><span data-stu-id="a16ad-128">CertificateSubjectName</span></span> | <span data-ttu-id="a16ad-129">Задает имя субъекта сертификата, используемого для поиска в локальном хранилище сертификатов для сертификата.</span><span class="sxs-lookup"><span data-stu-id="a16ad-129">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="a16ad-130">Поиск является сравнение строк без учета регистра, используя указанное значение, которое будет найти все сертификаты с именем субъекта, содержащему эту строку, независимо от того, другие значения субъекта.</span><span class="sxs-lookup"><span data-stu-id="a16ad-130">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="a16ad-131">С параметрами - CertificateStoreName и - CertificateStoreLocation можно указать в хранилище сертификатов.</span><span class="sxs-lookup"><span data-stu-id="a16ad-131">The certificate store can be specified by -CertificateStoreName and -CertificateStoreLocation options.</span></span> |
| <span data-ttu-id="a16ad-132">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a16ad-132">ConfigFile</span></span> | <span data-ttu-id="a16ad-133">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="a16ad-133">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a16ad-134">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="a16ad-134">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a16ad-135">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a16ad-135">ForceEnglishOutput</span></span> | <span data-ttu-id="a16ad-136">Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="a16ad-136">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a16ad-137">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="a16ad-137">HashAlgorithm</span></span> | <span data-ttu-id="a16ad-138">Хэш-алгоритм, используемый для подписывания пакета.</span><span class="sxs-lookup"><span data-stu-id="a16ad-138">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="a16ad-139">По умолчанию — SHA256.</span><span class="sxs-lookup"><span data-stu-id="a16ad-139">Defaults to SHA256.</span></span> |
| <span data-ttu-id="a16ad-140">Справка</span><span class="sxs-lookup"><span data-stu-id="a16ad-140">Help</span></span> | <span data-ttu-id="a16ad-141">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="a16ad-141">Displays help information for the command.</span></span> |
| <span data-ttu-id="a16ad-142">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="a16ad-142">NonInteractive</span></span> | <span data-ttu-id="a16ad-143">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="a16ad-143">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a16ad-144">Выходной каталог</span><span class="sxs-lookup"><span data-stu-id="a16ad-144">OutputDirectory</span></span> | <span data-ttu-id="a16ad-145">Указывает каталог, где следует сохранить подписанных пакетов.</span><span class="sxs-lookup"><span data-stu-id="a16ad-145">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="a16ad-146">По умолчанию исходный пакет, перезаписывается подписанных пакетов.</span><span class="sxs-lookup"><span data-stu-id="a16ad-146">By default the original package is overwritten by the signed package.</span></span> |
| <span data-ttu-id="a16ad-147">Перезаписать</span><span class="sxs-lookup"><span data-stu-id="a16ad-147">Overwrite</span></span> | <span data-ttu-id="a16ad-148">Переключатель, чтобы указать, должны ли перезаписываться подписи текущего.</span><span class="sxs-lookup"><span data-stu-id="a16ad-148">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="a16ad-149">По умолчанию команда завершится ошибкой, если пакет уже имеет подпись.</span><span class="sxs-lookup"><span data-stu-id="a16ad-149">By default the command will fail if the package already has a signature.</span></span> |
| <span data-ttu-id="a16ad-150">Timestamper</span><span class="sxs-lookup"><span data-stu-id="a16ad-150">Timestamper</span></span> | <span data-ttu-id="a16ad-151">URL-адрес сервера метки времени RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="a16ad-151">URL to an RFC 3161 timestamping server.</span></span> |
| <span data-ttu-id="a16ad-152">TimestampHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="a16ad-152">TimestampHashAlgorithm</span></span> | <span data-ttu-id="a16ad-153">Хэш-алгоритм, используемый сервером отметок времени RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="a16ad-153">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="a16ad-154">По умолчанию — SHA256.</span><span class="sxs-lookup"><span data-stu-id="a16ad-154">Defaults to SHA256.</span></span> |
| <span data-ttu-id="a16ad-155">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="a16ad-155">Verbosity</span></span> | <span data-ttu-id="a16ad-156">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="a16ad-156">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="a16ad-157">Примеры</span><span class="sxs-lookup"><span data-stu-id="a16ad-157">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```