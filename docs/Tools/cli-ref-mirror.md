---
title: "Команду NuGet CLI зеркальной | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Справочник по команда зеркало nuget.exe"
keywords: "Справочник по зеркальной NuGet, зеркальный команды"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0c1969cc04b2e2cead5e9dadf9739fdabdf65f6c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="0cc8d-104">Команда зеркальной (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="0cc8d-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="0cc8d-105">**Применяется к:** пакета публикации &bullet; **поддерживаемые версии:** устаревшими в версии 3.2 +</span><span class="sxs-lookup"><span data-stu-id="0cc8d-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="0cc8d-106">Отражает пакет и его зависимости от репозиториев указанного источника в целевой репозиторий.</span><span class="sxs-lookup"><span data-stu-id="0cc8d-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="0cc8d-107">Чтобы включить эту команду для NuGet версии до версии 3.2, обратитесь к [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)выберите последнюю стабильный выпуск, загрузите `NuGet.ServerExtensions.dll` и `Nuget-Signed.exe` на локальный диск и переименования `Nuget-Signed.exe` для `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="0cc8d-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="0cc8d-108">Использование</span><span class="sxs-lookup"><span data-stu-id="0cc8d-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="0cc8d-109">где `<packageID>` является пакет, чтобы создать зеркало, или `<configFilePath>` идентифицирует `packages.config` файл, который содержит список пакетов, подлежащих зеркальному отображению.</span><span class="sxs-lookup"><span data-stu-id="0cc8d-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="0cc8d-110">`<listUrlTarget>` Указывает исходный репозиторий и `<publishUrlTarget>` указывает целевой репозиторий.</span><span class="sxs-lookup"><span data-stu-id="0cc8d-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="0cc8d-111">Если включено репозиторий целевой `https://machine/repo` , на котором выполняется [NuGet.Server](../hosting-packages/nuget-server.md), URL-адреса со списком и push будут `https://machine/repo/nuget` и `https://machine/repo/api/v2/package`соответственно.</span><span class="sxs-lookup"><span data-stu-id="0cc8d-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="0cc8d-112">Параметры</span><span class="sxs-lookup"><span data-stu-id="0cc8d-112">Options</span></span>

| <span data-ttu-id="0cc8d-113">Параметр</span><span class="sxs-lookup"><span data-stu-id="0cc8d-113">Option</span></span> | <span data-ttu-id="0cc8d-114">Описание:</span><span class="sxs-lookup"><span data-stu-id="0cc8d-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0cc8d-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="0cc8d-115">ApiKey</span></span> | <span data-ttu-id="0cc8d-116">Ключ API для целевой репозиторий.</span><span class="sxs-lookup"><span data-stu-id="0cc8d-116">The API key for the target repository.</span></span> <span data-ttu-id="0cc8d-117">Если не существует, заданный в файле конфигурации используется (`%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac и Linux)).</span><span class="sxs-lookup"><span data-stu-id="0cc8d-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="0cc8d-118">Справка</span><span class="sxs-lookup"><span data-stu-id="0cc8d-118">Help</span></span> | <span data-ttu-id="0cc8d-119">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="0cc8d-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="0cc8d-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="0cc8d-120">NoCache</span></span> | <span data-ttu-id="0cc8d-121">Запрещает NuGet с помощью пакетов из кэшей локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="0cc8d-121">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="0cc8d-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="0cc8d-122">Noop</span></span> | <span data-ttu-id="0cc8d-123">Регистрирует, что выполняются, но не выполняет действий; предполагается успеха для принудительной операций.</span><span class="sxs-lookup"><span data-stu-id="0cc8d-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="0cc8d-124">Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="0cc8d-124">PreRelease</span></span> | <span data-ttu-id="0cc8d-125">Включает предварительные версии пакетов в процессе зеркального отображения.</span><span class="sxs-lookup"><span data-stu-id="0cc8d-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="0cc8d-126">Исходный код</span><span class="sxs-lookup"><span data-stu-id="0cc8d-126">Source</span></span> | <span data-ttu-id="0cc8d-127">Список источников пакетов, подлежащих зеркальному отображению.</span><span class="sxs-lookup"><span data-stu-id="0cc8d-127">A list of package sources to mirror.</span></span> <span data-ttu-id="0cc8d-128">Если не заданы ни один из источников, тех, которые определены в файле конфигурации (см. выше ApiKey), используются, по умолчанию nuget.org, если не указан ни один.</span><span class="sxs-lookup"><span data-stu-id="0cc8d-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="0cc8d-129">Время ожидания</span><span class="sxs-lookup"><span data-stu-id="0cc8d-129">Timeout</span></span> | <span data-ttu-id="0cc8d-130">Указывает время ожидания в секундах для принудительной отправки на сервер.</span><span class="sxs-lookup"><span data-stu-id="0cc8d-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="0cc8d-131">Значение по умолчанию — 300 секунд (5 минут).</span><span class="sxs-lookup"><span data-stu-id="0cc8d-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="0cc8d-132">Версия</span><span class="sxs-lookup"><span data-stu-id="0cc8d-132">Version</span></span> | <span data-ttu-id="0cc8d-133">Версия пакета для установки.</span><span class="sxs-lookup"><span data-stu-id="0cc8d-133">The version of the package to install.</span></span> <span data-ttu-id="0cc8d-134">Если не указан, последняя версия является зеркальным.</span><span class="sxs-lookup"><span data-stu-id="0cc8d-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="0cc8d-135">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0cc8d-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0cc8d-136">Примеры</span><span class="sxs-lookup"><span data-stu-id="0cc8d-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
