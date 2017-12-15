---
title: "Команду NuGet CLI зеркальной | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 190d7010-172e-44b8-8a32-94a2a63be4f3
description: "Справочник по команда зеркало nuget.exe"
keywords: "Справочник по зеркальной NuGet, зеркальный команды"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67daa1aa278b42b7974c562ba4097a525e7bb105
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="9935c-104">Команда зеркальной (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9935c-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="9935c-105">**Применяется к:** пакета публикации &bullet; **поддерживаемые версии:** устаревшими в версии 3.2 +</span><span class="sxs-lookup"><span data-stu-id="9935c-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="9935c-106">Отражает пакет и его зависимости от репозиториев указанного источника в целевой репозиторий.</span><span class="sxs-lookup"><span data-stu-id="9935c-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="9935c-107">Чтобы включить эту команду для NuGet версии до версии 3.2, обратитесь к [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)выберите последнюю стабильный выпуск, загрузите `NuGet.ServerExtensions.dll` и `Nuget-Signed.exe` на локальный диск и переименования `Nuget-Signed.exe` для `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="9935c-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="9935c-108">Использование</span><span class="sxs-lookup"><span data-stu-id="9935c-108">Usage</span></span>

```
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="9935c-109">где `<packageID>` является пакет, чтобы создать зеркало, или `<configFilePath>` идентифицирует `packages.config` файл, который содержит список пакетов, подлежащих зеркальному отображению.</span><span class="sxs-lookup"><span data-stu-id="9935c-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="9935c-110">`<listUrlTarget>` Указывает исходный репозиторий и `<publishUrlTarget>` указывает целевой репозиторий.</span><span class="sxs-lookup"><span data-stu-id="9935c-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="9935c-111">Если включено репозиторий целевой `https://machine/repo` , на котором выполняется [NuGet.Server](../hosting-packages/NuGet-Server.md), URL-адреса со списком и push будут `https://machine/repo/nuget` и `https://machine/repo/api/v2/package`соответственно.</span><span class="sxs-lookup"><span data-stu-id="9935c-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/NuGet-Server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="9935c-112">Параметры</span><span class="sxs-lookup"><span data-stu-id="9935c-112">Options</span></span>

| <span data-ttu-id="9935c-113">Параметр</span><span class="sxs-lookup"><span data-stu-id="9935c-113">Option</span></span> | <span data-ttu-id="9935c-114">Описание</span><span class="sxs-lookup"><span data-stu-id="9935c-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9935c-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="9935c-115">ApiKey</span></span> | <span data-ttu-id="9935c-116">Ключ API для целевой репозиторий.</span><span class="sxs-lookup"><span data-stu-id="9935c-116">The API key for the target repository.</span></span> <span data-ttu-id="9935c-117">Если не существует, указанная в *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="9935c-117">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="9935c-118">Справка</span><span class="sxs-lookup"><span data-stu-id="9935c-118">Help</span></span> | <span data-ttu-id="9935c-119">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="9935c-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="9935c-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="9935c-120">NoCache</span></span> | <span data-ttu-id="9935c-121">Запрещает NuGet с помощью пакетов из кэшей локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="9935c-121">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="9935c-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="9935c-122">Noop</span></span> | <span data-ttu-id="9935c-123">Регистрирует, что выполняются, но не выполняет действий; предполагается успеха для принудительной операций.</span><span class="sxs-lookup"><span data-stu-id="9935c-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="9935c-124">Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="9935c-124">PreRelease</span></span> | <span data-ttu-id="9935c-125">Включает предварительные версии пакетов в процессе зеркального отображения.</span><span class="sxs-lookup"><span data-stu-id="9935c-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="9935c-126">Исходный код</span><span class="sxs-lookup"><span data-stu-id="9935c-126">Source</span></span> | <span data-ttu-id="9935c-127">Список источников пакетов, подлежащих зеркальному отображению.</span><span class="sxs-lookup"><span data-stu-id="9935c-127">A list of package sources to mirror.</span></span> <span data-ttu-id="9935c-128">Если не заданы ни один из источников, тех, которые определены в *%AppData%\NuGet\NuGet.Config* используются, по умолчанию принимается nuget.org Если ничего не указано.</span><span class="sxs-lookup"><span data-stu-id="9935c-128">If no sources are specified, the ones defined in *%AppData%\NuGet\NuGet.Config* are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="9935c-129">Время ожидания</span><span class="sxs-lookup"><span data-stu-id="9935c-129">Timeout</span></span> | <span data-ttu-id="9935c-130">Указывает время ожидания в секундах для принудительной отправки на сервер.</span><span class="sxs-lookup"><span data-stu-id="9935c-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="9935c-131">Значение по умолчанию — 300 секунд (5 минут).</span><span class="sxs-lookup"><span data-stu-id="9935c-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="9935c-132">Версия</span><span class="sxs-lookup"><span data-stu-id="9935c-132">Version</span></span> | <span data-ttu-id="9935c-133">Версия пакета для установки.</span><span class="sxs-lookup"><span data-stu-id="9935c-133">The version of the package to install.</span></span> <span data-ttu-id="9935c-134">Если не указан, последняя версия является зеркальным.</span><span class="sxs-lookup"><span data-stu-id="9935c-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="9935c-135">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9935c-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9935c-136">Примеры</span><span class="sxs-lookup"><span data-stu-id="9935c-136">Examples</span></span>

```
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
