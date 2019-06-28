---
title: Команда delete интерфейса командной строки NuGet
description: Справочник по командам nuget.exe delete
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3ea2dc3e87d0a626704fe5623d39eaf5bd3f3446
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426111"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="1fb3c-103">удалить команду (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1fb3c-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="1fb3c-104">**Применяется к:** пакета публикации &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="1fb3c-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="1fb3c-105">Удаляет или из списка пакетов из источника пакета.</span><span class="sxs-lookup"><span data-stu-id="1fb3c-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="1fb3c-106">Для nuget.org, команда delete [из списка пакета](../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="1fb3c-106">For nuget.org, the delete command [unlists the package](../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="1fb3c-107">Использование</span><span class="sxs-lookup"><span data-stu-id="1fb3c-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="1fb3c-108">где `<packageID>` и `<packageVersion>` идентифицировать точный пакет для удаления или удалить из списка.</span><span class="sxs-lookup"><span data-stu-id="1fb3c-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="1fb3c-109">Точное поведение зависит от источника.</span><span class="sxs-lookup"><span data-stu-id="1fb3c-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="1fb3c-110">Для локальных папок например, пакет удаляется; для пакета nuget.org, отсутствующие в списке.</span><span class="sxs-lookup"><span data-stu-id="1fb3c-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="1fb3c-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="1fb3c-111">Options</span></span>

| <span data-ttu-id="1fb3c-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="1fb3c-112">Option</span></span> | <span data-ttu-id="1fb3c-113">Описание</span><span class="sxs-lookup"><span data-stu-id="1fb3c-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1fb3c-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="1fb3c-114">ApiKey</span></span> | <span data-ttu-id="1fb3c-115">Ключ API для целевого репозитория.</span><span class="sxs-lookup"><span data-stu-id="1fb3c-115">The API key for the target repository.</span></span> <span data-ttu-id="1fb3c-116">Если не указано, используется, указанную в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1fb3c-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="1fb3c-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1fb3c-117">ConfigFile</span></span> | <span data-ttu-id="1fb3c-118">Чтобы применить файл конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="1fb3c-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1fb3c-119">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="1fb3c-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1fb3c-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1fb3c-120">ForceEnglishOutput</span></span> | <span data-ttu-id="1fb3c-121">*(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры.</span><span class="sxs-lookup"><span data-stu-id="1fb3c-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1fb3c-122">Help</span><span class="sxs-lookup"><span data-stu-id="1fb3c-122">Help</span></span> | <span data-ttu-id="1fb3c-123">Отображает справку для команды.</span><span class="sxs-lookup"><span data-stu-id="1fb3c-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="1fb3c-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1fb3c-124">NonInteractive</span></span> | <span data-ttu-id="1fb3c-125">Подавление для пользователя данные или подтверждения.</span><span class="sxs-lookup"><span data-stu-id="1fb3c-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1fb3c-126">Source</span><span class="sxs-lookup"><span data-stu-id="1fb3c-126">Source</span></span> | <span data-ttu-id="1fb3c-127">Определяет URL-адрес сервера.</span><span class="sxs-lookup"><span data-stu-id="1fb3c-127">Specifies the server URL.</span></span> <span data-ttu-id="1fb3c-128">URL-адреса для nuget.org — `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="1fb3c-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="1fb3c-129">Для частных каналов замените имя узла, например, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="1fb3c-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="1fb3c-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="1fb3c-130">Verbosity</span></span> | <span data-ttu-id="1fb3c-131">Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="1fb3c-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="1fb3c-132">Также см. в разделе [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1fb3c-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1fb3c-133">Примеры</span><span class="sxs-lookup"><span data-stu-id="1fb3c-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
