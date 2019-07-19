---
title: Зеркальная команда CLI NuGet
description: Справочник по команде NuGet. exe Mirror
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327671"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="b3a66-103">Команда mirror (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b3a66-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="b3a66-104">Область **применения:** &bullet; **Поддерживаемые версии** публикации пакетов: не рекомендуется в 3.2 +</span><span class="sxs-lookup"><span data-stu-id="b3a66-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="b3a66-105">Отражает пакет и его зависимости от указанных исходных репозиториев в целевом репозитории.</span><span class="sxs-lookup"><span data-stu-id="b3a66-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="b3a66-106">Чтобы включить эту команду для версий NuGet до 3,2, перейдите на [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)страницу, выберите последний стабильный выпуск, `NuGet.ServerExtensions.dll` Скачайте `Nuget-Signed.exe` и перейдите на локальный диск и `Nuget-Signed.exe` переименуйте в `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="b3a66-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="b3a66-107">Использование</span><span class="sxs-lookup"><span data-stu-id="b3a66-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="b3a66-108">где `<packageID>` — это пакет для зеркального отображения `<configFilePath>` , или `packages.config` файл, в котором перечислены пакеты для зеркального отображения.</span><span class="sxs-lookup"><span data-stu-id="b3a66-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="b3a66-109">Указывает исходный репозиторий и `<publishUrlTarget>` указывает целевой репозиторий. `<listUrlTarget>`</span><span class="sxs-lookup"><span data-stu-id="b3a66-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="b3a66-110">Если целевой репозиторий находится на `https://machine/repo` [сервере NuGet. Server](../../hosting-packages/nuget-server.md), `https://machine/repo/nuget` `https://machine/repo/api/v2/package`URL-адреса списка и отправки отправляются соответственно.</span><span class="sxs-lookup"><span data-stu-id="b3a66-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="b3a66-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="b3a66-111">Options</span></span>

| <span data-ttu-id="b3a66-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="b3a66-112">Option</span></span> | <span data-ttu-id="b3a66-113">Описание</span><span class="sxs-lookup"><span data-stu-id="b3a66-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b3a66-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="b3a66-114">ApiKey</span></span> | <span data-ttu-id="b3a66-115">Ключ API для целевого репозитория.</span><span class="sxs-lookup"><span data-stu-id="b3a66-115">The API key for the target repository.</span></span> <span data-ttu-id="b3a66-116">Если он отсутствует, используется указанный в файле конфигурации (`%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="b3a66-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="b3a66-117">Help</span><span class="sxs-lookup"><span data-stu-id="b3a66-117">Help</span></span> | <span data-ttu-id="b3a66-118">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="b3a66-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="b3a66-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="b3a66-119">NoCache</span></span> | <span data-ttu-id="b3a66-120">Предотвращает использование кэшированных пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="b3a66-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="b3a66-121">См. раздел [Управление глобальными пакетами и папками кэша](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="b3a66-121">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="b3a66-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="b3a66-122">Noop</span></span> | <span data-ttu-id="b3a66-123">Записывает в журнал то, что было сделано, но не выполняет действия. Предполагается успешность операций принудительной отправки.</span><span class="sxs-lookup"><span data-stu-id="b3a66-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="b3a66-124">Предварительной</span><span class="sxs-lookup"><span data-stu-id="b3a66-124">PreRelease</span></span> | <span data-ttu-id="b3a66-125">Включает предварительные пакеты в операцию зеркального отображения.</span><span class="sxs-lookup"><span data-stu-id="b3a66-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="b3a66-126">Source</span><span class="sxs-lookup"><span data-stu-id="b3a66-126">Source</span></span> | <span data-ttu-id="b3a66-127">Список источников пакетов для зеркального отображения.</span><span class="sxs-lookup"><span data-stu-id="b3a66-127">A list of package sources to mirror.</span></span> <span data-ttu-id="b3a66-128">Если источники не указаны, используются те, которые определены в файле конфигурации (см. ApiKey выше), по умолчанию используется значение nuget.org, если не указано ни одного.</span><span class="sxs-lookup"><span data-stu-id="b3a66-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="b3a66-129">Время ожидания</span><span class="sxs-lookup"><span data-stu-id="b3a66-129">Timeout</span></span> | <span data-ttu-id="b3a66-130">Указывает время ожидания в секундах для отправки на сервер.</span><span class="sxs-lookup"><span data-stu-id="b3a66-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="b3a66-131">Значение по умолчанию — 300 секунд (5 минут).</span><span class="sxs-lookup"><span data-stu-id="b3a66-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="b3a66-132">Версия</span><span class="sxs-lookup"><span data-stu-id="b3a66-132">Version</span></span> | <span data-ttu-id="b3a66-133">Версия пакета для установки.</span><span class="sxs-lookup"><span data-stu-id="b3a66-133">The version of the package to install.</span></span> <span data-ttu-id="b3a66-134">Если не указано, отображается последняя версия.</span><span class="sxs-lookup"><span data-stu-id="b3a66-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="b3a66-135">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b3a66-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b3a66-136">Примеры</span><span class="sxs-lookup"><span data-stu-id="b3a66-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
