---
title: Команда проверьте NuGet CLI
description: Справочник по nuget.exe проверьте команды
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c2c31b71358bc50a1fb9aab8905c279cd1235b07
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="7aec3-103">Команда verify (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7aec3-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="7aec3-104">**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="7aec3-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="7aec3-105">Проверка пакета.</span><span class="sxs-lookup"><span data-stu-id="7aec3-105">Verifies a package.</span></span>

<span data-ttu-id="7aec3-106">Проверка подписанных пакетов еще не поддерживается в .NET Core в Mono, так и на платформах, отличных от Windows.</span><span class="sxs-lookup"><span data-stu-id="7aec3-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="7aec3-107">Использование</span><span class="sxs-lookup"><span data-stu-id="7aec3-107">Usage</span></span>

```cli
nuget verify <package(s)> [options]
```

<span data-ttu-id="7aec3-108">где `<package(s)>` одной или нескольких `.nupkg` файлов.</span><span class="sxs-lookup"><span data-stu-id="7aec3-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="7aec3-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="7aec3-109">Options</span></span>

| <span data-ttu-id="7aec3-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="7aec3-110">Option</span></span> | <span data-ttu-id="7aec3-111">Описание</span><span class="sxs-lookup"><span data-stu-id="7aec3-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7aec3-112">Все</span><span class="sxs-lookup"><span data-stu-id="7aec3-112">All</span></span> | <span data-ttu-id="7aec3-113">Указывает, что все проверки на возможные должна быть выполнена на пакетов.</span><span class="sxs-lookup"><span data-stu-id="7aec3-113">Specifies that all verifications possible should be performed on the package(s).</span></span> |
| <span data-ttu-id="7aec3-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="7aec3-114">CertificateFingerprint</span></span> | <span data-ttu-id="7aec3-115">Указывает один или несколько отпечатки сертификата SHA-256, какие знаком должен быть подписан с помощью сертификатов (s).</span><span class="sxs-lookup"><span data-stu-id="7aec3-115">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="7aec3-116">Отпечаток сертификата SHA-256 является хэш сертификата SHA-256.</span><span class="sxs-lookup"><span data-stu-id="7aec3-116">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="7aec3-117">Несколько входов должно быть разделенных точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="7aec3-117">Multiple inputs should be semicolon separated.</span></span> |
| <span data-ttu-id="7aec3-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7aec3-118">ConfigFile</span></span> | <span data-ttu-id="7aec3-119">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="7aec3-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7aec3-120">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="7aec3-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7aec3-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7aec3-121">ForceEnglishOutput</span></span> | <span data-ttu-id="7aec3-122">Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="7aec3-122">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7aec3-123">Справка</span><span class="sxs-lookup"><span data-stu-id="7aec3-123">Help</span></span> | <span data-ttu-id="7aec3-124">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="7aec3-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="7aec3-125">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="7aec3-125">NonInteractive</span></span> | <span data-ttu-id="7aec3-126">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="7aec3-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7aec3-127">Сигнатуры</span><span class="sxs-lookup"><span data-stu-id="7aec3-127">Signatures</span></span> | <span data-ttu-id="7aec3-128">Указывает, что должна быть выполнена проверка подписи пакета.</span><span class="sxs-lookup"><span data-stu-id="7aec3-128">Specifies that package signature verification should be performed.</span></span> |
| <span data-ttu-id="7aec3-129">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="7aec3-129">Verbosity</span></span> | <span data-ttu-id="7aec3-130">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="7aec3-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="7aec3-131">Примеры</span><span class="sxs-lookup"><span data-stu-id="7aec3-131">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```