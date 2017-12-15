---
title: "NuGet CLI удалить команду | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: c213a07a-711d-47e0-9ee6-1d582e6cdb69
description: "Ссылка для команды delete nuget.exe"
keywords: "NuGet ссылки, удалите пакет команд"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 92af9dc356f3932347864976496e0ba1216496c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="fca5c-104">Удаление команды (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fca5c-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="fca5c-105">**Применяется к:** пакета публикации &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="fca5c-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="fca5c-106">Удаляет или unlists пакета из исходного пакета.</span><span class="sxs-lookup"><span data-stu-id="fca5c-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="fca5c-107">Для nuget.org команды удаления [unlists пакета](../policies/Deleting-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="fca5c-107">For nuget.org, the delete command [unlists the package](../policies/Deleting-Packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="fca5c-108">Использование</span><span class="sxs-lookup"><span data-stu-id="fca5c-108">Usage</span></span>

```
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="fca5c-109">где `<packageID>` и `<packageVersion>` определить точный пакета для удаления или исключить.</span><span class="sxs-lookup"><span data-stu-id="fca5c-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="fca5c-110">Точное поведение зависит от источника.</span><span class="sxs-lookup"><span data-stu-id="fca5c-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="fca5c-111">Для локальных папок например, пакет удаляется; для nuget.org пакета, отсутствующие в списке.</span><span class="sxs-lookup"><span data-stu-id="fca5c-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="fca5c-112">Параметры</span><span class="sxs-lookup"><span data-stu-id="fca5c-112">Options</span></span>

| <span data-ttu-id="fca5c-113">Параметр</span><span class="sxs-lookup"><span data-stu-id="fca5c-113">Option</span></span> | <span data-ttu-id="fca5c-114">Описание</span><span class="sxs-lookup"><span data-stu-id="fca5c-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fca5c-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="fca5c-115">ApiKey</span></span> | <span data-ttu-id="fca5c-116">Ключ API для целевой репозиторий.</span><span class="sxs-lookup"><span data-stu-id="fca5c-116">The API key for the target repository.</span></span> <span data-ttu-id="fca5c-117">Если не существует, указанная в *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="fca5c-117">If not present, the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="fca5c-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fca5c-118">ConfigFile</span></span> | <span data-ttu-id="fca5c-119">*(2.5 +)*  NuGet файла конфигурации для применения.</span><span class="sxs-lookup"><span data-stu-id="fca5c-119">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="fca5c-120">Если не указан, *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="fca5c-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="fca5c-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fca5c-121">ForceEnglishOutput</span></span> | <span data-ttu-id="fca5c-122">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="fca5c-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fca5c-123">Справка</span><span class="sxs-lookup"><span data-stu-id="fca5c-123">Help</span></span> | <span data-ttu-id="fca5c-124">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="fca5c-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="fca5c-125">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="fca5c-125">NonInteractive</span></span> | <span data-ttu-id="fca5c-126">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="fca5c-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fca5c-127">Исходный код</span><span class="sxs-lookup"><span data-stu-id="fca5c-127">Source</span></span> | <span data-ttu-id="fca5c-128">Определяет URL-адрес сервера.</span><span class="sxs-lookup"><span data-stu-id="fca5c-128">Specifies the server URL.</span></span> <span data-ttu-id="fca5c-129">URL-адрес для nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="fca5c-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="fca5c-130">Закрытый веб-каналы, замените на имя узла, например, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="fca5c-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="fca5c-131">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="fca5c-131">Verbosity</span></span> | <span data-ttu-id="fca5c-132">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="fca5c-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="fca5c-133">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fca5c-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fca5c-134">Примеры</span><span class="sxs-lookup"><span data-stu-id="fca5c-134">Examples</span></span>

```
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
