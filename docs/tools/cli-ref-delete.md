---
title: Команды удаления NuGet CLI
description: Ссылка для команды delete nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0f33dd5475521da47972a6f032ac6ea86d98c83
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817182"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="febff-103">Удаление команды (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="febff-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="febff-104">**Применяется к:** пакета публикации &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="febff-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="febff-105">Удаляет или unlists пакета из исходного пакета.</span><span class="sxs-lookup"><span data-stu-id="febff-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="febff-106">Для nuget.org команды удаления [unlists пакета](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="febff-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="febff-107">Использование</span><span class="sxs-lookup"><span data-stu-id="febff-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="febff-108">где `<packageID>` и `<packageVersion>` определить точный пакета для удаления или исключить.</span><span class="sxs-lookup"><span data-stu-id="febff-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="febff-109">Точное поведение зависит от источника.</span><span class="sxs-lookup"><span data-stu-id="febff-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="febff-110">Для локальных папок например, пакет удаляется; для nuget.org пакета, отсутствующие в списке.</span><span class="sxs-lookup"><span data-stu-id="febff-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="febff-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="febff-111">Options</span></span>

| <span data-ttu-id="febff-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="febff-112">Option</span></span> | <span data-ttu-id="febff-113">Описание:</span><span class="sxs-lookup"><span data-stu-id="febff-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="febff-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="febff-114">ApiKey</span></span> | <span data-ttu-id="febff-115">Ключ API для целевой репозиторий.</span><span class="sxs-lookup"><span data-stu-id="febff-115">The API key for the target repository.</span></span> <span data-ttu-id="febff-116">Если он отсутствует, используется заданный в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="febff-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="febff-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="febff-117">ConfigFile</span></span> | <span data-ttu-id="febff-118">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="febff-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="febff-119">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="febff-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="febff-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="febff-120">ForceEnglishOutput</span></span> | <span data-ttu-id="febff-121">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="febff-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="febff-122">Справка</span><span class="sxs-lookup"><span data-stu-id="febff-122">Help</span></span> | <span data-ttu-id="febff-123">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="febff-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="febff-124">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="febff-124">NonInteractive</span></span> | <span data-ttu-id="febff-125">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="febff-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="febff-126">Исходный код</span><span class="sxs-lookup"><span data-stu-id="febff-126">Source</span></span> | <span data-ttu-id="febff-127">Определяет URL-адрес сервера.</span><span class="sxs-lookup"><span data-stu-id="febff-127">Specifies the server URL.</span></span> <span data-ttu-id="febff-128">URL-адрес для nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="febff-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="febff-129">Закрытый веб-каналы, замените на имя узла, например, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="febff-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="febff-130">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="febff-130">Verbosity</span></span> | <span data-ttu-id="febff-131">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="febff-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="febff-132">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="febff-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="febff-133">Примеры</span><span class="sxs-lookup"><span data-stu-id="febff-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
