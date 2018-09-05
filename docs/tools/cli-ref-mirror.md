---
title: Зеркальный команды интерфейса командной строки NuGet
description: Справочник по командам зеркальной nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550210"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="c0176-103">Команда mirror (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c0176-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="c0176-104">**Применяется к:** пакета публикации &bullet; **поддерживаемые версии:** устаревшей в 3.2 +</span><span class="sxs-lookup"><span data-stu-id="c0176-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="c0176-105">Отражает пакет и его зависимости из указанного источника репозиториев в целевом репозитории.</span><span class="sxs-lookup"><span data-stu-id="c0176-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="c0176-106">Чтобы включить эту команду для версии NuGet до версии 3.2, перейдите к [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)выберите последний стабильный выпуск, скачайте `NuGet.ServerExtensions.dll` и `Nuget-Signed.exe` на локальный диск и переименования `Nuget-Signed.exe` для `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="c0176-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="c0176-107">Использование</span><span class="sxs-lookup"><span data-stu-id="c0176-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="c0176-108">где `<packageID>` — пакет, чтобы создать зеркало, или `<configFilePath>` идентифицирует `packages.config` файл, который содержит список пакетов, подлежащих зеркальному отображению.</span><span class="sxs-lookup"><span data-stu-id="c0176-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="c0176-109">`<listUrlTarget>` Указывает исходный репозиторий и `<publishUrlTarget>` указывает целевого репозитория.</span><span class="sxs-lookup"><span data-stu-id="c0176-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="c0176-110">Если ваш целевой репозиторий находится в `https://machine/repo` , на котором выполняется [NuGet.Server](../hosting-packages/nuget-server.md), списка и Push-URL-адреса будут `https://machine/repo/nuget` и `https://machine/repo/api/v2/package`, соответственно.</span><span class="sxs-lookup"><span data-stu-id="c0176-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="c0176-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="c0176-111">Options</span></span>

| <span data-ttu-id="c0176-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="c0176-112">Option</span></span> | <span data-ttu-id="c0176-113">Описание</span><span class="sxs-lookup"><span data-stu-id="c0176-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c0176-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="c0176-114">ApiKey</span></span> | <span data-ttu-id="c0176-115">Ключ API для целевого репозитория.</span><span class="sxs-lookup"><span data-stu-id="c0176-115">The API key for the target repository.</span></span> <span data-ttu-id="c0176-116">Если не существует, заданный в файле конфигурации используется (`%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="c0176-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="c0176-117">Справка</span><span class="sxs-lookup"><span data-stu-id="c0176-117">Help</span></span> | <span data-ttu-id="c0176-118">Отображает справку для команды.</span><span class="sxs-lookup"><span data-stu-id="c0176-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="c0176-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="c0176-119">NoCache</span></span> | <span data-ttu-id="c0176-120">Запрещает использовать кэшированные пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="c0176-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="c0176-121">См. в разделе [управление папкой установки глобальных пакетов и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="c0176-121">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="c0176-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="c0176-122">Noop</span></span> | <span data-ttu-id="c0176-123">Журналы, что можно сделать, но не выполняет действий; предполагается, что успех для операции отправки.</span><span class="sxs-lookup"><span data-stu-id="c0176-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="c0176-124">Предварительные выпуски</span><span class="sxs-lookup"><span data-stu-id="c0176-124">PreRelease</span></span> | <span data-ttu-id="c0176-125">Включает в себя предварительные выпуски пакетов в процессе зеркального отображения.</span><span class="sxs-lookup"><span data-stu-id="c0176-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="c0176-126">Исходный код</span><span class="sxs-lookup"><span data-stu-id="c0176-126">Source</span></span> | <span data-ttu-id="c0176-127">Список источников пакетов, подлежащих зеркальному отображению.</span><span class="sxs-lookup"><span data-stu-id="c0176-127">A list of package sources to mirror.</span></span> <span data-ttu-id="c0176-128">Если источники не указаны, тех, которые определены в файле конфигурации (см. в разделе ApiKey выше), используются, установка значений по умолчанию на сайте nuget.org, если не указан ни один.</span><span class="sxs-lookup"><span data-stu-id="c0176-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="c0176-129">Время ожидания</span><span class="sxs-lookup"><span data-stu-id="c0176-129">Timeout</span></span> | <span data-ttu-id="c0176-130">Указывает время ожидания в секундах, для передачи на сервер.</span><span class="sxs-lookup"><span data-stu-id="c0176-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="c0176-131">Значение по умолчанию — 300 секунд (5 минут).</span><span class="sxs-lookup"><span data-stu-id="c0176-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="c0176-132">Версия</span><span class="sxs-lookup"><span data-stu-id="c0176-132">Version</span></span> | <span data-ttu-id="c0176-133">Версия устанавливаемого пакета.</span><span class="sxs-lookup"><span data-stu-id="c0176-133">The version of the package to install.</span></span> <span data-ttu-id="c0176-134">Если не указан, зеркально последней версии.</span><span class="sxs-lookup"><span data-stu-id="c0176-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="c0176-135">Также см. в разделе [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c0176-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c0176-136">Примеры</span><span class="sxs-lookup"><span data-stu-id="c0176-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
