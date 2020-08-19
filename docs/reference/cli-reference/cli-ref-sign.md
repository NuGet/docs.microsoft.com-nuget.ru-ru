---
title: Команда Sign интерфейса командной строки NuGet
description: Справочник по команде nuget.exe Sign
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622776"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="3c4fd-103">Команда Sign (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="3c4fd-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="3c4fd-104">Область **применения:** &bullet; **Поддерживаемые версии** для создания пакетов: 4.6 +</span><span class="sxs-lookup"><span data-stu-id="3c4fd-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="3c4fd-105">Подписывает все пакеты, соответствующие первому аргументу, с помощью сертификата.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="3c4fd-106">Сертификат с закрытым ключом можно получить из файла или из сертификата, установленного в хранилище сертификатов, указав имя субъекта или отпечаток.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

> [!Note]
> <span data-ttu-id="3c4fd-107">Подписывание пакетов пока не поддерживается в .NET Core, в Mono или на платформах, отличных от Windows.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="3c4fd-108">Использование</span><span class="sxs-lookup"><span data-stu-id="3c4fd-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="3c4fd-109">где `<package(s)>` — один или несколько `.nupkg` файлов.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="3c4fd-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="3c4fd-110">Options</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="3c4fd-111">Указывает отпечаток SHA-1 сертификата, используемого для поиска сертификата в локальном хранилище сертификатов.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-111">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span>

- **`-CertificatePassword`**

  <span data-ttu-id="3c4fd-112">Указывает пароль сертификата (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="3c4fd-112">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="3c4fd-113">Если сертификат защищен паролем, но пароль не указан, команда запрашивает пароль во время выполнения, если не `-NonInteractive` передается параметр.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-113">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the `-NonInteractive` option is passed.</span></span>

- **`-CertificatePath`**

  <span data-ttu-id="3c4fd-114">Указывает путь к файлу сертификата, который будет использоваться при подписывании пакета.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-114">Specifies the file path to the certificate to be used in signing the package.</span></span>

- **`-CertificateStoreLocation`**

  <span data-ttu-id="3c4fd-115">Указывает имя хранилища сертификатов X. 509, используемое для поиска сертификата.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-115">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="3c4fd-116">По умолчанию используется значение CurrentUser, хранилище сертификатов X. 509, используемое текущим пользователем.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-116">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="3c4fd-117">Этот параметр следует использовать при указании сертификата с помощью `-CertificateSubjectName` `-CertificateFingerprint` параметров или.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-117">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateStoreName`**

  <span data-ttu-id="3c4fd-118">Указывает имя хранилища сертификатов X. 509, которое будет использоваться для поиска сертификата.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-118">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="3c4fd-119">По умолчанию используется хранилище сертификатов X. 509 для личных сертификатов.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-119">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="3c4fd-120">Этот параметр следует использовать при указании сертификата с помощью `-CertificateSubjectName` `-CertificateFingerprint` параметров или.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-120">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateSubjectName`**

  <span data-ttu-id="3c4fd-121">Указывает имя субъекта сертификата, используемого для поиска сертификата в локальном хранилище сертификатов.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-121">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="3c4fd-122">При поиске выполняется сравнение строк без учета регистра с использованием заданного значения, где будут найдены все сертификаты с именем субъекта, содержащими эту строку, независимо от других значений субъекта.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-122">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="3c4fd-123">Хранилище сертификатов можно указать с помощью `-CertificateStoreName` параметров и `-CertificateStoreLocation` .</span><span class="sxs-lookup"><span data-stu-id="3c4fd-123">The certificate store can be specified by `-CertificateStoreName` and `-CertificateStoreLocation` options.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="3c4fd-124">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3c4fd-125">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="3c4fd-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="3c4fd-126">Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-126">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-HashAlgorithm`**

  <span data-ttu-id="3c4fd-127">Хэш-алгоритм, используемый для подписания пакета.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-127">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="3c4fd-128">По умолчанию используется SHA256.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-128">Defaults to SHA256.</span></span> <span data-ttu-id="3c4fd-129">Возможные значения: SHA256, SHA384 и SHA512.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-129">Possible values are SHA256, SHA384, and SHA512.</span></span>

- **`-?|-help`**

  <span data-ttu-id="3c4fd-130">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-130">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="3c4fd-131">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-131">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="3c4fd-132">Указывает каталог, в котором должен быть сохранен подписанный пакет.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-132">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="3c4fd-133">По умолчанию исходный пакет перезаписывается подписанным пакетом.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-133">By default the original package is overwritten by the signed package.</span></span>

- **`-Overwrite`**

  <span data-ttu-id="3c4fd-134">Параметр, указывающий, следует ли перезаписывать текущую сигнатуру.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-134">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="3c4fd-135">По умолчанию команда завершится ошибкой, если у пакета уже есть сигнатура.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-135">By default the command will fail if the package already has a signature.</span></span>

- **`-Timestamper`**

  <span data-ttu-id="3c4fd-136">URL-адрес сервера отметок времени RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-136">URL to an RFC 3161 timestamping server.</span></span>

- **`-TimestampHashAlgorithm`**

  <span data-ttu-id="3c4fd-137">Хэш-алгоритм, используемый сервером меток RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-137">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="3c4fd-138">По умолчанию используется SHA256.</span><span class="sxs-lookup"><span data-stu-id="3c4fd-138">Defaults to SHA256.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="3c4fd-139">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="3c4fd-139">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="3c4fd-140">Примеры</span><span class="sxs-lookup"><span data-stu-id="3c4fd-140">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
