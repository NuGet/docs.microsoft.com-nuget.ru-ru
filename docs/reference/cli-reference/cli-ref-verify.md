---
title: Команда проверки интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe Verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327501"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="56f29-103">Команда verify (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="56f29-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="56f29-104">Область **применения:** &bullet; **Поддерживаемые версии** потребления пакетов: 4.6 +</span><span class="sxs-lookup"><span data-stu-id="56f29-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="56f29-105">Проверяет пакет.</span><span class="sxs-lookup"><span data-stu-id="56f29-105">Verifies a package.</span></span>

<span data-ttu-id="56f29-106">Проверка подписанных пакетов еще не поддерживается в .NET Core, на Mono или на платформах, отличных от Windows.</span><span class="sxs-lookup"><span data-stu-id="56f29-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="56f29-107">Использование</span><span class="sxs-lookup"><span data-stu-id="56f29-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="56f29-108">где `<package(s)>` — один или несколько `.nupkg` файлов.</span><span class="sxs-lookup"><span data-stu-id="56f29-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="56f29-109">Проверка NuGet — все</span><span class="sxs-lookup"><span data-stu-id="56f29-109">nuget verify -All</span></span>

<span data-ttu-id="56f29-110">Указывает, что все проверки можно выполнить для пакетов.</span><span class="sxs-lookup"><span data-stu-id="56f29-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="56f29-111">Проверка NuGet — подписи</span><span class="sxs-lookup"><span data-stu-id="56f29-111">nuget verify -Signatures</span></span>

<span data-ttu-id="56f29-112">Указывает, что необходимо выполнить проверку подписи пакета.</span><span class="sxs-lookup"><span data-stu-id="56f29-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="56f29-113">Параметры для «Verify-Signatures»</span><span class="sxs-lookup"><span data-stu-id="56f29-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="56f29-114">Параметр</span><span class="sxs-lookup"><span data-stu-id="56f29-114">Option</span></span> | <span data-ttu-id="56f29-115">Описание</span><span class="sxs-lookup"><span data-stu-id="56f29-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="56f29-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="56f29-116">CertificateFingerprint</span></span> | <span data-ttu-id="56f29-117">Указывает один или несколько отпечатков сертификатов SHA-256 сертификатов, которые подписанные пакеты должны быть подписаны.</span><span class="sxs-lookup"><span data-stu-id="56f29-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="56f29-118">Отпечаток сертификата SHA-256 — это хэш сертификата SHA-256.</span><span class="sxs-lookup"><span data-stu-id="56f29-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="56f29-119">Несколько входов должны быть разделены точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="56f29-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="56f29-120">Параметры</span><span class="sxs-lookup"><span data-stu-id="56f29-120">Options</span></span>

| <span data-ttu-id="56f29-121">Параметр</span><span class="sxs-lookup"><span data-stu-id="56f29-121">Option</span></span> | <span data-ttu-id="56f29-122">Описание</span><span class="sxs-lookup"><span data-stu-id="56f29-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="56f29-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="56f29-123">ConfigFile</span></span> | <span data-ttu-id="56f29-124">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="56f29-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="56f29-125">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="56f29-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="56f29-126">форцеенглишаутпут</span><span class="sxs-lookup"><span data-stu-id="56f29-126">ForceEnglishOutput</span></span> | <span data-ttu-id="56f29-127">Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="56f29-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="56f29-128">Help</span><span class="sxs-lookup"><span data-stu-id="56f29-128">Help</span></span> | <span data-ttu-id="56f29-129">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="56f29-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="56f29-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="56f29-130">Verbosity</span></span> | <span data-ttu-id="56f29-131">Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*.</span><span class="sxs-lookup"><span data-stu-id="56f29-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="56f29-132">Примеры</span><span class="sxs-lookup"><span data-stu-id="56f29-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```