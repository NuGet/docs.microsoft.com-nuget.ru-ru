---
title: Команда отправки интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe Push
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327631"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="bf541-103">команда push (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="bf541-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="bf541-104">Область **применения:** &bullet; **Поддерживаемые версии** публикации пакетов: ALL; 4.1.0 + требуется для NuGet.org</span><span class="sxs-lookup"><span data-stu-id="bf541-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="bf541-105">Чтобы отправить пакеты в nuget.org, необходимо использовать NuGet. exe v 4.1.0 +, который реализует необходимые [протоколы NuGet](../../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="bf541-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="bf541-106">Отправляет пакет в источник пакета и публикует его.</span><span class="sxs-lookup"><span data-stu-id="bf541-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="bf541-107">Конфигурация NuGet по умолчанию получается путем `%AppData%\NuGet\NuGet.Config` загрузки (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux), а затем `Nuget.Config` загрузки `.nuget\Nuget.Config` любых файлов или, начиная с корневого диска и заканчивая текущим каталогом (см. Общие сведения о NuGet). [ конфигурации](../../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="bf541-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="bf541-108">Использование</span><span class="sxs-lookup"><span data-stu-id="bf541-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="bf541-109">где `<packagePath>` идентифицирует пакет для отправки на сервер.</span><span class="sxs-lookup"><span data-stu-id="bf541-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="bf541-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="bf541-110">Options</span></span>

| <span data-ttu-id="bf541-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="bf541-111">Option</span></span> | <span data-ttu-id="bf541-112">Описание</span><span class="sxs-lookup"><span data-stu-id="bf541-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bf541-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="bf541-113">ApiKey</span></span> | <span data-ttu-id="bf541-114">Ключ API для целевого репозитория.</span><span class="sxs-lookup"><span data-stu-id="bf541-114">The API key for the target repository.</span></span> <span data-ttu-id="bf541-115">Если он отсутствует, используется указанный в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bf541-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="bf541-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="bf541-116">ConfigFile</span></span> | <span data-ttu-id="bf541-117">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="bf541-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="bf541-118">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="bf541-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="bf541-119">дисаблебуфферинг</span><span class="sxs-lookup"><span data-stu-id="bf541-119">DisableBuffering</span></span> | <span data-ttu-id="bf541-120">Отключает буферизацию при принудительной отправке на сервер HTTP (s) для уменьшения использования памяти.</span><span class="sxs-lookup"><span data-stu-id="bf541-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="bf541-121">Внимание! при использовании этого параметра встроенная проверка подлинности Windows может не работать.</span><span class="sxs-lookup"><span data-stu-id="bf541-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="bf541-122">форцеенглишаутпут</span><span class="sxs-lookup"><span data-stu-id="bf541-122">ForceEnglishOutput</span></span> | <span data-ttu-id="bf541-123">*(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="bf541-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="bf541-124">Help</span><span class="sxs-lookup"><span data-stu-id="bf541-124">Help</span></span> | <span data-ttu-id="bf541-125">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="bf541-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="bf541-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="bf541-126">NonInteractive</span></span> | <span data-ttu-id="bf541-127">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="bf541-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="bf541-128">Символы с символами</span><span class="sxs-lookup"><span data-stu-id="bf541-128">NoSymbols</span></span> | <span data-ttu-id="bf541-129">*(3.5 +)* Если пакет символов существует, он не будет отправлен на сервер символов.</span><span class="sxs-lookup"><span data-stu-id="bf541-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="bf541-130">Source</span><span class="sxs-lookup"><span data-stu-id="bf541-130">Source</span></span> | <span data-ttu-id="bf541-131">Определяет URL-адрес сервера.</span><span class="sxs-lookup"><span data-stu-id="bf541-131">Specifies the server URL.</span></span> <span data-ttu-id="bf541-132">NuGet определяет источник в формате UNC или локальную папку и просто копирует файл вместо отправки с помощью HTTP.</span><span class="sxs-lookup"><span data-stu-id="bf541-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="bf541-133">Кроме того, начиная с NuGet 3.4.2 этот параметр является обязательным, если только `NuGet.Config` в файле не указано значение *дефаултпушсаурце* (см. раздел [Настройка поведения NuGet](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="bf541-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="bf541-134">скипдупликате</span><span class="sxs-lookup"><span data-stu-id="bf541-134">SkipDuplicate</span></span> | <span data-ttu-id="bf541-135">*(5.1 и* более поздние версии) Если пакет и версия уже существуют, пропустите их и продолжайте работу со следующим пакетом в push-уведомлений, если таковые имеются.</span><span class="sxs-lookup"><span data-stu-id="bf541-135">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="bf541-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="bf541-136">SymbolSource</span></span> | <span data-ttu-id="bf541-137">*(3.5 +)* Указывает URL-адрес сервера символов; nuget.smbsrc.net используется при принудительной отправке в nuget.org</span><span class="sxs-lookup"><span data-stu-id="bf541-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="bf541-138">симболапикэй</span><span class="sxs-lookup"><span data-stu-id="bf541-138">SymbolApiKey</span></span> | <span data-ttu-id="bf541-139">*(3.5 +)* Указывает ключ API для URL-адреса, указанного `-SymbolSource`в.</span><span class="sxs-lookup"><span data-stu-id="bf541-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="bf541-140">Время ожидания</span><span class="sxs-lookup"><span data-stu-id="bf541-140">Timeout</span></span> | <span data-ttu-id="bf541-141">Указывает время ожидания в секундах для отправки на сервер.</span><span class="sxs-lookup"><span data-stu-id="bf541-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="bf541-142">Значение по умолчанию — 300 секунд (5 минут).</span><span class="sxs-lookup"><span data-stu-id="bf541-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="bf541-143">Verbosity</span><span class="sxs-lookup"><span data-stu-id="bf541-143">Verbosity</span></span> | <span data-ttu-id="bf541-144">Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*.</span><span class="sxs-lookup"><span data-stu-id="bf541-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="bf541-145">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="bf541-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="bf541-146">Примеры</span><span class="sxs-lookup"><span data-stu-id="bf541-146">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
