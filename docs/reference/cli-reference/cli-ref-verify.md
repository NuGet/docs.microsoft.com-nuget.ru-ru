---
title: Команда проверки интерфейса командной строки NuGet
description: Справочник по команде nuget.exe Verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7ce08f11195437e94bfe69883ff525e9ad3a73f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238144"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="d449a-103">Команда "проверить" (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="d449a-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="d449a-104">Область **применения:** &bullet; **Поддерживаемые версии** для использования пакетов: 4.6 +</span><span class="sxs-lookup"><span data-stu-id="d449a-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="d449a-105">Проверяет пакет.</span><span class="sxs-lookup"><span data-stu-id="d449a-105">Verifies a package.</span></span>

<span data-ttu-id="d449a-106">Проверка подписанных пакетов пока не поддерживается в Mono.</span><span class="sxs-lookup"><span data-stu-id="d449a-106">Verification of signed packages is not yet supported under Mono.</span></span>

## <a name="usage"></a><span data-ttu-id="d449a-107">Использование</span><span class="sxs-lookup"><span data-stu-id="d449a-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="d449a-108">где `<package(s)>` — один или несколько `.nupkg` файлов.</span><span class="sxs-lookup"><span data-stu-id="d449a-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="d449a-109">Проверка NuGet — все</span><span class="sxs-lookup"><span data-stu-id="d449a-109">nuget verify -All</span></span>

<span data-ttu-id="d449a-110">Указывает, что для пакетов нужно выполнить все возможные проверки.</span><span class="sxs-lookup"><span data-stu-id="d449a-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="d449a-111">Проверка NuGet — подписи</span><span class="sxs-lookup"><span data-stu-id="d449a-111">nuget verify -Signatures</span></span>

<span data-ttu-id="d449a-112">Указывает, что необходимо выполнить проверку подписи пакета.</span><span class="sxs-lookup"><span data-stu-id="d449a-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="d449a-113">Параметры для «Verify-Signatures»</span><span class="sxs-lookup"><span data-stu-id="d449a-113">Options for "verify -Signatures"</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="d449a-114">Указывает один или несколько отпечатков сертификатов SHA-256 сертификатов, которые подписанные пакеты должны быть подписаны.</span><span class="sxs-lookup"><span data-stu-id="d449a-114">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="d449a-115">Отпечаток сертификата SHA-256 — это хэш сертификата SHA-256.</span><span class="sxs-lookup"><span data-stu-id="d449a-115">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="d449a-116">Несколько входов должны быть разделены точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="d449a-116">Multiple inputs should be semicolon separated.</span></span>

## <a name="options"></a><span data-ttu-id="d449a-117">Параметры</span><span class="sxs-lookup"><span data-stu-id="d449a-117">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="d449a-118">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="d449a-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d449a-119">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="d449a-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="d449a-120">Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="d449a-120">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="d449a-121">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="d449a-121">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="d449a-122">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="d449a-122">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="d449a-123">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="d449a-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="d449a-124">Примеры</span><span class="sxs-lookup"><span data-stu-id="d449a-124">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```