---
title: Интерфейс командной строки NuGet проверьте команду
description: Справочник по nuget.exe проверьте команду
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545217"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="f11e6-103">Команда verify (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f11e6-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="f11e6-104">**Применяется к:** упаковать потребления &bullet; **поддерживаемые версии:** 4.6 или более поздней</span><span class="sxs-lookup"><span data-stu-id="f11e6-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="f11e6-105">Проверяет ли пакет.</span><span class="sxs-lookup"><span data-stu-id="f11e6-105">Verifies a package.</span></span>

<span data-ttu-id="f11e6-106">Проверка подписанных пакетов еще не поддерживается в .NET Core, в рамках проекта Mono или на платформах, отличных от Windows.</span><span class="sxs-lookup"><span data-stu-id="f11e6-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="f11e6-107">Использование</span><span class="sxs-lookup"><span data-stu-id="f11e6-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="f11e6-108">где `<package(s)>` — это один или несколько `.nupkg` файлов.</span><span class="sxs-lookup"><span data-stu-id="f11e6-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="f11e6-109">проверить NuGet — все</span><span class="sxs-lookup"><span data-stu-id="f11e6-109">nuget verify -All</span></span>

<span data-ttu-id="f11e6-110">Указывает, что все возможные проверки, необходимые должна выполняться на пакеты.</span><span class="sxs-lookup"><span data-stu-id="f11e6-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="f11e6-111">NuGet проверки - сигнатур</span><span class="sxs-lookup"><span data-stu-id="f11e6-111">nuget verify -Signatures</span></span>

<span data-ttu-id="f11e6-112">Указывает, что должна быть выполнена проверка подписи пакета.</span><span class="sxs-lookup"><span data-stu-id="f11e6-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="f11e6-113">Параметры для «verify - подписей»</span><span class="sxs-lookup"><span data-stu-id="f11e6-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="f11e6-114">Параметр</span><span class="sxs-lookup"><span data-stu-id="f11e6-114">Option</span></span> | <span data-ttu-id="f11e6-115">Описание</span><span class="sxs-lookup"><span data-stu-id="f11e6-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f11e6-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="f11e6-116">CertificateFingerprint</span></span> | <span data-ttu-id="f11e6-117">Указывает один или несколько отпечатков сертификата SHA-256, какие подписанные пакеты должны быть подписаны с помощью сертификатов (s).</span><span class="sxs-lookup"><span data-stu-id="f11e6-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="f11e6-118">Отпечаток сертификата SHA-256 — это хэш SHA-256 сертификата.</span><span class="sxs-lookup"><span data-stu-id="f11e6-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="f11e6-119">Несколько наборов входных данных должно быть разделенных точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="f11e6-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="f11e6-120">Параметры</span><span class="sxs-lookup"><span data-stu-id="f11e6-120">Options</span></span>

| <span data-ttu-id="f11e6-121">Параметр</span><span class="sxs-lookup"><span data-stu-id="f11e6-121">Option</span></span> | <span data-ttu-id="f11e6-122">Описание</span><span class="sxs-lookup"><span data-stu-id="f11e6-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f11e6-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f11e6-123">ConfigFile</span></span> | <span data-ttu-id="f11e6-124">Чтобы применить файл конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="f11e6-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f11e6-125">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="f11e6-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f11e6-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f11e6-126">ForceEnglishOutput</span></span> | <span data-ttu-id="f11e6-127">Nuget.exe силы для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры.</span><span class="sxs-lookup"><span data-stu-id="f11e6-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f11e6-128">Справка</span><span class="sxs-lookup"><span data-stu-id="f11e6-128">Help</span></span> | <span data-ttu-id="f11e6-129">Отображает справку для команды.</span><span class="sxs-lookup"><span data-stu-id="f11e6-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="f11e6-130">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="f11e6-130">Verbosity</span></span> | <span data-ttu-id="f11e6-131">Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="f11e6-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="f11e6-132">Примеры</span><span class="sxs-lookup"><span data-stu-id="f11e6-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```