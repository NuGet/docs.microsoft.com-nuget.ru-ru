---
title: Команда зеркальной NuGet CLI
description: Справочник по команда зеркало nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4cec854f05fcd207bb15a50ea4ebdc201fdb3ac6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818156"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="7edde-103">Команда mirror (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7edde-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="7edde-104">**Применяется к:** пакета публикации &bullet; **поддерживаемые версии:** устаревшими в версии 3.2 +</span><span class="sxs-lookup"><span data-stu-id="7edde-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="7edde-105">Отражает пакет и его зависимости от репозиториев указанного источника в целевой репозиторий.</span><span class="sxs-lookup"><span data-stu-id="7edde-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="7edde-106">Чтобы включить эту команду для NuGet версии до версии 3.2, обратитесь к [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)выберите последнюю стабильный выпуск, загрузите `NuGet.ServerExtensions.dll` и `Nuget-Signed.exe` на локальный диск и переименования `Nuget-Signed.exe` для `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="7edde-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="7edde-107">Использование</span><span class="sxs-lookup"><span data-stu-id="7edde-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="7edde-108">где `<packageID>` является пакет, чтобы создать зеркало, или `<configFilePath>` идентифицирует `packages.config` файл, который содержит список пакетов, подлежащих зеркальному отображению.</span><span class="sxs-lookup"><span data-stu-id="7edde-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="7edde-109">`<listUrlTarget>` Указывает исходный репозиторий и `<publishUrlTarget>` указывает целевой репозиторий.</span><span class="sxs-lookup"><span data-stu-id="7edde-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="7edde-110">Если включено репозиторий целевой `https://machine/repo` , на котором выполняется [NuGet.Server](../hosting-packages/nuget-server.md), URL-адреса со списком и push будут `https://machine/repo/nuget` и `https://machine/repo/api/v2/package`соответственно.</span><span class="sxs-lookup"><span data-stu-id="7edde-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="7edde-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="7edde-111">Options</span></span>

| <span data-ttu-id="7edde-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="7edde-112">Option</span></span> | <span data-ttu-id="7edde-113">Описание:</span><span class="sxs-lookup"><span data-stu-id="7edde-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7edde-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="7edde-114">ApiKey</span></span> | <span data-ttu-id="7edde-115">Ключ API для целевой репозиторий.</span><span class="sxs-lookup"><span data-stu-id="7edde-115">The API key for the target repository.</span></span> <span data-ttu-id="7edde-116">Если не существует, заданный в файле конфигурации используется (`%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac и Linux)).</span><span class="sxs-lookup"><span data-stu-id="7edde-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="7edde-117">Справка</span><span class="sxs-lookup"><span data-stu-id="7edde-117">Help</span></span> | <span data-ttu-id="7edde-118">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="7edde-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="7edde-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="7edde-119">NoCache</span></span> | <span data-ttu-id="7edde-120">Предотвращает использование кэшированных пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="7edde-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="7edde-121">В разделе [управление глобального пакетами и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="7edde-121">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="7edde-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="7edde-122">Noop</span></span> | <span data-ttu-id="7edde-123">Регистрирует, что выполняются, но не выполняет действий; предполагается успеха для принудительной операций.</span><span class="sxs-lookup"><span data-stu-id="7edde-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="7edde-124">Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="7edde-124">PreRelease</span></span> | <span data-ttu-id="7edde-125">Включает предварительные версии пакетов в процессе зеркального отображения.</span><span class="sxs-lookup"><span data-stu-id="7edde-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="7edde-126">Исходный код</span><span class="sxs-lookup"><span data-stu-id="7edde-126">Source</span></span> | <span data-ttu-id="7edde-127">Список источников пакетов, подлежащих зеркальному отображению.</span><span class="sxs-lookup"><span data-stu-id="7edde-127">A list of package sources to mirror.</span></span> <span data-ttu-id="7edde-128">Если не заданы ни один из источников, тех, которые определены в файле конфигурации (см. выше ApiKey), используются, по умолчанию nuget.org, если не указан ни один.</span><span class="sxs-lookup"><span data-stu-id="7edde-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="7edde-129">Время ожидания</span><span class="sxs-lookup"><span data-stu-id="7edde-129">Timeout</span></span> | <span data-ttu-id="7edde-130">Указывает время ожидания в секундах для принудительной отправки на сервер.</span><span class="sxs-lookup"><span data-stu-id="7edde-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="7edde-131">Значение по умолчанию — 300 секунд (5 минут).</span><span class="sxs-lookup"><span data-stu-id="7edde-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="7edde-132">Версия</span><span class="sxs-lookup"><span data-stu-id="7edde-132">Version</span></span> | <span data-ttu-id="7edde-133">Версия пакета для установки.</span><span class="sxs-lookup"><span data-stu-id="7edde-133">The version of the package to install.</span></span> <span data-ttu-id="7edde-134">Если не указан, последняя версия является зеркальным.</span><span class="sxs-lookup"><span data-stu-id="7edde-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="7edde-135">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7edde-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7edde-136">Примеры</span><span class="sxs-lookup"><span data-stu-id="7edde-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
