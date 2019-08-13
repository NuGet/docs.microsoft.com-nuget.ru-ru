---
title: Зеркальная команда CLI NuGet
description: Справочник по команде NuGet. exe Mirror
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 81866172bfbf55c42ee96c213c0117f1f986235c
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959713"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="10c97-103">Команда mirror (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="10c97-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="10c97-104">Область **применения:** &bullet; **Поддерживаемые версии** публикации пакетов: не рекомендуется в 3.2 +</span><span class="sxs-lookup"><span data-stu-id="10c97-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="10c97-105">Отражает пакет и его зависимости от указанных исходных репозиториев в целевом репозитории.</span><span class="sxs-lookup"><span data-stu-id="10c97-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="10c97-106">NuGet. Серверекстенсионс. dll и нужет-сигнед. exe, которые ранее поддерживали эту команду в NuGet 2. x (путем переименования нужет-сигнед. exe в NuGet. exe), больше не доступны для загрузки.</span><span class="sxs-lookup"><span data-stu-id="10c97-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="10c97-107">Чтобы использовать команду, аналогичную этой, попробуйте [нужетмиррор](https://www.nuget.org/packages/NuGetMirror/).</span><span class="sxs-lookup"><span data-stu-id="10c97-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="10c97-108">Использование</span><span class="sxs-lookup"><span data-stu-id="10c97-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="10c97-109">где `<packageID>` — это пакет для зеркального отображения `<configFilePath>` , или `packages.config` файл, в котором перечислены пакеты для зеркального отображения.</span><span class="sxs-lookup"><span data-stu-id="10c97-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="10c97-110">Указывает исходный репозиторий и `<publishUrlTarget>` указывает целевой репозиторий. `<listUrlTarget>`</span><span class="sxs-lookup"><span data-stu-id="10c97-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="10c97-111">Если целевой репозиторий находится на `https://machine/repo` [сервере NuGet. Server](../../hosting-packages/nuget-server.md), `https://machine/repo/nuget` `https://machine/repo/api/v2/package`URL-адреса списка и отправки отправляются соответственно.</span><span class="sxs-lookup"><span data-stu-id="10c97-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="10c97-112">Параметры</span><span class="sxs-lookup"><span data-stu-id="10c97-112">Options</span></span>

| <span data-ttu-id="10c97-113">Параметр</span><span class="sxs-lookup"><span data-stu-id="10c97-113">Option</span></span> | <span data-ttu-id="10c97-114">Описание</span><span class="sxs-lookup"><span data-stu-id="10c97-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="10c97-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="10c97-115">ApiKey</span></span> | <span data-ttu-id="10c97-116">Ключ API для целевого репозитория.</span><span class="sxs-lookup"><span data-stu-id="10c97-116">The API key for the target repository.</span></span> <span data-ttu-id="10c97-117">Если он отсутствует, используется указанный в файле конфигурации (`%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="10c97-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="10c97-118">Help</span><span class="sxs-lookup"><span data-stu-id="10c97-118">Help</span></span> | <span data-ttu-id="10c97-119">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="10c97-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="10c97-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="10c97-120">NoCache</span></span> | <span data-ttu-id="10c97-121">Предотвращает использование кэшированных пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="10c97-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="10c97-122">См. раздел [Управление глобальными пакетами и папками кэша](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="10c97-122">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="10c97-123">NOOP</span><span class="sxs-lookup"><span data-stu-id="10c97-123">Noop</span></span> | <span data-ttu-id="10c97-124">Записывает в журнал то, что было сделано, но не выполняет действия. Предполагается успешность операций принудительной отправки.</span><span class="sxs-lookup"><span data-stu-id="10c97-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="10c97-125">Предварительной</span><span class="sxs-lookup"><span data-stu-id="10c97-125">PreRelease</span></span> | <span data-ttu-id="10c97-126">Включает предварительные пакеты в операцию зеркального отображения.</span><span class="sxs-lookup"><span data-stu-id="10c97-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="10c97-127">Source</span><span class="sxs-lookup"><span data-stu-id="10c97-127">Source</span></span> | <span data-ttu-id="10c97-128">Список источников пакетов для зеркального отображения.</span><span class="sxs-lookup"><span data-stu-id="10c97-128">A list of package sources to mirror.</span></span> <span data-ttu-id="10c97-129">Если источники не указаны, используются те, которые определены в файле конфигурации (см. ApiKey выше), по умолчанию используется значение nuget.org, если не указано ни одного.</span><span class="sxs-lookup"><span data-stu-id="10c97-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="10c97-130">Время ожидания</span><span class="sxs-lookup"><span data-stu-id="10c97-130">Timeout</span></span> | <span data-ttu-id="10c97-131">Указывает время ожидания в секундах для отправки на сервер.</span><span class="sxs-lookup"><span data-stu-id="10c97-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="10c97-132">Значение по умолчанию — 300 секунд (5 минут).</span><span class="sxs-lookup"><span data-stu-id="10c97-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="10c97-133">Версия</span><span class="sxs-lookup"><span data-stu-id="10c97-133">Version</span></span> | <span data-ttu-id="10c97-134">Версия пакета для установки.</span><span class="sxs-lookup"><span data-stu-id="10c97-134">The version of the package to install.</span></span> <span data-ttu-id="10c97-135">Если не указано, отображается последняя версия.</span><span class="sxs-lookup"><span data-stu-id="10c97-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="10c97-136">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="10c97-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="10c97-137">Примеры</span><span class="sxs-lookup"><span data-stu-id="10c97-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
