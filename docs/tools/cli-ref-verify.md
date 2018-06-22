---
title: Команда проверьте NuGet CLI
description: Справочник по nuget.exe проверьте команды
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c80334104f7d8b2ccbf16ea2c11dc37b39408eeb
ms.sourcegitcommit: c8485dc61469511485367d2067b97d6f74b49f6e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2018
ms.locfileid: "34462856"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="aed16-103">Команда verify (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="aed16-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="aed16-104">**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="aed16-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="aed16-105">Проверка пакета.</span><span class="sxs-lookup"><span data-stu-id="aed16-105">Verifies a package.</span></span>

<span data-ttu-id="aed16-106">Проверка подписанных пакетов еще не поддерживается в .NET Core в Mono, так и на платформах, отличных от Windows.</span><span class="sxs-lookup"><span data-stu-id="aed16-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="aed16-107">Использование</span><span class="sxs-lookup"><span data-stu-id="aed16-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="aed16-108">где `<package(s)>` одной или нескольких `.nupkg` файлов.</span><span class="sxs-lookup"><span data-stu-id="aed16-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="aed16-109">-Все проверки NuGet</span><span class="sxs-lookup"><span data-stu-id="aed16-109">nuget verify -All</span></span>

<span data-ttu-id="aed16-110">Указывает, что все проверки на возможные должна быть выполнена на пакетов.</span><span class="sxs-lookup"><span data-stu-id="aed16-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="aed16-111">Проверка NuGet - подписей</span><span class="sxs-lookup"><span data-stu-id="aed16-111">nuget verify -Signatures</span></span>

<span data-ttu-id="aed16-112">Указывает, что должна быть выполнена проверка подписи пакета.</span><span class="sxs-lookup"><span data-stu-id="aed16-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="aed16-113">Параметры «проверить - подписи»</span><span class="sxs-lookup"><span data-stu-id="aed16-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="aed16-114">Параметр</span><span class="sxs-lookup"><span data-stu-id="aed16-114">Option</span></span> | <span data-ttu-id="aed16-115">Описание</span><span class="sxs-lookup"><span data-stu-id="aed16-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aed16-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="aed16-116">CertificateFingerprint</span></span> | <span data-ttu-id="aed16-117">Указывает один или несколько отпечатки сертификата SHA-256, какие знаком должен быть подписан с помощью сертификатов (s).</span><span class="sxs-lookup"><span data-stu-id="aed16-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="aed16-118">Отпечаток сертификата SHA-256 является хэш сертификата SHA-256.</span><span class="sxs-lookup"><span data-stu-id="aed16-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="aed16-119">Несколько входов должно быть разделенных точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="aed16-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="aed16-120">Параметры</span><span class="sxs-lookup"><span data-stu-id="aed16-120">Options</span></span>

| <span data-ttu-id="aed16-121">Параметр</span><span class="sxs-lookup"><span data-stu-id="aed16-121">Option</span></span> | <span data-ttu-id="aed16-122">Описание</span><span class="sxs-lookup"><span data-stu-id="aed16-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aed16-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="aed16-123">ConfigFile</span></span> | <span data-ttu-id="aed16-124">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="aed16-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="aed16-125">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="aed16-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="aed16-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="aed16-126">ForceEnglishOutput</span></span> | <span data-ttu-id="aed16-127">Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="aed16-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="aed16-128">Справка</span><span class="sxs-lookup"><span data-stu-id="aed16-128">Help</span></span> | <span data-ttu-id="aed16-129">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="aed16-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="aed16-130">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="aed16-130">Verbosity</span></span> | <span data-ttu-id="aed16-131">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="aed16-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="aed16-132">Примеры</span><span class="sxs-lookup"><span data-stu-id="aed16-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```