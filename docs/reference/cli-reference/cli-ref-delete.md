---
title: Команда удаления интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe Delete
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327841"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="3298d-103">команда Delete (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="3298d-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="3298d-104">Область **применения:** &bullet; **Поддерживаемые версии** публикации пакетов: все</span><span class="sxs-lookup"><span data-stu-id="3298d-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="3298d-105">Удаляет пакет из источника пакета или выводит из него список.</span><span class="sxs-lookup"><span data-stu-id="3298d-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="3298d-106">Для nuget.org команда Delete удаляет [из списка пакет](../../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="3298d-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="3298d-107">Использование</span><span class="sxs-lookup"><span data-stu-id="3298d-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="3298d-108">где `<packageID>` и`<packageVersion>` выявление точного пакета, который нужно удалить или отменить из списка.</span><span class="sxs-lookup"><span data-stu-id="3298d-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="3298d-109">Точное поведение зависит от источника.</span><span class="sxs-lookup"><span data-stu-id="3298d-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="3298d-110">Например, для локальных папок пакет удаляется. для nuget.org пакет не входит в список.</span><span class="sxs-lookup"><span data-stu-id="3298d-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="3298d-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="3298d-111">Options</span></span>

| <span data-ttu-id="3298d-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="3298d-112">Option</span></span> | <span data-ttu-id="3298d-113">Описание</span><span class="sxs-lookup"><span data-stu-id="3298d-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3298d-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="3298d-114">ApiKey</span></span> | <span data-ttu-id="3298d-115">Ключ API для целевого репозитория.</span><span class="sxs-lookup"><span data-stu-id="3298d-115">The API key for the target repository.</span></span> <span data-ttu-id="3298d-116">Если он отсутствует, используется указанный в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3298d-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="3298d-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3298d-117">ConfigFile</span></span> | <span data-ttu-id="3298d-118">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="3298d-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3298d-119">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="3298d-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3298d-120">форцеенглишаутпут</span><span class="sxs-lookup"><span data-stu-id="3298d-120">ForceEnglishOutput</span></span> | <span data-ttu-id="3298d-121">*(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="3298d-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3298d-122">Help</span><span class="sxs-lookup"><span data-stu-id="3298d-122">Help</span></span> | <span data-ttu-id="3298d-123">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="3298d-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="3298d-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3298d-124">NonInteractive</span></span> | <span data-ttu-id="3298d-125">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="3298d-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3298d-126">Source</span><span class="sxs-lookup"><span data-stu-id="3298d-126">Source</span></span> | <span data-ttu-id="3298d-127">Определяет URL-адрес сервера.</span><span class="sxs-lookup"><span data-stu-id="3298d-127">Specifies the server URL.</span></span> <span data-ttu-id="3298d-128">URL-адрес для nuget.org `https://api.nuget.org/v3/index.json`—.</span><span class="sxs-lookup"><span data-stu-id="3298d-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="3298d-129">Для частных веб-каналов замените имя узла, например, *% HostName%/API/V3*.</span><span class="sxs-lookup"><span data-stu-id="3298d-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="3298d-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="3298d-130">Verbosity</span></span> | <span data-ttu-id="3298d-131">Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*.</span><span class="sxs-lookup"><span data-stu-id="3298d-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3298d-132">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3298d-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3298d-133">Примеры</span><span class="sxs-lookup"><span data-stu-id="3298d-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
