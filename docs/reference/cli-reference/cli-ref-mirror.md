---
title: Зеркальная команда CLI NuGet
description: Справочник по команде nuget.exe Mirror
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a7247aeb21418e78dbfe9be15c2e7cd152aa3f4a
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622971"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="a05b4-103">Команда Mirror (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="a05b4-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="a05b4-104">Область **применения:** &bullet; **Поддерживаемые версии** публикации пакетов: не рекомендуется в 3.2 +</span><span class="sxs-lookup"><span data-stu-id="a05b4-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="a05b4-105">Отражает пакет и его зависимости от указанных исходных репозиториев в целевом репозитории.</span><span class="sxs-lookup"><span data-stu-id="a05b4-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="a05b4-106">NuGet.ServerExtensions.dll и NuGet-Signed.exe, которые ранее поддерживали эту команду в NuGet 2. x (путем переименования NuGet-Signed.exe в nuget.exe), больше не доступны для загрузки.</span><span class="sxs-lookup"><span data-stu-id="a05b4-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="a05b4-107">Чтобы использовать команду, аналогичную этой, попробуйте [нужетмиррор](https://www.nuget.org/packages/NuGetMirror/).</span><span class="sxs-lookup"><span data-stu-id="a05b4-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="a05b4-108">Использование</span><span class="sxs-lookup"><span data-stu-id="a05b4-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="a05b4-109">где `<packageID>` — это пакет для зеркального отображения, или `<configFilePath>` `packages.config` файл, в котором перечислены пакеты для зеркального отображения.</span><span class="sxs-lookup"><span data-stu-id="a05b4-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="a05b4-110">`<listUrlTarget>`Указывает исходный репозиторий и `<publishUrlTarget>` указывает целевой репозиторий.</span><span class="sxs-lookup"><span data-stu-id="a05b4-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="a05b4-111">Если целевой репозиторий находится на `https://machine/repo` [сервере NuGet. Server](../../hosting-packages/nuget-server.md), URL-адреса списка и отправки отправляются `https://machine/repo/nuget` `https://machine/repo/api/v2/package` соответственно.</span><span class="sxs-lookup"><span data-stu-id="a05b4-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="a05b4-112">Параметры</span><span class="sxs-lookup"><span data-stu-id="a05b4-112">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="a05b4-113">Ключ API для целевого репозитория.</span><span class="sxs-lookup"><span data-stu-id="a05b4-113">The API key for the target repository.</span></span> <span data-ttu-id="a05b4-114">Если он отсутствует, используется указанный в файле конфигурации ( `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="a05b4-114">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span>

- **`-Help`**

  <span data-ttu-id="a05b4-115">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="a05b4-115">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="a05b4-116">Предотвращает использование кэшированных пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="a05b4-116">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="a05b4-117">См. раздел [Управление глобальными пакетами и папками кэша](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="a05b4-117">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-Noop`**

  <span data-ttu-id="a05b4-118">Записывает в журнал то, что было сделано, но не выполняет действия. Предполагается успешность операций принудительной отправки.</span><span class="sxs-lookup"><span data-stu-id="a05b4-118">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="a05b4-119">Включает предварительные пакеты в операцию зеркального отображения.</span><span class="sxs-lookup"><span data-stu-id="a05b4-119">Includes prerelease packages in the mirroring operation.</span></span>

- **`-Source`**

  <span data-ttu-id="a05b4-120">Список источников пакетов для зеркального отображения.</span><span class="sxs-lookup"><span data-stu-id="a05b4-120">A list of package sources to mirror.</span></span> <span data-ttu-id="a05b4-121">Если источники не указаны, используются те, которые определены в файле конфигурации (см. ApiKey выше), по умолчанию используется значение nuget.org, если не указано ни одного.</span><span class="sxs-lookup"><span data-stu-id="a05b4-121">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span>

- **`-Timeout`**

  <span data-ttu-id="a05b4-122">Указывает время ожидания в секундах для отправки на сервер.</span><span class="sxs-lookup"><span data-stu-id="a05b4-122">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="a05b4-123"> Значение по умолчанию — 300 секунд (5 минут).</span><span class="sxs-lookup"><span data-stu-id="a05b4-123">The default is 300 seconds (5 minutes).</span></span>

- **`-Version`**

  <span data-ttu-id="a05b4-124">Версия пакета для установки.</span><span class="sxs-lookup"><span data-stu-id="a05b4-124">The version of the package to install.</span></span> <span data-ttu-id="a05b4-125">Если не указано, отображается последняя версия.</span><span class="sxs-lookup"><span data-stu-id="a05b4-125">If not specified, the latest version is mirrored.</span></span>

<span data-ttu-id="a05b4-126">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a05b4-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a05b4-127">Примеры</span><span class="sxs-lookup"><span data-stu-id="a05b4-127">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
