---
title: NuGet CLI удалить команду | Документы Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Ссылка для команды delete nuget.exe
keywords: NuGet ссылки, удалите пакет команд
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9445042c46ef41721def1fbbb8dcebf4afc14d1b
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="ab542-104">Удаление команды (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ab542-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="ab542-105">**Применяется к:** пакета публикации &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="ab542-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ab542-106">Удаляет или unlists пакета из исходного пакета.</span><span class="sxs-lookup"><span data-stu-id="ab542-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="ab542-107">Для nuget.org команды удаления [unlists пакета](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ab542-107">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="ab542-108">Использование</span><span class="sxs-lookup"><span data-stu-id="ab542-108">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="ab542-109">где `<packageID>` и `<packageVersion>` определить точный пакета для удаления или исключить.</span><span class="sxs-lookup"><span data-stu-id="ab542-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="ab542-110">Точное поведение зависит от источника.</span><span class="sxs-lookup"><span data-stu-id="ab542-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="ab542-111">Для локальных папок например, пакет удаляется; для nuget.org пакета, отсутствующие в списке.</span><span class="sxs-lookup"><span data-stu-id="ab542-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="ab542-112">Параметры</span><span class="sxs-lookup"><span data-stu-id="ab542-112">Options</span></span>

| <span data-ttu-id="ab542-113">Параметр</span><span class="sxs-lookup"><span data-stu-id="ab542-113">Option</span></span> | <span data-ttu-id="ab542-114">Описание</span><span class="sxs-lookup"><span data-stu-id="ab542-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ab542-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="ab542-115">ApiKey</span></span> | <span data-ttu-id="ab542-116">Ключ API для целевой репозиторий.</span><span class="sxs-lookup"><span data-stu-id="ab542-116">The API key for the target repository.</span></span> <span data-ttu-id="ab542-117">Если он отсутствует, используется заданный в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ab542-117">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="ab542-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ab542-118">ConfigFile</span></span> | <span data-ttu-id="ab542-119">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="ab542-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ab542-120">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="ab542-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ab542-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ab542-121">ForceEnglishOutput</span></span> | <span data-ttu-id="ab542-122">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="ab542-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ab542-123">Справка</span><span class="sxs-lookup"><span data-stu-id="ab542-123">Help</span></span> | <span data-ttu-id="ab542-124">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="ab542-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="ab542-125">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="ab542-125">NonInteractive</span></span> | <span data-ttu-id="ab542-126">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="ab542-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ab542-127">Исходный код</span><span class="sxs-lookup"><span data-stu-id="ab542-127">Source</span></span> | <span data-ttu-id="ab542-128">Определяет URL-адрес сервера.</span><span class="sxs-lookup"><span data-stu-id="ab542-128">Specifies the server URL.</span></span> <span data-ttu-id="ab542-129">URL-адрес для nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="ab542-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="ab542-130">Закрытый веб-каналы, замените на имя узла, например, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="ab542-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="ab542-131">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="ab542-131">Verbosity</span></span> | <span data-ttu-id="ab542-132">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="ab542-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ab542-133">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ab542-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ab542-134">Примеры</span><span class="sxs-lookup"><span data-stu-id="ab542-134">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
