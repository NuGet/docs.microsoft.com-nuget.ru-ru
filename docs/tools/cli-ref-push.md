---
title: Команда интерфейса командной строки NuGet push
description: Справочник по командам nuget.exe Push-уведомлений
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 125671ca3f695f82bd74f8097e590c3972003e22
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548347"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="60594-103">Команда Push (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="60594-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="60594-104">**Применяется к:** пакета публикации &bullet; **поддерживаемые версии:** всем: 4.1.0, необходимые для nuget.org</span><span class="sxs-lookup"><span data-stu-id="60594-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="60594-105">Чтобы отправлять пакеты на сайте nuget.org необходимо использовать nuget.exe версии 4.1.0 +, которая реализует необходимые [протоколы NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="60594-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="60594-106">Отправляет пакет источник пакета и публикует его.</span><span class="sxs-lookup"><span data-stu-id="60594-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="60594-107">Конфигурацию NuGet по умолчанию можно получить, загрузив `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), затем загрузить любое `Nuget.Config` или `.nuget\Nuget.Config` файлы начиная с корневого каталога диска и заканчивая текущим каталогом (см. в разделе [Настройка Поведение NuGet](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="60594-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="60594-108">Использование</span><span class="sxs-lookup"><span data-stu-id="60594-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="60594-109">где `<packagePath>` идентифицирует пакет для отправки на сервер.</span><span class="sxs-lookup"><span data-stu-id="60594-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="60594-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="60594-110">Options</span></span>

| <span data-ttu-id="60594-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="60594-111">Option</span></span> | <span data-ttu-id="60594-112">Описание</span><span class="sxs-lookup"><span data-stu-id="60594-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="60594-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="60594-113">ApiKey</span></span> | <span data-ttu-id="60594-114">Ключ API для целевого репозитория.</span><span class="sxs-lookup"><span data-stu-id="60594-114">The API key for the target repository.</span></span> <span data-ttu-id="60594-115">Если не указано, используется, указанную в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="60594-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="60594-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="60594-116">ConfigFile</span></span> | <span data-ttu-id="60594-117">Чтобы применить файл конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="60594-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="60594-118">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="60594-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="60594-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="60594-119">DisableBuffering</span></span> | <span data-ttu-id="60594-120">Отключает буферизацию при передаче на сервер HTTP (s), чтобы уменьшить использование памяти.</span><span class="sxs-lookup"><span data-stu-id="60594-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="60594-121">Внимание: Если этот параметр используется, встроенная проверка подлинности Windows может не работать.</span><span class="sxs-lookup"><span data-stu-id="60594-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="60594-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="60594-122">ForceEnglishOutput</span></span> | <span data-ttu-id="60594-123">*(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры.</span><span class="sxs-lookup"><span data-stu-id="60594-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="60594-124">Справка</span><span class="sxs-lookup"><span data-stu-id="60594-124">Help</span></span> | <span data-ttu-id="60594-125">Отображает справку для команды.</span><span class="sxs-lookup"><span data-stu-id="60594-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="60594-126">Неинтерактивная</span><span class="sxs-lookup"><span data-stu-id="60594-126">NonInteractive</span></span> | <span data-ttu-id="60594-127">Подавление для пользователя данные или подтверждения.</span><span class="sxs-lookup"><span data-stu-id="60594-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="60594-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="60594-128">NoSymbols</span></span> | <span data-ttu-id="60594-129">*(3.5 и более поздние)*  Если существует пакет символов, он не будет включено на сервере символов.</span><span class="sxs-lookup"><span data-stu-id="60594-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="60594-130">Исходный код</span><span class="sxs-lookup"><span data-stu-id="60594-130">Source</span></span> | <span data-ttu-id="60594-131">Определяет URL-адрес сервера.</span><span class="sxs-lookup"><span data-stu-id="60594-131">Specifies the server URL.</span></span> <span data-ttu-id="60594-132">NuGet идентифицирует UNC-путь или локальную папку источника и просто копирует в нее файл вместо передачи его с помощью HTTP.</span><span class="sxs-lookup"><span data-stu-id="60594-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="60594-133">Кроме того, начиная с NuGet 3.4.2, это является обязательным параметром Если `NuGet.Config` указывает файл *DefaultPushSource* значение (см. в разделе [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="60594-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="60594-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="60594-134">SymbolSource</span></span> | <span data-ttu-id="60594-135">*(3.5 и более поздние)*  Указывает URL-адрес сервера символов; nuget.smbsrc.net используется при передаче данных на сайте nuget.org</span><span class="sxs-lookup"><span data-stu-id="60594-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="60594-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="60594-136">SymbolApiKey</span></span> | <span data-ttu-id="60594-137">*(3.5 и более поздние)*  Содержит ключ API для URL-адрес, указанной в `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="60594-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="60594-138">Время ожидания</span><span class="sxs-lookup"><span data-stu-id="60594-138">Timeout</span></span> | <span data-ttu-id="60594-139">Указывает время ожидания в секундах, для передачи на сервер.</span><span class="sxs-lookup"><span data-stu-id="60594-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="60594-140">Значение по умолчанию — 300 секунд (5 минут).</span><span class="sxs-lookup"><span data-stu-id="60594-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="60594-141">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="60594-141">Verbosity</span></span> | <span data-ttu-id="60594-142">Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="60594-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="60594-143">Также см. в разделе [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="60594-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="60594-144">Примеры</span><span class="sxs-lookup"><span data-stu-id="60594-144">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
