---
title: "NuGet CLI проверьте команду | Документы Microsoft"
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Справочник по nuget.exe проверьте команды"
keywords: "NuGet проверить ссылку, проверьте команды"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 096c79670267d9b602dd6ad30640e832441c31c5
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="2d66a-104">Проверьте команду (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2d66a-104">verify command (NuGet CLI)</span></span>

<span data-ttu-id="2d66a-105">**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="2d66a-105">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="2d66a-106">Проверка пакета.</span><span class="sxs-lookup"><span data-stu-id="2d66a-106">Verifies a package.</span></span>

## <a name="usage"></a><span data-ttu-id="2d66a-107">Использование</span><span class="sxs-lookup"><span data-stu-id="2d66a-107">Usage</span></span>

```cli
nuget verify <package(s)> [options]
```

<span data-ttu-id="2d66a-108">где `<package(s)>` одной или нескольких `.nupkg` файлов.</span><span class="sxs-lookup"><span data-stu-id="2d66a-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="2d66a-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="2d66a-109">Options</span></span>

| <span data-ttu-id="2d66a-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="2d66a-110">Option</span></span> | <span data-ttu-id="2d66a-111">Описание:</span><span class="sxs-lookup"><span data-stu-id="2d66a-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2d66a-112">Все</span><span class="sxs-lookup"><span data-stu-id="2d66a-112">All</span></span> | <span data-ttu-id="2d66a-113">Указывает, что все проверки на возможные должна быть выполнена на пакетов.</span><span class="sxs-lookup"><span data-stu-id="2d66a-113">Specifies that all verifications possible should be performed on the package(s).</span></span> |
| <span data-ttu-id="2d66a-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="2d66a-114">CertificateFingerprint</span></span> | <span data-ttu-id="2d66a-115">Указывает один или несколько отпечатки сертификата SHA-256, какие знаком должен быть подписан с помощью сертификатов (s).</span><span class="sxs-lookup"><span data-stu-id="2d66a-115">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="2d66a-116">Отпечаток сертификата SHA-256 является хэш сертификата SHA-256.</span><span class="sxs-lookup"><span data-stu-id="2d66a-116">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="2d66a-117">Несколько входов должно быть разделенных точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="2d66a-117">Multiple inputs should be semicolon separated.</span></span> |
| <span data-ttu-id="2d66a-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2d66a-118">ConfigFile</span></span> | <span data-ttu-id="2d66a-119">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="2d66a-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2d66a-120">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="2d66a-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2d66a-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2d66a-121">ForceEnglishOutput</span></span> | <span data-ttu-id="2d66a-122">Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="2d66a-122">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2d66a-123">Справка</span><span class="sxs-lookup"><span data-stu-id="2d66a-123">Help</span></span> | <span data-ttu-id="2d66a-124">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="2d66a-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="2d66a-125">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="2d66a-125">NonInteractive</span></span> | <span data-ttu-id="2d66a-126">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="2d66a-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2d66a-127">Сигнатуры</span><span class="sxs-lookup"><span data-stu-id="2d66a-127">Signatures</span></span> | <span data-ttu-id="2d66a-128">Указывает, что должна быть выполнена проверка подписи пакета.</span><span class="sxs-lookup"><span data-stu-id="2d66a-128">Specifies that package signature verification should be performed.</span></span> |
| <span data-ttu-id="2d66a-129">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="2d66a-129">Verbosity</span></span> | <span data-ttu-id="2d66a-130">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="2d66a-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="2d66a-131">Примеры</span><span class="sxs-lookup"><span data-stu-id="2d66a-131">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```