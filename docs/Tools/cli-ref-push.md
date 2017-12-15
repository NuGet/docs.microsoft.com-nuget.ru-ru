---
title: "Команду NuGet CLI принудительной | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a9709eee-add2-47fb-98e6-eec0697087f6
description: "Ссылка для команды push nuget.exe"
keywords: "Справочник по принудительной NuGet, команда push"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2828cdc41903d8a948870155b23721724bfa781e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="75f45-104">Команда Push (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="75f45-104">push command (NuGet CLI)</span></span>

<span data-ttu-id="75f45-105">**Применяется к:** пакета публикации &bullet; **поддерживаемые версии:** все; 4.1.0+, необходимые для nuget.org</span><span class="sxs-lookup"><span data-stu-id="75f45-105">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="75f45-106">Для принудительной отправки пакетов nuget.org необходимо использовать nuget.exe v4.1.0 +, которая реализует необходимые [протоколы NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="75f45-106">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="75f45-107">Отправляет пакет источник пакета и публикует его.</span><span class="sxs-lookup"><span data-stu-id="75f45-107">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="75f45-108">Конфигурация по умолчанию NuGet можно получить, загрузив `%AppData%\NuGet\NuGet.Config`, затем загрузки любой `Nuget.Config` или `.nuget\Nuget.Config` файлы, начиная с корневого каталога диска и заканчивается в текущем каталоге (см. [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="75f45-108">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config`, then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="75f45-109">Использование</span><span class="sxs-lookup"><span data-stu-id="75f45-109">Usage</span></span>

```
nuget push <packagePath> [options]
```

<span data-ttu-id="75f45-110">где `<packagePath>` идентификатор пакета для отправки на сервер.</span><span class="sxs-lookup"><span data-stu-id="75f45-110">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="75f45-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="75f45-111">Options</span></span>

| <span data-ttu-id="75f45-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="75f45-112">Option</span></span> | <span data-ttu-id="75f45-113">Описание</span><span class="sxs-lookup"><span data-stu-id="75f45-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="75f45-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="75f45-114">ApiKey</span></span> | <span data-ttu-id="75f45-115">Ключ API для целевой репозиторий.</span><span class="sxs-lookup"><span data-stu-id="75f45-115">The API key for the target repository.</span></span> <span data-ttu-id="75f45-116">Если не существует, указанная в *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="75f45-116">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="75f45-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="75f45-117">ConfigFile</span></span> | <span data-ttu-id="75f45-118">*(2.5 +)*  NuGet файла конфигурации для применения.</span><span class="sxs-lookup"><span data-stu-id="75f45-118">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="75f45-119">Если не указан, *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="75f45-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="75f45-120">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="75f45-120">DisableBuffering</span></span> | <span data-ttu-id="75f45-121">Отключает буферизацию при принудительной установке на сервер HTTP (s), чтобы уменьшить использование памяти.</span><span class="sxs-lookup"><span data-stu-id="75f45-121">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="75f45-122">Внимание: Если этот параметр используется, встроенная проверка подлинности Windows может не работать.</span><span class="sxs-lookup"><span data-stu-id="75f45-122">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="75f45-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="75f45-123">ForceEnglishOutput</span></span> | <span data-ttu-id="75f45-124">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="75f45-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="75f45-125">Справка</span><span class="sxs-lookup"><span data-stu-id="75f45-125">Help</span></span> | <span data-ttu-id="75f45-126">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="75f45-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="75f45-127">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="75f45-127">NonInteractive</span></span> | <span data-ttu-id="75f45-128">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="75f45-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="75f45-129">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="75f45-129">NoSymbols</span></span> | <span data-ttu-id="75f45-130">*(3.5 +)*  Если существует пакет символов, оно не будет включено на сервере символов.</span><span class="sxs-lookup"><span data-stu-id="75f45-130">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="75f45-131">Исходный код</span><span class="sxs-lookup"><span data-stu-id="75f45-131">Source</span></span> | <span data-ttu-id="75f45-132">Определяет URL-адрес сервера.</span><span class="sxs-lookup"><span data-stu-id="75f45-132">Specifies the server URL.</span></span> <span data-ttu-id="75f45-133">С помощью NuGet 2.5 + NuGet идентификации UNC-путь или локальную папку источника и просто скопируйте в нее файл вместо него с помощью протокола HTTP.</span><span class="sxs-lookup"><span data-stu-id="75f45-133">With NuGet 2.5+, NuGet will identify a UNC or local folder source and simply copy the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="75f45-134">Кроме того, начиная с помощью NuGet 3.4.2 Это обязательный параметр если не `NuGet.Config` файл определяет *DefaultPushSource* значение (в разделе [NuGet Настройка поведения](../Consume-Packages/Configuring-NuGet-Behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="75f45-134">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md)).</span></span> |
| <span data-ttu-id="75f45-135">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="75f45-135">SymbolSource</span></span> | <span data-ttu-id="75f45-136">*(3.5 +)*  Указывает URL-адрес сервера символов; nuget.smbsrc.net используется при принудительной установке в nuget.org</span><span class="sxs-lookup"><span data-stu-id="75f45-136">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="75f45-137">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="75f45-137">SymbolApiKey</span></span> | <span data-ttu-id="75f45-138">*(3.5 +)*  Указывает ключ API для URL-адрес, указанной в `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="75f45-138">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="75f45-139">Время ожидания</span><span class="sxs-lookup"><span data-stu-id="75f45-139">Timeout</span></span> | <span data-ttu-id="75f45-140">Указывает время ожидания в секундах для принудительной отправки на сервер.</span><span class="sxs-lookup"><span data-stu-id="75f45-140">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="75f45-141">Значение по умолчанию — 300 секунд (5 минут).</span><span class="sxs-lookup"><span data-stu-id="75f45-141">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="75f45-142">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="75f45-142">Verbosity</span></span> | <span data-ttu-id="75f45-143">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="75f45-143">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="75f45-144">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="75f45-144">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="75f45-145">Примеры</span><span class="sxs-lookup"><span data-stu-id="75f45-145">Examples</span></span>

```
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
